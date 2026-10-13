---
name: ieee-transactions-writing
description: Plan, draft, revise, and review IEEE Transactions papers. Coordinate seven section skills around contributions, mechanisms, evidence, affirmative phrasing, cross-section coherence, and length control.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch Task
metadata:
  language: en
  trigger: Planning, drafting, revision, and review of IEEE Transactions-style academic papers.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-writing-zh.git
---
# IEEE Transactions Writing

## Scope and Use

The main skill governs shared principles, section responsibilities, and acceptance checks. Load only the section skills needed for the task.

| Section skill           | File                                                  | Responsibility                                                     |
| ----------------------- | ----------------------------------------------------- | ------------------------------------------------------------------ |
| Abstract                | [SKILL.md](subskills/abstract/SKILL.md)                | Self-contained abstract without specific numbers; Index Terms      |
| Introduction            | [SKILL.md](subskills/introduction/SKILL.md)            | Motivation, challenges, related work, gap, overview, contributions |
| Problem definition      | [SKILL.md](subskills/problem-definition/SKILL.md)      | Formulation, assumptions, difficulties, design requirements        |
| Methodology             | [SKILL.md](subskills/methodology/SKILL.md)             | Mechanisms, formalization, theoretical explanation, method figures |
| Results and discussions | [SKILL.md](subskills/results-and-discussions/SKILL.md) | Concise setup, qualitative interpretation, figures and tables      |
| Conclusion              | [SKILL.md](subskills/conclusion/SKILL.md)              | Validated contributions, mechanism value, significance             |
| Citation                | [SKILL.md](subskills/citation/SKILL.md)                | Claim support, source verification, metadata, reference formatting |

## Writing Workflow

### LaTeX Outlines

Use the [template index](references/template-guide.md) when building a section outline. The snippets specify section order and paragraph responsibilities, not a fixed research topic or sentence pattern. Adapt them to the study. They do not replace an official typesetting template or the revision approval workflow.

Adapt the workflow to the existing workspace and user feedback. The sequence below assumes an initially empty workspace.

### Build the Structure

When the user has neither special requirements nor an outline, first prepare an outline with a 10-page initial-submission budget. Treat this as the suite's default budget; explicit requirements of the target journal take precedence.

