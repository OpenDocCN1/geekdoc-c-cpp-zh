
确保已加载 `MASS` 包，一旦获得访问 `UScereal` 数据框的权限。如果你尚未这样做，请检查帮助文件 `?cereal` 并重新创建 `cereal` 对象，正如练习 24.1 (a) 中指定的那样。然后执行以下操作：

+ c. 设置一个单选按钮对象以在制造商、货架和维生素变量之间进行选择。确保每个单选按钮的标签清晰，并为将形成用于着色点的选项集合设置适当的标题标签。将对象命名为 `filler`。

+ d. 借用第 24.4 节中创建的 `sizer` 和 `opacity` 对象，并使用你在 (c) 中创建的对象来控制 `fill`，创建一个卡路里与蛋白质的交互式散点图。整理轴并抑制点颜色的图例标题。结果在功能上应基本上与 Figure 24-8 中最上面的屏幕截图中出现的图形相同。

+ e. 为与 (c) 中指定的相同单选按钮创建一个新对象，该对象将控制点的形状（即用于绘图点的字符）。相应地修改标题标签。将此对象命名为 `shape`。

+ f. 最后，重新创建卡路里与蛋白质的交互式散点图，正如 (d) 中那样，但这次 additionally 将 (e) 中的 `shaper` 分配给 `ggvis` 中的 `shape` 修饰符。为防止两组单选按钮的图例相互重叠，你需要添加管道到代码：

```
add_legend("shape", title="",
properties=legend_props(legend=list(y=100)))
```

```
and

set_options(duration=0)
```

第一个只是将形状修饰符的图例垂直向下移动，第二个消除了切换交互式图形中的选项时默认发生的轻微“动画延迟”。再次使用 `add_axis` 和 `add_legend` 的额外调用来澄清或抑制轴和图例标题。

# 本章的重要代码

| 函数/运算符 | 简要说明 | 首次出现 |
|---|---|---|
| `ggplot` | 初始化 ggplot 图 | 第 24.1 节，p. 610 |
| `geom_smooth` | 趋势线图层 | 第 24.2.1 节，p. 612 |
| `loess` | 计算 LOESS（base R） | 第 24.2.1 节，p. 612 |
| `rev` | 反转向量元素 | 第 24.2.1 节，p. 612 |
| `adjustcolor` | 修改颜色不透明度（base R） | 第 24.2.1 节，p. 612 |
| `geom_density` | 核密度图层 | 第 24.2.2 节，p. 614 |
| `ggtitle` | 添加 ggplot 标题 | 第 24.2.2 节，p. 615 |
| `grid.arrange` | 多个 ggplot 图 | 第 24.3.1 节，p. 616 |
| `facet_wrap` | 单向分面 | 第 24.3.2 节，p. 619 |
| `facet_grid` | 双因子分面 | 第 24.3.2 节，p. 620 |
| `ggvis` | 初始化 ggvis 图 | 第 24.4 节，p. 624 |
| `%>%` | 管道到 ggvis 图层 | 第 24.4 节，p. 624 |
| `layer_histograms` | ggvis 直方图图层 | 第 24.4 节，p. 624 |
| `input_slider` | 交互式滑块 | 第 24.4 节，p. 624 |
| `:` | 常量 ggvis 赋值 | 第 24.4 节，p. 624 |
| `layer_points` | ggvis 点图层 | 第 24.4 节，p. 626 |
| `input_radiobuttons` | 交互式按钮 | 第 24.4 节，p. 626 |
| `add_legend` | 添加/修改 ggvis 图例 | 第 24.4 节，p. 626 |
| `layer_smooths` | ggvis 趋势线图层 | 第 24.4 节，p. 627 |
| `add_axis` | 添加/修改 ggvis 坐标轴 | 第 24.4 节，p. 627 |

# 定义颜色和绘制高维图形

![](img/b2cfc85cbb129f60fe595a2bae074fe4_664_0.png)

现在你已经掌握了一些基础的可视化技能，你可以超越标准 x 和 y 轴，例如，根据某些附加值或变量对点进行着色，或添加 z 轴来构建 3D 图。像这样的高维图允许你使用比其他方式更多的变量来直观探索数据或模型。

