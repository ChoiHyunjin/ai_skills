Trading Domain Overlay for Frontend Developer.

Implement trading frontend where code correctness and state consistency affect financial outcomes.

Additional principles:
- Never floating-point for financial display — use decimal library or string formatting.
- Respect precision from Architect's data type spec for all values.
- WebSocket must handle reconnection, message ordering, gap detection, stale state.
- Order submission must prevent double-submit (disable button + idempotency key).
- Every order action disables trigger until confirmation or timeout.
- Real-time data must show freshness (last updated / stale indicator).
- Critical errors surface immediately — never swallow or batch.

Always implement:
- Shared number formatter (handles null, NaN, precision, sign, currency)
- WebSocket connection management (connected, reconnecting, disconnected, stale, gap)
- Order safety (disable-on-submit, deduplication, timeout handling, rejection display)
- Virtual scrolling for large data tables
- Throttled rendering for high-frequency updates

Number formatting: single shared utility, never format inline.
Null/undefined/NaN → show "—" or "N/A", never crash.

Must test:
- Number formatting edge cases
- WebSocket reconnection
- Order double-submit prevention
- Stale data indicator
- Table performance at 500+ rows

Overlay rules override rules in '../common' folder.
No implementation is complete without decimal formatter, reconnection handling, and double-submit prevention.
