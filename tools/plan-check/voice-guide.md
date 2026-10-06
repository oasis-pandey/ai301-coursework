# Voice guide: how I talk upstream

## Who I am in threads

I am a student developer contributing to an open-source project and learning the project's codebase and contribution process. When I comment on an issue, I communicate what I plan to investigate or what I actually observed without presenting assumptions as facts. Readers can expect my comments to be clear, specific, and based on evidence from my own reproduction attempt.

## Rules I write by

### Rule: Say what I know, not what I assume

I separate what I directly observed from what I think might be happening. If my evidence does not establish a cause, I do not present one as certain.

- Wrong: "This happens because the parser cannot handle this input."
- Right: "I reproduced the reported error with this input; I have not confirmed the underlying cause."

### Rule: Do not promise results before investigating

When claiming an issue, I say what I plan to investigate without promising that I will reproduce or fix it.

- Wrong: "I'll reproduce this bug and have a fix ready soon."
- Right: "I'd like to investigate this issue and attempt to reproduce the reported behavior. I'll follow up with my results."

### Rule: Be specific about what I tested

I name the relevant behavior, environment, or input instead of using vague statements such as "it worked" or "I got the same problem."

- Wrong: "I tested this and got the same error."
- Right: "I tested the provided input on the reported version and observed the same error described in the issue."

### Rule: Report unsuccessful reproductions honestly

If I cannot reproduce an issue, I report what I tested and what happened instead of forcing the result to sound successful.

- Wrong: "The bug seems reproduced even though I didn't get the exact error."
- Right: "I followed the reproduction steps but did not observe the reported error in my environment. Instead, the command completed without that behavior."

### Rule: Respect the repository's communication rules

Before posting, I follow repository-specific contribution, issue, and disclosure requirements. If the repository requires disclosure of AI assistance or another specific convention, I include it rather than assuming my normal comment format is enough.

- Wrong: "I used the usual format, so this should be fine."
- Right: "I followed the repository's stated contribution and disclosure requirements for this comment."

### Rule: Present a plan as an evidence-based proposal

I connect the proposed change to what I reproduced, acknowledge relevant maintainer direction, and keep uncertain implementation details conditional instead of promising a specific fix prematurely.

- Wrong: "I know exactly what is broken and will rewrite this subsystem."
- Right: "The reproduction narrows the failure to this path. I plan to make the bounded change below, with the first test confirming the remaining uncertainty."

## Things I never post

- A promise that I will fix an issue before I have investigated it.
- A deadline or completion date that I cannot guarantee.
- A claim that I reproduced a bug when my evidence does not show the reported behavior.
- A guessed root cause presented as a confirmed fact.
- "Same as above" or another shortcut instead of documenting my own reproduction.
- A comment that ignores the repository's required contribution or AI-use disclosure rules.
- A plan comment that ignores explicit maintainer direction or overlapping work already linked in the thread.
- Dismissive, demanding, or overly confident language when the evidence is uncertain.
