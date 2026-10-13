# Citation Verification Tools

## Layers and Boundaries

For online publication metadata, prefer the optional [Bibverify CLI](bibverify-integration.md), pinned to 0.5.0 in a separate Python 3.11+ environment. If it is unavailable or incompatible, use the built-in metadata script below. Commands, statuses, and exit codes in this guide refer to the built-in tools, not Bibverify.

The tools produce reports without modifying `.bib`, `.tex`, or citation keys. All three entry points share `scripts/citation_common.py`.

| Entry point | Purpose | Network |
| --- | --- | --- |
| `scripts/audit_bibtex.py` | Parse BibTeX; check duplicate keys/DOIs/titles, required fields, author truncation, years, DOI syntax, page separators, and undefined AUX citations | Never |
| `scripts/verify_metadata.py` | Fallback metadata backend; DOI-first comparison of titles, authors, years, volume/issue, pages/article numbers, and venues; DataCite fallback; optional title candidate search | Explicit `--online`, or offline `--cache-only` |
| `scripts/check_updates.py` | Find retractions, corrections, expressions of concern, and other notices pointing to the cited DOI; retain notice DOI, type, and source | Explicit `--online`, or offline `--cache-only` |

The scripts do not determine whether a source supports a manuscript claim, provide JCR quartiles, or equate a DOI hit with authenticity. Continue with the [claim-support workflow](integrity-review.md).

No reference-count threshold is enforced by default because manuscript budgets vary. Pass `--min-count` when needed. The scripts do not infer journal quartiles or research quality from abbreviations.

## Installation and Local Tests

Python 3.10+ is required. BibTeX is parsed with `bibtexparser`, and LaTeX prose with `pylatexenc`; regular expressions do not replace BibTeX parsing.

Run these commands from the suite root using PowerShell 7 on Windows:

```powershell
$ErrorActionPreference = 'Stop'
python -m venv .venv
if ($LASTEXITCODE -ne 0) { throw 'Virtual environment creation failed.' }
& ./.venv/Scripts/python.exe -m pip install -r ./subskills/citation/scripts/requirements.txt
if ($LASTEXITCODE -ne 0) { throw 'Dependency installation failed.' }
& ./.venv/Scripts/python.exe -X utf8 -m unittest discover -s ./subskills/citation/tests -v
if ($LASTEXITCODE -ne 0) { throw 'Tests failed.' }
```

On other systems, use the corresponding interpreter and virtual-environment executable paths.

## Offline Audit

```powershell
$ErrorActionPreference = 'Stop'
& ./.venv/Scripts/python.exe -X utf8 ./subskills/citation/scripts/audit_bibtex.py 'C:/paper/ref.bib' --aux 'C:/paper/main.aux' --out-dir './reports/offline-01'
if ($LASTEXITCODE -eq 2) { throw 'Audit incomplete; inspect the diagnostic output.' }
```

Omit `--aux` to inspect the whole bibliography. With AUX, inspect entries selected by the compiled manuscript, excluding BibTeX control entries from the bibliography count. Duplicate keys are still checked across the whole input. AUX must belong to the current manuscript. The tool does not compile LaTeX or infer active sections from a superficial `.tex` scan. It supports `\citation`, `\abx@aux@cite`, `\abx@aux@nocite`, and child AUX files; child files cannot escape the root AUX directory.

## Publication Metadata

```powershell
$ErrorActionPreference = 'Stop'
& ./.venv/Scripts/python.exe -X utf8 ./subskills/citation/scripts/verify_metadata.py 'C:/paper/ref.bib' --aux 'C:/paper/main.aux' --online --cache-dir './reports/cache' --out-dir './reports/metadata-01'
if ($LASTEXITCODE -eq 2) { throw 'Network or processing failure; inspect the report.' }
```

Entries without a DOI default to `NO_DOI`. `--search-titles` sends titles to Crossref and returns candidates, not confirmed matches. Title similarity explains differences; it does not automatically overwrite source data. Use `--limit 2` for a smoke test; the report explicitly records partial coverage.

## Retractions and Corrections

