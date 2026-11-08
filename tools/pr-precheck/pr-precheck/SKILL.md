---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

Looking at a PR package, decide whether the pull request is ready to submit. A PR package contains a plan.md with its deviation notes, a branch's diff, a draft PR title and description, test evidence, and the issue that the plan belongs to. The tool reads these artifacts against the plan's stated boundary, the test plan, and the repo's stated template and disclosure asks.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Live Mode: The tool reads the plan.md and its deviation notes from the PR package, the branch's diff from the working copy using `git diff main...HEAD`, the draft PR title and description from the PR package, the test evidence from the PR package, and the issue that the plan belongs to from the PR package. A house-chain student reads these inputs instead of fetching them.

Eval mode: The tool reads the PR package bundle which should be a markdown file with all of the relevant PR information (plan.md, branch's diff, draft PR title and description, test evidence, issue)  nothing is fetched, and every check runs with the full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, the tool reads scope.md to determine which repository the pull request may target and what the house rules are for that repository. The tool should refuse to grade any PR package that targets a repository other than the one specified in scope.md. If the repo line in scope.md is an unfilled placeholder, the tool should refuse to grade the PR package and instruct the user to fill in the correct repository. In eval mode, scope.md is ignored entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, the tool reads voice-guide.md to determine the rules for the PR title and description. The tool should report any broken rules in the PR title and description, but it should not change the verdict on its own. In eval mode, voice-guide.md is ignored entirely.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Rubric.md defines the checks and the verdict rule, references/evidence-guide.md maps where each evidence family lives, and procedure.md is executed as written. If the procedure is silent on a step, the tool should report the gap and never improvise around it. If rubric.md or procedure.md has no content, the tool should refuse to grade the PR package and report the issue.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict space is binary: `accept` means the pull request is ready to submit, and `reject` means the pull request should be held, any unclear grades are treated as failures. The tool should end its reply with the fenced JSON block below.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

These are not style advice; they are interface guarantees the master
tool honors and the bar assumes:

- **Evidence first.** No check is graded without naming the fact or
  quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** A terse complete PR can be
  ready and a beautiful confident one can be hiding drift. Every check
  reads the artifact itself against the plan, the issue, and the
  stated standards, never the formatting.
- **The rubric decides, not the run.** If a check passes by its stated
  condition but feels wrong, it still passes; the fix belongs in the
  rubric, not in the run.
- **The procedure decides how, not the run.** The tool follows
  `procedure.md` as written and reports its gaps instead of silently
  inventing steps.
- **Unclear defaults to fail.** Treat `unclear` as the rubric's
  verdict rule directs; where the rule is silent, an unverifiable
  claim is a failing one. A PR you cannot verify from the package is a
  PR that is not ready to submit.