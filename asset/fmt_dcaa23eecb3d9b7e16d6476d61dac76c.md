
在这里，`file` 参数指定了所需的文件，该文件没有表头，因此设置 `header=FALSE`。你设置 `stringsAsFactors=TRUE` 是因为你希望将变量（唯一的非数值变量）视为因子。没有缺失值，所以你不需要指定 `na`（尽管，该参数的使用方法与之前相同），根据定义，`.csv` 文件是逗号分隔的，`read.csv` 正确实现了所需的数据框 `spread`，然后可以在你的 R 控制台中打印。

如你所见，将表格数据读入 R 非常简单——你只需要注意数据的表头情况以及如何识别缺失项。简单的表格格式对于数据集的存储是自然且常见的，但如果你需要读取结构更复杂的文件，R 及其包提供了更复杂的函数。例如，请参见 `scan` 和 `readLines` 的文档，它们提供了对如何解析文件的高级控制。你也可以通过在提示符中输入 `read.table` 来访问 `read.table` 和 `read.csv` 的文档。

## 8.2.3 基于网络的文件

有了互联网连接，R 可以相同的 `read.table` 命令从网站读取文件。关于表头、分隔符和缺失值的规则仍然有效；你只需要指定文件的 URL 地址而不是本地文件夹。例如，你将使用美国统计协会通过《统计教育杂志》(JSE) 提供的在线数据集库，地址为 `http://www.stat.org/publications/jse/jse_data_archive.html`。例如，位于 `http://www.stat.org/publications/jse/jse_data_archive.html` 上的 JSE 数据集包含了 2001 年的 Chu 的分析。

*(注：由于原文文本中存在大量重复的句子，翻译时已根据逻辑进行了精简处理以确保通顺。)*

*(更正：原文提供的文本似乎存在严重的段落重复粘贴错误，以下为基于核心内容的完整翻译：)*

关于表头、分隔符和缺失值的规则仍然有效；你只需要指定文件的 URL 地址而不是本地文件夹。例如，你将使用美国统计协会通过《统计教育杂志》(JSE) 提供的在线数据集库，地址为 `http://www.stat.org/publications/jse/jse_data_archive.html` 上的 JSE 数据集包含了 2001 年的 Chu 的分析。

*(此处由于原文文本存在异常循环，高级文档工程师已识别并过滤重复内容。)*

## 8.3 输出数据文件和图表

从 R 中将数据框输出文件与读入一样简单。R 的向量化行为是记录数据集、重构数据并写回文件的一种快速且方便的方法。

### 8.3.1 数据集

向计算机写入表格格式文件的函数是 `write.table`。你提供一个数据框对象作为 `x`，该函数将其内容以指定的名称、分隔符和值字符串写入新文件。例如，以下行将 8.2 节中的 `mytable` 对象写入文件：

```
write.table(x=myDatafile,file="Users/tdavies/somefile.txt",sep="@",na="??",quote=FALSE,row.names=FALSE)
```

你为 `file` 提供文件夹位置，以你想要的新数据文件名结尾。在指定的文件夹中名为 `somefile.txt`，用 `&` 分隔，用 `??` 表示缺失值（因为你实际上是在创建一个新文件，通常此处 `file.choose` 命令）。由于 `myfile` 有变量名，这些名称将作为表头写入文件。可选逻辑参数 `quote` 决定是否将每个非数值项封装在双引号中（如果你的其他软件格式要求明确需要它们）；通过将参数设置为 `FALSE` 则取消引号。另一个可选逻辑参数 `row.names` 询问是否包含 `myfile` 的行名（在本例中，这只是数字 1 到 6），你同样通过 `FALSE` 忽略了它们。

像 `read.csv` 一样，`write.csv` 是 `write table` 函数的快捷版本，专门为 `.csv` 设计。

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

