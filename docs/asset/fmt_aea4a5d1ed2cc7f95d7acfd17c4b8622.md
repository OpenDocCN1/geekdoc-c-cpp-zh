
```
R text(0,6,label="sans text (default)family=\sans",font=1)
R text(0,5,label="serif textfamily=\serif",font=1,
family="serif",font=1)
R text(0,4,label="mono textfamily=\mono",font=1,
family="mono",font=1)
R text(0,3,label="mono text (bold, italic)family=\mono",font=4,
family="mono",font=4)
R text(0,2,label="sans text (italic)family=\sans",font=3,
family="sans",font=3)
R text(0,1,label="serif text (bold)family=\serif",font=2,
family="serif",font=2)
R mtext("some",line=1,at=-0.5,cex=2,family="sans")
R mtext("different",line=1,at=0,cex=2,family="serif")
R mtext("fonts",line=1,at=0.5,cex=2,family="mono")
```

这里，`text` 用于在预定坐标处放置内容，而 `mtext` 用于添加到顶部图形边距。

# some different fonts

![](img/b2cfc85cbb129f60fe595a2bae074fe4_631_0.png)

图 23-11：通过使用 `family` 和 `font` 图形参数显示字体

### 23.5.2 希腊符号

对于统计或数学技术绘图，注释偶尔需要希腊符号或数学标记。你可以使用 `expression` 函数显示这些，它在其他方面能够调用 R 的 `plotmath`（Murrell and Ihaka, 2000; Murrell, 2011）。使用 `expression` 返回一个特殊对象，其类名与之相同，并且随后可以传递给任何绘图函数中需要显示字符字符串的参数。

暂时聚焦于希腊符号，图 23-12 是使用以下代码生成的：

```
R par(mar=c(3,3,3,3))
R plot(1,1,type="n",xlim=(-1,1),ylim=c(0.5,4.5),xaxt="n",yaxt="n"
    ann=FALSE)
R text(0,4,label=expression(alpha),cex=1.5)
R text(0,3,label=expression(paste("sigma", "sigma", Sigma = "Sigma",
family="mono", cex=1.5))
R text(0,2,label=expression(paste("beta", "gamma", "Phi")),cex=1.5)
R text(0,1,label=expression(paste(Gamma,(",tau,") = 24 when ",tau,") = 5\)),
family="serif", cex=1.5)
R title(main=expression(paste("Gr",epsilon,epsilon, "k")),cex.main=2)
```

# Greek

![](img/b2cfc85cbb129f60fe595a2bae074fe4_632_0.png)

图 23-12：使用 `expression` 显示希腊符号

如果你只想要一个单独的字符，那么像 `expression(alpha)` 这样就足够在绘图中生成 $\alpha$，就像代码块中 `text` 的第一次调用一样。注意，特殊字符的指定是在所需符号名称周围不加引号的情况下完成的。更常见的是，你希望字符与其他组件一起出现，例如普通文本或方程。为此，你需要在 `expression` 的调用中使用 `paste`，用逗号分隔组件。这些在对 `text` 的其余三次调用中显示。

你可以使用 `cex` 控制大小，不过 `family` 和 `font` 的使用仅影响带引号的普通文本，而不影响符号，正如最后一次对 `cex` 的调用所演示的那样。

`title` 函数允许你添加轴和主标题，然后用于通过向 `main` 供应相应的 `expression` 来添加标题“Greek”。在调用中使用 `cex.main=2` 将其大小加倍（需要略有不同的标签 `cex.main` 来区分主标题的大小和通过 `cex.lab` 控制的任何轴标题的大小）。

### 23.5.3 数学表达式

在 R 绘图中格式化整个数学表达式有点复杂，并且让人联想到使用类似 LaTeX 的标记语言。正因如此，我不会在这里详细阐述所需的语法，但我将提供一些示例，展示可能实现的内容，如图 23-13 所示。要创建图像，我首先按如下方式定义了四个 `expression` 对象：

