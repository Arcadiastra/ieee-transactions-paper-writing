# Public Citation Tools: Comparison and Selection

Source review date: 2026-10-12. This translates the source suite's recorded review of public GitHub projects, documentation, selected verification code, and tests. It is neither a ranking of all commercial products nor an accuracy benchmark on a common labeled dataset. Translation does not constitute a new upstream audit.

## Integration Decision

Among the reviewed projects, **Bibverify was the strongest reference for an overall verification architecture**: identifier-first lookup, explainable matching, structured failure states, write protection, and cross-platform test organization. This is an architectural fit judgment, not a claim of best-in-industry accuracy.

The suite retains its small read-only tools and offers [optional Bibverify CLI integration](bibverify-integration.md), without making it a base dependency or starting an MCP server. The validated baseline is 0.5.0, with Crossref enabled by default. Enable other sources explicitly according to access conditions. Main-branch features do not establish released-package behavior.

## Comparison

| Project | Useful design observed | Decision for this suite |
| --- | --- | --- |
| [Hylouis233/bibverify](https://github.com/Hylouis233/bibverify) | Identifier-first checks; explainable title, author, year, venue, and page matching; provider states; source-protection tests | Main architectural reference; retain field-level reporting, conflicts, and unchecked scope; no automatic merging |
| [chrisyangsong/citegate](https://github.com/chrisyangsong/citegate) | Verification exit codes, CI workflows, Crossref update checks | Reuse publication-status checking concepts; not every update is a retraction |
| [ComDec/citekeep](https://github.com/ComDec/citekeep) | Citation-key preservation, per-entry decisions, evidence records, unresolved-entry retention | Preserve keys and review history; built-in scripts have no write-back path |
| [Altman-conquer/bibtex-verifier](https://github.com/Altman-conquer/bibtex-verifier) | Mature BibTeX parser, field comparisons, Crossref/DataCite fallback, date explanations | Use a mature parser, preserve different publication dates, and compare author order and names |
| [tvquynh/citation-verifier](https://github.com/tvquynh/citation-verifier) | DOI/title conflicts and failure-versus-not-found distinction | Preserve status boundaries; avoid simplified parsing or whole-entry verification from a title threshold |
| [QuiXamii/refright](https://github.com/QuiXamii/refright) | Title/venue normalization and explainable differences | Reference abbreviation comparisons without automatic repair or permissive fuzzy acceptance |
| [CloudWave818/ieee-skills](https://github.com/CloudWave818/ieee-skills) | Separates citation logic, metadata, and formatting | Useful review guidance; its citation module is not itself an executable verification script |

## Three Distinct Qualities

- Broad database coverage does not establish correct matching for every entry.
- Mature metadata verification does not establish support for manuscript claims.
- Automatic correction does not make a tool suitable for modifying an already reviewed bibliography by default.

Keep four layers separate: static checks, metadata, publication updates, and full-text claim support. The last requires locating and reviewing original evidence, not claiming automatic proof of citation appropriateness.

## Pinned Source Evidence

The following files and revisions were inspected in the source review. Runtime tasks need not fetch them automatically.

- Bibverify `17d65e3a178e055e649d09c88fa22b56e2599b52`: [matching.py](https://github.com/Hylouis233/bibverify/blob/17d65e3a178e055e649d09c88fa22b56e2599b52/src/bibverify/matching.py), [source-protection tests](https://github.com/Hylouis233/bibverify/blob/17d65e3a178e055e649d09c88fa22b56e2599b52/tests/test_golden_workflow.py), [small regression cases](https://github.com/Hylouis233/bibverify/blob/17d65e3a178e055e649d09c88fa22b56e2599b52/benchmarks/cases.json). These were read; the full upstream test suite was not run locally.
- Citegate `94cc0a02a63a11154664c88b25923cbd0dc7c028`: [sources.py](https://github.com/chrisyangsong/citegate/blob/94cc0a02a63a11154664c88b25923cbd0dc7c028/src/citegate/sources.py), [core.py](https://github.com/chrisyangsong/citegate/blob/94cc0a02a63a11154664c88b25923cbd0dc7c028/src/citegate/core.py).
- CiteKeep `e7f2c92d5d06e30e44cd4e056b08750512ee630e`: [core.py](https://github.com/ComDec/citekeep/blob/e7f2c92d5d06e30e44cd4e056b08750512ee630e/src/citekeep/core.py).
- BibTeX Verifier `5b4961e574aad56d86ad05470b14068fbb89a612`: [loader.py](https://github.com/Altman-conquer/bibtex-verifier/blob/5b4961e574aad56d86ad05470b14068fbb89a612/bibtex_verifier/loader.py), [comparator.py](https://github.com/Altman-conquer/bibtex-verifier/blob/5b4961e574aad56d86ad05470b14068fbb89a612/bibtex_verifier/comparator.py), [apis.py](https://github.com/Altman-conquer/bibtex-verifier/blob/5b4961e574aad56d86ad05470b14068fbb89a612/bibtex_verifier/apis.py).
- Citation Verifier `e6e8ae0bc2913fcba88536751760c59733b2d0f8`: [verify_citations.py](https://github.com/tvquynh/citation-verifier/blob/e6e8ae0bc2913fcba88536751760c59733b2d0f8/verify_citations.py).
- Refright `6ff5b9958f54a287d344b3e97b797045c1e19ea5`: [match.py](https://github.com/QuiXamii/refright/blob/6ff5b9958f54a287d344b3e97b797045c1e19ea5/refright/match.py).
- IEEE Skills `ee30fda73e76b93ede86c07b90bcd09319a50f16`: [metadata-check.md](https://github.com/CloudWave818/ieee-skills/blob/ee30fda73e76b93ede86c07b90bcd09319a50f16/skills/ieee-citation/static/fragments/task_type/metadata-check.md).

The reviewed repositories were recorded as MIT-licensed at the review date. This suite's tools are independently implemented with their own tests; it does not bundle those upstream source files. Dependencies retain their own licenses. Preserve copyright notices if upstream implementations are later ported directly.

## Research-Paper-Writing-Skills Templates

The source review inspected [Master-cai/Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills) at `77e7c2c1ba06f7d71844873147665437a03aac1b`.

Its [abstract template](https://github.com/Master-cai/Research-Paper-Writing-Skills/blob/77e7c2c1ba06f7d71844873147665437a03aac1b/research-paper-writing/references/examples/abstract/template-b.md) and [method overview template](https://github.com/Master-cai/Research-Paper-Writing-Skills/blob/77e7c2c1ba06f7d71844873147665437a03aac1b/research-paper-writing/references/examples/method/overview-template.md) are writing outlines, not IEEEtran classes or official typesetting templates.

Borrow useful organization, not the entire template set: challenge -> insight -> contribution for abstracts, information-flow navigation for method overviews, and paragraph-level reverse outlining. Specific vision-task names, negative contrasts, and example numbers require adaptation; they do not override this suite's affirmative phrasing and number-free abstract rules.

The source review did not directly import upstream templates or change the confirmed section structure. This suite provides simplified local outlines through the [template index](../../../references/template-guide.md); official IEEE templates remain responsible for typesetting.

## Official Verification References

- [Crossref REST API](https://www.crossref.org/documentation/retrieve-metadata/rest-api/)
- [Crossref retraction data](https://www.crossref.org/blog/retraction-watch-retractions-now-in-the-crossref-api/)
- [Crossref versions, corrections, and retractions](https://www.crossref.org/documentation/principles-practices/best-practices/versioning)
- [BibtexParser documentation](https://bibtexparser.readthedocs.io/en/v1.4.0/bibtexparser.html)