```powershell
$ErrorActionPreference = 'Stop'
& ./.venv/Scripts/python.exe -X utf8 ./subskills/citation/scripts/check_updates.py 'C:/paper/ref.bib' --aux 'C:/paper/main.aux' --online --cache-dir './reports/cache' --out-dir './reports/updates-01'
if ($LASTEXITCODE -eq 2) { throw 'Publication-update check incomplete.' }
```

Query Crossref `updates:DOI` and verify that each notice's `update-to` points to the target DOI. The notice and affected paper are distinct records; never reverse the relationship. Ask the author to read any notice found rather than automatically deleting citations. Read at most 100 notices per DOI; results beyond that limit are `PARTIAL`. No notice means `NO_UPDATE_FOUND`, not a guarantee that the paper was never retracted.

## Output, Privacy, and Status

The Markdown header displays mode, whole-library or AUX selection, bibliography size, processed/selected counts, coverage, processing completion, and status counts. `--limit` truncation is `PARTIAL`. Source failures or unread notice pages produce `INCOMPLETE`, even when all selected entries were processed.

Each run generates UTF-8 JSON and Markdown with the input SHA-256, selection scope, and per-entry status. Network responses are cached with their request URLs and retrieval times. Cache lifetime defaults to 24 hours; adjust `--cache-hours`, or use `--cache-only --cache-dir ...` for offline review. Missing, stale, or damaged cache data does not silently enable networking.

Reports do not overwrite existing files. Choose a new `--out-dir` for each run. A shared cache can be reused and refreshed during explicitly online checks; use separate cache directories when historical evidence must be retained.

Online requests send DOIs only to Crossref/DataCite. Titles are sent only when title search is explicitly enabled. Optional `--email` puts a contact address in the API User-Agent. The scripts do not upload manuscripts, PDFs, complete BibTeX files, or secrets, and do not follow arbitrary URLs in bibliography entries. Consider disclosure before enabling title search for unpublished work.

| Status | Meaning |
| --- | --- |
| `LOCAL_ONLY` | Local checks only; publication facts not verified |
| `MATCHED_FIELDS` | Compared fields agree; unchecked fields remain explicit. Earlier source failure keeps `provider_complete` false even after successful fallback |
| `REVIEW` | Returned and local fields differ; inspect manually |
| `NO_DOI` / `TITLE_CANDIDATES` | Missing DOI or candidate-only search; not confirmed |
| `NOT_INDEXED` | The queried indexes returned no DOI record; not evidence of fabrication |
| `UNAVAILABLE` | Network, rate limit, cache, or response-format failure; not equivalent to no record |
| `UPDATE_NOTICE` | A notice points to the DOI; read the publisher notice |
| `NO_UPDATE_FOUND` | No notice found in this check; not a guarantee against retraction or correction |
| `PARTIAL` | Update-notice results exceed the read limit |

Exit codes: `0` means the process completed without triggering this run's error threshold; `1` means errors, differences, or notices require review; `2` means input, output, network, or processing was incomplete. Exit-0 reports may still contain warnings and unverified entries. Online tools with `--strict` also fail on unconfirmed or partial checks; strict mode does not replace full-text review.

## Known Limitations

- Decode percent escapes in DOI URLs once; preserve literal percent signs in bare DOI identifiers. Handle common LaTeX character escapes, not arbitrary macros or general LaTeX prose conversion.
- The parser handles `@string`, nested braces, and concatenation. Parent-entry `crossref` inheritance is not merged automatically and requires manual review.
- Suspected unparsed BibTeX entries cause failure rather than silent skipping. Complete BibTeX examples inside explicit comments may also trigger this safeguard.
- `.bbl`, arbitrary `.tex` macro expansion, bibliography merging, and compile diagnostics are outside the scope. Generate current AUX files with TeX tools first.
- Name variants, corporate authors, journal abbreviations, retitled preprints, and publication-date variants may need manual judgment; the scripts flag uncertainty rather than silently correct it.
- Months, final IEEEtran display, missing source fields, JCR quartiles, and claim support require separate review.
- Crossref/DataCite fallback is registration-agency fallback, not independent multi-database confirmation. Missing records in both are not two independent proofs against authenticity.
