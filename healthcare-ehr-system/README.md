# HIPAA-Compliant Healthcare EHR Platform

**Domain:** Healthcare Technology
**Challenge:** Build a production-grade EHR system with strict PHI isolation and architectural integrity
**Outcome:** Event-driven architecture passing 11/12 critical compliance rules with 35% cost optimization

---

## Overview

Designed and implemented a HIPAA-compliant Electronic Health Records platform using event-driven architecture with bounded contexts. The system enforces data isolation for Protected Health Information (PHI) through PostgreSQL Row-Level Security and prevents architectural violations through automated auditing.

## Key Achievements

- **Architecture Enforcement:** Automated audit system blocking deployments with schema violations
- **Cost Optimization:** Reduced AWS infrastructure costs by 35-40% ($125/month savings)
- **PHI Compliance:** Zero cross-schema foreign keys, RLS-protected patient data
- **Event-Driven Sync:** Outbox pattern enabling cross-context data flow without coupling

## Technical Highlights

- 8 bounded contexts (identity, clinical, compliance, billing, media, messaging, catalog, reporting)
- PostgreSQL RLS for PHI access control
- Per-schema outbox tables with background event consumer
- AWS ECS/Fargate deployment with RDS PostgreSQL
- Voice transcription → AI medical data extraction pipeline
- Architecture audit automation with CI/CD integration

## System Scale

- Multi-tenant with provider and patient portals
- Production deployment on AWS with high availability
- Automated compliance checking before every deployment
- Real-time voice-to-chart documentation

---

**See [scope.md](./scope.md) for technical architecture details**
**See [results.md](./results.md) for measurable outcomes**
**See [redactions.md](./redactions.md) for what was sanitized from this case study**
