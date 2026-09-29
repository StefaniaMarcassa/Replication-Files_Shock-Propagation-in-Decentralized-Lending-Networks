# Replication Files — *Shock Propagation in Decentralized Lending Networks*

Replication package for the paper *Shock Propagation in Decentralized Lending Networks* (Review of Finance, revision round 2).

## Repository structure

```
.
├── paper/
│   ├── Review_Finance_Round2.tex   # LaTeX source of the paper
│   └── figures/                    # All figures included in the paper
├── code/                           # Jupyter notebooks producing tables and figures
├── data/                           # Input data (CSV files, see data/README.md)
├── requirements.txt                # Python dependencies
└── README.md
```

## How to replicate

1. Put the input CSV files in `data/` (list in [`data/README.md`](data/README.md)).
2. Install the dependencies: `pip install -r requirements.txt`
3. Run the notebooks from inside `code/` (e.g. `cd code && jupyter lab`). Every notebook reads its inputs through
   `DATA_PATH = '../data/'`. Figures and `.tex` tables are written to the working directory (`code/`);
   copy the figures used in the paper to `paper/figures/`.

To compile the paper, run `pdflatex`/`bibtex` from inside `paper/` (the `.tex` refers to images as `figures/...`).
The bibliography file `refs.bib` and the `informs3` class are not included in this repository.

## Notebooks → tables and figures

| Notebook (`code/`) | Figures | Tables |
|---|---|---|
| `Regressions_REVISION.ipynb` | 7, 9, 10, 11, 17, 18, 19 | 5 (Panels A and B), 7, 8, 9, 10, 11 |
| `incremental_liquidity_RF_REVISION.ipynb` | 20 | |
| `incremental_solvency_RF_REVISION.ipynb` | 21 | |
| `Regressions_DesStats_REVISION.ipynb` | 3, 4, 5, 6, 8 | |
| `DataVSSimul_REVISION.ipynb` | 14, 15 | |
| `incremental_solvency_REVISION_new.ipynb` | 13 (solvency risk) | 2 (solvency risk) |
| `incremental_liquidity_REVISION_new.ipynb` | 13 (liquidity risk) | 2 (liquidity risk) |
| `Regressions_april29_B_all_size_shocks.ipynb` | 12 | |
| `Regressions_REVISION_all_size_shocks_with_borrowers.ipynb` | 16 | |

Figures 1 and 2 (bipartite network and balance-sheet diagrams) are illustrations and not produced by code.

Additional notebooks (robustness / supporting analyses, not mapped above):

- `Regressions_REVISION_liq_real.ipynb` — same as `Regressions_REVISION.ipynb`, using realized liquidations (`liquidation_real.csv`, `liquidation_pools_real.csv`).
- `Robustness_old_vs_new.ipynb` — compares results obtained with the original and the realized liquidation files; writes `robustness_old_vs_new.csv` and `close_factor_wedge.csv`.
- `predictive_tests_STANDALONE.ipynb` — predictive tests (null vs. full model); writes `table2_with_tests.tex`, `pr_curve_null_vs_full.pdf`, `precision_null_vs_full.pdf`.

## Figures → files

| Figure | Label | File (`paper/figures/`) |
|---|---|---|
| 1 | `fig:Bipartite_graph` | `Bipartite_Network.png` |
| 2 | `fig:liquidation_panels` | `Balance_Sheet_PreShock.png`, `Balance_Sheet_PostShock.png` |
| 3 | `fig:lending_pools` | `lending_pools.pdf` |
| 4 | `fig:users` | `users.pdf` |
| 5 | `fig:Pool_Contribution` | `Pool_contribution.png` |
| 6 | `fig:Share_Borrow` | `Pct_UtilRatio_Borrow.png` |
| 7 | `fig:r2_by_shock_size` | `shock_size.png` |
| 8 | `fig:reserve_changes` | `liquidity_risk_mean_new1.png` |
| 9 | `fig:liquidity_predictions` | `liquidity_risk_prediction_50.png` |
| 10 | `fig:forecast_errors` | `errors.png` |
| 11 | `fig:solvency_predictions` | `solvency_risk_predictions.png` |
| 12 | `fig:solvency_stablecoins_size100` | `solvency_stablecoins.png` |
| 13 | `fig:incremental` | `incremental_liquidity.png`, `solvency_risk_increment.png` |
| 14 | `fig:pr_curve` | `precision_recall.png` |
| 15 | `fig:liquidations_stress` | `liquidations_stress_episodes.png` |
| 16 | `fig:borrowers_comparison` | `borrowers_crypto.png` |
| 17 | `fig:robustness_size` | `robustness_size_shock.png` |
| 18 | `fig:appendix_fe_comparison` | `liquidity_risk_predictions_comp.png` |
| 19 | `fig:appendix_fe_comparison_solv` | `solvency_risk_prediction_comp.png` |
| 20 | `fig:rf_benchmark_liquidity` | `liquidity_RF.png` |
| 21 | `fig:rf_benchmark_solvency` | `solvency_RF_new.png` |
