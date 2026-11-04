# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

[Cole-House]

**Plan comment**

[https://github.com/codepath/pathreview-ai301-fa26-s3/issues/11#issuecomment-6617496660]
Here is my plan to address the document gap regarding the ambiguity of the hybrid retrieval scoring formula in the RAG section of ARCHITECTURE.md

Diagnosis: doc gap, not a code bug. At 2f4e82f, docs/ARCHITECTURE.md describes RAG scoring in general terms only. The weights (vector_weight=0.7, keyword_weight=0.3) and the blend line (blended_score = self.vector_weight * vector_score + self.keyword_weight * keyword_score) only exist in rag/retriever/hybrid.py. HybridRetriever.retrieve also divides each score by the max score in that query's results before blending, and a chunk found by only one search gets 0 for the other score.

Change: add a short subsection under the existing "Hybrid retrieval" sentence in docs/ARCHITECTURE.md with:

default weights: vector 0.7, keyword 0.3, set as constructor defaults in hybrid.py
the formula: score = w_v · (s_vec / max s_vec) + w_k · (s_bm25 / max s_bm25)
the min_score (0.3) filter and max_chunks (10) cap
one illustrative example: a chunk at 1.0 vector / 0.5 BM25 scores 0.85 and is kept; a vector-only chunk at 0.4 scores 0.28 and is dropped
Not touching: hybrid.py itself, the generator/evaluator parts of that paragraph, weight tuning, the unused all_chunks fetch (tracked in #6), and README.md.

Check: reread the doc against hybrid.py so every number matches, recompute the example by hand, and check the GitHub preview renders.

Open questions:

I haven't checked yet if any caller of HybridRetriever( overrides 0.7 / 0.3. If one does, the doc will list the override next to the defaults.
I'll cite function and parameter names instead of line numbers so the doc doesn't drift.

---

## Your branch

**Branch**

[docs/11-hybrid-scoring-docs]

**Evidence**

[**Before** (the doc as it was before my change, at the commit before the fix):

```
$ git show HEAD~1:docs/ARCHITECTURE.md | grep -n -iE "weight|formula|0\.7|0\.3|blended"; echo "exit code: $?"
exit code: 1
```

No matches: the doc had no weights, formula, or blend terms.

**After** (the doc with my change):

```
$ grep -n -iE "weight|formula|0\.7|0\.3|blended" docs/ARCHITECTURE.md; echo "exit code: $?"
67:blended_score = vector_weight × vector_score + keyword_weight × keyword_score
70:- **Default weights:** `vector_weight = 0.7` and `keyword_weight = 0.3`. These are constructor defaults, so the blend favors semantic similarity over exact word matches.
73:- **Filtering:** chunks with a blended score below `min_score` (default 0.3) are dropped, and the top `max_chunks` (default 10) are returned, highest first.
75:**Example (illustrative numbers, default weights):**
77:| Chunk | Vector (normalized) | Keyword (normalized) | Blended score | Result |
79:| A | 1.00 | 0.50 | 0.7 × 1.00 + 0.3 × 0.50 = 0.85 | Kept |
80:| C | 0.60 | 1.00 | 0.7 × 0.60 + 0.3 × 1.00 = 0.72 | Kept |
81:| B | 0.40 | 0 (not found by keyword search) | 0.7 × 0.40 + 0.3 × 0 = 0.28 | Dropped (below 0.3) |
exit code: 0
```

The doc now states the default weights (0.7 / 0.3), the blend formula, and a worked example, and each claim was checked against `rag/retriever/hybrid.py` (lines 18, 19, 73, 74, 101, 113, 117). Recomputing the example math gave 0.85, 0.72, and 0.28.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[Run 1: 18/20
Run 2: 19/20 (after adding a new check)]

**Package analysis**

[**pkg-03** (BurntSushi/ripgrep#3222, calling compression tools with `--`)

In my final run (19/20), my rubric decided **accept** and the gold label was
**clear-accept**, so they agree. In my first run (18/20) this package was a miss:
my `bounded-scope` check rejected it.

Why the rubric reads it as an accept: the plan's Change section names one
bounded location and states its limits: "in the command construction in
`crates/cli/src/decompress.rs`, append `--` before the file path for every
spawned decompression tool. In scope: the argument separator only. Not in scope:
shell quoting, the choice of tools, or the matching logic." The only other
thing it touches is the test plan's "Add the dash-named fixture to the
compression integration tests", which is a test that accompanies the fix, not
an unlisted source change. My first version of the check required every changed
file to be listed, so it read that fixture as an unlisted file and failed a plan
that was clearly bounded. The revised check asks whether the plan names where the
change goes and what is in and out of scope, and does not count accompanying
tests, so it now passes this plan.]

**Check rationale**

[| bounded-scope | The plan's scope statement, its list of files or code areas to be changed, and its fix and test descriptions | The plan names where the change will be made (a file, module, or code path specific enough to locate in the repo) and states what is in scope and out of scope, and nothing in the fix description implies changes outside that named area. Tests and fixtures that accompany the fix are expected and need not be listed separately. A plan may leave exact functions to be pinned in the PR if the named area is already bounded. | required |
I noticed my first run missed clear accepts due to bounded scope because my original wording was too black or white, but this version is more inclusive and allows more reasonable flexibiltiy to the bounding of the scope]

**Trade-offs**

[Loosening `bounded-scope` fixed pkg-03 (a clear-accept my first version rejected
because the test fixture counted as an unlisted file), but it changed another
result: pkg-19 went from a matching verdict in run 1 to a miss in run 2. My
rubric accepted it, and the gold label was [reject/fail], because
[thread-convention problem, quoted from the package: "..."].

The cost: [a looser check, or the new comms check, no longer catches this case].
I accept that it will miss plans like this, where [one-line description].]

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
