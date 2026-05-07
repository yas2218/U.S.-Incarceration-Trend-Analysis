# **Forensic Analysis: U.S. Incarceration Trends (1990–2015)**
## **Project Aim**
### The goal of this project is to perform a detailed longitudinal data analysis of incarceration rates in the United States between 1990 and 2015. Using the Tidy Tuesday "incarceration Trends" dataset, compiled by the Vera Institute of Justice, this analysis models how state and county-level prison populations changed per capita over a 25-year period. 
### Specifically, this study is designed to identify and statistically evaluate key "turning points" in the U.S. carceral trajectory, with a particular focus on the transition from the late 20th-century "tough on crime" sentencing era to the early 21st-century shift toward legislative reform and budgetary restructuring. 

## **Variable Construction and Data Logic**
### The raw dataset contains county-level demographic and confinement metrics over several decades. To prepare the data for statistical modeling, the following variables were constructed:
* **Temporal Window (year):** Filtered specifically to the years 1990 through 2015 to focus on the peak and subsequent decline of modern U.S. mass incarceration
* **Normalized Incarceration Rate (rate_per_100k):** Relying on raw prison population counts over time introduces a significant confound due to general population growth. To control for this, a normalized was constructed:

<img width="554" height="80" alt="Screenshot 2026-05-06 at 20 31 32" src="https://github.com/user-attachments/assets/b7556387-6597-433e-8987-6abbb793f9e2" />

  ### * The general population column, representing county residents, was used as the denominator, and the national sum was calculated per year to aggregate county-level data. 
### * **Missing Data Handling:** Variables containing missing values (NA) in the prison_population or population columns were handled dynamically within the aggregation function using na.rm = TRUE to avoid distorting the yearly national sums. 

## **Dependencies**
### To run this analysis, you must have R installed along with the following packages: 
### * tidyverse: a collection of core packages (readr, dplyr, ggplot2) used for data import, manipulation, and visualization.

## **How to Run the Analysis**
### * Save the script analysis.R to your local working directory
### * Launch RStudio and set your working directory to the folder containing the script
### * Run Sections 1 through 3 of the script. This will automatically stream the raw CSV data directly from the official TidyTuesday repository, filter the temporal window, handle missing values, and calculate the normalized incarceration rates.
### * Run Section 4 to fit and print the linear regression model.
### * Run Section 5 to render the ggplot visualization. The plot will display in your RStudio viewer and will automatically be exported to your directory as incarceration_trend_plot.png.

## Results and Statistical Modeling
### 1. Descriptive Statistics
### From 1990 to 2015, the aggregate dataset comprises over 1.3 million records tracking county-level trends across the United States. Aggregating these records nationally reveals:
  ### * **1990 Baseline Rate:** Approximately 288.1 prisoners per 100,000 residents.
  ### * **Peak Rate (2008):** Approximately 597.5 prisoners per 100,000 residents.
  ### * **2015 Post-Peak Rate:** Approximately 446.5 prisoners per 100,000 residents. 

### 2. Linear Regression Model
### A simple linear regression was conducted to model the overall trajectory of the normalized incarceration rate over time ("year" acting as the independent variable).
### Module Formula:
$$\text{rate\_per\_100k} = \beta_0 + \beta_1(\text{year})$$
### R Console Output:
<img width="568" height="325" alt="Screenshot 2026-05-06 at 20 06 39" src="https://github.com/user-attachments/assets/b532a76b-3a0e-40e5-bc3f-23f64ad2a35e" />

### Statistical Interpretation:
### + The overall linear model is highly statistically significant ($F(1, 24) = 47.18$, $p < .001$).
### + The temporal predictor (year) is a significant predictor of the incarceration rate ($\beta = 8.85$, $t(24) = 6.87$, $p < .001$). For every passing year, the U.S. incarcerated population increased by approximately 8.85 individuals per 100,000 residents. 
### + The model achieves a Multiple $R^2 = 0.6628$, indicating that time alone accounts for 66.3% of the variance in national incarceration rates over this 25-year span. 

## Visualization and Policy Discussion
### **Trend Visualization**
### Below is the generated trend line displaying the rise and fall of the U.S. incarceration rates: 
<img width="840" height="840" alt="US Incarceration Rates Linear" src="https://github.com/user-attachments/assets/01da7fc5-0d68-4534-b78f-2460936b26ee" />

### The 2008 Turning Point and Legal Context:
### While the linear model indicates a strong, positive upward trajectory over the entire 25-year period, the visualization reveals a clear non-linear trend. Incarceration rates rose sharply through the 1990s and early 2000s, peaking in 2008 at 597.5 per 100,000 before entering a steady, year-over-year decline.
### This peak and subsequent downturn correspond to several major national and state-level policy shifts:
### 1. **The Great Recession (2007-2009):** The severe economic downturn forced state legislatures to grapple with the immense budgetary strain of maintaining massive carceral systems. Fiscal conservatism led directly to bipartisan efforts to reduce prison populations to cut state spending. 
### 2. **Decriminalization and Sentencing Reforms:** The late 2000s marked a significant shift in legal and forensic psychology frameworks, with states increasingly moving away from mandatory minimum sentencing for non-violent offenses and expanding drug courts, mental health diversion programs, and community-based rehabilitation alternatives. 

### Data Limitations
### 1. **National Aggregation:** While aggregating county-level data to a national rate provides a clear view of macroscopic trends, it masks massive regional variations. Southern and rural jurisdictions often sustained high incarceration rates long after urban centers began implementing decarceration reforms. 
### 2. **Capacity Variables:** This model treats the general and prison populations uniformly; it does not account for jail capacity constraints, state-level policy differences, or variations in prosecutorial discretion across jurisdictions. 
