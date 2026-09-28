# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54

**Verdict output**

Live-mode run, 2026-09-29, on three candidates; all three accepted and ranked by
fit, with `#54` first. Output verbatim:

All evidence gathered. Grading against the rubric.

## Repo-level checks (shared by all three candidates)

| Check | Grade | Evidence |
|---|---|---|
| commits-alive | pass | All 5 latest `main` commits by `Aburke225` (human, no `[bot]` suffix), dated 2026-09-16 ×3 and 2026-08-24 ×2 — all within 90 days of today |
| responds-to-issues | pass | Repo created 2026-09-10, so every issue is <30 days old and all sample rows are ignored per rubric; fallback satisfied — `Aburke225` (COLLABORATOR) commented on #52 and #43 on 2026-09-16, 13 days ago |
| repo-in-use | pass | `archived = False`; no releases, but `pushed_at = 2026-09-16` (13 days) satisfies the 90-day branch of the OR |
| policy-allows-ai | pass | `docs/CONTRIBUTING.md` and `.github/PULL_REQUEST_TEMPLATE.md` never mention AI; no `AI_POLICY.md`. Silence passes |

`unclaimed` deserves a note: every claim comment across all three issues is from an `author_association: NONE` account — classmates, not maintainers. The Path Review house rule says student claim comments don't block, so all three pass despite being visibly crowded. No issue has an assignee, and the only linked PR anywhere (#64 → PR #1) is closed and merged, and is a Unit-2 write-up rather than a fix attempt.

## Ranked read-out — all three accepted

**1. #54 — Resume section detection fails on leading whitespace.** The best fit. It's the only one of the three that changes Python *source* (`_detect_sections()` in a 145-line `resume_parser.py`) plus its tests — squarely the "read a codebase I didn't write well enough to change one thing safely, and fix tests that prove it" goal. It ships a copy-pasteable repro with observed (`[]`) vs expected (`Education, Skills`), names the three failing tests, and the fix is localised to two files with no design decision left open.

**2. #64 — Relevance scorer "partial overlap" fixture.** Fully determined: the body states the fix outright ("fix the fixture so the overlap is genuinely partial"), so nothing is left to design, and it's one file with one `xfail` marker to drop. Ranks below #54 only because it's a test-fixture edit rather than a source change, exercising less of the codebase-reading skill.

**3. #63 — README scorer fixture too short.** Equally small and well-evidenced, but it leaves a choice — "Extend the fixture (**or** correct the assertion)" — and the fit profile explicitly ranks issues lower when a decision has to be made before starting. Rubric-wise it's still bounded and still accepts.

