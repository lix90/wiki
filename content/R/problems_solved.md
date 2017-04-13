---
title: "Problems solved"
date: 2017-03-21
tag: r, problem solving
---

# Problem of installing units package

```
-----Error: libudunits2.a not found-----
     If the udunits2 library is installed in a non-standard location,
     use --configure-args='--with-udunits2-lib=/usr/local/lib' for example,
     or --configure-args='--with-udunits2-include=/usr/include/udunits2'
     replacing paths with appropriate values for your installation.
     You can alternatively use the UDUNITS2_INCLUDE and UDUNITS2_LIB
     environment variables.
     If udunits2 is not installed, please install it.
     It is required for this package.
```

已解决：

1. 安装依赖 `udunits`: `brew install udunits`
2. 安装依赖 `udunits2`: `install.packages('udunits2', type = 'source')`
3. 安装 `units`: `devtools::install_github('edzer/units', type = 'source')` 或者 `install.packages('udunits2', type = 'source', configure.args = "--with-udunits2-lib=/usr/local/Cellar/udunits/2.2.20/lib/")
`

参考：https://github.com/edzer/units/issues/1
