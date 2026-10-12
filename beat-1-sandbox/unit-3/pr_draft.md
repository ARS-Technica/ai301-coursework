fix: configure structlog for standard library logging capture in tests

## Summary
- **What the change does:** Configures structlog in tests/conftest.py to propagate log events into the standard library logging system during test runs, allowing pytest's caplog fixture to properly capture them.
- **Why:** The application logs through structlog, but it lacked integration with stdlib logging during tests. As a result, tests asserting on caplog (such as test_empty_chunks_list_returns_empty in tests/unit/test_batch_processor.py) failed suite-wide even though the expected warnings were visibly emitted to stderr.

## Issue
Closes #66

## Changes
- Configure global structlog processor chain or capture settings in tests/conftest.py so events forward to stdlib logging.
- Remove the @pytest.mark.xfail marker from tests/unit/test_batch_processor.py for issue #66, enabling the test suite to validate logging assertions properly.

## Testing
- [x] Unit tests added/updated and passing
- [ ] Integration tests (N/A)
- [x] Lint checks passing
- [x] Type checks passing
- [ ] CI/CD checks (Will run upon opening PR)

### Before and After Reproduction Output
**Before:**
```powershell
python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s --runxfail
# Output: Fails because caplog.text is empty despite the warning being emitted.

# Output: Fails because caplog.text is empty despite the warning being emitted.
**After:**
python -m pytest "tests/unit/test_batch_processor.py::TestBatchEmbeddingProcessor::test_empty_chunks_list_returns_empty" -vv -s
# Output: Passes successfully with caplog catching the log message.

## Notes for Reviewers
AI-use disclosure: I used AI collaborative assistance as a programming partner to help draft and verify test reproduction logic, configure structlog test setup settings, and format documentation for this pull request.

Plan deviations: None, implemented exactly as planned.
