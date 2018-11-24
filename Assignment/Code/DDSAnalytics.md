Talent Management Solutions for DDS Analytics
================
Satish, Tyler, Lieng, James
November 23, 2018

**GitHub**:<https://github.com/HammerLynch/MSDS6306_Case_Study_2>

### R-version info

Environment information where the code was executed.

``` r
# R Version Used:
R.version
```

    ##                _                           
    ## platform       x86_64-w64-mingw32          
    ## arch           x86_64                      
    ## os             mingw32                     
    ## system         x86_64, mingw32             
    ## status                                     
    ## major          3                           
    ## minor          5.1                         
    ## year           2018                        
    ## month          07                          
    ## day            02                          
    ## svn rev        74947                       
    ## language       R                           
    ## version.string R version 3.5.1 (2018-07-02)
    ## nickname       Feather Spray

### Libraries and Initial Data Prepration

R Libraries required for the proejct

-   plyr
-   dplyr
-   tidyr
-   ggplot2

Once the libraries are loaded, the data sets are loaded and prepared for further analysis.

``` r
require(plyr)
```

    ## Loading required package: plyr

``` r
require(dplyr)
```

    ## Loading required package: dplyr

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:plyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
require(tidyr)
```

    ## Loading required package: tidyr

``` r
require(ggplot2)
```

    ## Loading required package: ggplot2

``` r
require(gridExtra)
```

    ## Loading required package: gridExtra

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

``` r
# download data 2.a
data <- read.csv("C:/Users/Satish Mylapore/Documents/SMU/MSDS 6306/Homework/CaseStudy2/CaseStudy2_2_2_2/data.csv")
```

### 1. Formulate your Repo

**a** The client wants this to be reproducible and know exactly what you did. There needs to be an informative Readme, complete with several sections, as referenced in Live Session. Give contact information, session Info, and the objective of the repo at least.
**b** You have a large data set, and it needs its own Codebook, formatted in an approachable way. Make sure you describe peculiarities of the data by variable and what needs transforming. However, do not make it too long either. **c** Create a file structure that is accessible and transparent. Document it in the root directory, ideally in the Readme.

``` r
#Setting up seed for reproducible results
set.seed(2018)
# R Version Used:
R.version
```

    ##                _                           
    ## platform       x86_64-w64-mingw32          
    ## arch           x86_64                      
    ## os             mingw32                     
    ## system         x86_64, mingw32             
    ## status                                     
    ## major          3                           
    ## minor          5.1                         
    ## year           2018                        
    ## month          07                          
    ## day            02                          
    ## svn rev        74947                       
    ## language       R                           
    ## version.string R version 3.5.1 (2018-07-02)
    ## nickname       Feather Spray

``` r
# Session information
sessionInfo()
```

    ## R version 3.5.1 (2018-07-02)
    ## Platform: x86_64-w64-mingw32/x64 (64-bit)
    ## Running under: Windows 10 x64 (build 17134)
    ## 
    ## Matrix products: default
    ## 
    ## locale:
    ## [1] LC_COLLATE=English_United States.1252 
    ## [2] LC_CTYPE=English_United States.1252   
    ## [3] LC_MONETARY=English_United States.1252
    ## [4] LC_NUMERIC=C                          
    ## [5] LC_TIME=English_United States.1252    
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ## [1] gridExtra_2.3 ggplot2_3.0.0 tidyr_0.8.1   dplyr_0.7.6   plyr_1.8.4   
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Rcpp_0.12.18     knitr_1.20       bindr_0.1.1      magrittr_1.5    
    ##  [5] munsell_0.5.0    tidyselect_0.2.4 colorspace_1.3-2 R6_2.2.2        
    ##  [9] rlang_0.2.2      stringr_1.3.1    tools_3.5.1      grid_3.5.1      
    ## [13] gtable_0.2.0     withr_2.1.2      htmltools_0.3.6  lazyeval_0.2.1  
    ## [17] yaml_2.2.0       rprojroot_1.3-2  digest_0.6.16    assertthat_0.2.0
    ## [21] tibble_1.4.2     crayon_1.3.4     bindrcpp_0.2.2   purrr_0.2.5     
    ## [25] glue_1.3.0       evaluate_0.11    rmarkdown_1.10   stringi_1.1.7   
    ## [29] compiler_3.5.1   pillar_1.3.0     scales_1.0.0     backports_1.1.2 
    ## [33] pkgconfig_2.0.2

### 2. Clean your Raw Data

**a** Read the csv into R and take a look at the data set. Output how many rows and columns the data.frame is. **b** The column names are either too much or not enough. Change the column names so that they do not have spaces, underscores, slashes, and the like. All column names should be under 12 characters. Make sure you’re updating your codebook with information on the tidied data set as well. **c** Some columns are, due to Qualtrics, malfunctioning.
d Make sure your columns are the proper data types (i.e., numeric, character, etc.). If they are incorrect, convert them.

``` r
#display #row,#cols and fields 2.d (verified the data for data types)
str(data)
```

    ## 'data.frame':    1470 obs. of  35 variables:
    ##  $ Age                     : int  41 49 37 33 27 32 59 30 38 36 ...
    ##  $ Attrition               : Factor w/ 2 levels "No","Yes": 2 1 2 1 1 1 1 1 1 1 ...
    ##  $ BusinessTravel          : Factor w/ 3 levels "Non-Travel","Travel_Frequently",..: 3 2 3 2 3 2 3 3 2 3 ...
    ##  $ DailyRate               : int  1102 279 1373 1392 591 1005 1324 1358 216 1299 ...
    ##  $ Department              : Factor w/ 3 levels "Human Resources",..: 3 2 2 2 2 2 2 2 2 2 ...
    ##  $ DistanceFromHome        : int  1 8 2 3 2 2 3 24 23 27 ...
    ##  $ Education               : int  2 1 2 4 1 2 3 1 3 3 ...
    ##  $ EducationField          : Factor w/ 6 levels "Human Resources",..: 2 2 5 2 4 2 4 2 2 4 ...
    ##  $ EmployeeCount           : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ EmployeeNumber          : int  1 2 4 5 7 8 10 11 12 13 ...
    ##  $ EnvironmentSatisfaction : int  2 3 4 4 1 4 3 4 4 3 ...
    ##  $ Gender                  : Factor w/ 2 levels "Female","Male": 1 2 2 1 2 2 1 2 2 2 ...
    ##  $ HourlyRate              : int  94 61 92 56 40 79 81 67 44 94 ...
    ##  $ JobInvolvement          : int  3 2 2 3 3 3 4 3 2 3 ...
    ##  $ JobLevel                : int  2 2 1 1 1 1 1 1 3 2 ...
    ##  $ JobRole                 : Factor w/ 9 levels "Healthcare Representative",..: 8 7 3 7 3 3 3 3 5 1 ...
    ##  $ JobSatisfaction         : int  4 2 3 3 2 4 1 3 3 3 ...
    ##  $ MaritalStatus           : Factor w/ 3 levels "Divorced","Married",..: 3 2 3 2 2 3 2 1 3 2 ...
    ##  $ MonthlyIncome           : int  5993 5130 2090 2909 3468 3068 2670 2693 9526 5237 ...
    ##  $ MonthlyRate             : int  19479 24907 2396 23159 16632 11864 9964 13335 8787 16577 ...
    ##  $ NumCompaniesWorked      : int  8 1 6 1 9 0 4 1 0 6 ...
    ##  $ Over18                  : Factor w/ 1 level "Y": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ OverTime                : Factor w/ 2 levels "No","Yes": 2 1 2 2 1 1 2 1 1 1 ...
    ##  $ PercentSalaryHike       : int  11 23 15 11 12 13 20 22 21 13 ...
    ##  $ PerformanceRating       : int  3 4 3 3 3 3 4 4 4 3 ...
    ##  $ RelationshipSatisfaction: int  1 4 2 3 4 3 1 2 2 2 ...
    ##  $ StandardHours           : int  80 80 80 80 80 80 80 80 80 80 ...
    ##  $ StockOptionLevel        : int  0 1 0 0 1 0 3 1 0 2 ...
    ##  $ TotalWorkingYears       : int  8 10 7 8 6 8 12 1 10 17 ...
    ##  $ TrainingTimesLastYear   : int  0 3 3 3 3 2 3 2 2 3 ...
    ##  $ WorkLifeBalance         : int  1 3 3 3 3 2 2 3 3 2 ...
    ##  $ YearsAtCompany          : int  6 10 0 8 2 7 1 1 9 7 ...
    ##  $ YearsInCurrentRole      : int  4 7 0 7 2 7 0 0 7 7 ...
    ##  $ YearsSinceLastPromotion : int  0 1 0 3 2 3 0 0 1 7 ...
    ##  $ YearsWithCurrManager    : int  5 7 0 0 2 6 0 0 8 7 ...

``` r
#Change col names less than 12 char 2.b,c
names(data) <- c("Age","Attrition","BusTravel","DailyRate","Department","DistFromHome","Education","EducationFd","EmpCount","EmpNumber","EnvSatis","Gender","HourlyRate","JobInvolvemt","JobLevel","JobRole","JobbSatis","MaritalStat","MntlyIncome","MntlyRate","NumCompWrk","Over18","OverTime","PercSalHike","PerfRating","RelatSatis","StdHrs","StkOptLevel","TotalWrkYrs","TrTmLastYr","WrkLfBalance","YrsAtComp","YrsInCurrRle","YrsSceLstProm","YrsWtCurrMgr")
# cleaning data - removed column Over18 as this column has only value "Y", StdHrs = 80, EmpCount = 1
# lapply(data, function(x) {unique(x)}) # code used to check unique values
data <- subset(data, select = -c(Over18, StdHrs, EmpCount, EmpNumber))
```

### 3. Preliminary Analysis

**a** Remove all observations where the participant is under age 18. No further analysis of underage individuals is permitted by your client. Remove any other age outliers as you see fit, but be sure to tell what you’re doing and why. b Please provide (in table format or similar), descriptive statistics on at least 7 variables (age, Income, etc.). Create **a** simple histogram for two of them. Comment on the shape of the distribution in your markdown. *c* Give the frequencies (in table format or similar) for Gender, Education, and Occupation. They can be separate tables, if that’s your choice. *d* Give the counts (again, table) of management positions.

``` r
# check for data with age less than 18 3.a
data[data$Age < 18,]
```

    ##  [1] Age           Attrition     BusTravel     DailyRate     Department   
    ##  [6] DistFromHome  Education     EducationFd   EnvSatis      Gender       
    ## [11] HourlyRate    JobInvolvemt  JobLevel      JobRole       JobbSatis    
    ## [16] MaritalStat   MntlyIncome   MntlyRate     NumCompWrk    OverTime     
    ## [21] PercSalHike   PerfRating    RelatSatis    StkOptLevel   TotalWrkYrs  
    ## [26] TrTmLastYr    WrkLfBalance  YrsAtComp     YrsInCurrRle  YrsSceLstProm
    ## [31] YrsWtCurrMgr 
    ## <0 rows> (or 0-length row.names)

``` r
#Inspection the significant features and identifying 7 important variables that impacts the response variable (Attrition)
data.glm <- glm(Attrition ~., data = data, family = "binomial")
data.glm.reduced <- glm(Attrition ~ YrsSceLstProm + OverTime + NumCompWrk + MaritalStat + JobbSatis + JobInvolvemt + EnvSatis + DistFromHome + BusTravel, data = data, family = "binomial")
data.glm.reduced <- glm(Attrition ~ YrsSceLstProm + OverTime + MaritalStat + JobbSatis + JobInvolvemt + EnvSatis + DistFromHome + BusTravel, data = data, family = "binomial")
data.glm.reduced <- glm(Attrition ~ OverTime + MaritalStat + JobbSatis + JobInvolvemt + EnvSatis + DistFromHome + BusTravel, data = data, family = "binomial")

