---
title: "Miscellaneous"
author: Lixiang
date: 2017-03-18 17:52:33
tag: python
description: "Python有关的杂项"
---

# pip

从 github 库中安装 python 模块

``` shell
pip install git+https://github.com/user/repo_name.git
```

# 环境管理

[virtualenv](https://virtualenv.pypa.io/en/stable/)
[virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/)

``` shell
conda create --name/-n <environment name> anaconda
```

# Jupyter

Jupyter matlab kernel

``` shell
pip install pymatbridge matlab_kernel
python -m matlab_kernel install
printf "export MATLAB_EXECUTABLE=/Applications/MATLAB_2014b.app/bin/matlab" >> ~/.bash_profile
```

