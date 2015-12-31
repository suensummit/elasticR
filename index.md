---
title       : Elastic R API Demo
subtitle    : Elasticsearch Workshop
author      : Summit Suen
job         : 木刻思股份有限公司
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
require('elastic')
# load("es.RData")
# connect(es_base = base, es_port = port)
connect()
```

```
## url:       http://127.0.0.1 
## port:      9200 
## username:  NULL 
## password:  NULL 
## errors:    simple 
## Elasticsearch (ES) details:   
##    name:                    Night Nurse 
##    ES version:              2.1.1 
##    ES version timestamp:    2015-12-15T13:05:55Z 
##    ES build hash:           40e2c53a6b6c2972b3d13846e450e66f4375bd71 
##    lucene version:          5.3.1
```

```r
# default base = "http://127.0.0.1" and default port = 9200
```

---

## Get Data

- Sample data provided by elastic package, use bulk api to put json file into elasticsearch


```r
shakespeare <- system.file("examples", "shakespeare_data.json", package = "elastic")
aliases_get()
```

```
## $shakespeare
## $shakespeare$aliases
## named list()
## 
## 
## $.kibana
## $.kibana$aliases
## named list()
```

---

## Get Data

- Sample data provided by elastic package, use bulk api to put json file into elasticsearch


```r
index_delete(index = "shakespeare")
```

```
## http://127.0.0.1:9200/shakespeare
```

```
## $acknowledged
## [1] TRUE
```

```r
aliases_get()
```

```
## $.kibana
## $.kibana$aliases
## named list()
```

---

## Get Data

- Sample data provided by elastic package, use bulk api to put json file into elasticsearch


```r
res <- docs_bulk(shakespeare)
res$items[[length(res$items)]]
```

```
## $index
## $index$`_index`
## [1] "shakespeare"
## 
## $index$`_type`
## [1] "line"
## 
## $index$`_id`
## [1] "4999"
## 
## $index$`_version`
## [1] 5
## 
## $index$`_shards`
## $index$`_shards`$total
## [1] 2
## 
## $index$`_shards`$successful
## [1] 1
## 
## $index$`_shards`$failed
## [1] 0
## 
## 
## $index$status
## [1] 200
```

---

## Get Data

- Sample data provided by elastic package, use bulk api to put json file into elasticsearch


```r
aliases_get()
```

```
## $shakespeare
## $shakespeare$aliases
## named list()
## 
## 
## $.kibana
## $.kibana$aliases
## named list()
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
out$hits$hits[[2]]$`_source`$speaker
```

```
## [1] "KING HENRY IV"
```

```r
out$hits$hits[[2]]$`_source`$text_entry
```

```
## [1] "Did lately meet in the intestine shock"
```