在本章中，你将更详细地了解在 R 中处理颜色和调色板的问题，然后你将查看四种新的图：3D 散点图、等高线图、像素图像图和透视图。

## 25.1 表示和使用颜色

颜色在许多图中起着关键作用。正如你已经看到的，颜色可以纯粹用于美观增强，也可以成为解释数据/模型的重要辅助，通过区分值和变量。在学习更复杂的数据和模型可视化工具之前，了解 R 如何正式表示和处理颜色是有用的。在本节中，你将检查创建和表示特定颜色的常见方法，以及如何定义和使用一组连贯的颜色；后者被称为 *palette*。

### 25.1.1 红绿蓝十六进制颜色代码

在指定绘图中的颜色时，到目前为止你对 R 的指示要么是以 1 到 8 的整数值形式给出，要么是字符字符串形式（参见第 7.2.3 节的相关注释）。对于编程目的，你需要这些颜色的更客观的表示。

最常见的颜色指定方法之一是定义三种原色的饱和度或强度——红、绿、蓝（RGB），然后将它们混合形成目标颜色。标准 RGB 系统的每个原色都分配一个从 0 到 255（包含）的整数。这种混合能够形成总共 $256^3 = 16,777,216$ 种可能的颜色。

你始终以（R，G，B）顺序表达这些值；结果通常被称为 *triplet*。例如，(0,0,0) 表示黑色，(255,255,255) 表示白色，而 (0,255,0) 是全绿色。

`col` 参数允许你在提供 1 到 8 的整数时选择八种颜色之一。你可以用以下调用诱导出这些颜色：

```
R palette()
[1] "black" "red" "green3" "blue" "cyan" "magenta"
[7] "yellow" "gray"
```

这些是 650 多种命名颜色中的一个小子集，你可以通过在 R 提示符下输入 `colors()` 来列出所有这些颜色。所有这些命名颜色也可以用标准 RGB 格式表示。要查找颜色的 RGB 值，将所需的颜色名称作为字符字符串向量提供给内置的 `col2rgb()` 函数。以下是一个示例：

```
R col2rgb("black","green3", "pink")
     [,1] [,2] [,3]
red    0   0  255
green  0 205  192
blue   0   0  203
```

结果是一个 RGB 值矩阵，每个列代表你指定的其中一种颜色。这就是 R 在 RGB 意义上实际意味着什么，当你要求它使用相应的字符字符串绘制这些颜色时。

这些 RGB 三元组经常表示为 *hexadecimals*，一种在计算中常用的数字编码系统。在 R 中，十六进制或 hex 代码是一个字符字符串，以 # 开头，后跟六个字母数字字符：有效字符为字母 A 到 F 和数字 0 到 9。第一对字符表示红色分量，第二和第三对分别表示绿色和蓝色。如果你必须创建一个或多个 RGB 三元组，你可以通过 `rgb` 函数将它们转换为 hex 以在任何后续代码中使用。此命令接受 RGB 值矩阵，注意它期望每个（R，G，B）是该矩阵的一行（与例如对 `col2rgb` 的调用的列相反）。

你需要告诉 `rgb` 你的最大颜色值，根据标准 RGB 格式为 255（因为默认情况下它会缩放此值并使用 1）。以下代码对上一次调用 `col2rgb` 的结果执行转置（参见第 3.3 节），将我的三个作为所需的 RGB 三元组形式，并相应地设置 `maxColorValue`：

```
R> rgb(t(col2rgb(c("black","green","pink"))),maxColorValue=255)
[1] "#000000" "#00CD00" "#FFC0CB"
```

输出为你提供了 R 指代名称 "black","green," 和 "pink" 的 RGB 值的十六进制代码。

我不会详细介绍将 RGB 三元组转换为十六进制的具体细节，因为它超出了本书的范围，但重要的是要知道 R 使用 RGB 三元组创建的所有颜色都表示为 hex 代码，因此当你在绘图中处理颜色和调色板时，你应该至少能够识别十六进制。

