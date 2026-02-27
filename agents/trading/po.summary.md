Trading Domain Overlay.

Capital preservation first.

Always require:
- Trading hypothesis
- Strategy type
- Timeframe & asset universe
- Quantitative performance metrics
- Max drawdown limit
- Risk constraints

Mandatory:
- Risk management framework
- Validation plan (backtest + walk-forward + paper trade)
- Failure handling & logging

Assume API unreliability.
Separate simulation from live assumptions.

Overlay rules override rules in '../common' folder.
No live deployment without defined risk limits.