data.7 <- subset(data, select = c(Attrition,OverTime,MaritalStat,JobbSatis,JobInvolvemt,EnvSatis,DistFromHome, BusTravel))
# descriptive statistics on at least 7 variables
summary(data.7)
```

    ##  Attrition  OverTime     MaritalStat    JobbSatis      JobInvolvemt 
    ##  No :1233   No :1054   Divorced:327   Min.   :1.000   Min.   :1.00  
    ##  Yes: 237   Yes: 416   Married :673   1st Qu.:2.000   1st Qu.:2.00  
    ##                        Single  :470   Median :3.000   Median :3.00  
    ##                                       Mean   :2.729   Mean   :2.73  
    ##                                       3rd Qu.:4.000   3rd Qu.:3.00  
    ##                                       Max.   :4.000   Max.   :4.00  
    ##     EnvSatis      DistFromHome                BusTravel   
    ##  Min.   :1.000   Min.   : 1.000   Non-Travel       : 150  
    ##  1st Qu.:2.000   1st Qu.: 2.000   Travel_Frequently: 277  
    ##  Median :3.000   Median : 7.000   Travel_Rarely    :1043  
    ##  Mean   :2.722   Mean   : 9.193                           
    ##  3rd Qu.:4.000   3rd Qu.:14.000                           
    ##  Max.   :4.000   Max.   :29.000

``` r
data.freq <- subset(data, select = c(Gender, Education, JobRole))

