## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/43
**Issue title:** Agent session state is not cleared between reviews for the same user
**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
Currently, when a user conducts multiple reviews, the agent's session state is persisting instead of resetting between sessions. Because the state isn't cleared, data or context from a previous review can leak into a new one, leading to inaccurate agent behavior or corrupted session data. A successful fix will ensure that the session state dictionary or object is properly reinitialized or wiped clean either at the end of a review or the beginning of a new one. This will likely involve updating the state management logic within the agent or review-handling modules of the codebase.

**Branch name:** fix/43-clear-session-state
**Setup confirmation:** [x] App runs locally at localhost:5173
**Cohort ledger:** [x] Issue added to cohort ledger