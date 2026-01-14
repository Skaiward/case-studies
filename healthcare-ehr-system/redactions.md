# Redactions & Sanitization

This document explains what information was changed or removed from the original project to create this public case study.

---

## AWS Account Information

**Removed:**
- AWS Account ID
- Specific RDS instance identifiers
- ECR repository URIs
- S3 bucket names
- IAM user ARNs
- CloudWatch log group paths

**Why:** Prevents unauthorized access attempts and security scanning of production infrastructure.

---

## Client & Business Data

**Removed:**
- Client names and organizations
- Specific provider names
- Patient counts and demographics
- Revenue numbers and pricing
- Contract details
- Geographic locations beyond region level

**Sanitized to:**
- Generic "multi-tenant" and "production scale" descriptions
- Percentage-based metrics instead of absolute numbers
- No identifying business information

**Why:** Protects client confidentiality and business sensitive information.

---

## Code & Schema Details

**Changed:**
- Specific database schema implementation details → generic "bounded context" patterns
- Exact table structures → conceptual descriptions
- Proprietary business logic → architectural patterns
- Custom medical entity extraction logic → "AI-powered extraction"

**Kept:**
- Architectural patterns (outbox, RLS, event-driven)
- Technology stack (PostgreSQL, ECS, RDS)
- General schema organization (8 bounded contexts)
- Audit rules and enforcement mechanisms

**Why:** Shares architectural knowledge without exposing proprietary implementation.

---

## Infrastructure Details

**Removed:**
- Specific VPC IDs and subnet configurations
- Security group rules and port numbers
- Exact IAM policies and permissions
- API endpoint URLs
- Database connection strings
- Secrets Manager secret names

**Generalized:**
- "AWS ECS/Fargate deployment" instead of exact task definitions
- "RDS PostgreSQL" instead of specific instance types and configurations
- "Encrypted S3 storage" instead of bucket policies

**Why:** Prevents infrastructure reconnaissance and maintains security posture.

---

## API & Integration Details

**Removed:**
- Specific AI/ML model versions and parameters
- API keys and authentication tokens
- Third-party service configurations
- Webhook URLs and callback endpoints

**Generalized:**
- "OpenAI API" instead of specific model and prompting strategies
- "Speech-to-text API" instead of vendor and configuration
- "Event consumer" instead of specific queue implementation

**Why:** Protects proprietary configurations and third-party relationships.

---

## Metrics & Analytics

**Changed:**
- Exact user counts → "multi-tenant production system"
- Specific cost numbers → percentage reductions
- Precise performance metrics → general performance characteristics
- Exact IOPS and throughput → before/after comparisons

**Example:**
- Before: "$272.45/month → $147.82/month"
- After: "35-40% cost reduction ($125/month savings)"

**Why:** Shares meaningful outcomes without revealing exact business scale.

---

## Timeline & Dates

**Changed:**
- Specific project start/end dates → relative timeframes
- Exact deployment dates → "production-ready" status
- Client milestones → general implementation phases

**Kept:**
- Recent optimization dates (October 2025) for context on modern approaches
- Relative timeframes for understanding project scope

**Why:** Prevents correlation with business events or client contracts.

---

## What Remains Authentic

Despite redactions, this case study accurately represents:

✅ **Real architectural patterns used in production**
- Event-driven bounded contexts with outbox pattern
- PostgreSQL RLS for PHI compliance
- Automated architecture auditing

✅ **Actual technical challenges solved**
- Cross-schema data sync without coupling
- HIPAA compliance enforcement
- Infrastructure cost optimization

✅ **Genuine measurable outcomes**
- 35-40% cost reduction (real percentage, sanitized amounts)
- 11/12 architectural rules passing (real metric)
- Zero cross-schema violations (verified via audit)

✅ **Production-proven technology choices**
- AWS ECS/Fargate, RDS PostgreSQL
- Node.js/TypeScript backend
- CloudWatch monitoring, SNS alerting

---

## Verification

While client names and specific metrics are redacted, the architectural patterns, technical approaches, and percentage-based outcomes are genuine and reflect production systems shipped to real healthcare organizations.

**Code samples and architectural decisions in this case study can be validated through:**
- Discussion of event-driven architecture patterns
- PostgreSQL RLS and schema isolation techniques
- AWS cost optimization strategies
- Architecture audit automation approaches

**This case study demonstrates real-world system design experience without compromising client confidentiality or security.**
