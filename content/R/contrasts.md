---
title: "Making contrasts in R"
date: 2017-03-22
tag: r
---

# 什么是正交的 contrasts？如何建立正交 contrasts？

查看当前的 contrasts：`options("contrasts")`

两种应用 contrasts 的方式：
- 添加 contrasts 到 data.frame 中，那么只要用到 data.frame 来构建模型，contrasts 将每次都将被使用。
- 添加 contrasts 到 model 中，那么在检验模型时就会使用到它的 contrasts，只在检验对应模型是使用一次。

R 中默认的 contrasts 为非等级因子，使用 treatment contrasts (dummy coding)；等级因子使用 polynomial trend contrasts，考察回归系数时有效。

传统的 dummy coding 适用于回归系数，但是并不适用于方差分解，因为 dummy coding 非正交（non-orthogonal）。而且，`aov` 使用 `Type I` 平方和。其他包函数如 `car::Anova` `ez::ezANOVA` `afex::aov_ez` 等支持 `Type III` 平方和。

在进行方差分析时，需要改为 effects codding 或者 orthogonal contrast coding。可以使用 `contr.sum` 函数，或者直接通过 `afex::set_sum_contrasts()`。

使用 `car::Anova` 并不会显示出每个独立的比较，而仅仅显示出每个因子的总效应。可以把模型对象传入函数 `summary(modobj)`，这样就能显示出每个独立的比较的结果。如果使用 `aov` 建立模型，而不是 `lm`，传入 `split` 参数到 `summary` 才能看到比较的结果。`summary(..., split = list(var = list(...), ...))`。其中，split 参数中也可以不包含所有变量的所有水平。

在构建自定义的比较时，需要谨慎，因为 `contrasts` 函数有一些小技巧，特别时当应用 contrast 权重时，需要对 contasts 矩阵进行求逆运算。

以下为构建自定义比较的步骤：
1. Specfiy the weights for your contrasts (and be sure to check the order of the levels of the factor, so your weights will line up properly). 首先指定 contrasts 的权重。
2. Create a temporary matrix with each contrast as one row. The top row (for the constant) should be 1/j for j groups. 构建临时的矩阵，第一列每个元素为 1/j，如果 j 为水平数。使用 `rbind` 构建临时矩阵。
3. Get the inverse of that temporary matrix. 使用 `solve` 函数对临时矩阵求逆。
4. The first column of the inverse will be all 1’s. Drop that first column. The remaining columns are your contrast matrix. 求逆后的矩阵第一列每一个元素都为1，删除第一列，剩余的列即为最终的 contrast 矩阵。然后就可以在建立模型时传入 contrasts 参数 `contrasts = list(...)`。

如果指定的 contrasts 为 orthogonal，每个比较的回归系数应该等于比较的组的均值的差值。

不进行矩阵求逆会出现什么结果呢？如果 contrasts 为正交的，那么对回归系数检验的 t 值和 p 值时没有问题的，但是 contrast estimate 以及对应的标准误可能不等于比较的组的均值的差值。如果 contrasts 不是正交的，那么所得到的结果是无效的。所以，最好是对所有 contasts 权重矩阵进行求逆。

如果进行的比较次数少于 j-1，那么 R 会自动地计算出剩余的正交 contrasts。只不过，此时无法进行矩阵逆运算。不过只要 contrasts 是正交的，那么就不用担心检验的结果。需要考虑的是，contrast estimates 将可能不等于比较的组均值的差值。

需要注意，如果 `lm()` 模型中 contrasts 少于 j-1 次，没有反映在 contrasts 中的组差异将被纳入到误差项中。


> **Orthogonal contrasts** are a set of contrasts in which, for any distinct pair, **the sum of the cross-products of the coefficients is zero** (assume sample sizes are equal). Although there are potentially infinite sets of orthogonal contrasts, within any given set there will always be a maximum of exactly k – 1 possible orthogonal contrasts (where k is the number of group means available).

> There are only k-1 orthogonal comparisons, where k is the number of factor levels.
> Comparisons/contrasts orthogonal to each other are statistically independent.
> Which of the possible comparisons should we conduct? Well, this very much depends on our hypothesis we have in mind.

> We need to specify a contrast matrix, showing which comparisons we want to make. A contrast matrix consists of so-called contrast coefficients that (in the end) all have to sum to zero. This means, those things we want to compare have to get the opposite sign (e.g. +1 and –1), while those things we don ́t want to compare will receive a value of zero.

> Orthogonal contrasts are planned, a priori tests that partition the experimental variance cleanly. They are a powerful tool for analyzing data, but they are not appropriate for all experiments. Less restrictive comparisons among treatment means can be performed using various means separation tests, or multiple comparison tests.

- 两个比较的向量点对点相乘的和等于0的比较为正交比较。
- 水平数为 k 的因子，最多有 k-1 次正交比较。
- 正交比较之间在统计上相对独立。
- 进行什么样的比较与研究假设相关。
- 在一个比较中，相互比较的水平之间的比较矩阵中对应的数值和为0，两者符号相反，其它水平数值为0。


参考：

[A (sort of) Complete Guide to Contrasts in R](http://rstudio-pubs-static.s3.amazonaws.com/65059_586f394d8eb84f84b1baaf56ffb6b47f.html)
