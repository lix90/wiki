---
title: "forcats"
date: 2017-03-18
tag: rpackage,factor
description: "类别/因子"
collection: R包
---

# forcats

[forcats](https://github.com/tidyverse/forcats) 一个用于操作分类变量／因子的R包。

``` r
install.packages("forcats")
devtools::install_github("tidyverse/forcats")
```

`forcats::fct_recode()` 对指定的因子的水平重新编码。

``` r
. %>%
  mutate(
    fct = fct_recode(fct, "level_label2" = "level1", "level_label2" = "level2")
  )
```
