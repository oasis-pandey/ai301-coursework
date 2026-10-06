# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis_grounded | The candidate plan's diagnosis and approach, read against the repro-evidence block's commands, outputs, controls, and stated result and against relevant issue/thread facts. | Pass if the proposed cause or causal boundary explains the reproduced behavior and does not contradict a supplied control or artifact. A plan may state a bounded hypothesis instead of a confirmed cause only when it names that uncertainty and makes verification the first executable step. Fail when the evidence rules out the proposed cause, the plan ignores decisive evidence, or the chosen change only masks a symptom while the evidence locates an underlying cause. | required |
| scope_bounded | The candidate plan's in-scope and out-of-scope statements, proposed changes, files/areas, and approach, read against the issue, repro evidence, and thread direction. | Pass if the work is one coherent change needed to address the reproduced issue, with unrelated migrations, redesigns, options, cleanup, and adjacent fixes explicitly excluded or justified as necessary. Fail if the issue-sized fix is bundled with drive-by work or a broad redesign that is not required by the evidence. | required |
| approach_executable | The candidate plan's files/areas, approach, ordering, and unresolved decisions, read with repo facts and the locations implicated by the repro or thread. | Pass if a contributor unfamiliar with the draft can identify where to start, what behavior to change, and the concrete implementation path without first choosing among materially different layers or solutions. A narrow verification step may precede editing, but the plan must say what fact it will resolve and what bounded action follows. | required |
| test_decisive | The candidate plan's test plan read against the repro-evidence block's trigger, controls, commands, artifacts, and observed failure. | Pass if the tests rerun or faithfully convert the reproduction through the real changed code and name an observable post-fix result that distinguishes success from the original failure; include focused regression coverage where practical. Fail for only a broad suite, subjective outcomes such as “feels faster,” or checks that do not exercise the reported behavior. | required |
| uncertainty_honest | The diagnosis, risks, unknowns, conditional steps, and Deviations section read against gaps or conflicts in the repro evidence and thread. | Pass if material unknowns are labeled rather than asserted as facts, each build-blocking unknown has a concrete way to resolve it, and any recorded deviation says what changed and why. No unknowns or deviations is acceptable when the supplied evidence fully supports the bounded approach and the plan says so. | required |
| thread_direction | The candidate plan and plan comment read against issue requirements, thread highlights or live maintainer comments, linked/prior work, and explicit requested direction. | Pass if the proposed work acknowledges and follows explicit maintainer direction, or clearly explains a relevant evidence-based departure, and coordinates with linked or overlapping work instead of silently racing or ignoring it. Pass when no relevant direction or overlap exists. | required |
| repo_conventions | The candidate plan comment read against the repo-facts block or live repository contribution rules, templates, and AI-use policy, plus applicable Path Review house rules in live mode. | Pass if the comment is a self-contained plan in the student's own words and satisfies every applicable repository-specific requirement, including an AI-use disclosure when the stated policy requires one. Fail when a required disclosure or contribution convention is omitted. | required |
| comment_clarity | The candidate plan comment read against the candidate plan, issue, and repro evidence. | Pass if the comment accurately summarizes the grounded diagnosis, bounded intended change, and observable validation without overpromising or contradicting the full plan. | preferred |

## Verdict rule

Return `accept` only when every required check passes. Return `reject`
when any required check fails or is `unclear`; missing evidence for a
required check is not readiness. Preferred checks identify improvements
but never change the verdict, and an `unclear` preferred check is treated
the same as a failed preferred check for feedback only.
