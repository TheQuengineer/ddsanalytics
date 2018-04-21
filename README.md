# DDS Analytics & Talent Management

### Research Data Scientists
- Olha Tanyuk
- Sita Daggubati
- Tosin Akinpelu
- Quentin Thomas

### Introduction

DDS Analytics is a analytics company that specializes in talent management solutions for Fortune 1000 companies. Talent management is defined as the iterative process of developing and retaining employees. It may include workforce planning, employee training programs, identifying high-potential employees and reducing/preventing voluntary employee turnover (attrition). To gain a competitive edge over its competition, DDS Analytics is planning to leverage data science for talent management. The executive leadership has identified predicting employee turnover as its first application of data science for talent management. This repo is the full data analysis of our findings after exploring the many facets of the data.

### The Data

CaseStudy2-data.xlsx

### BusinessTrvl

"Travel_Rarely" "Travel_Frequently" "Non-Travel"   

### JobRole

"Sales Executive"           "Research Scientist"       
"Laboratory Technician"     "Manufacturing Director"   
"Healthcare Representative" "Manager"                  
"Sales Representative"      "Research Director"        
"Human Resources"   

### Attrition

"Yes" "No"   

### Department

"Sales"  "Research & Development" "Human Resources"   

### EduField

"Life Sciences"    "Other"            "Medical"         
"Marketing"        "Technical Degree" "Human Resources"   


| FEATURE      | DESCRIPTION                                                       |
|:------------:|:-----------------------------------------------------------------:|
|Age           | Employee Age                                                      |
|Attrition     | Attrition, Yes/No                                                 |
|BusinessTrvl  | Business Travel thats indicates if its Rare,Frequent or no travel |
|DailyRate     | Daily Rate(Pay)                                                   |
|Department    | Department                                                        |
|DistFromHome  | Distance From Home for Work                                       |
|YrsOfEdu      | Years Of Education of employee                                    |
|EduField      | Employee's Field of Education                                     |
|EmployeeCnt   | Employee Count                                                    |
|EmployeeNum   | Employee Number                                                   |
|EnvSatfctn    | Environment Satisfaction                                          |
|Gender        | Gender, Male/Female                                               |
|HourlyRate    | Hourly Rate                                                       |
|JobInvolmnt   | Job Involvement                                                   |
|JobLevel      | Job Level                                                         |
|JobRole       | Job Role                                                          |
|JobSatfctn    | Job Satisfaction                                                  |
|MaritalStat   | Marital Satisfaction                                              |
|MonthlyIncm   | Monthly Income(Salary)                                            |
|MonthlyRate   | Monthly Rate(Pay)                                                 |
|NumCmpWorked  | Number of Companies worked                                        |
|Over18        | Over 18 years of Age                                              |
|OverTime      | OverTime required or not, Yes/No                                  |
|PrcntSalHike  | Percent Salary Hike received from date of employment              |
|PerfRating    | Performance Rating                                                |
|RlnSatfctn    | Relationship Satisfaction within the company                      |
|StandardHrs   | Standard Hours of work                                            |
|StockOptLvl   | Current Stock option level of the employee                        |
|TtlWrkngYrs   | Total Number of Years worked                                      |
|TrngTmsLstYr  | Training times since last year                                    |
|WrkLifeBal    | Work Life Balance                                                 |
|YrsAtCompany  | Number of Years at the Company                                    |
|YrsInCrntRl   | Number of years in the current Job Role                           |
|YrsSncLstPrn  | Years Since last promotion                                        |
|YrsWthCurMgr  | Years With Current Manager                                        |



### Folder & File Information

- `ddsanalytics/` This folder contains case_study_info, reports and readme.

- `case_study_info` Contains all the background information important for understanding
the purpose of the study.
  + `CaseStudy2.pdf` The entire case study file that shows the list of questions being answered in the study.
  + `CaseStudy02Updated.docx` The list of requirements that the study must contain
  upon submission.

- `report`This has the r markdown file , html and dataset

