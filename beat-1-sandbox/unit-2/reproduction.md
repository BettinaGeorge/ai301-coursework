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

<!-- BETTINA: paste the PERMALINK to your claim comment here (on the comment's
timestamp, Copy link), then paste the exact text you posted underneath it. -->

**Reproduction comment**

<!-- BETTINA: same — permalink, then the exact text you posted underneath. -->

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

<!-- ⬇ BETTINA: REWRITE THIS PARAGRAPH IN YOUR OWN WORDS. The facts above are
fixed; this is the reasoning, and it is what the 2 points are for. -->

My check reads both of those lines as requirements and fails the package if any
of them goes unmet. The policy line here sets no disclosure requirement at all —
it asks that comments be human-written, which this package satisfies — but the
template line names seven separate fields, and my check treated every one of
them as mandatory. So a package that proves the bug properly gets held for a
missing template field. Comparing it with `pkg-20`, where ghostty's policy says
outright that "all AI usage in any form must be disclosed" and the comments do
not disclose, shows the distinction I missed: a stated *policy* requirement is
a hard gate, and a bug template's list of asks is not.

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

<!-- ⬇ BETTINA: REWRITE IN YOUR OWN WORDS. -->

This check exists because the eval set contains exactly one `disclosure` package
and no other check in my rubric can see that family at all. Every other check I
wrote reads the proof — the environment, the steps, the artifact, the honesty of
the conclusion — and `pkg-20` passes all of them. It is an excellent
reproduction. What makes it a reject is entirely about the words next to the
proof: ghostty's policy requires disclosing AI use and the comments do not. With
no conventions check, my rubric scores 19/20 and still fails on the category
floor. That is the same trap as Unit 1's `policy` category, which is why I wrote
this one in from the start rather than discovering it in a run.

**Trade-offs**

<!-- ⬇ BETTINA: REWRITE IN YOUR OWN WORDS. -->

What it gives up is precision: by treating bug-template field asks with the same
force as stated policy requirements, it holds two packages that a maintainer
would have been glad to receive. `pkg-03` and `pkg-05` are both real
reproductions with artifacts and controls, and both were rejected for unmet
template fields rather than for anything wrong with their proof.

I know the narrower version — fail only on an explicitly stated policy
requirement, treat template asks as preferred — would fix both, and would leave
`pkg-20` rejecting, because `pkg-20` fails on the policy line and not the
template line. I did not make that change. `disclosure` is a single-package
category, so that one package is the entire category floor; the eval README's
canary rule exists for exactly this move, and a confirming full run costs about
$4 to chase a score that earns no points on its own. Holding two good packages
is the price of reliably catching the one that decides the floor, and at 18/20
with every category matched I would rather bank a run I trust than spend
credit improving a number the rubric does not score.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
