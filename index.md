---
title       : Elastic R API
subtitle    : Data Science Team Weekly Sync 2015-04-24
author      : Summit Suen
job         : Etu
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Install 


```r
## Install from CRAN
install.packages("devtools")
## Or install development version:
devtools::install_github("ropensci/elastic")

library('elastic')
```

---

## Connect


```r
connect()
```

---

## Get Data

- Sample data provided by elastic package, use bulk api to put json file into elasticsearch


```r
shakespeare <- system.file("examples", "shakespeare_data.json", package = "elastic")
docs_bulk(shakespeare)
```

---

## Search


```r
out <- Search(index="shakespeare")
out$hits$total
```

---

## Modeling


```r
library(tm)
```

```
## Loading required package: NLP
## 
## Attaching package: 'NLP'
## 
## The following object is masked from 'package:ggplot2':
## 
##     annotate
```
