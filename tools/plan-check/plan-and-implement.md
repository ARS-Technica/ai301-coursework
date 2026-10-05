# Unit 3: Plan and Implement Report
# Implementation Plan - Issue #66: structlog output is not captured by pytest caplog

## 1. Plan Text
**Quoted Candidate Plan:**
```markdown
## Diagnosis

The application logs through `structlog`, which is not configured to capture or route log records into standard library (`logging`) handlers during test execution. As a result, pytest's `caplog` fixture (which captures `logging` module output) remains empty during assertions even when the code under test correctly emits log events.

This root cause was verified during local reproduction on commit `2f4e82f`. 

### Quoted Reproduction Evidence
**Environment:**
 - OS: Windows 11 (`win32`)
 - Python: 3.13.5
 - pytest: 9.1.1
 - structlog: 26.1.0

**Command executed:**
```powershell
 python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s --runxfail
```

**Observed Output:**
The warning message was emitted to stderr during the test run:
```text
 Empty chunks list provided to BatchEmbeddingProcessor
```

The test then failed specifically at the `caplog` assertion:
```text
       assert "Empty chunks list" in caplog.text or any(
             "empty" in record.message.lower() for record in caplog.records
         )
 E       AssertionError: assert ('Empty chunks list' in '' or False)
 E        +  where '' = <_pytest.logging.LogCaptureFixture object at 0x000001F4BBDFCC20>.text
 E        +  and   False = any(...)
```

**Conclusion:**
`structlog` emits the warning during execution, but because it is not propagated to stdlib logging in `tests/conftest.py`, pytest's `caplog` fixture fails to capture the output.

---

## Scope

### In Scope
- Configure `structlog` inside `tests/conftest.py` so that its outputs propagate to `logging.stdlib` during pytest runs.
- Ensure existing suite-wide log assertions using `caplog` capture `structlog` messages.
- Remove the `@pytest.mark.xfail(strict=True, reason="issue #66...")` decorator on `test_empty_chunks_list_returns_empty` in `tests/unit/test_batch_processor.py` so the test passes natively.

### Not in Scope
- Modifying production logging logic or changing `structlog` behavior outside the test suite setup in `tests/conftest.py`.
- Altering existing application business logic or adding new test cases beyond fixing the `caplog` assertion bridge.

---

## Files to Modify

1. `tests/conftest.py`: Add `structlog.configure()` or standard library integration processors (such as `structlog.stdlib.filter_by_level` and `structlog.stdlib.add_logger_name`) so `structlog` formats and emits records through `logging.getLogger()`.
2. `tests/unit/test_batch_processor.py`: Remove the temporary `xfail` marker from `test_empty_chunks_list_returns_empty`.

---

## Approach

1. Inspect `tests/conftest.py` to see current fixture setups.
2. Add a session-level pytest fixture or top-level configuration in `tests/conftest.py` using `structlog.configure()` configured with stdlib processors:
   - `structlog.stdlib.add_logger_name`
   - `structlog.stdlib.add_log_level`
   - `structlog.stdlib.PositionalArgumentsFormatter()`
   - `structlog.processors.StackInfoRenderer()`
   - `structlog.processors.format_exc_info()`
   - `structlog.stdlib.ProcessorFormatter.wrap_for_formatter`
   - Set `logger_factory=structlog.stdlib.LoggerFactory()`
3. Ensure standard library logging handler captures these events during testing.
4. Remove the `xfail` decorator on `test_empty_chunks_list_returns_empty`.

---

## Test Plan

### Pre-Fix Verification Command (Reproduction Step Re-run)
Run the unit test target:
```powershell
python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s
```

---

## 2. Setup Instructions
**Quoted Setup Instructions:**
```text
1. Open PowerShell and navigate to the repository clone directory:
   cd C:\Python\CodePath\AI\ai301-unit3-starter-main\eval\pathreview-ai301-fa26-s3

2. Activate the Python virtual environment:
   .\.venv\Scripts\Activate.ps1

3. Install the package and dependencies in editable mode:
   pip install -e .

4. Create and checkout a dedicated feature branch for Issue #66:
   git checkout -b fix/66-structlog-pytest-caplog
> ```
---

## 3. Execution Steps
> **Quoted Execution Steps:**
> ```text
1. Inspected `tests/conftest.py` to review existing pytest fixtures and logger setups.

2. Updated `tests/conftest.py` to configure `structlog` to emit logs via Python's standard library `logging` module during pytest runs using `structlog.stdlib.LoggerFactory()`.

3. Opened `tests/unit/test_batch_processor.py` and removed the `@pytest.mark.xfail(strict=True, reason="issue #66...")` decorator from `test_empty_chunks_list_returns_empty`.

4. Verified that `plan.md` and `comment.md` were untracked and excluded from staging via `git status`.

5. Staged and committed only the source file changes:
   git add tests/conftest.py tests/unit/test_batch_processor.py
   git commit -m "fix(tests): configure structlog stdlib integration for caplog assertions"

6. Pushed the feature branch to the GitHub remote fork:
   git push -u origin fix/66-structlog-pytest-caplog
```

---

## 4. Verification Strategy
**Quoted Verification Strategy:**
```text
1. Pre-Fix / Reproduction Check:
   Run the specific test with xfail enabled to observe failure behavior:
   python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s --runxfail

2. Post-Fix Verification:
   Run the specific test without the --runxfail flag to verify caplog captures structlog output and passes:
   python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s

   Expected Result: 1 passed in ~0.25s.

3. Suite Regression Check:
   Run the full unit test suite to ensure no existing tests regress:
   python -m pytest tests/unit/
