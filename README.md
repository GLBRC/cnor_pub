# cnor_pub

## Description
This repository includes the experimental data collected for the reduction of NO to N<sub>2</sub>O by purified *Paracoccus denitrificans* cytochrome *c* nitric oxide reductase (cNOR) and the R code used to analyze these data.
## Getting started

To clone the remote repository to your local drive and create a new directory on your local drive at the same time:

- Go to the parent directory where you want to put this repository:

    ```
    cd parent_directory
    ```
- Clone this remote repo into a new sub-directory and navigate to that sub-directory.
    - For GitHub (non-GLBRC) users:
    ```
    git clone https://github.com/GLBRC/cnor_pub
    cd cnor_pub
    ```
    - For GLBRC users:
    ```
    git clone https://gitpub.wei.wisc.edu/rivettel/cnor_pub.git
    cd cnor_pub
    ```
Cloning the repository will create three sub-directories under `cnor_pub`:
- `code` includes markdown (.qmd) files with code written in R
    - `exp_cNOR_pub` - code for analyzing the experimental isotopic (GC-IRMS) data presented in the main text
    - `controls_cNOR_pub` - code for analyzing the control GC-ECD and GC-IRMS data
- `data` includes: experimental data (.csv files) under `input`, and `output` (initially empty)
- `graphs` (initially empty)

Running the code will create additional files that will be stored in these sub-directories. To write files properly, the package `here` has to be loaded in `cnor_pub`.

## Data
### exp_cNOR_pub
- cNOR_all_raw.csv
    - All isotopic data from the first set of experiments
    - Includes data collected after N<sub>2</sub>O production plateaued
- cNOR_raw.csv
    - The isotopic data presented in the main text and used to determine KIEs (Figures 1-3, Table 1, Figures S5-6, Table S1)
    - Excludes data collected after N<sub>2</sub>O production plateaued
    - Note that this file can also be generated using cNOR_all_raw.csv as input and running the `controls_cNOR_pub` code.

### controls_cNOR_pub
- no_enzyme_GC-ECD.csv
    - GC-ECD data for no-enzyme negative controls (Figure S7)
- controls_all.csv
    - All isotopic data from the second set of experiments (N<sub>2</sub>O production measured in the presence or absence of H<sub>2</sub><sup>18</sup>O-enriched water)
    - Includes data where *f* is greater than or equal to 0.9
    - Includes data collected after N<sub>2</sub>O production plateaued
    - Includes outliers
- controls.csv
    - The isotopic data from the second set of experiments presented in Figures S1-4 and Table S2 (N<sub>2</sub>O production measured in the presence or absence of H<sub>2</sub><sup>18</sup>O-enriched water)
    - Excludes data where *f* is greater than or equal to 0.9
    - Excludes data collected after N<sub>2</sub>O production plateaued
    - Excludes outliers identified with Grubbs' test
    - Note that this file can also be generated using controls_all.csv as input and running the `exp_cNOR_pub` code.
## General outline for analyzing experimental data
- Load packages
- Load data
- Calculate additional values needed for analysis
- Remove observations
    - Where *f* is greater than or equal to 0.9
    - After N<sub>2</sub>O production plateaued
- Combine (pool) data from all replicates
- Apply standard Rayleigh model to bulk N
    - Perform Grubbs' test for outliers
    - Remove outlier and reapply standard Rayleigh model if necessary
- Plot data
- Apply Expanded Rayleigh model to determine KIE_alpha and KIE_beta
- Combine results in summary table(s)
 - Bootstrapping (if needed)
## Authors
Elise Rivett
## References
Grubbs, F. E. (1950) Sample criteria for testing outlying observations, *Ann Math Stat 21*, 27-58.

Komsta, L. (2006) Processing data for outliers, *R News 6*, 10-13.

Rivett, E. D., Ma, W., Ostrom, N. E., and Hegg, E. L. (2024) Position-specific kinetic isotope effects for nitrous oxide: a new expansion of the Rayleigh model, *Biogeosciences 21*, 4549-4567.

