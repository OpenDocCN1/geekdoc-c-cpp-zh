

# 26.1.2 视觉增强和图例

你也可以以熟悉的方式以及新的方式改变散点图的显示外观。例如，可选的 type 参数默认为 "p" 表示 "points"，会将最近的散点图中的点绘制为点。你可以将点绘制为 3D 球体，type="s"。你可以使用 size 控制任何绘制点的大小或球体的大小，并可以使用 col 控制颜色（或颜色）。legend 函数是 legend 的 rgl 类似物，也很有用：它通过改变交互式绘图所在的背景图像来工作。

为了说明这些修改，让我们重新绘制相同的鸢尾花观测数据。首先，清除任何打开的 R 图形设备。然后，执行以下操作：

```
R plot3d(x=pwid,z=sw,size=1.5,type="s",ncol=c(1,2,3)[as.numeric(iris$Species)])
```

这将启动一个新的 RGL 设备，根据花种对球体进行着色。像往常一样，你将 col 参数传递给与绘制坐标长度相同的向量，它将以逐元素的方式将颜色分配给相应的点。你在传统的 R 图形参数 cex 上指定 size 参数，它会根据 type 的值而变化——请查阅帮助文件 ?plot3d 了解详情。通过一点实验，很容易找到适合绘图的大小值。

要添加图例，首先使用你喜欢的显示尺寸调整 RGL 设备，然后执行以下操作：

```
R legend3("topright",col=1:3,legend=levels(iris$Species),pch=16,cex=2)
```

这会插入一个静态的、不可移动的图例，通过颜色引用绘制的物种。legend3 函数实际上调用了基础 R 的 legend 函数，因此它们可以方便地以相同的方式使用。静态图例就位后，散点图仍然完全交互式，你可以继续旋转和缩放。图 26-2 显示了全部内容。

legend3 函数会改变背景画布，这就是为什么在添加图例之前你必须打开一个新设备并手动调整大小的原因。如果你在同一设备中不关闭或重置背景的情况下在同一设备中生成新的 rgl 绘图，花种图例仍会存在。如果你要制作多个 rgl 绘图，可以随时通过调用以下命令将背景重置为默认的白色画布：

```
R bg3d(color="white")
```

如果你在最近的绘图仍处于活动状态时尝试这样做，你会看到花种图例消失而散点图仍然存在。或者，你也可以在完成后关闭 RGL 设备，以便后续的任何绘图都使用新设备。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_727_0.png)

图 26-2：重新绘制鸢尾花花瓣宽度、花瓣长度和萼片宽度数据。观测值绘制为球体，增大尺寸，并根据物种类型着色；图例通过 legend3d 添加。

## 26.13 添加进一步的 3D 组件

你还可以向当前 3D 绘图添加新的观测值和线条。rgl 包包含 points3d、lines3d 和 segments3d 函数，类似于基础 R 图形中的 points、lines 和 segments。作为示例，在第 25.2.2 节中，你使用了一个可选参数将垂直线添加到 scatterplot3d 中每个绘制点的 x-y 平面底部。在 plot3d 散点图中，你将使用 segments3d 实现相同的效果。此外，你还可以使用 rgl 图形的 grid3d 函数添加 scatterplot3d 绘图中默认在同一平面上绘制的网格。

让我们付诸实践。回顾一下第 652 页的图 25-8。使用 rgl 功能创建类似的绘图，其中颜色用于引用第四个连续变量，萼片长度，首先重新创建调色板并为每个观测值设置颜色。这里使用 50 种颜色的分类完成（参见第 25.1.4 节）。

```
R> slen <- colorRampPalette("purple","yellow","blue")
R> cols <- slen.pal(50)
R> cols <- cut(slen,breaks=seq(min(slen),max(slen),length=51),
      include.lowest=TRUE)
```

然后，选择任何当前活动的 RGL 设备或清除所关注设备的背景。plot3d 的调用以适当着色的球体开始绘图。

```
plot3d(x=pwid,y=plen,z=swid,type="s",size=1.5,col=cols[slen.cols],
      aspect=c(1.1,1.75,1),xlab="Petal width",ylab="Petal length",
      zlab="Sepal width")
```

