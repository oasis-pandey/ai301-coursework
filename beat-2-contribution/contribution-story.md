# Contribution: vis.js timeline rounding off timeAxis.step

Path: `beat-2-contribution/contribution-story.md`

**Contribution Number:** [1]
**Student:** Oasis Pandey
**GitHub Username:** oasis-pandey
**Issue:** https://github.com/visjs/vis-timeline/issues/1030
**Pull Request:** https://github.com/visjs/vis-timeline/pull/2150


---

## Toolkit

These entries are organized by course unit. All work recorded here was completed on November 5, 2026; the entries are not backdated. Tool files and logs remain local for the Unit 9 portfolio.

**Unit 5: Searching broadly and checking the scout against live evidence**

2026-11-05: I upgraded issue-select to issue-scout, preserved my fit profile and rubric, and wrote four open-issue queries for Python, Java, JavaScript, and TypeScript with explicit ranking rules and a five-issue grading limit. The first scan accepted three issues and rejected two, but its fewest-comments/newest-first ranking favored newly created repositories, and my activity-based repo-in-use check was too weak. I added a two-per-repository ranking cap, strengthened the shared-use evidence, and added an open-issue check after finding a closed issue still listed on the course site. GitHub sign-in and an expired Claude session initially blocked the live runs; reauthentication resolved both, and I saved the actual scan and three course-site issue grades instead of treating failed runs as evidence.

**Unit 6: One voice guide, guarded claim, and focused repository memory**

2026-11-05: I merged the differing Unit 2–4 voice guides into one canonical guide, retaining added rules and the latest wording, then added concrete rules and wrong/right examples for claims, questions, and pings. I installed the voice guard, linked all three checking skills to that guide, and wrote a local memory file from CONTRIBUTING.md and one scoped Claude orientation of TimeStep and its tests. The bodyless-comment wiring test stopped as expected, and the guard log recorded a pass when my actual claim was posted. Repro-check warned that my first draft's wording could imply a promised PR by November 7, so I changed that promise to an update on what I found.

**Unit 7: A manifest and gate for the committed branch**

2026-11-05: I installed ship-gate and wrote a manifest that builds the package before running tests, lint, and formatting. The initial suite failed on the packaging snapshot until I built the bundles, so I made that setup dependency explicit instead of excluding the check. My Unit 4 checker also assumed main, a sandbox Repo line, and docs/CONTRIBUTING.md; I updated those live-mode seams to honor the wild scope, master, and the root contribution guide. The gate passed the repository and PR-rubric checks, and its voice feedback led me to simplify the AI disclosure and rerun the gate for the final description.

**Unit 8: A review playbook and a wait decision from the PR monitor**

2026-11-05: I installed the PR monitor and filled all four playbook sections from the repo's rules and a five-PR outside-contributor review sample, choosing 21 quiet days before one nudge. The sample's median first human response was 8.85 days, with a 1.75–33.70 day range. The console called its template a polite-nudge form, which was confusing, but the actual MOVE was “No nudge yet; wait note” for my newly opened PR with no comments or reviews and one pending check. I compared the draft with the live thread and my threshold, kept it local, and posted nothing; no threshold change was needed because the actual decision followed the playbook.

---

## Why I Chose This Issue

I began with my existing Python, Java, JavaScript/TypeScript, Git, and web-development fit profile. My four GitHub queries searched open good-first issues with 100 results each; the first five-issue scan accepted three and rejected two. That did not produce a good final pick: the ranking favored freshly created, low-comment repositories, and one repository supplied three of the five candidates. I added a two-per-repository cap, required evidence of an active human and shared interest for repo-in-use, and added an explicit open-issue check after finding a closed issue in the course list. My first three course-site picks—Meteor #14910, #14918, and #14924—were all rejected because existing PRs already covered them, even though their issue comment threads were empty. That was a useful success of the scout's claim check rather than a reason to override it.

