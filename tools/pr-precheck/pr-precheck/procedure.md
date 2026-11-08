# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

Read the package in this order before grading any check. Find each part using evidence-guide.md, which gives its location in both eval mode and live mode. Write down the notes listed for each part; later stages use these notes instead of re-reading.

1. **The issue and the plan** (evidence-guide.md → Plan fidelity, Test evidence). Read these first, so the diff is judged against what was promised, not rationalized after seeing the code. Note:
   - the scope list: every file the plan names
   - the boundary: everything marked not in scope
   - the step list, with each step tagged "code" (changes a file) or "verify" (runs a check)
   - the test plan
   - any deviation notes
2. **The PR title and description** (evidence-guide.md → Plan fidelity, Standards and comms). Read these before the diff, so their claims are recorded before you see whether the diff supports them. Note:
   - the claims list: each claim about what changed or how closely the plan was followed
   - the disclosure list: every limitation, known issue, or incomplete-work note
   - whether the issue is referenced
3. **The diff and commits** (evidence-guide.md → Diff quality). Note:
   - every changed file
   - for each hunk, the code step it serves, or "none"
   - each commit message
4. **The test evidence** (evidence-guide.md → Test evidence). Note:
   - each command run, with its before and after output
   - each repo check result, if the repo requires any
5. **The repo's asks** (evidence-guide.md → Standards and comms). Read these last, since they judge the form of everything above. Note:
   - each required template section
   - each required disclosure
   - each house rule
   - any maintainer direction in the thread
   - If the repo states no template or no policy, note "none stated."


## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

For each check in rubric.md, gather its evidence as a pairing between two of your notes. Find each source using evidence-guide.md.

- **Silent drift:** pair the diff's file list against the plan's scope list (evidence-guide.md → Plan, Diff). Record files outside scope. Pair the plan's step list against the hunk notes. Record steps with no matching hunks or verified checks. Pair the claims list against the diff. Record any claim the diff contradicts or drifts doing more or less.
- **Not tested:** pair the test evidence against the plan's test plan and the repo's required checks (evidence-guide.md → Test evidence, CI). Record which required checks ran and passed, and whether there is observable evidence shoiwng expected and actual are both stated and match.
- **Unreviewable:** from the hunk notes, record every hunk marked "none" and classify it: debris, unrelated formatting or refactor, or a needed extra. For each needed extra, record whether the description explains it.
- **Standards wall:** pair the contributing-doc notes against the description and commits (evidence-guide.md → Contributing docs). Record each missing template section, missing disclosure, and broken house rule.
- **Honest outcome:** for each problem recorded above, check the disclosure list. Record whether that problem was disclosed.


## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Run every check in rubric.md, in rubric order: Silent drift, Not tested, Unreviewable, Standards wall, Honest outcome. Do not stop after a failure.
2. Grade each check only from the evidence recorded for it. Re-read the package only to fill a missing note.
3. For each Required check, go through the problems recorded for it one at a time:
   - Look the problem up in the Honest outcome record.
   - If it was disclosed, apply the honest-outcome rule in rubric.md. If the rule excuses it, mark it "excused" and note the disclosure that covers it.
   - Otherwise, mark it "counted." This includes problems that were never disclosed, and disclosed problems the rule says it cannot excuse.
4. Grade each Required check as one of:
   - **Pass:** the rubric.md pass condition is met, and every problem recorded for the check is excused.
   - **Fail:** at least one problem is counted.
   - **Unclear:** the package you were given is missing a part you need to judge (no plan supplied, diff cut off). Name the missing part. Do not guess.
5. Grade Honest outcome last:
   - **Pass:** every problem found by the Required checks was disclosed.
   - **Fail:** any problem was not disclosed.
6. For every grade, record the rubric.md pass condition, the evidence that decided it, and any excused problems with their disclosures.
7. If a stage of this procedure doesn't cover a situation, report the gap. Do not improvise a step.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Apply the verdict rule in rubric.md: the PR is ready only if every Required check passes. A check that passes with excused problems still counts as passing.
2. An unclear Required check counts as not passing. The verdict is not ready, and the reason is "could not confirm."
3. Preferred checks (Honest outcome) do not change the verdict. Report their grades alongside it.
4. If the verdict is not ready, the deciding check is the first failing Required check in rubric order. If none failed but one was unclear, it is the first unclear Required check. Quote its pass condition and the counted problem that broke it.
5. After the deciding check, list every other failed or unclear check with its counted problems, so the author can fix everything in one pass.
6. If the verdict is ready, quote no deciding check. List the pass evidence for each check tersley, then list every excused problem with the disclosure that covers it, so the maintainer sees the known gaps up front.