gender <- data.freq %>% count(Gender)
Education <- data.freq %>% count(Education)
JobRole <- data.freq %>% count(JobRole)
Education[Education$Education == 1,1] <- "Below College"
Education[Education$Education == 2,1] <- "College"
Education[Education$Education == 3,1] <- "Bachelor"
Education[Education$Education == 4,1] <- "Master"
Education[Education$Education == 5,1] <- "Doctor"

gender
```

    ## # A tibble: 2 x 2
    ##   Gender     n
    ##   <fct>  <int>
    ## 1 Female   588
    ## 2 Male     882

``` r
g <- ggplot(data=gender, aes(x=reorder(Gender, -n), y=n, fill = n)) + geom_bar(stat="identity", color="black", position=position_dodge())+theme_minimal() + ylab("Frequency/Count") + xlab("Gender")
grid.arrange(g)
```

![](DDSAnalytics_files/figure-markdown_github/Question_3-1.png)

``` r
Education
```

    ## # A tibble: 5 x 2
    ##   Education         n
    ##   <chr>         <int>
    ## 1 Below College   170
    ## 2 College         282
    ## 3 Bachelor        572
    ## 4 Master          398
    ## 5 Doctor           48

``` r
e <- ggplot(data=Education, aes(x=reorder(Education, -n), y=n, fill = n)) + geom_bar(stat="identity", color="black", position=position_dodge())+theme_minimal() + ylab("Frequency/Count") + xlab("Education")
grid.arrange(e)
```

![](DDSAnalytics_files/figure-markdown_github/Question_3-2.png)

``` r
JobRole
```

    ## # A tibble: 9 x 2
    ##   JobRole                       n
    ##   <fct>                     <int>
    ## 1 Healthcare Representative   131
    ## 2 Human Resources              52
    ## 3 Laboratory Technician       259
    ## 4 Manager                     102
    ## 5 Manufacturing Director      145
    ## 6 Research Director            80
    ## 7 Research Scientist          292
    ## 8 Sales Executive             326
    ## 9 Sales Representative         83

``` r
j <- ggplot(data=JobRole, aes(x=reorder(JobRole, -n), y=n, fill = n)) + geom_bar(stat="identity", color="black", position=position_dodge())+theme_minimal() + ylab("Frequency/Count") + xlab("Job Role")
grid.arrange(j)
```

![](DDSAnalytics_files/figure-markdown_github/Question_3-3.png)

``` r
# Considering JobRole with Manager/Director as Management Positions
JobRole.Manager <- JobRole[which(JobRole$JobRole == "Manager" | JobRole$JobRole == "Manufacturing Director" | JobRole$JobRole == "Research Director"),]
JobRole.Manager
```

    ## # A tibble: 3 x 2
    ##   JobRole                    n
    ##   <fct>                  <int>
    ## 1 Manager                  102
    ## 2 Manufacturing Director   145
    ## 3 Research Director         80

``` r
jm <- ggplot(data=JobRole.Manager, aes(x=reorder(JobRole, -n), y=n, fill = n)) + geom_bar(stat="identity", color="black", position=position_dodge())+theme_minimal() + ylab("Frequency/Count") + xlab("Managers")
grid.arrange(jm)
```

![](DDSAnalytics_files/figure-markdown_github/Question_3-4.png)

### 4. Deeper Analysis and Visualization

**a** Note: You should make all of these appealing looking. Remember to include things like a clean, informative title, axis labels that are in plain English, and readable axis values that do not overlap. **b** Create bar charts in ggplot or similar. The bars should be in descending order, Use any color palette of your choice other than the default. **c** Is there a relationship between Age and Income? Create a scatterplot and make an assessment of whether there is a relationship. Color each point based on the Gender of the participant. You’re welcome to use lm() or similar functions to back up your claims. **d** What about Life Satisfaction? Create another scatterplot. Is there a discernible relationship there to what?

``` r
ggplot(data=data, aes(x=Age, y=MntlyIncome, col = Gender)) + geom_point() + geom_smooth(method = "lm", aes(fill = Gender)) + geom_density2d()
```

![](DDSAnalytics_files/figure-markdown_github/Question_4-1.png)

``` r
js <- data %>% group_by(Age) %>% count(JobbSatis)
mi <- data %>% group_by(Age) %>% count(WrkLfBalance)

#Work Life Balance
ggplot(data=mi, aes(x=WrkLfBalance, y=n, col = Age)) + geom_point() + geom_smooth(method = "lm", aes(fill = Age)) + geom_density2d()
```

![](DDSAnalytics_files/figure-markdown_github/Question_4-2.png)

``` r
#Job Satisfaction
ggplot(data=js, aes(x=JobbSatis, y=n, col = Age)) + geom_point() + geom_smooth(method = "lm", aes(fill = Age)) + geom_density2d()
```

![](DDSAnalytics_files/figure-markdown_github/Question_4-3.png)

### Conclusion
