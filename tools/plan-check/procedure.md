# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Determine the mode. In live mode, read `scope.md`, confirm the issue is in the scoped repository, note the Path Review house rules, then read `voice-guide.md`. In eval mode, use only the bundle and do not use either file.
2. Read `rubric.md` and the evidence guide before the package. Record every check, its weight, and the verdict rule so no check is skipped.
3. Read the issue context and repo facts first. Record the requested behavior, explicit constraints, contribution rules, disclosure policy, and facts the issue states without yet accepting a proposed solution.
4. Read the thread highlights or live thread next. Record maintainer direction, rejected or preferred approaches, linked work, and decisions made after the issue body.
5. Read the complete repro evidence before the candidate plan. Record the exact trigger, observed failure, controls, outputs, environment qualifications, and what those artifacts establish or rule out. This order prevents the plan's diagnosis from biasing the evidence reading.
6. Read the candidate plan and then its comment. Record the diagnosis, bounds, files or areas, implementation sequence, test observables, risks, unknowns, deviations, and any differences between the full plan and comment. Do not grade until the whole package has been read.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For diagnosis grounding, pair each causal claim in the diagnosis or approach with the repro artifact that supports it. Separately list every control or output that rules out a layer or cause. If no cause is confirmed, record the plan's hypothesis, verification step, and bounded follow-up action.
2. For scope, make two lists from the plan: work necessary for the reproduced issue and additional work. Check every additional migration, refactor, option, cleanup, adjacent fix, or platform expansion against the issue, evidence, and thread for a stated necessity; record explicit exclusions.
3. For executability, extract the first work step, named files or code areas, intended behavior change, order of later steps, and every choice postponed until build time. Mark any materially different alternatives for which the plan supplies no decision rule.
4. For testing, map every planned test to the original trigger and failure. Record the exact command or scenario, the changed code path it exercises, and the expected observable after the fix. Distinguish focused proof from broad suites and subjective checks.
5. For honesty, list claims whose certainty exceeds the evidence, acknowledged risks and unknowns, how each build-blocking unknown will be resolved, and any deviation with its reason. Treat a clear statement that no deviation occurred as evidence, not as a missing deviation.
6. For communications, compare the plan and comment with maintainer instructions, linked work, templates, contribution policy, AI-use policy, and Path Review house rules. Record the exact requirement and the comment text that satisfies or misses it. Also compare the comment's promises with the full plan.
7. In eval mode, quote or precisely cite only facts present in the bundle sections named by the evidence guide. In live mode, gather issue-side facts from the GitHub issue, thread, linked work, and repository documentation, while treating `plan.md` and `comment.md` as the complete candidate-side evidence.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute checks in rubric order using only the evidence gathered for that row; do not compensate for a failed check with strength elsewhere.
2. Apply every clause of each pass condition. Grade `pass` only when the evidence satisfies it, `fail` when evidence violates it, and `unclear` only when the named evidence is genuinely absent or insufficient after all mapped locations were checked.
3. Write one concise deciding fact or quote with every grade. For a pass, name the strongest observable fact. For a fail, name the contradiction, excess work, deferred choice, non-observable test, hidden uncertainty, ignored direction, or unmet convention. For `unclear`, name the missing evidence and where it should have appeared.
4. Re-read only the relevant mapped sections when gathered facts conflict. Resolve conflicts in this order: reproduced artifacts over unsupported diagnosis; later explicit maintainer direction over earlier suggestions; repository policy over generic comment practice; the full candidate plan over a shorter comment for implementation detail, while still grading omissions that the comment itself must communicate.
5. Do not fail a terse plan for length or headings. Do not pass a polished plan because it names many files or tests. Grade the planned outcome and whether the evidence makes it buildable.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Confirm every rubric row has exactly one `pass`, `fail`, or `unclear` grade and a one-line evidence fact.
2. Apply the verdict rule mechanically: return `accept` only if all required checks pass; return `reject` if any required check fails or is unclear. Never let a preferred check alter the verdict.
3. In the readable summary, show a line per check and, in live mode, quote any broken voice-guide rule. For a rejection, lead with the first failing required check in rubric order and include its deciding evidence; include all other failures so the author can revise once.
4. Emit the required fenced JSON object last, with the issue URL or bundle id, every check and grade, its deciding one-line evidence, and the binary verdict. Output nothing after the JSON fence.
