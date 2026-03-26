# C4 Report

`C4 Report` is a Codex skill for turning a validated smart-contract vulnerability into a Code4rena-ready submission.

It is designed for the last mile of audit writing: once the issue is already confirmed, the skill helps structure the report around root cause, impact, mitigation, and PoC format without adding generic audit filler.

## What It Does

- Converts one confirmed issue into one Code4rena-style finding.
- Keeps the report aligned with the standard C4 submission fields.
- Pushes the writer toward code-backed claims and narrow mitigations.
- Encourages PoCs that are minimal, runnable, and clearly explained.

## Repository Layout

```text
C4_Report/
├── SKILL.md
├── README.md
├── LICENSE
└── agents/
    └── openai.yaml
```

## Files

- `SKILL.md`: the main skill instructions and writing workflow.
- `agents/openai.yaml`: metadata used to surface the skill in a Codex-compatible environment.

## Usage

Invoke the skill with:

```text
$c4-report
```

Example prompt:

```text
$c4-report
Turn this validated issue into a Code4rena-ready submission. Keep one root cause per finding, include GitHub root-cause links, and add a runnable Forge PoC.
```

## Expected Output Shape

Unless a subset is requested, the skill writes these sections:

- `Severity rating`
- `Title *`
- `Links to root cause *`
- `Vulnerability details *`
- `Proof of Concept (PoC) *`

Inside `Vulnerability details *`, it uses:

- `## Finding description and impact`
- `## Recommended mitigation steps`

## Writing Principles

- One finding per root cause.
- Claims should be grounded in code, preferably with GitHub line links.
- Impact should be separated from root cause.
- Mitigations should be as narrow as possible.
- PoCs should be runnable, minimal, and explicit about what they prove.

## Best Fit

This skill is useful when:

- the vulnerability is already validated
- the remaining task is report drafting or cleanup
- the target format is Code4rena or a very similar contest report

This skill is not meant to replace triage or vulnerability discovery.

## Installation

Place this folder in your Codex skills directory:

```text
~/.codex/skills/c4-report
```

If your environment uses a different skill path, adjust accordingly.

## Open Source Notes

This repository contains prompt and metadata files only. It does not include private findings, sponsor code, or proprietary audit content.

## License

MIT
