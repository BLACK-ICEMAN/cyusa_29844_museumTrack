# Research Log: MuseumTrack

## 1. Source Matrix

| # | Source (APA 7th) | Type | Link | Key finding | Gap it shows |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | The Audit Office. (2005/06). *Management of heritage collections in local museums and art galleries, Part 5: Managing collection information*. Office of the Auditor-General New Zealand. | Report | https://ao.parliament.nz/2006/heritage/part5.htm | Examines how local museums and art galleries record, maintain, and govern information about their collections. | Reviews collection record-keeping at a policy and audit level; it does not provide a relational database that enforces loan, exhibition, and conservation rules. |
| 2 | The Metropolitan Museum of Art. (n.d.). *The Met Open Access CSV* [Data set]. GitHub. | Dataset | https://github.com/metmuseum/openaccess | Public-domain (CC0) dataset listing over 470,000 artworks on GitHub (503,378 rows in the downloaded file), without images and with incomplete metadata in several fields. | Contains artwork catalog rows only—no borrowers, loans, exhibitions, or conservation checks—so operational tables and test records are generated for MuseumTrack. |
| 3 | Gallery Systems. (n.d.). *TMS Collections* [Product page]. | Existing system | https://www.gallerysystems.com/products-tms-suite/tms-collections/ | Commercial collections management software connecting cataloguing, exhibitions, incoming/outgoing loans, conservation, and reporting with configurable workflows and concurrent-user licensing. | The product page does not say that it blocks overlapping bookings, applies material-based duration caps, or enforces a post-loan quarantine. MuseumTrack states these rules explicitly in PL/SQL. |
| 4 | Oracle. (n.d.). Providing security through authorization. In *Oracle APEX App Builder User's Guide*. | Technical documentation | https://docs.oracle.com/en/database/oracle/apex/24.1/htmdb/creating-an-authorization-scheme.html | APEX authorization schemes restrict access to applications, pages, and UI components using PL/SQL boolean functions evaluated once per session by default. | UI authorization only controls what appears on screen; MuseumTrack repeats role checks inside its PL/SQL packages so business rules cannot be bypassed outside the interface. |
| 5 | Vohland, K. (2026). The development of a coherent museum collection database management system: Some reflections on the process. *Curator: The Museum Journal*, *69*(1), 122–128. | Research paper | https://doi.org/10.1111/cura.70001 | Describes how a large natural history museum designed a modular collection database system, starting from a review of existing departmental databases and a build-versus-adapt decision. | Focuses on general collection database architecture and organizational lessons; it does not address booking conflict prevention, pre-loan conservation gates, or an immutable change audit trail. |
| 6 | Taylor, J., & Spangler-Bickell, C. (2026). The costs of changing: Factors affecting museum loan specifications and their revision. *Studies in Conservation*, *71*(4), 373–388. | Research paper | https://doi.org/10.1080/00393630.2025.2515308 | Draws on interviews with registrars and conservation, exhibitions, and insurance staff to show that loan specifications cut across multiple departments and are difficult and costly to revise. | Examines how staff negotiate and revise loan conditions rather than providing database-enforced rules such as separate registrar and conservator sign-offs or automated revision logging. |

---

## 2. References (APA 7th Edition)

The Audit Office. (2005/06). *Management of heritage collections in local museums and art galleries, Part 5: Managing collection information*. Office of the Auditor-General New Zealand. https://ao.parliament.nz/2006/heritage/part5.htm

Gallery Systems. (n.d.). *TMS Collections* [Product page]. https://www.gallerysystems.com/products-tms-suite/tms-collections/

The Metropolitan Museum of Art. (n.d.). *The Met Open Access CSV* [Data set]. GitHub. https://github.com/metmuseum/openaccess

Oracle. (n.d.). Providing security through authorization. In *Oracle APEX App Builder User's Guide*. https://docs.oracle.com/en/database/oracle/apex/24.1/htmdb/creating-an-authorization-scheme.html

Taylor, J., & Spangler-Bickell, C. (2026). The costs of changing: Factors affecting museum loan specifications and their revision. *Studies in Conservation*, *71*(4), 373–388. https://doi.org/10.1080/00393630.2025.2515308

Vohland, K. (2026). The development of a coherent museum collection database management system: Some reflections on the process. *Curator: The Museum Journal*, *69*(1), 122–128. https://doi.org/10.1111/cura.70001

---
**Name:** Cyusa Bruno   
**ID:** 29844   
**Group:** D 
