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

- **In a practice package:** Found under the "Plan context" section (stating the accepted plan and files in scope) compared against the package's "Diff" section.
- **In your live PR:** Found in `plan.md` (specifically the file scope and approach sections) compared against your branch diff (`git diff main...HEAD`).
- **What good looks like:** Every modified file in the diff is explicitly listed in the plan or its deviation notes. There are no unannounced file modifications, stray cleanups, or unrelated bug fixes.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

- **In a practice package:** Found under the "Test evidence" section at the bottom of the package file.
- **In your live PR:** Found in your `test_evidence.md` file (containing local test runs, linter outputs, and reproduction checks).
- **What good looks like:** Real, printed terminal command outputs showing execution results (e.g., passing unit tests or honestly disclosed test failures), rather than hand-typed placeholder notes or empty comments.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

- **In a practice package:** Found by inspecting the hunks in the package's "Diff" and "Commits" sections.
- **In your live PR:** Found by running `git diff main...HEAD` and inspecting commit history.
- **What good looks like:** A focused diff containing only the necessary changes, free from extraneous debugging code, stray print statements, commented-out dead code, or messy formatting changes.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

- **In a practice package:** Found in the package's "Repo facts" (checking contribution guidelines and AI policy requirements) and the PR's title/description.
- **In your live PR:** Found in your `pr_draft.md` file (checked against `.github/PULL_REQUEST_TEMPLATE.md` and repository contribution rules).
- **What good looks like:** Every required section of the repository's PR template (Summary, Issue, Changes, Testing, and Notes for Reviewers including explicit AI-use disclosure) is fully and honestly filled out.
