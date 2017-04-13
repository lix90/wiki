---
title: "graphics"
date: 2017-03-22
tag: rpackage, rbase
collection: R包
---

[TOC]

# 函数索引 #

## 常用底层函数 ##

函数名 | 中文描述 | 用途
:-----|:--------|:--------
Axis (axis) | 添加坐标轴，调用函数 `axis` | ``
abline | 添加直线（垂直、水平、斜线） |
lines | 添加连接线段
segments | 一对点之间绘制线段
**arrows** | 一对点之间绘制箭头 | 添加注释，误差线
box | 绘制线框
grid | 添加网格线
title | 绘制标题
legend | 添加图例
mtext | 在图形边距上添加文字
text | 添加文本内容
points | 添加点
rect | 绘制矩形
polygon | 绘制多边形
polypath | 绘制路径
symbols | 绘制符号 (Circles, Squares, Stars, Thermometers, Boxplots)
xspline | Draw an X-spline
**rug** | 添加轴须图 | 散点图添加轴须图呈现分布特征

**par** | 设置和查询图形参数
axTicks                 Compute Axis Tickmark Locations
clip                    Set Clipping Region
filled.contour          Level (Contour) Plots
frame                   Create / Start a New Plot Frame
grconvertX              Convert between Graphics Coordinate Systems
identify                Identify Points in a Scatter Plot
**layout**                  Specifying Complex Plot Arrangements
locator                 Graphical Input
screen                  Creating and Controlling Multiple Screens on a Single Device
xinch                   Graphical Units
strwidth/strheight | 计算字符串和数学表达式的宽/高

plot                    Generic X-Y Plotting
plot.data.frame         Plot Method for Data Frames
plot.default            The Default Scatterplot Function
plot.design             Plot Univariate Effects of a Design or Model
plot.factor             Plotting Factor Variables
plot.formula            Formula Notation for Scatterplots
plot.histogram          Plot Histograms
plot.raster             Plotting Raster Images
plot.table              Plot Methods for 'table' Objects
plot.window             Set up World Coordinates for Graphics Window
plot.xy                 Basic Internal Plot Function

assocplot               Association Plots
barplot                 Bar Plots
boxplot                 Box Plots
boxplot.matrix          Draw a Boxplot for each Column (Row) of a Matrix
bxp                     Draw Box Plots from Summaries
cdplot                  Conditional Density Plots
coplot                  Conditioning Plots
curve                   Draw Function Plots
dotchart                Cleveland's Dot Plots
fourfoldplot            Fourfold Plots
hist                    Histograms
hist.POSIXt             Histogram of a Date or Date-Time Object
matplot                 Plot Columns of Matrices
mosaicplot              Mosaic Plots
pairs                   Scatterplot Matrices
panel.smooth            Simple Panel Plot
persp                   Perspective Plots
pie                     Pie Charts
smoothScatter           Scatterplots with Smoothed Densities Color Representation
spineplot               Spine Plots and Spinograms
stars                   Star (Spider/Radar) Plots and Segment Diagrams
stem                    Stem-and-Leaf Plots
stripchart              1-D Scatter Plots
sunflowerplot           Produce a Sunflower Scatter Plot

双变量

contour | 绘制轮廓线/等高线图
image | 绘制二维图像
rasterImage | 绘制栅格图

# par: graphical parameters #

**margins**: (bottom, left, top, right)
mar (margins size in lines)
mai (margin size in inches)
mex (scale fator of line height of margins)
oma (out margins area)

[tutorials of margins and outer margins]
[R graphics]

**multiple figures**
mlcol (multiple figures column)
mlrow (multiple figures row)

**cex**: scale factor of text and symbols
cex.axis: axis tick labels
cex.lab: x-y axis labels
cex.main: main title
cex.sub: subtitle

**axis**

**xaxs**: x-axis style of interval calculation: R 语言仅支持 r 和 i 两种风格
- r = regular 会在原始数据的基础上有一个拓展，即原始数据点与边框之间有一段距离
- i = interval 按照原始数据的大小进行计算，原始数据点可能与边框重叠

**xaxt**: x-axis type
- n = no axis, 不绘制坐标轴
- s/l/t = plot, 绘制坐标轴

**plot regions**
**plt**: the coordinates of the plot region, (x1/left, x2/right, y1/bottom, y2/top), 每个值为 0 \~ 1 之间，为相对于 device 的长宽的比率。x1 为 device 左边缘至 plot region 左边缘的距离，x2 为 device 的左边缘至 plot region 的右边缘的距离。y1 为 device 的下边缘至 plot region 的下边缘的距离，y2 为 device 的下边缘至 plot region 的上边缘的距离。
**pin**: specify the size of the plot region in inches, (width, height)
**pty**: default "m", 占据可用空间的所有空间；"s"，以正方形的形式占据可用空间的最大空间。

**xpd**
`par(xpd = NA)` clipped to device
`par(xpd = TRUE)` clipped to the current figure region
`par(xpd = FALSE)` clipped to the current plot region
