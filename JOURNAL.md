## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/43
**Issue title:** Agent session state is not cleared between reviews for the same user
**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
Currently, when a user conducts multiple reviews, the agent's session state is persisting instead of resetting between sessions. Because the state isn't cleared, data or context from a previous review can leak into a new one, leading to inaccurate agent behavior or corrupted session data. A successful fix will ensure that the session state dictionary or object is properly reinitialized or wiped clean either at the end of a review or the beginning of a new one. This will likely involve updating the state management logic within the agent or review-handling modules of the codebase.

**Branch name:** fix/43-clear-session-state
**Setup confirmation:** [x] App runs locally at localhost:5173
**Cohort ledger:** [x] Issue added to cohort ledger

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)
**Current progress:**
I have successfully set up the local environment, reproduced the session leakage issue (#43), and written out my implementation plan. I identified `session_storage.py` and its `SessionStore.delete()` method as the tool I will use to clear the state.

**Next steps:**
I need to locate the specific API controller/route that initializes a new review, inject the cache deletion logic into it, write/update unit tests to ensure it works, and run `make check`.

**Blockers:**
None at the moment.

### Check-in 2 (end of week)
**PR link:** [Paste your GitHub PR URL here]
**Branch:** fix/43-clear-session-state
**What you built:**
I fixed the issue where the AI agent's session state leaked between reviews for the same user. I updated `api/routes/reviews.py` to directly connect to Redis and delete the user's specific session cache key (`session:{current_user.id}`) immediately before a new review is initialized. This ensures the agent always starts with a completely blank memory slate.
**Tests added or updated:**
Added a new test file `tests/unit/test_issue_43.py`. It uses `@patch` to mock the Redis client and verifies that `create_review_endpoint` successfully calls `Redis.delete("session:<user_id>")` exactly once before creating the review.
**Self-review confirmation:** [x] make check passes  [x] make test-unit passes
**Draft PR feedback received from:** none