为了进行更丰富的探索，让我们编写一个小函数来以单独的颜色绘制点并用 RGB 三元组和相应的 hex 代码进行标记。考虑编辑器中的以下内容：

```
pcol <- function(cols){
n <- length(cols)
dev.new(width=7,height=4)
par(mar=rep(1,4))
plot(1,5,1,type="n",xaxt="n",yaxt="n",ann=FALSE)
for (i in 1:n){
pt <- locator(1)
rgbval <- col2rgb(cols[i])
points(pt,x+1,y,pch=19,family="mono",
label=paste("\",",cols[i],"\","\nR: ",rgbval[1],
" G: ",rgbval[2]," B: ",rgbval[3],
" hex: ",rgb(rgbval),maxColorValue=255,
sep="=")
}
```

函数 `pcol` 接受一个参数， intended to be a character vector of colors recognized by R。当你执行它时，它会打开一个新的图形设备并将图形边距均等化为每侧一行的边距。开始一个绘图，除了一个框外全部被抑制。这是为了让你可以使用 `locator`（参见第 23.3 节）在区域中放置点，

定义颜色和在高维中绘图 633

在循环中实现

以下代码设置设备，首先将 14 个 R 颜色名称（随机选择）存储在字符向量 `mycols` 中。在耗尽这些鼠标点击不同区域的绘图后，执行完成。

```
R mycols <- c("black","blue","royalblue2","pink","magenta","purple",
"violet","coral","lightgray","seagreen4","red","red2",
"yellow","lemonchiffon3")
```

```
R pcol(mycols)
```

当我像这里一样执行 `pcol` 时，我点击了 14 个点，在我的图形设备上绘制了粗略的列。图 25-1 显示了结果。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_667_0.png)

> 图 25-1：命名 R 颜色及其对应的 RGB 三元组和 hex 代码。

本质上，你可以通过指定 RGB 值并获取其代码来获得你想要的任何颜色（换句话说，远不止 R 内置的命名颜色）。这些十六进制可以作为传统 R 图形函数中任何指定颜色的地方提供（通常提供给 `col` 参数）。随着本章的进展，你会看到这一点。当然，你

也可以为 R 工作区中的新对象分配十六进制代码或十六进制代码向量（例如，如果你正在创建自己的自定义颜色），以便在后续绘图中使用。

## 25.1.2 内置调色板

能够实现自己的 RGB 颜色在需要许多颜色时最有用，这些颜色的集合称为调色板。当颜色用于描述连续体上的某事物时，你通常需要一个调色板，比如图 24-6 中用于高度测量的各种蓝色阴影。

基础 R 安装中内置了若干种颜色调色板。这些由函数 `rainbow`、`heat.colors`、`terrain.colors`、`topo.colors`、`cm.colors`、`gray.colors` 和 `gray` 定义。`gray` 除外，你可以直接指定想要的颜色数量，它们将被作为字符向量返回，表示在该特定调色板整个范围上等间距的序列。

使用可视化最容易看到这一点。以下代码从每个调色板生成恰好 600 种颜色：

```
R N <- 600
R rainbow <- rainbow(N)
R heat <- heat.colors(N)
R terr <- terrain.colors(N)
R topo <- topo.colors(N)
R cm <- cm.colors(N)
R gray1 <- gray.colors(N)
R gray2 <- gray(level=seq(0,1,length=N))
```

请注意，单个 `gray` 期望 0（全黑）到 1（全白）之间的数值向量来提供灰度。它的对应函数 `gray.colors` 与其他内置调色板的工作方式相同，但默认的视觉范围在黑白极端之间略窄。这些范围可使用稍后会看到的可选参数 `start` 和 `end` 来重置。

下一段使用第 23 章的技能初始化新绘图，并使用向量重复在一次调用中为每个调色板放置 600 个点，并根据颜色向量适当着色。

