# BARS — NQ & ES futures price bars

All times **America/New_York** (ISO 8601 with UTC offset). Real bars only — gaps are never filled; see `gaps` in `catalog.json`. Prices are **unadjusted** front month (jumps at quarterly rolls).

## Which file should my app use?

| Need | File |
|---|---|
| NQ 1-min, everything in one file | [`NQ/1min/NQ_1min_continuous.csv.gz`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_continuous.csv.gz) (gzip; 2024-06-21 → 2026-10-08) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2024-06-21_2024-12-31_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2024-06-21_2024-12-31_stitched.csv) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2025-01-01_2025-12-31_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2025-01-01_2025-12-31_stitched.csv) |
| NQ 1-min, one year | [`NQ/1min/NQ_1min_2026-01-01_2026-10-08_stitched.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/1min/NQ_1min_2026-01-01_2026-10-08_stitched.csv) |
| ES 1-min (2025-12 → 2026-10) | [`ES/1min/ES_1min_2025-12-23_2026-10-02_ibkr-continuous.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/ES/1min/ES_1min_2025-12-23_2026-10-02_ibkr-continuous.csv) |
| ES 2024–2025 history (3-min) | [`ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview.csv) |
| NQ 2min (Yahoo) | [`NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv) |
| NQ 5min (Yahoo) | [`NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv) |
| Every file + metadata, machine-readable | [`catalog.json`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/catalog.json) |

## Columns
`datetime,open,high,low,close,volume,source,trading_date,session` (ES 1-min adds `contract`). `session` = `RTH` for 09:30–15:59 ET bars, else `ETH`. `trading_date` = CME session date (bars from 18:00 ET belong to the next weekday). `volume` is blank where the source had none (TradingView continuous).

## How the NQ continuous file is built
Per minute, the first available of: TradingView NQ1! → alfordlabs → SS50 vendor → Yahoo NQ=F 1-min → Yahoo-derived 2-min. On overlap TradingView and alfordlabs match 98–99% exactly. `source` column shows which won.

## ES continuous
IBKR single-contract bars; switches to next contract on the first trading date its volume is higher. Rolls: 2026-03-16: ESH6->ESM6; 2026-06-15: ESM6->ESU6; 2026-09-14: ESU6->ESZ6.

## Known gaps / quality
- Holiday early closes and closures are real (not missing data); 2025-01-09 closure (national day of mourning).
- **NQ 2026-08-28 17:00 → 2026-09-02 20:00 missing** (no source covers it).
- **NQ 2026-09-02 → 09-09: 2-minute bars only** (Yahoo-derived), so ~195 of 390 RTH rows per day; full 1-min resumes 2026-09-09.
- `raw/` TradingView *chart* exports roll at expiry and differ ~215–320 pts from the others during roll weeks (2026-03-17..19, 2026-06-14..18); not used in continuous files.
- ES 3-min has no volume. ES 1-min covers only 2025-12-23 → 2026-10-02.

## raw/
Original sources (normalized to ET, deduped), named `SYMBOL_TF_START_END_SOURCE.csv`.

| File | Rows |
|---|---|
| [`raw/ES/1min/ib/ES_1min_2025-12-23_2026-03-17_ibkr-ESH6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2025-12-23_2026-03-17_ibkr-ESH6.csv) | 78,375 |
| [`raw/ES/1min/ib/ES_1min_2026-03-08_2026-06-16_ibkr-ESM6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-03-08_2026-06-16_ibkr-ESM6.csv) | 97,695 |
| [`raw/ES/1min/ib/ES_1min_2026-06-07_2026-09-15_ibkr-ESU6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-06-07_2026-09-15_ibkr-ESU6.csv) | 97,680 |
| [`raw/ES/1min/ib/ES_1min_2026-09-01_2026-10-02_ibkr-ESZ6.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/1min/ib/ES_1min_2026-09-01_2026-10-02_ibkr-ESZ6.csv) | 31,498 |
| [`raw/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/ES/3min/ES_3min_2024-01-01_2025-12-19_tradingview-chart.csv) | 232,740 |
| [`raw/NQ/1min/NQ_1min_2024-06-21_2025-07-11_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2024-06-21_2025-07-11_tradingview.csv) | 373,108 |
| [`raw/NQ/1min/NQ_1min_2025-01-01_2025-12-31_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2025-01-01_2025-12-31_alfordlabs.csv) | 353,233 |
| [`raw/NQ/1min/NQ_1min_2025-07-13_2026-07-31_tradingview.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2025-07-13_2026-07-31_tradingview.csv) | 373,785 |
| [`raw/NQ/1min/NQ_1min_2026-01-01_2026-08-21_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-01-01_2026-08-21_alfordlabs.csv) | 227,415 |
| [`raw/NQ/1min/NQ_1min_2026-03-01_2026-06-18_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-03-01_2026-06-18_tradingview-chart.csv) | 108,441 |
| [`raw/NQ/1min/NQ_1min_2026-03-01_2026-07-02_tradingview-vol.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-03-01_2026-07-02_tradingview-vol.csv) | 121,944 |
| [`raw/NQ/1min/NQ_1min_2026-05-31_2026-08-28_unknown-ss50.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-05-31_2026-08-28_unknown-ss50.csv) | 89,032 |
| [`raw/NQ/1min/NQ_1min_2026-06-15_2026-07-31_unknown-seed.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-06-15_2026-07-31_unknown-seed.csv) | 47,100 |
| [`raw/NQ/1min/NQ_1min_2026-07-02_2026-07-27_tradingview-chart.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-07-02_2026-07-27_tradingview-chart.csv) | 22,976 |
| [`raw/NQ/1min/NQ_1min_2026-08-02_2026-08-28_alfordlabs.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-08-02_2026-08-28_alfordlabs.csv) | 27,600 |
| [`raw/NQ/1min/NQ_1min_2026-09-02_2026-10-08_yahoo-derived.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-09-02_2026-10-08_yahoo-derived.csv) | 31,428 |
| [`raw/NQ/1min/NQ_1min_2026-09-09_2026-10-08_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/1min/NQ_1min_2026-09-09_2026-10-08_yahoo.csv) | 28,742 |
| [`raw/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/2min/NQ_2min_2026-09-02_2026-10-09_yahoo.csv) | 17,361 |
| [`raw/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv`](https://raw.githubusercontent.com/kfccolonel1/BARS/main/raw/NQ/5min/NQ_5min_2026-07-31_2026-10-09_yahoo.csv) | 13,509 |
