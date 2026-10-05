# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the **Repro Evidence** first. Take note of the exact environment, reproduce steps, baseline timing/behavior data, and key findings (e.g., impact of individual flags or configuration changes).

2. Read the **Issue Description** and **Thread Highlights** to understand user reports and maintainer/community context.

3. Read the **Candidate Plan** and **Candidate Plan Comment**.


## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. Compare the plan's `Diagnosis` section against the **Repro Evidence**.

2. Does the Repro evidence actually point to the component or cause named in the diagnosis?
If the plan blames a component, but Repro tests show the problem persists/disappears regardless of that component, flag it as a Fail.

3. If there is no `Diagnosis`, flag it as a Fail.

4. If there is a `Diagnosis`, but there is no evidence, flag it as a Fail.

5. Compare the plan's `Scope` and `Approach` against the **Thread Highlights** and repro guidelines.

6. Does the plan respect maintainer directions, existing thread consensus, or repro-specific conventions (e.g., `CONTRIBUTING.md`) mentioned in the Thread Highlights? If not, flag it as a Fail.

7. If maintainers explicitly requested a specific fix path or barred changes to a specific file or module in the thread, verify that the plan described honors those boundaries. If not, flag it as a Fail.

8. Compare the **Candidate Plan Comment** against both the plan body and the thread context.

9. Does the comment accurately summarize the plan without making exaggerated claims or ignoring maintainer feedback?  If not, flag it as a Fail.


## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. **Grade `diagnosis-grounded`:**
   - Look at the `Diagnosis` in the candidate plan.
   - Cross-reference with the Repro timing data.
   - Assign **Pass** if grounded in Repro evidence; assign **Fail** if contradicted or unsupported by Repro data.

2. **Grade `scope-bounded`:**
   - Examine the `Scope` section.
   - Assign **Pass** if it lists modified files AND explicit "not in scope" boundaries.
   - Assign **Fail** if boundaries are missing or if the excluded scope contains the actual root cause.

3. **Grade `test-decisive`:**
   - Examine the `Test plan` section.
   - Assign **Pass** if it includes automated tests or clear, measurable benchmarks/metrics.
   - Assign **Fail** if the test criteria are vague or unmeasurable.

4. **Grade `comment-faithful`:**
   - Compare the `Candidate plan comment` against the plan body.
   - Assign **Pass** if the comment accurately summarizes the plan.
   - Assign **Fail** if the comment makes exaggerated claims about performance or fixes that the plan cannot deliver.

5. Grade `repo-convention`:
   - Check `Repo facts` for explicit posting rules (e.g., mandatory AI disclosures, required boilerplate, or vouching rules).
   - Read the `Candidate plan comment`.
   - Assign **Pass** if the comment complies with all repo facts and contribution rules.
   - Assign **Fail** if the comment omits required disclosures (e.g., missing AI-use disclosure when required by AI_POLICY.md) or violates repo rules.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Review the grades for all checks.

2. If **ALL** checks are **P**, **Pass**, output a verdict of `ready`.

3. If **ANY** check is **F**, **Fail**, **?**, or **Unclear**, output a verdict of `hold`.

4. Provide a clear, evidence-backed justification for any failed checks citing specific lines from the Repro data or Plan.

