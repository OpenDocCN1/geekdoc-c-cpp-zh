
## 10.9 构建二维变换的另一个示例

假设我们想找到一个 3 × 3 矩阵变换，将整个平面绕点 P = (2, 4) 逆时针旋转 30°，如图 10.14 所示。你可能还记得，WPF 通过类似下面的代码来表达这个变换：

```xml
<RotateTransform Angle="-30" CenterX="2" CenterY="4"/>
```

![](img/f464cd0043eb5336aa0543fe20a0561b_288_0.png)

*图 10.14：* 我们希望将整个平面绕点 P = (2, 4) 逆时针旋转 30°。

随后，WPF 的实现者必须创建一个类似于我们即将构建的矩阵。

这里有两种方法。

首先，我们知道如何绕原点旋转 30°；可以使用本章开头的变换 T1。因此，我们可以分三步完成所需的变换（见图 10.15）。

- 1. 将点 (2, 4) 移到原点。
- 2. 旋转 30°。
- 3. 将原点移回 (2, 4)。

将点 (2, 4) 移到原点的矩阵是

```text
[ 1  0 -2 ]
[ 0  1 -4 ]
[ 0  0  1 ]        (10.74)
```

将其移回的矩阵类似，只是 2 和 4 不再取负。而旋转矩阵（用我们新的 3 × 3 格式表示）是

```text
[ cos 30°  -sin 30°   0 ]
[ sin 30°   cos 30°   0 ]
[   0         0       1 ]        (10.75)
```

因此，表示整个变换序列的矩阵是

```text
[ 1  0  2 ] [ cos 30°  -sin 30°   0 ] [ 1  0 -2 ]
[ 0  1  4 ] [ sin 30°   cos 30°   0 ] [ 0  1 -4 ]
[ 0  0  1 ] [   0         0       1 ] [ 0  0  1 ]        (10.76)
```

> **内联练习 10.18：** (a) 解释为什么这是为得到所需结果而相乘这些变换的正确顺序。  
> (b) 通过将 [2 4 1]^T 依次乘以上面的矩阵序列，验证点 (2, 4) 确实保持不变。

第二种方法同样更加自动化：我们找到三个已知目标位置的点，就像上面处理窗口变换时那样。我们将使用 P = (2, 4)、Q = (3, 4)（P 右侧一个单位的点）和 R = (2, 5)（P 上方一个单位的点）。我们知道希望将 P 映射到 P，将 Q 映射到 (2 + cos 30°, 4 + sin 30°)，将 R 映射到 (2 − sin 30°, 4 + cos 30°)。（画一幅图来说服自己这些是正确的。）实现这一点的矩阵就是

$$
\begin{bmatrix}
2 & 2+\cos30^\circ & 2-\sin30^\circ\\
4 & 4+\sin30^\circ & 4+\cos30^\circ\\
1 & 1 & 1
\end{bmatrix}
\begin{bmatrix}
2 & 3 & 2\\
4 & 4 & 5\\
1 & 1 & 1
\end{bmatrix}^{-1}. \qquad (10.77)
$$

这两种方法都相当容易使用。

还有第三种方法——第二种方法的变体——其中我们指定一个点和两个向量应映射到的位置，而不是指定三个点。在这种情况下，我们可以说希望点 $P$ 保持不动，而向量 $\mathbf e_1$ 和 $\mathbf e_2$ 分别映射到

$$
\begin{bmatrix}
\cos30^\circ\\
\sin30^\circ\\
0
\end{bmatrix}
\quad \text{and} \quad
\begin{bmatrix}
-\sin30^\circ\\
\cos30^\circ\\
0
\end{bmatrix}, \qquad (10.78)
$$

在这种情况下，我们不再寻找把向量 $\mathbf e_1$、$\mathbf e_2$ 和 $\mathbf e_3$ 映射到变换前后所需三个点的矩阵，而是寻找把这些向量映射到变换前后所需一个点和两个向量的矩阵。这些矩阵是

$$
\begin{bmatrix}
2&1&0\\
4&0&1\\
1&0&0
\end{bmatrix}
\quad \text{and} \quad
\begin{bmatrix}
2&\cos30^\circ&-\sin30^\circ\\
4&\sin30^\circ&\cos30^\circ\\
1&0&0
\end{bmatrix}, \qquad (10.79)
$$

因此整体矩阵是

$$
\begin{bmatrix}
2&\cos30^\circ&-\sin30^\circ\\
4&\sin30^\circ&\cos30^\circ\\
1&0&0
\end{bmatrix}
\begin{bmatrix}
2&1&0\\
4&0&1\\
1&0&0
\end{bmatrix}^{-1}. \qquad (10.80)
$$

这些通用技术可用于创建 $w=1$ 平面上的任何线性加平移变换，但有一些特定的变换值得了解。在 $xy$ 平面内旋转角度 $\theta$（将正 $x$ 轴朝正 $y$ 轴方向旋转）由下式给出

$$
R_{xy}(\theta)=
\begin{bmatrix}
\cos\theta&-\sin\theta&0\\
\sin\theta&\cos\theta&0\\
0&0&1
\end{bmatrix}. \qquad (10.81)
$$

在一些书和软件包中，这被称为绕 $z$ 轴旋转；我们更喜欢“在 $xy$ 平面内旋转”这一说法，因为它还表明了旋转方向（从 $x$ 朝向 $y$）。另外两个标准旋转是

$$
R_{yz}(\theta)=
\begin{bmatrix}
1&0&0\\
0&\cos\theta&-\sin\theta\\
0&\sin\theta&\cos\theta
\end{bmatrix}. \qquad (10.82)
$$

