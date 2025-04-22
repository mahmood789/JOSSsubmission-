
title: '786-MIII RR/OR app: An Interactive R Dashboard for Binary Outcome Meta-Analysis'
tags:
  - R
  - Shiny
  - meta-analysis
  - systematic review
  - evidence synthesis
  - binary outcomes
  - risk ratio
  - odds ratio
  - visualization
  - research software
authors:
  # List authors who meet JOSS contribution criteria
  - name: Mahmood Ahmad. MBBS
  - name: Abdullahi Noor, MBBS 
  - name: Parichatra Homhuan, MBBS
  - name: Manpreet Kour, MBBS

affiliations:
 - name: Royal Free Hospital, London, UK

date: 22 April 2025 
bibliography: paper.bib # Ensure this matches your BibTeX file name

---

# Summary

Meta-analysis of binary outcomes requires combining Risk Ratios (RR) or Odds Ratios (OR) across multiple studies - a process demanding significant methodological rigor and statistical expertise. We developed `MetaAnalysisApp`, an interactive dashboard using R [@RCoreTeam] and Shiny [@RShiny], to address these analytical challenges. Our application enables researchers to upload binary outcome data in CSV format and conduct comprehensive analyses through a graphical interface, eliminating the need for custom coding.

The dashboard supports calculation of pooled effect estimates using various methodological approaches, generation of publication-quality forest plots, assessment of publication bias through funnel plots and formal tests [@Egger1997], exploration of heterogeneity, and implementation of advanced techniques such as meta-regression and Bayesian analysis [@Simonsohn2014]. By integrating established R packages including `meta` [@metaPackage], `metafor` [@metaforPackage], `dmetar` [@dmetarPackage], and `bayesmeta` [@bayesmetaPackage], `MetaAnalysisApp` makes sophisticated meta-analytic methods accessible to researchers across disciplines, regardless of programming experience.

# Statement of Need

Meta-analysis represents an essential approach to evidence synthesis, yet conducting comprehensive analyses often presents substantial technical barriers. Despite the availability of powerful R packages, performing a thorough meta-analysis requires integrating multiple analytical components - model selection, diagnostics, bias assessment, and visualization - typically necessitating extensive programming expertise. This requirement creates significant obstacles for researchers seeking to rapidly explore analytical options or those with limited statistical programming experience.

Current graphical tools frequently lack comprehensive diagnostic capabilities or the methodological flexibility required for rigorous analysis. Our development of this app was for these reasons. 

1.A structured analytical workflow allowing researchers to progress from data upload through comprehensive analysis without writing code
2. Integrated methodological safeguardscombining primary analysis with essential assessments for publication bias and heterogeneity
3.Methodological flexibility enabling immediate visualization of how parameter modifications affect results and conclusions
4. Accessible advanced methods including meta-regression, subgroup analysis, and Bayesian approaches through a consistent interface

Through this integration of methods, `MetaAnalysisApp` supports more methodologically robust meta-analyses while simultaneously serving educational purposes for those learning evidence synthesis techniques.

# Functionality

`MetaAnalysisApp` guides users through a structured meta-analytic process using a dashboard built with `bs4Dash` [@bs4Dash].

**Implementation:**

The workflow begins with data importation via CSV upload, containing at minimum event counts and sample sizes for experimental and control groups, along with study identifiers. Optional fields include publication year, subgroup classification, and regression moderators. Users then select methodological parameters including:

* Effect measure (RR or OR)
* Statistical model (Fixed Effect or Random Effects)
* Combination method (Mantel-Haenszel [@MantelHaenszel], Inverse Variance, etc.)
* Between-study variance estimator (REML, Paule-Mandel [@PauleMandel], etc.)

Results are presented across several methodologically focused sections:

* **Meta-Analysis Results:** Provides numerical output from `meta::metabin` [@metaPackage], including pooled effect estimates with confidence intervals, heterogeneity metrics ($I^2$, $\tau^2$), Q-test results, and study-level data. Complementary output from `metafor::rma` [@metaforPackage] offers methodological triangulation.

* **Forest Plots:** Presents the primary meta-analytic visualization via `meta::forest`, with customizable formatting options (standard, JAMA, or RevMan5 styles). Alternative visualizations include Drapery plots for uncertainty distributions, Radial plots for detecting asymmetry, L'Abbé plots comparing event rates, and Beeswarm plots (`ggbeeswarm` [@ggbeeswarm]) showing effect distribution patterns.

* **Publication Bias:** Implements multiple bias assessment approaches: standard and contour-enhanced funnel plots (`meta::funnel`), trim-and-fill analysis (`meta::trimfill`), limit meta-analysis (`meta::limitmeta`), P-curve analysis (`dmetar::pcurve`), and formal statistical tests (Egger's regression and Begg's rank correlation via `meta::metabias` [@Begg1994]). The section includes Albatross plots [@Schwarzer2023Albatross] visualizing sample size versus p-value relationships to identify small-study effects.

* **Heterogeneity:** Presents key heterogeneity statistics with visual diagnostics from `dmetar::InfluenceAnalysis` [@dmetarPackage]. Baujat plots [@Baujat2002] identify studies contributing disproportionately to heterogeneity or overall effect, while leave-one-out analyses demonstrate result sensitivity to individual studies.

* **Meta-Regression:** For datasets containing moderator variables, this section explores their relationship with effect size variation using `meta::metareg`. The interface displays models with up to three moderators, accompanying bubble plots (`meta::bubble`), and multicollinearity diagnostics (`PerformanceAnalytics` [@PerformanceAnalytics]).

* **Bayesian Meta-Analysis:** Provides alternative estimation using `bayesmeta::bayesmeta` [@bayesmetaPackage], displaying posterior distributions and credible intervals for both pooled effect and heterogeneity parameters.

* **Advanced Analysis:** Contains specialized analytical approaches including cumulative meta-analysis (`meta::metacum`), subgroup analysis (`meta::metabin` with `byvar`), and influence analysis (`meta::metainf`).

Throughout the application, results can be exported as publication-ready figures (PNG format) or numerical summaries (text files) for reporting purposes.

# Availability

**Operating system:** Platform independent (requires R installation)

**Programming language:** R (≥ 4.0 recommended)

**Dependencies:** shiny, bs4Dash, meta, dmetar, metafor, ggplot2, ggbeeswarm, fontawesome, shinyjs, dplyr, magrittr, bayesmeta, PerformanceAnalytics. *(Optional: car)*

**Installation & Reproducibility:** The project includes an `renv.lock` file for environment reproducibility via `renv::restore()` [@renv]. Comprehensive installation instructions are provided in the repository documentation.

**License:** Apache License 2.0. *(Confirm this is the license used in LICENSE.md)*

**Source Code Repository:** [Link to Your GitHub/GitLab Repository, e.g., https://github.com/your_username/MetaAnalysisApp]

**Archived Version:** [Link to Zenodo/Figshare DOI - Add upon JOSS acceptance]

# Acknowledgements

We thank the Ahmadiyya Muslim Research Association and Luciano Candilio for their support. [Add any other necessary acknowledgements].

# References

*(References should be listed in the `paper.bib` file in BibTeX format. Ensure entries exist for all cited packages [@RCoreTeam; @RShiny; @metaPackage; @metaforPackage; @dmetarPackage; @bayesmetaPackage; @bs4Dash; @ggplot2; @ggbeeswarm; @PerformanceAnalytics; @renv] and methods [@MantelHaenszel; @Peto; @PauleMandel; @DerSimonianLaird; @Egger1997; @Begg1994; @Simonsohn2014; @Baujat2002; @Schwarzer2023Albatross])*
