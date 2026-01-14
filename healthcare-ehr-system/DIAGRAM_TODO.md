# TODO: Add Architecture Diagram

You need to create `architecture.png` or `architecture.svg` for this case study.

## Option 1: Use This Mermaid Code (Easiest)

Copy this code to https://mermaid.live, then export as PNG or SVG:

```mermaid
graph TB
    subgraph "Application Layer"
        API[REST API Server<br/>Node.js/TypeScript]
        MW[Middleware<br/>Auth + RLS Context]
    end

    subgraph "PostgreSQL Database - 8 Bounded Contexts"
        IDENTITY[(identity schema<br/>patient_phi + RLS<br/>providers, auth)]
        CLINICAL[(clinical schema<br/>encounters<br/>diagnoses, procedures)]
        COMPLIANCE[(compliance schema<br/>legal reviews<br/>regulatory checks)]
        BILLING[(billing schema<br/>claims, contracts<br/>payments)]
        MEDIA[(media schema<br/>documents<br/>recordings)]
        MESSAGING[(messaging schema<br/>notifications)]
        CATALOG[(catalog schema<br/>CPT, ICD-10 codes)]
        REPORTING[(reporting schema<br/>analytics views)]
    end

    subgraph "Event System"
        OUTBOX1[identity.outbox]
        OUTBOX2[clinical.outbox]
        OUTBOX3[compliance.outbox]
        OUTBOX4[billing.outbox]
        CONSUMER[Event Consumer<br/>Background Worker]
    end

    subgraph "External Services"
        S3[AWS S3<br/>Encrypted Storage]
        AI[OpenAI API<br/>Medical Extraction]
    end

    API --> MW
    MW --> IDENTITY
    MW --> CLINICAL
    MW --> COMPLIANCE
    MW --> BILLING
    MW --> MEDIA
    MW --> MESSAGING
    MW --> CATALOG
    MW --> REPORTING

    IDENTITY -.-> OUTBOX1
    CLINICAL -.-> OUTBOX2
    COMPLIANCE -.-> OUTBOX3
    BILLING -.-> OUTBOX4

    CONSUMER --> OUTBOX1
    CONSUMER --> OUTBOX2
    CONSUMER --> OUTBOX3
    CONSUMER --> OUTBOX4

    CONSUMER -.->|propagate events| CLINICAL
    CONSUMER -.->|propagate events| CATALOG
    CONSUMER -.->|propagate events| COMPLIANCE

    MEDIA --> S3
    CLINICAL --> AI

    classDef phi fill:#ff6b6b,stroke:#c92a2a,color:#fff
    classDef outbox fill:#51cf66,stroke:#2f9e44,color:#000
    classDef external fill:#4dabf7,stroke:#1971c2,color:#fff

    class IDENTITY phi
    class OUTBOX1,OUTBOX2,OUTBOX3,OUTBOX4,CONSUMER outbox
    class S3,AI external
```

## Option 2: Draw It Yourself

Create a diagram showing:

**Main Components:**
- Application layer (API server)
- 8 database schemas (boxes)
- Event outbox tables (one per schema)
- Event consumer (background worker)
- External services (S3, AI APIs)

**Key Relationships:**
- API connects to all schemas (solid lines)
- Each schema has its own outbox (dotted lines)
- Event consumer reads outboxes (solid lines)
- Event consumer writes to other schemas (dotted lines)
- Highlight `identity` schema in different color (PHI data)

**Tools:**
- Excalidraw: https://excalidraw.com
- Draw.io: https://app.diagrams.net
- Or screenshot from your actual architecture docs

## Option 3: Simple Boxes and Arrows

Even a hand-drawn diagram (photographed clearly) showing the 8 bounded contexts with event flow is better than nothing!

---

**Once created, save as `architecture.png` or `architecture.svg` in this folder and delete this file.**
