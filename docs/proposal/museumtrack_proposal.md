# MuseumTrack: Museum Collection, Exhibition and Loan Tracker

## Problem Statement

Museums lend artworks to external borrowers and place them in internal exhibitions, yet outgoing loans, exhibition schedules, and conservation work are often tracked in separate spreadsheets. Because these records are disconnected, registrars cannot quickly verify whether an artwork is already promised to a borrower or a gallery, whether it has been inspected recently, or whether it has returned from a previous loan. This fragmentation leads to double booked artworks, missed return dates, and a weak audit trail with no reliable record of who changed what. Although collection information systems are expected to link loan documentation, condition reporting, and object records (Office of the Auditor General, 2006), many small collections still lack such an integrated link. MuseumTrack addresses this gap as an Oracle PL/SQL database that centralizes collection records and enforces scheduling, conservation, and auditing rules automatically.

## Proposed Solution

MuseumTrack is an Oracle 21c database in Third Normal Form, with PL/SQL packages that enforce the booking and conservation rules, and an Oracle APEX web application for staff. A registrar can check artwork availability for a date range, record loans and returns, and monitor overdue loans. A curator can schedule exhibitions, and a conservator records inspections.

Six roles keep these duties separate:
- **Administrator**
- **Chief Registrar**
- **Registrar**
- **Conservator**
- **Curator**
- **Auditor**

## Data Source

The Metropolitan Museum of Art Open Access dataset (`MetObjects.csv`), released under the Creative Commons Zero licence (The Metropolitan Museum of Art, n.d.). The full file has 503,378 records and 54 columns. The project uses a random sample of 1,500 public-domain objects drawn across 15 departments. Its 235 raw classifications will be mapped to eight material families that set maximum loan periods (90 days for light-sensitive materials, 365 days for durable ones). Borrowers, loans, exhibitions and conservation checks are generated as fictional institutions and records, so no real person is identified.

## Planned Tables

Nine tables with surrogate keys:
1. `departments`
2. `classifications` (material family and maximum loan days)
3. `artworks` (keeps the original Met object ID)
4. `exhibitions`
5. `exhibition_artworks` (junction table)
6. `borrowers`
7. `loans`
8. `conservation_checks`
9. `audit_log`

## Planned PL/SQL Features

- **Availability Checks (`is_artwork_available`):** Function `is_artwork_available` blocks any loan or exhibition booking that overlaps in dates, or that targets an artwork on loan, on exhibition, under conservation, missing or deaccessioned.
- **Loan & Return Procedures (`create_loan`, `return_artwork`):** Procedures `create_loan` and `return_artwork` require a `CLEARED` conservation check from the last 180 days, cap the duration by material family, and start a 30-day quarantine after a return.
- **Overdue Monitoring (`flag_overdue_loans`):** A cursor-based procedure `flag_overdue_loans` marks late loans as overdue, and overdue borrowers cannot request new loans.
- **Modular Packages:** Packages `pkg_loan_mgmt`, `pkg_exhibition_mgmt`, and `pkg_conservation`, with custom exceptions raised through `RAISE_APPLICATION_ERROR` in plain English.
- **Triggers & Audit Trail:** Triggers check dates and role separation (registrars cannot approve inspections, conservators cannot approve loans), and write every change to loans and artwork status into an append-only `audit_log` that cannot be edited or deleted.

## Innovation

**User Interface (Oracle APEX):** Six pages—dashboard with overdue monitor, collection and availability check, loans and returns, exhibition scheduler, conservation checks, and audit log—call the PL/SQL packages instead of writing to the tables directly. APEX authorization schemes show each role only its own actions, and an error-handling function turns database errors into readable messages. The business rules stay in PL/SQL, and the application will be demonstrated live.

## References

- The Audit Office. (2006). *Management of heritage collections in local museums and art galleries, Part 5: Managing collection information*. [Performance Audit Report](https://bills.parliament.nz/download/Paper/85ab511c-ebd5-47e3-86db-33e4324e4c8d)
- The Metropolitan Museum of Art. (n.d.). *The Met Open Access CSV* [Data set]. [GitHub Repository](https://github.com/metmuseum/openaccess)
- Gallery Systems. (n.d.). *TMS Collections* [Product page]. Existing system ([Gallery Systems, TMS Collections](https://www.gallerysystems.com/solutions/collections-management/)).
- Oracle. (n.d.). Providing security through authorization. In *Oracle APEX App Builder User's Guide*. [Oracle Help Center](https://docs.oracle.com/en/database/oracle/apex/24.2/htmdb/providing-security-through-authorization.html)
- Vohland, K. (2025). The development of a coherent museum collection database management system: Some reflections on the process. *Curator: The Museum Journal*. Research paper about building a museum collection database system ([DOI: 10.1111/cura.70001](https://doi.org/10.1111/cura.70001)).
- Taylor, J., & Spangler-Bickell, C. (2026). The costs of changing: Factors affecting museum loan specifications and their revision. *Studies in Conservation*, 71(4), 373–388. Research paper about museum loan specifications ([DOI: 10.1080/00393630.2025.2515308](https://doi.org/10.1080/00393630.2025.2515308)).