- `dataset/` This folder contains all the data files that is used in the study.

  + `CaseStudy2-data.xlsx` 

- `report.html` The html page of the entire report of the study 
- `report.Rmd` Is the Rmarkdown version of the entire report. Contains all the code as well as a complete insights found during the research in an effort to answer the questions in the study.

- `README.md` The codebook summarizing the purpose of the entire project and how it is organized.

### The Tasks We're Addressing

1.	Formulate your Repo

- a.	The client wants this to be reproducible and know exactly what you did.  There needs to be an informative Readme, complete with several sections, as referenced in Live Session.  Give contact information, sessionInfo, and the objective of the repo at least.

- b.	You have two large data sets, and they will need its own Codebook, formatted in an approachable way.  Make sure you describe peculiarities of the data by variable and what needs transforming.  However, do not make it too long either.

- c.	Create a file structure that is accessible and transparent.  Document it in the root directory, ideally in the Readme.

2.	Clean your Raw Data 

- a.	Read the csv into R and take a look at the data set.  Output how many rows and columns the data.frame is.

- b.	The column names are either too much or not enough.  Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you're updating your codebook with information on the tidied data set as well.

- c.	Some columns are, due to Qualtrics, malfunctioning.

- d.	Make sure your columns are the proper data types (i.e., numeric, character, etc.).  If they are incorrect, convert them. 

3.	Preliminary Analysis

- a.	Remove all observations where the participant is under age 18.  No further analysis of underage individuals is permitted by your client.  Remove any other age outliers as you see fit, but be sure to tell what you're doing and why.

- b.	Please provide (in pretty-fied table format or similar), descriptive statistics on at least 7 variables (age, Income, etc.).  Create a simple histogram for two of them.  Comment on the shape of the distribution in your markdown.

- c.	Give the frequencies (in table format or similar) for Gender, Education, and Occupation.  They can be separate tables, if that's your choice.

- d.	Give the counts (again, pretty table) of management positions.

4.	Deeper Analysis and Visualization 

- a.	Note: You should make all of these appealing looking.  Remember to include things like a clean, informative title, axis labels that are in plain English, and readable axis values that do not overlap.

- b.	Create barcharts in ggplot or similar  The bars should be in descending order, Use any color palette of your choice other than the default.

- c.	Is there a relationship between Age and Income?  Create a scatterplot and make an assessment of whether there is a relationship.  Color each point based on the Gender of the participant.  You're welcome to use lm() or similar functions to back up your claims.

- d.	What about Life Satisfaction?  Create another scatterplot.  Is there a discernible relationship there to what?   


### Researcher Information & Responsibilities



| Researcher | Questions of Interest |
|:-----------:|:---------------------:|
|Sita Daggubati | Task 1, 2  & Codebook    |
|Olha Tanyuk  | Task 3B ,4C, 4D & Conclusion|
|Tosin Akinpelu| Task4D & PDF(Executive Summary, Prescriptive Analysis) |
|Quentin Thomas | Introduction, Task 1, 3C,3D, 4|


### Session Info for the CaseStudy II

sessionInfo()
R version 3.4.3 (2017-11-30)
Platform: x86_64-w64-mingw32/x64 (64-bit)
Running under: Windows >= 8 x64 (build 9200)

Matrix products: default

locale:
[1] LC_COLLATE=English_United States.1252  LC_CTYPE=English_United States.1252   
[3] LC_MONETARY=English_United States.1252 LC_NUMERIC=C                          
[5] LC_TIME=English_United States.1252    

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

loaded via a namespace (and not attached):
 [1] compiler_3.4.3  backports_1.1.2 magrittr_1.5    rprojroot_1.3-2 htmltools_0.3.6
 [6] tools_3.4.3     yaml_2.1.16     Rcpp_0.12.15    stringi_1.1.6   rmarkdown_1.8  
[11] knitr_1.20      stringr_1.3.0   digest_0.6.15   evaluate_0.10.1
 
