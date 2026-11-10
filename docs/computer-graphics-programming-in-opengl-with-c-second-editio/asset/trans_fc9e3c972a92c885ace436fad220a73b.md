
## 12.3 地形/高度图的细分

回顾一下，在顶点着色器中执行高度映射可能会因顶点数量不足而无法渲染出所需细节。既然现在我们已有办法生成大量顶点，那就回到 Hastings-Trew 的月球表面纹理图（来自 [HT12]），通过抬升*细分*后的顶点将其用作*高度图*，以生成月球表面细节。正如我们将看到的，这样做的好处是能够获得与月球图像更匹配的顶点几何形状，并改善轮廓（边缘）细节。

我们的策略是修改程序 12.1，在 X-Z 平面中放置一个细分网格，并使用高度映射来设置每个细分网格点的 Y 坐标。为此不需要面片，因为我们可以硬编码细分网格的位置。因此，我们将像程序 12.1 那样，在 glDrawArrays() 和 glPatchParameteri() 中指定每个面片所需的最少 1 个顶点。Hastings-Trew 的月球纹理图像既用于颜色，也用作高度图。

我们通过在细分评估着色器中将细分网格的 gl_TessCoord 值映射到适合顶点和纹理的范围，来生成顶点坐标和纹理坐标。⁴ 高度映射也在细分评估着色器中执行，具体做法是将月球纹理颜色分量的一小部分加到输出顶点的 Y 分量上。着色器的修改如程序 12.3 所示。

⁴ 在某些应用中，纹理坐标是在外部生成的，例如当细分用于为导入的模型提供额外顶点时。在这种情况下，所提供的纹理坐标将需要进行插值。

### 程序 12.3 简单细分地形

**顶点着色器**

```c
#version 430
uniform mat4 mvp_matrix;
layout(binding = 0) uniform sampler2D tex_color;
void main(void) { }
```

**细分控制着色器**

```c
...
layout(vertices = 1) out;    // no control points are necessary for this application
void main(void)
{  int TL=32;
   if (gl_InvocationID == 0)
   {  gl_TessLevelOuter[0] = TL; gl_TessLevelOuter[2] = TL;
      gl_TessLevelOuter[1] = TL; gl_TessLevelOuter[3] = TL;
      gl_TessLevelInner[0] = TL; gl_TessLevelInner[1] = TL;
   }
}
```

**细分评估着色器**

```c
...
out vec2 tes_out;
uniform mat4 mvp_matrix;
layout(binding = 0) uniform sampler2D tex_color;
void main (void)
{  // map the tessellated grid vertices from [0..1] onto the desired vertices [-0.5,+0.5]
   vec4 tessellatedPoint = vec4(gl_TessCoord.x - 0.5, 0.0, gl_TessCoord.y - 0.5, 1.0);
   // map the tessellated grid vertices as texture coordinates by "flipping" the Y values vertically.
   // Vertex coordinates have (0,0) at upper left, texture coordinates have (0,0) at the lower left.
   vec2 tc = vec2(gl_TessCoord.x, 1.0 - gl_TessCoord.y);
   // The image is grayscale, so either component (R, G, or B) can serve as height offset.
   tessellatedPoint.y += (texture(tex_color, tc).r) / 40.0;      // Scale down color values.
   // convert the height-map raised point to eye space
   gl_Position = mvp_matrix * tessellatedPoint;
   tes_out = tc;
}
```

**片元着色器**

```c
...
in vec2 tes_out;
out vec4 color;
layout (binding = 0) uniform sampler2D tex_color;

void main(void)
{
    color = texture(tex_color, tes_out);
}
```

片元着色器与程序 12.2 中的片元着色器类似，仅根据纹理图像输出颜色。C++/OpenGL 应用程序基本上没有变化——它加载纹理（该纹理同时充当纹理和高度图），并为其启用采样器。图 12.6 显示了纹理图像（左侧）以及第一次尝试的最终输出；遗憾的是，它尚未实现正确的高度映射。

![](img/1695de1bc7486362f86c143285f3fb40_306_0.png)

最初的结果存在严重缺陷。尽管我们现在能在远处地平线上看到轮廓细节，但那里的隆起与纹理图中的实际细节并不对应。回顾一下，在高度图中，白色应表示“高”，黑色应表示“低”。尤其是右上方的区域显示出巨大的山丘，它们与图像中的明暗颜色毫无关系。

