# Contribution: Standardize loading skeleton heights across dashboard widgets

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** [Cole House]
**GitHub Username:** [Cole-House]
**Issue:** [[GitHub issue link]](https://github.com/Priyanshu-byte-coder/devtrack/issues/44)
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Enhancing our issue-select skill to issue-scout ot explore live repos**

In this unit we upgraded our issue-select skill to issue-scout where we used the same rubric checks from week 1 that determine if an issue is a good-first issue for us based on various factors including if the maintainer is active on the repo, scoped for newcomer, available to work on and if repo allows ai use. We added a scouting layer to the skill where we use "gh search issues" commands to search on github for live issues that match our given queries that help find issues that fit our profile, and from the issues found we also filter it to rank the top 5 found. I felt like the ranking step was important because we tell them what results to drop and how to find the top 5 issues to then be ran through an actual evaluation and get graded. Through my grading process we were able to fix the ranking a bit to not allow issues that are related to issues I didn't want to work on through to the grading process.

**Unit 6: Setting up voice-guide for claiming issue and getting lay of the land**

I felt that this unit we learned how to use hooks to help avoid uneccesary and costly commands being run by checking that our comment adheres to the rules we set for how we want our voice to be heard in repo's. It was interesting learning about how different open source repos operate and the process they use for contributor's, I gravitated towards a smaller project that doesn't require onboarding paperwork and utilizes automation in the process so as a contributor I can claim issues that are up for grabs and get working right away. I cloned my repo and enjoyed learning how to set-up my CLAUDE.local.md file (with under 60 lines) using claude itself to explore the important subsystem around the issue I am working on and distill the conventions of contributing into a file that will get loaded into every claude session so it has the key context when working on the PR.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I chose issue#44 Standardize loading skeleton heights across dashboard widgets in the open source devtrack repo which is a repo building a dashboard for developers to see streaks and their place on a global ranking system. This was not found through the codepath issue site or the issue-scout but rather through asking claude to suggest me a repo that satisfied my checks and profile especially one that was active, and I could get working right away to get a PR merged before the end of the course lol. My issue-scout runs were sort of helpful but needed tweaking because it would still rank issues that weren't that interesting to me in my top 5 and while looking through issues on the codepath site I would add the filters for good first issue and up for grabs but the issues I would find would have PRs already open and was unclear if it was truly up for grabs. I went with devtrack repo because the contributing process was straightforward, maintainer was active, the issue touched on the front-end UI experience I was looking to gain and I was able to claim the issue successfully.

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**
I'm reproducing this on a fork of Priyanshu-byte-coder/devtrack at main @ 2a5c5161, macOS 26.5.2, Node v22.23.5 / pnpm 11.13.1. I used Chrome with a 1440 x 900 viewport, signed in with GitHub. My account has sparse data (2 goals, few PRs), so the loaded heights below are close to a floor.

Fork and clone the repo, then follow the Quick Start in the README and the Development Guide (`DEVELOPMENT.md`) to install dependencies, create a GitHub OAuth App, set up Supabase (including loading the SQL schema), and fill in `.env.local` with necessary values.

**Steps to Reproduce**
1. `pnpm install`, `pnpm dev`, open http://localhost:3000, sign in with GitHub.
2. DevTools → Network → add Slow 4G throttling with devtools to allow time to measure skeleton dimensions and then loaded state.
3. In the Console, log layout shifts:
   `new PerformanceObserver(l => l.getEntries().forEach(e => !e.hadRecentInput && console.log('layout-shift', e.value.toFixed(4), Math.round(e.startTime) + 'ms'))).observe({type:'layout-shift', buffered:true});`
4. Hard-reload each page: `/dashboard/goals` (GoalTracker), `/dashboard/activity` (StreakTracker), `/dashboard/pull-requests` (PRMetrics).
5. While the skeleton shows, measure each card's own root, then measure again after the data loads (selectors below).
6. Per-section heights are the children of each card root.

<details><summary>Measuring snippet</summary>

```js
console.table(Object.entries({
  'Goal Tracker': ['[aria-labelledby="goal-tracker-title"] > .px-frame'],
  'Streak Tracker': ['[data-testid="streak-widget"]', '[aria-labelledby="streak-tracker-title"] > div'],
  'PR Metrics': ['[aria-labelledby="pr-metrics-title"] > .px-frame']
}).map(([widget, sels]) => { const el = sels.map(s => document.querySelector(s)).find(Boolean); return { widget, px: el ? Math.round(el.getBoundingClientRect().height) : 'not on this page' }; }));
```
</details>

**Setup gotcha:** I left the `your_upstash_redis_rest_url` placeholders from `.env.example` in place, and every `/api/metrics/*` call returned 502 ("GitHub API error") and `/api/user/settings` returned 500 until I commented them out. 

**Reproduction Evidence**

- **Commit showing reproduction:** N/A
- **Screenshots/logs:**
<img width="809" height="446" alt="Screenshot 2026-11-17 at 11 15 43 AM" src="https://github.com/user-attachments/assets/8d05743e-01a2-4df7-866f-18e886761478" />
<img width="814" height="567" alt="Screenshot 2026-11-17 at 1 03 33 PM" src="https://github.com/user-attachments/assets/cf668663-29bc-4306-87b2-9ab844c9b10f" />
<img width="803" height="537" alt="Screenshot 2026-11-17 at 12 52 53 PM" src="https://github.com/user-attachments/assets/a7eee42d-38b3-4f26-80c8-dcdd9e53a685" />
<img width="792" height="563" alt="Screenshot 2026-11-17 at 11 30 50 AM" src="https://github.com/user-attachments/assets/7813ad4b-609d-43a1-9356-162a7be2fc67" />
<img width="791" height="561" alt="Screenshot 2026-11-17 at 11 29 41 AM" src="https://github.com/user-attachments/assets/38838db0-d73b-4c4b-a907-7b9970040d3c" />
<img width="801" height="517" alt="Screenshot 2026-11-17 at 11 16 22 AM" src="https://github.com/user-attachments/assets/8ee0c59b-b9f5-482d-b538-b9b4eb71a3fd" />


- **My findings:** 
 Widget | Skeleton | Loaded |
|---|---|---|
| GoalTracker | 232 px | 686 px (0 goals), 966 px (2 goals) |
| StreakTracker | 700 px | 980 px |
| PRMetrics | 648 px | 750 px |

**GoalTracker.** The skeleton is a 24 px header and three 32 px rows. The loaded card is 35 px header, 26 px category chips, goals list (about 132 px per goal), 16 px "Updated" line, a 440 px create-goal form, and a 37 px bottom row. The skeleton reserves nothing for the form, which is most of the gap.

**StreakTracker.** The skeleton's content is only about 328 px (title plus a 2x2 grid of `h-28`), so its 700 px comes from `min-h-[700px]`. Loaded sections: header 32, stats grid 189, month strip 38, "Updated" 16, freeze row 50, calendar 531. The skeleton has no placeholder for the strips or the calendar. Note: measuring the `role="region"` wrapper on /dashboard/activity gives 1164 → 1404 px, because the grid row appears to stretch to the sibling column (Weekly Summary / Consistency Score). The numbers above are the card roots.

**PRMetrics.** There are two skeleton stages. The first is a 320 px generic fallback with no header, from the dynamic import in `widgets.tsx`. The second is PRMetrics' own skeleton at 648 px. Body sections, skeleton vs loaded: stat tiles 92 vs 104, weekly chart 192 vs 236, panel row 224 vs 127, and a second panel row (127) that the skeleton doesn't have.

**Layout shifts** (page-wide, so they include other widgets on the page):
- /dashboard/goals: 0.0629, 0.0434, 0.0617 (sum ≈ 0.168)
- /dashboard/activity: 0.0323, 0.0162, 0.0050, 0.0430, 0.0262 (sum ≈ 0.123)
- /dashboard/pull-requests: 0.0701, 0.0620, 0.0235 (sum ≈ 0.156)
Each logged value is the browser's layout-shift score (the fraction of the viewport that moved times the distance it moved), so higher means a bigger visible jump. With Slow 4G throttle, each page logged 3 to 5 shifts as data replaced the skeletons (summed per page: about 0.17 on /dashboard/goals, 0.12 on /dashboard/activity, 0.16 on /dashboard/pull-requests).

**Toolkit**

- Tool: repro-check
- What it produced: accepted my repro comment
- Difficulties: Setting up the environment and debugging
- What changed: NA

---

## Solution Approach

Analysis

The layout shifts come from loading skeletons that don't match the structure of the loaded widgets. Each skeleton reserves less height than the content that replaces it, so when data arrives, everything below the card is pushed down. Measured at 1440 x 900 on Slow 4G, the page-wide layout-shift totals were about 0.17 on /dashboard/goals, 0.12 on /dashboard/activity, and 0.16 on /dashboard/pull-requests.

src/components/GoalTracker.tsx: the loading skeleton is a header row and three thin bar pairs. The loaded card is 686 px with 0 goals and 966 px with 2. The skeleton has no placeholder for the category chips, the "Updated" line, the bottom row, or the 440 px create-goal form. The form is always rendered, so most of the gap comes from fixed content, not from data.
src/components/StreakTracker.tsx: the skeleton's content is only about 328 px (title plus a 2x2 grid of h-28 tiles). Its 700 px comes from min-h-[700px], not from placeholders. The loaded card is 980 px: header 32, stats grid 189, month strip 38, "Updated" 16, freeze row 50, and a 531 px calendar. The skeleton has nothing for the month strip, "Updated" line, freeze row, or calendar.
src/components/PRMetrics.tsx: the in-component skeleton is 648 px against a 750 px loaded card. Section heights (skeleton vs loaded): stat tiles 92 vs 104, weekly chart 192 vs 236, first panel row 224 vs 127. The second panel row (127 px) has no placeholder at all. PRMetrics also has an earlier loading stage: the dynamic import in src/components/dashboard/widgets.tsx first shows a generic 320 px fallback. That stage is outside this issue's scope (see Deviations).

Proposed Solution

Update the existing skeleton markup in the three files listed in the issue so each skeleton's height matches its loaded widget, section by section, using the measurements above. Keep the existing SkeletonBlock markup where possible and change its h-* classes. Add a SkeletonBlock only for a loaded section that has no placeholder at all. Use Tailwind scale classes where a height matches exactly (h-4 = 16 px, h-8 = 32 px), and arbitrary values (h-[132px]) otherwise.

Deliberately NOT changing:

Any file outside the three listed in the issue, including src/components/dashboard/widgets.tsx and its shared lazy helper
The loaded layout, styles, or content of any widget
Data fetching, API routes, or caching
Shared skeleton pieces (SkeletonBlock, .skeleton-shimmer), which 12 widgets use
Other widgets on these pages (Weekly Summary, Consistency Score)

Implementation Plan

src/components/GoalTracker.tsx: size the skeleton to the loaded sections: header 35 px, category chips 26 px, one goal row 132 px, "Updated" line 16 px, create-goal form 440 px, bottom row 37 px. Keep the loaded markup's margins (mb-4, mb-3, mt-2, mt-6) as spacing. Expected skeleton height: 818 px (the loaded height with one goal).
src/components/StreakTracker.tsx: size the skeleton to header 32 px, stats grid 189 px, month strip 38 px, "Updated" 16 px, freeze row 50 px, calendar 531 px, with the loaded markup's margins. Remove min-h-[700px] once the placeholders provide the height. Expected skeleton height: 980 px.
src/components/PRMetrics.tsx: in the existing in-component skeleton, change the stat tiles to h-[104px], the chart to h-[236px], and the panels to h-[127px], and add the missing second panel row (two h-[127px] blocks in the same grid). Expected skeleton height: 750 px.
Verify: repeat the reproduction (1440 x 900, Slow 4G, hard reload) with the same measuring snippet and layout-shift observer. Record skeleton vs loaded heights and per-page shift totals, before and after, in the PR.
Tests and checks: check whether these components already have tests and update any that assert on skeleton markup. Run the ship manifest in order: pnpm install --frozen-lockfile, pnpm run lint, pnpm run type-check, pnpm run test, pnpm run build.

Known limits (to note in the PR)

Heights were measured at 1440 x 900. On narrower screens, PRMetrics' tiles wrap and its panels stack, so heights will differ.
Data-dependent sections (goal count, category chips, StreakTracker's month strip, freeze row, and calendar) vary by account. The skeleton reserves a typical layout, so accounts with very different data will still see a small jump.

Deviations

Narrowed scope to the three files listed in the issue. An earlier draft also changed src/components/dashboard/widgets.tsx and added a new PRMetricsSkeleton.tsx to replace PRMetrics' generic 320 px fallback. That's dropped to keep this PR skeleton-dimensions-only, so that first-stage shift on /dashboard/pull-requests remains and is left for a follow-up.

**Toolkit**

- Tool: plan-check
- What it produced: validated approach based off of reproduction evidence and issue scope. 
- Difficulties: Not all repos require repro comments so when my skill was looking for a repro comment and couldn't find on in the comment thread then it failed the relevant check. 
- What changed: Need to go in and add some more flexible logic for my check.

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

For each component in my branch with changes using Slow 4G throttling and the 1440 x 900 viewport identical to my reproduction of the issue, II ran this command in the console:

console.table(Object.entries({
'Goal Tracker': ['[aria-labelledby="goal-tracker-title"] > .px-frame'],
'Streak Tracker': ['[data-testid="streak-widget"]', '[aria-labelledby="streak-tracker-title"] > div'],
'PR Metrics': ['[aria-labelledby="pr-metrics-title"] > .px-frame']
}).map(([widget, sels]) => { const el = sels.map(s => document.querySelector(s)).find(Boolean); return { widget, px: el ? Math.round(el.getBoundingClientRect().height) : 'not on this page' }; }));

to get the measurements of the targeted components skeleton while loading and then ran it again to get the dimensions with loaded data to compare.

- For `src/components/StreakTracker.tsx`
    - Skeleton: 980px
    - Loaded: 982px
- For `src/components/GoalTracker.tsx`
    - Skeleton: 818px
    - Loaded: 1058px; off by ~200px
        - This actually makes sense considering we want the skeleton to be at the floor length of 0 goals set (I have 2 goals loaded in)
- For `src/components/PRMetrics.tsx`
    - Skeleton: 750px
    - Loaded: 750px
┌─────────────────────┬─────────────────────────────────┐
│        Check        │             Result              │
├─────────────────────┼─────────────────────────────────┤
│ pnpm run lint       │ ✓ passed                        │
├─────────────────────┼─────────────────────────────────┤
│ pnpm run type-check │ ✓ passed                        │
├─────────────────────┼─────────────────────────────────┤
│ pnpm run test       │ ✓ passed: 201 files, 2635 tests │
├─────────────────────┼─────────────────────────────────┤
│ pnpm run build      │ ✓ passed on the second run      │
└─────────────────────┴─────────────────────────────────┘

**Toolkit**

- Tool: ship-gate
- What it produced: ran the mandatory checks needed for my branch
- Difficulties: having some issues with wrong version of node, but updated on the second run and build went smoothly
- What changed: N/A

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**11/18/26**

All three loading skeletons are now sized to match their loaded cards, so a card shouldn't jump when its data arrives:

- StreakTracker.tsx: removed the fixed min-h-[700px], so the skeleton's height now comes from its contents. The title bar and four stat tiles are resized, and I added blocks for the rest of the card, including a 531px calendar area.
- GoalTracker.tsx: the three repeated goal rows (about 150px total) are replaced by a layout that mirrors the loaded card: header pills, one goal block, a 440px list area and a footer.
- PRMetrics.tsx: resized the six stat tiles (104px) and the chart (236px), and the two large panels became two rows of two 127px panels.

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
