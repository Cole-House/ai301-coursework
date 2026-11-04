# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
Read the issue first, then the repro evidence checing to see if reproduced corrctly and root issue identified, then candidate plan checking to see if it tracks with the evidence so far and comes up with a logical plan, then thread highlights for auxilairy evidence to guage any problems with candidate plan.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
**Extract the plan's claims.** Copy verbatim: the stated root cause, the list of files to be changed, the test plan's success outcome, and every file path cited anywhere in the plan (as its own list).
2. **Pull the repro evidence.** Record the repro steps, observed behavior, expected behavior, and any error message, log line, or file named in the repro or issue.
3. **Pair the evidence per check.**
   - diagnosis-grounded: the root-cause quote next to the repro detail it relies on, or "none" if it's only asserted.
   - bounded-scope: files named as modified in the plan body that are missing from the scope list.
   - test-success: the plan's success outcome next to the repro's expected behavior.
   - evidence-base: each cited file marked "found (where)" or "not found" in the repo evidence.
4. **Log one line per check** with the exact quote or location relied on.


## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->
**Order.** Run the checks in this order: bounded-scope, diagnosis-grounded, test-success, evidence-base (preferred). Scope comes first because the later checks refer to the file list it establishes.

### 1. bounded-scope
1. List every file the plan says it will change, and next to each one record what the plan says will change in it.
2. Add any file that the plan's fix description or test plan implies must change but that is missing from the list.
3. **Pass** only if every file that will change appears in the list. If a changed file is implied but unlisted, **fail** and name the file.

### 2. diagnosis-grounded
1. State the plan's claimed root cause in one-two sentence.
2. Find the repro evidence that supports it: the error output, failing file or function, or observed behavior the cause explains. Record the specific detail.
3. **Look for contrasting evidence.** Search the repro and issue data for anything that points elsewhere or contradicts the claim: a different failing location, an error the diagnosis does not account for, behavior that would not occur if the claimed cause were true, or a symptom the plan ignores. Record each item found, or "none found."
4. **Pass** if supporting evidence exists and no contrasting evidence is left unexplained. **Fail** if the cause is only asserted, or if contrasting evidence is unaddressed. If the contrasting evidence is addressed in the plan, record how and pass.

### 3. test-success
1. Record the repro's expected outcome.
2. Record the plan's defined success outcome for its test.
3. Confirm the test plan's steps exercise the files and behavior listed in the scope, so the test runs within the intended scope. A test that only touches code outside the scope list does not show the fix worked.
4. **Pass** if the success outcome matches the repro's expected outcome and the test runs within the intended scope. **Fail** if the outcomes differ, the success outcome is vague, or the test never exercises the scoped files.

### 4. evidence-base (preferred)
1. Take the cited-files list from the evidence gathering step.
2. Mark each file "found" or "not found" in the repo evidence.
3. **Pass** only if every cited file is found.

- If the evidence a check needs is missing from the package (for example, no repro output at all), mark that check **fail** and write "evidence missing: <what was needed>." Do not infer the evidence from the plan's own claims.
- Absent evidence is different from contrasting evidence: absence means the check cannot pass, while contrasting evidence means the check is judged against it.
- For the preferred check, missing evidence is recorded as a miss but carries only its low weight.

A check may be graded from the evidence log alone when the log holds the exact quote or location for each item that check needs. Go back to the package only when a log entry is missing, ambiguous, or conflicts with another entry.

For each check, write the verdict, the evidence relied on, and any contrasting evidence or missing item, so a second executor reaches the same verdict.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
For an accept all required checks must pass, otherwise it is a reject. If unclear if the comment is a plan return "Unclear".
