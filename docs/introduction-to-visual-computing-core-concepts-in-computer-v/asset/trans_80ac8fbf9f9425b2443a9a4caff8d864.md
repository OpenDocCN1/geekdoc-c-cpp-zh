

![](img/66c45bbed85bb7ba7f7b05dff49b5060_336_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_336_1.png)

Increasing c_d

Increasing s

Figure 14.4. 此图展示了我们简单的环境光、漫反射光和镜面光照对物体的影响。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_336_2.png)

Ambient
Ambient + Diffuse
Ambient + Diffuse + Specular

Figure 14.5. 此图展示了我们简单的环境光、漫反射光和镜面光照对物体从两个不同视角的影响。

restrictive and may not be able to provide the visual effect of a large number of materials, it is quite effective in interactive applications due to its simplicity.

对于漫反射光和镜面光照，通常会使用衰减参数来模拟光强随离光源距离增加而衰减的效果。因此，我们不用 I 而用 I/f，其中 f 是依赖于点光源到表面点距离 d 的函数。物理上，f ∝ d²。但为了给应用程序提供更多控制参数，f 被定义为

![](img/66c45bbed85bb7ba7f7b05dff49b5060_337_0.png)

Figure 14.6. 此图展示了相同光源在平面着色（左）、高洛德着色（中）和 Phong 着色（右）下的效果。注意高洛德着色遗漏了金字塔上被 Phong 着色捕捉到的镜面高光。

as f = ad² + bd + c where a, b and c are parameters that can be set by the application.

回想一下，前述模型假设了点光源。其他种类的光源是定向光源或面光源。定向光源是沿单一均匀方向照射的光，即从光源发出的所有光线彼此平行。面光源更像是一个光面板而不是一个光点。定向光源在计算机图形学中常用于模拟太阳等强远距离光源。定向光源可通过无限远的点光源来建模。因此，只使用光方向向量 L，并且忽略衰减因子（将其设为 1）。面光源或扩展光源可通过一组紧密放置的点光源来建模。计算机图形学中另一种经常有用的光源是聚光灯。它被建模为角范围受限的光源。角度由点光源和定义被聚光灯照亮区域的表面上圆所形成的圆锥角给出。

## 14.2 Shading

一旦我们在每个顶点计算出光照，我们需要在光栅化期间计算三角形内部某一点的光照。基于顶点处的光照对三角形内部进行绘制的过程称为着色。交互式图形中使用了三种着色算法。

Flat Shading: 这里我们为每个三角形计算一次光照。这可以通过对三角形三个顶点的法向量取平均来实现。然后，我们可以使用光照模型为整个三角形计算一次颜色，并在光栅化期间将相同的颜色应用于三角形的每个像素。平面着色的优点是其简单性。然而，一个边可能从其上的两个三角形得到截然不同的颜色。因此，

## Put a Face to the Name

Bui Tuong Phong 被认为是在推进交互式计算机图形学方面的重要人物之一，这得益于他提出了一种计算成本低廉的简单光照模型，使得以每秒 30 帧的视频速率实现光照成为可能。他以其著名的名言而闻名：“我们并不期望能够像现实中那样精确地显示物体，包括纹理、阴影等。我们只希望显示一个足够接近真实物体的图像，以提供一定程度的真实感”，这句话概括了交互式图形背后的哲学。Bui Tuong Phong 出生于 1942 年的河内，当时是法国印度支那的一部分。他后来移居西贡，然后移居法国，在 1966 年于格勒诺布尔理工学院获得理科学士学位，并在 1968 年于 ENSEEIHT 图卢兹获得工程师文凭。1968 年，他加入了信息与自动化研究所（当时为 INRIA）担任计算机科学研究员，从事数字计算机操作系统开发工作。1971 年 9 月，他前往犹他大学工程学院攻读博士学位，1973 年毕业后加入斯坦福大学担任教授。Phong 在读学生期间就知道自己患有白血病这种绝症，并在完成论文不久后去世。尽管他只活了 33 年，但他在交互式计算机图形学领域留下了长久的影响。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_340_0.png)

让我们现在考虑渲染的第二遍。从观察者视角创建的深度缓冲区 Z_v 记录了仅对观察者可见的 3D 点的深度。其余 3D 点在我们判断其是否处于阴影的上下文中无关紧要。对于从观察者视角可见的这些点，我们需要找到它们相对于光源的深度。让我们考虑一个 3D 点 P = (X, Y, Z_v)，它是在使用矩阵 M_v 进行 3D 到 2D 投影（视图变换后）并进行遮挡解析后在 (x_v, y_v) 处最终渲染的点。我们知道