I broadened the course site's Tag filter to bug while retaining my four language filters, then inspected visjs. I directly graded vis-timeline #1030, #1275, and #1315: the scout accepted the first two and rejected #1315 because PR #1701 already covers it. It ranked #1275 ahead of #1030, but I chose #1030 because I could reproduce a precise numeric failure on current master and trace it to one iterator branch. The scout called it ambitious: the open question was whether explicit intervals or major-unit alignment should take precedence. I raised that exact question in my [claim comment](https://github.com/visjs/vis-timeline/issues/1030#issuecomment-6670906850) and proposed preserving automatic rounding while correcting explicit millisecond steps. I also reserved #1030 on the course site, which lists it as my one claimed issue. This fits my goal of improving debugging and regression testing in existing JavaScript code; the verdict is evidence, not proof that the maintainer has approved the design.

**Toolkit**

- Tool: issue-scout through Claude Code; I ran the five-issue scan, graded three Meteor site picks, regraded them after the Unit 6 patch, and graded three replacement visjs site picks.
- What it produced: three accepts/two rejects in the scan, three Meteor rejects for existing PRs, and two accepts/one reject among the visjs picks; #1030 accepted with an ambitious difficulty note.
- Difficulties: fewest-comments/newest-first ranking overvalued new repos, a recent commit alone did not establish shared use, and a two-human-author rule then overcorrected against an established repo with many bot commits.
- What changed: capped candidates per repository; required a non-archived repo, recent human activity, and either shared-interest or multiple-human evidence; added issue-open; replaced bounded-scope with the required scope-feasible row and difficulty note. The saved output and dated notes preserve each actual run and change.

---

## Understanding the Issue

**Problem Description**

An explicitly configured millisecond axis step can lose part of its interval when TimeStep crosses a second boundary. A timeline used for evenly spaced audio bars can therefore display the wrong spacing even though the caller supplied a fixed step.

**Expected Behavior**

Without a hidden-date jump, successive explicit 3500 ms ticks should advance by exactly 3500 ms. Automatic scale selection and its existing alignment should retain their current behavior.

**Current Behavior**

On master fec1bfe, requesting 3500 ms produces successive 3000 ms increments. A 1500 ms request becomes 1000 ms, and a 350 ms request has a shortened 300 ms boundary interval; the 250 ms control stays correct.

**Affected Components**

lib/timeline/TimeStep.js (setScale and next), its test/TimeStep.test.js regression suite, the timeAxis options in docs/timeline/index.html, and the new fixed-millisecond example. TimeAxis uses this iterator to generate labels; no separate browser-rendering cause is being claimed.

**Toolkit**

- Tool: a scoped Claude Code orientation, direct source reading, and a Node reproduction of the real TimeStep class.
- What it produced: the causal chain from setScale disabling autoScale to next adding the interval and then clearing its remainder; automatic steps all divide 1000.
- Difficulties: the old thread identifies the rounding but explicitly questions whether deleting it is safe; a numeric iterator test alone does not prove browser rendering.
- What changed: narrowed the proposed fix to explicit millisecond stepping, retained the automatic branch, and included a runnable example and regression controls.

---

## Reproduction Process

**Environment Setup**

macOS 15.7.7, Node 24.21.0, npm 11.19.0; unchanged master fec1bfe3bdfcd54cdde16eb71cc252d3d7b05c82. I cloned the repository and ran npm ci. The initial full-suite Package/Exported files snapshot failed because generated bundles were absent; after npm run build, all 98 baseline tests passed, as did lint and formatting. The numeric reproduction imports the real source and installed Moment dependency and needs no browser or service after installation.

**Steps to Reproduce**

1. Prepare the exact source and dependencies:

```sh
git clone https://github.com/visjs/vis-timeline.git
cd vis-timeline
git checkout fec1bfe3bdfcd54cdde16eb71cc252d3d7b05c82
npm ci
```

2. From that checkout root, run:

