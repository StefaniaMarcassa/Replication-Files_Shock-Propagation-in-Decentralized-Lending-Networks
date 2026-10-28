# Shock Propagation in Decentralized Lending Networks: Evidence from the Compound Protocol

Replication code for the paper. Tovanich, Kitzler, Makridis, Marcassa and Prat.

This repository holds the analysis code. The data it reads, roughly 1 GB of simulation
output and feature files, is archived separately because GitHub cannot host files of that
size.

**Data:** [https://doi.org/10.7910/DVN/XXXXXX](https://doi.org/10.7910/DVN/XXXXXX)
(Harvard Dataverse)

---

## Reproducing the paper

```bash
git clone https://github.com/StefaniaMarcassa/Replication-Files_Shock-Propagation-in-Decentralized-Lending-Networks.git
cd Replication-Files_Shock-Propagation-in-Decentralized-Lending-Networks
pip install -r requirements.txt
```

Download the eleven source files from the Dataverse deposit into `data/`. The notebooks
read them from there and will not run without them. `data/README.md` lists the files and
says which notebooks use each one.

```bash
jupyter lab
```

Then open any notebook in `code/` and run it top to bottom. The notebooks are independent
of one another: each builds the panel it needs in its first cells, so they can be run in
any order or on their own.

### The analysis panel

`data/analysis_panel.csv.gz` ships with this repository. It is the merge of the simulation
output and the feature files that the notebooks otherwise build for themselves: 151,440
rows by 168 columns, the four analysis pools (ETH, WBTC, DAI, USDC), daily from 1 January
2021 to 15 June 2024, at ten shock sizes and three health thresholds.

The notebooks do not read it. It is here so that the estimation sample can be inspected,
or reused in other work, without downloading the full deposit.

Filtering it to the estimation sample reproduces the paper's samples exactly:

```python
import pandas as pd
panel = pd.read_csv('data/analysis_panel.csv.gz', parse_dates=['date'])

crypto = panel[(panel['asset_group'] == 'Crypto')
               & (panel['size'] == 0.50)
               & (panel['health_threshold'] == 10)]
# 2,524 pool-days: ETH 1,262 and WBTC 1,262
# training 1,607 to 15 March 2023, test 401 to 1 October 2023
```

Stablecoin specifications use `asset_group == 'Stablecoin'` and `size == 1.00`.

---

## What each notebook produces

The numbering follows the order in which the results appear in the paper.

| Notebook | Paper outputs |
|---|---|
| `01_descriptive_figures` | Descriptive figures. Figures 3, 4, 5, 6 and 8. The descriptive statistics in Tables 7 and 8 come from `02_main_regressions` |
| `02_main_regressions` | The main liquidity and solvency regressions. Tables 7 and 8, Tables 9 to 12 in Appendix F, Table 14 in Appendix H; Figures 7, 9, 10, 11, 17, 18 and 19 |
| `03_incremental_value_liquidity` | Table 2 and Figure 13, liquidity |
| `04_incremental_value_solvency` | Table 2 and Figure 13, solvency |
| `05_predictive_tests` | Table 13 in Appendix G, and the Clark–West comparisons in the note to Table 2 |
| `06_liquidation_rule_comparison` | Table 4, health-restoring against close-factor liquidation |
| `07_shock_size_robustness` | Figure 12 |
| `08_borrower_features_robustness` | Figure 16, robustness to borrower features |
| `09_random_forest_liquidity` | Figure 20, random-forest benchmark, liquidity |
| `10_random_forest_solvency` | Figure 21, random-forest benchmark, solvency |
| `11_simulated_vs_realized` | Appendix D. Figures 14 and 15, simulated against realized liquidations |
| `12_main_regressions_close_factor` | The specifications of `02_main_regressions` refitted to the close-factor simulation output. The two notebooks differ on three lines, all filenames |

Tables 1, 3, 5 and 6 are not produced by code. They are written directly in the
manuscript: the balance-sheet structure, the comparison of protocol designs, the node
feature definitions and the predictor list. Figures 1 and 2 are likewise drawn rather
than estimated.

---
## Simulation

The shock-propagation simulation that produces the liquidation*.csv files is available from the authors on request. It is not needed to reproduce the paper, since its output is among the deposited files.

## Requirements

Python 3.9. See `requirements.txt`.

## Repository layout

```
code/     analysis notebooks, outputs stripped
data/     analysis_panel.csv.gz, plus the deposited files once downloaded
paper/    manuscript and figures
```

Only `analysis_panel.csv.gz` is tracked in `data/`. The deposited files are ignored by
git, so they can be downloaded into the same folder without disturbing the repository.

## Data sources

Daily snapshots of Compound V2 from 1 January 2020 to 15 June 2024, from The Graph's
indexed subgraph of the Compound V2 contracts. The hosted subgraph was deprecated after
June 2024, following The Graph's migration to a decentralized network; by that point
Compound V2 activity was negligible. Section 4.1 of the paper gives the details.

## Citation

Tovanich, N., Kitzler, S., Makridis, C., Marcassa, S. and Prat, J. "Shock Propagation in
Decentralized Lending Networks: Evidence from the Compound Protocol." *Review of Finance*,
forthcoming.
