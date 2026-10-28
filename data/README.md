# Data

The notebooks in `code/` read their inputs from this folder (`DATA_PATH = '../data/'`).
Download the eleven files below from the Dataverse deposit and place them here:

**[https://doi.org/10.5281/zenodo.23456346]**

Nothing in `code/` runs without them.

| File | Read by |
|---|---|
| `liquidation.csv` | `01` to `10` |
| `liquidation_pools.csv` | `01` to `10` |
| `pool_statistics_with_cf.csv` | `01` to `10`, `12` |
| `pool_centralities.csv` | `01` to `10`, `12` |
| `network_statistics.csv` | `01` to `10`, `12` |
| `shockAsset_lenders_borrowers_new.csv` | `01` to `10`, `12` |
| `shockAsset_collateral_filtered.csv` | `01` to `10`, `12` |
| `liquidation_real.csv` | `06`, `12` |
| `liquidation_pools_real.csv` | `06`, `12` |
| `liquidation_pools_real_mul.csv` | `11` |
| `financialDailySnapshots.csv` | `11` |

The `_real` files hold the close-factor simulation output, which `06` compares against the
health-restoring rule and `12` refits the main specifications to.

`analysis_panel.csv.gz` is tracked in this repository and is not part of the deposit. It is
the merged panel, provided for inspection. No notebook reads it; see the main README.
