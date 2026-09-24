# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**ARS-Technica**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

---

## Posted upstream

**Claim comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5809804756

I'm claiming this issue to set up reproduction steps and build a baseline test case for adding the missing tests.


[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5810065958

Environment & Baseline Verification
OS / Platform: Windows 11 (win32, Python 3.13.5)
Test Runner: pytest-9.1.1
Reproduction Steps & Results
Executed existing unit tests for prompt templates:

pytest tests/unit/test_prompt_templates.py


collected 37 items

tests\unit\test_prompt_templates.py ..................................... [100%]
37 passed in 0.12s

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Run 1: 18/20 (Agreement: 90.0%, all categories matched)

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

`pkg-03`
- Rubric Verdict: `accept`
- Gold Label: `accept`
- Explanation: The package contained a complete claim comment and reproduction report for an issue describing unexpected behavior in template parsing. My rubric evaluated all required checks (`complex-prose`, `punctuation-check`, `symptom-alignment`, `tools-record`, and `traceable-proof`). The reproduction report included explicit OS environment details, step-by-step commands, and verbatim terminal output showing the reproduced error trace. Because all required checks passed, the verdict rule evaluated to `accept`, perfectly matching the gold label.


[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

"| symptom-alignment | output excerpt read against the issue's description | For bugs: the actual output or error trace matches the specific bug described in the issue. For enhancements or missing tests: the baseline report demonstrates the current missing functionality, failing test output, or initial state described in the issue ticket. | required |"

I revised this check to include an explicit branch for enhancement and missing-test issues. Initially, the check strictly required an error trace matching a bug report, which caused valid baseline reports for non-bug issues (like adding missing test suites) to evaluate as `unclear` and trigger an unwarranted `reject` verdict. Adding the enhancement branch ensured the check could validate baseline test execution output for missing-test issues while maintaining strict verification for bug reports.

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

By expanding the `symptom-alignment` check to accept baseline test suite execution (such as `pytest` output showing 100% passing tests) for enhancement issues, the rubric trades strictness for flexibility. The trade-off is accepting that a baseline test run confirms environment readiness even when no failing assertion exists yet. I re-ran `pkg-12` with `--only` to verify that this revision allowed valid enhancement baseline reports to pass without compromising the strict error-trace requirements for standard bug reports.

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
