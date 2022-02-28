# Complex sample survey analysis in R: NSDUH tutorial

## Information and instructions to prepare for this tutorial
To complete this tutorial, you will need to complete the following steps:
1. Install R and R Studio
2. Download and save the tutorial materials
3. Install the survey, svydiags, tidyverse, naniar, stats, and jtools packages (if you do not already have them)

Follow the instructions below to install and download everything you will need.

### Install R and R Studio
R is the software and R Studio is the IDE (Interactive Development Environment) that makes R easier to use. Install R before you install R Studio because R Studio will look for R during installation.

**If you don't already have it, download and install R:**
+ Click the download R link on the [R Project for Statistical Computing](https://www.r-project.org/) website
+ Choose any one of the options from the [CRAN Mirrors](https://cran.r-project.org/mirrors.html) list
+ Click on the download that is appropriate for your operating system, Linux, Mac, or Windows; if you are not given this option, go back to the [CRAN Mirrors](https://cran.r-project.org/mirrors.html) and try a different one.
+ Find the link for install R for the first time and click on it
+ Click on the the Download R link on the page that opens
+ Use the installer that downloads to install R

**Download and install R Studio:**
+ Go to the [R Studio downloads](https://www.rstudio.com/products/rstudio/download/) page
+ Click on the DOWNLOAD button under the RStudio Desktop column on the downloads page
+ Choose the download for the operating system you have and click on it
+ Use the installer that downloads to install R Studio

### Download and save the tutorial materials
+ Download the participant files and save them together in the same folder on your computer:
+ Click on the green Code button toward the top of this GitHub page
Choose Download ZIP
+ Unzip the downloaded zip file and save all the files in a single folder on your computer

### Install the survey, svydiags, tidyverse, naniar, stats, and jtools packages**

Open RStudio and follow these instructions:
+ Click on the Tools menu
+ Type survey, svydiags, tidyverse, naniar, stats, and jtools into the dialog box that opens
+ Click install (R will do stuff for a while, this might look like errors but is fine)

## **Background and purpose of this tutorial**

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
4. T-tests and design-based Wald (chi-square) tests of independence
5. Regression analysis using `svyglm` 
6. Regression diagnositics using the `svydiags` package (**under construction!**)

Note: A useful resource for analyzing complex sample data in R is available [here](http://asdfree.com/national-study-on-drug-use-and-health-nsduh.html).