```
R expr1 <- expression(c^2=a[1]^2+b[1]^2)
R expr2 <- expression(paste(pi^{x[i]}, (1-pi)(n-x[i]))
R expr3 <- expression(paste("Sample mean: ",
```

然后我在以下代码中使用它：

```
R par(mar=c(3,3,3,3))
R plot(1,type="n",xlim=(-1,1),ylim=(0.5,4.5),xaxt="n",yaxt="n",
  ann=FALSE)
R text(0,4,1,labels=c(expr1,expr2,expr3,expr4),cex=1.5)
R title(main="Math",cex.main=2)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_633_0.png)

图 23-13：R 绘图中排版数学表达式的一些示例

所有希腊和数学标记都包含在对 `expression` 的调用中。如果需要由逗号分隔的单独组件，其中一些可能是或可能不是普通文本（即带引号），则必须使用 `paste` 来产生最终结果。以下是一些关键说明：

- 上标由 `^` 给出，下标由 `_` 给出；例如，`c^2` `c_2` in expri，以及 `a[1]` 组件提供 `a_12`。

- 你可以用括号 `( )` 对组件进行分组，它们是可见的（例如，`expr2` 的 `(1-pi)^n-(x[i])` 组件），或用大括号 `{ }`，它们不可见（例如，`pi^(x[i])` 组件）。

- 斜体变量用 `italic()` 绘制；例如，`italic(n)` 在 `expr3` 中产生 `n`。

- 常见算术运算符的构造已经存在，例如 `sum( , )` 和 `frac( )`；例如，在 `expr3` 中，调用 `sum(italic(x)[italic(i)],italic(i)=1,italic(n))` 产生看起来像的结果：

![](img/b2cfc85cbb129f60fe595a2bae074fe4_634_0.png)

而 `frac(italic(x)[1]+...+italic(x)[n]),italic(n)` 产生如下表达式：

![](img/b2cfc85cbb129f60fe595a2bae074fe4_634_1.png)

- 还有额外的标记工具用于正确格式化表达式，例如将带引号的普通文本直接与数学标记组合，以及在无需插入引号的情况下在组件之间创建空格。这些需求取决于标记内容所在的确切位置（即 `paste` 调用中的组件或运算符工具 `frac` 的组件）。例如，参见 `expr4` 的 `""=frac( , )` 部分，以及分数分子中两个组件 `x^(alpha-1)~(1-x)^(beta-1)` 的空格分隔，使用 `~`（设置在分数的分子上）。

R 为此类型的图形显示中的字符串格式化内置了大量功能，我在这里没有涵盖。如果你有兴趣了解更多，请在提示符下输入 `?plotmath` 访问文件作为第一步。还有一个非常有用的演示，你可以在 R 中通过输入 `demo(plotmath)` 查看，它展示了可能实现的内容以及 `expression` 的相关语法。

## 23.6 一个完全注释的散点图

为了提供一个涵盖迄今为止你考虑过的大多数概念的最终示例，让我们创建一个详细绘图，展示第 23.4.1 节至 23.4.3 节中使用的 MPG 与马力数据。图 23-14 中的图像显示了最终结果作为底部最大的绘图，顶部有较小的绘图以说明生产的各个阶段。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_635_0.png)

![](img/b2cfc85cbb129f60fe595a2bae074fe4_635_1.png)

图 23-14：`mtcars` 散点图的详细版本，MPG 与马力，点大小与重量成比例

首先，确保你已在工作区中准备好对象 `mpg`、`hp`、`wtcec` 和 `hpgseq2`（在第 23.4.1 节和 23.4.3 节中定义），因为你将使用它们来简化代码的长度。它们再次如下：

```
R hp <- mtcars$hp
R mpg <- mtcars$mpg
R wtcec <- mtcars$wt/mean(mtcars$wt)
R hpgseq2 <- seq(50,325,by=25)
```

绘图，右侧边距比默认稍宽且为 U 形框，使用以下代码开始：

```
R dev.new()
R par(mar=c(5,4,4,4))
R plot(hp,mpg,cex=wtcec,axes=FALSE,ann=FALSE)
R box(bty="u")
```

This provides the top-left image of Figure 23-14. I've used `dev.new` to explicitly open a new graphics device on my machine, which defaults to 7 × 7 inches. You can use `width` and `height` arguments supplied to `dev.new` to alter this on my machine if you want.

Add some axes:

```
R axis(2,las=1,tcl=-0.8,family="mono")
R axis(1,at=hseq2,labels=FALSE,tcl=-1)
```

These two lines add the left vertical axes for MPG; the tick marks are lengthened using `tcl`, their labels are horizontal across, and a `"mono"` is requested. For the horizontal axis (horsepower), longer outward marks are drawn at the values in `hseq2`, their labels are pressed by setting `labels=FALSE`. You'll populate those in a moment.

Rather than MPG as a measure of fuel efficiency, many countries use liters per hundred kilometer (L/100km). So, for their benefit, let's say you want to provide a second axis on the right of the plot that provides L/100km. To do this, you need the conversion formula. Based on a US gallon, an approximate conversion between the two is given by the:

```
MPG ≈ 378.541 / 1.609 × (L/100km)
```

It turns out that function is inverse. That is, to convert from MPG to L/100km, simply swap those variables in the equation.

A little experimentation with the conversion formula, based on the limits of the observed MPG data, has given me a sensible collection of L/100km values at which to mark the right axis.

```
R L100 <- seq(22,13,by=-3)
R L100
[1] 22 19 16 13
```

Note that these are in decreasing order for convenience, since you can see after you convert these to MPG, the results are:

```
R MPG.L100 <- (378.541 / 1.609) / L100
R MPG.L100
[1] 10.69385 12.38236 14.70405 18.09729 23.52648 33.60925
```

This means a smaller number for L/100km means a more efficient car.

Why do you need the MPG version of these numbers? Well, remember that the plot itself is on the scale of MPG, so to instruct R to mark off the appropriate tick marks on the right side, you need the L/100km values in MPG "coordinates."

With that done, one final call to `axis` leaves you with the top-middle plot in Figure 23-14.

```
R axis(4,at=MPG.L100,labels=L100,las=1,tcl=0.3,mgp=c(3,0.3,0),family="mono")
```

Of particular note is that you've used `at` to specify the tick marks on the MPG scale, the values in `MPG.L100`, but since they correspond to the L/100km scale in `L100`, it's the latter vector that you supply to `labels` to actually label those tick marks.

Next, it's time to annotate the axes with some titles and provide the labels for the tick marks on the horizontal axis. Before doing this, construct an expression for the MPG-to-L/100km conversion to label the right vertical.

```
R L100 <- expression(paste(L/100,"km"~"≈"~frac(378.541,1.609)~"×"))
```

In plotmath, the `~` provides an "approximately equal to" sign (≈), and `~` provides an explicit multiplication symbol (×).

Then, by running the following lines, you get the top-right image in Figure 23-14.

```
R title(main="MPG by Horsepower",xlab="Horsepower",ylab="MPG",family="serif")
R mtext(L100,side=4,line=3,family="serif")
R text(hseq2,rep(7.5,length(hseq2)),labels=hseq2,srt=45,
xpd=TRUE,family="mono")
```

The first line places a main title and x- and y axes in a `"serif"` style. `mtext` places a `"serif"` version of the arithmetic expression just created in an appropriate position `line=3` on the right axis (`side=4`). The third line places a `"mono"` style tick labels in `hseq2` at the appropriate coordinate in the same vector, with a vertical position of 7.5, after a little trial and error. Since you're using `text` to draw in the figure margin, you must set `xpd` to TRUE. Special to `text` is the optional `srt` parameter, which allows you to rotate the labels. Here, they've rotated 45 degrees.
