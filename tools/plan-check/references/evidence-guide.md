# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repo evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives:**
  - Look under `## Diagnosis` in the local `plan.md` draft (or posted plan comment), cross-referenced against the student's Unit 2 repro comment on the GitHub issue thread.
**What good looks like:**
  - The stated cause explicitly cites specific functions, state variables, or flags that account for the exact behavior or outputs shown in the repro evidence.
  - The diagnosis does not attribute the bug to a component or mechanism that the repro evidence proves is uninvolved (e.g., blaming a pager when `--paging=never` exhibits the exact same delay).


## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives:**
  - Look under `## Scope` and `## Files to Modify` in `plan.md` draft or the plan comments on GitHub.
**What good looks like:**
  - The plan explicitly lists the exact files to be modified AND contains an explicit statement naming components, refactors, or behaviors "Not in scope" that will not be touched.
  - The bounded change targets only the minimal set of files necessary to resolve the grounded cause without introducing unrelated code reformatting or architectural shifts.


## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives:**
  - Look under `## Approach` in `plan.md` draft.
**What good looks like:**
  - The plan specifies concrete function calls, code logic changes, or specific configuration keys in named files rather than vauge descriptions.
  - A contributor who doesn't know with the author can identify the exact entry point and modification path to begin writing code immediately without further clarification.  (I.E. All information required is already provided.)


## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repo evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives:**
  - Look under `## Test Plan` in `plan.md` draft or the plan comment.
**What good looks like:**
  - The test plan specifies an automated test command or exact reproduction command paired with explicit quantifiable expected outputs.
  - Success is defined by concrete observable criteria rather than vague manual validation statements like "run app and check if it works."


## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives:**
  - Look under `## Risks` and `## Deviations` in `plan.md`.
**What good looks like:**
  - The plan explicitly identifies potential side effects, breaking changes, or unverified assumptions before building, rather than asserting complete certainty.
  - If the implementation diverges from the initial plan during building, the `## Deviations` section records what changed and why, or explicitly states "No deviations from plan" if executed as written.


## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives:**
  - Read the draft comment in `comment.md` or posted comment on GitHub against maintainer comments in the issue thread and the repro's contribution docs.
**What good looks like:**
  - The comment accurately summarizes the plan's diagnosis and scope without overpromising performance gains or claiming root-cause fixes outside what the plan delivers.
  - The comment directly respects all maintainer constraints in the thread and strictly complies with repo conventions, such as an AI-use disclosures statement.

