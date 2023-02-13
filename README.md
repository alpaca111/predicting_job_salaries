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
<img src = "https://user-images.githubusercontent.com/74214807/217845194-ff7356e9-5d9e-4852-9a68-6224d055bc6f.png" width="888" height="640" />


Chart shows the distribution of the yearly salary for the different categories of a quoted salary. For example a salary quoted as a daily rate is converted to a yearly salary as with others to be able to compare. Most of the salaries are at the lower end with a few very high values. The median salary is £38,300. Can see that the distribution is positively skewed showing that most salaries are at the lower end with a long tail of higher yearly salaries.

Can see that salaries quoted in daily format tend to be higher than the salaries which are quoted hourly, weekly or monthly. This implies that how the salary is quoted could be a good predictor of salary.

**Salary Distribution by location**

<img src = "https://user-images.githubusercontent.com/74214807/217849693-df99e205-64fd-4a51-a530-dc7268042e86.png" width="920" height="668" />

The plot shows salary distribution for every city, ordered by the median salary (shown by the line). Can see that London has the largest number of data points and the highest median salary while Newcastle has lowest paid salaries. City should be a reasonable predictor for salary

Boxplot shows that London and Newcastle have the highest and lowest average paid salaries respectively. Expect that both will give the largest coefficients for a simple logisitical regression model on just city as a feature, for each class, 'high' and 'low' respectively.

**Median salary by position type**
                                                                                                                                          
<img src = "https://user-images.githubusercontent.com/74214807/217851203-91617cb4-97e4-47de-9e08-aaf417632b63.png" width="923" height="615" />

Bar plot shows the average yearly salary for different job positions and for salary security type (long term security vs short term). The plot shows that gnerally shorter term security is higher paid vs long term. Annual salary scales as expected with increasing position apart from mid level (could point to inaccurately choosing list of words categorising a mid level position instead of senior position)

## Modelling

To answer the question about which industry factors are most important in predicting the salary amounts for data related jobs, we created a model which tries to predict whether a salary is 'high' or 'low'. This was converted into a binary classification problem to help remove some of the noise of the extreme salaries. The high - low salary split was done on the Median to have a balanced dataset - giving a baseline accuracy of around 50%. The model predictions were based on the following factors:

- Location
- Key words in the job title
- Salary pay type (e.g. annual, daily..)
- Salary security (feature engineered from salary pay type)
- Position level (entry, mid-level, intermediate senior)
- 
A 'high' salary is defined as being above the median salary of £38,300 and a 'low' salary is below.

Six different models were tuned and tested. The model was chosen based on optimal accuracy score while also having the highest precision such that the chosen model gives lowest percentage of False Positives. The main reason for also optimising on precision was due to the fact that we wanted to limit the dissapointment factor when telling someone they should be receiving a 'high' salary from a given job when in fact they would be receiving a 'low' salary job.

The chosen model was a randomforest classifier type and it was able to predict correctly whether a salary is 'high' or 'low' based on the above factors 75% of the time.

<img src = "https://user-images.githubusercontent.com/74214807/218445895-52cb252f-4975-43c6-a002-a81d0076cfab.png" />


The bar chart above shows the top 20 feature importances for the Random Forest model. Words from the job title make up 14 out of the 20 most important features from the model for example: analyst, engineer, data, senior, architect. The region London is the 8th most important feature - this makes sense given that salaries tend to be higher in London.

## Improvements 

- Further feature engineering of predictor variables
- Incude more features - i.e could include Job summary and apply NLP. I presume this would add value to model performance as the jobtitle key words dominated in terms of importance and job summary would have more detailed keywords to choose from. - Further gridsearch parameter tuning
- Increased data pool (only had 1392 data points)
- Investigate outliers thoroughly and treat accordingly to be able to apply a regression model instead of classification with 2 categories.

## Limitations

The data for this project was collected in January 2021. It does not take into account any trends in the job market over time and therefore the model will not reflect any changes over time e.g. a shift to remote working.
