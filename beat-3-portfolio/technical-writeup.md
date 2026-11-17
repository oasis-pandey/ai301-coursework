# Preserving Exact Millisecond Steps in vis-timeline

## Overview

I opened a [pull request to vis-timeline](https://github.com/visjs/vis-timeline/pull/2150) for a bug that shortened explicitly configured millisecond intervals when a timeline crossed a one-second boundary. I reproduced the failure in the project's real `TimeStep` iterator, wrote regression tests, changed one condition so only automatically chosen intervals are rounded, and added documentation and a working example. The pull request is still open and awaiting maintainer review; all local checks and all five upstream CircleCI checks pass.

## What happened

The original issue reported that a 3,500-millisecond timeline step appeared as 3,000 milliseconds. An earlier contributor had traced the behavior to `TimeStep.next()`, but noted that simply removing the rounding might affect other scenarios. I first tested the current `master` branch at commit `fec1bfe` instead of assuming that the old report still described the code.

I ran the real iterator with explicit steps of 250, 350, 1,500, and 3,500 milliseconds. This output proved both the bug and a useful control:

```json
{"requestedStep":250,"deltas":[250,250,250,250]}
{"requestedStep":350,"deltas":[350,350,300,350]}
{"requestedStep":1500,"deltas":[1000,1000,1000,1000]}
{"requestedStep":3500,"deltas":[3000,3000,3000,3000]}
```

The 250-millisecond control worked because it divides evenly into one second. The other results showed that the failure was broader than the single 3,500-millisecond example: the iterator discarded the remainder after adding an explicit interval.

Before editing the implementation, I added tests for the four explicit intervals and controls for every automatic millisecond step supported by the project. The first focused run produced `19 passing, 3 failing`. The failures showed actual and expected deltas of `300/350`, `1000/1500`, and `3000/3500`. That failing run mattered because it demonstrated that the tests could detect the reported behavior rather than merely pass alongside my change.

My first idea could have been to remove the reset entirely, but the existing code uses it to align automatically selected steps. I changed the implementation only after separating automatic and explicit behavior. The complete source change was one added guard:

```diff
- if (this.current.milliseconds() > 0 && this.current.milliseconds() < this.step)
+ if (this.autoScale && this.current.milliseconds() > 0 && this.current.milliseconds() < this.step)
    this.current.milliseconds(0);
```

This was the key revision in my work: the failing tests showed that unconditional rounding was wrong, while the automatic-step controls showed what had to remain unchanged. I therefore narrowed the fix instead of deleting the rounding logic.

After that change, the same focused suite reported `22 passing`. The reproduction also preserved every requested interval:

```json
{"requestedStep":250,"deltas":[250,250,250,250]}
{"requestedStep":350,"deltas":[350,350,350,350]}
{"requestedStep":1500,"deltas":[1500,1500,1500,1500]}
{"requestedStep":3500,"deltas":[3500,3500,3500,3500]}
```

I then added a browser example using a 3,500-millisecond axis and clarified the `timeAxis.step` documentation. Before running the full suite, I encountered a packaging snapshot failure because the repository's generated bundles did not exist yet. Instead of excluding the test, I changed my check order to build first. The final local evidence was:

```text
npm run build     passed
npm test          108 passing
npm run lint      passed with no diagnostics
npm run style     all matched files use the correct format
```

On November 5, 2026, I committed the four-file change and opened pull request #2150. The result that followed was a clean upstream run: CircleCI's prepare, build, lint, test, and examples checks all passed. The pull request currently has no maintainer comments or reviews, so the accurate outcome is that I opened a tested fix, not that the project has accepted or merged it.

## Limitations and what's next

My tests exercise the same iterator that generates timeline ticks, but I did not rerun the original JSFiddle or verify the layout across browsers. The change also deliberately leaves initial alignment, major labels, snapping, and hidden-date jumps alone. Most importantly, passing tests do not settle the design question of whether maintainers want every explicit millisecond interval preserved across second boundaries.

Next, I would add browser-level coverage that renders the 3,500-millisecond example and asserts the displayed tick spacing. I would also use maintainer feedback to confirm the explicit-versus-automatic boundary before expanding the change. Until that review happens, I will keep the pull request's scope narrow and describe its status as awaiting review.
