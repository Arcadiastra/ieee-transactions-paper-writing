---
name: ieee-transactions-writing-problem-definition
description: Plan, draft, revise, and review IEEE Transactions problem definitions and analyses. Formalize objects, inputs, outputs, objectives, and assumptions; unify notation; derive design requirements from the key difficulties.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch
metadata:
  language: en
  trigger: IEEE Transactions problem definition planning, drafting, revision, and review.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-writing-zh.git
---
# Problem Definition

Read the [main skill](../../SKILL.md). Formalize the task and explain its difficulties without prematurely repeating method implementation. Recommended length: 1.5-2.5 pages; hard maximum: 3 pages.

If the contributions include analysis of representative traditional research approaches, use the title *Problem Definition and Analysis*. After a formulation subsection, give each representative approach a formal analysis subsection. Otherwise omit subsection headings.

**Equation (1) must give the overall mathematical formulation of the problem.**

## Purpose and Inputs

Use the [template guide](references/template-guide.md) for an adaptable LaTeX outline.

With contributions already established, draft this section after results and discussions, in coordination with methodology.

## Logical Structure

Research object and representation -> known information and unknown variables -> mathematical objective or decision task -> necessary constraints and assumptions -> information or paradigm bottlenecks -> method design requirements.

Do not repeat detailed foundational theory unrelated to the core contributions.

## Modeling Rules

- Distinguish physical objects, observations, unknowns, estimates, and ground truth; distinguish individual samples, batches, training distributions, and prediction tasks.
- Define symbols, sets, indices, dimensions, and necessary units at first use. Avoid undefined internal codes. Definitions must be internally consistent; explain any part not given a formal definition clearly in words. Use affirmative definitions rather than negative exclusions.
- Specify inputs, outputs, domains, and codomains. The mathematics must stand on its own, and the relationship between key inputs/outputs and the physical setting must be explicit.
- Explain assumptions needed for theorems, identifiability, or mathematical solvability, concisely and affirmatively.
- Align constraints with the algorithms and metrics in the experiments.
- Explain the meaning and role of equations. Introduce core inputs or known quantities above a displayed equation; explain outputs, intermediate variables, and local subscripts below it. Avoid redundant definitions and never assign conflicting definitions to a symbol.
- Exclude experimental condition definitions and results. Do not cite or depend on notation introduced only in methodology.
- Define all notation needed later, but do not introduce unused notation. Coordinate this with methodology.

## From Analysis to Contributions

Apply this subsection only when analyzing traditional approaches.

For each approach, explain its obstacle, how the obstacle appears under the formal problem framework, and what mechanism is needed. Embed the approach in the formulation and identify its theoretical deficiency through mathematics and engineering context.

Conclude affirmatively with the deficiency and resulting design requirement. Do not use negative phrasing to narrow the research gap defensively. The analysis must motivate the central innovation.

## Acceptance

- Define necessary symbols, sets, indices, dimensions, and units at first use.
- Keep the mathematics independently coherent.
- Avoid unnecessary repeated or contradictory definitions.
- Follow the logical structure.
- Exclude experimental conditions, results, and dependence on later method notation.
- Use every introduced symbol and equation later; maintain clear scope.
- Equation (1) states the overall problem formulation.
- Stay within the hard length limit.
