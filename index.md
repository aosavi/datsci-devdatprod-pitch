---
title       : Predicting Happiness
subtitle    : Pitch for course project Data Science - Developing Data Products
author      : Alexander Savi
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Disclaimer

This presentation is part of a project for the Data Science Developing Data Products track from Coursera.

The course can be found at: https://class.coursera.org/devdataprod-002

The Shiny app this pitch refers to can be found at: https://aosavi.shinyapps.io/datsci-devdatprod/

---

## Shiny app

A Shiny app was built and hosted on shinyapps.io, see https://aosavi.shinyapps.io/datsci-devdatprod/

This app uses a `state-of-the-art' algorithm to quantify happiness as a result of a sleep drug taken and the side of the bed one gets out.

The user may select the NotSoSuperSleep(TM) drug or the SuperSleep(TM) drug, and the wrong or the right side of the bed. From these to predictors an 'insanely accurate' prediction of happiness (informal studies) is calculated.

---

## Technology

The algorithm takes the mean amount of extra sleep that participants from two empirical samples had after taking one of two different drugs (see help(sleep) in R for details).

The means are then divided by either a 'wrong side' factor (2) or a 'right side' factor (1/2).

The algorithm spits out the predicted happiness for each of the 4 circumstances. Please note that a higher prediction refers to more happiness.

---

## Example

An example prediction is shown here, where the SuperSleep(TM) drug is taken, but unfortunately the wrong side of the bed was used.


```r
drug <- "SuperSleep(TM)"
side <- "Wrong side"
```


```r
data(sleep)
expHappiness <- function(drug, side) {
        if(drug=="NotSoSuperSleep(TM)") drug <- 1
        if(drug=="SuperSleep(TM)") drug <- 2
        if(side=="Wrong side") side <- 2
        if(side=="Right side") side <- 1/2
        mean(sleep[sleep[,"group"]==drug, "extra"]) / side
}
pred <- expHappiness(drug, side)
```

The predicted happiness the following day is a rather suboptimal 1.165.
