---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about one PR package: is it ready to submit? Treat the package as the candidate title, description, commits, diff, and test evidence, read against the accepted plan (including deviations), its issue, and the repository's stated standards. Do not review a different change, suggest a replacement implementation, or grade from general impressions.

## Inputs and modes

Determine the mode before gathering evidence.

- **Live mode:** Read the issue URL named by the invocation; `plan.md`, including `## Deviations`; the committed branch diff produced by `git diff main...HEAD` from the working copy; the draft title and description in `pr_draft.md`; and the captured results in `test_evidence.md`. Read the complete live issue thread and the repository's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. The three-dot diff is the candidate change; do not substitute uncommitted working-tree changes. For a house-chain submission, read the supplied house plan and house repro pack in place of the student's own plan and reproduction, then apply the same checks.
- **Eval mode:** Read the supplied package bundle only. It is the whole world: do not fetch URLs, inspect a checkout, or introduce outside facts. Read its issue context, thread highlights, repo facts, plan context, and every candidate-PR field. Run every rubric check and the full verdict rule.

Grade only one package per invocation.

## The scope seam (live mode only)

In live mode, read `scope.md` before any candidate artifact. Confirm that its `Repo:` line is filled and that the issue and intended PR base repository match it. Apply every Path Review house rule recorded there. If the repo line is still a bracketed placeholder, stop without grading and tell the student to fill it. If the package targets another repository, refuse to grade and identify the mismatch. Never guess scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after scope and check both the draft PR title and description against it. Report each broken rule in the readable summary and quote the rule. The voice guide changes the verdict only if a row in `rubric.md` expressly uses it; otherwise it is feedback. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read `rubric.md` for the complete check table, weights, and verdict rule. Read `references/evidence-guide.md` to locate each evidence family and recognize a sufficient observable. Execute `procedure.md` exactly as written for read order, evidence pairings, check grades, and verdict assembly.

If either `rubric.md` contains no filled check or `procedure.md` contains no concrete step, refuse to grade and name the empty component. If the procedure is silent on an operation, report that gap rather than inventing a step. Do not add runtime checks or exceptions that the rubric does not state.

## Verdict and output

Use only `accept` (ready to submit) or `reject` (hold). Give a compact readable per-check summary first. End with the following fenced JSON block, valid and last, with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Put evidence first. Give every grade one precise fact, quote, command result, or file comparison that decided it; “looks good” is not evidence.
- Grade the delivered change, not its length, confidence, prose polish, number of commits, or heading count. A terse complete package can pass, while a polished package that contradicts its diff fails.
- Let the rubric decide. Apply each written pass condition even when intuition differs; change the rubric later rather than moving the bar during a run.
- Let the procedure decide how. Follow it as written and expose gaps instead of silently compensating for them.
- Apply the rubric's explicit treatment of `unclear`. If it is ever silent, count unverifiable evidence as a failure: a package that cannot be checked is not ready to submit.
- Treat an honestly disclosed, re-scoped shortfall according to the plan's deviation notes and description; do not fail merely because the delivered scope is smaller than the original idea. Do fail a shortfall that is hidden or contradicted by a fidelity claim.
