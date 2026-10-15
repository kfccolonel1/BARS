# bars

Raw NQ and ES futures price bars. All timestamps converted to **America/New_York** (ISO with UTC offset). Columns: datetime,open,high,low,close[,volume]; IBKR files add `contract`. Files overlap; sources differ slightly.

| File | Symbol | TF | From | To | Rows | Size | Source |
|---|---|---|---|---|---|---|---|
| NQ/1min/tv_2024-06_2025-07.csv | NQ | 1min | 2024-06-21 | 2025-07-11 | 373,108 | 22.0 MB | TradingView CME_MINI:NQ1! export (continuous) |
| NQ/1min/tv_2025-07_2026-07.csv | NQ | 1min | 2025-07-13 | 2026-07-31 | 373,785 | 22.0 MB | TradingView CME_MINI:NQ1! export (continuous) |
| NQ/1min/tv_volume_2026-03_07.csv | NQ | 1min | 2026-03-01 | 2026-07-02 | 121,944 | 7.9 MB | TradingView NQ1! export with volume |
| NQ/1min/tv_chart_2026-03_06.csv | NQ | 1min | 2026-03-01 | 2026-06-18 | 108,441 | 6.4 MB | TradingView NQ1! chart exports, indicator columns stripped, merged |
| NQ/1min/tv_chart_2026-07.csv | NQ | 1min | 2026-07-02 | 2026-07-27 | 22,976 | 1.4 MB | TradingView CME_MINI:NQ1! chart exports (7 files), indicators stripped, merged |
| NQ/1min/alfordlabs_2025.csv | NQ | 1min | 2025-01-01 | 2025-12-31 | 353,233 | 22.1 MB | alfordlabs |
| NQ/1min/alfordlabs_2026-01_08.csv | NQ | 1min | 2026-01-01 | 2026-08-21 | 227,415 | 14.2 MB | alfordlabs |
| NQ/1min/alfordlabs_2026-08.csv | NQ | 1min | 2026-08-02 | 2026-08-28 | 27,600 | 1.7 MB | alfordlabs |
| NQ/1min/jun-aug_2026.csv | NQ | 1min | 2026-05-31 | 2026-08-28 | 89,032 | 5.8 MB | unknown vendor (SS50 project) |
| NQ/1min/ext_2026-09_10.csv | NQ | 1min | 2026-09-02 | 2026-10-08 | 31,428 | 1.9 MB | unknown vendor (extension after alfordlabs) |
| NQ/1min/seed_2026-06_07.csv | NQ | 1min | 2026-06-15 | 2026-07-31 | 47,100 | 2.8 MB | unknown vendor (fangap trader seed; believed NQ) |
| NQ/1min/yahoo_2026-09_10.csv | NQ | 1min | 2026-09-09 | 2026-10-08 | 28,742 | 1.8 MB | Yahoo Finance NQ=F |
| NQ/2min/yahoo_2026-09_10.csv | NQ | 2min | 2026-09-02 | 2026-10-09 | 17,361 | 1.1 MB | Yahoo Finance NQ=F |
| NQ/5min/yahoo_2026-07_10.csv | NQ | 5min | 2026-07-30 | 2026-10-09 | 13,509 | 0.9 MB | Yahoo Finance NQ=F |
| ES/3min/tv_2024_2025.csv | ES | 3min | 2024-01-01 | 2025-12-19 | 232,740 | 12.8 MB | TradingView ES1! chart export, indicators stripped |
| ES/1min/ib/ESH6.csv | ES | 1min | 2025-12-23 | 2026-03-17 | 78,375 | 5.2 MB | IBKR historical bars, contract ESH6 |
| ES/1min/ib/ESM6.csv | ES | 1min | 2026-03-08 | 2026-06-16 | 97,695 | 6.4 MB | IBKR historical bars, contract ESM6 |
| ES/1min/ib/ESU6.csv | ES | 1min | 2026-06-07 | 2026-09-15 | 97,680 | 6.4 MB | IBKR historical bars, contract ESU6 |
| ES/1min/ib/ESZ6.csv | ES | 1min | 2026-09-01 | 2026-10-02 | 31,498 | 2.1 MB | IBKR historical bars, contract ESZ6 |
