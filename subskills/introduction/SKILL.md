---
name: ieee-transactions-paper-writing-introduction
description: Plan, draft, revise, and review IEEE Transactions introductions. Connect application needs, challenges, related work, research gaps, method overviews, and contribution lists to problem analysis and methodological innovation.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch
metadata:
  language: en
  trigger: IEEE Transactions introduction planning, drafting, revision, and review.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-paper-writing-zh.git
---
# Introduction

Read the [main skill](../../SKILL.md). Check bibliographic claims with the [citation skill](../citation/SKILL.md). Recommended initial-draft length: 0.9-1.3 pages; hard maximum: 2 pages. Draft the main introduction after results and discussions, problem definition, and methodology. Prepare the contribution list first, as specified by the main workflow.

**Do not divide this section into subsections or include specific experimental designs or numerical results. Equations are generally unnecessary.**

## Purpose and Inputs

Use the [template guide](references/template-guide.md) for an adaptable LaTeX outline.

Follow the main skill's first principles. Every argument should highlight the novelty and practical value represented by problem definition, methodology, and the already established contributions.

Use real application needs and gaps in existing work as motivation for the original research increment. Apart from the contribution list, base this section on the three completed sections above.

## Logical Structure

1. Define the research topic and its broader importance; this may occupy one paragraph.
2. Establish the concrete needs and challenges in the real target setting corresponding to problem definition. Define that setting clearly.
3. Identify the task's key difficulties, the mechanisms creating them, and their consequences.
4. Organize related work from overview to groups to synthesis. Group references by research approach, summarize each group's idea, and explain its inherent limitations and causes when facing the identified difficulties in the target setting. Conclude by identifying the combination of difficulties that remains unresolved in that setting.
5. Give a qualitative method overview: what approach is proposed, which mechanisms address the difficulties, and how this leads to the contributions. Example transition: `To summarize, the contributions of this paper include:`.
6. Present the contribution list, prepared first according to the main skill.
7. Add a concise roadmap if needed: `The remainder of this paper is organized as follows.` Describe each section's role in a few words.

Do not turn related work into a paper-by-paper list of implementations and judgments.

## Writing Rules

- Exclude experimental numbers.
- Describe mechanisms qualitatively in the overview; reserve detail for methodology.
- Each contribution should identify the proposed or established item, its key novelty, and its value for the problem. Use parallel syntax and comparable granularity.
- Theory, formulation, and mechanisms may be separate contributions when each adds something distinct and receives support later.
- Standard components, implementation effort, and the number of experiments are not innovations by themselves. Experimental contributions should identify a new insight or demonstrated capability.
- Avoid `first`, `comprehensively solves`, and similarly strong claims unless established.

## Connections and Boundaries

Connect related approaches through problems and mechanisms. Use `however` only for real contrasts and `therefore` or `these challenges motivate` when difficulties lead to a design requirement.

Criticism of prior work must be specific, localized, and tied to research conditions, with citations close to the supported claims. Do not subsequently negate that criticism through rhetorical hedging.

## Acceptance

- Each important gap is deepened in Section II, addressed in Section III, and tested in Section IV.
- The argument follows this skill's structure.
- Each contribution can be located in later sections.
- The method overview has a distinct role from the abstract and contribution list.
- Remove generic background and unnecessary engineering numbers.
- Stay within the hard length limit.
