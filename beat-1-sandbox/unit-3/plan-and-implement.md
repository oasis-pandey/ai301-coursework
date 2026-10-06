# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

oasis-pandey

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-6025511187

Plan for #73, based on my reproduction above.

After `cp .env.example .env`, my grep showed `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here`, while the explicit check printed `OPENROUTER_API_KEY not found in .env`. `README.md:24` and `docs/SETUP.md:47` both tell users to set that key, and `core/config.py:20` already defines `openrouter_api_key`, so the copied example is missing the field referenced by the setup instructions.

I will update `.env.example` only, adding `OPENROUTER_API_KEY=sk-or-your-key-here` beside the existing API-key placeholder. I will keep `LLM_PROVIDER=mock`, the current `mock`/`openai` options comment, and `OPENAI_API_KEY` unchanged. I am not changing runtime provider selection or wiring a new client; the repository's embedding factory currently accepts only `mock` and `openai`.

I noticed that PR #85 proposes the same one-line example-file fix. Per the Path Review classroom rules, I am still posting and building my own plan on my fork, and I will keep the change independent and equally bounded.

For verification, I will repeat my reproduction: copy `.env.example` to `.env` and grep for `LLM_PROVIDER`, `OPENAI_API_KEY`, and `OPENROUTER_API_KEY`. After the fix, the copied file should contain all three entries and the OpenRouter-specific grep should find the placeholder instead of printing the not-found message. I will also run `git diff --check` and confirm the tracked diff contains only the intended `.env.example` line.

---

## Your branch

**Branch**

`fix/73-env-openrouter-key`

**Evidence**

Before (`main` at `2f4e82f`):

```text
$ cp .env.example .env
$ grep -nE 'LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY' .env
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
$ grep -n 'OPENROUTER_API_KEY' .env || echo 'OPENROUTER_API_KEY not found in .env'
OPENROUTER_API_KEY not found in .env
```

After (`fix/73-env-openrouter-key` at `bd66273`):

```text
$ cp .env.example .env
$ grep -nE 'LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY' .env
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
20:OPENROUTER_API_KEY=sk-or-your-key-here
$ grep -n 'OPENROUTER_API_KEY' .env || echo 'OPENROUTER_API_KEY not found in .env'
20:OPENROUTER_API_KEY=sk-or-your-key-here
$ git diff --check
```

`git diff --check` produced no output and exited successfully. The tracked change is one added line in `.env.example`; `plan.md` and `comment.md` remained untracked and were not committed.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20

This was the only full scored run. Before it, I ran the four unscored `calib-` packages as a formatting and procedure smoke check; all four matched, but calibration packages have no agreement score and are not part of the run history above.

**Package analysis**

`pkg-03`: my rubric decided `reject`, while the gold label was `accept`. The run reported `failed: thread_direction`. The package's comment did engage both pieces of overlapping work: "I saw the prior art note (#3224) and the open PR #3314 that adds the separator; my intent is not to race it. If #3314 is picked up I will add the regression tests against it instead." My required `thread_direction` check asks the plan to coordinate with linked or overlapping work rather than silently racing it. The evaluator read that conditional coordination as insufficient and failed the check, even though the gold label treats the explicit acknowledgment and fallback as ready. This is the run's only disagreement.

**Check rationale**

My uploaded rubric contains this exact check:

> `thread_direction | The candidate plan and plan comment read against issue requirements, thread highlights or live maintainer comments, linked/prior work, and explicit requested direction. | Pass if the proposed work acknowledges and follows explicit maintainer direction, or clearly explains a relevant evidence-based departure, and coordinates with linked or overlapping work instead of silently racing or ignoring it. Pass when no relevant direction or overlap exists. | required`

I made this check required because a technically sound plan can still be unready when it ignores a maintainer's requested direction or duplicates active work without acknowledging it. I used an outcome-based condition—acknowledge and follow the direction, or explain an evidence-based departure—instead of requiring a particular heading or number of thread references. I rejected a looser version that would pass any plan merely because it mentioned the issue thread, since that would miss the assignment's thread-and-convention failure family.

**Trade-offs**

The required `thread_direction` check is deliberately conservative, so it can reject a plan whose coordination language is reasonable but conditional. `pkg-03` is the concrete cost: it named prior art #3224, acknowledged open PR #3314, promised not to race it, and offered to contribute regression tests if that PR moved forward, yet the evaluator still failed the check while the gold label accepted the package. I accept that false-reject risk because the same check correctly caught the two thread/convention packages in the final run (`pkg-04` and `pkg-20`), giving that category a 2/2 match instead of allowing plans that ignore maintainer direction or repository policy.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
