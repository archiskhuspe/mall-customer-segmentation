# Mall Customer Segmentation

![R](https://img.shields.io/badge/R-4.0%2B-276DC3?logo=r)
![License](https://img.shields.io/badge/license-MIT-green)

An R script that segments mall customers into distinct groups using K-means clustering on Age, Annual Income, and Spending Score. The optimal number of clusters is determined by three independent methods — elbow, silhouette, and gap statistic — and results are visualised with ggplot2 scatter plots and a PCA cluster plot.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [How It Works](#how-it-works)
- [Dataset](#dataset)
- [Prerequisites](#prerequisites)
- [Installation & Usage](#installation--usage)
- [Project Structure](#project-structure)
- [Limitations](#limitations)
- [License](#license)

## Features

- Exploratory data analysis: descriptive statistics and distributions for Age, Annual Income, and Spending Score
- Gender breakdown via bar chart and 3D pie chart
- K-means clustering with Lloyd's algorithm across k = 2–10
- Cluster count selection via elbow method, silhouette analysis, and gap statistic
- Final 6-cluster model with ggplot2 scatter plots (Income vs Score, Score vs Age)
- PCA dimensionality reduction for a 2-D cluster overview

## Tech Stack

- **Language:** R 4.0+
- **Clustering:** `cluster` (silhouette), `NbClust`, `factoextra` (fviz helpers)
- **Visualisation:** `ggplot2`, `plotrix` (pie3D), base R graphics
- **Utilities:** `purrr` (map_dbl for elbow curve)

## How It Works

1. **EDA (sections 1–5):** Load the dataset, print structure and summaries, plot histograms, boxplots, and a density plot for each numeric feature; visualise gender distribution.
2. **Elbow method (section 6):** Compute total within-cluster sum of squares for k = 1–10 and plot the elbow curve.
3. **Silhouette analysis (sections 7–7.9):** Fit K-means for k = 2–10, plot individual silhouette widths, and use `fviz_nbclust` to identify the optimal k.
4. **Gap statistic (section 8):** Confirm the optimal k via `clusGap` + `fviz_gap_stat`.
5. **Final model (sections 8.1–8.5):** Fit k = 6, run PCA for visualisation, and plot cluster membership on two 2-D scatter plots and a PCA biplot.

## Dataset

`mall_customers.csv` — 200 rows, 5 columns: `CustomerID`, `Gender`, `Age`, `Annual.Income..k..` (in $k), `Spending.Score..1.100.` (1–100 scale).

This is the public [Mall Customers dataset](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python) from Kaggle.

## Prerequisites

- R 4.0 or later
- The following R packages:

```r
install.packages(c("plotrix", "purrr", "cluster", "ggplot2",
                   "NbClust", "factoextra"))
```

## Installation & Usage

```bash
# Clone the repo
git clone https://github.com/archiskhuspe/mall-customer-segmentation.git
cd mall-customer-segmentation
```

Open `mall_customer_segmentation.R` in RStudio (or set your working directory to the repo root) and run the script section by section, or source it all at once:

```r
source("mall_customer_segmentation.R")
```

> **Note:** The script uses `read.csv("mall_customers.csv")` with a relative path. Make sure your R working directory is the repo root before running (`setwd("<path-to-repo>")`).

## Project Structure

```
mall-customer-segmentation/
├── mall_customer_segmentation.R   # Main analysis script
├── mall_customers.csv             # Input dataset (200 customers)
├── literature_survey.docx         # Survey of related research papers
├── .gitignore
├── LICENSE
└── README.md
```

## Limitations

- The dataset is the public Kaggle Mall Customers dataset; data was not collected independently.
- Only three numeric features (Age, Annual Income, Spending Score) are used for clustering; Gender is excluded.
- K-means requires specifying k in advance. The optimal k = 6 is supported by elbow, silhouette, and gap statistic heuristics but is not a guaranteed global optimum.
- No ground-truth cluster labels exist; quality is assessed by internal indices only.
- Features are not scaled before clustering, so Annual Income (range 15–137) dominates the distance metric over Age (range 18–70) and Spending Score (range 1–99).
- PCA is used only for 2-D visualisation; the clustering itself runs on the original three features.

## License

Released under the [MIT License](LICENSE).
