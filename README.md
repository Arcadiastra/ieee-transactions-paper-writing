# IEEE Transactions Paper Writing Skill

A skill suite for planning, drafting, revising, and reviewing IEEE Transactions papers.

Organize the paper around contributions and mechanisms, with affirmative phrasing, clear sentence logic, cross-section coherence, and qualitative interpretation of experimental results. The suite contains one main skill and seven section skills.

Although this is an agent writing skill, authors are encouraged to draw on its principles and **write the initial draft themselves**. This skill advocates using AI to assist with planning, organization, translation, revision, and polishing, rather than delegating the entire writing process to AI.

**Writing is thinking; the draft embodies the logic.**

> *Although using AI to polish a manuscript is fine, the writing will become irrelevant when too much AI is applied.*

## Scope

- Build paper outlines, draft sections, revise and review manuscripts, verify references, and control length.
- Reuse the writing conventions and citation tooling of [ieee-transactions-writing-zh](https://github.com/Arcadiastra/ieee-transactions-writing-zh), with distinct skill names and localized documentation.

## Installation

Copy the entire `ieee-transactions-writing` folder into the skills directory of your agent, retaining all subdirectories:

| Agent | macOS / Linux | Windows |
| --- | --- | --- |
| Codex | `~/.agents/skills/` | `%USERPROFILE%\.agents\skills\` |
| Claude Code | `~/.claude/skills/` | `%USERPROFILE%\.claude\skills\` |

### Verify Installation

Reload skills or restart the agent, then invoke the main skill:

Codex:

```text
$ieee-transactions-writing
```

Claude Code:

```text
/ieee-transactions-writing
```

## Structure and Entry Points

```text
ieee-transactions-writing/
|-- SKILL.md
|-- README.md
|-- LICENSE
|-- agents/openai.yaml
|-- assets/templates/
|-- references/template-guide.md
`-- subskills/
    |-- abstract/
    |-- introduction/
    |-- problem-definition/
    |-- methodology/
    |-- results-and-discussions/
    |-- conclusion/
    `-- citation/
        |-- SKILL.md
        |-- agents/
        |-- assets/
        |-- scripts/
        |-- tests/
        `-- references/
```

Each section skill has its own instructions, UI metadata, and outline template.

| Entry | Responsibility |
| --- | --- |
| [Main skill](SKILL.md) | Workflow, argument structure, shared rules, acceptance |
| [Abstract](subskills/abstract/SKILL.md) | Abstract and Index Terms |
| [Introduction](subskills/introduction/SKILL.md) | Motivation, gaps, and contributions |
| [Problem definition](subskills/problem-definition/SKILL.md) | Formulation, notation, and difficulties |
| [Methodology](subskills/methodology/SKILL.md) | Mechanisms, theory, and method figures |
| [Results and discussions](subskills/results-and-discussions/SKILL.md) | Setup, visuals, and qualitative interpretation |
| [Conclusion](subskills/conclusion/SKILL.md) | Synthesis, significance, and future work |
| [Citation](subskills/citation/SKILL.md) | Claim support, metadata, and reference formatting |

## Usage

```text
$ieee-transactions-writing Review the paper structure and contribution chain. Propose changes without editing the manuscript yet.

$ieee-transactions-writing-abstract Revise the abstract using the paper's actual findings. Show the original, revision, and rationale.

$ieee-transactions-writing-results-and-discussions Check whether the discussion connects the results to the problem and mechanisms without repeating figure values.
```

If the host does not discover nested skills independently, use the main skill to route the task or provide the relevant file path. All eight skills include `agents/openai.yaml` metadata.

## Citation Tools

Three read-only entry points provide offline BibTeX/AUX checks, Crossref/DataCite metadata verification, and Crossref publication-update checks. Reports retain citation keys, input hashes, and source evidence.

An optional **Bibverify 0.5.0 CLI** backend runs in a separate environment with `--dry-run --json`; the built-in metadata script remains the fallback.

- [Installation, commands, exit codes, and statuses](subskills/citation/references/tools.md)
- [Bibverify integration](subskills/citation/references/bibverify-integration.md)
- [Full-text claim-support review](subskills/citation/references/integrity-review.md)
- [Tool comparisons and template decisions](subskills/citation/references/source-comparison.md)

## Metadata and Tools

Every `SKILL.md` includes `name`, `description`, `license`, `allowed-tools`, and `metadata`.

- `metadata.trigger` describes the intended task; it is not a standardized activation switch.
- `metadata.target-venue` is `IEEE Transactions journals`.
- `metadata.language` is `en`.
- `metadata.source_repository` identifies the source suite.
- `allowed-tools` lists conventional file, shell, and search tool names. The main and abstract skills also list `Task` for independent review.

Tool names and support vary across hosts. Metadata does not grant execution permissions. Where PowerShell is required, use `pwsh`, strict error handling, and explicit UTF-8 text encoding.

## Writing Conventions

The abstract contains no specific numerical values, and results prose does not repeat figure/table values. Organize the body around problems, mechanisms, and evidence. The default full-paper budget is 10 pages, adjusted for the venue and the user's requirements. Section skills define length budgets, citation conventions, and revision approval requirements.

## License

Licensed under the [MIT License](LICENSE).
