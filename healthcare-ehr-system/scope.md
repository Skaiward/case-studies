# Technical Scope

## Architecture Pattern: Event-Driven Bounded Contexts

### Problem Statement
Healthcare systems require strict data isolation for PHI compliance while enabling cross-functional features (billing, compliance, reporting). Traditional monolithic databases create tight coupling and regulatory risk.

### Solution Design

**Bounded Context Isolation:**
- 8 isolated PostgreSQL schemas, each owning its domain
- No cross-schema foreign keys (enforced via automated audit)
- Each context has independent data model and access patterns

**Event-Driven Synchronization:**
- Per-schema `outbox` tables for cross-context events
- Background consumer polls outboxes, propagates events
- Guarantees eventual consistency without coupling
- Idempotent event handlers prevent duplicate processing

**PHI Protection:**
- All PHI isolated in `identity.patient_phi` table
- PostgreSQL Row-Level Security (RLS) policies enforce access
- Session variables (`set_current_user`) control data visibility
- Middleware sets/clears context on every request

### Core Technical Components

#### 1. Database Architecture
```
identity schema      → Patient PHI, providers, authentication
clinical schema      → Encounters, diagnoses, procedures
compliance schema    → Legal reviews, regulatory checks
billing schema       → Claims, contracts, payments
media schema         → Documents, images, recordings
messaging schema     → Notifications, communications
catalog schema       → CPT codes, ICD-10, medications
reporting schema     → Analytics views, dashboards
```

#### 2. Event System
Each schema includes:
- `outbox` table with columns: `id`, `aggregate_id`, `aggregate_type`, `event_type`, `payload`, `created_at`, `processed_at`, `status`
- Events written transactionally with domain changes
- Consumer marks events processed, triggers handlers in other contexts

#### 3. Voice Documentation Pipeline
- Audio upload → S3 encrypted storage
- Transcription via speech-to-text API
- AI extraction of medical entities (symptoms, diagnoses, medications)
- Structured data inserted into clinical schema

#### 4. Architecture Audit System
Automated script validates:
- No cross-schema foreign keys
- All timestamps use `timestamptz` (timezone-aware)
- Status columns use proper enums
- No cross-schema writes in application code
- PHI tables have RLS enabled with active policies
- Outbox tables have required columns

Audit runs in CI/CD pipeline, blocks deployment on violations.

### Infrastructure

**Deployment:**
- AWS ECS Fargate (serverless containers)
- Application Load Balancer for traffic routing
- RDS PostgreSQL (Multi-AZ for production)
- S3 for encrypted file storage
- CloudWatch for logs and monitoring

**Environments:**
- Production: 2 ECS tasks (high availability), db.t3.medium RDS
- Development: 1 ECS task, db.t4g.micro RDS

**Cost Optimization Techniques:**
- Reduced dev service from 2 → 1 tasks
- Switched dev database from io2 → gp3 storage
- Set CloudWatch log retention policies
- Deregistered unused task definitions

### Security & Compliance

**HIPAA Controls:**
- Encryption at rest (S3, RDS)
- Encryption in transit (TLS)
- RLS policies on PHI tables
- Audit logging of all data access
- Session-based user context

**Access Control:**
- JWT authentication
- Role-based permissions (admin, provider, patient)
- Middleware sets PostgreSQL session variables for RLS
- API rate limiting via rate limit tables

### Key Architectural Rules

1. **No cross-schema foreign keys** - Prevents coupling, enforced via audit
2. **Outbox pattern only for cross-context sync** - Maintains loose coupling
3. **PHI only in identity schema** - Single boundary for compliance
4. **RLS enforced on PHI tables** - Row-level data access control
5. **Architecture audit blocks bad deployments** - Prevents regressions

---

## Technology Stack

- **Backend:** Node.js with TypeScript
- **Database:** PostgreSQL 14+ with schemas and RLS
- **Infrastructure:** AWS ECS/Fargate, RDS, S3, ALB
- **AI/ML:** OpenAI API for medical data extraction
- **Monitoring:** CloudWatch, SNS for alerts
- **CI/CD:** GitHub Actions with architecture audit gate
