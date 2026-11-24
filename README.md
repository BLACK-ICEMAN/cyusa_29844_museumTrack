# MuseumTrack: Museum Collection, Exhibition and Loan Tracker

**MuseumTrack** is an Oracle PL/SQL and Oracle APEX database application that replaces fragmented museum spreadsheets with automated, database-enforced rules for managing artwork collections, internal exhibitions, outward loans, and conservation clearances.

## Overview

Museums lending artworks to external institutions or scheduling them for internal galleries risk double-booking pieces, missing return deadlines, lending fragile works without valid condition checks, and losing track of record modifications. MuseumTrack enforces these rules directly at the database layer using stored PL/SQL packages, triggers, and custom exceptions across a normalized (3NF) nine-table schema, paired with a role-segmented Oracle APEX interface.

## 🚀 Key Database Features & Business Rules

1. **Mandatory Pre-Loan Conservation Clearance:** Blocks loans or exhibition bookings unless an artwork has a `'CLEARED'` status recorded in `conservation_checks` within the last 180 days.
2. **30-Day Post-Loan Recovery Quarantine:** Enforces a mandatory 30-day quarantine period after actual return before an artwork can be re-loaned or displayed.
3. **Fragility-Based Duration Caps:** Automatically caps loan/display durations based on material sensitivity (e.g., textiles/paper capped at 90 days; stone/bronze up to 365 days).
4. **Loan Cap & Single Renewal Rule:** Limits standard loans to 365 days and restricts active loans to a maximum of one renewal.
5. **Overdue Borrower Freeze:** Automatically blocks institutions holding overdue loans or lacking verified facility accreditation.
6. **Chronological & Exhibition Window Integrity:** Prevents backdated loan creation, checks cross-channel booking conflicts, and ensures artwork display dates fall strictly within parent exhibition dates.
7. **Role-Based Separation of Duties:** Enforces 6 distinct user roles (`ROLE_ADMIN`, `ROLE_CHIEF_REGISTRAR`, `ROLE_REGISTRAR`, `ROLE_CONSERVATOR`, `ROLE_CURATOR`, `ROLE_AUDITOR`) via Oracle APEX Authorization Schemes.
8. **Tamper-Evident APEX Audit Trail:** Captures `COALESCE(SYS_CONTEXT('APEX$SESSION', 'APP_USER'), USER)` on data updates/deletes in `audit_log`, enforced by an append-only trigger blocking log tampering.


### Database Schema (3NF)
`departments` · `classifications` · `artworks` · `exhibitions` · `exhibition_artworks` · `borrowers` · `loans` · `conservation_checks` · `audit_log`

## 🛠 Tech Stack & Environment

* **Database Engine:** Oracle Database 21c Enterprise Edition Release 21.0.0.0.0 (Version 21.3.0.0.0)
* **Backend Logic:** Oracle PL/SQL (Packages, Stored Procedures, Functions, Triggers, Cursors)
* **Application Frontend:** Oracle APEX 23.2 (Universal Theme, Interactive Grids, Authorization Schemes)
* **Data Source:** The Metropolitan Museum of Art Open Access Dataset (`MetObjects.csv`, CC0 License)


## 📂 Repository Directory Structure

```text
cyusa_29844_museumTrack/
├── README.md                          # Main repository overview and setup documentation
├── data/
│   ├── raw/                           # Raw dataset storage (MetObjects.csv)
│   └── dataset_card.md                # Open access dataset metadata and quality card
├── docs/
│   ├── research/
│   │   └── research_log.md            # APA research log (6 credible academic/industry sources)
│   ├── proposal/
│   │   └── museumtrack_proposal.md    # Formal 2-page project proposal
│   ├── presentation/
│   │   └── museumtrack_presentation.md # 12-slide capstone presentation deck
│   └── business_process/              # Phase I BPMN workflow diagrams and explanation
├── database/                          # Oracle Database setup scripts (Phases III - VI)
│   ├── setup/
│   ├── ddl/
│   ├── dml/
│   ├── plsql/
│   └── tests/
└── screenshots/                       # Verification evidence and execution screenshots
```




