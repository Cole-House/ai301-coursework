# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment_clear    | The repro report's environment record (version, OS, commit/branch if given)                                | Someone could stand up the same runtime from what's recorded, and nothing in it contradicts the environment the issue itself describes.                     | required |
| minimal_steps        | The repro report's steps, read against the repo-facts block and the issue's description                    | Following the steps exactly as written reproduces the outcome the report claims — the issue's failure if the report claims reproduction, or a clean/expected run if the report honestly claims it does not reproduce. No skipped setup, no step that assumes outsider knowledge.                                         | required |
| expected_and_result  | The repro report's expected/actual comparison, read against the issue's stated symptom                     | The actual result recorded matches what the artifact shows, and the gap between expected and actual is the same failure the issue reports (not a different one). | required |
| artifact_check       | The artifact attached at the end of the report, read against the issue's description and the actual-result claim | The artifact itself shows the outcome the report claims — the failure, if reproduction is claimed, or the absence of it, if a cannot-reproduce is claimed — and matches the actual-result line. A missing artifact only fails this if the report needed one to back its claim.          | required |
| comms | The claim comment (or draft comment), read against the issue thread, the report's own findings, and the repo's stated contribution/AI policy in the repo-facts block | Default PASS. Fails only if one of these holds: (1) the comment asserts an outcome the evidence doesn't support — a fix timeline, a guaranteed resolution, or certainty beyond what was tested; (2) the comment's stated finding contradicts or is unrelated to what the report's steps/artifact actually show; (3) the repo-facts block states an AI-use or comment-voice policy, and the comment fails to meet that specific policy as written — e.g. omitting a required disclosure statement, or reading as obviously AI-generated where the policy requires human voice. If the repo-facts block says no AI policy is stated, this disqualifier does not apply. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

accept if every required check passes; if the comment is identified as an issue claim make verdict "Not applicable" and any other case with required checks failing is a reject.