M_v^{-1} \begin{pmatrix} x_v \\ y_v \\ \frac{1}{Z_v} \\ 1 \end{pmatrix} = \begin{pmatrix} X \\ Y \\ Z_v \end{pmatrix} \tag{14.4}

![](img/66c45bbed85bb7ba7f7b05dff49b5060_341_0.png)

Figure 14.8. 此图展示了渲染阴影的流程。从左到右：无阴影渲染的 3D 场景、第一次渲染后得到的阴影贴图、帧缓冲中处于阴影中的点用非绿色值表示，这些非绿色像素颜色被衰减以产生阴影效果。注意球体也会相互投射阴影。

同一点相对于光源的深度 $Z_v^l$ 因此可通过以下方式求得

$$\begin{pmatrix} x_l \\ y_l \\ \frac{1}{Z_v^l} \end{pmatrix} = M_l \begin{pmatrix} X \\ Y \\ Z_v \end{pmatrix} = M_l M_v^{-1} \begin{pmatrix} x_v \\ y_v \\ \frac{1}{Z_v} \\ 1 \end{pmatrix} \tag{14.5}$$

乘以 $4 \times 4$ 矩阵 $M_l M_v^{-1}$ 矩阵可得到同一点 P 相对于光源的投影和深度。如果 $Z_l(x_l, y_l) < Z_v^l$，则点 P 处于阴影中，且帧缓冲在 $(x_v, y_v)$ 处的颜色会被小于 1.0 的因子衰减以产生阴影效果。整个过程如图 14.8 所示。

## 14.4 Texture Mapping

纹理映射是将 2D 图像贴到物体上以增加数字场景丰富度和视觉细节的过程。纹理映射使用三种坐标系：2D 纹理空间、3D 物体空间和 2D 屏幕空间。纹理图像的 2D 坐标定义在 2D 纹理空间中。场景中物体的顶点 3D 坐标定义在 3D 物体空间中。最后，投影物体原语内部的像素坐标定义在 2D 屏幕空间中。物体空间中的每个 3D 顶点坐标都被分配一个纹理空间中的纹理坐标。屏幕空间在光栅化期间用于将图像映射到投影物体原语内部，在纹理映射过程中使用。

### 14.4.1 Texture to Object Space Mapping

在此步骤中，一个矩形 2D 图像被映射到任意 3D 形状上。直观上，这类似于给复杂的 3D 物体（例如花瓶、水果碗、托盘）包礼物。形状越复杂，映射越困难（例如书很容易包礼物，而地球仪则不容易）。因此，在将 2D 图像映射到复杂形状上时，不同位置会出现不同程度的拉伸或褶皱，这完全取决于底层局部几何形状以及我们如何局部地将纹理包裹其上。让我们用两个坐标 s 和 t 定义纹理空间，其中 0 ≤ s, t ≤ 1。设 (x, y, z) 表示物体空间中需要分配 2D 纹理坐标的顶点的 3D 坐标。在本节中我们将描述计算 3D 物体坐标的 2D 纹理坐标的方法。有两种计算这种映射的方法。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_342_0.png)

Figure 14.9. 此图展示了使用两个参数对纹理映射的物体或表面进行参数化表示，左侧为圆柱，右侧为球体。

parameters: u, −180 ≤ u ≤ 180, defining the angle around the axis and v, 0 ≤ v ≤ 1, defining the height of the cylinder (Figure 14.9). Therefore, a 3D point (x, y, z) on the surface can be expressed by the two parameters (u, v) as follows.

```
x = r cos(u);  (14.6)
y = r sin(u);  (14.7)
z = v.  (14.8)
```

通过求解上述方程，我们可以计算圆柱上任意顶点 (x, y, z) 相关的 2D 参数 (u, v)。接下来，我们可以将 (u, v) 与归一化纹理坐标 (s, t) 关联为

```
s = (u + 180) / 360;  (14.9)
t = v.  (14.10)
```

类似地，球体可由两个角度 u, −180 ≤ u ≤ 180 和 v, −90 ≤ u ≤ 90 参数化（图 14.9）。同样，我们可以定义 2D 参数化

Parametric Shapes: There are shapes that have 2D parametric representations, such as a sphere or a cylinder. In such cases, we will map the two coordinates of the texture space to the two parameters used for the parametric surface representation. Consider an example of a cylinder. A 3D point (x, y, z) on a cylinder of radius r can be described using two

