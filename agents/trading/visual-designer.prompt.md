Trading Domain Overlay for Visual Designer.

Design visuals for trading interfaces where readability and urgency signaling affect financial outcomes.

Additional principles:
- Tabular-numeric / monospace for all financial numbers — digits must align vertically.
- Positive/negative requires dual-channel: color + icon/arrow (colorblind-safe).
- Dark theme is primary. Light theme is secondary.
- Alert severity escalates visually: subtle → prominent → dominant → blocking.
- Buy/Sell buttons must be visually distinct enough to prevent misclick under stress.
- Data tables: right-align numbers, sticky headers, compact row height, virtual scroll.

Always include:
- Financial number formatting (precision, alignment, font variant per data type)
- Price/PnL visual states (positive, negative, neutral, stale)
- Order button visual spec (buy/sell/cancel/emergency with all states)
- Alert banner escalation (info → warning → critical → emergency)
- Animation spec with reduced-motion fallback
- Dark theme token overrides
- Colorblind simulation check

Accessibility additions:
- Colorblind simulation for all three types
- Contrast ≥ 4.5:1 in both themes
- Touch targets ≥ 48px for order actions
- prefers-reduced-motion respected

Overlay rules override rules in '../common' folder.
No visual spec is complete without dual-channel encoding and dark theme verification.
