---
title: "Some Basics"
date: 2017-03-22
tag: machine learning
---

关于什么是机器学习？
> algorithms for inferring unknowns from knowns.
>
> using a set of observations (samples) to uncover an underlying process (distributions).

Supervised learning:
we get (input, correct output) 有训练集（包含数据及其分类）及测试集（有数据没分类）

Unsupervised learning:
instead of (input, correct output), we get (input, ?)

Reinforcement learning:
instead of (input, correct output), we get (input, *some* output, **grade for this output**)

Reinforcement learning 增强学习
- 结果会有相应的奖励与惩罚（Rewards or losses）
- 目标：奖励最大化

学习的成分：
- 未知的目标函数 f: x —> y；
- X 的分布 P；
- 训练集 D；
- 学习算法 A；
- 假设集 H。

机器学习的本质
- A pattern exists; 有规律存在（学习的对象）
- We cannot pin it down mathematically; 无法在数学上进行确定（否则没有学习的必要）
- We have data on it. 有足够的数据（学习的基础）

什么为学习：当前数据集所告知我们数据集之外信息（推广度问题）。
**样本复杂度**：随着问题规模的增长所带来的所需训练样本的增长。
在实际问题中，限制学习器成功的最大因素是有限的可用的训练数据。
**学习的可行性**：可以通过训练错误率估计真实错误率；存在数据集 D，使得可以在假设集 H 中自由的选择子假设 h。
如果现有有限个假设且训练数据量够多的情况下，那么不管我们如何选择训练数据，训练错误率和真实错误率都会很接近；我们设计算法来找一个 Ein 最小的假设，PAC 理论就保证了 Eout 很小。这样机器学习算法是有可能学到有用的知识的。
