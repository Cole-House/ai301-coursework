# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

**Where it lives (eval):**
- `## Plan context`: the plan's steps, its "Not in scope" boundary, its "Files:" list, and any deviation notes.
- `## Candidate PR` → `### Diff`: the files and hunks that actually changed.
- `## Candidate PR` → `### Description`: claims about what changed and how closely the plan was followed.

**Where it lives (live):**
- `plan.md` in your working copy, including its deviation notes.
- Your branch's diff: `git diff main...HEAD`, or the PR's "Files changed" tab on GitHub.
- Your draft PR title and description.

**What good looks like:** every changed file is in the plan's "Files:" list or covered by a deviation note; every plan step has a matching hunk; nothing named "Not in scope" is touched. Every claim in the description matches the diff. Drift runs both ways: a diff doing more than the plan, or less with no note, both fail.


## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

**Where it lives (eval):**
- `## Plan context`: the repro evidence and the test plan (what to re-run, what to expect).
- `## Candidate PR` → `### Test evidence`: the commands run and their before and after output.
- `## Repo facts`: any checks or suite the repo requires.

**Where it lives (live):**
- The test plan in `plan.md`.
- Your captured test output (terminal logs, screenshots), and the test section of your draft description.
- The PR's "Checks" tab on GitHub, and the CI config (`.github/workflows/`) for which checks the repo runs.

**What good looks like:** there is observable evidence in the test section where the plan's repro is re-run with the before (failure) and after (expected result) both shown; each test plan item has matching output; the repo's required checks show a visible pass. "Tests pass" with no output shown does not count.


## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

**Where it lives (eval):**
- `## Candidate PR` → `### Diff`: every hunk.
- `## Candidate PR` → `### Commits`: the commit list and messages.

**Where it lives (live):**
- Your branch's diff (`git diff main...HEAD`, or "Files changed" on GitHub).
- Your commit list (`git log main..HEAD --oneline`, or the PR's "Commits" tab).

**What good looks like:** every hunk serves a plan step, and the fix is visible and understandbale at a glance. Only code diffs implementing change and none of these appear: debug output, dead or commented-out code, formatting-only changes, edits to unrelated lines, or generated or lockfile churn the change didn't need. Only comtains atomic commit messages describe each small change made.


## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

**Where it lives (eval):**
- `## Repo facts`: the "pull requests" line (template and contribution asks) from CONTRIBUTING.md and the "contribution policy" line (including any AI-use policy). PR templates in the docs if mentioned
- `## Thread highlights`: any explicit maintainer direction.
- `## Candidate PR` → `### Title`, `### Description`, `### Commits`: where the PR honors those asks (issue referenced, required sections filled, disclosure present).

**Where it lives (live):**
- `.github/pull_request_template.md` (or `.github/PULL_REQUEST_TEMPLATE/`), and `CONTRIBUTING.md` at the repo root or in `.github/` or `docs/`.
- The issue thread on GitHub, for maintainer comments.
- Your draft title, description, and commit messages.

**What good looks like:** every ask the repo states is met: the template is used with real content in each required section (if templatye present), the required disclosure is present, the issue is referenced if asked, and maintainer direction in the thread is followed or answered. If the repo states no template or no policy, that ask doesn't apply and is not a fail.