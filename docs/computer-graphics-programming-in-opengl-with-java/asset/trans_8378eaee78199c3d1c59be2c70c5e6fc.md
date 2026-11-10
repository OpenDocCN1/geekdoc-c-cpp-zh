

处理完成）。因此，LOD 计算（它告诉细分器要生成多少个顶点）会在每个面片的第 0 个顶点处理期间进行。

### 程序 12.5 细分的细节层次（LOD）

细分控制着色器

```glsl
...
void main(void)
{
    float subdivisions = 16.0;    // tunable constant based on density of detail in height map
    if (gl_InvocationID == 0)
    {
        vec4 p0 = mvp * gl_in[0].gl_Position;    // control pt. positions in screen space
        vec4 p1 = mvp * gl_in[1].gl_Position;
        vec4 p2 = mvp * gl_in[2].gl_Position;
        p0 = p0 / p0.w;
        p1 = p1 / p1.w;
        p2 = p2 / p2.w;
        float width = length(p2.xy - p0.xy) * subdivisions + 1.0;    // perceived "width" of tess grid
        float height = length(p1.xy - p0.xy) * subdivisions + 1.0;   // perceived "height" of tess grid
        gl_TessLevelOuter[0] = height;    // set tess levels based on perceived side lengths
        gl_TessLevelOuter[1] = width;
        gl_TessLevelOuter[2] = height;
        gl_TessLevelOuter[3] = width;
        gl_TessLevelInner[0] = width;
        gl_TessLevelInner[1] = height;
    }
    // forward texture coordinates and control points to TES as before
    tcs_out[gl_InvocationID] = tcs[gl_InvocationID];
    gl_out[gl_InvocationID].gl_Position = gl_in[gl_InvocationID].gl_Position;
}
```

将这些控制着色器更改应用到图 12.7 中场景的实例化（但未光照）版本，并将高度图替换为图 12.8 所示的 Hastings-Trew 调校得更精细的版本，就会生成图 12.10 所示的改进场景，其地平线细节更加逼真。

在这个示例中，将评估着色器中的布局限定符从

```glsl
layout(quads, equal_spacing, ccw) in;
```

改为

```glsl
layout(quads, fractional_even_spacing, ccw) in;
```

也很有用。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_316_0.png)

**图 12.10** 具有受控细节层次（LOD）的细分月球。

这种修改的原因很难用静态图像说明。在动画场景中，当细分对象在 3D 空间中移动时，如果使用了 LOD，有时可以*看到*对象表面细分级别的变化，表现为称为“跳变”的抖动伪影。从*等间距*改为*小数间距*可以减弱这种效果，因为它使相邻面片实例的网格几何结构更加相似，即使它们的细节层次不同。（参见练习 12.2 和 12.3。）

采用 LOD 可以显著降低系统负载。例如，在动画运行时，与不控制 LOD 的情况相比，场景更不容易显得卡顿或出现延迟。

将这种简单的 LOD 技术应用到包含 Phong 着色的版本（即程序 12.4）会稍微棘手一些。这是因为相邻面片实例之间的 LOD 变化又会引起相关法向量的突然变化，从而在光照中造成跳变伪影！与往常一样，构建复杂 3D 场景时需要考虑权衡和折中。

### 补充说明

将细分与 LOD 结合使用，在实时虚拟现实应用中特别有用，因为这些应用既需要复杂细节来实现真实感，又需要频繁的物体移动和/或相机位置变化，例如计算机游戏。在本章中，我们展示了细分和 LOD 在实时地形生成中的用法，尽管它也可以应用于其他领域，例如 3D 模型的位移映射（其中将细分顶点添加到模型表面，然后移动这些顶点以增加细节）。它在计算机辅助设计应用中也有用。

Sellers 及其同事将 LOD 技术（如程序 12.5 所示）扩展到了我们介绍的范围之外，他们还消除了*位于相机后方*的面片中的顶点（他们通过将内部和外部级别设置为零来实现这一点）[SW15]。这是*剔除*技术的一个示例，而且它非常有用，因为实例化细分仍可能给系统带来负载。

程序 12.1 中使用的 createShaderProgram() 四参数版本已添加到 Utils.java 文件中。稍后，我们将添加其他版本以支持几何着色器阶段。

## 练习

