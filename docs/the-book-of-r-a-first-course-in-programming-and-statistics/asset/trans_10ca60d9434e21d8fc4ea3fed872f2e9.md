

# somenewile.txt

```
person@bag@ex@funny@bage.mon
Petr7777@Mpeop638
Laid88@p73468
Mog16@Mpeop168
Chris16@Mpeop168
Stewied@Pomigh??
Brian7777@Pomigh??7
```

图 8-6: somewewile.txt 的内容

## 8.3.2 图表与图形文件

图表可以直接被写入到文件中。在第 7 章中，你在活跃的图形设备中创建并显示了图表。这个图形设备不需要是一个屏幕窗口；它可以被指定为文件。R 不是立即在屏幕上显示图表，而是按照以下步骤操作：打开一个“文件”图形设备，关闭该设备。R 支持使用同名函数直接写入 .jpg、.bmp、.png 和 .tiff 文件。例如，以下代码使用这三个步骤来创建一个 .jpg 文件：

```R
R jpeg(filename="/Users/tdavis/myjpegplot.jpeg",width=600,height=600)
R plot(1:5,6:10,ylab="a nice ylab",xlab="here's an xlab",nmain="a saved .jpeg plot")
R plot(1:5,10:6,cex=2,pch=4,col=2)
R dev.off()
null device
```

通过调用 jpeg 打开图形设备，其中你提供了预期的文件名和默认的文件夹位置，设备的尺寸设置为 480 x 480 像素，但在这里你将其更改为 600 x 600。你也可以通过为带有可选 units 参数的文件向 width 和 height 提供其他单位（英寸、厘米或毫米）来设置这些尺寸。一旦文件打开，你就可以执行所需的任何 R 绘图命令来创建图像——这个示例绘制了一些点，并使用第二个命令包含了一些额外的点。最终的图形结果将像在屏幕上显示一样，直接写入指定的文件。当你完成绘图后，必须通过调用 dev.off() 显式关闭设备，它会打印出剩余活跃设备的信息（这里，“null device”可以宽泛地解释为“没有设备处于打开状态”）。如果没有调用 dev.off()，R 将继续将任何后续绘图命令输出到文件中，并可能覆盖已有的内容。图 8-7 左侧的图显示了此示例创建的文件。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_191_0.png)

图 8-7: 直接写入磁盘的 R 图表：相同绘图命令的 .jpeg 版本（左侧）和 .pdf 版本（右侧）

你也可以将 R 图表存储为其他类型的文件，例如 PDF（使用 pdf 函数）和 EPS 文件（使用 postscript 函数）。尽管这些函数的参数名和默认值有所不同，但它们遵循相同的基本原理。你指定文件夹位置、文件名以及宽度和高度尺寸；输入你的绘图命令；然后用 dev.off() 关闭设备。图 8-7 的右面板显示了用以下代码创建的 .pdf 文件：

```R
R> pdf(file="/users/tidies/mypdfplot.pdf",width=5,height=5)
R> plot(1:5,6:10,ylab="nice ylab",xlab="here's an xlab",
      main="saved .pdf plot")
R> points(1:5,1:6,cex=2,pch=4,col=2)
R> dev.off()
```

在这里，你像以前一样使用绘图命令，代码中有几处细微差别。文件的参数是 file（而不是 filename），且 width 和 height 的单位在 pdf 中默认为英寸。图 8-7 中两个图像之间的外观差异主要源于这些宽度和高度的差异。

此过程也适用于 ggplot2 图像。然而，ggplot2 提供了一个方便的替代方案。gsave 函数可用于将最近绘制的 ggplot2 图形写入文件，并在一行代码中完成设备打开的关闭操作。

例如，以下代码从一个简单的数据集中创建并显示了一个 ggplot2 对象。

```R
R> foo <- c(1,2,3,5,3,9,4,2)
R> bar <- c(2,2.2,-1.3,0.0,0.2)
```

```R
R> qplot(foo,bar,geom="blank")
+ geom_point(size=3,shape=8,color="darkgreen")
+ geom_line(color="orange",linetype=4)
```

