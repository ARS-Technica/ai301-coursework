# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

* **Where it lives:**
  * **Eval bundle:** Located in the `repro report` section under `## Environment` or `## Setup`.
  * **Live mode:** Located in the draft reproduction comment or the system context section of the GitHub comment.
* **What good looks like:** The record explicitly names the Operating System (e.g., `macOS 15.5`, `Ubuntu 22.04 LTS`), the runtime/language version (e.g., `Node v20.10.0`, `Python 3.11.4`), and the specific tool or package version (e.g., `yq v4.53.3`). The versions named either match the issue target or explicitly account for any version differences tested.


## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

* **Where it lives:**
  * **Eval bundle:** Located in the `repro report` under `## Steps to Reproduce` or `## Execution`.
  * **Live mode:** Located in the step-by-step code/terminal block section of the draft comment.
* **What good looks like:** The steps provide explicit CLI commands or minimal code snippets starting from a clean checkout state to the execution point. A developer unfamiliar with the project could run the exact commands sequentially without needing to infer missing parameters or configuration flags.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

* **Where it lives:**
  * **Eval bundle:** Located in the `repro report` raw log output block, cross-referenced against the `issue context` problem description.
  * **Live mode:** Located in the terminal output/stack trace code block (` ``` `) in the draft comment, compared against the issue thread URL.
* **What good looks like:** The terminal output or stack trace directly displays the specific error message, exception type, or failure described in the original issue ticket (e.g., `panic: not a string`), rather than an unrelated build setup, path error, or syntax typo.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

* **Where it lives:**
  * **Eval bundle:** Located where the conclusion statement in the `repro report` meets the attached execution log output.
  * **Live mode:** Located in the summary text of the draft comment evaluated directly against the provided log outputs.
* **What good looks like:** The written summary accurately matches what the attached log displays. If the bug could not be reproduced or yielded a different output, the text explicitly reports a failure to reproduce rather than falsely claiming a successful reproduction.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

* **Where it lives:**
  * **Eval bundle:** Located in the `claim comment` and `repro report` bodies, evaluated against the `repo-facts` block (such as `CONTRIBUTING.md` policies or template rules).
  * **Live mode:** Located in the text of the draft comment, cross-referenced against the repository's posted issue templates and AI disclosure policies.
* **What good looks like:** The text adheres to all repository-specific rules (including required AI disclosures if mandated by repo policy), omits generic AI boilerplate and superficial greetings, and limits formatting to simple text and standard code blocks.