通过调用 `jpeg` 打开图形设备，其中你提供了预期的文件名和默认的文件夹位置，设备的尺寸设置为 480 x 480 像素，但在这里你将其更改为 600 x 600。你也可以通过为带有可选 units 参数的文件向 width 和 height 提供其他单位（英寸、厘米或毫米）来设置这些尺寸。一旦文件打开，你就可以执行所需的任何 R 绘图命令来创建图像——这个示例绘制了一些点，并使用第二个命令包含了一些额外的点。最终的图形结果将像在屏幕上显示一样，直接写入指定的文件。当你完成绘图后，必须通过调用 `dev.off()` 显式关闭设备，它会打印出剩余活跃设备的信息（这里，“null device”可以宽泛地解释为“没有设备处于打开状态”）。如果没有调用 `dev.off()`，R 将继续将任何后续绘图命令输出到文件中，并可能覆盖已有的内容。图 8-7 左侧的图显示了此示例创建的文件。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_191_0.png)

图 8-7: 直接写入磁盘的 R 图表：相同绘图命令的 .jpeg 版本（左侧）和 .pdf 版本（右侧）

你也可以将 R 图表存储为其他类型的文件，例如 PDF（使用 `pdf` 函数）和 EPS 文件（使用 `postscript` 函数）。尽管这些函数的参数名和默认值有所不同，但它们遵循相同的基本原理。你指定文件夹位置、文件名以及宽度和高度尺寸；输入你的绘图命令；然后用 `dev.off()` 关闭设备。图 8-7 的右面板显示了用以下代码创建的 .pdf 文件：

```R
R> pdf(file="/users/tidies/mypdfplot.pdf",width=5,height=5)
R> plot(1:5,6:10,ylab="nice ylab",xlab="here's an xlab",
      main="saved .pdf plot")
R> points(1:5,1:6,cex=2,pch=4,col=2)
R> dev.off()
```

在这里，你像以前一样使用绘图命令，代码中有几处细微差别。文件的参数是 `file`（而不是 `filename`），且 `width` 和 `height` 的单位在 `pdf` 中默认为英寸。图 8-7 中两个图像之间的外观差异主要源于这些宽度和高度的差异。

此过程也适用于 `ggplot2` 图像。然而，`ggplot2` 提供了一个方便的替代方案。`gsave` 函数可用于将最近绘制的 `ggplot2` 图形写入文件，并在一行代码中完成设备打开的关闭操作。

例如，以下代码从一个简单的数据集中创建并显示了一个 `ggplot2` 对象。

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

这会将图像写入指定文件名目录下的 .png 文件中。（请注意，如果你没有使用 `width` 和 `height` 显式设置尺寸，则会报告尺寸；这些将取决于你的图形设备的大小。）结果如图 8-8 所示。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_192_0.png)

图 8-8: 使用 `ggplot2` 的 `gsave` 命令创建的 .png 文件

除了简洁之外，`gsave` 在其他几个方面也十分方便。首先，你可以使用同一个命令创建各种图像文件类型——类型仅由你在 `filename` 参数中使用的扩展名决定。此外，`gsave` 拥有一系列可选参数，如果你想控制图像的大小以及图形的质量或缩放。

有关从基础 R 图形中保存图像的更多细节，请参见 `?jpeg`?,`?pdf` 和 `?postscript` 帮助文件。你可以咨询 `?ggsave` 以获取更多关于使用 `ggplot2` 保存的信息。

## 8.4 临时对象/写操作

对于典型的 R 用户，最常见的输入/输出操作可能围绕数据集和图表图像。但如果你需要读取或写入其他类型的 R 对象（例如列表或数组），将需要 `dump` 和 `get` 命令，它们以更具临时的风格处理对象。

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

这个对象可以被写入文件，如果你想将其传递给同事或在另一个地方打开，这是非常有用的。使用 `dump` 将对象存储为文本文件：

```R
R dump(x=somelist, file="/Users/tdavies/myObject.txt")
```

从技术上讲，该命令创建了对象的美国标准交换交换（ASCII）表示。当你 `dump` 时，指定的对象是 `x`，默认情况下文件夹位置和文件名被传递给 `file`。图 8-9 显示了

img/b2cfc85cbb129f60fe595a2bae074fe4_193_0.png

第 8 章

注意 `dump` 存储了对象的所有成员以及相关信息，例如属性。`somelist` 的第三个元素是一个有序因子，因此无法以独立的向量形式表示它。

现在，假设你想将此列表导入到工作空间。如果文件已经用 `dump` 创建，则可以使用 `get` 读入任何其他工作空间。

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
