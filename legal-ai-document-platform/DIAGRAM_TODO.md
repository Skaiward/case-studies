# TODO: Add Architecture Diagram

You need to create `architecture.svg` or `architecture.png` for this case study.

## Option 1: Use This Mermaid Code (Easiest)

Copy this code to https://mermaid.live, then export as PNG or SVG:

```mermaid
graph LR
    subgraph "User Interface"
        UPLOAD[Document Upload<br/>Eviction Notice<br/>Termination Letter]
        QUEST[Smart Questionnaire<br/>Dynamic Q&A]
        PREVIEW[Document Preview<br/>Edit & Review]
        EXPORT[Export<br/>PDF/DOCX]
    end

    subgraph "AI Processing"
        OCR[OCR<br/>Text Extraction]
        ENTITY[Entity Recognition<br/>Names, Dates, Amounts]
        CLASSIFY[Issue Classification<br/>Legal Problem Type]
        AI[OpenAI GPT-4<br/>Analysis & Extraction]
    end

    subgraph "Document Generation"
        TEMPLATE[Template Engine<br/>Court-Compliant Formats]
        CITATION[Citation System<br/>Statutes & Case Law]
        FORMAT[Formatting<br/>Times New Roman 12pt]
    end

    subgraph "Supporting Systems"
        DEADLINE[Deadline Tracker<br/>Alert System]
        SETTLEMENT[Settlement Calculator<br/>Damage Estimation]
        EVIDENCE[Evidence Manager<br/>Photo Upload]
        DB[(Database<br/>Cases & Documents)]
    end

    UPLOAD --> OCR
    OCR --> AI
    AI --> ENTITY
    AI --> CLASSIFY
    ENTITY --> QUEST
    CLASSIFY --> QUEST
    QUEST --> TEMPLATE
    TEMPLATE --> CITATION
    CITATION --> FORMAT
    FORMAT --> PREVIEW
    PREVIEW --> EXPORT

    CLASSIFY --> DEADLINE
    ENTITY --> DEADLINE
    QUEST --> SETTLEMENT
    QUEST --> EVIDENCE
    QUEST --> DB
    TEMPLATE --> DB

    classDef ai fill:#4dabf7,stroke:#1971c2,color:#fff
    classDef ui fill:#51cf66,stroke:#2f9e44,color:#000
    classDef doc fill:#ff6b6b,stroke:#c92a2a,color:#fff
    classDef support fill:#ffd43b,stroke:#f59f00,color:#000

    class OCR,ENTITY,CLASSIFY,AI ai
    class UPLOAD,QUEST,PREVIEW,EXPORT ui
    class TEMPLATE,CITATION,FORMAT doc
    class DEADLINE,SETTLEMENT,EVIDENCE,DB support
```

## Option 2: Flow Diagram

Create a diagram showing the document processing flow:

**Step 1: Document Upload**
- User uploads eviction notice or termination letter
- System detects document type

**Step 2: AI Analysis**
- OCR extracts text
- AI identifies entities (names, dates, amounts)
- System classifies legal issues

**Step 3: Smart Questionnaire**
- Dynamic questions based on detected issues
- User provides additional context
- System validates responses

**Step 4: Document Generation**
- Template selected based on issue type
- Auto-populate from extracted data + user answers
- Apply court formatting (font, spacing, citations)

**Step 5: Review & Export**
- User reviews generated document
- Make edits if needed
- Export as PDF or DOCX

**Tools:**
- Excalidraw: https://excalidraw.com
- Draw.io: https://app.diagrams.net
- Lucidchart (if you have access)

## Option 3: System Architecture Diagram

Show the main components:
- Frontend (Next.js)
- API Server (Node.js)
- AI Integration (OpenAI)
- Database (PostgreSQL)
- File Storage
- Background Jobs (document processing queue)
- Email/SMS alerts

## Option 4: Use Screenshots

If you have screenshots from OpenCourt showing:
- Document upload screen
- AI extraction results
- Generated document preview

Combine them into a single flow image showing the process.

---

**Once created, save as `architecture.svg` or `architecture.png` in this folder and delete this file.**