One tension worth recording: `maintainer-in-thread` fails on all three. Every comment is student-to-student, so nobody has had a maintainer confirm their reading yet. That's a preferred check, so it changes no verdict — but on #63 it means the extend-vs-fix-assertion decision has no maintainer steer behind it.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
    "checks": [
      {"name": "commits-alive", "grade": "pass", "evidence": "5/5 latest main commits by human Aburke225, dated 2026-09-16 and 2026-08-24, all within 90 days of today"},
      {"name": "responds-to-issues", "grade": "pass", "evidence": "Repo created 2026-09-10 so all issues are <30 days old and every sample row is ignored; fallback met by COLLABORATOR Aburke225 commenting on #52 and #43 on 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=False and main pushed 2026-09-16, 13 days ago"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "One fix to _detect_sections() in the 145-line resume_parser.py plus 3 named tests in tests/unit/test_resume_parser.py; no umbrella, no design debate, no core-internals claim"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, no linked PRs; sole claim from DuBaem is author_association NONE, ignored under the Path Review house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template contain no mention of AI; silence passes"},
      {"name": "labeled-friendly", "grade": "pass", "evidence": "Labels include 'good first issue', applied by Aburke225 on 2026-09-10"},
      {"name": "maintainer-in-thread", "grade": "fail", "evidence": "Both comments have author_association NONE; no Owner/Member/Collaborator has commented"},
      {"name": "spec-included", "grade": "pass", "evidence": "Body names the function, the file, a runnable repro with observed [] vs expected Education/Skills, and the related failing tests"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/64",
    "checks": [
      {"name": "commits-alive", "grade": "pass", "evidence": "5/5 latest main commits by human Aburke225, dated 2026-09-16 and 2026-08-24, all within 90 days of today"},
      {"name": "responds-to-issues", "grade": "pass", "evidence": "All repo issues are <30 days old so sample rows are ignored; fallback met by COLLABORATOR Aburke225 commenting on #52 and #43 on 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=False and main pushed 2026-09-16, 13 days ago"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Single fixture fix in tests/unit/test_relevance_scorer.py with one xfail marker to remove; expected behaviour stated as 'fix the fixture so the overlap is genuinely partial'"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignees; only linked PR (#1) is closed and merged and is a Unit-2 write-up, not a fix; claims from rishabhlingam and srithimahi are author_association NONE, ignored under the house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template contain no mention of AI; silence passes"},
      {"name": "labeled-friendly", "grade": "pass", "evidence": "Labels include 'good first issue', applied by Aburke225 on 2026-09-10"},
      {"name": "maintainer-in-thread", "grade": "fail", "evidence": "All 5 comments have author_association NONE; no Owner/Member/Collaborator has commented"},
      {"name": "spec-included", "grade": "pass", "evidence": "Body names the test function, the file, the repro command, and the observed failure 'assert 1.0 < 0.9'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/63",
    "checks": [
      {"name": "commits-alive", "grade": "pass", "evidence": "5/5 latest main commits by human Aburke225, dated 2026-09-16 and 2026-08-24, all within 90 days of today"},
      {"name": "responds-to-issues", "grade": "pass", "evidence": "All repo issues are <30 days old so sample rows are ignored; fallback met by COLLABORATOR Aburke225 commenting on #52 and #43 on 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived=False and main pushed 2026-09-16, 13 days ago"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Single fixture in tests/unit/test_readme_scorer.py with one xfail marker; the extend-vs-adjust-assertion choice is a bounded either/or inside one test, not an open product decision"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignees, no linked PRs; claims from AliceKindle2, riyag0 and Stephen-Agyemang are all author_association NONE, ignored under the house rule"},
      {"name": "policy-allows-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template contain no mention of AI; silence passes"},
      {"name": "labeled-friendly", "grade": "pass", "evidence": "Labels include 'good first issue', applied by Aburke225 on 2026-09-10"},
      {"name": "maintainer-in-thread", "grade": "fail", "evidence": "All 5 comments have author_association NONE; no Owner/Member/Collaborator has commented"},
      {"name": "spec-included", "grade": "pass", "evidence": "Body names the test function, the file, the repro command, and the observed failure 'assert 51 > 100'"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

**Run history**

1. Smoke run, `--limit 3`: 2 of 3 matched. `issue-01` (gold `accept`) was rejected
   on `scope-bounded`.
2. Change: widened `scope-bounded` so that an issue naming several specific files
   in one deliverable is not treated as an umbrella issue. `issue-01` is a conda
   docs task listing five files to touch, all in a single pull request.
3. Full run: **18/20**. Categories: claimed 4/4, clear-accept 6/8, dead-repo 3/3,
   policy 1/1, scope 4/4. Misses: `issue-14`, `issue-19`.
4. Live mode on three Path Review candidates: all three rejected on
   `responds-to-issues`. The repo is 18 days old, so every row in the response
   sample was discarded by my young-issue clause and the fallback then required a
   maintainer comment in the issue's own thread, which none had.
5. Change: widened the `responds-to-issues` fallback to accept a maintainer-badged
   comment anywhere in the repository within 45 days, not only in this issue's
   thread.
6. Confirming full run, `--save-run eval-run.txt`: **18/20**, same category
   tallies, same two misses. This is the run committed in `eval-run.txt`.

**Issue analysis**

`issue-19` (zxcalc/zxlive#517, "Selecting large subgraphs in proof mode freezes the
UI"). My rubric graded it **reject**; the gold label is **accept**
("maintainer-diagnosed performance bug with named causes, unclaimed"). The check
that failed it was `scope-bounded`.

The bundle's body opens with "There are two potential causes which should be
fixed:" — "The matchers are slow for certain rewrites (quadratic instead of
linear)" and "UI update is waiting for the matching thread to finish" — followed
by three numbered "Additional suggestions". The issue line reads "opened by
RazinShaikh (COLLABORATOR) on 2026-05-08".

I think my checklist got `issue-19` wrong because it saw five numbered points and
treated them like five separate jobs. It missed that a maintainer had already
broken down the bug, which actually made the issue easier to approach.

**Check rationale**

From the checks table in `rubric.md`:

> | responds-to-issues | The "maintainer first-response sample" under Repo facts,
> plus the `author_association` field on each comment in this issue's own thread
> (live: Owner / Member / Collaborator badges on recently-updated issues). | At
> least one first response from an Owner, Member, or Collaborator arrived within
> 45 days in the response sample. When reading the sample, ignore rows for issues
> that had been open fewer than 30 days at the capture date: a young issue without
> a reply is not evidence of neglect. If every row is ignored on that basis, or the
> sample is absent or empty, this check passes instead when a maintainer-badged
> account has commented within 45 days anywhere the evidence reaches — this issue's
> own thread, or any other issue or pull request thread in the same repository.
> That second fallback exists because a repository younger than the response window
> has no old issues to sample, and a young repository is not a neglected one. Grade
> `unclear` only when no maintainer-badged comment can be found in any available
> source. | required |

This check has two fallbacks because a single cutoff kept failing repos that were
not actually inactive. Repos can show that maintainers are active in different
ways. Conda had a response, but it took just over 30 days — `issue-01`'s sample
reads "#16275 (opened 2026-06-24 by a maintainer): 32.9 days", and my original
30-day line rejected a project that had pushed five commits the day before
capture. Path Review was only 18 days old, so it couldn't possibly have older
issues to measure. A single cutoff can reject both even though neither is
necessarily inactive. So the window went to 45 days, young issues stopped counting
as evidence of neglect, and the last fallback looks for a maintainer anywhere in
the repo rather than only in one thread.

**Trade-offs**

The risk with my last change is that activity elsewhere in a repo could make an
ignored issue look safe to pick up. A maintainer might be replying to other people
while the specific issue I'm considering has gone unanswered for a year.

My canary was `issue-14` (LegalQuants/lq-ai#490, gold `accept`). It failed
`responds-to-issues` before the change and still fails after it, because its
bundle has no maintainer comment anywhere for the widened fallback to find. The
change cost nothing on the eval — 18/20 before, 18/20 after, with identical
category tallies — and it is what let the rubric grade a three-week-old classroom
repo at all.

---

## Selection rationale

**Selection rationale**

1. **Fit and time.** This issue makes sense to me: the parser misses headings when
   a resume has spaces at the start of the line. It's one Python function with
   failing tests that show what should happen, so I think I can make time to work
   on it this week.

2. **What the verdict got right, and what I weighed that the rubric could not.**
   The rubric got the repo and issue checks right, but it doesn't know I'm already
   behind and this would be my first open-source contribution. I weighed whether I
   could understand the bug and finish the fix.

3. **Anticipated difficulty in claiming it.** I'd feel a little awkward claiming it
   after DuBaem, and I'd worry about doing the same work. Knowing the course
   expects shared issues makes me more comfortable opening my own PR.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
