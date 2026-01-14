# Technical Scope

## Architecture Pattern: OCR-Driven Document Processing

### Problem Statement
Traffic attorneys process hundreds of citations monthly. Manual ticket entry is time-consuming and error-prone. Clients expect instant responses, but ticket details must be accurately captured. Marketing requires jurisdiction-specific content for local SEO.

### Solution Design

**Ticket Processing Pipeline:**
1. **Upload:** Client uploads ticket photo (mobile camera or PDF scan)
2. **OCR Processing:** Azure Form Recognizer extracts text and fields
3. **Entity Extraction:** Parse ticket number, violation code, court, date, amount
4. **Violation Matching:** Map extracted code to violation database
5. **Defense Generation:** Suggest applicable defense strategies
6. **Admin Review:** Attorney dashboard for case management
7. **Payment:** Stripe integration for consultation/retainer booking

### Core Technical Components

#### 1. Azure OCR Integration

**Form Recognizer Implementation:**
- Custom model trained on Florida traffic ticket layouts
- Key-value pair extraction (ticket number, violation, date, etc.)
- Confidence scoring for each extracted field
- Fallback to general OCR for non-standard tickets

**Extracted Fields:**
- Ticket/citation number
- Violation code (e.g., 316.183, 316.074)
- Court name and location
- Court date and time
- Defendant name
- Fine amount
- Issuing officer
- Location of violation

**Quality Assurance:**
- Confidence threshold validation
- Manual review queue for low-confidence extractions
- Field-level validation rules (date formats, amount ranges)
- Duplicate ticket detection

#### 2. Violation Database & Matching

**Violation Repository:**
- Miami-Dade County violation codes
- Florida Statute references
- Point system impact (0-6 points)
- Fine ranges by violation type
- License suspension thresholds

**Matching Logic:**
- Exact violation code match
- Fuzzy matching for OCR errors
- Statute citation parsing
- Violation type categorization (moving vs. non-moving)

**Defense Strategy Templates:**
- Speeding: Radar calibration, officer training, speed survey
- Red light: Amber time calculation, intersection engineering
- Stop sign: Visibility, obstruction, signage compliance
- Lane violations: Necessity, emergency circumstances
- Equipment violations: Pre-stop corrections

#### 3. SEO Content System

**Dynamic Page Generation:**
- Violation-specific pages (e.g., `/violations/speeding-florida`)
- Location-specific pages (e.g., `/locations/miami-traffic-lawyer`)
- Combined pages (e.g., `/violations/red-light-miami`)

**SEO Optimization:**
- Primary keyword in H1 and first 100 words
- Secondary keywords in subheadings
- Meta titles 55-60 characters
- Meta descriptions 150-160 characters
- FAQ schema for featured snippets
- Canonical URLs for duplicate content
- Internal linking structure

**Content Structure:**
- Overview of violation/location
- Legal implications and point system
- Defense strategies available
- Court information and procedures
- FAQ section (5+ questions)
- Strong CTA (upload ticket, free evaluation)

**Example Keyword Targeting:**
- Primary: "Miami traffic lawyer speeding"
- Secondary: "fight speeding ticket Miami", "Miami-Dade traffic court"
- Long-tail: "speeding ticket lawyer Coral Gables", "reduce points Florida"

#### 4. Admin Dashboard

**Authentication:**
- Supabase Auth for user management
- Email/password login
- Role-based access control (admin vs. attorney vs. staff)
- Session management with automatic logout

**Case Management:**
- View all submitted tickets
- Filter by status (new, in review, retained, closed)
- Sort by date, violation type, court date
- Search by client name, ticket number
- Bulk actions (assign attorney, update status)

**Client Portal Features:**
- View ticket details and OCR results
- Upload additional documents
- Communication history
- Payment status and invoices
- Court date reminders

**Analytics Dashboard:**
- Ticket submission volume by violation type
- Conversion rates (submission → consultation → retention)
- Revenue by violation category
- Average case duration
- Court success rates

