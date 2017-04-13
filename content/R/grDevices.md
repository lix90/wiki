---
title: "grDevices"
date: 2017-03-22
tag: rpackage,rbase
collection: R包
---

[TOC]

# grDevices

## 函数索引 ##

Devices                 List of Graphical Devices
Hershey                 Hershey Vector Fonts in R
Japanese                Japanese characters in R
Type1Font               Type 1 and CID Fonts
X11Fonts                X11 Fonts
as.graphicsAnnot        Coerce an Object for Graphics Annotation
as.raster               Create a Raster Object
axisTicks               Compute Pretty Axis Tick Scales
boxplot.stats           Box Plot Statistics
check.options           Set Options with Consistency Checks
chull                   Compute Convex Hull of a Set of Points
cm                      Unit Transformation
contourLines            Calculate Contour Lines
dev.capabilities        Query Capabilities of the Current Graphics Device
dev.capture             Capture device output as a raster image
dev.copy                Copy Graphics Between Multiple Devices
dev.cur                 Control Multiple Devices
dev.flush               Hold or Flush Output on an On-Screen Graphics Device.
dev.interactive         Is the Current Graphics Device Interactive?
dev.size                Find Size of Device Surface
dev2bitmap              Graphics Device for Bitmap Files via Ghostscript
devAskNewPage           Prompt before New Page
embedFonts              Embed Fonts in PostScript and PDF
extendrange             Extend a Numerical Range by a Small Percentage
getGraphicsEvent        Wait for a mouse or keyboard event from a graphics window
grDevices-package       The R Graphics Devices and Support for Colours and Fonts
grSoftVersion           Report Versions of Graphics Software
n2mfrow                 Compute Default mfrow From Number of Plots
nclass.Sturges          Compute the Number of Classes for a Histogram
pdf                     PDF Graphics Device
pdf.options             Auxiliary Function to Set/View Defaults for Arguments of pdf
pictex                  A PicTeX Graphics Driver
plotmath                Mathematical Annotation in R
png                     BMP, JPEG, PNG and TIFF graphics devices
postscript              PostScript Graphics
postscriptFonts         PostScript and PDF Font Families
pretty.Date             Pretty Breakpoints for Date-Time Classes
ps.options              Auxiliary Function to Set/View Defaults for Arguments of postscript
quartz                  macOS Quartz Device
quartzFonts             quartz Fonts
recordGraphics          Record Graphics Operations
recordPlot              Record and Replay Plots
savePlot                Save Cairo X11 Plot to File
svg                     Cairographics-based SVG, PDF and PostScript Graphics Devices
trans3d                 3D to 2D Transformation for Perspective Plots
x11                     X Window System Graphics
xfig                    XFig Graphics Device
xy.coords               Extracting Plotting Structures
xyTable                 Multiplicities of (x,y) Points, e.g., for a Sunflower Plot
xyz.coords              Extracting Plotting Structures

设定颜色
`rgb` | RGB 颜色设定 | `rgb(red, green, blue, alpha)`
rgb2hsv                 RGB to HSV Conversion
gray                    Gray Level Specification
gray.colors             Gray Color Palette
hcl                     HCL Color Specification
hsv                     HSV Color Specification
make.rgb                Create colour spaces
rainbow                 Color Palettes
col2rgb                 Color to RGB Conversion
colorRamp               Color interpolation
colors                  Color Names
convertColor            Convert between Colour Spaces
densCols                Colors for Smooth Density Plots
adjustcolor             Adjust Colors in One or More Directions Conveniently.
palette                 Set or View the Graphics Palette

## 图形设备 Devices ##

`grDevices::Devices` R 绘图时支持的图形设备。
- `pdf` `postscript` `xfig` `bitmap` `pictex`
- `X11` 在 X11 视窗系统下支持
- `svg` 基于 cairo 图形的 SVG 设备
- 位图 `png` `jpeg` `bmp` `tiff`
- `quartz` 仅在 macOS 上支持

如果未打开图形设备，高阶图形函数会自动打开设备，默认打开的设备通过 `options("device")` 指定。 返回。默认的设备为初始化设置为当前平台最合适的设备。

在 R 中，只允许存在一个“活动（active）”的设备，所有图形操作均在活动设备之上。只要 R 在运行，就有一个“空设备”一直处于开启状态，但仅仅作为占位，任何使用这个空设备的尝试将会打开一个新的设备。设备与一个名称和数字编号关联，数字编号范围为1到63。空设备为编号1。一旦设备被打开，空设备将变成非活动的设备。可以通过 `dev.next` 和 `dev.prev` 选择一列开启的设备中，活动的设备的上一个或者下一个设备。

可以通过 `dev.off` 关闭指定的设备。如果未指定编号，默认关闭当前活动的设备。如果当前活动设备被关闭，那么下一个设备会被当作活动设备。编号1的设备不能关闭。正常结束一个对话可以执行 `graphics.off()`。

`dev.set` 将指定设备更改为活动设备。`dev.cur` 返回当前活动设备。`dev.list` 列出所有开启的设备，如果不存在开启的设备，那么返回空设备。如果不存在指定编号的设备，那么默认将 `dev.next` 所得到的设备当作活动设备。如果指定编号1设备，那么将开启新的设备，并将其设置为活动设备。

`dev.new` 将开启新的设备。正常情况下，需要时 R 会自动开启新的设备，但这是**让你开启独立于平台的设备**(?疑问：原文"this enables you to open further devices in a platform-indenpendent way.")。当基于文件的设备（`pdf`等），文件名将依次命名为 `Rplots<1~99>.pdf`。对于标准位图设备，如果未指定单位和分辨率，默认强制设置为 `units = "in", res = 72`。

图形设备相关参数：
- `title` 标题
- `width` 宽度
- `height` 高度
- `pointsize` 点尺寸
- `family` 字体
- `antialias` 是否抗锯齿
- `type` 类型
- `file` 文件名
- `bg` 背景色
- `canvas` 画布
- `dpi` 分辨率（每英寸点数）

PDF 设备参数：
- `paper` 纸张类型，`"a4","letter","legal",...`
- `bg` 背景色，默认为 `"transparent"`
- `fg` 前景色，默认为 `"black"`
- `pointsize` 默认为 `12`，1/72英寸为一个点
- `colormodel` 颜色模式 `"srgb","gray","cmyk"`，默认为 `"srgb"`

PDF 设备并不嵌入字体到 PDF 文件中，所以建议使用常见的字体例如：`"Times"(="serif"),"Helvetica"(="sans"),"Courier"(="mono")`。
- 默认设备尺寸为 7 英寸的正方形。
- 字体大小为 “big points”。
- 默认字体为 Helvetica。
- 线宽为1/96英寸的倍数，最小为 0.01。
- 可支持任意弧度的圆形。
- 颜色模式默认为 sRGB。
- 如果线宽特别细，线型默认强制为实线。

位图设备参数：
- 默认宽高均为 `480px`
- 默认单位为 `px`
- 默认点大小为 `12`
- 默认背景色为 `"white"`
- 默认分辨率为 `res = 72` 单位为 ppi
