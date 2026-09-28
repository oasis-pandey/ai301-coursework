# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment_recorded | The repro report's environment record, read against the issue's stated environment and the repo-facts block. | Pass if the report records enough relevant environment information for another person to understand the setup used for the reproduction, including applicable software/version and platform or runtime details. Fail if important environment details that could affect the result are missing or contradicted. | required |
| steps_reproducible | The commands, setup instructions, inputs, and reproduction steps in the repro report, read with any referenced artifacts. | Pass if a stranger could follow the provided setup and steps in order and reach the tested behavior without having to guess a material command, input, configuration, or prerequisite. | required |
| behavior_matches_issue | The observed output, error, logs, screenshots, or other artifacts read against the behavior described in the issue. | Pass if the evidence tests and demonstrates the same behavior the issue describes. An adjacent, similar, or unrelated failure does not pass. | required |
| outcome_supported | The repro report's stated outcome read against the supplied artifacts and observed output. | Pass if the conclusion accurately reflects the evidence. A reproduced issue passes when the evidence demonstrates the reported behavior; a cannot-reproduce result also passes when the attempted reproduction is adequately evidenced and the report states that result honestly. Fail if the conclusion claims more than the evidence supports or confidently identifies the wrong behavior. | required |
| repo_conventions | The claim comment and repro report read against the repo-facts block, scope.md, and applicable repository contribution or disclosure requirements identified in references/evidence-guide.md. | Pass if the proposed comments comply with applicable repository-specific conventions, including required disclosures or contribution requirements. | required |
| evidence_clarity | The artifacts and output excerpts referenced by the repro report, interpreted using references/evidence-guide.md. | Pass if the evidence makes the relevant observed behavior identifiable and connects it to the stated outcome without relying only on an unsupported assertion. | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks may identify improvements but never change the final verdict. Treat `unclear` on any required check as a failure and reject the package until the evidence is sufficient to make that check pass. An `unclear` or failed preferred check does not change an otherwise accepting verdict.