---
title: "DDSAnalyticsReport"
author: "Quentin,Sita,Olha,Tosin"
date: "4/4/2018"
output: 
  html_document:
    keep_md: true
---



## Abstract

DDS Analytics is a analytics company that specializes in talent management solutions for Fortune 1000 companies. Talent management is defined as the iterative process of developing and retaining employees. It may include workforce planning, employee training programs, identifying high-potential employees and reducing/preventing voluntary employee turnover (attrition). To gain a competitive edge over its competition, DDS Analytics is planning to leverage data science for talent management. The executive leadership has identified predicting employee turnover as its first application of data science for talent management. This repo is the full data analysis of our findings after exploring the many facets of the data.

## I. Introduction

Talent is a precious commodity, especially in the corporate sector. Every organization no matter how big or small seeks not only to hire, but also to retain the best talent possible. Employee retention however, is much easier said than done these days, especially when the average amount of years an employee is likely to remain at a specific place of employment is [4.5 years](https://www.forbes.com/sites/davidsturt/2016/01/13/true-or-false-employees-today-only-stay-one-or-two-years/#6736606b6b4c) as of 2014. What are the factors that lead to employee attrition? This is an age old question that most companies continue to try to answer. Can employee attrition be slowed, or avoided all together? Is there any data to support that job satisfaction is the main cause for an employee remaining at a job? All these questions and more will be explored in this study. Our goal is to find sound answers to these questions rooted in strong statistical analysis of a dataset we have gathered from some of the most influential companies in the world.



## II. Background

As a Talent Management organization we set out to leverage the strength of Data Science in order to maintain the best employees at our organization DDS Analytics. In order for the organization to move forward in this endeavor it was neccessary to study the key factors in maintaining the best employees. As a result this study was launched by the management team in order to gain more insight into this arena.


## III.  Methodology

### Data Cleaning & Preparation

In order to make sure our data was ready for proper analysis we had to go through a series of steps in order to prepare the data. These steps include the following...

1. Data Import
2. Data Type Conversion
3. Factorization For Catagorical Variables
4. Handling of Missing or Inaccurate Values

We will discuss the process of each step below.

#### Data Import

We have obtained a dataset which incldudes 35 variables with 1470 observations. The dataset is will be referred to as `talentMgmtData`. In order to better understand our data we needed to proceed with cleaning it appropriately.

#### Data Type Conversion

Analysis could not be done properly if our variables are not in the correct type. Several of the numerical based variables showed up as doubles which was not neccessarily appropriate for research and analysis. For example, the years of experience for specfic employees needed to be converted to integer types, and Standard Working hours had no reason to show as a double, so it to was converted to an integer. This process was followed for each one of the 35 variables on order to ensure each columns assigned data type made sense for the context of the study.

#### Factorization For Catagorical Variables

Within our `talentMgmtData` we noticed that there were several columns that were improperly listed as integers when they were simply catagories. In order for us to be able to do factor analysis we picked out the columns that would be better suited to be catagories instead of integers so that we could get a better understanding of how our talent was spread out over different situations. For example, Columns like Department, BusinessTravel, Over18, & Jobsatisfaction to name a few, are all better suited to be treated as catagorical variables for our research purposes. As a result, we have converted the appropriate columns that explained how our data points were separated by making them factors instead of numerical values.

#### Handling of Missing or Inaccurate Values

In order for our mathematical calculations to work we had to convert many of our data points into numerical values so that our regression analysis would be more accurate. For example, DailyRate, Total Working Years, Years with Current Manager, are all examples of numerical based data points that can have mathematical operations performed on them. As a result we located variables like these and made sure the data type was appropriate giving us more flexibility during analysis.

#### DATA CLEANING

```r
#a.	Read the csv into R and take a look at the data set.  Output how many rows and columns the data.frame is.
library(readxl)
talentMgmtData <- read_excel("datasets/CaseStudy2-data.xlsx")
dim(talentMgmtData)
```

```
## [1] 1470   35
```

```r
#b	The column names are either too much or not enough.  Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. TODO: Make sure you're updating your codebook with information on the tidied data set as well.

names(talentMgmtData) <- c("Age","Attrition","BusinessTrvl","DailyRate","Department","DistFromHome","YrsOfEdu","EduField","EmployeeCnt","EmployeeNum","EnvSatfctn","Gender","HourlyRate","JobInvolmnt","JobLevel","JobRole","JobSatfctn","MaritalStat","MonthlyIncm","MonthlyRate","NumCmpWorked","Over18","OverTime","PrcntSalHike","PerfRating","RlnSatfctn","StandardHrs","StockOptLvl","TtlWrkngYrs","TrngTmsLstYr","WrkLifeBal","YrsAtCompany","YrsInCrntRl","YrsSncLstPrn","YrsWthCurMgr")

names(talentMgmtData)
```

```
##  [1] "Age"          "Attrition"    "BusinessTrvl" "DailyRate"   
##  [5] "Department"   "DistFromHome" "YrsOfEdu"     "EduField"    
##  [9] "EmployeeCnt"  "EmployeeNum"  "EnvSatfctn"   "Gender"      
## [13] "HourlyRate"   "JobInvolmnt"  "JobLevel"     "JobRole"     
## [17] "JobSatfctn"   "MaritalStat"  "MonthlyIncm"  "MonthlyRate" 
## [21] "NumCmpWorked" "Over18"       "OverTime"     "PrcntSalHike"
## [25] "PerfRating"   "RlnSatfctn"   "StandardHrs"  "StockOptLvl" 
## [29] "TtlWrkngYrs"  "TrngTmsLstYr" "WrkLifeBal"   "YrsAtCompany"
## [33] "YrsInCrntRl"  "YrsSncLstPrn" "YrsWthCurMgr"
```

```r
# c	Some columns are, due to Qualtrics, malfunctioning.

# TODO: Discuss with team, delete Over18 and StandardHrs(80hrs) columns
talentMgmtData$Over18 <- NULL
talentMgmtData <- subset(talentMgmtData, select = -c(StandardHrs))

# d	Make sure your columns are the proper data types (i.e., numeric, character, etc.).  If they are incorrect, convert them. 
str(talentMgmtData)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1470 obs. of  33 variables:
##  $ Age         : num  41 49 37 33 27 32 59 30 38 36 ...
##  $ Attrition   : chr  "Yes" "No" "Yes" "No" ...
##  $ BusinessTrvl: chr  "Travel_Rarely" "Travel_Frequently" "Travel_Rarely" "Travel_Frequently" ...
##  $ DailyRate   : num  1102 279 1373 1392 591 ...
##  $ Department  : chr  "Sales" "Research & Development" "Research & Development" "Research & Development" ...
##  $ DistFromHome: num  1 8 2 3 2 2 3 24 23 27 ...
##  $ YrsOfEdu    : num  2 1 2 4 1 2 3 1 3 3 ...
##  $ EduField    : chr  "Life Sciences" "Life Sciences" "Other" "Life Sciences" ...
##  $ EmployeeCnt : num  1 1 1 1 1 1 1 1 1 1 ...
##  $ EmployeeNum : num  1 2 4 5 7 8 10 11 12 13 ...
##  $ EnvSatfctn  : num  2 3 4 4 1 4 3 4 4 3 ...
##  $ Gender      : chr  "Female" "Male" "Male" "Female" ...
##  $ HourlyRate  : num  94 61 92 56 40 79 81 67 44 94 ...
##  $ JobInvolmnt : num  3 2 2 3 3 3 4 3 2 3 ...
##  $ JobLevel    : num  2 2 1 1 1 1 1 1 3 2 ...
##  $ JobRole     : chr  "Sales Executive" "Research Scientist" "Laboratory Technician" "Research Scientist" ...
##  $ JobSatfctn  : num  4 2 3 3 2 4 1 3 3 3 ...
##  $ MaritalStat : chr  "Single" "Married" "Single" "Married" ...
##  $ MonthlyIncm : num  5993 5130 2090 2909 3468 ...
##  $ MonthlyRate : num  19479 24907 2396 23159 16632 ...
##  $ NumCmpWorked: num  8 1 6 1 9 0 4 1 0 6 ...
##  $ OverTime    : chr  "Yes" "No" "Yes" "Yes" ...
##  $ PrcntSalHike: num  11 23 15 11 12 13 20 22 21 13 ...
##  $ PerfRating  : num  3 4 3 3 3 3 4 4 4 3 ...
##  $ RlnSatfctn  : num  1 4 2 3 4 3 1 2 2 2 ...
##  $ StockOptLvl : num  0 1 0 0 1 0 3 1 0 2 ...
##  $ TtlWrkngYrs : num  8 10 7 8 6 8 12 1 10 17 ...
##  $ TrngTmsLstYr: num  0 3 3 3 3 2 3 2 2 3 ...
##  $ WrkLifeBal  : num  1 3 3 3 3 2 2 3 3 2 ...
##  $ YrsAtCompany: num  6 10 0 8 2 7 1 1 9 7 ...
##  $ YrsInCrntRl : num  4 7 0 7 2 7 0 0 7 7 ...
##  $ YrsSncLstPrn: num  0 1 0 3 2 3 0 0 1 7 ...
##  $ YrsWthCurMgr: num  5 7 0 0 2 6 0 0 8 7 ...
```

```r
#TODO: Discuss with team foll. factor levels of dataset
unique(talentMgmtData$BusinessTrvl)
```

```
## [1] "Travel_Rarely"     "Travel_Frequently" "Non-Travel"
```

```r
unique(talentMgmtData$JobRole)
```

```
## [1] "Sales Executive"           "Research Scientist"       
## [3] "Laboratory Technician"     "Manufacturing Director"   
## [5] "Healthcare Representative" "Manager"                  
## [7] "Sales Representative"      "Research Director"        
## [9] "Human Resources"
```

```r
unique(talentMgmtData$Attrition)
```

```
## [1] "Yes" "No"
```

```r
unique(talentMgmtData$Department)
```

```
## [1] "Sales"                  "Research & Development"
## [3] "Human Resources"
```

```r
unique(talentMgmtData$EduField)
```

```
## [1] "Life Sciences"    "Other"            "Medical"         
## [4] "Marketing"        "Technical Degree" "Human Resources"
```

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
#Get an Idea of the current format of the colums we are currently using.
glimpse(talentMgmtData)
```

```
## Observations: 1,470
## Variables: 33
## $ Age          <dbl> 41, 49, 37, 33, 27, 32, 59, 30, 38, 36, 35, 29, 3...
## $ Attrition    <chr> "Yes", "No", "Yes", "No", "No", "No", "No", "No",...
## $ BusinessTrvl <chr> "Travel_Rarely", "Travel_Frequently", "Travel_Rar...
## $ DailyRate    <dbl> 1102, 279, 1373, 1392, 591, 1005, 1324, 1358, 216...
## $ Department   <chr> "Sales", "Research & Development", "Research & De...
## $ DistFromHome <dbl> 1, 8, 2, 3, 2, 2, 3, 24, 23, 27, 16, 15, 26, 19, ...
## $ YrsOfEdu     <dbl> 2, 1, 2, 4, 1, 2, 3, 1, 3, 3, 3, 2, 1, 2, 3, 4, 2...
## $ EduField     <chr> "Life Sciences", "Life Sciences", "Other", "Life ...
## $ EmployeeCnt  <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
## $ EmployeeNum  <dbl> 1, 2, 4, 5, 7, 8, 10, 11, 12, 13, 14, 15, 16, 18,...
## $ EnvSatfctn   <dbl> 2, 3, 4, 4, 1, 4, 3, 4, 4, 3, 1, 4, 1, 2, 3, 2, 1...
## $ Gender       <chr> "Female", "Male", "Male", "Female", "Male", "Male...
## $ HourlyRate   <dbl> 94, 61, 92, 56, 40, 79, 81, 67, 44, 94, 84, 49, 3...
## $ JobInvolmnt  <dbl> 3, 2, 2, 3, 3, 3, 4, 3, 2, 3, 4, 2, 3, 3, 2, 4, 4...
## $ JobLevel     <dbl> 2, 2, 1, 1, 1, 1, 1, 1, 3, 2, 1, 2, 1, 1, 1, 3, 1...
## $ JobRole      <chr> "Sales Executive", "Research Scientist", "Laborat...
## $ JobSatfctn   <dbl> 4, 2, 3, 3, 2, 4, 1, 3, 3, 3, 2, 3, 3, 4, 3, 1, 2...
## $ MaritalStat  <chr> "Single", "Married", "Single", "Married", "Marrie...
## $ MonthlyIncm  <dbl> 5993, 5130, 2090, 2909, 3468, 3068, 2670, 2693, 9...
## $ MonthlyRate  <dbl> 19479, 24907, 2396, 23159, 16632, 11864, 9964, 13...
## $ NumCmpWorked <dbl> 8, 1, 6, 1, 9, 0, 4, 1, 0, 6, 0, 0, 1, 0, 5, 1, 0...
## $ OverTime     <chr> "Yes", "No", "Yes", "Yes", "No", "No", "Yes", "No...
## $ PrcntSalHike <dbl> 11, 23, 15, 11, 12, 13, 20, 22, 21, 13, 13, 12, 1...
## $ PerfRating   <dbl> 3, 4, 3, 3, 3, 3, 4, 4, 4, 3, 3, 3, 3, 3, 3, 3, 3...
## $ RlnSatfctn   <dbl> 1, 4, 2, 3, 4, 3, 1, 2, 2, 2, 3, 4, 4, 3, 2, 3, 4...
## $ StockOptLvl  <dbl> 0, 1, 0, 0, 1, 0, 3, 1, 0, 2, 1, 0, 1, 1, 0, 1, 2...
## $ TtlWrkngYrs  <dbl> 8, 10, 7, 8, 6, 8, 12, 1, 10, 17, 6, 10, 5, 3, 6,...
## $ TrngTmsLstYr <dbl> 0, 3, 3, 3, 3, 2, 3, 2, 2, 3, 5, 3, 1, 2, 4, 1, 5...
## $ WrkLifeBal   <dbl> 1, 3, 3, 3, 3, 2, 2, 3, 3, 2, 3, 3, 2, 3, 3, 3, 2...
## $ YrsAtCompany <dbl> 6, 10, 0, 8, 2, 7, 1, 1, 9, 7, 5, 9, 5, 2, 4, 10,...
## $ YrsInCrntRl  <dbl> 4, 7, 0, 7, 2, 7, 0, 0, 7, 7, 4, 5, 2, 2, 2, 9, 2...
## $ YrsSncLstPrn <dbl> 0, 1, 0, 3, 2, 3, 0, 0, 1, 7, 0, 0, 4, 1, 0, 8, 0...
## $ YrsWthCurMgr <dbl> 5, 7, 0, 0, 2, 6, 0, 0, 8, 7, 3, 8, 3, 2, 3, 8, 5...
```

```r
# Factor appropriate columns 
talentMgmtData$Department <- as.factor(talentMgmtData$Department)
talentMgmtData$BusinessTrvl <- as.factor(talentMgmtData$BusinessTrvl)
talentMgmtData$OverTime <- as.factor(talentMgmtData$OverTime)
talentMgmtData$EduField <- as.factor(talentMgmtData$EduField)
talentMgmtData$Gender <- as.factor(talentMgmtData$Gender)
talentMgmtData$Attrition <- as.factor(talentMgmtData$Attrition)
talentMgmtData$MaritalStat <- as.factor(talentMgmtData$MaritalStat)
talentMgmtData$JobRole <- as.factor(talentMgmtData$JobRole)
talentMgmtData$EnvSatfctn <- as.factor(talentMgmtData$EnvSatfctn)
talentMgmtData$JobLevel <- as.factor(talentMgmtData$JobLevel)
talentMgmtData$StockOptLvl <- as.factor(talentMgmtData$StockOptLvl)
talentMgmtData$PerfRating <- as.factor(talentMgmtData$PerfRating)
talentMgmtData$EmployeeCnt <- as.factor(talentMgmtData$EmployeeCnt)
talentMgmtData$JobInvolmnt <- as.factor(talentMgmtData$JobInvolmnt)
talentMgmtData$RlnSatfctn <- as.factor(talentMgmtData$RlnSatfctn)
talentMgmtData$WrkLifeBal <- as.factor(talentMgmtData$WrkLifeBal)
talentMgmtData$JobSatfctn <- as.factor(talentMgmtData$JobSatfctn)
# handle numeric based columns to show as double or integer if need be.
talentMgmtData$Age <- as.integer(talentMgmtData$Age)
talentMgmtData$EmployeeNum <- as.integer(talentMgmtData$EmployeeNum)
talentMgmtData$DistFromHome <- as.integer(talentMgmtData$DistFromHome)
talentMgmtData$YrsOfEdu <- as.integer(talentMgmtData$YrsOfEdu)
talentMgmtData$DailyRate <- as.numeric(talentMgmtData$DailyRate)
talentMgmtData$TtlWrkngYrs <- as.integer(talentMgmtData$TtlWrkngYrs)
talentMgmtData$YrsAtCompany <- as.integer(talentMgmtData$YrsAtCompany)
talentMgmtData$NumCmpWorked <- as.integer(talentMgmtData$NumCmpWorked)
talentMgmtData$YrsInCrntRl <- as.integer(talentMgmtData$YrsInCrntRl)
talentMgmtData$YrsSncLstPrn <- as.integer(talentMgmtData$YrsSncLstPrn)
talentMgmtData$YrsWthCurMgr <- as.integer(talentMgmtData$YrsWthCurMgr)
talentMgmtData$TrngTmsLstYr <- as.integer(talentMgmtData$TrngTmsLstYr)
#Take a look at data after type conversions are applied to the appropriate columns
glimpse(talentMgmtData)
```

```
## Observations: 1,470
## Variables: 33
## $ Age          <int> 41, 49, 37, 33, 27, 32, 59, 30, 38, 36, 35, 29, 3...
## $ Attrition    <fctr> Yes, No, Yes, No, No, No, No, No, No, No, No, No...
## $ BusinessTrvl <fctr> Travel_Rarely, Travel_Frequently, Travel_Rarely,...
## $ DailyRate    <dbl> 1102, 279, 1373, 1392, 591, 1005, 1324, 1358, 216...
## $ Department   <fctr> Sales, Research & Development, Research & Develo...
## $ DistFromHome <int> 1, 8, 2, 3, 2, 2, 3, 24, 23, 27, 16, 15, 26, 19, ...
## $ YrsOfEdu     <int> 2, 1, 2, 4, 1, 2, 3, 1, 3, 3, 3, 2, 1, 2, 3, 4, 2...
## $ EduField     <fctr> Life Sciences, Life Sciences, Other, Life Scienc...
## $ EmployeeCnt  <fctr> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, ...
## $ EmployeeNum  <int> 1, 2, 4, 5, 7, 8, 10, 11, 12, 13, 14, 15, 16, 18,...
## $ EnvSatfctn   <fctr> 2, 3, 4, 4, 1, 4, 3, 4, 4, 3, 1, 4, 1, 2, 3, 2, ...
## $ Gender       <fctr> Female, Male, Male, Female, Male, Male, Female, ...
## $ HourlyRate   <dbl> 94, 61, 92, 56, 40, 79, 81, 67, 44, 94, 84, 49, 3...
## $ JobInvolmnt  <fctr> 3, 2, 2, 3, 3, 3, 4, 3, 2, 3, 4, 2, 3, 3, 2, 4, ...
## $ JobLevel     <fctr> 2, 2, 1, 1, 1, 1, 1, 1, 3, 2, 1, 2, 1, 1, 1, 3, ...
## $ JobRole      <fctr> Sales Executive, Research Scientist, Laboratory ...
## $ JobSatfctn   <fctr> 4, 2, 3, 3, 2, 4, 1, 3, 3, 3, 2, 3, 3, 4, 3, 1, ...
## $ MaritalStat  <fctr> Single, Married, Single, Married, Married, Singl...
## $ MonthlyIncm  <dbl> 5993, 5130, 2090, 2909, 3468, 3068, 2670, 2693, 9...
## $ MonthlyRate  <dbl> 19479, 24907, 2396, 23159, 16632, 11864, 9964, 13...
## $ NumCmpWorked <int> 8, 1, 6, 1, 9, 0, 4, 1, 0, 6, 0, 0, 1, 0, 5, 1, 0...
## $ OverTime     <fctr> Yes, No, Yes, Yes, No, No, Yes, No, No, No, No, ...
## $ PrcntSalHike <dbl> 11, 23, 15, 11, 12, 13, 20, 22, 21, 13, 13, 12, 1...
## $ PerfRating   <fctr> 3, 4, 3, 3, 3, 3, 4, 4, 4, 3, 3, 3, 3, 3, 3, 3, ...
## $ RlnSatfctn   <fctr> 1, 4, 2, 3, 4, 3, 1, 2, 2, 2, 3, 4, 4, 3, 2, 3, ...
## $ StockOptLvl  <fctr> 0, 1, 0, 0, 1, 0, 3, 1, 0, 2, 1, 0, 1, 1, 0, 1, ...
## $ TtlWrkngYrs  <int> 8, 10, 7, 8, 6, 8, 12, 1, 10, 17, 6, 10, 5, 3, 6,...
## $ TrngTmsLstYr <int> 0, 3, 3, 3, 3, 2, 3, 2, 2, 3, 5, 3, 1, 2, 4, 1, 5...
## $ WrkLifeBal   <fctr> 1, 3, 3, 3, 3, 2, 2, 3, 3, 2, 3, 3, 2, 3, 3, 3, ...
## $ YrsAtCompany <int> 6, 10, 0, 8, 2, 7, 1, 1, 9, 7, 5, 9, 5, 2, 4, 10,...
## $ YrsInCrntRl  <int> 4, 7, 0, 7, 2, 7, 0, 0, 7, 7, 4, 5, 2, 2, 2, 9, 2...
## $ YrsSncLstPrn <int> 0, 1, 0, 3, 2, 3, 0, 0, 1, 7, 0, 0, 4, 1, 0, 8, 0...
## $ YrsWthCurMgr <int> 5, 7, 0, 0, 2, 6, 0, 0, 8, 7, 3, 8, 3, 2, 3, 8, 5...
```

### Preliminary Analysis



---

####3.A####


```r
talentData <- talentMgmtData[talentMgmtData$Age > 18, ]
range(talentData$Age)
```

```
## [1] 19 60
```

As we can see above, only Ages 19 to 60 exists within our dataset.

Now that the data has been prepared and formatted accordingly it is neccessary to explore it to its depths.

#### Descriptive statistics

Lets check descriptive statistics for some of the data we have

```r
library(knitr)
library(kableExtra)
DescriptiveStatistics<-c("min", "max", "mean", "sd")
HourlyRate <- c(min(talentData$HourlyRate), max(talentData$HourlyRate), mean(talentData$HourlyRate), sd(talentData$HourlyRate))
MonthlyIncome <- c(min(talentData$MonthlyIncm), max(talentData$MonthlyIncm), mean(talentData$MonthlyIncm), sd(talentData$MonthlyIncm))
TotalWorkYears <- c(min(talentData$TtlWrkngYrs), max(talentData$TtlWrkngYrs), mean(talentData$TtlWrkngYrs), sd(talentData$TtlWrkngYrs))
Age <- c(min(talentData$Age), max(talentData$Age), mean(talentData$Age), sd(talentData$Age)) 
YearsAtCompany <-c(min(talentData$YrsAtCompany), max(talentData$YrsAtCompany), mean(talentData$YrsAtCompany), sd(talentData$YrsAtCompany))
MonthlyRate <- c(min(talentData$MonthlyRate), max(talentData$MonthlyRate), mean(talentData$MonthlyRate), sd(talentData$MonthlyRate))
YrsOfEdu <- c(min(talentData$YrsOfEdu), max(talentData$YrsOfEdu), mean(talentData$YrsOfEdu), sd(talentData$YrsOfEdu))
table <- data.frame(DescriptiveStatistics, HourlyRate, MonthlyRate, MonthlyIncome, TotalWorkYears, YearsAtCompany, Age,  YrsOfEdu)
table %>%
  kable("html") %>%
  kable_styling()
```

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> DescriptiveStatistics </th>
   <th style="text-align:right;"> HourlyRate </th>
   <th style="text-align:right;"> MonthlyRate </th>
   <th style="text-align:right;"> MonthlyIncome </th>
   <th style="text-align:right;"> TotalWorkYears </th>
   <th style="text-align:right;"> YearsAtCompany </th>
   <th style="text-align:right;"> Age </th>
   <th style="text-align:right;"> YrsOfEdu </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> min </td>
   <td style="text-align:right;"> 30.00000 </td>
   <td style="text-align:right;"> 2094.000 </td>
   <td style="text-align:right;"> 1009.000 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 0.000000 </td>
   <td style="text-align:right;"> 19.000000 </td>
   <td style="text-align:right;"> 1.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> max </td>
   <td style="text-align:right;"> 100.00000 </td>
   <td style="text-align:right;"> 26999.000 </td>
   <td style="text-align:right;"> 19999.000 </td>
   <td style="text-align:right;"> 40.000000 </td>
   <td style="text-align:right;"> 40.000000 </td>
   <td style="text-align:right;"> 60.000000 </td>
   <td style="text-align:right;"> 5.000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> mean </td>
   <td style="text-align:right;"> 65.87893 </td>
   <td style="text-align:right;"> 14312.212 </td>
   <td style="text-align:right;"> 6530.207 </td>
   <td style="text-align:right;"> 11.341313 </td>
   <td style="text-align:right;"> 7.046512 </td>
   <td style="text-align:right;"> 37.027360 </td>
   <td style="text-align:right;"> 2.915185 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> sd </td>
   <td style="text-align:right;"> 20.34338 </td>
   <td style="text-align:right;"> 7124.669 </td>
   <td style="text-align:right;"> 4706.273 </td>
   <td style="text-align:right;"> 7.757034 </td>
   <td style="text-align:right;"> 6.121228 </td>
   <td style="text-align:right;"> 9.052093 </td>
   <td style="text-align:right;"> 1.025173 </td>
  </tr>
</tbody>
</table>

####3.B####
The average Hourly rate is $65.88/hour, the average Monthly Rate is $14,312.21/month, the average Monthly Income is $6,530.21/month, average Total Worked Years is 11.34 years, average Worked years at the company is 7.04 years, average Age of the employees is 37 years and average Years of Education of the employees is 2.9 years ('Bachelor' degree).

Lets check histograms of Hourly Rate and Monthly income.


```r
hist(talentData$HourlyRate, col = "darkred", xlab="Hourly Rate", main="Histogram of Hourly Rate")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
hist(talentData$MonthlyIncm, col = "darkgreen", xlab="Monthly Income", main="Histogram of Monthly Income")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

#### 3.B####

On the histograms we can see almost equal spread of hourly rates within the company, but we can not say the same about monthly income, it means that employees work different amount of hours (some of them are part time, and some of them work with overtime (more then 40hours), we do not have information if any bonuses were paid in the company, so it does not make sense to continue analize working hours). 

#### 3.C####

##### Understanding Gender, Education, & Occupations

Next we explore how Gender, Education and Job Role is broken down within our dataset. Below are frequency tables of our findings for these three catagories...


```r
library(ggplot2)

demographics <- talentData[,c("JobRole", "Gender", "EduField")]

build_table <- function(column_name, title) {
  
   t <- as.data.frame(table(column_name))
    names(t) <- c(title, "Frequency")
      t %>% kable("html") %>% kable_styling(bootstrap_options = c("striped", "hover", "condensed", "responsive")) 

}

build_table(demographics$Gender, "Gender")
```

<table class="table table-striped table-hover table-condensed table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Gender </th>
   <th style="text-align:right;"> Frequency </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Female </td>
   <td style="text-align:right;"> 584 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Male </td>
   <td style="text-align:right;"> 878 </td>
  </tr>
</tbody>
</table>

```r
build_table(demographics$EduField, "Education")
```

<table class="table table-striped table-hover table-condensed table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Education </th>
   <th style="text-align:right;"> Frequency </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Human Resources </td>
   <td style="text-align:right;"> 27 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Life Sciences </td>
   <td style="text-align:right;"> 603 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Marketing </td>
   <td style="text-align:right;"> 158 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Medical </td>
   <td style="text-align:right;"> 460 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Other </td>
   <td style="text-align:right;"> 82 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Technical Degree </td>
   <td style="text-align:right;"> 132 </td>
  </tr>
</tbody>
</table>

```r
build_table(demographics$JobRole, "Job Role")
```

<table class="table table-striped table-hover table-condensed table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Job Role </th>
   <th style="text-align:right;"> Frequency </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Healthcare Representative </td>
   <td style="text-align:right;"> 131 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Human Resources </td>
   <td style="text-align:right;"> 52 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Laboratory Technician </td>
   <td style="text-align:right;"> 256 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Manager </td>
   <td style="text-align:right;"> 102 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Manufacturing Director </td>
   <td style="text-align:right;"> 145 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Research Director </td>
   <td style="text-align:right;"> 80 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Research Scientist </td>
   <td style="text-align:right;"> 290 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Sales Executive </td>
   <td style="text-align:right;"> 326 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Sales Representative </td>
   <td style="text-align:right;"> 80 </td>
  </tr>
</tbody>
</table>


Next, we examine the frequency for gender and how it is distributed across job roles visually.


```r
theme_set(theme_light())

ggplot(demographics, aes(demographics$JobRole)) + 
  geom_bar(aes(fill=Gender), width = 0.5) +
  labs(title = "Gender by Job Role",
       subtitle = "Men & Women in Specific JobRole",
       x = "Job Role",
       y = "Frequency") +
  coord_flip()
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

Our chart shows a bimodal distribution of our job roles. What is interesting here is we can see that sales executive is the most commonly occuring job in our dataset with more than 300 people represented in that category. It is also interesting to note that the spread between male and female in that job catagory looks almost equally represented. Our Lowest category is Human Resources Which has partitioned of mostly males even though there are just under 50 people in this catagory as a whole.

What about Education? How is education represented across the genders. We take a look at that distribution next.


```r
theme_set(theme_dark())

ggplot(demographics, aes(demographics$EduField)) + 
  geom_bar(aes(fill=Gender), width = 0.5) +
  labs(title = "Gender by Field Of Education",
       subtitle = "A breakdown in what fields of education was explored by the genders",
       x = "Field Of Study",
       y = "Frequency") +
  coord_flip()
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

We can see from this chart that Human Resources has the lowest participation in terms of education which actually makes sense given that it is our lowest filled job role. Life Science seems to be the most popular field of study between all the listed education choices with 600 different people in our dataset who studied in this field. This does not neccesarily match with our discovery regarding our popular job role. Life Science skills can translate into making great Sales Executives, but this educational field of study does not seem to be directly related to the Sales Executive.

#### 3.D####

Finally, we take a look at a frequency Table for all the different management positions.


```r
t <- droplevels(filter(demographics, JobRole == "Manager" | JobRole == "Manufacturing Director" | JobRole == "Research Director"))

build_table(t$JobRole, "ManagementOnly")
```

<table class="table table-striped table-hover table-condensed table-responsive" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> ManagementOnly </th>
   <th style="text-align:right;"> Frequency </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Manager </td>
   <td style="text-align:right;"> 102 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Manufacturing Director </td>
   <td style="text-align:right;"> 145 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Research Director </td>
   <td style="text-align:right;"> 80 </td>
  </tr>
</tbody>
</table>


Now that we have an overall view of our data now we can begin to try to answer our questions of interest regarding our dataset. Our questions of interest are simply the following...

1. What are the factors that lead to employee attrition?
2. Can employee attrition be slowed, or avoided all together?

Our next section will use all of our recent discoveries about the `talentData` to answer these inquiries.

## IV. Deeper Analysis and Visualization


When it comes to jobs the first thing that we want to look at is our age distribution. This is an imporatant step in our EDA process as we would like to get an idea of how old or young our these individuals in our entire dataset as it might give us a good place to start. We are only interested in exploring individuals in the workforce that are older than 18, so all of the forward analysis will take this constraint into consideration.


```r
hist(talentData$Age, xlab= "Ages",
     ylab="Frequency Of Occurrence",
     main= "Age Distribution Frequency",
     col = "blue")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

Based on the chart above we can see that our age range is between 20 and 60 with a large portion of ages being between 25 and 45. This is insightful as it might help us with interpretation of our findings moving forward. It is also worth noting that  between 30 and 35  is the most occurring age of all the age groups with over 350 recorded ages within this group!

Another thing that we would like to explore is whether or not there is a relationship between our Ages and the number of years they have spent at a specific company. If there is a relationship, we would like to understand whether or not the relationship is positive or negatively correlated.


```r
library(ggplot2)
theme_set(theme_light())

ggplot(talentData, aes(x=Age, y=YrsAtCompany)) +
  ggtitle("Years at Company vs Age") +
  theme(plot.title = element_text(hjust = 0.5)) +
  labs(x= "Age", y="Years") +
  geom_point(shape=1, col = "purple") +
  geom_smooth(method = "gam")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

Our findings here are not surprising. We notice that visually there might be evidence of a positive linear relationship between age and years at a specific company. This finding suggests that the older you are the more likely you are to have a greater number of years at a specific company. To know for sure we examine pearson correlation between `YrsAtCompany` and `Age`.


```r
cor.test(x=talentData$Age, y=talentData$YrsAtCompany,
         alternative = "two.sided",
         method="pearson",
         conf.level = 0.95,
         exact = TRUE)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  talentData$Age and talentData$YrsAtCompany
## t = 12.148, df = 1460, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.2556936 0.3488375
## sample estimates:
##      cor 
## 0.302989
```

Based on the results of our correlation test we have a pearsons correlation value of `0.302989` (95% CI: 0.25 to 0.34) which is more evidence of a positive linear relationship between Age and Years at a specific company. It is important for us to keep this relationship in mind moving forward for the rest of the study.

##### Understaning Incomes in the dataset

The next important thing we want to explore is our income distribution. Income is a major factor in employment. Without income, there is no reason for anyone worker to make effort to join a company in the first place. We would like to get an Idea of how the income distribution looks within our dataset. We would also like to understand the relationship between our income and our age as this might give us more insight as to whether or not these two factors influence employee retention overall.


```r
hist(talentData$MonthlyIncm,
     xlab="Monthly Income",
     ylab="Frequency Of Occurrence",
     main= "Income Distribution Frequency",
     col= "grey")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

From the above chart we can see that there is a right skewed distribution for our Monthly Income in our dataset. It is also clear that the majority of the population in this dataset makes between \$1000 and $6000 per month. The higher we go out in income the more the distribution becomes narrower.

##### Exploring the Relationship between Years At a company and Satisfaction

Now that we know that Age, and Income have a positive impact on employee retention we would like to visually confirm our assumption that Job Satisfaction also contributes in a major way to someone remaining at a company. We can do this by examining our different levels of employee satisfaction and their Years they have remained at a particular company.


```r
ggplot(talentData, aes(YrsAtCompany)) +
  geom_density(aes(fill=JobSatfctn), alpha=0.8) +
  labs(title= "Years At Company Density Plot",
       subtitle="Years at Company grouped by Job Satisfaction",
       x="Years at Company",
       y="Density")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

The Chart above is very telling. We take a look at our probability distribution across different Job Satisfaction levels. 1 indicates that there is low employee job satisfaction, and 4 represents that there is really high employee job satisfaction. If we examine the probability of each within the context of the years an individual stays at a company it becomes clear that lower job satisfaction indicates that this catagory has the lowest number of years spent at a company. This is no surprise, but it does give us more infomration regarding negative factors to employee attrition.

##### Correlation Plot of TalentData

In our data set there are a large number of numerical based values. We would like to get an idea of the relationship of those variables relate to one another in one glance. Below is a comprised chart of all the correlations regarding our talent data.


```r
library(ggcorrplot)

continuous_vars <- talentData[, c("YrsWthCurMgr",
                                  "YrsSncLstPrn",
                                  "YrsInCrntRl",
                                  "YrsAtCompany",
                                  "TrngTmsLstYr",
                                  "TtlWrkngYrs",
                                  "PrcntSalHike",
                                  "MonthlyIncm",
                                  "HourlyRate",
                                  "DailyRate",
                                  "Age",
                                  "DistFromHome",
                                  "YrsOfEdu")]

correlations <- round(cor(continuous_vars), 1)

ggcorrplot(correlations, hc.order = TRUE,
           type = "lower",
           lab = TRUE,
           lab_size = 4,
           method="circle",
           colors= c("tomato2", "white", "springgreen3"),
           title = "Correlation Chart For TalentData",
           ggtheme=theme_bw)
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

The chart above shows us that there are no negative linear relationships in our data between our variables. We can also see that there are some positive relationships between variables that are linearly correlated and we have now been able to narrow these down so they can be examined in depth.


Let's check if there is any relationship between Age and Income. Does Gender makes any effect on the Monthly income?


```r
MonthlyIncm <- talentData$MonthlyIncm
Age <- talentData$Age
Gender <- talentData$Gender
ggplot(talentData, aes(MonthlyIncm, Age, color = Gender, shape=Gender))+geom_point()+ggtitle("Correlation between Monthly income and Ages")
```

![](DDSAnalyticsReport_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

```r
model_AgeIncome <- lm(MonthlyIncm ~ Age+Gender, data = talentData)
summary(model_AgeIncome)
```

```
## 
## Call:
## lm(formula = MonthlyIncm ~ Age + Gender, data = talentData)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -9927.2 -2623.9  -711.1  1817.3 12595.1 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -2872.67     475.14  -6.046 1.88e-09 ***
## Age           256.12      11.85  21.616  < 2e-16 ***
## GenderMale   -134.31     218.91  -0.614     0.54    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4096 on 1459 degrees of freedom
## Multiple R-squared:  0.2434,	Adjusted R-squared:  0.2424 
## F-statistic: 234.7 on 2 and 1459 DF,  p-value: < 2.2e-16
```
####4.C####
From regression analysis above we can say that Gender does not make significant change in the Monthly employee income. But Age is indeed significant variable (p<0.0001), it can explain 24% of monthly income change.

#### What Factors Cause Employee Turnover?

Our goal is to determine which indicators might lead to employee attrition. The best way for us to find what causes this is to study the subset of data points that have the flag `Yes` marked for attrition. Once we have our dataset we will need to determine an appropriate sample size from this population in order to perform ANOVA with a good statistical power.


```r
attrition_set <- filter(talentData, Attrition == "Yes")
```

##### Determine Sample Size

First, we want to get a good idea of the sample size needed in order to lower the chances of a Type I or Type II error.


```r
library(pwr)

pwr.anova.test(k=2, f=0.5, sig.level=0.05, power=0.8)
```

```
## 
##      Balanced one-way analysis of variance power calculation 
## 
##               k = 2
##               n = 16.71472
##               f = 0.5
##       sig.level = 0.05
##           power = 0.8
## 
## NOTE: n is number in each group
```

We decided to go with a comparison for two groups with an effect size of `0.5` because we are dealing with a medium size dataset. In addition to that we want to use a significance level of `0.05` which will be based on a 95% confidence level. Finally, the power level we set is `0.8`. Based on our calculation we will need at least 17 samples from each group to have good results that will limit our Type I and Type II error types.

Now that we know our sample size, we separate them into two groups. The two groups are randomly chosen observations that had an Attrition value of Yes and the other group are random samples that had an attrition value of No.


```r
group1 <- sample_n(filter(talentData, Attrition == "Yes"), size = 16)
group2 <- sample_n(filter(talentData, Attrition == "No"), size = 16)


study_set <- rbind(group1, group2)
```

##### Assumptions

Below are a list of Assumptions we will proceed this test under

1. `Random Sample`: Our Data was indeed sampled randomly from the dataset using computation, therefore every data point had equal opportunity of being chosen.
2. `Independent Observations`: It is assumed that all the data points within the population are independent of each other. No employee data is assumed to affect the outcome of another employee based on the variables that are within our model. As a result we can assume this assumption has not been violated.
3. `Equal Variances`: In order to determine whether or not the variances were equal we performed a lavene test on the logged incomes to be sure there is no difference
4. `Normality` : Based on our EDA we have discovered that our data has come from a normaly distributed population due to a large sample size which allows for the central limit theorem to kick in..
5. `Equal Sample Size`: Sample size is set at 16 for each group.


```r
model <- aov(DailyRate + MonthlyIncm + YrsAtCompany + YrsInCrntRl + YrsWthCurMgr + MonthlyRate + DistFromHome + Age ~ Attrition, data = study_set)
summary(model)
```

```
##             Df    Sum Sq  Mean Sq F value Pr(>F)
## Attrition    1 3.749e+07 37489141   0.739  0.397
## Residuals   30 1.522e+09 50743941
```

If we check for differnces in each group of those that experienced Attrition and those that did not we can see that there is no significant difference between the groups based on the `Daily Rate`, `YearsAtCompany`, `YrsInCorntRl`, `YrsWithCurMgr`, `MonthlyRate` , `DistFromHome` and `Age`!. None of these variables showed any type of difference between the two groups at the 0.05 level of significance. Therefore we can fail to reject the hypothesis that there is some kind of a differnece in those that experienced attrition over those that did not.

Now that we know there is no difference between the two groups we will proceed to try finding the most relevant variables in finding employee attrition another way. Next we prepare our data for use in a general linear model. We take this approach because we would like to see what the variables are that might help us with determining the outcome of what makes an employee decide to leave his or her job at a higher rate than others.


```r
library(dummies)
```

```
## dummies-1.5.6 provided by Decision Patterns
```

```r
encoded_dataset <- dummy.data.frame(as.data.frame(talentData), names=c("BusinessTrvl", "Department", "EduField",
                                                             "EmployeeCnt", "EnvSatfctn", "Gender",
                                                             "JobInvolmnt", "JobLevel", "JobRole",
                                                             "JobSatfctn", "MaritalStat", "OverTime",
                                                             "PerfRating", "RlnSatfctn", "StockOptLvl",
                                                             "WrkLifeBal"))
encoded_dataset <- encoded_dataset %>% mutate(Attrition = ifelse(Attrition == "Yes", 1 , 0))
```


Now that our data is encoded properly we will try locating the significant variables using the General Linear Model approach



```r
glm_model <- glm(formula=Attrition~.,data=encoded_dataset)

summary(glm_model)
```

```
## 
## Call:
## glm(formula = Attrition ~ ., data = encoded_dataset)
## 
## Deviance Residuals: 
##      Min        1Q    Median        3Q       Max  
## -0.57128  -0.20363  -0.07768   0.09682   1.14256  
## 
## Coefficients: (15 not defined because of singularities)
##                                      Estimate Std. Error t value Pr(>|t|)
## (Intercept)                         7.773e-01  1.826e-01   4.256 2.22e-05
## Age                                -3.204e-03  1.304e-03  -2.457 0.014121
## `BusinessTrvlNon-Travel`           -6.689e-02  2.833e-02  -2.361 0.018340
## BusinessTrvlTravel_Frequently       8.714e-02  2.152e-02   4.050 5.41e-05
## BusinessTrvlTravel_Rarely                  NA         NA      NA       NA
## DailyRate                          -3.087e-05  2.085e-05  -1.480 0.138977
## `DepartmentHuman Resources`        -8.039e-02  1.190e-01  -0.675 0.499554
## `DepartmentResearch & Development`  3.209e-02  6.936e-02   0.463 0.643655
## DepartmentSales                            NA         NA      NA       NA
## DistFromHome                        4.147e-03  1.032e-03   4.020 6.12e-05
## YrsOfEdu                            5.067e-03  8.386e-03   0.604 0.545781
## `EduFieldHuman Resources`           1.828e-02  8.581e-02   0.213 0.831374
## `EduFieldLife Sciences`            -9.458e-02  3.056e-02  -3.095 0.002010
## EduFieldMarketing                  -5.503e-02  4.122e-02  -1.335 0.182002
## EduFieldMedical                    -1.087e-01  3.162e-02  -3.437 0.000605
## EduFieldOther                      -1.091e-01  4.493e-02  -2.428 0.015293
## `EduFieldTechnical Degree`                 NA         NA      NA       NA
## EmployeeNum                        -7.759e-06  1.393e-05  -0.557 0.577757
## EnvSatfctn1                         1.260e-01  2.430e-02   5.184 2.49e-07
## EnvSatfctn2                         1.447e-02  2.439e-02   0.594 0.552917
## EnvSatfctn3                        -7.351e-04  2.127e-02  -0.035 0.972436
## EnvSatfctn4                                NA         NA      NA       NA
## GenderFemale                       -2.785e-02  1.709e-02  -1.630 0.103381
## GenderMale                                 NA         NA      NA       NA
## HourlyRate                         -9.044e-05  4.110e-04  -0.220 0.825863
## JobInvolmnt1                        2.250e-01  4.402e-02   5.111 3.64e-07
## JobInvolmnt2                        7.582e-02  3.143e-02   2.412 0.015984
## JobInvolmnt3                        3.728e-02  2.876e-02   1.296 0.195211
## JobInvolmnt4                               NA         NA      NA       NA
## JobLevel1                          -1.204e-01  1.187e-01  -1.014 0.310795
## JobLevel2                          -2.481e-01  1.018e-01  -2.438 0.014908
## JobLevel3                          -1.362e-01  7.925e-02  -1.718 0.086024
## JobLevel4                          -1.124e-01  5.545e-02  -2.028 0.042779
## JobLevel5                                  NA         NA      NA       NA
## `JobRoleHealthcare Representative` -1.678e-01  8.737e-02  -1.921 0.054991
## `JobRoleHuman Resources`           -4.825e-02  1.248e-01  -0.386 0.699230
## `JobRoleLaboratory Technician`     -1.264e-01  8.004e-02  -1.579 0.114473
## JobRoleManager                     -1.505e-01  8.916e-02  -1.688 0.091592
## `JobRoleManufacturing Director`    -1.506e-01  8.699e-02  -1.731 0.083699
## `JobRoleResearch Director`         -2.165e-01  1.030e-01  -2.103 0.035623
## `JobRoleResearch Scientist`        -2.199e-01  7.973e-02  -2.758 0.005886
## `JobRoleSales Executive`           -4.887e-02  5.036e-02  -0.970 0.331984
## `JobRoleSales Representative`              NA         NA      NA       NA
## JobSatfctn1                         1.201e-01  2.393e-02   5.020 5.84e-07
## JobSatfctn2                         5.797e-02  2.431e-02   2.385 0.017210
## JobSatfctn3                         5.360e-02  2.132e-02   2.514 0.012037
## JobSatfctn4                                NA         NA      NA       NA
## MaritalStatDivorced                -3.610e-02  3.673e-02  -0.983 0.325873
## MaritalStatMarried                 -2.866e-02  2.966e-02  -0.966 0.334119
## MaritalStatSingle                          NA         NA      NA       NA
## MonthlyIncm                        -9.972e-06  7.913e-06  -1.260 0.207824
## MonthlyRate                         7.034e-07  1.173e-06   0.600 0.548803
## NumCmpWorked                        1.850e-02  3.742e-03   4.944 8.58e-07
## OverTimeNo                         -2.099e-01  1.859e-02 -11.291  < 2e-16
## OverTimeYes                                NA         NA      NA       NA
## PrcntSalHike                       -6.310e-04  3.610e-03  -0.175 0.861264
## PerfRating3                        -9.834e-03  3.637e-02  -0.270 0.786910
## PerfRating4                                NA         NA      NA       NA
## RlnSatfctn1                         9.118e-02  2.466e-02   3.698 0.000226
## RlnSatfctn2                         2.191e-02  2.407e-02   0.910 0.362988
## RlnSatfctn3                         1.611e-02  2.158e-02   0.746 0.455507
## RlnSatfctn4                                NA         NA      NA       NA
## StockOptLvl0                        4.542e-02  4.451e-02   1.020 0.307780
## StockOptLvl1                       -5.806e-02  3.748e-02  -1.549 0.121574
## StockOptLvl2                       -5.689e-02  4.317e-02  -1.318 0.187708
## StockOptLvl3                               NA         NA      NA       NA
## TtlWrkngYrs                        -3.505e-03  2.407e-03  -1.456 0.145576
## TrngTmsLstYr                       -1.098e-02  6.515e-03  -1.685 0.092201
## WrkLifeBal1                         1.066e-01  4.434e-02   2.403 0.016369
## WrkLifeBal2                        -1.054e-02  3.121e-02  -0.338 0.735709
## WrkLifeBal3                        -5.113e-02  2.803e-02  -1.824 0.068337
## WrkLifeBal4                                NA         NA      NA       NA
## YrsAtCompany                        5.286e-03  2.941e-03   1.797 0.072517
## YrsInCrntRl                        -7.403e-03  3.835e-03  -1.931 0.053718
## YrsSncLstPrn                        9.218e-03  3.362e-03   2.742 0.006191
## YrsWthCurMgr                       -7.785e-03  3.918e-03  -1.987 0.047089
##                                       
## (Intercept)                        ***
## Age                                *  
## `BusinessTrvlNon-Travel`           *  
## BusinessTrvlTravel_Frequently      ***
## BusinessTrvlTravel_Rarely             
## DailyRate                             
## `DepartmentHuman Resources`           
## `DepartmentResearch & Development`    
## DepartmentSales                       
## DistFromHome                       ***
## YrsOfEdu                              
## `EduFieldHuman Resources`             
## `EduFieldLife Sciences`            ** 
## EduFieldMarketing                     
## EduFieldMedical                    ***
## EduFieldOther                      *  
## `EduFieldTechnical Degree`            
## EmployeeNum                           
## EnvSatfctn1                        ***
## EnvSatfctn2                           
## EnvSatfctn3                           
## EnvSatfctn4                           
## GenderFemale                          
## GenderMale                            
## HourlyRate                            
## JobInvolmnt1                       ***
## JobInvolmnt2                       *  
## JobInvolmnt3                          
## JobInvolmnt4                          
## JobLevel1                             
## JobLevel2                          *  
## JobLevel3                          .  
## JobLevel4                          *  
## JobLevel5                             
## `JobRoleHealthcare Representative` .  
## `JobRoleHuman Resources`              
## `JobRoleLaboratory Technician`        
## JobRoleManager                     .  
## `JobRoleManufacturing Director`    .  
## `JobRoleResearch Director`         *  
## `JobRoleResearch Scientist`        ** 
## `JobRoleSales Executive`              
## `JobRoleSales Representative`         
## JobSatfctn1                        ***
## JobSatfctn2                        *  
## JobSatfctn3                        *  
## JobSatfctn4                           
## MaritalStatDivorced                   
## MaritalStatMarried                    
## MaritalStatSingle                     
## MonthlyIncm                           
## MonthlyRate                           
## NumCmpWorked                       ***
## OverTimeNo                         ***
## OverTimeYes                           
## PrcntSalHike                          
## PerfRating3                           
## PerfRating4                           
## RlnSatfctn1                        ***
## RlnSatfctn2                           
## RlnSatfctn3                           
## RlnSatfctn4                           
## StockOptLvl0                          
## StockOptLvl1                          
## StockOptLvl2                          
## StockOptLvl3                          
## TtlWrkngYrs                           
## TrngTmsLstYr                       .  
## WrkLifeBal1                        *  
## WrkLifeBal2                           
## WrkLifeBal3                        .  
## WrkLifeBal4                           
## YrsAtCompany                       .  
## YrsInCrntRl                        .  
## YrsSncLstPrn                       ** 
## YrsWthCurMgr                       *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.09833113)
## 
##     Null deviance: 195.87  on 1461  degrees of freedom
## Residual deviance: 137.76  on 1401  degrees of freedom
## AIC: 819.68
## 
## Number of Fisher Scoring iterations: 2
```

Based on a 0.05 level of significance the top factors contributing to Attrition in the data set are listed in the table below

| Significant Variables at 0.05 Alpha           | P-value  | 95% ConfidenceInterval |
|-----------------------------------------------|----------|------------------------|
| BusinessTrvlTravel_Frequently                 | 5.41e-05 | None As it is a Factor |
| DistFromHome                                  | 6.12e-05 | 2.13 to 6.16           |
| EduFieldMedical                               | 0.000605 | None As it is a Factor |
| EnvSatfctn1                                   | 2.49e-07 | None As it is a Factor |
| JobInvolmnt1                                  | 3.64e-07 | None As it is a Factor |
| JobSatfctn1                                   | 5.84e-07 | None As it is a Factor |
| NumCmpWorked                                  | 8.58e-07 | 1.1 to 2.6             |
| OverTimeNo                                    | < 2e-16  | None As it is a Factor |
| RlnSatfctn1                                   | 0.000226 | None As it is a Factor |


## V. Discussion And Conclusions

After extensive statistical analysis we have been able to conclude that there are indeed several factors that lead to the attrition of employees. Based on what these factors are there are things the business can do to make it much harder for someone to decide if they want to leave a company. We have compiled a list of recommendations that DDSAnalytics can follow to help reduce Attrition. It should be stated that the following factors below will not guarantee employee Attrition will stop, but it will increase the chances of slowing Attrition at an organization.

#### Limit Business Travel

We found that Frequent business travel was a major contributor to churn in the dataset. If a company wants to reduce the the chances of someone wanting to leave a specific job they should make sure that worker has a reduced responsiblity to travel as it could make all the difference in deciding whether to change companies.

#### Consider Remote Work

Based on studying the significance of the distance traveled from home to get to work i.e. commuting we found that this is an extremely significant factor. Based on a 95% confidence Interval the optimal distance is somewhere between 2 miles to 6 miles. If an employee has to travel more than that one should consider offering a remote option in order to limit attrition due to the Distance from Home.

#### Consider Hiring people that worked for less Companies

After studying the data we found that the ideal number of companies worked for those that did experience  attrition was 1 to 3 companies on a 95% confidence interval. This indicates that people that work for multiple companies are more likely to contribute to the Attrition rate. This is an extreme solution, but one should consider the amount of companies a potential employee worked before hiring them, as it might be a key predictor as to whether or not that individual will stay or leave.

#### Satisfaction Indicators

We found that Environment Satisfaction Level 1, Job Invovlment Level 1, and Job Satisfaction Level 1 all contributed to employee churn in a major way. This indicates that management should consider doing things to make the work environment more comfortable so that the employees feel great about going to work every day. Employees also need to feel heavily involved in their job in as well as be satisfied doing it. It is important to conduct reviews and surveys to find out how employees feel in these areas so that an overall general pulse can be gathered on how the company is performing here.

#### Understand How workers feel about Overtime

We found that Not having overtime was very significant in determining employee attrition. This might indicate that management should limit the amount of times they ask employees to pick up extra hours, or only consider asking those that need the extra hours for personal reasons. This can go a long way into contributing to employee attrition.

#### Work relationships must be maintained

Employees consider work relationships to be an extremeley important factor and it also contributes to employee attrition. It makes sense to have relationship building events that improves ties within employee to employee relationships. People generally have to like who they work with, and management can improve this by tracking how their employees are relating to each other on the job. Management should consider improving situations that cause bad relationships between workers.

## References

[Forbes "True Or False Employees Today only stay one or Two Years : David Sturt and Todd Nordstrom "](https://www.forbes.com/sites/davidsturt/2016/01/13/true-or-false-employees-today-only-stay-one-or-two-years/#6736606b6b4c)

