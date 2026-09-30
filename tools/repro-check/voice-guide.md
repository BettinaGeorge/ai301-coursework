# Voice guide: how I talk upstream

<!-- BETTINA: this is drafted from things you actually said in working
through Unit 1 — being new, being behind, and feeling awkward claiming an
issue a classmate had already claimed. Read it once and change anything that
doesn't sound like you. Eval mode never reads this file, so nothing here can
cost you eval points; it is graded as part of the skill you upload. -->

## Who I am in threads

I am a student making my first open-source contribution, working in a course
sandbox repo. I am not an expert in this codebase and I am not going to
pretend to be one. What a reader can expect from me is that anything I state
as fact, I actually ran, and that I say plainly when I am unsure or when
something did not work.

## Rules I write by

### Rule: Promise the artifact, never the outcome or the date

I only promise things I control: that I will investigate, and that I will post
what I find. I do not promise a fix, and I do not promise a day — I have been
behind before and the temptation to sound keen by naming a date is exactly
when I should not.

- Wrong: "I'll have a fix up by tomorrow!"
- Right: "Picking this up now; I'll post a repro report with my environment and output once I've run it."

### Rule: Name the specific thing, or say nothing

Every comment I post has to contain something that is true only of this issue
— the version, the failing test, the function, the observed output. If I strip
that out and the comment would fit on any other issue, it is not worth posting.

- Wrong: "I'm interested in this issue and would like to work on it."
- Right: "Looking at `_detect_sections()` in `resume_parser.py` — section headers are anchored to the start of the line, so indented resumes return `[]`."

### Rule: Say I'm new instead of performing expertise

Flagging that this is my first contribution costs me nothing and tells a
maintainer how to read the rest of my comment. Hedging language that tries to
sound senior does the opposite.

- Wrong: "As expected, this is a trivial regression in the parser layer."
- Right: "This is my first contribution, so flagging that — here's what I observed, and I may be missing context."

### Rule: My own words, even on a shared issue

Classmates may be on the same issue. I never piggyback on someone else's
proof. If I did not run it, I do not confirm it, and I write my report from my
own run even when it reaches the same conclusion as theirs.

- Wrong: "Same as above, can confirm!"
- Right: "Reproduced independently on my own setup — environment and output below; this matches what @DuBaem reported."

### Rule: Report what happened, including when nothing did

A run where the bug did not appear is a real result and I post it as one, with
the same environment and output I would have given for a reproduction. I do
not quietly retry until I get the answer I wanted.

- Wrong: *(say nothing, and try again later hoping it breaks)*
- Right: "Could not reproduce on this version — environment, steps and the actual output below, in case that narrows it."

## Things I never post

- A date, a deadline, or "by tomorrow".
- A promise to fix something before I have reproduced it.
- "Can I be assigned?" with nothing else in the comment.
- Enthusiasm standing in for content — "great project!!", "amazing catch!!".
- A confirmation of anyone else's result that I did not run myself.
- A guess about the cause written as though I had established it.
