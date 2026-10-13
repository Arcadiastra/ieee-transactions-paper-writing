---
name: ieee-transactions-writing-methodology
description: Plan, draft, revise, and review IEEE Transactions methodology sections and method figures. Explain novel mechanisms through an overall framework, formal definitions, and theoretical reasoning while keeping non-core engineering details concise.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch
metadata:
  language: en
  trigger: IEEE Transactions methodology planning, drafting, revision, and review.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-writing-zh.git
---
# Methodology

Read the [main skill](../../SKILL.md), the problem definition, and the confirmed implementation or derivation. Focus on methodological foundations and mechanism innovation. Recommended length: 2.5-3.5 pages; hard maximum: 4.5 pages.

**Use an overview-to-detail structure: introduce the whole framework, then explain the modules rigorously in subsections, emphasizing original designs or findings.**

**The overview contains this section's first equation, which must state the overall model corresponding to the core contribution. Define its symbols in problem definition or immediately after the equation.**

## Purpose and Inputs

Use the [template guide](references/template-guide.md) for an adaptable LaTeX outline.

With contributions already established, draft this section after results and discussions, together with problem definition.

## Logical Structure

Use the overall framework equation to introduce inputs, processing paths, information interactions, and outputs. Explain each core novel mechanism in a subsection, then give essential decision, training, or solution procedures.

For each mechanism: prerequisite notation and assumptions -> formal mechanism -> theoretical analysis of novelty and effectiveness.

Briefly explain the role of standard components and give original mechanisms enough space. Analyze novelty and effectiveness through formal or qualitative theory, including mechanism-level reasoning and proofs where appropriate.

## Expression Rules

- Explain design through problem requirements and novel mechanisms, emphasizing theoretical innovation. An advanced component alone is not an explanation of effectiveness.
- Except in the abstract and relevant contribution statements, do not disclose experimental results in this section or earlier. Keep datasets, parameter settings, and experimental engineering details in the experimental section.
- Distinguish existing components from original organization or mechanisms. Describe necessary established methods briefly and substantially compress nonessential implementation detail.
- Keep notation and dimensions consistent across equations, text, and figures. Connect inputs to outputs and complete the task formalized in Section II. Check indices, normalization ranges, valid elements, and constraints where needed.
- Explain solution steps necessary to understand the mechanisms.
- Omit data volumes, full hyperparameter lists, hardware, complexity, and tuning procedures here unless they are part of an innovative contribution. If efficiency or complexity is not a claimed contribution, it need not appear in this section.
- Use affirmative phrasing throughout.

## Method Figures

- Show the complete model structure or end-to-end data, work, or control flow.
- Follow the field's scientific visualization conventions.
- Serve the overall structure or a clear claim and keep the abstraction level consistent.
- Derive modules, arrows, symbols, and connections from the actual study.
- Use overview figures for module cooperation and detail figures for innovations. Avoid redundant figures. A complex overview may span both columns if space permits.
- Keep labels and strokes legible at final column width; labels must not obscure arrows. Reduce whitespace, repeated legends, and decoration.
- Emphasize research innovation and simplify routine experimental parameters, components, and implementation constraints.
- **Do not add explanatory phrases or sentences as small gray text inside figures or tables.**

## Acceptance

- Follow the logical structure and expression rules.
- The overview's first equation clearly represents the model behind the core contribution.
- Formalize and justify the mechanisms named in the contribution list.
- Method figures follow the conventions and show no apparent AI-generation or fabrication artifacts.
- Compress non-core engineering detail before cutting innovation explanations.
- Stay within the hard length limit.