If no template is supplied, use the [official IEEE LaTeX template](https://journals.ieeeauthorcenter.ieee.org/create-your-ieee-journal-article/authoring-tools-and-templates/tools-for-ieee-authors/ieee-article-templates/). Immediately flag an incompatible user-provided format.

Unless instructed otherwise, use five main body sections, plus the abstract and references, within 10 total PDF pages.

| Section                 | Recommended budget              |
| ----------------------- | ------------------------------- |
| Abstract                | 150-200 words                   |
| Introduction            | 0.9-1.3 pages                   |
| Problem definition      | 1.5-2.5 pages                   |
| Methodology             | 2.5-3.5 pages                   |
| Results and discussions | 2.0-3.0 pages                   |
| Conclusion              | 150-200 words                   |
| References              | At least 30 entries; 0.7-1 page |

Use this structure unless the paper requires a special arrangement. If the target page limit differs from 10, scale section budgets and reference-count budgets proportionally. Configure `.latexmkrc` as appropriate for a working automatic build.

If an existing paper substantially differs from this structure, stop and ask the user to choose:

1. A major structural revision or rewrite using the recommended structure (recommended).
2. Disable this skill for the session.
3. A user-defined approach.

Proceed only according to the selected option.

### Drafting Order

Follow this order unless the user specifies another. Skip completed material. For substantial incompatibilities, propose a major revision or rewrite and obtain approval before editing.

1. Establish 3-5 distinct contributions. Use parallel noun phrases or parallel gerund phrases throughout, such as `an algorithm that...` or `Proposing an algorithm that...`. Present them explicitly in the introduction.
2. Select experiments supporting those contributions: at least one main experiment explained in detail and at most two supporting mechanism experiments.
3. Draft results and discussions using its section skill and hard length limit.
4. Draft problem definition and methodology within their hard limits.
5. Draft the introduction and organize, verify, and format citations.
6. Distill the abstract, Index Terms, and conclusion.
7. Adjust the full manuscript to the total page budget. First keep the abstract within 150-200 words. For a two-column final page, fill the left column and approximately 60% of the right column's text height; for a single-column final page, target approximately 80% of the text height.

Respect section hard limits during drafting. In the final length pass, use recommended ranges while keeping the whole PDF within its limit.

## First Principles

- Organize the argument around contributions: important problem -> key obstacle -> novel mechanism -> experimental evidence -> significance.
- Allocate space to mechanism innovation. Do not turn the body into an implementation checklist or research diary. Do not include filesystem paths. Avoid internal codes; if necessary, define their full names on first use.
- Explain positively what the paper solves, how, and why it works. Unless requested, reserve limitations, unfinished work, and defensive negative boundary statements for the limitations and future work passage.
- Preserve the conditions and evidence scope necessary for the conclusions. Calibrate certainty without diluting claims until they cease to explain the contribution. Express key conclusions affirmatively.
- No specific numerical values in the abstract. Do not repeat numerical values from figures or tables in results analysis prose. Put necessary values in figures, tables, or mathematical expressions.
- Default to at most 10 pages for the full initial-submission PDF, including references.

## Five Body Sections and Contribution Roles

Default order: Introduction -> Problem Definition and Analysis -> Methodology -> Results and Discussions -> Conclusion.

In working notes, map problem obstacles to mechanisms, experimental tests, and contribution claims. This map need not appear in the manuscript. Questions raised in the introduction must receive responses later; method claims need evidence, and interpretations must return to the problem and mechanisms.

Use distinct treatments of the same contribution: the abstract gives a miniature complete argument; the introduction overview connects the gap to mechanism cooperation; the contribution list identifies original research increments; the conclusion distills validated value. Do not repeat the same sentences in all four places.

## Affirmative Phrasing

Review `instead`, `instead of`, `rather than`, `not`, `but not`, `without`, `unlike`, `as opposed to`, and `not only ... but also`. For rhetorical "not A, but B" statements, remove A and state B directly. Where this suite prohibits negative phrasing, these expressions are also prohibited. If an equivalent affirmative statement is impossible or a counterexample's implications are unclear, ask the author.

| Original                                                                                                                  | Affirmative direction                                                                              |
| ------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Instead of processing each source separately, the method jointly models their interactions.                               | The method jointly models interactions among the sources.                                          |
| The improvement is not merely empirical but reflects the value of complementary information.                              | The improvement reflects the value of complementary information.                                   |
| The discussion explains how the mechanism addresses the identified challenge rather than repeating the numerical results. | The discussion explains how the mechanism addresses the identified challenge.                      |
| The experiment is not a comparison of unrelated architectures but a controlled evaluation of the proposed component.      | The experiment is a controlled evaluation of the proposed component.                               |
| Without changing the input information, the comparison isolates the effect of the interaction mechanism.                  | With identical input information, the comparison isolates the effect of the interaction mechanism. |
| The evaluation varies the operating conditions but not the underlying system.                                             | The evaluation varies the operating conditions within the same underlying system.                  |
| The framework not only integrates heterogeneous observations but also models their interactions.                          | The framework integrates heterogeneous observations and models their interactions.                 |
| The analysis focuses on the mechanism's contribution as opposed to routine implementation details.                        | The analysis focuses on the mechanism's contribution.                                              |

State necessary conditions affirmatively, for example `Under the stated assumptions, ...`. Group and streamline criticism of related work, targeting the specific research gap that motivates this paper.

## Sentence Logic and Terminology

- Prefer an overview-to-detail structure within paragraphs and clear transitions between paragraphs.
- Advance one central judgment per paragraph: topic -> evidence or mechanism -> inference -> transition.
- Identify causation, progression, parallelism, contrast, conditions, or synthesis before choosing connectors such as `therefore`, `furthermore`, `meanwhile`, `however`, `under`, or `taken together`. Omit a connector when unnecessary.
- Keep technical terms, module names, abbreviations, symbols, and figure labels consistent. Do not rename technical concepts merely for variety.
- When over length, remove empty emphasis and formulaic filler first. Every sentence should convey information or reasoning.

## Figures and Tables

- **Figures must be self-explanatory. Symbols must be understandable or explicitly defined in problem definition or methodology. Do not add explanatory phrases or sentences as small gray text inside figures or tables.**
- Put titles in LaTeX captions, not inside the graphics.
- Add a legend when the visual encoding is unclear.
- **Use concise caption phrases or sentences, at most 15 words, and keep every caption on one rendered PDF line.**
- Cite every figure and table in the body.
- Do not duplicate the same data in both a figure and a table. Prefer line plots for many experimental groups emphasizing trends, bar charts for fewer groups emphasizing comparisons, pie charts for proportions, and tables for dense heterogeneous data.

## Launch-Presentation Principles

1. Organize the narrative around original contributions and substantial experimentally supported advantages.
2. Do not narrate the sequence of what was done, tried, or failed.
3. Do not undermine the core contribution with expressions such as "unfortunately," "merely," "still substantially behind," or "limited effectiveness." Do not write a weakness summary on the reviewers' behalf.
4. Retain the field's standard metrics. Prefer academically valid evaluation dimensions or comparison settings that support the contribution over metrics that work against its central argument.
5. Do not turn a non-leading result into direct rejection or weakening of the core contribution. Give an evidence-based explanation using research objectives, applicable conditions, and reasonable tradeoffs.
6. State advantages explicitly; do not expect reviewers to discover them unaided in a table.
7. Every experiment must have an argumentative purpose; remove it if it has none.
8. Reinforce the key takeaways in the conclusion rather than introducing sudden self-negation.

## Revision and Acceptance Workflow

Spelling, grammar, formatting, and punctuation corrections may be applied directly when they do not alter substance. For substantive edits, prepare a revision proposal unless the user explicitly waives it.

For passages other than section endings, abstracts, and conclusions, a proposal has eight parts: preceding original passage, its connection to the target passage, following original passage, its connection to the target passage, original target passage, revised target passage, rationale, and a summary of changes. Add translations only when requested. Obtain approval before applying the change and moving to the next passage.

For newly added passages or missing context at section boundaries, explain the absence briefly.

Proofreading order:

1. Compare the full structure with the suite's five-section structure; ask before major restructuring or rewriting.
2. Compare each section with its section skill; ask before major restructuring or rewriting.
3. Correct clear spelling, grammar, and formatting errors.
4. Improve wording, sentences, paragraphs, transitions, and logical relations.
5. Resolve clear internal mismatches and contradictions.
6. Review misleading expressions and claims stronger than the evidence.
7. Reduce repetition, retaining one detailed explanation or distinct perspectives where needed.
8. Address other detailed issues.
9. Align length and submission formatting.

Editing checks:

1. Read the current manuscript and supporting material; confirm scope, build entrypoint, and target version. Propose substantive edits before applying them.
2. Check the contribution chain and section responsibilities first. Identify missing facts for confirmation.
3. Edit only the authorized scope and preserve the user's existing changes.
4. After layout changes, compile and inspect PDF page count, references, numbering, overflow, and key rendered pages.
5. If over length, report it and propose low-loss reductions: repeated discussion -> rhetorical negation -> non-core engineering details -> redundant visuals and whitespace. Never silently alter margins, shrink fonts, or delete essential mechanisms.
6. If figures show clear signs of fabricated data, immediately alert the author to the academic risk.
7. If figures appear strongly suggestive of AI generation, flag the possible publication concern and propose redrawing.
8. Crop unnecessary margins and prefer width-to-height ratios of at least 4:3 to save space. For portrait-oriented figures, propose rotation, coordinate transformations, or rearrangement of visual elements as appropriate.

## Overall Acceptance

- Every core contribution has motivation, a method realization, and evidence.
- Innovations connect across sections while retaining distinct roles.
- Structure follows the suite or the user's explicit alternative.
- Abstracts contain no specific numbers; results prose does not repeat plotted or tabulated values.
- Experimental setup is concise, without unsolicited multi-seed studies or exhaustive engineering reproduction requirements.
- Preserve true conditions and match connectors to logical relations.
- Figures, equations, text, and citations agree; the complete PDF meets its length target.
- Figures show no apparent fabrication or AI-generation artifacts, and visuals agree with one another and the text.
