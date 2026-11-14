# cyusa_29844_museumTrack
# MuseumTrack: Museum Collection, Exhibition and Loan Tracker

**Student:** Cyusa Bruno | **ID:** 29844
**Course:** INSY 8311 Database Development with PL/SQL | **Instructor:** Eric Maniraguha
**University:** Adventist University of Central Africa (AUCA)

## Problem Statement
Museums lend artworks to other institutions and place them in exhibitions, but loans, conservation work and return dates are often tracked in separate spreadsheets. This leads to double-booked artworks, missed return dates and no reliable record of who changed what. MuseumTrack is an Oracle PL/SQL database that enforces these rules automatically.

## Objectives
**Main objective:** Build an Oracle PL/SQL database that manages a museum's collection, exhibitions and loans and prevents conflicting bookings.

**Specific objectives:**
1. Load a real museum collection dataset into a normalized (3NF) schema.
2. Block loans or exhibition bookings for artworks that are unavailable (already on loan or under conservation).
3. Calculate loan durations and flag overdue returns automatically.
4. Record every loan change in an audit log.
5. Provide an Oracle APEX interface for registrars that calls the PL/SQL procedures.

## Data Source
The Metropolitan Museum of Art Open Access dataset (CSV, UTF-8, CC0 licence).
https://github.com/metmuseum/openaccess
A subset of the collection records will be loaded. Loan, exhibition and conservation records are generated on top of the real collection data.

## Innovation
**Option:** User interface. **Tool:** Oracle APEX. A registrar records a loan or return in the app, and the app calls the PL/SQL procedures. Business rules stay in PL/SQL.

## Planned Tables
departments, classifications, artworks, exhibitions, exhibition_artworks, borrowers, loans, conservation_checks, audit_log

## Planned PL/SQL Features
- **Trigger:** blocks a loan or exhibition booking for an unavailable artwork.
- **Procedure `create_loan`:** validates dates and creates the loan.
- **Function `loan_days`:** calculates loan length and overdue days.
- **Cursor:** lists loans due back in the next 30 days.
- **Package:** groups the loan and exhibition logic.
- **Exceptions:** custom errors such as `artwork_unavailable`.
- **Audit trigger:** logs every loan change and denies edits outside working hours.

## References
(To be added after the research log is complete.)