以及

$$
R_{zx}(\theta)=
\begin{bmatrix}
\cos\theta&0&\sin\theta\\
0&1&0\\
-\sin\theta&0&\cos\theta
\end{bmatrix}; \qquad (10.83)
$$

注意，最后一个表达式将 $z$ 朝 $x$ 方向旋转，而不是相反方向。使用这种命名约定有助于保持正负号模式对称。

![](img/f464cd0043eb5336aa0543fe20a0561b_289_0.png)

*图 10.15：* 将 $(2,4)$ 平移到原点后、旋转 $30^\circ$ 后，以及将原点平移回 $(2,4)$ 后的房子。

现在代码开头如下：

```xml
<Canvas ...
    <Canvas.Resources>
        <ControlTemplate x:Key="ClockHandTemplate">
            <Polygon
                Points="0.3,-1   -0.2,8   0,9   0.2,8   0.3,-1"
                Fill="Navy"/>
        </ControlTemplate>
        <ControlTemplate x:Key="CircleTemplate">
            <Polygon
                Points="1,0   0.707,0.707   0,1   -0.707,0.707
                        -1,0   -0.707,-0.707   0,-1   0.707,-0.707"
                Fill="LightGray"/>
        </ControlTemplate>
    </Canvas.Resources>
```

这段代码定义了我们用来创建钟面和指针的几何图形。通过这一改动，圆形钟面将通过变换一个模板“圆”来定义，该模板由单位圆上八个均匀分布的点表示。这种指定形式虽然在 WPF 中并不地道，但与许多其他场景图包中的场景指定方式非常相似。

现在场景的实际创建包括从 `CircleTemplate` 构建钟面，以及像之前一样构建指针。

```xml
<!-- 1. Background of the clock -->
<Control Name="Face"
         Template="{StaticResource CircleTemplate}">
    <Control.RenderTransform>
        <ScaleTransform ScaleX="10" ScaleY="10" />
    </Control.RenderTransform>
</Control>

<!-- 2. The minute hand -->
<Control Name="MinuteHand"
         Template="{StaticResource ClockHandTemplate}">
    <Control.RenderTransform>
        <TransformGroup>
            <RotateTransform Angle="180" />
            <RotateTransform x:Name="ActualTimeMinute" Angle="0" />
        </TransformGroup>
    </Control.RenderTransform>
</Control>

<!-- 3. The hour hand -->
<Control Name="HourHand" Template="{StaticResource ClockHandTemplate}">
    <Control.RenderTransform>
        <TransformGroup>
            <ScaleTransform ScaleX="1.7" ScaleY="0.7" />
            <RotateTransform Angle="180" />
            <RotateTransform x:Name="ActualTimeHour"
                             Angle="0" />
        </TransformGroup>
    </Control.RenderTransform>
</Control>
```

剩下的就是从 `Canvas` 到 WPF 坐标的变换，以及用于动画的计时器，它们会设置 `ActualTimeMinute` 和 `ActualTimeHour` 的值。

```xml
<Canvas.RenderTransform>
  ...same as before...
</Canvas.RenderTransform>

<Canvas.Triggers>
  <EventTrigger RoutedEvent="FrameworkElement.Loaded">
    <BeginStoryboard>
      <Storyboard>
        <DoubleAnimation
          Storyboard.TargetName="ActualTimeHour"
          Storyboard.TargetProperty="Angle"
          From="0.0" To="360.0"
          Duration="00:00:01.0" RepeatBehavior="Forever"
        />
        <DoubleAnimation
          Storyboard.TargetName="ActualTimeMinute"
          Storyboard.TargetProperty="Angle"
          From="0.0" To="4320.0"
          Duration="00:00:01.0" RepeatBehavior="Forever"
        />
      </Storyboard>
    </BeginStoryboard>
  </EventTrigger>
</Canvas.Triggers>

</Canvas>
```

作为将此场景描述转换为图像的起点，我们假设有一个基本图形库：给定表示多边形的点数组，它就能绘制该多边形。这些点将由一个 3×k 的齐次坐标三元组数组表示，因此数组的第一列将是第一个多边形点的齐次坐标，依此类推。

现在我们将解释如何从类似 WPF 描述的内容转到一系列 drawPolygon 调用。首先，让我们把 XAML 代码转换为树结构，如图 10.18 所示，表示场景图（见第 6 章）。

我们把变换画成菱形，把几何图形画成蓝色框，把命名部件画成米色框。目前，我们省略了 ClockHandTemplate 的实例化问题，并假定钟表指针的几何图形有两个独立且完全相同的副本。我们还在每个变换旁边画出了该变换的矩阵表示。我们假设 ActualTimeHour 中的角度为 15°（其余弦和正弦分别约为 0.96 和 0.26），ActualTimeMinute 中的角度为 180°（即钟表显示 12:30）。

> **内联练习 10.19：** (a) 记住 WPF 中的旋转以度为单位指定，并且它们以*顺时针*方向旋转对象，检查给出的将时针旋转 15° 的矩阵是否正确。  
> (b) 如果你发现该矩阵有误，回想一下在 WPF 中 x 向右增加，y 向*下*增加。这会改变你的答案吗？顺便说一下，如果你在 WPF 中运行此程序，调试并打印该矩阵，你会发现在 (2, 1) 元素而不是 (1, 2) 元素上有负号。这是因为 WPF 内部使用行向量表示点，并在右侧乘以变换矩阵。
