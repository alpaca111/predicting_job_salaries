## What industry factors are important in predicting salaries for data related jobs?
### Aim
We would like to understand which industry factors are most important in predicting the salary amounts for data related jobs. Only focused on data related jobs in the UK (e.g. data scientist, data analyst, business intelligence).

### Acquiring the date

The job data was acquired by scraping www.indeed.co.uk using BeautifulSoup. Searches were performed on different data related job titles for key cities in the United Kingdom with the main search options of 'data+scientist,+data+analyst,+machine+learning,+Data+Architect,+data+engineer'.
For each job listing the following components were collected :
- Job title
- Company
- Salary
- Location
