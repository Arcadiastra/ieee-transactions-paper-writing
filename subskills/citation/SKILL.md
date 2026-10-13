---
name: ieee-transactions-writing-citation
description: Plan, draft, revise, and review IEEE Transactions citations and references. Find and verify sources, claim support, publication versions, bibliographic metadata, source quality, and BibTeX display conventions.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch
metadata:
  language: en
  trigger: IEEE Transactions citation and reference planning, drafting, revision, and review.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-writing-zh.git
---
# Citation

Read the [main skill](../../SKILL.md). The following display rules are suite defaults, not universal requirements for all IEEE publications. Explicit target-venue requirements take precedence. **Use at least 30 references, including at least 20 from IEEE Transactions sources.**

Prioritize source quality. Limit references from JCR Q3 or lower journals and lower-tier conferences; favor relevant Q1/Q2 work, particularly IEEE Transactions. Prefer work from the past 15 years. Leading AI conferences may be appropriate for interdisciplinary work, while IEEE Transactions remains the primary source family.

Do not cite ResearchGate as the publication source. Trace the final publication and the original source of the conclusion; avoid relying repeatedly on one review article.

## Verification

1. Citation logic: does the reference support background, an approach, a baseline, a data source, or a specific claim, and does its content match?
2. Publication facts: verify authors, title, venue, year, volume, issue, pages or article number, DOI, and version relationships.
3. Display: format verified information consistently across the paper.
4. Is the source formally published? If not, is a more authoritative version available?
5. What is the venue's quartile and the quality of this particular paper?
6. Is this the original source of the conclusion, or can it be traced further?

## Citation Writing

Use the [template guide](references/template-guide.md) for an adaptable LaTeX outline.

- Place references near their claims. Avoid assigning multiple distinct claims to one long citation cluster at a paragraph's end.
- **At most three references in one consecutive citation cluster.** Split larger clusters by specific subclaims or retain the most direct, representative sources. Count adjacent citation commands together and expand numbered ranges when counting.
- Group related work by method ideas and relevance to the problem, not chronologically or by citation volume.
- Prefer original studies directly supporting the claim. Reviews summarize a field but do not automatically replace original method sources.
- Cite inherited components and the closest related work, distinguishing inheritance from innovation.

## Default Display

| Item | Rule |
| --- | --- |
| Authors | Initials before family names; list up to six authors, otherwise first author plus et al.; retain all authors in the database |
| Repeated authors | Repeat names explicitly, not a replacement dash |
| Title | Sentence case; protect acronyms, proper nouns, and model names |
| Journal | Consistent standard abbreviation, e.g. IEEE Trans. Signal Process. |
| Date | Verified volume, issue, pages/article number, publication month, and year; do not mix online-first and issue dates |
| Continuous publication | Do not invent an issue or month |
| Pages | pp. for a page range; Art. no. for article numbers; do not treat an article number as one page or duplicate identifiers unnecessarily |
| Conference | in Proc. plus the standard conference name; volume/pages only when supported |
| Preprint | Actual authors, title, year, and arXiv or equivalent identifier; do not present it as formally published |
| DOI/URL | Hide for ordinary journal/conference entries by default while retaining verified database fields; keep necessary addresses for web/data sources |
| In-text numbers | First-citation order, separate brackets such as [1], [2], [3], without range compression |

## IEEEtran Implementation

Reuse the existing BST and control entry. Do not edit generated BBL files manually. Check package settings before using:

```latex
\usepackage[nocompress]{cite}
```

Set these fields in the applicable BST control entry using the project's existing invocation:

```bibtex
CTLuse_url = {no},
CTLuse_forced_etal = {yes},
CTLmax_names_forced_etal = {6},
CTLnames_show_etal = {1},
CTLdash_repeated_names = {no}
```

BST support varies; verify the compiled output. Do not paste control fields into ordinary bibliography entries.

## Verification Workflow

- Process only actually cited entries within the authorized scope; do not rewrite the reserve bibliography.
- Prefer first pages, publisher records, and official proceedings. Crossref and author pages provide cross-checks. Explain conflicting evidence and do not guess initials from naming conventions.
- Confirm authors, titles, and content relationships when seeking a final version. Distinguish workshops from main conferences, preprints from journal papers, and renamed versions.
- Leave unverified fields unresolved. Do not invent DOIs, months, volumes, issues, or pages. Keep source metadata accurate and treat display rules separately.
- After changes, compile and inspect numbering, author truncation, journal abbreviations, capitalization, article numbers, links, undefined citations, and the rendered bibliography.

## Delivery

### Tools and Full-Text Review

- Before batch verification, read the [tool guide](references/tools.md) and run the read-only offline BibTeX/AUX audit. Online checks require explicit activation; do not rewrite bibliography files or citation keys automatically.
- When the user requests online verification, prefer an installed compatible Bibverify CLI with `--dry-run --json`, following the [integration guide](references/bibverify-integration.md). Never use `--apply` or install/upgrade automatically. If unavailable or incompatible, use `scripts/verify_metadata.py` and disclose the backend without concealing network failures or conflicts.
- Bibverify checks the entire input bibliography and has no `--aux` filter. Confirm a cited-entry subset first when that is the scope. Use `scripts/check_updates.py` for retractions, corrections, and expressions of concern. Distinguish network failure, missing index records, metadata differences, and lack of textual support.
- A DOI hit only establishes a returned record. Inspect comparisons, differences, and unchecked fields. Do not interpret `MATCHED_FIELDS` or Bibverify's `verified` as complete verification. Even exit code 0 requires checking `field_diffs`. No update notice does not prove that a paper has never been retracted.
- For important claims, follow the [claim-support workflow](references/integrity-review.md), read the original text, and record evidence locations. Scripts do not verify manuscript claims or infer JCR quartiles.
- See [source comparisons](references/source-comparison.md) for tool selection. Reuse useful verification ideas without adopting automatic rewriting or overriding this suite's formatting rules.

For small edits, report the actual changes and concise results. For audits, use an entry/problem/source/action/status table if helpful. Do not expand ordinary formatting tasks into a full literature review. Stay within the applicable length budget.
