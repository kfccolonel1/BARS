# BARS — NQ & ES futures price bars

All times **America/New_York** (ISO 8601 with offset). Real bars only, never gap-filled (see `gaps` in `catalog.json`). Prices are **unadjusted** front month (jumps at quarterly rolls).

## Which file should my app use?

| Need | File |
|---|---|
| NQ 1-min, everything (2024-06-21 → 2026-10-08, with volume) | [`NQ/1min/NQ_1min_continuous.csv.gz`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_continuous.csv.gz) (gzip) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2024-06-21_2024-12-31_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2024-06-21_2024-12-31_stitched.csv) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2025-01-01_2025-12-31_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2025-01-01_2025-12-31_stitched.csv) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2026-01-01_2026-10-08_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2026-01-01_2026-10-08_stitched.csv) |
| ES 1-min (2025-06-20 → 2026-10-09, with volume) | [`ES/1min/ES_1min_2025-06-20_2026-10-09_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/ES/1min/ES_1min_2025-06-20_2026-10-09_stitched.csv) |
| ES 3-min history 2024–2025 | [`ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview.csv) |
| NQ 2min (Yahoo) | [`NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv) |
| NQ 5min (Yahoo) | [`NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv) |
| All files + metadata | [`catalog.json`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/catalog.json) |

## Columns
`datetime,open,high,low,close,volume,source,trading_date,session`. `session`=`RTH` 09:30–15:59 ET else `ETH`; `trading_date`=CME session date (bars from 18:00 ET belong to next weekday).

## Sources & priority
Per minute, first available: **alfordlabs** (from kfccolonel1/AlfordLabs `bars/`, with volume) → TradingView NQ1! → IBKR → older alfordlabs → Yahoo NQ=F. ES: alfordlabs → IBKR. alfordlabs matches TradingView on 98.3% of overlapping NQ minutes and IBKR on 93.4% of ES minutes (differences around roll weeks). `rows_by_source` in catalog.json.

## Known gaps
Only exchange closures remain: holidays/early closes, 2025-01-09 (national day of mourning), Good Friday 2025-04-18 and 2026-04-03, New Year. NQ before 2024-08-04 comes from TradingView (no volume).

## raw/
Original sources, normalized to ET, named `SYMBOL_TF_START_END_SOURCE`. Note: `raw/NQ/1min/*_ibkr-ext.csv` is labeled IBKR per Rich but its prices match Yahoo NQ=F exactly; TradingView *chart* exports roll at expiry.

| File | Rows |
|---|---|
| [`raw/ES/1min/ES_1min_2025-06-20_2026-10-09_alfordlabs-gh.csv.gz`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ES_1min_2025-06-20_2026-10-09_alfordlabs-gh.csv.gz) | 464,160 |
| [`raw/ES/1min/ib/ES_1min_2025-12-23_2026-03-17_ibkr-ESH6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2025-12-23_2026-03-17_ibkr-ESH6.csv) | 78,375 |
| [`raw/ES/1min/ib/ES_1min_2026-03-08_2026-06-16_ibkr-ESM6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-03-08_2026-06-16_ibkr-ESM6.csv) | 97,695 |
| [`raw/ES/1min/ib/ES_1min_2026-06-07_2026-09-15_ibkr-ESU6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-06-07_2026-09-15_ibkr-ESU6.csv) | 97,680 |
| [`raw/ES/1min/ib/ES_1min_2026-09-01_2026-10-02_ibkr-ESZ6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-09-01_2026-10-02_ibkr-ESZ6.csv) | 31,498 |
| [`raw/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview-chart.csv) | 232,740 |
| [`raw/NQ/1min/NQ_1min_2024-06-21_2025-07-11_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2024-06-21_2025-07-11_tradingview.csv) | 373,108 |
| [`raw/NQ/1min/NQ_1min_2024-08-04_2026-10-08_alfordlabs-gh.csv.gz`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2024-08-04_2026-10-08_alfordlabs-gh.csv.gz) | 772,780 |
| [`raw/NQ/1min/NQ_1min_2025-01-01_2025-12-31_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2025-01-01_2025-12-31_alfordlabs.csv) | 353,233 |
| [`raw/NQ/1min/NQ_1min_2025-07-13_2026-07-31_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2025-07-13_2026-07-31_tradingview.csv) | 373,785 |
| [`raw/NQ/1min/NQ_1min_2026-01-01_2026-08-21_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-01-01_2026-08-21_alfordlabs.csv) | 227,415 |
| [`raw/NQ/1min/NQ_1min_2026-03-01_2026-06-18_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-03-01_2026-06-18_tradingview-chart.csv) | 108,441 |
| [`raw/NQ/1min/NQ_1min_2026-03-01_2026-07-02_tradingview-vol.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-03-01_2026-07-02_tradingview-vol.csv) | 121,944 |
| [`raw/NQ/1min/NQ_1min_2026-05-31_2026-08-28_ibkr-ss50.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-05-31_2026-08-28_ibkr-ss50.csv) | 89,032 |
| [`raw/NQ/1min/NQ_1min_2026-06-15_2026-07-31_ibkr-seed.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-06-15_2026-07-31_ibkr-seed.csv) | 47,100 |
| [`raw/NQ/1min/NQ_1min_2026-07-02_2026-07-27_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-07-02_2026-07-27_tradingview-chart.csv) | 22,976 |
| [`raw/NQ/1min/NQ_1min_2026-08-02_2026-08-28_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-08-02_2026-08-28_alfordlabs.csv) | 27,600 |
| [`raw/NQ/1min/NQ_1min_2026-09-02_2026-10-08_ibkr-ext.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-09-02_2026-10-08_ibkr-ext.csv) | 31,428 |
| [`raw/NQ/1min/NQ_1min_2026-09-09_2026-10-08_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-09-09_2026-10-08_yahoo.csv) | 28,742 |
| [`raw/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv) | 17,361 |
| [`raw/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv) | 13,509 |
