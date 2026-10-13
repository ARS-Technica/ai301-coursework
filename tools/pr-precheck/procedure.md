# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. **Read the Issue, PR Title, and Description (`pr_draft.md`):** Read the issue thread, requirements, and the contributor's draft PR description first to understand the stated goals, claimed testing, and intended scope.
2. **Read the Plan (`plan.md`):** Read the plan's declared file scope, approach, and test plan before reviewing the diff, so you know exactly what changes were promised.
3. **Read the Diff (`git diff main...HEAD`) and Test Evidence (`test_evidence.md`):** Examine the branch diff file-by-file and check the test execution outputs to see what was actually committed and verified.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

1. **Silent Drift Gathering:** Cross-reference every modified file in the branch diff (`git diff main...HEAD`) against the plan's stated file list and deviation notes to verify that no unannounced modifications or unrelated cleanups occurred.
2. **Test Evidence Gathering:** Read `test_evidence.md` against the plan's test plan and repository check instructions (`make test-unit`, etc.). Verify whether command outputs contain real printed terminal logs rather than placeholders or hand-typed notes.
3. **Diff Quality Gathering:** Inspect the commit history and diff structure for extraneous debugging code, stray print statements, or dead code.
4. **Standards & Comms Gathering:** Read the PR title and description (`pr_draft.md`) against the repository's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and AI-use disclosure policies to check for missing required fields or skipped disclosures.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. **Grade `silent-drift`:** Compare the diff's changed files list against the plan. Assign **Pass** if every changed file is explicitly authorized by the plan or its deviation notes; assign **Fail** if any unlisted file was modified or refactored.
2. **Grade `not-tested`:**
   - Review `test_evidence.md` command blocks.
   - Assign **Pass** if test commands are accompanied by real terminal execution logs or command output traces demonstrating before/after behavior.
   - Assign **Fail** only if test evidence is completely missing, relies entirely on empty placeholders like `[paste output here]`, or lacks command output entirely.
3. **Grade `unreviewable`:** Review diff cleanliness. Assign **Pass** if focused and free of debugging clutter; assign **Fail** (preferred weight) if debris or stray hunks obstruct review.
4. **Grade `standards-wall`:** Compare `pr_draft.md` against the repository template. Assign **Pass** if every template section and the mandatory AI-use disclosure are fully populated; assign **Fail** if any template requirement or disclosure is skipped.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Review the per-check grades across all rubric checks.
2. Apply the binary verdict rule: output `accept` if **all** `required` checks pass and preferred checks are accounted for; output `reject` if **any** `required` check fails or evaluates to `unclear`.
3. If multiple checks fail, quote the **first failing required check in rubric order** in the output evidence block to anchor the rejection decision.
