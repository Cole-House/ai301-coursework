# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

link: [https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

ACCEPT

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
All three grade out. Evidence gathered live from the GitHub API (gh isn't installed here, so I used the REST API directly).

Repo-level facts (shared by all three, measured against today, 2026-09-23):
- maintainer_active — pass: all 5 most recent main commits are by Aburke225 (human, non-bot), newest 2026-09-16. Worth knowing: the first-response sample shows zero maintainer replies — every commenter across #69, #53, #57, #60 carries author_association: NONE (students). The commit leg carries this check; nobody is answering threads.
- repo_used — pass: archived: false, last push 2026-09-16 (7 days ago). No releases exist, but the rule is an OR.
- ai_allowed — pass: docs/CONTRIBUTING.md has no mention of AI/assistants/generated code; the PR template has no disclosure checkbox. Silence passes.

Ranked read-out

1. #60 — Faithfulness checker crashes on text: None · accept. Labeled good first issue (the only preferred check in the rubric, and it ranks labeled above unlabeled), and it's a genuine one-line bug with a copy-paste repro and a named failing test (test_none_context_chunk_text). Fits your AI-engineering goal: it's in the RAG evaluator, and rag/evaluator/faithfulness_checker.py exists. pkmaster21 commented "I'll take this" on 2026-09-21 — under the Path Review house rule that's a classmate claim and doesn't block; the repo has 0 pull requests total, so no linked PR either. The 2026-09-21 referenced event by dannguyen111 is a commit reference, not an open PR.
2. #73 — README vs .env.example disagree on the LLM key · accept. Also good first issue, completely untouched (no comments, no assignee), two named files, 1–2 hours. Ranks below #60 only on fit: it's a docs/config reconciliation, so there's less to learn from it.
3. #42 — jest-axe accessibility tests for the review page · accept. This is the strongest match to your fit profile by a wide margin — React/TS front-end, accessibility, your QA background, your stated UI/UX goal — and the tooling is already wired: jest-axe and @types/jest-axe are in frontend/package.json, and ReviewPage.tsx exists. It ranks third only because your rubric's preferred check demotes it: labels are frontend, tests, tier-2 with no good-first-issue label. Two things to know before you take it: the file the issue names, frontend/src/pages/__tests__/ReviewPage.test.tsx, returns 404 — you'd be creating it, not editing it — and the estimate is 4–6 hours.

A tension worth naming, since the fix belongs in the rubric rather than in this run: your rubric's only preferred check is the good-first-issue label, so it outranks fit and pushes your best-fit issue to last. If front-end/UX exposure matters more to you than the label, add a preferred check for it (or drop the label check's priority) and #42 moves to the top.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
    "checks": [
      {"name": "maintainer_active", "grade": "pass", "evidence": "All 5 latest main commits authored by human account Aburke225, newest 2026-09-16T21:42:18Z"},
      {"name": "repo_used", "grade": "pass", "evidence": "archived: false; last push 2026-09-16T21:50:20Z, 7 days before today"},
      {"name": "scoped_for_newcomer", "grade": "pass", "evidence": "Single .get() None-default bug with runnable repro and named failing test test_none_context_chunk_text; not umbrella, no design debate, no core-internals claim"},
      {"name": "up_for_grabs", "grade": "pass", "evidence": "assignees: []; repo has 0 PRs total so no linked PR; only claim is pkmaster21 (author_association NONE), a classmate claim the Path Review house rule says does not block"},
      {"name": "ai_allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/assistant/generated-code policy line; no ban"},
      {"name": "good_first_issue", "grade": "pass", "evidence": "labels: ['bug', 'good first issue', 'rag', 'tier-1']"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "maintainer_active", "grade": "pass", "evidence": "All 5 latest main commits authored by human account Aburke225, newest 2026-09-16T21:42:18Z"},
      {"name": "repo_used", "grade": "pass", "evidence": "archived: false; last push 2026-09-16T21:50:20Z, 7 days before today"},
      {"name": "scoped_for_newcomer", "grade": "pass", "evidence": "Bounded mismatch between two named files (README.md, .env.example), est. 1-2 hours; no umbrella, debate, or support question"},
      {"name": "up_for_grabs", "grade": "pass", "evidence": "assignees: []; 0 comments; repo has 0 PRs total"},
      {"name": "ai_allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/assistant/generated-code policy line; no ban"},
      {"name": "good_first_issue", "grade": "pass", "evidence": "labels: ['bug', 'good first issue', 'docs', 'tier-1']"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/42",
    "checks": [
      {"name": "maintainer_active", "grade": "pass", "evidence": "All 5 latest main commits authored by human account Aburke225, newest 2026-09-16T21:42:18Z"},
      {"name": "repo_used", "grade": "pass", "evidence": "archived: false; last push 2026-09-16T21:50:20Z, 7 days before today"},
      {"name": "scoped_for_newcomer", "grade": "pass", "evidence": "One bounded task (add jest-axe tests for ReviewPage); jest-axe already in frontend/package.json; no umbrella, design debate, core-internals claim, or abandoned attempts"},
      {"name": "up_for_grabs", "grade": "pass", "evidence": "assignees: []; 0 comments; repo has 0 PRs total"},
      {"name": "ai_allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/assistant/generated-code policy line; no ban"},
      {"name": "good_first_issue", "grade": "fail", "evidence": "labels: ['frontend', 'tests', 'tier-2'] - no good-first-issue or equivalent label"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1st full run: 16/20, missed issue-01, issue-04, issue-15, issue-19 (scope over-rejecting and missing clear-acceptance issues). 
2nd: revised scoped_for_newcomer to default-to-pass wording and also weigh good-first-issue labels heavier, re-ran --only on those 4, was able to fix 3/4 issue verdicts. 
3rd: full confirming run, 17/20 (or however yours ends up), saved as eval-run.txt.

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

issue-15:Gold says reject (note: "years of design debate and two abandoned PRs behind a friendly label"). My rubric's scoped_for_newcomer check said reject because in the default to pass requirements it checks the issues comments and determined that there was indeed design debate for the open issue.


**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

|ai_allowed|"contribution policy" line under Repo facts|contribution policy does not contain an outright ban on AI-generated contributions (conditions like disclosure/testing/review requirements are fine; silence passes)|required|

This check is absolutely crucial for picking an issue for this class as we must first know whether the repo allows AI assisted contributions in the first place. 

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Changing my scoped_for_newcomer check and pass evaluation rationale impacted my results the most where changing from a list of requirements to a default to pass reasoning, still allowed shorter descriptions of issues with clear scope pass the check.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
   - I chose this issue because it was a good-first-issue with clear scope and fit in my time commitment as a first issue to get my feet wet. I also gravitated towards this issue to learn more about AI Engineering and how API keys such as Openrouter are properly set up in a production repo.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
   - So for the most part my skill successfully evaluated the issues for most of the checks, but I purposely selected some issues that had some flags that the skill did not recognize correctly. For example I added an issue that had a comment claiming it already but the up_for_grabs check still passed because " only claim is pkmaster21 (author_association NONE), a classmate claim the Path Review house rule says does not block". It also said passed the scoped_for_newcomer check for an issue that was labeled tier-2, but still justified it with ""One bounded task (add jest-axe tests for ReviewPage); jest-axe already in frontend/package.json; no umbrella, design debate, core-internals claim, or abandoned attempts".
3. The anticipated difficulty in claiming it.
   - I anticipate this first issue to not be super difficult and allow me to get oriented with the codebase as it mainly deals with documentation and making sure information matches in .env files.
]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
