# MetaAnalysisApp: Meta-Analysis Dashboard for Binary Outcomes

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE.md)
**An Interactive R Shiny Application for Meta-Analysis of Binary Data (Risk Ratios & Odds Ratios)**

## Overview

This application provides a comprehensive, interactive dashboard for conducting meta-analyses focusing on binary outcome data (e.g., event counts in intervention vs. control groups). Users can upload their study data in CSV format and perform a wide range of analyses, including:

* Calculating pooled effect sizes (Risk Ratio or Odds Ratio) using various methods.
* Generating publication-quality forest plots (Standard, JAMA, RevMan5 styles).
* Assessing publication bias through funnel plots and statistical tests (Egger's, P-curve, Limit Meta-Analysis).
* Evaluating heterogeneity using statistical measures and plots (Baujat, Influence, I², Radial, Drapery, L'Abbé).
* Performing meta-regression to explore sources of heterogeneity.
* Conducting subgroup and cumulative meta-analyses.
* Running sensitivity analyses (Leave-One-Out).
* Performing Bayesian meta-analysis.

The tool aims to make advanced meta-analysis techniques accessible through a user-friendly graphical interface, powered by the R packages `shiny`, `bs4Dash`, `meta`, `metafor`, `dmetar`, and `bayesmeta`.

## Features

* **Data Import:** Upload study data via CSV file.
* **Effect Measures:** Choose between Risk Ratio (RR) and Odds Ratio (OR).
* **Analysis Methods:** Select from various combination methods (Inverse Variance, Mantel-Haenszel, Peto, GLMM, SSW) and heterogeneity estimators (PM, DL, REML, EB, SJ).
* **Model Choice:** Fixed Effect or Random Effects models.
* **Forest Plots:**
    * Standard forest plot with prediction interval.
    * JAMA-style forest plot.
    * RevMan5-style forest plot.
    * Customizable appearance (colors, labels, text size).
* **Publication Bias Assessment:**
    * Standard and contour-enhanced funnel plots.
    * Trim and Fill analysis and plot.
    * Limit Meta-Analysis (standard and shrunken) plots.
    * Egger's regression test (output).
    * P-curve analysis and plot.
* **Heterogeneity Analysis:**
    * Text summary ($I^2$, $\tau^2$, Q-statistic).
    * Baujat plot.
    * Influence diagnostics plots (Influence, Effect Size change, I² change).
    * Radial plot, Drapery plot, L'Abbé plot.
* **Meta-Regression:**
    * Perform meta-regression with up to three continuous moderator variables (columns named `Reg`, `Reg2`, `Reg3`).
    * Bubble plots for visualizing moderator effects.
    * Correlation plots (via `PerformanceAnalytics`).
    * Diagnostic outputs (Residuals, Correlation Matrix, AIC/BIC).
* **Advanced Analyses:**
    * Cumulative meta-analysis (requires `year` column).
    * Subgroup analysis (requires `subgroup` column).
    * Leave-One-Out sensitivity analysis.
    * Bayesian meta-analysis (using `bayesmeta`).
* **Visualization & Export:**
    * Interactive plots within the dashboard.
    * Download options for all generated plots (PNG format) and analysis results (TXT format).

## Installation

**Prerequisites:**

* R (version 4.0 or later recommended).
* RStudio (Recommended IDE, but not strictly required).

**Steps:**

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/mahmood789/JOSSsubmission-)
    cd your_repository_name
  
https://github.com/mahmood789/JOSSsubmission-

2.  **Install Dependencies:**
    This project uses `renv` for package management to ensure reproducibility.

    * Open the project in RStudio or navigate to the project directory in your R console.
    * Run the following command in the R console to install all required packages from the `renv.lock` file (if provided):
        ```R
        renv::restore()
        ```
    * **Note:** The Bayesian analysis tab requires the `bayesmeta` package. While `renv` should handle this, if you encounter issues specifically with Bayesian analysis, you might need to install it manually: `install.packages("bayesmeta")`. The meta-regression correlation plot requires `PerformanceAnalytics`, and VIF calculation requires `car`. If `renv` is not used, ensure all packages listed in the `library()` calls at the top of `app.R` are installed.

    *(Alternative if not using `renv`:)*
    * *(Ensure you have the `remotes` package: `install.packages("remotes")`)*
    * *(Install dependencies from the DESCRIPTION file (if provided): `remotes::install_deps(dependencies = TRUE)`)*
    * *(Or manually install packages listed in the `library()` calls at the top of `app.R`)*

## Usage

1.  **Launch the Application:**
    Open R/RStudio in the project directory and run:
    ```R
    shiny::runApp()
    ```
    This will launch the Meta-Analysis Dashboard in your default web browser.

2.  **Prepare Input Data:**
    * Create a CSV file containing your study data.
    * **Required Columns:**
        * `eventintervention`: Number of events in the intervention/exposure group.
        * `totalintervention`: Total number of participants in the intervention/exposure group.
        * `eventcontrol`: Number of events in the control group.
        * `totalcontrol`: Total number of participants in the control group.
        * `author`: Unique identifier for each study (e.g., FirstAuthorYYYY).
    * **Optional Columns:**
        * `year`: Year of publication (numeric, for cumulative meta-analysis).
        * `Reg`, `Reg2`, `Reg3`: Continuous moderator variables for meta-regression.
        * `subgroup`: Categorical variable defining subgroups for subgroup analysis.
    * *(See `sample_data.csv` in this repository for an example)*

3.  **Upload Data & Set Options:**
    * Navigate to the "Introduction & Data Import" tab.
    * Click "Browse" to upload your prepared CSV file.
    * Select the desired "Effect Measure" (RR or OR).
    * Choose the "Combination Method", "Heterogeneity Method", and "Effect Model" appropriate for your analysis.
    * Select a moderator for the Bubble Plot if performing meta-regression.

4.  **Explore Results:**
    * Use the sidebar menu to navigate through different analysis tabs (Meta-Analysis Results, Forest Plots, Publication Bias, Heterogeneity, etc.).
    * View generated plots and statistical outputs.
    * Use the download buttons within each section to save plots (PNG) and text results (TXT).

## Sample Data

A sample CSV file (`sample_data.csv`) is included in this repository to demonstrate the required data format and allow testing of the application's features.

## Testing

*(This section assumes automated tests using `testthat` and `shinytest2` will be implemented for JOSS submission)*

Automated tests are included to verify core functionality. To run the tests:

1.  Ensure you have installed the necessary testing packages (e.g., `testthat`, `shinytest2`). These should be included in the `renv.lock` file or listed as suggested packages in the `DESCRIPTION` file.
2.  Open R in the project directory.
3.  Run the following command:
    ```R
    # If using testthat directly for non-reactive parts:
    # testthat::test_dir("tests/testthat")

    # If using shinytest2 for application testing:
    # shinytest2::test_app()
    ```
    *(Modify the commands above based on your specific testing setup and directory structure, e.g., tests might be in a `tests/` folder)*

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to the [repository issue tracker](https://github.com/your_username/your_repository_name/issues).

*(Optional: See `CONTRIBUTING.md` for more details. Create this file if you have specific guidelines.)*

## Authors

* Mahmood Ahmad, MBBS
* Abdullahi Noot, MBBS
* Parichatra Homhuan, MBBS
* Manpreet Kour, MBBS


## Acknowledgements

We acknowledge the support and encouragement from the Ahmadiyya Muslim Research Association and Luciano Candilio.

## License

This project is licensed under the Apache License, Version 2.0 - see the [LICENSE.md](LICENSE.md) file for details. *(Ensure LICENSE.md exists and contains the Apache 2.0 text)*

## Citation

If you use this software, please cite it as follows:

> Ahmad M., Noot A., Homhuan P., Kour M. (2025). MetaAnalysisApp: An Interactive R Shiny Dashboard for Binary Outcome Meta-Analysis. *Journal of Open Source Software*, [Volume]([Issue]), [ArticleNumber]. [https://doi.org/[JOSS_DOI]]()

*(Replace [Volume], [Issue], [ArticleNumber], and the DOI with the actual details upon publication by JOSS)*

We have cited the underlying R packages used for the analysis, particularly `meta` [@metaPackage], `metafor` [@metaforPackage], `dmetar` [@dmetarPackage], and `bayesmeta` [@bayesmetaPackage], as appropriate for the analyses performed. Refer to the documentation of these packages for their preferred citation formats (e.g., using `citation("meta")` in R).
