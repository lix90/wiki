---
title: "杂项"
date: 2017-03-22
---

[TOC]

# 如何在 ESS 中调出 R 包对应的 Vignettes？

- 首先得加载包 `library(pkg)`
- `C-c C-d C-v` 查找已载入包的 Vignettes，含有 Vignettes 的包则会列出来
- 光标移动到链接下，`enter/RET` 打开对应 Vignettes

或者

- 先搜索包的 vignette：`vignette(package = "pkg_name")`，获得 vignette 主题名称
- 然后再通过 `vignette(topic = "topic_name", package = "pkg_name")` 调出 vignette

# 如何阻止 R 打印启动信息（startup message）

- 命令行中，传给 R 参数即可 `R -q/--quiet/--silent`
- ESS 中，设定变量 `inferior-R-args` 的值 `(setq inferior-R-args "-q")`

# 如何将 R 中的统计结果导出为发表格式（APA）？

一般来说，用 R 统计之后导出的信息过于详细，直接复制并不能满足发表的格式要求。但是结果报告时只需要特定的指标，所以需要精简信息。两个包可以实现该需求，`schoRsch` 和 `apa`。

> apa generalizes this idea by providing formatters for different output formats (text, Markdown, RMarkdown, HTML, LaTeX, docx and R’s plotmath syntax).
>
> Currently supported tests are:
> - t-test (`t.test` and `apa::t_test`)
> - ANOVA (`ez::ezANOVA`, `afex::aov_car`, `afex::aov_ez`, and `afex::aov_4`)
> - chi-squared test (`chisq.test`)
> - test of a correlation (`cor.test`)

apa 包可以支持多种常见的心理学使用的统计检验方法，对应函数为：`anova_apa` `chisq_apa` `cor_apa` `t_apa`。apa 比 schoRsch 强大的地方是可以导出为多种格式，例如 Rmarkdown，html，latex，docx，以及在 R 绘图时的数学表达式。这样就可以直接复制结果到论文中了。

schoRsch 包中包含这几个导出结果的函数：`anova_out` `cor_out` `chi_out` `t_out`。

`apa::anova_apa`
- x: 支持 `ez::ezANOVA` `afex::afex_ez` `afex::afex_car` `afex::afex_4` 的结果作为输入对象。
- effect: 字符串，指定效应名称；如果值为 'NULL'，所有效应均报告。
- sph\_corr: 字符串，指定球形检验方法，包括 "greenhouse-geisser"(默认) "huynh-feldt" 或 "none"；或者使用简称 "gg" "hf"。
- es: 字符串，指定效应量类型，包括 "petasq"(partial eta squared) 或 "getasq"(generalized eta squared)；或者使用简称 "pes" 和 "ges"。
- format: 字符串，指定导出格式，包含 "text", "markdown", "rmarkdown", "html", "latex", "docx", "plotmath"。

`apa::t_apa`
- x: 来自 `apa::t_test` 或 `t.test` 的结果。
- es: 字符串，指定效应量类型，包括 "cohens\_d"(默认), "hedges\_g", 或 "glass\_delta"（如何 x 为独立样本 t 检验的结果）。如果 x 为配对样本或者单样本 t 检验结果，报告 cohen's d 值。
- format: 字符串，导出格式。

---

矫正 p.value：`p.adjust(p, method = p.adjust.methods)`

根据 p.value 的大小范围调整小数点位数：`afex::round_ps`，0.99-0.01 为两位小数点；p < 0.01 为三位小数点；p < 0.001 为四位小数点。

`plotrix::raw.means.plot`：用来绘制最多两因素实验设计结果的图形。该函数将原始数据绘制在背景上，将因子或者区组的均值绘制在前景。

`aov` 只适用于平衡设计（没有缺失值）。当存在两个或更多的误差项时，该方法将在统计上失效。此时可以使用 `nlme::lme`。数据是否平衡可以通过 `replications()` 函数检测。

默认的 'contrasts' 为非正交对比，`aov` 及其辅助函数在正交对比下更有效。可以通过 `options(contrasts = c("contr.helmert", "contr.poly"))` 修改 'contrasts'。

检验类型，type-I, type-II, type-III?

> The designations "type-II" and "type-III" are borrowed from SAS, but the definitions used here do not correspond precisely to those employed by SAS. **Type-II tests are calculated according to the principle of marginality, testing each term after all others**, except ignoring the term’s higher-order relatives; **so-called type-III tests violate marginality, testing each term in the model after all of the others.** This definition of Type-II tests corresponds to the tests produced by SAS for analysis-of-variance models, where all of the predictors are factors, but not more generally (i.e., when there are quantitative predictors). **Be very careful in formulating the model for type-III tests, or the hypotheses tested will not make sense.**
>
> As implemented here, type-II Wald tests are a generalization of the linear hypotheses used to gen- erate these tests in linear models.
>
> The standard R anova function calculates sequential ("type-I") tests. These rarely test interesting hypotheses in unbalanced designs.

- [btaining the same ANOVA results in R as in SPSS - the difficulties with Type II and Type III sums of squares](http://myowelt.blogspot.de/2008/05/obtaining-same-anova-results-in-r-as-in.html)
- [How to interpret type I, type II, and type III ANOVA and MANOVA?](http://stats.stackexchange.com/questions/20452/how-to-interpret-type-i-type-ii-and-type-iii-anova-and-manova)
- [Choice between Type-I, Type-II, or Type-III ANOVA](http://stats.stackexchange.com/questions/60362/choice-between-type-i-type-ii-or-type-iii-anova)
- [How does one do a Type-III SS ANOVA in R with contrast codes?](http://stats.stackexchange.com/questions/4544/how-does-one-do-a-type-iii-ss-anova-in-r-with-contrast-codes)
- [Types of Sums of Squares](https://afni.nimh.nih.gov/sscc/gangc/SS.html)
