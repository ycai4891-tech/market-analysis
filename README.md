# Market Analysis

Python analyses built alongside my MSc in Business Analytics and Financial
Technology at the University of Dundee.

Every notebook runs end to end in Google Colab with no setup beyond one `pip install`.

---

## Trend-Following on Bitcoin, and Why It Failed on the FTSE 100

`bitcoin_trend_backtest.ipynb`

A 50/200-day moving-average crossover, backtested against buy and hold on Bitcoin
from 2014 and on the FTSE 100 from 2006. The same rule, the same code, two markets.

| | Bitcoin (12.0y) | FTSE 100 (20.6y) |
|---|---|---|
| Buy & hold Sharpe | 0.98 | 0.27 |
| Strategy Sharpe | **1.04** | 0.20 |
| Buy & hold max drawdown | −83.4% | −47.8% |
| Strategy max drawdown | **−69.3%** | **−37.3%** |
| Time in market | 58% | 65% |
| Parameter pairs beating buy & hold | **61 of 63** | 2 of 63 |

On the FTSE the filter cut drawdown by 10.5 points and still lost on Sharpe. Only
2 of 63 parameter pairs beat buy and hold, both at the same fast average, which
reads as a bright spot rather than a plateau: noise, not structure.

On Bitcoin the same rule cut a far deeper drawdown and 61 of 63 pairs beat buy and
hold. That is a plateau, and plateaus are what survive out of sample.

A 200-day average is a slow filter. It only earns its cost when drawdowns are deep
and long enough that sitting flat beats the entries it misses. Bitcoin's bear
markets were both. The FTSE's were not.

**What argues against the Bitcoin result.** Buy and hold returned 16,883% against
the strategy's 13,629%, so roughly a fifth of terminal wealth is surrendered to cut
the drawdown. Sharpe rises 0.98 to 1.04 and Calmar 0.64 to 0.74, but Sortino falls
1.30 to 1.05: being flat 58% of the time removes upside faster than downside
deviation. And twelve years inside one secular uptrend is a small sample, in an
asset that is only here because it survived.

**How the backtest avoids flattering itself.** The signal is lagged one day, so a
crossover at Monday's close is traded at Tuesday's. Transaction costs of 10bps are
charged per position change. Annualisation is derived from the data rather than
assumed, because Bitcoin trades 365 days a year and an equity index about 252;
hardcoding 252 for both would report Bitcoin's twelve years as seventeen. And 63
parameter pairs are swept per asset, because any moving-average rule can be tuned
until one pair looks good.

---

## Trend-Following Overlay on the FTSE 100

`trend_following_backtest.ipynb`

The original single-asset study, kept because it is where the question started and
because it is the control case above. The finding was negative and is reported as
such. Superseded by `bitcoin_trend_backtest.ipynb`, which runs both assets with the
same code and a corrected annualisation.

---

## Drawdown, Attribution and Valuation

`market_analysis.ipynb`

Three shorter analyses in one notebook.

**Bitcoin drawdown, 2022–2023 cycle.** A 66.9% peak-to-trough drawdown over 10.6
months, $47,687 down to $15,787, measured with a cumulative-maximum method on daily
closes rather than eyeballed from a chart.

**Five-week equity portfolio against the FTSE 100.** An equal-weighted five-holding
portfolio returning 3.79% against the index's 2.84%, with per-holding attribution
so the 95bps of outperformance can be traced to individual positions rather than
left as a single headline number.

**Tesco PLC DCF.** A five-year FCFF discounted cash flow at a 7.66% WACC with
terminal value, producing a £51.8bn enterprise value and a 565p intrinsic value.
Rebuilt in Python and validated against the Excel model from a university
valuation project.

---

## Tools

Python · Pandas · yfinance · matplotlib
