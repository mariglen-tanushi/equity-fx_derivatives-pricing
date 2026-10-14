# Data Requirements

The pipeline expects the raw files in a `Raw_Data/` folder next to the notebook. Intermediate files are written to `thesis_processed/`, calibration and pricing results to `results/`, and the final tables and figures to `outputs/`.

```
Colab Notebooks/
├── thesis_pipeline.ipynb
├── Raw_Data/
│   ├── spx_eod_*.7z                  SPX option chains (optionsDX)
│   ├── vix_eod_*.7z                  VIX archives (optionsDX)
│   ├── eurusd_vol_snapshots_74.csv   EUR/USD OTC volatility quotes (LSEG REFINITIV)
│   ├── EURUSD_spot_LSEG.csv          EUR/USD spot, EUR= (LSEG REFINITIV)
│   ├── SP500_dailyclose.csv          S&P 500 daily close (FRED, SP500)
│   ├── ECB_EURIBOR_Data.csv          3-month Euribor, monthly (ECB Data Portal)
│   └── VIX_History.csv               VIX daily close (Cboe)
├── thesis_processed/
├── results/
└── outputs/
```

## Sources

| File | Provider | Access |
|------|----------|--------|
| `spx_eod_*.7z` | optionsDX | Paid subscription |
| `eurusd_vol_snapshots_74.csv` | LSEG REFINITIV | Institutional licence (ATM, 25Δ/10Δ RR and BF per tenor) |
| `EURUSD_spot_LSEG.csv` | LSEG REFINITIV | Institutional licence |
| `SP500_dailyclose.csv` | FRED | Free: https://fred.stlouisfed.org/series/SP500 |
| `ECB_EURIBOR_Data.csv` | ECB Data Portal | Free: series FM.M.U2.EUR.RT.MM.EURIBOR3MD_.HSTA |
| `VIX_History.csv` | Cboe | Free: https://cdn.cboe.com/api/global/us_indices/daily_prices/VIX_History.csv |
| USD Treasury rates (DGS3MO) | FRED | Downloaded by the notebook |

## Notes

- SPX implied volatilities are recomputed from bid-ask mid prices; the vendor IV column is used only as a cross-check.
- Euribor is published here as monthly averages. Each date uses the latest average that is complete on that date: its own month from the last TARGET business day of the month onwards, the previous month before that. No date relies on a fixing published after it.
- Without the optionsDX and LSEG files the surfaces cannot be rebuilt from scratch. The copula calibration and pricing sections can be rerun from the intermediate files in `thesis_processed/` if those are available.
