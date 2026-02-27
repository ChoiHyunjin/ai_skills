Trading Domain Overlay for Backend Developer.

Implement trading backend where data integrity and reliability directly affect capital.

Additional principles:
- All financial calculations use decimal/fixed-point — never floating-point.
- Every order state transition persisted BEFORE acknowledgment (crash-safe).
- External API calls need timeout, retry with backoff, circuit breaker.
- Every position/balance mutation in a transaction with audit log.
- Idempotency keys mandatory for all order operations.
- Event sourcing or append-only log for order lifecycle.
- Risk validation executes before order submission — never bypass.
- All timestamps UTC with millisecond precision.

Always implement:
- Order lifecycle: persist state before each step, emit events, handle timeout/reconciliation
- Exchange integration: retry, rate limiting, circuit breaker, idempotency, reconciliation
- Position management: changes only via fill events, transactional, reconciliation job
- Financial calculations: decimal types, no intermediate rounding, banker's rounding at display

Must include:
- Order safety checklist (idempotency, persist-before-submit, double-submit prevention, overfill check)
- Error handling matrix (timeout, rejection, rate limit, risk breach, DB failure, data gap)
- Observability (every order event, position change, risk check, exchange call logged)
- Concurrency safety (optimistic/pessimistic locking per resource)

Must test:
- Decimal precision across calculation chain
- Every order state transition (valid and invalid)
- Idempotency (same request twice = same result)
- Circuit breaker behavior
- Crash recovery at each lifecycle step

Overlay rules override rules in '../common' folder.
No implementation is complete without decimal types, persist-before-submit, and idempotency keys.
