# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/193

**Branch**

`fix/73-env-openrouter-key`

## Eval iterations

**Run history**

1. First full run: `agreement: 17/20 scored items  (bar: 18/20: below the bar)`. It rejected `pkg-02`, `pkg-05`, and `pkg-19` on `test_evidence` even though their primary repro evidence was decisive.
2. Targeted revision run: `agreement: 4/4 scored items`. After revising the test-evidence rule, `pkg-02`, `pkg-05`, and `pkg-19` accepted, while the `pkg-04` not-tested canary still rejected.
3. Confirming full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`. This is the run saved in `eval-run.txt`; its category line is `clear-accept 6/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`.

**Package analysis**

I analyzed `pkg-20`. My rubric decided `reject`, matching the gold label `reject`, because `standards_compliance` is required and the package omits an applicable AI-use disclosure. The bundle says: “All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance.” The candidate description explains the implementation and says “Repro evidence below; `zig build test` passes,” but provides no disclosure. A technically strong diff cannot compensate for a required standards check, so the verdict rejects.

**Check rationale**

My revised check reads exactly:

> | test_evidence | The candidate test-evidence block read against the reproduction trigger, controls, and expected outcome in the plan context, each behavior actually delivered, and the description's testing claims. | Pass when the primary reported failure is shown before the change and with an observable contrasting result after it, or a focused regression test demonstrates the same contrast through the changed path. For secondary delivered behavior and non-deferred test-plan cases, a specifically named observed outcome or focused test result is sufficient; a second full transcript is not required. The evidence must expose a falsifiable output, state, exit result, or assertion and may honestly report failures. Fail for “tested” or “passes” without the primary decisive observable, a control or unchanged path substituted for the failing path, subjective duration/manual claims, or silence about a promised case. | required |

The first version required visible raw output for every delivered behavior. That incorrectly rejected three clear accepts whose primary before/after proof was decisive and whose secondary outcomes were specifically reported. I revised it to keep the strict requirement on the primary failing path while allowing a named observable or focused test for secondary cases. This still rejects vague or off-path evidence.

**Trade-offs**

The looser secondary-evidence rule can accept a concise named outcome without a second full transcript, so it gives up some raw-output detail. I reran `pkg-04` as a not-tested canary because its entire evidence is: “Tested locally on Windows 11 with less-Windows: colors work now in paging mode. `cargo test` passes.” It still rejected: that text does not show the original paged-output failure before the change or a focused regression proving the contrast. The revision changed `pkg-02`, `pkg-05`, and `pkg-19` to accept without erasing the boundary that catches unsupported testing claims.
