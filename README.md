# What industry factors are important in predicting salaries for data related jobs?
### Aim
We wanted to understand which industry factors are most important in predicting the salary amounts for data related jobs. Only focused on data related jobs in the UK (e.g. data scientist, data analyst, business intelligence). 

Once the data was collected, cleaned and feature engineered we built a predictive model with salary being the target variable. Several models were validated to identify the best performer we then evaluated the chosen model to understand the most important predictors for salary.

### Acquiring the date

The job data was acquired by scraping www.indeed.co.uk using BeautifulSoup. Searches were performed on different data related job titles for key cities in the United Kingdom. For each job listing the following components were collected :
- Job title
- Company
- Salary
- Location

## Data cleaning
Many job listings did not contain salary information and these were removed along with any duplicates. The remaining listings were cleaned to extract useful information for our analysis. For example:

**Job type** - The scraped listings had included many non-data related jobs. A long keyword arguement list of only relevant job title words was created along with a function which filters the unrelated jobs.

**Salary** - this is often quoted as a range and sometimes quoted annually, sometimes daily etc. Where a range is given, we assumed the mid point and all salaries were annualised to allow comparison. 
  - A new feature was created, salary type, containing information on how the salary was quoted i.e. annual, daily etc. 
  - Another feature was created which categorised pay types into either short term pay or long term (defined hour/day/week as short_term, month/year as long_term)

**Location** - location is quoted inconsistently, sometimes as a town or a village, sometimes a county. Each location was assigned to its relevant city within the UK to allow for modelling as a categorical variable (London, Manchester, Leeds etc.)

After the data cleaning, we were left with 1,392 unique job listings.

## Exploratory Data Analysis

**Salary Distribution**

<img src="/Users/KarimChammaa/Desktop/Data_Science/GA/DSI15-lessons/project/project-4/fig1.png" width="566" height="308" />

Chart shows the distribution of the yearly salary for the different categories of a quoted salary. For example a salary quoted as a daily rate is converted to a yearly salary as with others to be able to compare. Most of the salaries are at the lower end with a few very high values. The median salary is £38,300. Can see that the distribution is positively skewed showing that most salaries are at the lower end with a long tail of higher yearly salaries.

Can see that salaries quoted in daily format tend to be higher than the salaries which are quoted hourly, weekly or monthly. This implies that how the salary is quoted could be a good predictor of salary.
