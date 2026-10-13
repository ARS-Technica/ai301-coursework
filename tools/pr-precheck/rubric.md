# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| silent-drift | The diff's changed files read against the plan's stated boundary and `plan.md` deviation notes. | Every file changed in the branch diff (such as code or config files) is explicitly named in the plan or its deviation notes, with zero unannounced file modifications or unrelated cleanups. | required |
| not-tested | The test evidence in `test_evidence.md` read against the plan's test plan and repository test execution logs. | Every test specified in the plan's test plan is backed by authentic command output or captured execution traces, allowing for standard terminal prompts and output descriptions. | required |
| unreviewable | The commit history and diff structure read against the PR package branch. | The PR diff contains no extraneous debugging code, stray print statements, commented-out dead code, or unrelated file cleanups that bury the actual change. | preferred |
| standards-wall | The PR title and `pr_draft.md` description read against the repository PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and contributing guidelines. | Every required section of the repository's PR template (Summary, Issue, Changes, Testing, and Notes for Reviewers including AI-use disclosure) is fully filled out. | required |

## Verdict rule

accept if every required check passes; preferred checks never change the verdict; unclear counts as fail.

Accept if and only if every required check (silent-drift, not-tested, unreviewable, standards-wall) receives a grade of Pass (P).

Reject is any required check receives a grade of Fail (F) or Unclear/Uncertain (?).

Fail if any required check (silent-drift, not-tested, unreviewable, standards-wall) receives a grade of Fail (F).  

Fail if any required check (silent-drift, not-tested, unreviewable, standards-wall) receives a grade of Unclear.