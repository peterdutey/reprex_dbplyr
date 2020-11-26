---
title: "testdplyr"
output: 
  html_document: 
    keep_md: yes
---

 

```r
packageVersion("DBI")
```

```
## [1] '1.1.0'
```

```r
packageVersion("RSQLite")
```

```
## [1] '2.2.1'
```

```r
packageVersion("dbplyr")
```

```
## [1] '2.0.0.9000'
```

```r
packageVersion("dplyr")
```

```
## [1] '1.0.2'
```

```r
temp_db <- DBI::dbConnect(RSQLite::SQLite(), ":memory:")
dbplyr::db_copy_to(
  con = temp_db,
  table = "mydata",
  values = data.frame(data=1:5),
  overwrite = TRUE,
  temporary = FALSE
)
```

```
## [1] "mydata"
```

```r
try({dbplyr::db_copy_to(
  con = temp_db,
  table = "mydata",
  values = data.frame(data=6:10),
  overwrite = TRUE,
  temporary = FALSE
)})
```

```
## Error : table 'mydata' already exists
```



```r
DBI::dbWriteTable(
  conn = temp_db,
  name = "mydata",
  value = data.frame(data=6:10),
  overwrite = TRUE,
  temporary = FALSE
)
```
 
