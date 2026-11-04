# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

Look for evidence of the diagnosis and grounding of said plan by looking for the proposed root cause and plan to handle it in the candidate plan section (or plan comment). Check the issue, repro evidence and comment thread for any supporting evidence of root cause identified or contradictions in plan or evidence gathered

Good looks like logic from both candidate's plan and diagnosis track with established truths found in the issue statemnet and reproduction evidence.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

To find evidence of a bounded-scope look in the issue's candidate plan where they discuss the proposed changes to address root cause.

This is good if the files listed are a bounded scope for the issue and works on problem discussed in grounded diagnosis.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

The executability evidnce will be located in the candidate section/comment where we are looking for their plan to execute the resolution of the issue.

A good plan should consist of the intended change/fix, list of files that will be affected, expected result of change and how testing will be executed.
A stranger should be able to
start executing without asking the author anything

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

The plan evidence should be found in the candidate's plan section/comment along with supporting evidence in the repro evidence section/comment.

Good will look like a detailed plan showing how they will test their change based on reproduction evidence of issue and achieving expected result.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

The honesty evidence can be found in the canddiate plan and comment, along with issue context and repro evidence.

Candidate should be communicating honestly throughout executin plan and bring up any unknowns with hypothesises spported by issue context and repro evidence.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

The candidate’s plan comment and other comments in the issue thread, read against the maintainer signals (thread highlights or the live thread) and the repo-facts block’s stated templates, contributing asks, and contribution policy, including AI-use disclosure requirements.

The candidate’s comments follow the repo-facts block’s stated templates, contributing asks, and contribution policy (including any required AI-use disclosure), and respond to what maintainers have actually said in the thread rather than reading as boilerplate.
