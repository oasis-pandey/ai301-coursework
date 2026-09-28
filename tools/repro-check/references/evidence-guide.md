# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:**  
In an eval bundle, look in the repro report's environment record, the issue context, and the repo-facts block. Compare the environment used for reproduction with any versions, operating systems, runtimes, dependencies, or configurations named by the issue. In live mode, look at the original GitHub issue, relevant repository setup documentation, and the environment information recorded in the student's draft repro comment.

**What good looks like:**  
The report identifies the relevant software/version, platform or runtime, and other setup details needed to understand the reproduction environment. When the environment differs materially from what the issue targets, the difference is explicitly stated rather than silently treated as equivalent.

## Steps

**Where it lives:**  
In an eval bundle, look in the repro report for setup instructions, commands, inputs, configuration, and the ordered steps used to trigger the behavior. Use referenced artifacts when they contain required inputs or commands. In live mode, look at the student's draft repro comment together with repository documentation needed to establish the starting state.

**What good looks like:**  
A stranger can start from the described state and follow the commands and actions in order without guessing a material prerequisite, input, configuration, or trigger. The steps describe what was actually attempted rather than only summarizing the intended test.

## Behavior shown

**Where it lives:**  
In an eval bundle, look at output excerpts, logs, error messages, screenshots, or other artifacts supplied with the repro report, and read them against the behavior described in the issue context. In live mode, compare the evidence in the student's draft repro comment with the behavior described by the GitHub issue.

**What good looks like:**  
The evidence shows the specific behavior being investigated, not merely that some error or unexpected behavior occurred. The relevant output, error, or state should be identifiable in the artifact and correspond to the issue's described symptom or trigger.

## Honesty

**Where it lives:**  
In an eval bundle, compare the repro report's stated outcome with its steps and supporting artifacts. Also compare any claim about reproducing or not reproducing the issue with the behavior shown by the evidence. In live mode, compare the student's conclusion in the draft repro comment with the commands, outputs, screenshots, or other evidence they provide.

**What good looks like:**  
The conclusion says only what the evidence supports. A successful reproduction states that the issue was reproduced only when the evidence shows the reported behavior; an honest cannot-reproduce is acceptable when the attempted reproduction is documented and the evidence supports that outcome. A report is not sufficient when it confidently claims reproduction while its evidence shows a different or unsupported behavior.

## Comms

**Where it lives:**  
In an eval bundle, compare the claim comment and repro report with the issue context, repo-facts block, and any repository-specific contribution, comment, template, or AI-use disclosure requirements included in the package. In live mode, check the GitHub issue, repository contribution documentation and templates, and other applicable repository policies against the student's draft comment.

**What good looks like:**  
The claim identifies the specific issue and states what the student intends to investigate without promising a fix, result, or completion date. The repro report communicates the actual result specifically and accurately. Both comments follow applicable repository conventions, including required AI-use disclosures, rather than relying on generic boilerplate that conflicts with the repository's stated requirements.