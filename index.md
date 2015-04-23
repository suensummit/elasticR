---
title       : Elastic R API
subtitle    : 2015-04-24
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

```
## Error: 
##   Failed to connect to http://127.0.0.1:9200
##   Remember to start Elasticsearch before connecting
```

---

## Search
