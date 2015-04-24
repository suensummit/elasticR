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
```

---

## Connect


```r
library('elastic')
load("es.RData")
connect(es_base = base, es_port = port)
```

```
## uri:       http://104.236.193.82 
## port:      9200 
## username:  NULL 
## password:  NULL 
## elasticsearch details:   
##    status:                  200 
##    name:                    Pretty Persuasions 
##    Elasticsearch version:   1.4.4 
##    ES version timestamp:    2015-02-19T13:05:36Z 
##    lucene version:          4.10.3
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

```
## [1] 5000
```

---

## Query


```r
out <- Search(index="shakespeare", type="act", q="speaker:KING HENRY IV")
out$hits[[1]]
```

```
## [1] 9
```

```r
out$hits$total
```

```
## [1] 9
```

---

## Query

- Query DSL searches - queries sent in the body of the request


```r
aggs <- '{"aggs":{"stats":{"terms":{"field":"text_entry"}}}}'
out <- Search(index="shakespeare", body=aggs)
out$hits$hits[[1]]$`_source`$speaker
```

```
## [1] "KING HENRY IV"
```

```r
out$hits$hits[[1]]$`_source`$text_entry
```

```
## [1] "Find we a time for frighted peace to pant,"
```

