# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:** In an eval bundle, compare the plan-context block's scope, exclusions, files, promised behavior, tests, and deviations with every file and hunk in the candidate PR's diff; compare the candidate description's claims with both. In live mode, use `plan.md` including `## Deviations`, the committed `git diff main...HEAD`, and `pr_draft.md`.

**What good looks like:** Every diff hunk maps to the plan or to a deviation that explains what changed and why, and every outcome still promised by the plan is present. A smaller result is ready when the plan and description honestly record the deferral; silent extra work, silent omission, or a description claiming absent work is drift.

## Test evidence (harness category: not-tested)

**Where it lives:** In an eval bundle, read the plan-context reproduction and test plan beside the candidate test-evidence block and the diff's added tests. In live mode, compare the Unit 2 reproduction (or house repro pack), `plan.md` test plan, branch diff, `test_evidence.md`, and testing claims in `pr_draft.md`. Repository-required checks live in repo facts or, live, the PR template and `docs/CONTRIBUTING.md`.

**What good looks like:** Evidence identifies the primary failing trigger and shows a before/failing observable with a contrasting after result through the changed path, or provides a focused regression test that proves the same contrast. Secondary delivered behaviors and non-deferred cases may be supported by a specifically named observed outcome or focused test result without duplicating a full transcript. Every applicable repo check's real outcome is reported. “Tests pass,” an unchanged control, an unrelated scenario, or an unshown required command is not proof. Expected “no tests ran” and honestly reported failures are evidence when shown.

## Diff quality (harness category: unreviewable)

**Where it lives:** In an eval bundle, inspect the complete unified diff first and use the commit list as a pointer to suspicious work. In live mode, inspect every line of `git diff main...HEAD` and the branch commits; do not use the clean working tree or diff stat as a substitute.

**What good looks like:** The intended fix and its focused coverage are visible without unrelated hunks. There are no debug prints, commented-out experiments, dead helpers, unexplained TODOs, generated debris, duplicated blocks, broad reformatting/reindentation, import churn, or drive-by cleanup. Messy commit names alone are not fatal if the final diff is clean.

## Standards and comms (harness category: standards-wall)

**Where it lives:** In an eval bundle, read repo facts for template asks, contribution policy, required companion files, and AI-use rules; use thread highlights for explicit maintainer direction; compare them with the candidate title, description, checkboxes, and diff. In live mode, read the complete issue thread, `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, `scope.md`, `pr_draft.md`, and the diff. Apply `voice-guide.md` separately to the outgoing title and description.

**What good looks like:** Every applicable section contains truthful substance; issue-closing syntax, checklists, tests, changelog/release notes, and maintainer asks are satisfied and verifiable; `N/A` includes a real reason. When AI disclosure is required by repo or course policy, it states in the author's own words how AI was used. Boilerplate, false boxes, missing required artifacts, and omitted disclosure do not pass. Description-to-diff truth belongs to plan fidelity even though clear communication makes it easier to review.
