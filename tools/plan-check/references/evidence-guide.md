# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives:** In an eval bundle, read the candidate plan's diagnosis and approach against the repro-evidence block's commands, outputs, controls, and conclusion, then use relevant issue and thread facts. In live mode, compare `plan.md` with the student's posted Unit 2 repro comment (or the quoted house repro pack), the issue body, and later maintainer comments. The candidate drafts must quote the repro facts they rely on; unquoted local investigation is not package evidence.

**What good looks like:** Every causal claim explains the observed trigger and survives the supplied controls. When the evidence narrows but does not prove the cause, the plan labels a hypothesis and begins with a concrete discriminating check whose outcomes lead to a bounded change. A diagnosis is not grounded when a control rules it out, it skips a decisive earlier-stage failure, or it proposes masking the visible symptom while ignoring the evidenced cause.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives:** In an eval bundle, inspect the plan's scope, proposed changes, files/areas, approach, risks, and explicit exclusions against the issue request, repro evidence, and thread direction. In live mode, use the same parts of `plan.md` and `comment.md` against the live issue and repro comment.

**What good looks like:** The plan contains one coherent issue-sized fix and the regression coverage needed to prove it. It excludes or convincingly justifies adjacent cleanup. Unrelated migrations, broad abstractions, new options, UI work, platform expansions, and "while here" refactors are scope creep when the issue can be fixed without them; listing them as files does not make them necessary.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives:** In an eval bundle, use the candidate plan's named files/areas, approach, ordered implementation steps, risks, and unknowns, with repo facts or thread locations that identify the relevant code. In live mode, inspect those draft sections plus repository paths and contribution docs. Do not require a heading; find the substance wherever it appears.

**What good looks like:** A stranger knows the first file or subsystem to inspect, the behavior or invariant to change, and the sequence for implementing and validating it. A narrow investigation step is executable when it names the exact question, how to answer it, and the bounded action for each relevant outcome. "Profile and optimize," "add a guard somewhere," or choosing between different libraries or layers during the build is not executable.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives:** In an eval bundle, compare the plan's test plan with the repro-evidence block's exact trigger, inputs, controls, commands, output, and failure artifact. In live mode, compare the planned commands and expectations with the posted repro evidence and the real changed code path. Repository test conventions in repo facts or docs establish where regression coverage belongs.

**What good looks like:** The plan reruns the original reproduction, or turns its inputs into a focused test through the real code, and names the observable result after the fix (exit status, exact state, output, timing threshold, absence of a specific panic, or another falsifiable signal). Focused regression coverage plus relevant broader checks is strong. Only running a full suite, saying it should work or feel better, or testing a stand-in that bypasses the changed path does not prove the fix.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives:** In an eval bundle, compare the diagnosis and approach with the plan's risks, unknowns, conditional steps, and Deviations section, and with ambiguity in the repro evidence or thread. In live mode, inspect the same locations in `plan.md` before and after the build and compare any changed approach with the posted comment.

**What good looks like:** The plan distinguishes observations, inferences, and unresolved questions. Any unknown that could change the implementation layer has a concrete resolution step before editing proceeds; minor checked unknowns may remain. After the build, Deviations states what changed and why, or states in the author's own words that implementation followed the plan. False certainty, silently deferred core decisions, or a blank Deviations section is not honest evidence.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives:** In an eval bundle, read the candidate plan and plan comment against thread highlights, linked or prior work, and the repo-facts block's templates, contribution policy, and AI-use policy. In live mode, inspect the complete GitHub thread, linked issues or pull requests, repository contribution docs/templates, `scope.md`, and both drafts. Apply `voice-guide.md` separately as a live-mode writing check.

**What good looks like:** The comment addresses explicit maintainer direction, coordinates with overlapping work, and explains any evidence-based departure instead of acting as though the thread is empty. It is a self-contained plan in the student's own words and follows all stated repository rules, including an AI-use disclosure whenever required. Its diagnosis, scope, and promised validation agree with the full plan and avoid guarantees the evidence cannot support.
