---
title: "lubridate"
date: 2017-03-18
tag: rpackage
description: "时间/日期数据"
collection: R包
---

# lubridate

[lubridate](https://github.com/hadley/lubridate) 一个用于处理日期对象的R包

``` r
devtools::install_github("hadley/lubridate")
```

解析日期和时间
`ymd()` `mdy()` `dmy()` `ymd_hms()`

设定和提取信息
`second()` `minute()` `hour()` `day()` `wday()` `yday()` `week()` `month()` `year()` `tz()`

时区的操作
`with_tz()` `force_tz()`

时间间隔 Time Intervals
`interval()` 或者 `%--%`
`int_overlaps()` `int_start()` `int_end()` `int_flip()` `int_shift()`
`int_aligns()` `union()` `intersect()` `setdiff()` `%within%`

对时间的计算 durations & periods

``` r
*s  # for period
d*s  # for duration
e*s  # for exact
leap_year()  # regular year
as.period()
```
