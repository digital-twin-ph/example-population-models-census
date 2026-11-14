# Population models beside a census

A Fieldwork worked example. Three gridded population estimates, **WorldPop**, **GRID3** and **GHS-POP**, are each
totalled over a country's census districts with **Sample a raster at points or over areas**, and set beside the 2022
census as each district's **share of the country**. Two countries: **Botswana** (28 census districts, large and sparsely
settled) and **Rwanda** (30 districts, small and dense).

| File | What it is |
| --- | --- |
| `fieldwork-project.json.gz` | The Fieldwork project: *Where does each source put Rwanda's people?* and *Where does each source put Botswana's people?* |
| `data/botswana_census_2022_districts.csv` | Botswana's 2022 census by district: the district as the census writes it, its name in the boundary file, its population. Statistics Botswana |
| `data/rwanda_census_2022_districts.csv` | Rwanda's 2022 census by district: its name and population. NISR |

## What it finds

| | Census 2022 | WorldPop 2025 | GRID3 2025 | GHS-POP 2025 |
| --- | --- | --- | --- | --- |
| Botswana, people | 2,359,609 | 2,541,726 | 2,541,726 | 2,764,784 |
| Largest district gap from the census share | | 0.02 points | 0.02 points | 4.09 points |
| Rwanda, people | 13,246,394 | 14,403,490 | 14,403,921 | 14,711,409 |
| Largest district gap from the census share | | 0.01 points | 0.01 points | 1.77 points |

**WorldPop's and GRID3's shares follow the census by construction.** Both spread projected census counts by district
over settlements, so at the census districts their shares are the census's own coming back. GRID3's grid is largely
WorldPop's. **GHS-POP is the independent comparison:** the JRC builds it another way, and it puts people differently.
A share is not a count, a model is not a census, and 2022 is not 2025.

**Side by side.** Each workflow ends in two maps of panels on one scale, so a shade is the same number in every panel:
the four sources' shares by district, two by two; and the three grids' cells in a row, as people per km² of each cell's
area, drawn at no more than 1,000 cells a side. Side by side shows where the sources differ; it does not say which is
right. Needs Fieldwork 0.113.0.

## Before opening it: the population files

The project carries where each raster came from, not its cells: a country's window from each source is hundreds of
megabytes. Download the four files below once, and keep them. Open the project, then in each **Raster input** choose the
file named there; it is checked against the digest of the file the example was built from before its window is read.
GHS-POP needs no download: its window is read from the JRC's copy, in parts, with **Read the window again**.

| Raster input | File | From | Bytes | sha256 |
| --- | --- | --- | --- | --- |
| Rwanda, WorldPop 2025 | `rwa_pop_2025_CN_100m_R2025A_v1.tif` | data.worldpop.org | 9,862,909 | `93bb39bb…580b` |
| Rwanda, GRID3 2025 | `rwa_SSApopulation_ 2025_v1_0_gridded.tif` | data.worldpop.org | 5,051,620 | `17fdb538…8693` |
| Botswana, WorldPop 2025 | `bwa_pop_2025_CN_100m_R2025A_v1.tif` | data.worldpop.org | 16,232,187 | `6d17fc52…8934` |
| Botswana, GRID3 2025 | `bwa_SSApopulation_ 2025_v1_0_gridded.tif` | data.worldpop.org | 11,647,427 | `65507d71…62a4` |

The full addresses and digests are in `provenance.json`.

## Checked

Every district's share from each source equals the share from rasterio's totals over the same files and boundaries
(`rasterio.mask`, cell centres inside), rounded as Fieldwork rounds: 120 for Rwanda, 112 for Botswana. Needs Fieldwork
0.111.0 or later.

Open `fieldwork-project.json.gz` in Fieldwork with **Import**.
