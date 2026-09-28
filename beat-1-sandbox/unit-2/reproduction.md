# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username** 
oasis-pandey


---

## Posted upstream

**Claim comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5861064211

Hi! I'd like to work on this issue. I'll investigate the reported configuration mismatch between README.md and .env.example, specifically the documentation's use of OPENROUTER_API_KEY and the LLM provider settings available in the example environment configuration.

I'll follow the repository's documented setup process, compare the resulting environment configuration with the documentation, and report back here with my reproduction steps, environment, and results.


**Reproduction comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5861132294

Reproduction Report
I reproduced the documentation and environment configuration mismatch described in #73.

Environment
macOS
Repository: pathreview-ai301-fa26-s3
Reproduction performed from the repository root
Steps
I checked the OpenRouter configuration instruction in README.md:

grep -n "OPENROUTER_API_KEY" README.md

Output:

24:# Configure environment (add your OPENROUTER_API_KEY to .env)
I checked docs/SETUP.md for the same configuration:

grep -n "OPENROUTER_API_KEY" docs/SETUP.md

Output:

47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
I checked the LLM-related settings provided by .env.example:

grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" .env.example

Output:

18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
I followed the documented environment setup by copying .env.example:

cp .env.example .env

I checked the LLM-related settings in the resulting .env:

grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" .env

Output:

18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
I explicitly checked whether OPENROUTER_API_KEY was present:

grep -n "OPENROUTER_API_KEY" .env || echo "OPENROUTER_API_KEY not found in .env"

Output:

OPENROUTER_API_KEY not found in .env
I checked the application's configuration fields:

grep -n "openrouter_api_key\|openai_api_key\|llm_provider" core/config.py

Output:

18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
Expected
The example environment configuration should be consistent with the setup documentation so that users following the documented setup can identify the OpenRouter configuration expected by the project.

Actual
Both README.md and docs/SETUP.md instruct users to configure OPENROUTER_API_KEY, but following the documented environment setup produces an .env with LLM_PROVIDER=mock and OPENAI_API_KEY and no OPENROUTER_API_KEY entry.

core/config.py also defines an openrouter_api_key configuration field.

This reproduces the documentation and environment configuration mismatch described in #73.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Full eval run: 19/20 scored items agreed with the gold labels. The run passed the 18/20 bar. The only disagreement was pkg-10.

**Package analysis**

pkg-10: My rubric decided reject, while the gold label was accept. The disagreement came from the required behavior_matches_issue check. The package was an honest cannot-reproduce report. It stated, "cannot reproduce on Linux + zsh with the report's exact layout and config," showed that the directory module continued to render, and explicitly documented that the original issue used macOS and fish 4.7.1 while the reproduction used Ubuntu 24.04 and zsh 5.9.

My rubric read this as a failure because behavior_matches_issue requires the evidence to demonstrate the same behavior described by the issue. In this package, the reported behavior did not occur. However, the gold label was accept because the package honestly reported a cannot-reproduce result and provided evidence supporting that result.

**Check rationale**

From my rubric.md:

behavior_matches_issue | The observed output, error, logs, screenshots, or other artifacts read against the behavior described in the issue. | Pass if the evidence tests and demonstrates the same behavior the issue describes. An adjacent, similar, or unrelated failure does not pass. | required

I made this check required because I wanted the rubric to distinguish reproduction of the actual reported behavior from an adjacent or unrelated failure. I rejected a looser rule where producing any related error could count as reproduction. The pkg-10 result showed the limitation of my wording: because the check requires the issue behavior to actually appear, it can also reject an honest cannot-reproduce report even when that report accurately documents what was tested and observed.

**Trade-offs**

The strict behavior_matches_issue check gives up some flexibility for cannot-reproduce reports in exchange for stronger protection against wrong-target reproductions. It correctly classified all 4/4 wrong-target packages in my eval, but it also caused my one disagreement on pkg-10. That package clearly documented that the reported behavior did not occur and identified the environment differences, but my check still failed it because the issue behavior itself was absent. I accept this limitation because the check is intentionally conservative about claiming that the reported behavior has been demonstrated. My final eval still agreed with 19/20 scored packages and passed the 18/20 bar.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
