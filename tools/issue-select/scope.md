# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s1`

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

I am a student at UNC taking AI 301, and this is my first open-source
contribution. My programming experience comes from coursework rather
than from production codebases, and Python is the language I am most
comfortable reading and writing. I have used git and GitHub for class
projects, but I have not worked inside a large unfamiliar repository
before.

What I want to get better at this term is reading a codebase I did not
write well enough to change one thing in it safely, and writing or
fixing tests that prove the change actually works.

Rank accepted issues higher when the bug has a clear reproduction or a
failing test showing exactly what is wrong, when the fix is localised to
one or two files, and when the issue states the expected behaviour
rather than leaving it to be designed. Rank them lower when they require
standing up heavy infrastructure (CI pipelines, databases, Docker), when
a product or design decision has to be made first, or when the change is
spread thinly across many files. I would rather take a small,
well-specified issue than an interesting vague one.
