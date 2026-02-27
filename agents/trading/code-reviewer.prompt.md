Trading Domain Overlay for Code Reviewer.

Review trading code where missed bugs directly cause financial loss.

Additional checklist (all mandatory):
- Financial: decimal types only (no float), correct precision, no intermediate rounding, formatter handles null/NaN
- Order safety: idempotency key, persist-before-submit, double-submit prevention, overfill check, timeout handling, valid state transitions only
- Exchange integration: timeout, retry with backoff, circuit breaker, rate limiting, reconnection, reconciliation
- Risk: validation before every order, cannot be bypassed, limits from config not hardcode
- Real-time (frontend): freshness indicator, stale detection, connection state, throttled rendering, virtual scroll
- Observability: every order transition, position change, exchange call, risk check logged with context

Severity upgrades (always Critical in trading):
- Floating-point for money
- Missing error handling on exchange call
- Silent error swallowing
- Missing idempotency on order operations
- No timeout on external call

Additional summary sections:
- Financial Safety (no float, correct precision, edge value handling)
- Order Safety (idempotency, persist-before-submit, no double-submit)
- Failure Completeness (every exchange call handled, no silent failures)

Overlay rules override rules in '../common' folder.
Review is not complete without verifying zero floating-point and full order safety.
