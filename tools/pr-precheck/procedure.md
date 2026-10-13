# Procedure: how this tool grades a PR package

## Read order

1. Determine live or eval mode. In live mode, read `scope.md`, validate the target repository, note its house rules, then read `voice-guide.md`. In eval mode, use only the bundle and skip both files.
2. Read `rubric.md` and `references/evidence-guide.md`. Record every row in order, its weight, and the verdict rule before reading the candidate.
3. Read the issue and complete thread, followed by repo facts, the PR template, and contribution policy. Record the requested outcome, explicit maintainer direction, applicable checks, required description content, and disclosure rules.
4. Read the accepted plan context before the candidate PR. Extract the intended scope, exclusions, files, promised behaviors, test plan, risks, and all deviation notes. This prevents the PR's description from redefining the baseline after the fact.
5. Read the commit list and entire diff before the description. Inventory every changed file and substantive hunk, including apparent debris or missing planned work. The diff is authoritative for what was delivered.
6. Read the title and description, then the complete test evidence. Record each delivery claim, disclosed shortfall, template response, checked box, command, result, before/after observable, and unreported plan case. Do not grade until all sections are read.

## Evidence gathering

1. For plan fidelity, build a two-column map: each planned file/behavior to its diff hunk, and each diff file/hunk back to a plan item or a deviation stating what changed and why. Mark planned items with no implementation and diff items with no authorization. Compare every description claim with that map.
2. For test evidence, list the reproduction's original trigger, failure observable, controls, and expected after-state. Require a captured before/after contrast or equivalent focused regression for that primary failure. Map secondary delivered behavior and each non-deferred test-plan case to a specifically named observed outcome or focused test result; do not demand a duplicate transcript when the outcome is falsifiable. Record whether the evidence travels through the changed path rather than a control.
3. For repository checks, list each command or suite the repo explicitly requests. Beside it record the exact reported outcome, expected no-tests condition, failure explanation, or supported inapplicability reason. Compare this list with all checked boxes and testing claims.
4. For diff quality, inspect every added and removed line, not only filenames or the description. Record unrelated changes and concrete debris signals: debug output, commented-out attempts, dead code, TODOs, artifacts, duplicated blocks, format/import churn, or sweeping rewrites. Use commits only as a pointer back to the diff.
5. For standards, list every applicable template, policy, and thread ask, then quote the candidate response and verify any promised file, test, changelog, or release note in the diff. Treat all eval packages as AI-assisted when the bundle says the repo requires disclosure. In live mode, apply the actual policy and the course-required AI-use disclosure.
6. For reviewer clarity and live voice, compare the title and description with the completed maps. Record misleading certainty, omitted material limitations, or broken voice-guide rules separately from universal rubric grades.

## Check execution

1. Execute checks in rubric order using the gathered evidence assigned to that row. Do not trade a strong check against a weak one.
2. Apply every clause of the pass condition. Grade `pass` only when the package establishes the condition, `fail` when a fact violates it, and `unclear` only after every mapped location has been checked and the necessary fact is genuinely absent or ambiguous.
3. Write one concise deciding evidence line for every grade. For a pass, cite the strongest observable pairing. For a fail, cite the first concrete contradiction or omission under that row. For unclear, name the missing fact and its expected location.
4. When evidence conflicts, prefer the diff for delivered scope, captured output for test outcome, the plan plus explicit deviations for intended scope, and repository policy for standards. A description cannot override a contradictory diff or output.
5. Re-read only the mapped source when a conflict needs resolution. Never infer that a command ran, an unshown path passed, or a required artifact exists.
6. Do not fail an honestly re-scoped package merely for delivering less. Verify that the deviation is explicit in the plan context, repeated where material in the description, and that the delivered remainder is evidenced. Hidden or falsely claimed omissions fail fidelity.

## Verdict assembly

1. Confirm that each rubric row has exactly one grade and one evidence line.
2. Apply the verdict rule mechanically: accept only if all required rows pass; reject if any required row fails or is unclear. Preferred rows never alter the result.
3. In a rejection summary, lead with the first failing or unclear required check in rubric order, then list the remaining rows so the author can revise in one pass. In an acceptance summary, list the strongest evidence for each required row.
4. In live mode, append any title/description voice-guide violations to the readable summary without changing the verdict unless the rubric independently fails them.
5. Emit the required fenced JSON object last with the PR URL or bundle id, all checks in rubric order, their grades and one-line evidence, and the binary verdict. Output nothing after the closing fence.
