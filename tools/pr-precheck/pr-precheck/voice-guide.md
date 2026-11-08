# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

Cole House a junior developer looking to grow his skills and help contribiute to open source projects.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: no promised timelines

Never put a timeline on when I will get something done, keep it more open ended.

- Wrong: ‘by tomorrow!’
- Right: ‘repro report on the way’

### Rule: no ai bot voice

Keep your responses/comments short and with only essential information, sound like a human.

- Wrong: ‘amazing project!’
- Right: ‘’

### Rule: name the version and the behavior

When reproducing an issue name the specfic version and behvior associated.

- Wrong: ‘this bug’
- Right: ‘v1.20.0 ignores --style’

### Rule: Clear comms

**Applies to:** the PR title, the PR description, and every commit message.

**Rule:**

- **Title:** says what changed in plain words, and follows the same format as the repo's recently merged PRs (prefix style like `fix:` or `themes:`, capitalization, issue number placement, length).
- **Description:** a maintainer can tell what changed, where, and why without opening the diff. Every statement describes something the diff actually contains.
- **Commits:** each commit holds one logical change, and its message says what that change is. No "wip," "fix stuff," or "updates."

**How to check:**

1. Pull the titles of the last 10 merged PRs (`gh pr list --state merged --limit 10`, or the repo's Pull requests tab filtered to merged). Note their shared format, and compare your title against it.
2. Read the description without the diff open. Write down what you think changed, where, and why, then compare with the diff.
3. For each commit, check that its changes could be described in one sentence, and that the message is that sentence.

**Broken looks like:** a title with no prefix in a repo where every merged PR has one; a description a reader can't follow without the diff; a commit that mixes the fix with unrelated cleanup; a vague message like "update file."

**Report a break as:** the rule name, the text that breaks it (quoted), and a suggested rewrite.

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

limit —em dashes
no fancy words
keep it terse and to the point, no extra UNNECESSARY pleasantries