#### 5. Payment Processing

**Stripe Integration:**
- Consultation fee booking
- Retainer payment processing
- Subscription plans (monthly, per-ticket)
- Invoice generation
- Receipt email automation

**Payment Workflows:**
- Freemium: Free ticket upload + analysis
- Consultation: $X booking fee
- Retainer: $Y upfront payment
- Subscription: Monthly plan for volume clients

**Financial Tracking:**
- Payment status per case
- Revenue reporting
- Refund management
- Tax documentation

### Technical Implementation

**Frontend:**
- Next.js 15 with App Router
- TypeScript for type safety
- Tailwind CSS for responsive design
- Hero UI component library
- Mobile-first design (60%+ mobile traffic)
- Camera API for mobile ticket photos

**Backend:**
- Next.js API routes
- Supabase for database and auth
- Server-side rendering for SEO pages
- Edge functions for performance
- Rate limiting for API protection

**Third-Party Services:**
- Azure Form Recognizer (OCR)
- Azure Blob Storage (document storage)
- Stripe (payment processing)
- Supabase (database, auth, storage)
- PostHog (analytics)
- Resend or SendGrid (email)

**Database Schema:**
- Users (attorneys, staff, clients)
- Citations (uploaded tickets with OCR data)
- Violations (violation code database)
- Cases (client matters)
- Payments (Stripe transactions)
- Analytics events (PostHog integration)

### SEO & Marketing Features

**100+ Optimized Pages:**
- 50+ violation types (speeding, red light, DUI, license violations, etc.)
- 30+ Miami-Dade locations (Miami, Coral Gables, Kendall, Hialeah, etc.)
- 20+ combination pages (violation × location)

**Technical SEO:**
- Server-side rendering for instant indexing
- Absolute canonical URLs
- Structured data (LocalBusiness, FAQPage)
- Image optimization with Next.js Image
- Mobile responsiveness
- Core Web Vitals optimization

**Content Strategy:**
- Informational intent (what is X violation)
- Commercial intent (fight X ticket)
- Transactional intent (hire lawyer for X)
- Local intent (X lawyer near me)

### Compliance & Legal

**Data Protection:**
- HTTPS enforcement
- Encrypted document storage (Azure Blob)
- PII protection in database
- Secure payment processing (PCI compliance via Stripe)
- GDPR cookie consent

**Attorney Ethics:**
- No guarantee of outcomes
- Clear fee disclosures
- Attorney-client relationship disclaimers
- Jurisdiction limitations (Florida-licensed attorneys only)

**Terms of Service:**
- Platform usage terms
- Payment and refund policies
- Data retention policies
- Limitation of liability

### Key Features by User Type

**Clients:**
- Upload ticket via mobile camera or PDF
- View OCR-extracted ticket details
- Receive violation analysis and defense options
- Book consultation with Stripe payment
- Track case status in portal

**Attorneys:**
- Review new ticket submissions
- Approve/edit OCR extraction
- Assign cases to self or staff
- Manage client communication
- Track court dates and deadlines
- Generate invoices and receipts

**Admins:**
- Manage attorney accounts
- View platform analytics
- Configure violation database
- Update SEO content
- Monitor payment processing
- Export data for reporting

---

## Technology Stack

- **Frontend:** Next.js 15, React 18, TypeScript, Tailwind CSS, Hero UI
- **Backend:** Next.js API routes, Edge functions
- **Database:** Supabase (PostgreSQL)
- **Authentication:** Supabase Auth (JWT)
- **OCR:** Azure Form Recognizer
- **Storage:** Azure Blob Storage, Supabase Storage
- **Payment:** Stripe
- **Analytics:** PostHog, Google Analytics
- **Email:** Resend or SendGrid
- **Hosting:** Vercel (frontend), Supabase (backend/DB)
- **Monitoring:** Vercel Analytics, Sentry (error tracking)
