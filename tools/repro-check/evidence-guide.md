# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
Where it lives: the repro report's environment record (version, OS,
commit/branch if given), read against the repo-facts block and the
issue's stated target version/OS. In live mode: the same fields in the
student's draft comment, read against what the issue thread says.

What good looks like: the recorded version and OS are specific enough
to stand up the same runtime (not "latest" or "a recent build"), and
if they differ from what the issue targets, the report says so instead
of leaving the mismatch implicit. A record that's specific but silently
targets the wrong version is not sufficient.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
Where it lives: the repro report's numbered steps, read against the
repo-facts block (for install/build commands that must match the repo)
and the issue's description (for the starting state and trigger).

What good looks like: a stranger with no more context than the steps
themselves, the environment record, and the repo can follow them in
order and land on the failure — no skipped setup, no step that
silently assumes something the reader wasn't told to do first. If the
steps require a person to already know the codebase to fill a gap, they
fail this even if there are only three of them.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
Where it lives: the artifact(s) attached at the end of the report
(output excerpt, log, screenshot), read against the issue's description
of the failure and against the report's own actual-result claim.

What good looks like: the artifact itself — not the surrounding prose —
contains the failure the issue describes (the same error, the same
wrong output, the same crash), not a different error, a warning, or a
success message the report re-describes as a failure. If the artifact
shows an adjacent problem instead of the one claimed, this fails even
if something did go wrong.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->
Where it lives: the report's claims (expected/actual, "this
reproduces," "this does not reproduce") read against what its own
evidence — environment, steps, artifact — actually shows.

What good looks like: every claim in the report is no stronger than
its evidence. An honest "I could not reproduce this" backed by a genuine
attempt — real environment, real steps followed, a real (non-)result —
is a complete, passing report, not a partial one. Treat it as equal in
kind to a confirmed repro, not as a fallback that merits weaker steps or
no artifact. The bar moves with the claim: what minimal_steps and
artifact_check are checking for is that the evidence matches whichever
claim was made, not that the claim was "yes, it broke."

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
Where it lives: the claim comment or draft comment, read against the
issue thread it responds to and the repo-facts block's stated
contribution policy and AI-use/comment-voice policy, when one exists.

What good looks like: default to PASS. A comms failure needs a
specific, pointable reason — not a vibe that the comment feels thin,
generic, or underwhelming. Fail only for one of:

- **Overpromising**: the comment guarantees something the repro
  evidence can't back — a fix timeline, a confirmed resolution, "this
  will be fixed by X." Specificity about the bug is good; specificity
  about the fix is not this report's job to promise.
- **Mismatch**: the comment's claimed finding doesn't match what the
  steps/artifact actually show.
- **Policy violation**: the repo-facts block states an actual AI-use
  or comment-voice policy, and the comment doesn't meet it *as that
  policy is actually written* — don't assume what satisfying it looks
  like. Some repos require an explicit disclosure line; others just
  require the comment read as genuinely human-voiced, with no
  disclosure sentence needed at all. Check the repo-facts block's exact
  wording before failing this.

If the repo-facts block says no AI policy is stated, there is nothing
to disclose and nothing to fail here on those grounds — do not apply a
default disclosure requirement the repo itself doesn't have. A comment
that is boilerplate-y, terse, or skips template headings still passes
if it doesn't hit one of the three above. Judge the claim against the
evidence and the repo's actual stated policy, not an assumed one.
