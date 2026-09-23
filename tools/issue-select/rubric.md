# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|maintainer_active|"last 5 default-branch commits" and "maintainer first-response sample" under Repo facts|at least 1 of the last 5 default-branch commits is from a human (non-[bot]) account, OR the maintainer first-response sample shows a reply from an Owner/Member/Collaborator within 15 days|required|
|repo_used|"last push to any branch," "latest release," and "archived:" under Repo facts|repo is not archived, AND (last push was within 60 days of the capture date OR latest release was within 90 days of the capture date)|required|
|scoped_for_newcomer|issue body and comment thread|Pass unless the issue is an umbrella/tracking issue splitting into sub-items, the design is still under debate with no maintainer decision, a maintainer says the fix touches core internals, it's a pure usage/support question, or its history shows repeated abandoned attempts. A terse body or missing reproduction steps does not by itself fail this check.|required|
|up_for_grabs|"this issue: assignees:", "linked PRs:", and the Comments section|no assignee is set, no linked PR is open, and no comment thread claim ("I'll take this" / "working on this") is unanswered-but-recent; if the sidebar and thread disagree, the thread wins|required|
|ai_allowed|"contribution policy" line under Repo facts|contribution policy does not contain an outright ban on AI-generated contributions (conditions like disclosure/testing/review requirements are fine; silence passes)|required|
|good_first_issue|issue labels|issue carries a good-first-issue or equivalent label|preferred|


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if all the required checks pass. Any required check graded unclear counts as a fail - meaning if there isn't enough evidence to confirm a required check,reject rather than assume. preferred checks never effect accept/reject; they only rank accepted issues (e.g. specifically labeled good-first-issues rank above unlabeled ones). Also with ranking the issues take my preferences into account locatted in my fit profile section of scope.md.
