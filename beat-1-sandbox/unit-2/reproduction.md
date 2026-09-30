# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`.

---

## Your identity upstream

**GitHub username**

BettinaGeorge

---

## Posted upstream

**Claim comment**
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5893060296
I'd like to take this one on. Per the issue body, _detect_sections() in ingestion/parsers/resume_parser.py anchors its patterns at line start (^Experience, \nExperience), so indented text comes back with an empty detected_sections. Reading the source, that matches what I see — but I haven't run it yet.

I'll run the reproduction from the issue body plus the xfail-marked tests in tests/unit/test_resume_parser.py against current main, then post a repro report with my environment, the exact steps and the output I see, whether or not it reproduces.

This is my first open-source contribution, so flagging that. I can see @DuBaem has already posted a reproduction. I'll write mine from my own run rather than confirming theirs. I'm also working with AI assistance as part of AI 301 coursework.

**Reproduction comment**
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5905836222
I reproduced this on my local clone. With leading whitespace, the parser returns no detected sections. Removing the indentation from the same input detects both Skills and Education.

**Environment**
- macOS 26.5.1
- Python 3.11.14
- pypdf 6.19.0
- Commit: `f89c06fc3ff292df2a04a39ac51319d32a76b779`

**Setup**

From the repository root, I ran:

```bash
python3.11 -m venv .venv
.venv/bin/python -m pip install -e ".[dev]"
```

**Reproduction and control**

I ran this from the repository root. The control uses `dedent()` to remove the leading indentation from the same text.

```bash
.venv/bin/python - <<'PY'
from ingestion.parsers.resume_parser import ResumeParser
from textwrap import dedent

text = (
    "\n    John Smith\n"
    "    john@example.com\n"
    "\n"
    "    Education:\n"
    "    - B.S. Computer Science\n"
    "\n"
    "    Skills: Python\n"
)

parser = ResumeParser()
print("Indented:", parser.parse(text).metadata["detected_sections"])
print("Without indentation:", parser.parse(dedent(text)).metadata["detected_sections"])
PY
```

Actual output:

```text
Indented: []
Without indentation: ['Skills', 'Education']
```

Expected: the indented input should also detect Education and Skills.

**Tests**

I also ran:

```bash
.venv/bin/python -m pytest tests/unit/test_resume_parser.py -rx -q
```

Result:

```text
5 passed, 5 xfailed in 1.08s
```

The five expected failures were:
- `test_parse_single_column_resume_text`
- `test_parse_resume_no_work_experience`
- `test_parse_markdown_resume`
- `test_detect_sections`
- `test_strip_markdown_syntax`

Each was marked with the reason “issue #54: resume section detection fails on leading whitespace.”

**Outcome**

The direct reproduction matches the reported bug. The control detects both sections once the indentation is removed. I haven’t changed the parser code.

I’m working with AI assistance as part of AI 301 coursework.

## Eval iterations

**Run history**

1. One full run of all 20 scored packages, `--save-run eval-run.txt`: **18/20**.
   Categories: clear-accept 6/8, disclosure 1/1, no-evidence 4/4,
   unfollowable-comms 3/3, wrong-target 4/4. Bar: PASS.
   Disagreements: `pkg-03` and `pkg-05`, both graded `reject` against a gold
   label of `accept`, both on `conventions-and-disclosure`.

   This first run cleared the bar and the category floor, so it is the run
   committed in `eval-run.txt`. I did not re-run: the change the disagreements
   point to would touch the one check holding the single-package `disclosure`
   category, and the reasoning for leaving it is in Trade-offs below.

**Package analysis**

`pkg-03` (ripgrep). My rubric graded it **reject**; the gold label is **accept**
("exact-steps repro on current version with a minus-replace control"). The check
that failed it was `conventions-and-disclosure`, and no other check on the
package failed.

The package's repo-facts block carries two separate lines. The policy line reads:
"AI-assisted coding is welcome with a human in the loop who understands the work;
comments to maintainers must be written by humans in their own words, and
AI-generated comments may be hidden." The template line reads: "template asks for
the ripgrep version, how it was installed, the operating system, a description of
the bug, steps to reproduce, actual behavior, and expected behavior."

The mistake here was treating everything the repo asked for as equally mandatory. Ripgrep’s policy asks for human-written comments, which this package satisfies; it does not require AI disclosure. My check still rejected the package because I treated all seven fields in the bug template as hard requirements, even though the reproduction showed the bug clearly. Comparing this with `pkg-20` helped me see the difference: ghostty explicitly requires disclosure of all AI use, and the comments leave that out. Missing a template field and breaking an explicit policy should not automatically carry the same weight.

**Check rationale**

From the checks table in `rubric.md`, as uploaded to `tools/repro-check/`:

> | conventions-and-disclosure | The repo's stated contribution policy and
> bug-report template asks in the repo-facts block (live: `CONTRIBUTING.md`, the
> repo's issue and PR templates, and any AI-use policy file), read against the
> text of the claim comment and the repro report. | Every requirement the repo
> actually states is met by the posted words. Where the policy requires
> contributors to disclose AI assistance, the package discloses it; where the bug
> template asks for named fields, the report supplies them. A repo that states no
> such requirement passes automatically — silence is not a restriction, and this
> check never invents a convention the repo has not stated. It fails when a stated
> requirement goes unmet in the package, most commonly an AI-use disclosure the
> policy demands and the comments omit. | required |

I included this check because a strong reproduction can still miss an explicit contribution requirement. `pkg-20` passes every other check in my rubric: the environment, steps, evidence, and conclusion all hold up. The problem is that ghostty requires AI-use disclosure, and the comments do not provide it. Without this check, I would get 19/20 overall but still fail the disclosure category floor. That is the disclosure trap: a higher total score does not mean the rubric catches every required category. I recognized the same pattern from Unit 1’s policy category, so I included this check from the start.

**Trade-offs**

The trade-off is that my check is too strict about template fields. It rejected `pkg-03` and `pkg-05` even though both had real reproductions with artifacts and controls. Their proof was not the issue; the missing template fields were.

I could narrow the check so explicit policy requirements are mandatory and template fields are preferred. Based on the package analysis, that should fix both disagreements while still rejecting `pkg-20` for missing the required disclosure. But I did not make or test that change. Since the disclosure category has only one package, changing this check would need the canary validation and a confirming full run, which costs about $4. My existing run already passed at 18/20 and met every category floor, so I chose to keep that verified result. That leaves two false rejections, which is a limitation I can explain, rather than claiming the narrower version works without running it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