- 12.1 修改程序 12.1，试验不同的内部和外部细分级别值，并观察生成的渲染网格。
- 12.2 按第 12.4 节所述，测试程序 12.5，将评估着色器中的布局限定符设置为 equal_spacing，然后设置为 fractional_even_spacing。观察相机移动时对渲染表面的影响。在第一种情况下应能观察到跳变伪影，而在第二种情况下这些伪影大多得到缓解。
- 12.3 *（项目）* 修改程序 12.4，使用你自己设计的高度图（你可以使用之前在练习 10.2 中构建的高度图）。然后添加光照和阴影映射，使你的细分地形能够投射阴影。这是一个复杂的练习，因为第一和第二个阴影映射通道中的一些代码需要移到评估着色器中。

## 参考文献

- [GN12] GIMP 法线贴图插件，访问于 2021 年 3 月，https://code.google.com/archive/p/gimp-normalmap/
- [HT12] J. Hastings-Trew，*JHT 的行星像素商场*，访问于 2021 年 3 月，http://planetpixelemporium.com/
- [LU16] F. Luna，*《DirectX 12 3D 游戏编程导论》*，第 2 版（Mercury Learning，2016 年）。
- [SW15] G. Sellers、R. Wright Jr. 和 N. Haemel，*《OpenGL 超级宝典：综合教程与参考》*，第 7 版（Addison-Wesley，2015 年）。
- [TS21] 曲面细分，维基百科，访问于 2021 年 3 月，https://en.wikipedia.org/wiki/Tessellation

## 第 13 章：几何着色器

- **13.1** *OpenGL 中的逐图元处理* … 299
- **13.2** *修改图元* … 301
- **13.3** *删除图元* … 305
- **13.4** *添加图元* … 306
- **13.5** *更改图元类型* … 309
- *补充说明* … 310

在 OpenGL 管线中，紧接在细分曲面之后的是*几何阶段*。在这里，程序员可以选择包含*几何着色器*。这个阶段实际上早于细分曲面出现；它在 2009 年的 3.2 版中成为 OpenGL 核心的一部分。

与细分曲面类似，几何着色器使程序员能够以顶点着色器中不可能做到的方式操作顶点的*组*。在某些情况下，某项任务既可以使用细分着色器完成，也可以使用几何着色器完成，因为它们的能力在某些方面有重叠。

### 13.1 OpenGL 中的逐图元处理

几何着色器阶段位于细分曲面和光栅化之间，处于管线中专门用于*图元处理*的部分中（请回顾图 2.2）。顶点着色器支持一次操作一个顶点，片元着色器支持一次操作一个片元（本质上是一个像素），而*几何着色器支持一次操作一个图元*。

回想一下，图元是 OpenGL 中绘制对象的基本构建块。可用的图元类型只有少数几种；我们将主要关注操作三角形的几何着色器。因此，当我们说几何着色器可以一次操作一个图元时，通常是指该着色器可以一次访问*三角形的全部三个顶点*。几何着色器允许你：

- 一次访问一个图元中的所有顶点，然后
- 原样输出同一个图元，或者
- 输出同一个图元但修改顶点位置，或者
- 输出不同类型的图元，或者
- 输出额外的图元，或者
- 删除该图元（完全不输出它）。

与细分评估着色器类似，传入的顶点属性在几何着色器中可作为*数组*访问。然而，在几何着色器中，传入属性数组的索引范围仅到图元大小。例如，如果图元是三角形，则可用索引为 0、1 和 2。访问顶点本身通过预定义数组 `gl_in` 完成，如下所示：

```glsl
gl_in[2].gl_Position   // position of the 3rd vertex
```

同样与细分评估着色器类似，几何着色器的输出顶点属性都是*标量*。也就是说，输出是一系列形成图元的单个顶点（它们的位置和其他属性变量，如果有的话）。

有一个布局限定符用于设置图元输入/输出类型和输出大小。

特殊 GLSL 命令 `EmitVertex()` 指定要输出一个顶点。特殊 GLSL 命令 `EndPrimitive()` 表示完成构建特定图元。

内置变量 `gl_PrimitiveID` 可用，它保存当前图元的 ID。ID 编号从 0 开始，一直计数到图元数量减 1。

我们将探讨四类常见操作：

- 修改图元
- 删除图元
- 添加图元
- 更改图元类型

