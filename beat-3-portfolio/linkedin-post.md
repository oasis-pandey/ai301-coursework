I opened a fix for a timing bug in vis-timeline, an open-source library for building interactive timelines. I found that some custom intervals were being shortened, then added tests and a focused code change to preserve the requested spacing.

The work began with a reported 3.5-second interval appearing as 3 seconds. I reproduced that behavior in the project's real timing code and found two more affected intervals. I wrote tests that failed before my change and passed afterward, while keeping the library's automatic interval behavior unchanged.

I also updated the documentation and added an example so reviewers can see the intended behavior. The pull request is still open and awaiting maintainer review, but all local checks and all five of the project's automated checks pass.

This project reinforced how I like to work: prove the problem, protect existing behavior, make the smallest defensible change, and communicate honestly about what remains unverified.

https://github.com/visjs/vis-timeline/pull/2150