你向 aspect 参数提供长度为 3 的向量，描述 x、y 和 z 轴的相对长度，按此顺序。通过将顺序更改为 1.7，你使 y 轴相对于其他轴变长。这会在 y 轴上产生拉伸效果。颜色是通过使用 slen.cols 因子向量进行向量索引分配的，而 xlab、ylab 和 zlab 用于整理轴标题。

现在，要从 x 平面向每个观测值添加一条垂直线，使用其基础对应物，segments3d 不会将“from”和“to”坐标分离到不同的参数中（回想一下 segments 和 arrows 中 x0、y0、x1 和 y1 的使用）。它将提供给 x、y 和 z 参数的每对观测值视为每条线的开始和结束，按此顺序。

因此，在现有 RGL 设备上绘制垂直线时，你首先需要设置包含 3D 空间中“from”位置和“to”位置的这些向量。考虑以下代码：

```
xfromto <- rep(pwid,each=2)
yfromto <- rep(plen,each=2)
zfromto <- rep(min(swid),times=2*nrow(iris))
zfromto[seq(2,length(zfromto),2)] <- swid
```

前两行分别通过复制每个观测值两次来设置 x 和 y 分量的向量 xfromto 和 yfromto。这些很容易，在这些坐标方向上“from-to”值不会改变。z 分量则会改变。你通过复制最小宽度值 min(swid) 两倍数据集的大小来创建 zfromto 向量，这样你就有一个与 xfromto 和 yfromto 长度匹配的向量。zfromto 的每个第二个位置都使用萼片宽度向量的元素覆盖。这为所有观测值提供了“from”z 值 min(swid)，以 segments3d 所要求的成对方式与 swid 本身中的“to”z 值匹配。有了 xfromto 和 yfromto，你将得到从绘图的底部 x-y 平面（其垂直位置自动水平设定在 min(swid)）向上到实际 swid 值（当然是每个球体的相应 z 值）的线条。

交互式 3D 绘图 695

为了帮助理解它们是如何设置的，将坐标向量输出到你的控制台屏幕以便查看它们包含的内容。然后调用 segments3d 将线条放置在绘图上。

```
R segments3d(x=xfromto,y=yfromto,z=zfromto,col=rep(cols[slen.cols],each=2))
```

为了确保每条线的颜色与其对应的球体匹配，还需要将由 cols[slen.cols] 提供的向量索引的颜色集合的每个条目复制两次，这意味着“from-to”颜色。然后，执行以下行将在下部 x-y 平面上放置一个参考网格：

```
R grid3d(side="z-")
```

side 参数你指定要保持恒定的轴（在本例中，）以及放置网格的末端（在本例中，因为你希望网格位于 z 轴的下端，你使用减号符号）。要将网格放置在垂直轴的上端，即长方体棱柱的顶部，你将指定 side="z+"。

最后，你可以向绘图添加自定义颜色图例以引用萼片长度。bgplot3d 函数是 legend3 的更通用版本；它允许你指定任何绘图命令来定义 RGL 设备背景。让我们使用 shape 包的 colorlegend 函数来做到这一点，该函数在 25.1.5 中首次探讨。确保 shape 包已加载并且你的散点图 RGL 设备已调整到你喜欢的大小。在我的机器上，我执行以下操作：

```
R bgplot3d({plot.new();colorlegend(len.pal(50),clim=range(len), zval=seq(4.5,7.5,0.5),digit=1, posc=(0.91,0.93),posc=(0.1,0.9), main="Sepal length")})
```

bgplot3d 函数可以接受多个绘图命令，你需要以大括号 {} 中的块形式提供，每个命令用分号（;）分隔。在此示例中，初始调用 plot.new() 初始化 RGL 设备的背景，以便你可以添加连续颜色图例。没有该调用，colorlegend 仍然可以工作，但会发出警告。图 26-3 显示了最终结果，散点图仍然可以用鼠标旋转和缩放。

能够使用简单的鼠标命令旋转 3D 散点图以及接下来的几节中看到的所有绘图，特别是在探索高维数据的可视化时非常有用。你不受单一视点的限制，也不需要在实际生成绘图之前手动决定视角。rgl 功能也使向轴绘图添加额外元素变得容易——这是更困难的事情

