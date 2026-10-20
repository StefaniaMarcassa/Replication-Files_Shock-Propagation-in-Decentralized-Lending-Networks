# Shock Propagation in Decentralized Lending Networks: Evidence from the Compound Protocol

Replication code for the paper. Tovanich, Kitzler, Makridis, Marcassa and Prat.

The repository holds the code and one analysis-ready panel, about 17 MB in total. The full
simulation output, roughly 1 GB, is deposited separately because GitHub cannot host files
of that size.

**Data:** [https://doi.org/10.5281/zenodo.23456346](https://doi.org/10.5281/zenodo.23456346)

---

## Reproducing the paper

Every table and figure can be reproduced from `data/analysis_panel.csv.gz`, which ships
with this repository. You do not need the Zenodo deposit unless you want to rerun the
simulation or rebuild the panel.

```bash
git clone https://github.com/StefaniaMarcassa/Replication-Files_Shock-Propagation-in-Decentralized-Lending-Networks.git
cd Replication-Files_Shock-Propagation-in-Decentralized-Lending-Networks
pip install -r requirements.txt
jupyter lab
```

Then open any notebook in `code/` and run it top to bottom.

### The analysis panel

`data/analysis_panel.csv.gz` is 151,440 rows by 168 columns: the four analysis pools
(ETH, WBTC, DAI, USDC), daily from 1 January 2021 to 15 June 2024, at ten shock sizes and
three health thresholds. It is the merge of the simulation output and the feature files,
which the notebooks otherwise build in their first dozen cells.

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

### Rebuilding the panel from the raw simulation output

Download the Zenodo deposit into `data/`, then run `code/notebooks/Regressions_REVISION.ipynb`
from the top. Its first cells rebuild the panel from the eleven source files.

---

## What each notebook produces

They are independent of one another: each reads the analysis panel and can be run on its
own. The numbering follows the order in which the results appear in the paper.

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

## Simulation code

The shock-propagation simulation that produces the liquidation files is available from
the authors on request. It is not needed to reproduce the paper, since the analysis panel
already contains its output.

---

## Requirements

Python 3.9. See `requirements.txt`.

## Repository layout

```
code/     analysis notebooks, outputs stripped
data/     analysis_panel.csv.gz
paper/    manuscript and figures
```

`data/` is otherwise empty in git. The Zenodo files land there.

## Data sources

Daily snapshots of Compound V2 from 1 January 2020 to 15 June 2024, from The Graph's
indexed subgraph of the Compound V2 contracts. The hosted subgraph was deprecated after
June 2024, following The Graph's migration to a decentralized network; by that point
Compound V2 activity was negligible. Section 4.1 of the paper gives the details.

## Citation

Tovanich, N., Kitzler, S., Makridis, C., Marcassa, S. and Prat, J. "Shock Propagation in
Decentralized Lending Networks: Evidence from the Compound Protocol."
