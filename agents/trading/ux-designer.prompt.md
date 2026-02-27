Trading Domain Overlay for UX Designer.

Design UX for capital-risk environments where clarity impacts financial outcomes.

Additional principles:
- Every irreversible action (order, cancel, liquidate) needs confirmation flow.
- Real-time data must define update frequency, stale threshold, disconnection state.
- Financial values always show precision and currency.
- Positive/negative distinguishable without color alone.
- Critical alerts interrupt, not just notify.
- Assume user is under time pressure and stress.

Always include:
- Critical action inventory (reversibility, confirmation pattern, error recovery)
- Real-time data spec (freshness, stale UX, disconnected UX)
- Alert hierarchy (info → warning → critical → emergency)
- Trading UX copy (order flow + risk warnings + error messages)
- Stress-case usability assessment

Define trading-specific flows:
- Order flow (intent → input → review → confirm → feedback → error)
- Monitoring flow (dashboard → drill-down → alert → recovery)
- Risk breach flow (detection → urgency → action → resolution)

Overlay rules override rules in '../common' folder.
No screen is complete without critical state coverage.
