---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

This tool answers exactly one question about a pull request package: **is this ready to submit?** A PR package consists of a candidate pull request (title, description, commits, diff, and test evidence), read against the plan it claims to implement and the issue that plan belongs to. The tool never answers any other question, never grades more than one package per run, and relies entirely on executing the components in this tool directory rather than gut feel.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

The tool runs in two distinct modes:

- **Live mode:** Grades your own upcoming pull request before submission. Inputs include your `plan.md` (with deviation notes included), your branch's diff (`git diff main...HEAD` run from the working copy against the repository's default branch), your draft PR title and description (`pr_draft.md`), your test evidence (`test_evidence.md`), and the issue thread. A house-chain student reads the house plan and house repro pack instead.
- **Eval mode:** Grades a frozen practice package bundle where the bundle is the whole world. Nothing is fetched or externally read, and every check runs with the full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, the tool reads `scope.md` first before checking any other file. It enforces the house rules found there and refuses to grade work outside the scoped repository. If the scope's `Repo:` line still carries an unfilled placeholder, the tool stops immediately without grading and instructs you to fill the `Repo:` line with your section's Path Review repository. Eval mode ignores `scope.md` entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, the tool reads `voice-guide.md` (carried forward from Unit 2) and holds outgoing PR text—specifically the PR title and description—against those rules, reporting any violated rules in its summary. The voice guide never alters the verdict on its own unless a rubric check explicitly reads it. Eval mode ignores `voice-guide.md` entirely, leaving universal communication-quality checks to the rubric.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

The tool connects component files sequentially: `rubric.md` defines checks and verdict rules, `references/evidence-guide.md` maps where each evidence family lives, and `procedure.md` executes as written step-by-step. If the procedure is silent on a step, the tool reports the gap instead of improvising. If `rubric.md` or `procedure.md` contains no content, the tool invokes the refusal rule and declines to grade.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

The verdict space is strictly binary: `accept` (ready to submit) or `reject` (hold). The tool ends its reply with the fenced JSON block below, valid and last, with nothing following it. The schema is reproduced verbatim from CONTRACT.md and must not be altered, extended, or reordered:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

The tool grades under strict standing rules:

Evidence first: No check is graded without naming the specific fact or quote that decided it.

Grade the thing, not the polish: Every check reads the artifact itself against the plan, issue, and stated standards, never mere formatting.

The rubric decides, not the run: If a check passes by its stated condition but feels wrong, it still passes; fixes belong in the rubric.

The procedure decides how, not the run: The tool follows procedure.md verbatim without silent workarounds.

Unclear defaults to fail: Where the rubric's verdict rule is silent, an unverifiable claim or an unverified PR defaults to a failing grade (reject).


### How to apply this:
1. Open your installed skill file: `~/.claude/skills/pr-precheck/SKILL.md`.
2. Replace its contents entirely with the block above.
3. Save the file and proceed to populate `rubric.md`, `procedure.md`, and `references/evidence-guide.md` as outlined in your assignment steps!