```sh
node --input-type=module <<'JS'
import TimeStep from "./lib/timeline/TimeStep.js";
const start = new Date("2026-01-01T00:00:00.000Z");
for (const size of [250, 350, 1500, 3500]) {
  const step = new TimeStep(start, new Date(start.valueOf() + 30000));
  step.setScale({ scale: "millisecond", step: size });
  step.start();
  const times = [step.getCurrent().valueOf()];
  for (let i = 0; i < 4; i++) { step.next(); times.push(step.getCurrent().valueOf()); }
  console.log(JSON.stringify({requestedStep: size, offsets: times.map(t => t - start.valueOf()), deltas: times.slice(1).map((t,i) => t-times[i])}));
}
JS
```

3. Compare each requestedStep with its observed deltas. The 3500 ms case produces 3000 ms steps, matching the issue; the 250 ms case is the control.

**Reproduction Evidence**

- **Commit showing reproduction:** none; the before-run used unchanged [master fec1bfe](https://github.com/visjs/vis-timeline/commit/fec1bfe3bdfcd54cdde16eb71cc252d3d7b05c82).
- **Screenshots/logs:** actual output from that source:

```json
{"requestedStep":250,"offsets":[0,250,500,750,1000],"deltas":[250,250,250,250]}
{"requestedStep":350,"offsets":[0,350,700,1000,1350],"deltas":[350,350,300,350]}
{"requestedStep":1500,"offsets":[0,1000,2000,3000,4000],"deltas":[1000,1000,1000,1000]}
{"requestedStep":3500,"offsets":[0,3000,6000,9000,12000],"deltas":[3000,3000,3000,3000]}
```

- **My findings:** next adds the requested milliseconds, then clears a positive millisecond remainder smaller than the step. That discards 500 ms from the reported 3500 ms case. This is an iterator reproduction, not a claim that I reran the original JSFiddle or verified browser layout.

**Toolkit**

- Tool: repro-check through Claude Code, checking the local claim and complete reproduction report against the live issue and my voice guide.
- What it produced: accept for the claim-only draft and accept for the full package; each required reproduction check passed.
- Difficulties: the checker could inspect and hand-trace the source but could not independently run the script with its read-only tool permissions; it also noted that the report's baseline-suite claims lacked their own pasted output.
- What changed: retained the actual executed reproduction output, included the exact environment and full script here, and kept the full report local as the course directs. The PR/testing section will carry the actual check outcomes; the checker verdict does not substitute for running tests.

---

## Solution Approach

**Analysis**

In lib/timeline/TimeStep.js, TimeStep.next()'s millisecond case adds the configured step, but a later reset clears a positive remainder smaller than that step. Adding 3500 ms produces 3.500 seconds and the reset turns it into 3.000 seconds. setScale marks an explicit scale with autoScale=false. Automatic millisecond steps are 1, 5, 10, 50, 100, and 200, all divisors of 1000. The root cause is the post-addition reset, not Moment's addition or browser drawing.

**Proposed Solution**

Add this.autoScale to the millisecond reset condition. Explicit millisecond scales then keep their requested elapsed interval; automatic rounding stays in place. Preserve initial tick alignment, other time scales, snapping, major-label detection, and hidden-date skipping. The exact-interval behavior applies between hidden-date jumps. The claim asks whether this explicit/automatic boundary matches the intended behavior; no maintainer approval is being assumed. Open PR #2130 touches the hour branch for another issue, so it is a possible future rebase consideration rather than competing work on this defect.

**Implementation Plan**

1. In test/TimeStep.test.js, add tests through the actual TimeStep iterator for explicit 250, 350, 1500, and 3500 ms steps and every automatic millisecond step size. Run them before changing the implementation.
2. In lib/timeline/TimeStep.js, gate only TimeStep.next()'s existing millisecond reset on autoScale, then rerun the focused tests and the same reproduction.
3. Clarify timeAxis.step in docs/timeline/index.html and add examples/timeline/other/fixedMillisecondSteps.html, as required by the PR template. The example shows minor labels with seconds/milliseconds and hides major labels; the major-label rule is unchanged.
4. Build the package, run the full suite, lint, and formatting; commit only the four planned source/test/docs/example files.

No implementation deviation was needed. A planning-process correction was needed: I ran plan-check before the claim had been posted, so it correctly refused to grade. I posted the approved claim, made the reproduction fully quoted in the plan, corrected the live-tool procedure, and reran the checker before building the change.

**Toolkit**

- Tool: plan-check through Claude Code on local plan.md and plan-comment.md, which stayed off the issue thread.
- What it produced: the first run refused on the missing posted claim; the rerun accepted all seven required checks and the preferred clarity check.
- Difficulties: the carried-over procedure still named Path Review house rules and comment.md, and the old frame assumed a posted reproduction even though Assignment 5 says to keep the report local.
- What changed: added the real claim gate, used current wild rules and plan-comment.md, and required complete reproduction facts in the plan. I followed the course's local-report instruction and preserved eval behavior; I also disclosed the separate hour-branch PR and the unchanged major-label behavior.

---

## Testing Strategy

I added the regression tests first and ran `node_modules/.bin/mocha --no-config test/TimeStep.test.js` against unchanged implementation code. The result was **19 passing, 3 failing**. The failing actual/expected deltas were **300/350**, **1000/1500**, and **3000/3500**. After the one-condition fix, the same file gave **22 passing**. Each explicit case checks eight consecutive next calls; automatic cases assert the selected scale/step and iterate across a second boundary.

The same source reproduction after the fix produced:

```json
{"requestedStep":250,"offsets":[0,250,500,750,1000],"deltas":[250,250,250,250]}
{"requestedStep":350,"offsets":[0,350,700,1050,1400],"deltas":[350,350,350,350]}
{"requestedStep":1500,"offsets":[0,1500,3000,4500,6000],"deltas":[1500,1500,1500,1500]}
{"requestedStep":3500,"offsets":[0,3500,7000,10500,14000],"deltas":[3500,3500,3500,3500]}
```

| Case | Before | After |
|---|---|---|
| Explicit 3500 ms, the issue trigger | 3000 ms increments | 3500 ms increments |
| Explicit 1500 ms | 1000 ms increments | 1500 ms increments |
| Explicit 350 ms crossing a second | One shortened 300 ms increment | Every increment 350 ms |
| Explicit 250 ms control | Every increment 250 ms | Every increment 250 ms |
| Automatic 1, 5, 10, 50, 100, 200 ms | All focused controls pass | All focused controls pass |

Repository commands on the final branch:

```text
npm run build     exit 0
npm test          108 passing (3s), exit 0
npm run lint      exit 0, no diagnostics
npm run style     All matched files use the correct format., exit 0
```

The clean baseline had 98 passing tests after building first. No checks were waived. The regression exercises the same iterator path used by TimeAxis; browser layout, the original JSFiddle, and a new design for snapping or initial alignment were not verified or claimed. Hidden-date jumps retain their existing semantics.

**Toolkit**

- Tool: Mocha/node:assert, the local Node reproduction, the four-command ship manifest, and pr-precheck's test-evidence rubric.
- What it produced: a failing-before/passing-after regression for the reported input, unchanged controls, 108 passing full-suite tests, and passing build/lint/style checks.
- Difficulties: running the package snapshot test before generating the distributable bundles failed on untouched master; a successful exit alone would not have explained that setup problem.
- What changed: made build the first manifest check, kept the real before/after deltas and test counts in test_evidence.md, and kept the iterator-versus-browser qualification explicit.

---

## Implementation Notes

All entries below record work done on **2026-11-05**; the Unit 5–8 Toolkit entries are organized by course unit, not backdated weekly work.

- Backed up the original issue-select tool and fit profile, installed the scout, authenticated GitHub, and refreshed an expired Claude session. Ran all four authored queries and the required five-issue scan.
- Recorded the scan's weak new-repo picks, then corrected ranking/adoption/open-state checks. A two-human-author check proved too strict for an established project with many bot commits, so I added a shared-interest alternative while retaining recent human activity.
- Rejected three Meteor course-site picks after finding existing PRs in otherwise empty issue threads. Graded replacement visjs picks and chose #1030 because I could reproduce an exact numeric failure.
- Consolidated the voice guides, installed and tested the voice guard, and posted the approved claim through Claude Code. Asked the scout's open semantic question instead of silently assuming agreement.
- Created local repository memory from the contribution guide and one scoped orientation. Installed ship-gate and wrote the four-check manifest. Its wiring test was summarized as one stop by Claude, but the separate voice-guard and gate logs both recorded the expected stops.
- Plan-check initially refused because I ran it before the claim existed publicly. After posting the claim, I corrected inherited live-mode procedure assumptions and obtained accept. The PR checker also needed its sandbox Repo-line, main-branch, and docs-only contribution-guide assumptions updated for a public repo targeting master.
- Added the regression tests before the source change: 19 passed and 3 failed. Added the autoScale guard, the option docs, and the example: 22 focused tests and 108 full-suite tests passed, along with build, lint, and formatting.
- Committed the four-file change as [0e8403e](https://github.com/oasis-pandey/vis-timeline/commit/0e8403e), on fix/1030-exact-millisecond-steps. The commit hook also ran the project's formatter and linter on the staged files. No unrelated cleanup, generated bundles, plans, reports, or local memory entered the diff.
- Opened [PR #2150](https://github.com/visjs/vis-timeline/pull/2150) through Claude Code after explicit approval. The ship-gate hook honored the final manual pass and the voice guard passed; I verified the upstream target, author, commit, and four-file diff. Ran the monitor, read its wait note against the live state, and kept the draft off the thread.
- Sampled five merged outside-contributor PRs for the monitor: waits were 7.31, 33.70, 8.85, 1.75, and 15.02 days to the first human maintainer response. Wrote a 21-day, single-nudge playbook; the course deadline does not shorten it.

**Toolkit**

- Tool: Git, the course tools' dated logs, local memory, and explicit before/after command logs.
- What it produced: a traceable sequence from issue selection and reproduction to the committed fix, including rejected picks and process corrections.
- Difficulties: a checker verdict could look final while still depending on inaccessible evidence or sandbox assumptions; the hook summary also did not surface both recorded stops.
- What changed: checked actual output, live thread state, tool files, and the separate guard/gate logs; recorded limitations and fixes when they arose rather than inventing a clean timeline.

---

## Pull Request

**PR Link:** https://github.com/visjs/vis-timeline/pull/2150

**PR Description:** “Preserve explicit millisecond time axis steps” fixes #1030 by restricting the remainder reset to automatic scales. It includes the one-condition fix, ten regression/control cases, the timeAxis.step documentation, and a runnable example. The GitHub description shows actual before/after JSON, the 19-pass/3-fail regression baseline, 22 focused passes, 108 full-suite passes, and passing build/lint/style checks. It discloses Codex and Claude Code assistance, the untested browser-layout/JSFiddle limitation, and the still-open explicit-versus-automatic design question.

The PR goes from oasis-pandey:fix/1030-exact-millisecond-steps into visjs/vis-timeline:master, at commit 0e8403e54706fef688666a8f1dcce30fa732c99a. Its diff contains only the four planned files. The repo's template asks for an example, documentation when behavior changes, and removal of its checklist; all are satisfied in the actual posted PR.

**Maintainer Feedback:**

- 2026-11-05: none yet. The live PR has no comments or reviews. The PR monitor recorded one pending CircleCI prepare status; local checks passed before the PR opened.

**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate invoking my updated pr-precheck on the committed branch, with the voice guard checking the outgoing description.
- What it produced: PASS for all four manifest checks and every required PR-rubric check. After I revised the AI disclosure, the final package passed again; the opening hook honored that exact cached pass, and the voice-guard log recorded pass.
- Difficulties: the live PR-checker frame still assumed the sandbox's Repo line, main base, and docs/CONTRIBUTING.md; the first passing run also suggested removing internal course-tool discussion from the maintainer-facing AI disclosure.
- What changed: updated only those live-mode seams to use the current public-repo scope, actual master base, and root contribution guide; simplified the description, reran the gate for the changed body, and opened the reviewed PR through Claude Code. No checks were excluded and no guard was bypassed.

---

## Learnings and Reflections

**Technical Skills Gained**

The concrete debugging lesson was to compare elapsed timestamps through the real iterator rather than infer behavior from the final labels. The 3500 ms case showed that addition was correct and a later reset discarded the remainder. Writing the tests before the fix made that distinction falsifiable: three cases failed with specific numeric differences while the 250 ms and automatic controls passed. I also worked through the difference between an explicit scale, automatic scale selection, and major-label alignment; fixing one does not require redesigning all three.

**Challenges Overcome**

The tools needed adaptation when moving from the classroom to real repositories. Empty issue threads hid existing PRs; an activity-only rubric accepted weak repositories; a stricter contributor-count rule then misread a bot-heavy established project. The reproduction and plan checks helped make the evidence and uncertainty explicit, but I still had to inspect their limits, correct inherited sandbox assumptions, and run the commands myself in the working session. The initial package snapshot failure was resolved by the documented build artifacts rather than by waiving the test.

**What I'd Do Differently Next Time**

I would check linked and keyword-matched PRs before spending time on environment setup, then post a reviewed claim before running plan-check. I would make live-tool scope and actual base-branch handling part of the first orientation and keep reproduction facts self-contained in the plan from the start. I would still keep the custom-interval design question visible to maintainers and give them the repo's normal review time; the submission deadline does not establish a review deadline.

---

## Resources Used

- [Unit 5 starter and scout instructions](https://github.com/codepath/ai301-unit5-starter): overlay install, search-strategy shape, and saved scan format.
- [Unit 6 starter](https://github.com/codepath/ai301-unit6-starter): voice guard, wild scopes, scope-feasible patch, and local-memory template.
- [Unit 7 starter](https://github.com/codepath/ai301-unit7-starter): ship-gate installation, manifest, and branch checks.
- [Unit 8 starter](https://github.com/codepath/ai301-unit8-starter): PR-monitor installation and the four-part playbook.
- [Course Issue Selection site](https://open-source-issue-tracker.onrender.com/): the source of the Meteor and visjs picks, checked against live GitHub before choosing.
- [vis-timeline issue #1030 and its discussion](https://github.com/visjs/vis-timeline/issues/1030): the 3500 ms trigger, the 2022 causal observation, and the unresolved rounding question.
- [CONTRIBUTING.md](https://github.com/visjs/vis-timeline/blob/master/CONTRIBUTING.md) and [PR template](https://github.com/visjs/vis-timeline/blob/master/.github/PULL_REQUEST_TEMPLATE.md): master as target, the example/docs asks, and removal of the checklist.
- [Baseline TimeStep source](https://github.com/visjs/vis-timeline/blob/fec1bfe3bdfcd54cdde16eb71cc252d3d7b05c82/lib/timeline/TimeStep.js) and [existing tests](https://github.com/visjs/vis-timeline/blob/fec1bfe3bdfcd54cdde16eb71cc252d3d7b05c82/test/TimeStep.test.js): actual stepping and control behavior.
- [package.json scripts](https://github.com/visjs/vis-timeline/blob/master/package.json) and [packaging test](https://github.com/visjs/vis-timeline/blob/master/test/package.test.js): build/test/lint/style commands and the build-before-snapshot requirement.
- Merged outside-contributor PRs [#2134](https://github.com/visjs/vis-timeline/pull/2134), [#2128](https://github.com/visjs/vis-timeline/pull/2128), [#2133](https://github.com/visjs/vis-timeline/pull/2133), [#2085](https://github.com/visjs/vis-timeline/pull/2085), and [#1972](https://github.com/visjs/vis-timeline/pull/1972): the observed review-wait sample used for my monitor playbook.

- [Full Assignment 5 grading rubric](https://courses.codepath.org/courses/ai301/pages/grading_rubrics): final check of the ten headings, four Understanding fields, seven Toolkit blocks, four weekly entries, real links, evidence, and dated log.
