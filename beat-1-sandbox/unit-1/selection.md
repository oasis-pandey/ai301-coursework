# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
All three pass every required check. Details:

Repo-level (shared by all three)
- maintainer-active: last default-branch commit 2026-09-16 by Aburke225 (collaborator, and the author of all three issues) — 4 days ago.
- repo-in-use: not archived, pushed 2026-09-16, 71 open issues, active labeling.
- contribution-policy: no CONTRIBUTING.md, no AI policy file; PR template imposes CI/test conditions only. Silence passes.

#73 — README vs .env.example disagree on LLM API key — bounded: two files, one outcome (make them agree). Unclaimed: no assignee, no linked PR, no comments.
#72 — verify_password raises UnknownHashError — bounded: one fail-closed fix plus removing the xfail marker. Two fork commits reference it (rafiatasafi, xyin20, today), but those are classmates' work, not linked PRs or claim comments — and the Path Review house rule says classmate claims don't block. Unclaimed passes.
#54 — section detection fails on leading whitespace — bounded: one regex-anchoring fix in _detect_sections() with a reproduction snippet and three named failing tests. Unclaimed: clean thread.

Note on ranking: scope.md's fit profile is still the placeholder (Write a few sentences here.), so I have no profile to rank against. The order below is my tie-break by newcomer friendliness only, not a fit judgment — fill in that section to get a real ranking.

1. #54 — clearest evidence in the issue: a runnable repro and three named tests to verify against.
2. #72 — smallest code change, but you must also find and clear the xfail/pyproject.toml suppression.
3. #73 — docs-only and lowest risk, but two students already have commits against #72 and none against this one; it teaches the least about the codebase.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by collaborator Aburke225, 4 days before capture date 2026-09-20"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16; issue opened 2026-09-10"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One fix: '_detect_sections() ... anchors every section-header pattern at the start of a line'; expected output given in repro"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; timeline has only 4 'labeled' events, no linked PR"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "CONTRIBUTING.md, .github/CONTRIBUTING.md, AI_POLICY.md all return 404; PR template states only CI/test conditions"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Issue authored by COLLABORATOR Aburke225; same account committed to main on 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16; 71 open issues"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "'Verification against a malformed hash should fail closed (return False)' plus removing the H-05 xfail marker — one primary bug fix"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; no open PRs in repo; two 'referenced' commits by classmates (rafiatasafi, xyin20) which the Path Review house rule says do not block"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "No CONTRIBUTING.md or AI policy file in repo root or .github/"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "Issue opened 2026-09-16 by COLLABORATOR Aburke225, same day as the latest main commit"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16, 4 days before capture"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "'Make the two files agree' — README.md and .env.example, one documentation change"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; timeline shows only 'labeled' events"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "No policy file found; PR template requires only green CI and tests"}
    ],
    "verdict": "accept"
  }
]

```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**
17/20 → 18/20 → 16/20 → 18/20

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**
issue-01 — My rubric decided reject, while the gold label was accept. The disagreement came from my bounded-scope check. My rubric requires an issue to have one primary change with an identifiable expected outcome and rejects issues that contain multiple unrelated changes or require a broad project-wide redesign. The evaluator interpreted issue-01 as failing this check, which caused the overall verdict to be reject because bounded-scope is required. The gold label was accept, showing that my scope check can sometimes interpret an acceptable issue too strictly.

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

For bounded-scope, my current check says:

"Pass if the issue requests one primary bug fix, feature, or documentation change with an identifiable expected outcome. Multiple files, multiple implementation steps, technical difficulty, multiple possible solutions, or a short description do not by themselves cause failure. Fail only if the issue requests multiple unrelated changes or explicitly requires a broad project-wide redesign."

I wrote the check this way because I wanted scope to be based on the requested outcome rather than assumptions about difficulty. An issue can touch multiple files or require several implementation steps and still be one focused change. I therefore made the failure condition more specific so that an issue fails when it contains unrelated changes or explicitly requires a broad project-wide redesign.

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

The trade-off is that this check can still reject an issue that is acceptable but appears broader when interpreted from its description. issue-01 demonstrates this: the gold label was accept, but my rubric rejected it because bounded-scope failed. I accept this trade-off because I would rather flag potentially broad work for a first contribution while still allowing multiple files or implementation steps when they contribute to one primary outcome.

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

Issue #73 fits my interests and the time available because it has a clear and limited goal: making the README and .env.example agree about the LLM API key. It seems manageable for a first contribution and gives me enough time to understand the repository and complete the work correctly.
The verdict correctly identified that the repository is active, the issue is unclaimed, there is no contribution policy preventing the work, and the issue has one bounded outcome even though it involves two files. Outside of the rubric, I also considered my comfort level with the task and how manageable it would be as my first contribution.
I expect claiming the issue to be relatively straightforward because it currently has no assignee, comments, or linked pull request. The main difficulty is that another student could claim or begin working on it before I claim it in Unit 2.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
