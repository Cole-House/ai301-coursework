# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

Cole-House

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/11#issuecomment-6335601996[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

I'd like to pick up this documentation issue. My plan is to look at the current `ARCHITECTURE.md` to see exactly what's missing, then find where the hybrid retrieval scoring formula and default weights are actually defined in the codebase, and add a section to the doc that explains the formula with a concrete example (and a diagram, if it helps make the weighting clear).

**Reproduction comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/11#issuecomment-6335298687
[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]
I am working in a fork of the codepath/pathreview-ai301-fa26-s3 and up to date with the most recent commit 2f4e82f.

I forked the repo and was able to complete setup with the steps detailed in README.md
I read the description of how the RAG scoring works on ARCHITECTURE.md and found no exact formula or weights
Looked for relevant code in the rag/retriever/hybrid.py file
Lines 18,19 detail the weights associated with both vectors and keywords:

 vector_weight: float = 0.7,
 keyword_weight: float = 0.3,
and also the blend formula on line 101

blended_score = self.vector_weight * vector_score + self.keyword_weight * keyword_score

In math form:

score = w_v · (s_vec / max s_vec) + w_k · (s_bm25 / max s_bm25)

The doc currently states this for the RAG scoring generation: “Hybrid retrieval (vector similarity + BM25 keyword) fetches relevant context from the user's ingested documents. The generator uses prompt templates to produce structured, evidence-based feedback. The evaluator scores retrieval relevance and generation faithfulness.” It does not explain the formula or weights used in the hybrid retrieval or give an example to reference.
## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]
First full run: 3 disagreements — pkg-09 (gold accept, graded reject, failed minimal_steps/artifact_check), pkg-19 and pkg-20 (gold reject, graded accept).
Rewrote minimal_steps/artifact_check to judge evidence against whatever the report claims, not just “did it reproduce.” Added a new comms check for pkg-19/pkg-20.
Re-ran --only pkg-09,pkg-19,pkg-20 — got worse. Found the bug: I’d been editing the clone, not the installed skill at ~/.claude/skills/repro-check/.
Copied corrected files into the installed copy, confirmed with diff, re-ran full eval — hit 18/20.
comms then broke two previously-passing packages: pkg-01, pkg-03.
Cause: comms assumed disclosure is always required. pkg-01’s repo has no AI policy; pkg-03’s only requires human voice, not disclosure.
Rewrote comms to default-pass and defer to the repo-facts block’s actual policy. Re-ran pkg-01/pkg-03, then one final confirming run with --save-run eval-run.txt which hit the passing grade of 18/20.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]
Package: pkg-01 (httpie/cli#1640, clear-accept)
Gold: accept. Mine (first comms version): reject, failed comms.

My check assumed AI disclosure was always required. pkg-01’s repo-facts block says “no stated AI policy” — nothing to disclose against. The comment itself was fine (gold note: “specific and modest”). Fix: comms now only applies its disclosure/voice rule when the repo-facts block actually states one.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]
“comms | The claim comment (or draft comment), read against the issue thread, the report’s own findings, and the repo’s stated contribution/AI policy in the repo-facts block | Default PASS. Fails only if one of these holds: (1) the comment asserts an outcome the evidence doesn’t support... (3) the repo-facts block states an AI-use or comment-voice policy, and the comment fails to meet that specific policy as written... If the repo-facts block says no AI policy is stated, this disqualifier does not apply. | required”

Why? Default-pass with named failure conditions, not a positive checklist to avoid over-rejecting. Condition 3 routes to the repo’s actual stated policy instead of assuming one shape fits all repos, after pkg-01/pkg-03 showed disclosure and policy-compliance aren’t the same thing.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Default-pass trades recall for precision causing it to miss comms problems outside the three named failure modes, but avoids over-rejecting honest comments. Deferring to the repo-facts block also means comms is only as accurate as that block: if it misses or misstates a repo’s real policy, the check inherits that blind spot.
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