现在，要将此图表保存到文件，你只需要：

```R
R ggsave(filename="/Users/tdavies/mypngqplot.png")
Saving 7 x 7 in image
```

这会将图像写入指定文件名目录下的 .png 文件中。（请注意，如果你没有使用 width 和 height 显式设置尺寸，则会报告尺寸；这些将取决于你的图形设备的大小。）结果如图 8-8 所示。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_192_0.png)

图 8-8: 使用 ggplot2 的 gsave 命令创建的 .png 文件

除了简洁之外，gsave 在其他几个方面也十分方便。首先，你可以使用同一个命令创建各种图像文件类型——类型仅由你在 filename 参数中使用的扩展名决定。此外，gsave 拥有一系列可选参数，如果你想控制图像的大小以及图形的质量或缩放。

有关从基础 R 图形中保存图像的更多细节，请参见 ?jpeg?,?pdf 和 ?postscript 帮助文件。你可以咨询 ?ggsave 以获取更多关于使用 ggplot2 保存的信息。

## 8.4 临时对象/写操作

对于典型的 R 用户，最常见的输入/输出操作可能围绕数据集和图表图像。但如果你需要读取或写入其他类型的 R 对象（例如列表或数组），将需要 dump 和 get 命令，它们以更具临时的风格处理对象。

例如，假设你在当前会话中创建了这个列表：

```R
R somelist <- list(foo=c(5,2,45),
bar=matrix(data=c(T,T,F),nrow=3,ncol=3),
baz=factor(c(1,2,3,1,1,3),ordered=T))
```

```R
R somelist
$foo
[1]  5  2 45

```

```R
$bar
     [,1] [,2] [,3]
[1] TRUE  TRUE FALSE
[2] TRUE  TRUE FALSE
[3] FALSE FALSE TRUE
```

```R
$baz
[ 1] 1 2 3 1 1 3
Levels: 1 < 2 < 3
```

这个对象可以被写入文件，如果你想将其传递给同事或在另一个地方打开，这是非常有用的。使用 dump 将对象存储为文本文件：

```R
R dump(x=somelist, file="/Users/tdavies/myObject.txt")
```

从技术上讲，该命令创建了对象的美国标准交换交换（ASCII）表示。当你 dump 时，指定的对象是 x，默认情况下文件夹位置和文件名被传递给 file。图 8-9 显示了

img/b2cfc85cbb129f60fe595a2bae074fe4_193_0.png

第 8 章

注意 dump 存储了对象的所有成员以及相关信息，例如属性。somelist 的第三个元素是一个有序因子，因此无法以独立的向量形式表示它。

现在，假设你想将此列表导入到工作空间。如果文件已经用 dump 创建，则可以使用 get 读入任何其他工作空间。

```R
R> newobject <- dget(file="Users/tdavies/myObject.txt")
R> newobject
$foo
[1]  5  2 45
```

```R
$bar
     [,1] [,2] [,3]
[1] TRUE  TRUE FALSE
[2] TRUE  TRUE FALSE
[3] FALSE FALSE TRUE
```

```R
$baz
[ 1] 1 2 3 1 1 3
Levels: 1 < 2 < 3
```

使用 get 从 myObject.txt 文件读取对象并将其赋值给 newobject。该对象与原始 somelist 相同，包含了所有的结构。

使用这些命令也有一些缺点。首先，dump 不像 write table 那么可靠，因为 R 有时很难为对象创建必要的文本表示（复杂类会产生问题）。此外，由于它们需要存储结构信息，使用 dump 创建的文件在空间和执行时间方面的效率较低。尽管如此，dump 和 get 是存储或传输特定对象的有用方法，无需保存整个工作空间。

## 练习 8.1

a. R 的内置数据集库中有一个 quakes 数据框。确保你可以访问该对象并查看相应的帮助文件，以了解该数据代表什么。然后：
i. 仅选择幅度（mag）大于等于 5 的记录，并将它们写入现有文件夹中名为 q5.txt 的表格格式文件中。

