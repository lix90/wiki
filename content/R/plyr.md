---
title: "plyr"
date: 2017-03-22
tag: rpackage
collection: R包
---

# plyr

split 分割：让复杂的问题分解成小块
apply 套用：对每一个小块进行计算
combine 组合：汇集每一小块的结果

plyr 函数命名规律与输入对象类型和输出对象类型有关，有以下几种数据对象类型：
- a = array
- l = list
- d = data.frame
- m = multiple inputs
- r = repeat multiple times
- _ = nothing

plyr 对于常见的数据分析问题提供了一系列辅助函数：
- arrange: 重新排序
- mutate: 增加新列，或者修改已存在的列，并将修改后的指派为新列
- summarise: 类似 mutate，但是新创建一个 data frame，不保存旧的 data frame 中的列
- join:
- match_df
- colwise
- rename: 修改 data frame 的列名
- round_any
- count: 快速计数，并返回 data frame
