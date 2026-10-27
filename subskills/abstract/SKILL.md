---
name: ieee-transactions-paper-writing-abstract
description: Plan, draft, revise, and review IEEE Transactions abstracts and Index Terms. Build a self-contained account of the problem, challenges, mechanisms, and qualitative validation without specific numerical values, and select searchable keywords.
license: MIT
allowed-tools: Read Write Edit Glob Grep Bash WebSearch WebFetch Task
metadata:
  language: en
  trigger: IEEE Transactions abstract planning, drafting, revision, and review.
  target-venue: IEEE Transactions journals
  source_repository: https://github.com/Arcadiastra/ieee-transactions-paper-writing-zh.git
---
# Abstract

Read the shared principles in the [main skill](../../SKILL.md) if not already loaded. Draft this concise summary after results and discussions, problem definition, methodology, and introduction, together with the conclusion. Recommended length: 150-200 words; hard maximum: 250 words.

**Use one compact paragraph. Do not split it into multiple paragraphs.**

## Inputs

Use the [template guide](references/template-guide.md) for an adaptable LaTeX outline.

The four completed body sections listed above are the primary inputs. Explicitly ask for missing evidence.

## Logical Structure

Context -> problem status and importance -> key challenges in the target setting -> gap in existing methods -> proposed approach -> core mechanisms and their roles -> how experimental findings support the conclusions.

Combine functions where appropriate, without mechanically prescribing a sentence count. Start from the specific problem and move quickly to the paper's work.

## Writing Rules

- Include at least one topic within the target journal's scope and at least one explicit noun naming a core research object within that scope.
- Make the abstract fully self-contained. Readers should be able to assess relevance from the abstract alone; preserve a complete logical chain independent of the main text.
- Do not include specific performance values, percentages, dataset sizes, system sizes, component counts, hyperparameters, or training settings. Spelling out numbers does not bypass this rule.
- Necessary established terms such as `three-dimensional` are not result values. Judge meaning rather than deleting characters globally.
- Do not include references, equations, figure or table pointers, or engineering checklists. Introduce abbreviations only when necessary and define them on first use.
- Explain how the main mechanisms address the challenges; a list of component names is not a contribution.
- Use supported qualitative judgments and state the conditions or dimensions of the advantage. Avoid unsupported `universal`, `optimal`, or `state-of-the-art` claims.
- Use concise affirmative phrasing throughout. Describe the difficulties faced by traditional methods rather than listing what they cannot handle.
- Do not emphasize limitations or automatically end with future work. Retain conditions necessary for understanding.
- Exclude undefined specialized abbreviations, reference numbers such as `[1]`, and body pointers such as `Fig. 3`.

# Index Terms

**Balance retrieval recall and precision while accurately representing the paper**, and give editors clear topic cues for reviewer assignment.

## Five-Term Strategy

Use five keywords or keyword phrases by default, covering the research chain. Keep them aligned with the target journal's topic scope: **include at least one keyword clearly within that scope**.

1. Research object or application setting (one): identify the system, such as `Distribution networks`, `Microgrids`, or `Power transmission systems`.
2. Core research task (one): identify the problem, such as `State estimation`, `Optimal power flow`, or `Network reconfiguration`.
3. Key data, measurement conditions, or problem features (one): select features central to the contribution, such as `Pseudo-measurements`, `Smart meters`, `Advanced metering infrastructure`, or `Phasor measurement units`.
4. Core mechanism and theoretical foundation (two): preferably choose one complementary term for each, such as `Attention mechanisms`, `Bayesian decision theory`, `Graph theory`, `Deep reinforcement learning`, or `Mixed-integer linear programming`.

## Three Selection Principles

**Complement the title.** Add useful synonyms, broader terms, or technical features not already captured in it.

For a title such as *Deep Learning Approaches for Feeder Parameter Estimation*, use actual model or learning-paradigm terms such as *Convolutional neural networks* or *Supervised learning* when appropriate, instead of automatically repeating *Deep learning*. Core domain terms may still repeat the title.

**Align with controlled vocabulary.** Prefer standardized terms in the IEEE Taxonomy or IEEE Thesaurus, such as *Phasor measurement units* rather than informal labels such as *Synchrophasor devices*. Use technical properties, not internal or invented codes.

**Choose useful granularity.**

- Too broad: *Algorithm*, *Model*, *Optimization*, *Simulation*, *Power*.
- Too narrow: *3-layer residual graph attention with leaky ReLU*.
- Appropriate: *Graph attention networks*, *Non-convex optimization*, *Measurement uncertainty*.

# Review and Delivery

When delegation is available and authorized, ask an independent reviewer to first read only the title, abstract, and Index Terms and search for the target journal's topic scope. Request:

1. Whether the title, abstract, and Index Terms each contain at least one topic within the target journal's scope and at least one explicit noun naming a core research object within that scope, and an assessment of the risk of desk rejection as `out of scope`.
2. Its inferred account of the body and estimated novelty and quality, including whether the text is sufficiently self-explanatory and contains apparent internal codes with no context.

If an independent reviewer cannot be assigned, perform this part of the review in the main agent.

Then read the body to check that every method and result judgment is supported, that specific numerical values are absent from the abstract, and that the logical chain is complete. Check smooth, logically accurate connectors and the target journal's known length requirements.

For revisions, propose changes and obtain approval before applying them. Include four parts: the complete original abstract, the complete revised abstract, the rationale, and supporting passages from the body. Add translations only when requested.

Stay within the hard length limit.