```

---

## 5. Run History & Logs
/references/evidence-guide.md --save-run eval-run.txt
grading 20 package(s) with rubric.md + evidence-guide.md + procedure.md, model sonnet, 5 worker(s)...
  pkg-05: accept
  pkg-02: accept
  pkg-03: accept
  pkg-01: reject
  pkg-04: reject
  pkg-08: accept
  pkg-10: reject
  pkg-06: reject
  pkg-07: reject
  pkg-09: accept
  pkg-13: accept
  pkg-15: reject
  pkg-11: reject
  pkg-12: reject
  pkg-14: accept
  pkg-17: reject
  pkg-18: reject
  pkg-20: reject
  pkg-19: reject
  pkg-16: reject

item    category           gold    verdict  agree  note
pkg-01  wrong-cause        reject  reject   yes    
pkg-02  clear-accept       accept  accept   yes    
pkg-03  clear-accept       accept  accept   yes    
pkg-04  thread-convention  reject  reject   yes    
pkg-05  clear-accept       accept  accept   yes    
pkg-06  scope-creep        reject  reject   yes    
pkg-07  wrong-cause        reject  reject   yes    
pkg-08  clear-accept       accept  accept   yes    
pkg-09  clear-accept       accept  accept   yes    
pkg-10  unbuildable        reject  reject   yes    
pkg-11  wrong-cause        reject  reject   yes    
pkg-12  scope-creep        reject  reject   yes    
pkg-13  clear-accept       accept  accept   yes    
pkg-14  clear-accept       accept  accept   yes    
pkg-15  scope-creep        reject  reject   yes    
pkg-16  wrong-cause        reject  reject   yes    
pkg-17  unbuildable        reject  reject   yes    
pkg-18  unbuildable        reject  reject   yes    
pkg-19  scope-creep        reject  reject   yes    
pkg-20  thread-convention  reject  reject   yes    

categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
run written to eval-run.txt

---

## 6. Plan Evaluation

**Diagnosis Accuracy:** 
Evaluated whether the diagnosis identified the grounded root cause in the reproduction evidence rather than a surface symptom.

**Scope Boundaries:** 
Verified that all modified files were explicitly listed and non-essential refactors were placed out of scope.

**Test Decisiveness:** 
Confirmed that success criteria relied on concrete, automated tests rather than vague manual steps.

**Repo & Thread Compliance:** 
Ensured the candidate comment followed repository policies (e.g., mandatory AI disclosures) and thread directions.

---

## 7. Implementation Evaluation

**Build Performance:** 
I judged that my group's initial tests were a bit too casually phrased, so I spent some time experimenting with more precise ways of wording the checks with ChatGPT so as not to expend my Claude credits.  As a result of experimenting with another AI before running
Claude, my first run was nearly perfect.  I had only forgotten to
add the check for AI disclosures that I had written last week.

**Test Results:** [State whether all regression tests passed and cite test runner output].

**Deviations:** 
The group project outlined the correct checks; however, the wording we used during the group project was left vague due to time constraints.  I had to expand on the descriptions of each check
extensively.

Also, my original plan only accounted for issues discussed in the third week's lesson.  I need to return to week two's assignment to complete the checks accurately.  

---

## 8. Comparison Between Runs (Initial Run vs. Second Run)

**Initial Run Outcome:**
My first run achieved a 19/20, missing only pkg-20, "thread-convention". 

pkg-20  thread-convention  reject  accept   NO     graded accept

categories: clear-accept 7/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4
agreement: 19/20 scored items  (bar: 18/20: PASS)


**Adjustments Made:**
Upon examination of pkg-20, I realized that I had omitted the
requirement for an AI disclosure that I had included last week.
I added the "repo-convention" to rubric.md to explicitly account for AI Policy and Disclosure Rules.  The check ensures that the candidate plan comment strictly satisfies all repository contribution requirements.


**Second Run Outcome:**
The second run a score of 20/20 with pkg-20 correctly flagged as hold.  


**Key Takeaways:**
Cross-referencing plan comments against repo facts can prevent non-compliant PRs from being approved.

---

## 9. Final Verdict Output

grading 20 package(s) with rubric.md + evidence-guide.md + procedure.md, model sonnet, 5 worker(s)...
  pkg-05: accept
  pkg-02: accept
  pkg-03: accept
  pkg-01: reject
  pkg-04: reject
  pkg-08: accept
  pkg-10: reject
  pkg-06: reject
  pkg-07: reject
  pkg-09: accept
  pkg-13: accept
  pkg-15: reject
  pkg-11: reject
  pkg-12: reject
  pkg-14: accept
  pkg-17: reject
  pkg-18: reject
  pkg-20: reject
  pkg-19: reject
  pkg-16: reject

item    category           gold    verdict  agree  note
pkg-01  wrong-cause        reject  reject   yes    
pkg-02  clear-accept       accept  accept   yes    
pkg-03  clear-accept       accept  accept   yes    
pkg-04  thread-convention  reject  reject   yes    
pkg-05  clear-accept       accept  accept   yes    
pkg-06  scope-creep        reject  reject   yes    
pkg-07  wrong-cause        reject  reject   yes    
pkg-08  clear-accept       accept  accept   yes    
pkg-09  clear-accept       accept  accept   yes    
pkg-10  unbuildable        reject  reject   yes    
pkg-11  wrong-cause        reject  reject   yes    
pkg-12  scope-creep        reject  reject   yes    
pkg-13  clear-accept       accept  accept   yes    
pkg-14  clear-accept       accept  accept   yes    
pkg-15  scope-creep        reject  reject   yes    
pkg-16  wrong-cause        reject  reject   yes    
pkg-17  unbuildable        reject  reject   yes    
pkg-18  unbuildable        reject  reject   yes    
pkg-19  scope-creep        reject  reject   yes    
pkg-20  thread-convention  reject  reject   yes    

categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
run written to eval-run.txt

