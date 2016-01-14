---
title       : "Heart Disease Prediction"
subtitle    : "A shiny Application"
author      : "Gurmeet Singh"
job         : "Budding Data Scientist"
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

1. [Application] (https://swiftgurmeet.shinyapps.io/coursera-ddp-project) to predict heart disease
2. Uses SAheart data set from "ElemStatLearn" package
3. Two models used: GLM and randomForest
4. Sliders and Checkbox used in GUI for "risk" factors
5. The GLM model predicts real valued "risk"
6. The Random Forest model predicts binary 0/1 outcome
7. The app takes some time to build models before it becomes interactive

--- .class #id 

## Data Set sample




```r
#The actual data is contained "inline" in the code at the end of the Rmd file.
head(SAheart)
```

```
##   sbp tobacco  ldl famhist alcohol age chd
## 1 160   12.00 5.73 Present   97.20  52   1
## 2 144    0.01 4.41  Absent    2.06  63   1
## 3 118    0.08 3.48 Present    3.81  46   0
## 4 170    7.50 6.41 Present   24.26  58   1
## 5 134   13.60 3.50 Present   57.34  49   1
## 6 132    6.20 6.47 Present   14.14  45   0
```
-  Fit a GLM and a Random Forest Model

```r
glmFit <- glm(chd ~ ., data=SAheart)
rfFit <- train(as.factor(chd) ~ ., method = "rf", data=SAheart, family="binomial")
```

--- .class #id 

## Predict a lower risk case

```r
predict(glmFit,data.frame(sbp=110,tobacco=0,ldl=4,famhist="Absent",alcohol=0,age=30))[[1]]
```

```
## [1] 0.07747464
```

```r
predict(rfFit,data.frame(sbp=110,tobacco=0,ldl=4,famhist="Absent",alcohol=0,age=30))[[1]]
```

```
## [1] 0
## Levels: 0 1
```


--- .class #id 

## Predict a higher risk case

```r
predict(glmFit,data.frame(sbp=150,tobacco=50,ldl=10,famhist="Present",alcohol=50,age=80))[[1]]
```

```
## [1] 1.658998
```

```r
predict(rfFit,data.frame(sbp=150,tobacco=50,ldl=10,famhist="Present",alcohol=50,age=80))[[1]]
```

```
## [1] 1
## Levels: 0 1
```





