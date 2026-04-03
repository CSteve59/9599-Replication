# Replication: "Liberals Lecture, Conservatives Communicate"

**Author:** Colton Stevenson
**Course:** P.S. 9599 – Text Analysis
**Date:** March 2026

## Paper

Schoonvelde, M., Brosius, A., & van Atteveldt, W. (2019). Liberals lecture, conservatives communicate: Analyzing complexity and ideology in 381,609 political speeches. *PLOS ONE*, 14(2), e0208450. https://doi.org/10.1371/journal.pone.0208450

## Summary

This repository contains a replication of Schoonvelde et al. (2019), which examines whether culturally liberal politicians use more complex language than conservatives across European parliaments, EU institutions, and party congresses. The original study finds that conservative cultural ideology predicts simpler speech in 7 of 8 corpora, that economic left-right ideology has no systematic effect, and that speech complexity has been declining over time.

This replication starts from the publicly available raw datasets (rather than the authors' pre-cleaned data) and independently reproduces the full cleaning pipeline, ideology scoring, complexity measurement, and statistical analyses.

## Repository Structure

```
.
├── README.md
├── code/
│   ├── cleaning.Rmd        # Data cleaning pipeline (raw -> analysis-ready)
│   └── analyses.Rmd        # Descriptive statistics, figures, and OLS regressions
├── data/
│   ├── raw/                 # Original public datasets (see Data Sources below)
│   │   ├── ParlSpeech/
│   │   ├── EUSpeech/
│   │   ├── PartyCongressSpeech/
│   │   └── ManifestoProject/
│   └── cleaned/             # Analysis-ready .RData file (produced by cleaning.Rmd)
├── figures/                 # Replicated figures (PNG)
│   ├── cole-fig-1.png
│   ├── cole-fig-2.png
│   ├── cole-fig-3.png
│   └── cole-fig-4.png
├── Presentation.pdf         # PDF version of presentation I gave in class
└── Replication Report.pdf   # Five Page Report on Replication
```

## How to Run

The `data/` folder is not included in this repository due to file size constraints. Before running any code, you'll need to get the data using one of the three options below. Then install the required R packages and run the notebooks in order.

### Step 1 — Get the Data

**Option A: Download raw files from original sources**

Download each dataset individually from the sources listed in the [Data Sources](#data-sources) section below and organize them into the following structure within the project root:

```
data/
├── raw/
│   ├── ParlSpeech/
│   ├── EUSpeech/
│   ├── PartyCongressSpeech/
│   └── ManifestoProject/
└── cleaned/             # will be created automatically in Step 3
```

Note that the Manifesto Project data requires free registration at manifesto-project.wzb.eu. Once the raw data is in place, proceed to Step 2 and run both notebooks (cleaning first, then analyses).

---

**Option B: Download pre-packaged files from Harvard Dataverse** (This isn't working download from google drive link)

A single archive containing all data and code for this replication is available at: `[HARVARD LINK]`

- **Full archive** — Includes the raw data, cleaned data, and all code. Download and extract into the project root, then skip directly to Step 3 (analyses only) or re-run everything from Step 3 (cleaning + analyses).
- **Data only** — Includes raw and cleaned datasets. Place this in the project repository beside the other folders (besides "code" and "figures" folders).

- Google Drive Link (Full Archive): https://drive.google.com/file/d/1l-5NgzgLvXx72KM8OhnNAsQVmNP1olGX/view?usp=drive_link
---

### Step 2 — Install R Packages

The following packages are required:

```r
install.packages(c(
  "tidyverse", "tidylog", "tidytext", "textdata",
  "quanteda", "quanteda.textstats", "wesanderson",
  "knitr", "stringr", "readxl", "cld2",
  "DAMisc", "broom", "patchwork", "stargazer"
))
```

### Step 3 — Run the Notebooks

Both notebooks use relative paths from the project root. Open them in RStudio and they will set the working directory automatically.

- **`code/cleaning.Rmd`** — Run this first if you are starting from raw data (Options A or B full archive). It processes the raw files and saves the cleaned dataset to `data/cleaned/cole_final_cleaned_data.RData`. Note: this takes approximately 37 minutes on the full dataset due to the size of ParlSpeech (~700k speeches) and requires at least 32 GB of RAM.

- **`code/analyses.Rmd`** — Run this second (or first, if you used the data-only download). It loads the cleaned dataset and produces all descriptive statistics, figures, and regression tables.

## Data Sources

The raw data is publicly available from the following sources:

| Dataset | Source | DOI |
|---------|--------|-----|
| ParlSpeech | Harvard Dataverse | https://doi.org/10.7910/DVN/E4RSP9 |
| EUSpeech (V4, unstemmed) | Harvard Dataverse | https://doi.org/10.7910/DVN/GKABNU |
| Party Congress Speeches | Harvard Dataverse | https://doi.org/10.7910/DVN/SFZI8O |
| Manifesto Project (2019) | manifesto-project.wzb.eu | Registration required |

**Note:** The EUSpeech DOI cited in the original paper (DVN/XPCVEI) links to a 2016 version with only stemmed/cleaned text. The V4 unstemmed corpus (DVN/GKABNU) is required for accurate Flesch-Kincaid scoring.

## Key Differences from Original

- **Observation counts differ**, especially for ParlSpeech (higher N in replication). The authors did not share their cleaning code, so some filtering decisions had to be inferred from the paper.
- **Main findings replicate**: conservative cultural ideology predicts simpler speech in 7/8 corpora (Great Britain is the exception in this replication, likely due to observation differences), no systematic economic left-right effect, declining complexity over time, and party fixed effects confirm the within-party relationship.
- **Coefficient magnitudes differ** from the original, but directions and significance levels are largely consistent.

## LLM Disclosure

An LLM (Claude) was used to assist with two specific data compilation tasks:
1. Researching and compiling party affiliations for ~60 EUSpeech speakers (the raw data does not include party information).
2. Compiling the governing coalition lookup table (which parties were in government during which periods).
