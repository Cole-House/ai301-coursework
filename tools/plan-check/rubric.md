# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's diagnosis section and the reproduction evidence (repro steps, error output, logs) | The diagnosis names the root cause of the issue, and that cause is supported by the reproduction evidence rather than assumed. | required |
| bounded-scope | The plan's scope statement, its list of files or code areas to be changed, and its fix and test descriptions | The plan names where the change will be made (a file, module, or code path specific enough to locate in the repo) and states what is in scope and out of scope, and nothing in the fix description implies changes outside that named area. Tests and fixtures that accompany the fix are expected and need not be listed separately. A plan may leave exact functions to be pinned in the PR if the named area is already bounded. | required |
| test-success | The plan's test section and the repro's expected outcome | The test plan defines a clear successful outcome and compares it against the repro's expected outcome, so a passing test shows the bug is fixed. | required |
| evidence-base | Files cited in the plan and the repo evidence gathered | Every file cited in the plan was actually examined in the repo evidence. | preferred |
| comms-compliant | The comment thread and the candidate's comments, checked against the repo-facts block's stated templates, contributing asks, and contribution policy (including AI-use disclosure requirements) | Every candidate comment follows the templates the repo-facts block states, meets the contributing asks, and complies with the contribution policy, including any AI-use disclosure the repo requires. |preferred|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
For an accept all required checks must pass, otherwise it is a reject. If unclear if the comment is a plan return "Unclear".