该问题的原因是细分网格的分辨率。细分器可生成的顶点最大数量取决于硬件，而为了符合 OpenGL 标准，每个细分级别至少需要支持最大值为 64。我们的程序指定了一个内部和外部细分级别均为 32 的单一细分网格，因此生成了约 32*32，也就是刚过 1000 个顶点，这不足以准确反映图像中的细节。这在右上方尤其明显（图中已放大）——边缘细节仅沿地平线在 32 个点处采样，因而产生了看起来随机的大型山丘。即使将细分值提高到 64，总计 64*64，也就是刚过 4000 个顶点，对于使用月球图像进行高度映射而言仍然远远不够。

增加顶点数量的一种好方法是使用实例化，我们在第 4 章已经见过。我们的策略是让细分器生成网格，并使用实例化将其重复多次。在顶点着色器中，我们构建一个由四个顶点定义的面片，每个顶点对应细分网格的一个角。在 C++/OpenGL 应用程序中，我们将 glDrawArrays() 调用改为 glDrawArraysInstanced()。在那里，我们指定一个 64×64 的面片网格，每个面片包含一个细分级别大小为 32 的细分网格。这样总共会得到 64*64*32*32，也就是超过四百万个顶点。

顶点着色器首先指定四个纹理坐标 (0,0)、(1,0)、(0,1) 和 (1,1)。使用实例化时，请记住顶点着色器可以访问一个整数变量 gl_InstanceID，它保存与当前正在处理的 glDrawArraysInstanced() 调用相对应的计数器。我们使用这个 ID 值来分配各个面片在较大网格中的位置。面片按行和列定位：第一个面片位于位置 (0,0)，第二个位于 (1,0)，下一个位于 (2,0)，依此类推，第一列的最后一个面片位于 (63,0)。下一列的面片位于 (0,1)、(1,1)，一直到 (63,1)。最后一列的面片位于 (0,63)、(1,63)，一直到 (63,63)。给定面片的 X 坐标是实例 ID 对 64 取模，Y 坐标是实例 ID 除以 64（整数除法）。然后着色器将这些坐标缩放回 [0..1] 范围。

控制着色器没有变化，只是传递顶点和纹理坐标。

接下来，细分评估着色器接收传入的细分网格顶点（由 gl_TessCoord 指定），并将它们移动到传入面片所指定的坐标范围中。它对纹理坐标也做同样的处理。它还应用高度

**细分评估着色器**

```glsl
...
in vec2 tes_out[1];
out vec2 tes_out;
void main(void)
{  // map the texture coordinates onto the sub-grid specified by the incoming control points
   vec2 tc = vec2(tes_out[0].x + (gl_TessCoord.x) / 64.0, tes_out[0].y + (1.0 - gl_TessCoord.y) / 64.0);

   // map the tessellated grid onto the sub-grid specified by the incoming control points
   vec4 tessellatedPoint = vec4(gl_in[0].gl_Position.x + gl_TessCoord.x / 64.0, 0.0,
                                gl_in[0].gl_Position.z + gl_TessCoord.y / 64.0, 1.0);

   // add the height from the height map to the vertex:
   tessellatedPoint.y += (texture(tex_height, tc).r) / 40.0;
   gl_Position = mvp_matrix * tessellatedPoint;
   tes_out = tc;
}
```

既然已经实现了高度映射，我们就可以着手改进它并加入光照。一个挑战是，我们的顶点还没有关联的法向量。另一个挑战是，简单地将纹理图像用作高度图会产生过于“锯齿状”的结果——在这个例子中，是因为纹理图像中的灰度变化并非都源于高度。对于这张特定的纹理图，恰好 Hastings-Trew 已经制作了一幅改进的高度图，我们可以使用它 [HT12]。该图如图 12.8 左侧所示。

为了创建法向量，我们可以在运行时计算它们：生成相邻顶点（或高度图中的相邻纹素）的高度，构建连接它们的向量，并使用叉积求出法向量。这需要根据场景（和/或高度图图像）的精度进行一些调整。在这里，我们改用 GIMP 的“normalmap”插件 [GP16]，基于 Hastings-Trew 的高度图生成法线贴图，如图 12.8 右侧所示。

![](img/1695de1bc7486362f86c143285f3fb40_309_0.png)

**图 12.7** 细分地形——第二次尝试，使用实例化。
