
![](img/1695de1bc7486362f86c143285f3fb40_310_0.png)

- *C++/OpenGL 应用程序*  
  我们加载并激活一个额外的纹理来保存法线贴图。我们还会像之前的应用程序那样添加代码来指定光照和材质。
- *顶点着色器*  
  唯一新增的是光照 uniform 变量和法线贴图采样器的声明。通常放在顶点着色器中的光照代码被移到细分求值着色器中，因为顶点直到细分阶段才会生成。
- *细分控制着色器*  
  唯一新增的是光照 uniform 变量和法线贴图采样器的声明。
- *细分求值着色器*  
  Phong 光照的预备代码现在放在求值着色器中：

  ```cpp
  varyingVertPos = (mv_matrix * position).xyz;
  varyingLightDir = light.position - varyingVertPos;
  ```
- *片元着色器*  
  前面描述的用于计算 Phong（或 Blinn-Phong）光照的典型代码段在这里完成，同时还包括从法线贴图中提取法线的代码。然后，光照结果通过加权和与纹理图像组合。

![](img/1695de1bc7486362f86c143285f3fb40_311_0.png)

**图 12.9**  
带法线贴图和光照的细分地形（光源分别位于左侧和右侧）。

包含高度映射、法线映射和 Phong 光照的最终结果如图 12.9 所示。地形现在会响应光照。在此示例中，左图中位置光源放在中心偏左处，右图中则放在中心偏右处。

尽管从静态图片中很难看出对光源移动的响应，但读者应该能够辨别漫反射光照变化，以及两幅图中山峰上的镜面高光非常不同。当相机或光源移动时，这当然会更明显。结果仍然不完美，因为输出中融入的原始纹理包含阴影，无论光照如何，这些阴影都会出现在渲染结果中。

## 12.4 控制细节层次（LOD）

像程序 12.4 中那样使用实例化实时生成数百万个顶点，即使对配置良好的现代计算机也可能造成负担。幸运的是，将地形划分为独立面片的策略——正如我们为提高生成的网格顶点数量所做的那样——也为我们提供了一种减轻该负担的良好机制。

在生成的数百万个顶点中，许多并非必要。靠近相机的面片中的顶点很重要，因为我们期望能辨认附近物体的细节。然而，面片离相机越远，光栅化中甚至很可能没有足够的像素来证明我们正在生成的顶点数量是合理的！

根据与相机的距离改变面片中的顶点数量，这种技术称为*细节层次*，或 *LOD*。Sellers 等人描述了一种在实例化细分中通过修改控制着色器来控制 LOD 的方法 [SW15]。程序 12.5 展示了 Sellers 等人方法的简化版本。该策略是利用面片的感知大小来确定其细分级别的值。由于面片的细分网格最终将放置在进入控制着色器的四个控制点所定义的方形内，我们可以利用控制点相对于相机的位置来确定应为该面片生成多少顶点。步骤如下：

- 1. 通过对四个控制点应用 MVP 矩阵来计算它们的屏幕位置。
- 2. 计算由控制点在屏幕空间中定义的方形的边长（即宽度和高度）。请注意，尽管四个控制点构成一个方形，但由于应用了透视矩阵，这些边长可能不同。
- 3. 根据细分级别所需的精度（基于高度图中的细节量），用一个可调常数缩放长度值。
- 4. 将缩放后的长度值加 1，以避免指定细分级别为 0（这会导致不生成任何顶点）。
- 5. 将细分级别设置为计算得到的相应宽度和高度值。

回想一下，在我们的实例化示例中，我们不是只创建一个网格，而是创建 64×64 个网格。因此，前一个列表中的五个步骤会对每个面片执行。因此，细节层次因面片而异。

所有更改都在控制着色器中，并显示在程序 12.5 中，生成的输出随后见图 12.10。请注意，变量 gl_InvocationID 指的是正在处理面片中的哪个顶点（而不是正在处理哪个面片）。因此，告诉细分器要生成多少顶点的 LOD 计算会在处理每个面片的第 0 个顶点期间进行。

### 程序 12.5 细分细节层次（LOD）

**细分控制着色器**

```glsl
    ...
    void main(void)
    {
        float subdivisions = 16.0;                 // tunable constant based on density of detail in height map
        if (gl_InvocationID == 0)
        {
            vec4 p0 = mvp * gl_in[0].gl_Position;      // control pt. positions in screen space
            vec4 p1 = mvp * gl_in[1].gl_Position;
            vec4 p2 = mvp * gl_in[2].gl_Position;
            p0 = p0 / p0.w;
            p1 = p1 / p1.w;
            p2 = p2 / p2.w;
            float width = length(p2.xy - p0.xy) * subdivisions + 1.0;   // perceived "width" of tess grid
            float height = length(p1.xy - p0.xy) * subdivisions + 1.0;  // perceived "height" of tess grid
            gl_TessLevelOuter[0] = height;             // set tess levels based on perceived side lengths
            gl_TessLevelOuter[1] = width;
            gl_TessLevelOuter[2] = height;
            gl_TessLevelOuter[3] = width;
            gl_TessLevelInner[0] = width;
            gl_TessLevelInner[1] = height;
        }
        // forward texture coordinates and control points to TES as before
        tcs_out[gl_InvocationID] = tcs_in[gl_InvocationID];
        gl_out[gl_InvocationID].gl_Position = gl_in[gl_InvocationID].gl_Position;
    }
```

将这些控制着色器更改应用到图 12.7 中场景的实例化（但未加光照）版本，并将高度图替换为图 12.8 中所示的 Hastings-Trew 更精细调整的版本，便产生了图 12.10 所示的改进场景，其地平线细节更逼真。

在此示例中，将求值着色器中的布局限定符从以下内容更改也很有用：

```glsl
    layout (quads, equal_spacing, cw) in
```

![](img/1695de1bc7486362f86c143285f3fb40_313_0.png)

**图 12.10**  
带受控细节层次（LOD）的细分月球。

## 练习

- 12.1 修改程序 12.1，试验各种内部和外部细分级别的值，并观察生成的渲染网格。
- 12.2 将求值着色器中的布局限定符设置为 equal_spacing，然后设置为 fractional_even_spacing（如第 12.4 节所述），测试程序 12.5。观察相机移动时对渲染表面的影响。在第一种情况下，你应该能观察到跳变伪影，而在第二种情况下这些伪影大多得到缓解。
- 12.3（项目）修改程序 12.4，以使用你自己设计的高度图（你可以使用之前在练习 10.2 中构建的高度图）。然后添加光照和阴影贴图，使你的细分地形能够投射阴影。这是一个复杂的练习，因为第一和第二个阴影贴图渲染通道中的一些代码需要移到求值着色器中。

## 参考文献

- [GP16] GIMP 插件注册表，*法线贴图插件*，访问于 2020 年 7 月，https://code.google.com/archive/p/gimp-normalmap
- [HT12] J. Hastings-Trew，*JHT 的行星像素商场*，访问于 2020 年 7 月，http://planetpixelemporium.com/
- [LU16] F. Luna，*DirectX 12 3D 游戏编程入门*，第 2 版（Mercury Learning，2016）。
- [SW15] G. Sellers、R. Wright Jr. 和 N. Haemel，*OpenGL 超级宝典：综合教程与参考*，第 7 版（Addison-Wesley，2015）。
- [TS20] Tessellation，维基百科，访问于 2020 年 7 月，https://en.wikipedia.org/wiki/Tessellation

