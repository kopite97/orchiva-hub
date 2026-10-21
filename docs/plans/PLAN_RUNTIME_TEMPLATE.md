# PLAN-XXXX: <Title>

## Overview

- **Status:** Planned
- **Issue:** <GitHub Issue or None>
- **Dependencies:** None
- **Authorization:** Pending

## Objective

Describe the expected outcome and purpose of this plan.

## Scope

**In Scope**
- <Required change>

**Out of Scope**
- <Explicitly excluded work>

## Acceptance Criteria

- [ ] <Observable requirement>
- [ ] <Expected behavior or constraint>
- [ ] <Failure or edge-case behavior>

## Implementation Steps

- [ ] <Step 1>
- [ ] <Step 2>
- [ ] <Step 3>

Keep implementation steps focused and independently verifiable.

## Runtime Verification

### Test Environment

- Use the isolated Docker environment defined in `compose.test.yml`.
- Follow `../agents/TESTING.md` for test execution and cleanup.
- Never use development or production databases for automated tests.

### Verification Checklist

- [ ] Required automated tests pass.
- [ ] Application builds successfully.
- [ ] Runtime behavior satisfies acceptance criteria.
- [ ] Database migrations and transactions are verified when applicable.
- [ ] Swagger / OpenAPI is verified when APIs change.
- [ ] Test containers, networks, and temporary volumes are removed.

Remove non-applicable checks when creating the plan.

### Verification Results

- **Status:** Not Run
- **Commands Executed:** None
- **Test Results:** Pending
- **Runtime Results:** Pending
- **Cleanup Results:** Pending
- **Unverified Items:** None

Record actual results and failures. Never report verification as successful without executing it.

## Progress

- **Completed:** None
- **Remaining:** <Remaining work>
- **Issues:** None

### On Hold / Blocked

- **Reason:** None
- **Resumption Conditions:** None

Update these fields when work is paused or blocked so another agent can resume safely.

## Completion

- [ ] Acceptance criteria satisfied.
- [ ] Implementation steps completed.
- [ ] Required verification passed.
- [ ] Plan status and `README.md` updated.

**Summary:** <Implemented changes and final outcome>

**Limitations:** None