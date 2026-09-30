# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The environment record in the repro report (the version, platform and commit or tag it names), read against the version the issue targets and against any version field the repo-facts block says the bug template asks for. | The report names both the version of the software it ran and the platform it ran on, and that version either matches the one the issue targets or the report calls out the difference explicitly. It fails when no version appears anywhere in the package, or when the only placement is unlocatable ("locally", "on my machine", "the latest version"), because a maintainer cannot line an unnamed setup up against their own. A version named without a commit hash still passes: a released version is locatable on its own. | required |
| steps-followable | The sequence of actions the repro report gives, from its starting state through to the trigger, read as a stranger with a fresh clone would read it. | A stranger could re-run the report without asking the author a question: the actions name the actual commands or operations and identify every input they act on. It fails when actions are given only in general terms ("I ran the tool on a file", "opened it and it broke"), or when the report acts on an input it never identifies. Judge only whether the path can be walked — not how many steps it has, whether they are numbered, or whether the report uses any particular headings. Three commands can be enough and ten can be insufficient. | required |
| behavior-matches-issue | The artifacts in the repro report (output excerpts, logs, screenshots), read against the specific failure the issue describes — its error type, exit code, message, or symptom. | The artifact shows the same failure the issue reports. Where the issue names an exit code, an exception type, or an error string, the artifact shows that same one. It fails when the artifact shows a different failure than the issue describes, however confident the surrounding text is — a config error where the issue reports a crash is a different bug, not a reproduction. It also fails when the report asserts an outcome and shows no artifact at all. A report concluding that the bug could not be reproduced passes this check when its artifact shows what the run actually did instead. | required |
| outcome-stated-honestly | The report's stated conclusion, compared with what its own artifacts actually support. | The conclusion claims no more than the evidence shows. An evidenced "could not reproduce on this version" is a pass and a complete result — reporting a negative faithfully is the job. It fails when the report states or implies a confirmed reproduction that its artifacts do not support, when it reports a reproduction while its artifact shows an adjacent failure, or when it presents a guess about the cause as an established finding. | required |
| conventions-and-disclosure | The repo's stated contribution policy and bug-report template asks in the repo-facts block (live: `CONTRIBUTING.md`, the repo's issue and PR templates, and any AI-use policy file), read against the text of the claim comment and the repro report. | Every requirement the repo actually states is met by the posted words. Where the policy requires contributors to disclose AI assistance, the package discloses it; where the bug template asks for named fields, the report supplies them. A repo that states no such requirement passes automatically — silence is not a restriction, and this check never invents a convention the repo has not stated. It fails when a stated requirement goes unmet in the package, most commonly an AI-use disclosure the policy demands and the comments omit. | required |
| claim-is-specific | The claim comment, read against the issue it is posted on. | The claim identifies this issue in particular — it names the version and behaviour, or the file, function or test at stake — so it could not be pasted unchanged onto a different issue. It also promises only what the author controls: an investigation, a reproduction, a report. It fails on boilerplate that would fit any issue ("please assign me", "I'm interested, can I work on this"), and on a promise of a fix or a delivery date, which is a commitment the author cannot guarantee. | required |
| control-run-shown | The repro report's artifacts, looked at for a second run alongside the failing one. | The package includes a contrasting run — a known-good version, an unaffected input, or the pre-change behaviour — that isolates the failure rather than leaving it as a single observation. | preferred |
| artifact-in-context | The output excerpt or log in the repro report. | The artifact carries the lines around the failure — the command that produced it and enough surrounding output to place it — rather than a single line lifted out of its run. | preferred |

## Verdict rule

Accept the package as ready to post only if every `required` check grades
`pass`. Any single `required` check graded `fail` holds the package, and a
`required` check graded `unclear` counts as a fail — proof I cannot verify is
proof that is not ready to go upstream.

`preferred` checks never change the verdict. They are reported with their
grades either way, and they describe the difference between a package that is
merely sufficient and one a maintainer can act on immediately.

When the package is a claim-only draft, the checks whose evidence is the repro
report (`environment-recorded`, `steps-followable`, `behavior-matches-issue`,
`outcome-stated-honestly`, `control-run-shown`, `artifact-in-context`) are
reported `unclear` with the evidence line `not yet applicable: claim-only
draft` and are left out of the verdict rule entirely. The verdict then rests
only on `claim-is-specific` and `conventions-and-disclosure`, and answers the
narrower question: is this claim comment ready to post?
