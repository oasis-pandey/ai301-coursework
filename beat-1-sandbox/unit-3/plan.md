# Plan for issue #73

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

## Diagnosis

My Unit 2 reproduction confirmed the setup mismatch after following the repository's documented copy step. The decisive evidence was:

> `README.md` output: `24:# Configure environment (add your OPENROUTER_API_KEY to .env)`

> `.env.example` and the copied `.env` output: `18:LLM_PROVIDER=mock` and `19:OPENAI_API_KEY=sk-your-key-here`

> Explicit check output: `OPENROUTER_API_KEY not found in .env`

> `core/config.py` output: `20:    openrouter_api_key: str = Field(default="")`

The example environment file therefore omits a configuration field that both setup guides tell users to fill in and that `Settings` already accepts. A repository search also shows that `LLM_PROVIDER` is currently consumed by the embedding-provider factory, whose supported values are only `mock` and `openai`. I will not add `openrouter` to that options comment because the reproduction did not establish it as a supported provider-selector value.

## Scope

In scope:

- Add an `OPENROUTER_API_KEY` placeholder to the LLM configuration block in `.env.example`.
- Preserve `LLM_PROVIDER=mock`, the documented `mock`/`openai` options, and the existing `OPENAI_API_KEY` placeholder.

Out of scope:

- No changes to `README.md`, `docs/SETUP.md`, or `core/config.py`.
- No new OpenRouter client wiring or changes to provider selection.
- No cleanup of other environment settings.

PR #85 proposes the same one-line example-file fix. Path Review permits each student to make their own plan and branch on a shared issue; I will keep my branch independent and will not expand its scope to differentiate it.

## Files

- `.env.example` — add `OPENROUTER_API_KEY=sk-or-your-key-here` beside the existing API-key example.

## Approach

1. Create `fix/73-env-openrouter-key` from the fork's `main` branch.
2. Add the OpenRouter placeholder directly after `OPENAI_API_KEY` so users who copy the example can see both accepted settings in one place.
3. Inspect the diff and confirm the change is limited to the intended line.

## Test plan

1. Before the change, rerun the Unit 2 check:

   ```bash
   cp .env.example .env
   grep -nE 'LLM_PROVIDER|OPENAI_API_KEY|OPENROUTER_API_KEY' .env
   grep -n 'OPENROUTER_API_KEY' .env || echo 'OPENROUTER_API_KEY not found in .env'
   ```

   The copied file should show `LLM_PROVIDER=mock` and `OPENAI_API_KEY`, followed by the explicit not-found message for `OPENROUTER_API_KEY`.

2. After the change, repeat the same copy and grep. The copied `.env` should show all three entries, including `OPENROUTER_API_KEY=sk-or-your-key-here`, and the explicit grep should find that line instead of printing the not-found message.
3. Run `git diff --check` and inspect `git diff -- .env.example` to confirm there are no whitespace errors or unrelated tracked changes.

## Risks and unknowns

- The repository currently has no application path that selects `openrouter` through `LLM_PROVIDER`; this plan intentionally does not claim to add that support or list it as a selector option.
- A placeholder must not be mistaken for a real secret. The `sk-or-your-key-here` form matches the existing clearly fake `OPENAI_API_KEY` example and keeps credentials out of the repository.
- Because this is an example-file-only documentation fix, no runtime API call is needed to prove the reported mismatch is corrected.

## Deviations

The implementation followed the posted plan without deviation. The tracked change adds only the planned `OPENROUTER_API_KEY` placeholder to `.env.example`; the scope, file, approach, and verification steps stayed the same.
