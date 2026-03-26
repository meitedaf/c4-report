---
name: c4-report
description: Draft Code4rena-ready vulnerability submissions from validated findings. Use only when the user explicitly invokes `$c4-report` to write, rewrite, compress, or standardize a smart-contract finding for C4/C4rena.
---

# C4 Report

## Overview

Turn a confirmed vulnerability into a submission that matches the Code4rena form.
Write only the fields the form expects and keep the wording concrete, source-backed, and exploit-focused.

## Workflow

1. Confirm the issue boundary.
Use one finding per root cause. Merge variants such as `expired`, `not-yet-valid`, and `future timestamp` when they are manifestations of the same missing validation.

2. Ground every claim in code.
Collect root-cause links from the public GitHub repo when available. Prefer the smallest line ranges that fully show:
- the missing check
- where unsafe state is stored or trusted
- where the unsafe value is later consumed

3. Separate root cause from impact.
State:
- what the code does
- what check is missing
- how that reaches an exploitable or economically relevant outcome
Do not rely on deployer intent or vague “could be dangerous” language.

4. Keep mitigation narrow.
Recommend the smallest fix that closes the cited issue. If multiple checks are needed, list them explicitly.

5. Include a complete PoC when requested.
Provide:
- where the PoC code should be inserted
- the exact code block
- any helper code block
- brief comments inside the PoC or a short explanation around it describing what each step proves
- the exact `forge test` command to run
Keep the exploit minimal but functional.

## Output Format

Write the report with exactly these labels unless the user asks for a subset:

`Severity rating`

`Title *`

`Links to root cause *`

`Vulnerability details *`

Inside `Vulnerability details *`, use these two subheaders:
- `## Finding description and impact`
- `## Recommended mitigation steps`

`Proof of Concept (PoC) *`

## Writing Rules

- State the title as one sentence under 255 characters.
- Use plain English and short paragraphs.
- Prefer “The contract does X and never checks Y” over abstract wording.
- In `Links to root cause *`, use GitHub links with line numbers.
- In `Proof of Concept (PoC) *`, explain exactly where the code should be placed using GitHub links when a public repo path is available.
- Add short explanatory comments in PoC code, or a short paragraph immediately before the code block, so the reader can see what the PoC is proving.
- If the PoC proves multiple manifestations of one root cause, explain that in one finding instead of splitting it.
- Do not add sections that the C4 form does not have.
- Do not add CVSS, matrices, timelines, or audit-summary filler.

## Root-Cause Checklist

Before finalizing, confirm all of the following:

- The title matches the actual root cause, not just one symptom.
- Every impact claim is reachable from the cited code.
- The GitHub links point to the sponsor repo, not local paths.
- The mitigation addresses the cited root cause.
- The PoC code is runnable with one explicit command.
- The PoC placement instructions use repo links instead of local filesystem paths whenever possible.

## PoC Checklist

When including exploit code, ensure the PoC:

- compiles in the current repo
- uses the repo's existing test harness when possible
- proves the incorrect behavior with assertions or expected reverts
- avoids unnecessary setup unrelated to the issue
- includes short comments or surrounding explanation describing what the code does and what it proves
- names the insertion point clearly using public repo links when possible
