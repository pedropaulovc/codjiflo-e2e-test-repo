# File First Modified in Later Iteration Test

This directory contains test data for the E2E test that verifies files are correctly marked as "Modified" (not "Added") when they first appear in a later iteration.

## Test Scenario

1. **Base state**: `target-file.yml` exists in the PR base branch
2. **Iteration 1**: Modify `other-file.js` (but NOT `target-file.yml`)
3. **Iteration 2**: Modify `target-file.yml` for the first time in this PR

## Expected Behavior

When viewing iteration 2, `target-file.yml` should:
- Show status as **"M" (Modified)**, not "A" (Added)
- This tests the "base equivalence" fix

## Related Test

See the E2E test implementation in the main CodjiFlo repository:
- **Test file**: [`e2e/prod/iteration-mode/iteration-file-status.spec.ts`](https://github.com/pedropaulovc/codjiflo/blob/main/e2e/prod/iteration-mode/iteration-file-status.spec.ts)
- **Test name**: "File first modified in later iteration shows as modified, not added"

## How This Tests the Fix

The issue being tested: When a file exists in the PR base but is first modified in iteration 2 (not iteration 1), the diff engine should recognize that the base content exists (from the PR base), so it should be marked as Modified, not Added.

Without the fix, the file would incorrectly show as Added (A) because it wasn't in iteration 1's changed files.
