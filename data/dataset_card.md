# Dataset card: MuseumTrack

## 1. Source
| Item | Value |
|---|---|
| Name | The Metropolitan Museum of Art Open Access dataset, `MetObjects.csv` |
| Source link | https://github.com/metmuseum/openaccess |
| Licence | Creative Commons Zero (CC0): free to use, including for education |
| Format | CSV, UTF-8, comma-separated, 54 columns |
| Full file | 503,378 records (about 334 MB) |
| Date collected | November 2026 (sample drawn 23 Nov 2026) |
| Raw file used | `data/raw/MetObjects_sample_1500.csv`: 1,500 records, 927,855 bytes |

**What one record represents:** one object in the Met's collection (identified by `Object ID`).

The full file is too large for GitHub (100 MB limit), so the repository holds a random sample.
The sample rows and values are copied from the download **unchanged**; no value was edited.

**How the sample was drawn (repeatable):**
1. Keep rows where `Is Public Domain` = TRUE and `Title`, `Classification` and `Medium` are not blank.
2. Keep rows with a single classification (no `|` list).
3. Take up to 90 random rows per department (random seed 29844), then fill to 1,500 at random.

Result: 1,500 records, 15 departments, 235 distinct classifications.

## 2. Personal data
The dataset describes artworks, not private people. `Artist Display Name` (618 filled records) and
the artist biography columns name historical or public artists, as published by the Met under CC0.
No phone numbers, ID numbers or private individuals appear. Borrowers, loans, exhibitions and
conservation checks are **generated** as fictional institutions and records.

## 3. Data quality report (counts on the 1,500-row sample; nothing fixed yet)
| Check | Count |
|---|---|
| Duplicate full rows | 0 |
| Duplicate `Object ID` | 0 |
| Duplicate `Object Number` | 0 |
| Blank `Object Date` | 47 |
| `Object Date` that is not a plain 4-digit year (e.g. "ca. 1865", "early 19th century") | 1,329 |
| Blank `AccessionYear` | 7 |
| Blank `Object Name` | 1 |
| Blank `Dimensions` | 98 |
| Blank `Culture` | 552 |
| Blank `Period` | 1,199 |
| Blank `Artist Display Name` | 882 |
| Blank `Tags` | 751 |
| `Object Begin Date` negative (BCE years) | 216 |
| `Object Begin Date` later than `Object End Date` | 0 |
| Non-numeric `Object Begin Date` / `Object End Date` | 0 / 0 |
| `Artist Display Name` holding several artists joined by `\|` | 176 |
| Cells with leading or trailing spaces | 2,104 |
| Distinct `Classification` values (to group into 8 material families) | 235 |
| Longest `Title` / `Medium` / `Credit Line` (characters) | 421 / 362 / 263 |
| Records with `Is Public Domain` = TRUE | 1,500 |

**Problems to handle in Phase IV (cleaning checklist):**
- Text dates in `Object Date` stay as text; use `Object Begin Date` and `Object End Date` as numbers.
- Convert `AccessionYear` text to NUMBER and blanks to NULL.
- Trim spaces in the 2,104 affected cells.
- Map 235 classifications to 8 material families (`material_family`, `max_loan_days`).
- Split or shorten multi-artist and over-long text values to fit column sizes.

## 4. Generated data (not from the Met)
| Table | Approximate rows | Notes |
|---|---|---|
| `borrowers` | about 30 | Fictional institutions |
| `exhibitions` | about 15 | Fictional titles and dates |
| `loans` | about 200 | Includes completed and overdue history |
| `conservation_checks` | about 1,500+ | Baseline checks seeded for the sample artworks |
