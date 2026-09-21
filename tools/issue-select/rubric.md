# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | repo-facts block and comment thread; look for recent maintainer comments, issue responses, merged PRs, or default-branch commits | Pass if there is maintainer or repository activity within the last 90 days | required |
| repo-in-use | repo-facts block; look at recent default-branch commit dates, merged PRs, and issue activity | Pass if the repository has at least one commit, merged PR, or issue interaction within the last 90 days | required |
| bounded-scope | issue body and comment thread; identify the main requested change and expected outcome | Pass if the issue requests one primary bug fix, feature, or documentation change with an identifiable expected outcome. Multiple files, multiple implementation steps, technical difficulty, multiple possible solutions, or a short description do not by themselves cause failure. Fail only if the issue requests multiple unrelated changes or explicitly requires a broad project-wide redesign. | required |
| unclaimed | repo-facts block and comment thread; check current assignee, open linked PRs, and recent comments indicating active work | Pass if there is no current assignee, no open linked PR, and no recent commenter clearly indicating they are actively working on the issue. Old abandoned claims or closed PRs do not count as currently claimed. | required |
| contribution-policy | repo-facts block; read the contribution policy or AI/tooling policy | Pass if the repository permits AI-assisted contributions or has no policy prohibiting them. Fail if the repository explicitly prohibits AI-generated or AI-assisted code or documentation required for the contribution. | required |

## Verdict rule

Accept only if every required check passes. Any failed required check rejects the issue. If the evidence is unclear for a required check, treat it as a fail. Preferred checks, if added later, do not change the verdict and are used only to rank accepted issues.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