```
dev.new(width=8,height=3)
R par(mar=c(1,1,1,1))
plot(1:N,ylim=c(0,0.5,7),type="n",xax="n",yax="n",ann=FALSE)
points(rep(1:N,7),rep(7,each=N),pch=19,cex=3)
col=c(rep("rainbow",heat,terrain,topo,cm,gray1,gray2))
axis(2,at=1:7,labels=c("rainbow","heat.colors","terrain.colors","topo.colors","cm.colors","gray.colors","gray"),family="mono",las=1)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_668_0.png)

# 图 25-2 显示了结果。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_669_0.png)

图 25-2：展示内置调色板的颜色范围，`gray.colors` 使用默认限制。

如需更多信息，请访问帮助文件 `?gray.colors` 和 `?gray` 获取相应的灰度调色板，其他调色板出现在 `?rainbow` 下。

## 25.1.3 自定义调色板

你并不受限于即用型的颜色设计。函数 `colorRampPalette` 允许你创建自己的调色板；你向同名参数提供两个或多个期望的颜色键，它就会创建在它们之间过渡的调色板。对 `colorRampPalette` 的调用结果本身就是一个函数——它与前面提到的内置调色板函数行为完全相同。

假设你想在紫色和黄色之间生成颜色。你以期望的顺序指定要插值的颜色键，作为 R 识别的颜色名称的字符向量。以下行创建此调色板函数：

```
R puryl.colors <- colorRampPalette(colors=c("purple","yellow"))
```

让我们再创建一个，这次选择一种在颜色图中使用时在灰度中会更清晰的颜色（在这种情况下，切换到单色调色板是个好主意）。

```
R blues <- colorRampPalette(colors=c("navyblue","lightblue"))
```

这里还有几个例子，这次使用超过两种颜色：

```
R fours <- colorRampPalette(colors=c("black","hotpink","seagreen4","tomato"))
R patriot.colors <- colorRampPalette(colors=c("red","white","blue"))
```

创建了一些自定义调色板函数后，你现在可以像之前一样从每个范围生成任意数量的颜色（此处使用之前存储的 `N` 值 600）。完成后，你可以调整之前的绘图代码以得到图 25-3 中的图像。

```
R py <- puryl.colors(N)
R bls <- blues(N)
R frs <- fours(N)
R pat <- patriot.colors(N)
R dev.new(width=8,height=2)
R par(mar=c(1,8,1,1),xlim=c(1,N),ylim=c(0.5,4.5),type="n",xax="n",yaxt="n",ann=FALSE)
R plot(points(1:N,4),rep=c(1,4,each),pch=19,cex=3,col=c(py,bls,fr,pat))
R axis(2,at=4,labels=c("puryl.colors","blues","fours","patriot.colors"),family="mono",las=1)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_670_0.png)

图 25-3：使用 `colorRampPalette` 创建的自定义颜色调色板的若干示例。

## 25.1.4 使用颜色调色板索引连续体

你现在已经多次看到颜色如何用于根据分类变量识别组（对应于某一水平的数据只是与其他颜色不同的颜色），这很容易做到。然而，将颜色适当分配给连续体上的值需要多一点。有两种方法：对连续值进行分类或归一化。让我们先看前一种方法。

### 通过分类

给值按连续变量着色的一种方法是将其转化为着色分类变量点的熟悉问题。你可以通过将连续值划分为固定数量的 k 个类别，从调色板生成 k 种颜色，并将每个观测匹配到其落入的适当颜色来实现。

在第 20.1 节中，你对 MASS 包的调查数据绘制了高度与手掌跨度。让我们使用颜色额外标识非书写手掌跨度变量。加载包并执行以下行：

```
R surv <- na.omit(survey[c("Wr.Hnd","NW.Hnd","Height")])
```

这创建了数据对象 `surv`

现在，第一件事是决定你的颜色调色板。

```
R NW.pal <- colorRampPalette(colors=c("red","yellow2"))
```

这将生成从尺度下端的暗淡红色到上端的略微褪色的黄色颜色（类似于内置的 `heat` 调色板；参见图 25-2）。接下来，你需要决定要为连续值构造多少个箱 k。这决定了从 `NW.pal` 生成多少种不同颜色。对于此数据，设 `k=5`。
