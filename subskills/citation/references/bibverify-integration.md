# Bibverify CLI Integration

## Integration Model

Call the official CLI directly. Do not maintain a custom adapter, copy its verification engine, or start an MCP server. The compatibility baseline is **Bibverify 0.5.0 with Python 3.11+**, based on the released PyPI package and its actual `--help`, not unreleased branch documentation.

Bibverify is an optional online metadata backend. Retain the suite's offline audit, publication-update check, full-text support review, and author approval rules.

| Task | Tool |
| --- | --- |
| BibTeX structure, duplicates, and AUX citation scope | `scripts/audit_bibtex.py` |
| Online publication metadata | Installed compatible Bibverify CLI |
| Metadata fallback when absent or incompatible | Built-in `scripts/verify_metadata.py`; disclose the backend |
| Retractions, corrections, expressions of concern | `scripts/check_updates.py` |
| Claim support, JCR quartiles, final display | Separate citation-skill review |

## Optional Installation

Install only when the user requests installation or integration, never automatically during ordinary writing. Use a separate environment to avoid conflicts with the built-in tools' pinned parser versions. The package includes upstream MCP dependencies, but this integration does not run or register a server or change host configuration.

Run from the suite root in PowerShell 7. This example assumes Python 3.12 is installed:

```powershell
$ErrorActionPreference = 'Stop'
if (Test-Path -LiteralPath './.venv-bibverify') { throw 'Environment already exists; inspect its version before proceeding.' }
py -3.12 -m venv .venv-bibverify
if ($LASTEXITCODE -ne 0) { throw 'Environment creation failed.' }
& ./.venv-bibverify/Scripts/python.exe -m pip install --index-url https://pypi.org/simple -r ./subskills/citation/scripts/requirements-bibverify.txt
if ($LASTEXITCODE -ne 0) { throw 'Installation failed.' }
& ./.venv-bibverify/Scripts/python.exe -m bibverify --version
if ($LASTEXITCODE -ne 0) { throw 'Version check failed.' }
& ./.venv-bibverify/Scripts/python.exe -m pip check
if ($LASTEXITCODE -ne 0) { throw 'Dependency conflict.' }
```

On other systems, use the available Python 3.11+ and virtual-environment paths. Check availability first. Upgrades require revalidation of read-only behavior, configuration fields, JSON structure, and exit codes.

## Network Scope and Default Configuration

Use the [read-only configuration](../assets/bibverify-readonly.json), not the upstream multi-provider default:

- Only Crossref is enabled; no API key is required.
- Other providers, persistent cache, and upstream report/backup/updated-bibliography/review-bibliography output are disabled.
- The contact email is empty. Users may supply a real contact through `BIBVERIFY_EMAIL`; do not send a fabricated email.
- To enable OpenAlex, Semantic Scholar, arXiv, DBLP, or other sources, explain the scope and current access requirements first, then copy and adjust the configuration in the working directory. Do not silently expand network access. Keep credentials in environment variables or protected local configuration, not the repository.
- Output language is `EN`; the suite identifier is `ieee-transactions-writing`.

**`--dry-run` prevents file writes; it does not mean offline.** DOI lookup or title fallback sends bibliographic information to enabled databases and still requires authorization. It does not verify JCR quartiles or manuscript claims.

Confirm the input scope first. The CLI checks the entire input `.bib` and has no `--aux` filter. For cited entries only, verify the current AUX with the offline audit and use a prepared subset copy. Do not send an entire library containing uncited or private entries. Preserve citation keys and necessary metadata, excluding private file paths, notes, and full abstracts. If a verifiable subset is unavailable, clarify the scope instead of claiming AUX filtering occurred.

## Read-Only Invocation and Reports

This calls the official program and captures its JSON with PowerShell; it is not a custom adapter. Replace the sample bibliography path with the authorized subset's absolute path.

```powershell
$ErrorActionPreference = 'Stop'
$python = (Resolve-Path './.venv-bibverify/Scripts/python.exe').Path
$config = (Resolve-Path './subskills/citation/assets/bibverify-readonly.json').Path
$bib = (Resolve-Path 'C:/paper/references.cited.bib').Path
$reportFile = Join-Path (Get-Location) 'reports/bibverify-01.json'
if (Test-Path -LiteralPath $reportFile) { throw 'Report already exists; choose a new filename.' }
$before = (Get-FileHash -LiteralPath $bib -Algorithm SHA256).Hash
$jsonLines = & $python -X utf8 -m bibverify check $bib --config $config --dry-run --json
$code = $LASTEXITCODE
if ($before -ne (Get-FileHash -LiteralPath $bib -Algorithm SHA256).Hash) { throw 'Source file changed; stop.' }
if (-not $jsonLines) { throw "No JSON returned; exit code $code" }
$jsonText = $jsonLines -join "`n"
$report = $jsonText | ConvertFrom-Json
if ($report.dry_run -ne $true -or $report.applied -ne $false) { throw 'Unexpected write state.' }
New-Item -ItemType Directory -Path (Split-Path $reportFile) -Force | Out-Null
$jsonText | Set-Content -LiteralPath $reportFile -Encoding UTF8
Write-Output "Bibverify exit code: $code; original report: $reportFile"
if ($code -notin @(0, 2, 3, 4)) { throw 'Input or runtime error; inspect diagnostics.' }
```

Never pass `--apply` or automatically replace the source bibliography with a candidate file. `--dry-run` disables upstream persistent cache and file output. Preserve stdout JSON as evidence when needed; do not claim a nonexistent disk cache.

## Report Interpretation

These are **Bibverify 0.5.0** exit codes, not the built-in tools' 0/1/2 codes:

| Code | Action |
| --- | --- |
| 0 | Inspect each result, field suggestions, and unchecked signals |
| 2 | Suggested updates; not evidence that files were modified |
| 3 | Ambiguous match, no match, or identifier conflict; review manually |
| 4 | Unavailable source or incomplete verification; preserve the failure |
| 5 | Invalid input/configuration; repair conditions before retrying |
| 1 / other | Runtime error; retain diagnostics rather than label the citation incorrect |

Inspect `complete`, `counts`, `entries[].provider_status`, `entries[].candidates`, `entries[].field_diffs`, `dry_run`, and `applied`.

**Exit 0 and `verified` do not establish that every field is correct.** In the source suite's baseline tests, records missing authors or pages could still receive an identity match while `field_diffs` suggested `add` operations. Review every action other than `keep_original` and report missing or unchecked signals separately.

Preserve original statuses and JSON. Explanations must not equate `not_found` with fabrication or `source_unavailable` with a nonexistent publication.

## Fallback and Revisions

- Missing installation, incompatible Python, or unvalidated version: disclose the reason and use the built-in backend; do not install or upgrade automatically.
- Timeout, rate limit, or conflicting records: preserve the result. With permission, query another provider, but do not let a new hit erase earlier conflicts or failures.
- Propose original fields, replacements, sources, and rationale before editing references; obtain author approval.
- Run the publication-update check as needed after metadata checks. Verify claim support and final IEEE display separately.

## Version Sources

- [PyPI 0.5.0](https://pypi.org/project/bibverify/0.5.0/)
- [Upstream v0.5.0](https://github.com/Hylouis233/bibverify/releases/tag/v0.5.0)
- [v0.5.0 CLI source](https://github.com/Hylouis233/bibverify/blob/v0.5.0/src/bibverify/cli.py)

Do not use `agent init` or `skill export` to overwrite this suite. This integration adds no automatic installation, repair, or MCP configuration.
