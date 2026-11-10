
![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_264_0.png)

**图 10.1**  
用于凹凸贴图的扰动法线向量。

如果我们能找到生成相应法线的方法，就能得到皱褶表面。

图 10.1 展示了与单个“凹凸”相对应的修改法线的概念。

因此，如果我们想让一个对象看起来具有凹凸（或皱纹、陨石坑等），一种方法是计算这种表面上会存在的*法线*。然后，当场景被照亮时，光照会产生所需的错觉。这由 Blinn 于 1978 年首次提出 [BL78]，并随着在片元着色器中执行逐像素光照计算的能力的出现而变得实用。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_264_1.png)

**图 10.2**  
程序化凹凸贴图示例。

程序 10.1 中展示的顶点和片元着色器给出了一个示例，它生成一个具有如图 10.2 所示“高尔夫球”表面的圆环体。该代码与之前程序 7.2 中所见几乎相同。唯一显著的变化在片元着色器中——传入的插值法线向量（在原程序中名为“varyingNormal”）被修改为凹凸，这些凹凸通过将正弦波函数沿 X、Y 和 Z 轴应用于圆环模型的原始（未变换）顶点来计算。注意，因此顶点着色器现在需要将这些未变换的顶点沿管线向下传递。

以这种方式使用运行时计算的数学函数来修改法线，称为*程序化凹凸贴图*。

### 程序 10.1 程序化凹凸贴图

**顶点着色器**

```glsl
#version 430
// same as Phong shading, but add this output vertex attribute:
out vec3 originalVertex;
...
void main(void)
{ // Include this pass-through of original vertex for interpolation:
    originalVertex = vertex;
    ...
}
```

**片元着色器**

```glsl
#version 430
// same as Phong shading, but add this input vertex attribute:
in vec3 originalVertex;
...
void main(void)
{
    ...
    //add the following to perturb the incoming normal vector:
    float a = 0.25;                 // a controls height of bumps
    float b = 100.0;                // b controls width of bumps
    float x = originalVertex.x;
    float y = originalVertex.y;
    float z = originalVertex.z;
    N.x = varyingNormal.x + a*sin(b*x);  // perturb incoming normal using sine function
    N.y = varyingNormal.y + a*sin(b*y);
    N.z = varyingNormal.z + a*sin(b*z);
    N = normalize(N);
    // lighting computations and output fragColor (unchanged) now utilize the perturbed normal N
    ...
}
```

## 10.2 法线贴图

凹凸贴图的一种替代方法是使用查找表替换法线。这使我们能够构造没有数学函数的凹凸，例如与月球陨石坑对应的凹凸。一种常见方法称为*法线贴图*。

为了理解其工作原理，我们首先注意到，一个向量可以以合理精度存储在三个字节中，X、Y、Z 分量各占一个字节。这使得可以将法线存储在彩色图像文件中，其中 R、G、B 分量分别对应 X、Y、Z。图像中的 RGB 值以字节存储，通常解释为范围 [0,1] 内的值，而向量的分量值可以为正或负。如果我们将法线向量分量限制在范围 [-1,+1] 内，那么一种可将法线向量 N 作为像素存储在图像文件中的简单转换是

R = (N_x + 1) / 2  
G = (N_y + 1) / 2  
B = (N_z + 1) / 2

法线贴图利用一个图像文件（称为*法线贴图*），其中包含与光照下所需表面外观相对应的法线。在法线贴图中，向量相对于任意 X-Y 平面表示，其 X 和 Y 分量表示相对于“垂直”的偏差，Z 分量设为 1。严格垂直于 X-Y 平面的向量（即没有偏差）将表示为 (0,0,1)，而非垂直向量将具有非零的 X 和/或 Y 分量。我们使用上述公式转换到 RGB 空间；例如，(0,0,1) 将存储为 (.5,.5,1)，因为实际偏移范围为 [-1,+1]，而 RGB 值范围为 [0,1]。

我们可以通过纹理单元的另一种巧妙应用来利用这种法线贴图：不在纹理单元中存储颜色，而是存储所需的法线向量。然后，我们可以使用采样器为给定片元查找法线贴图中的值，并且不是将返回的值应用于输出像素颜色（如我们在纹理贴图中所做的那样），而是将其用作法线向量。

这种法线贴图图像文件的一个示例如图 10.3 所示。它是通过将 GIMP 法线贴图插件 [GI21] 应用于来自 Luna [LU16] 的纹理而生成的。法线贴图图像文件并非供观看；我们展示这个示例是为了指出此类图像最终大部分呈蓝色。这是因为图像文件中的每个条目都有 B 值 1（最大蓝色），如果观看图像，会使其显得“偏蓝”。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_266_0.png)

**图 10.3**  
法线贴图图像文件示例 [LU16]。

图 10.4 展示了两个不同的法线贴图图像文件（二者均由 Luna [LU16] 的纹理构建）以及在 Blinn-Phong 光照下将它们应用于球体的结果。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_267_0.png)

从法线贴图中获取的法线向量不能直接使用，因为如上所述，它们是相对于任意 *X-Y* 平面定义的，没有考虑其在对象上的位置及其在世界空间中的方向。我们解决此问题的策略是构建一个变换矩阵，以将法线转换到世界空间，如下所示。

在对象上的每个顶点处，我们考虑一个与该对象相切的平面。该顶点处的对象法线垂直于该平面。我们在该平面中定义两个相互垂直且也垂直于法线的向量，称为*切线*和*副切线*（有时称为*副法线*）。构建所需变换矩阵要求我们的模型为每个顶点包含一个切线向量（副切线可以通过计算切线与法线的叉积来构建）。如果模型尚未定义切线向量，则可以计算它们。对于球体，可以精确计算它们，如下面对程序 6.1 的修改所示：

```
...
for (int i=0; i<=prec; i++)
{
  for (int j=0; j<=prec; j++)
  {
    float y = (float)cos(toRadians(180-i*180/prec));
    float x = -(float)cos(toRadians(i*360/prec)) * (float)abs(cos(asin(y)));
    float z = (float)sin(toRadians(i*360/prec)) * (float)abs(cos(asin(y)));
    vertices[i*(prec+1)+j].set(x,y,z);
  }
}
```

着色器使用片元的纹理坐标来提取与当前片元对应的法线贴图条目。采样器变量“normMap”用于此目的，在此情况下绑定到纹理单元 0（注意，因此 Java/JOGL 应用程序必须已将法线贴图图像附加到纹理单元 0）。为了将颜色分量从存储范围 [0..1] 转换回其原始范围 [-1..+1]，我们乘以 2.0 并减去 1.0。

然后将 TBN 矩阵应用于所得法线，以生成当前像素的最终法线。着色器的其余部分与用于 Phong 光照的片元着色器相同。片元着色器如程序 10.2 所示，基于 Etay Meiri [ME11] 的版本。

存在多种用于开发法线贴图图像的工具。一些图像编辑工具，例如 GIMP [GI21] 和 Photoshop [PH21]，具有此类功能。此类工具分析图像中的边缘，推断峰和谷，并生成相应的法线贴图。

图 10.5 展示了由 Hastings-Trew [HT12] 基于 NASA 卫星数据创建的月球表面纹理贴图。相应的法线贴图是通过将 GIMP 法线贴图插件 [GN12] 应用于同样由 Hastings-Trew 创建的黑白简化图而生成的。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_269_0.png)

**图 10.5**  
月球、纹理和法线贴图。
