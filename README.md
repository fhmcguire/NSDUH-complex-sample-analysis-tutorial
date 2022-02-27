# NSDUH-complex-sample-analysis-tutorial
## **Background and Purpose**

The purpose of this tutorial is to provide brief introduction to conducting design-based analysis of complex sample survey data using the `survey` package in `R`.

We will be using data from the **National Survey on Drug Use and Health (NSDUH)**. NSDUH is a repeated cross-sectional household survey distributed annually to a sample of non-institutionalized residents of the United States. Its primary aim is to monitor drug and alcohol use by providing nationally-representative estimates of substance use behaviors, mental health status, and correlates of these health outcomes/behaviors. Additional information on NSDUH can be found [here](https://nsduhweb.rti.org/respweb/about_nsduh.html).

To improve estimate precision and reduce overall survey costs, households (and specific individuals within households) who participate in NSDUH are selected through a complex set of **cluster and stratified sampling** procedures. Certain population subgroups (including younger people, Hispanic people, Black/African-American people) are also **oversampled relative to their general population size** to produce more reliable estimates (i.e., through standard error reduction). This ultimately generates a sample in which there is **unequal probability of selection** across sampling units, and produces somewhat homogeneous samples within clusters due to shared community characteristics (i.e., **nonindependence**). Together, these violate simple random sample assumptions (equal probability of selection, independence of observations) common across basic statistical procedures. 

**In order to generate accurate nationally-representative estimates (e.g., proportions, means, standard errors) from complex sample survey data, we have to conduct design-based analysis** (i.e., analysis that adjusts for unequal probability of selection). For more information on NSDUH sample design can be found in the [NSDUH 2019 Sample Design Report](https://www.samhsa.gov/data/sites/default/files/reports/rpt34664/NSDUHmrbSampleDesign2019.pdf). Guidance for statistical analysis can be found in the [NSDUH 2019 Statistical Inference Report](https://www.samhsa.gov/data/sites/default/files/reports/rpt34666/NSDUHmrbStatInference2019.pdf).

### Data frame information: NSDUH 2015-2019

The data frame included in this tutorial (`nsduh_20152019_subset.RData`) includes 5 combined waves (2015, 2016, 2017, 2018, 2019) and a subset of 15 variables to reduce the overall file size.

**Combining waves**: To increase the sample size of relatively small population subgroups, it is common practice in public health research to combine multiple waves from national cross-sectional datasets like NSDUH. However, additional procedures are needed to adjust sampling weights, and these simple steps are outlined in this tutorial.

**Unconditional analysis of a subpopulation**: In addition, researchers are often interested in studying a specific subpopulation (e.g., adolescents). Here, it is neccessary to identify the subpopulation within the overall dataset for the analysis at hand. **Avoid dropping unused observations as this removes key information used to generate variance estimates.** Additional background information on subpopulation analysis can be found in [West, Berglund, & Herringa, 2008](https://journals.sagepub.com/doi/pdf/10.1177/1536867X0800800404) and in [Lumley, 2021](https://cran.r-project.org/web/packages/survey/vignettes/domain.pdf).

### Key issues and procedures covered
1. Load the data frame and identify a subpopulation of interest
2. Setup design-based analysis using `svydesign`
3. Descriptive statistics using `svymean`, `svyby`, and `svyciprop`
4. T-tests, correlations, and design-based Wald (chi-square) tests of independence
5. Regression analysis using `svyglm` 
6. Regression diagnositics using the `svydiags` package (**under construction!**)

Note: A useful resource for analyzing complex sample data in R is available [here](http://asdfree.com/national-study-on-drug-use-and-health-nsduh.html).
