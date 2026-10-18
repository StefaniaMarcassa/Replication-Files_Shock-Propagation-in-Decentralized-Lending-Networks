# Shock Propagation in Decentralized Lending Networks: Evidence from the Compound Protocol

Replication code for the paper. Tovanich, Kitzler, Makridis, Marcassa and Prat.

The repository holds the code and one analysis-ready panel, about 17 MB in total. The full
simulation output, roughly 1 GB, is deposited separately because GitHub cannot host files
of that size.

**Data: `DOI_PLACEHOLDER`** (Zenodo). Replace this line with the DOI once the deposit is
published.

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

| Notebook | Paper outputs |
|---|---|
| `Regressions_REVISION` | The main liquidity and solvency regressions. Figures 7, 9, 10, 11, 17, 18 and 19; the model-comparison and coefficient tables in Appendix F |
| `Regressions_DesStats_REVISION` | Descriptive statistics. Figures 3, 4, 5, 6 and 8 |
| `incremental_liquidity_REVISION_new` | Table 2 and Figure 13, liquidity |
| `incremental_solvency_REVISION_new` | Table 2 and Figure 13, solvency |
| `incremental_liquidity_RF_REVISION` | Figure 20, random-forest benchmark, liquidity |
| `incremental_solvency_RF_REVISION` | Figure 21, random-forest benchmark, solvency |
| `DataVSSimul_REVISION` | Appendix D. Figures 14 and 15, simulated against realized liquidations |
| `Regressions_april29_B_all_size_shocks` | Figure 12 |
| `Regressions_REVISION_all_size_shocks_with_borrowers` | Figure 16, robustness to borrower features |
| `Robustness_old_vs_new` | **Table 4**, health-restoring against close-factor liquidation |
| `predictive_tests_STANDALONE` | The Clark–West comparisons in the note to Table 2 |

`Regressions_REVISION_liq_real.ipynb` is `Regressions_REVISION.ipynb` run on the
close-factor simulation output. The two differ on three lines, all filenames.

## Simulation code

`code/simulation/` contains the shock-propagation simulation that produces the liquidation
files. It is not needed to reproduce the paper from the analysis panel.

| Script | Produces |
|---|---|
| `liquidation.py` | Health-restoring liquidation, crypto pools |
| `liquidation2.py` | Health-restoring liquidation, ETH and WBTC jointly |
| `liquidation_real.py` | Close-factor liquidation |
| `liquidation_real_mul.py` | Close-factor liquidation with an intraday price multiplier |
| `statistics.py` | Network statistics, centralities and the user-level feature files |

All four liquidation scripts begin with `from debtrank import *`, which resolves to
`code/simulation/debtrank.py` in this repository.

---

## Requirements

Python 3.9. See `requirements.txt`. `networkit` and `pathos` are needed only by the
simulation scripts, not by the notebooks.

## Repository layout

```
code/              analysis notebooks, outputs stripped
code/simulation/   shock-propagation code and the debtrank module
data/              analysis_panel.csv.gz
paper/             manuscript and figures
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
