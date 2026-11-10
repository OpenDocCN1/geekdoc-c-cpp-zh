

![](img/1695de1bc7486362f86c143285f3fb40_324_0.png)

![](img/1695de1bc7486362f86c143285f3fb40_324_1.png)

**图 13.6** 几何着色器，图元删除。

**图 13.7** 显示背面的图元删除。

无需对代码做其他更改。注意 mod 函数的使用——所有顶点都会通过，但每三个图元中的第一个图元内的顶点除外，这些顶点会被忽略。这里同样，渲染背面三角形可以提高真实感，如图 13.7 所示。

## 13.4 添加图元

几何着色器最有趣且最强大的用途之一，可能是向正在渲染的模型添加额外顶点和/或图元。这使得可以实现诸如增加对象细节以改进高度映射，或完全改变对象形状等操作。

考虑以下示例，我们将圆环中的每个三角形改为一个微小的三角锥。

我们的策略与之前“爆炸”圆环示例类似，如图 13.8 所示。传入的三角形图元的顶点用于定义金字塔的底面。金字塔的侧壁由这些顶点以及一个新点（称为“尖点”）构成，该点通过对原始顶点的法线求平均计算得到。然后，通过取从尖点指向底面的两个向量的叉积，为金字塔的三个“侧面”分别计算新的法向量。

![](img/1695de1bc7486362f86c143285f3fb40_325_0.png)

程序 13.3 中的几何着色器对圆环中的每个三角形图元执行此操作。对于每个传入三角形，它输出三个三角形图元，总共九个顶点。每个新三角形都在函数 `makeNewTriangle()` 中构建，该函数被调用三次。它计算指定三角形的法线，然后调用函数 `setOutputValues()` 为每个发射的顶点分配适当的输出顶点属性。在发射全部三个顶点后，它调用 `EndPrimitive()`。为确保光照准确执行，会为每个新创建的顶点计算光照方向向量的新值。

### 程序 13.3 几何着色器：添加图元

```glsl
...
vec3 newPoints[9], lightDir[9];
float sLen = 0.01;   // sLen is the "spike length", the height of the small pyramid

void setOutputValues(int p, vec3 norm)
{  varyingNormal = norm;
   varyingLightDir = lightDir[p];
   varyingVertPos = newPoints[p];
   gl_Position = proj_matrix * vec4(newPoints[p], 1.0);
}

void makeNewTriangle(int p1, int p2)
{  // generate surface normal for this triangle
   vec3 c1 = normalize(newPoints[p1] - newPoints[3]);
   vec3 c2 = normalize(newPoints[p2] - newPoints[3]);
   vec3 norm = cross(c1,c2);

   // generate and emit the three vertices
   setOutputValues(p1, norm); EmitVertex();
   setOutputValues(p2, norm); EmitVertex();
   setOutputValues(3, norm); EmitVertex();
   EndPrimitive();
}
void main(void)
{
    // offset the three triangle vertices by the original surface normal
    vec3 sp0 = gl_in[0].gl_Position.xyz + varyingOriginalNormal[0]*sLen;
    vec3 sp1 = gl_in[1].gl_Position.xyz + varyingOriginalNormal[1]*sLen;
    vec3 sp2 = gl_in[2].gl_Position.xyz + varyingOriginalNormal[2]*sLen;

    // compute the new points comprising a small pyramid
    newPoints[0] = gl_in[0].gl_Position.xyz;
    newPoints[1] = gl_in[1].gl_Position.xyz;
    newPoints[2] = gl_in[2].gl_Position.xyz;
    newPoints[3] = (sp0 + sp1 + sp2)/3.0;       // spike point

    // compute the directions from the vertices to the new points
    lightDir[0] = light.position - newPoints[0];
    lightDir[1] = light.position - newPoints[1];
    lightDir[2] = light.position - newPoints[2];
    lightDir[3] = light.position - newPoints[3];

    // build three new triangles to form a small pyramid on the surface
    makeNewTriangle(0,1); // the third point is always the spike point
    makeNewTriangle(1,2);
    makeNewTriangle(2,0);
}
```

![](img/1695de1bc7486362f86c143285f3fb40_326_0.png)

结果输出如图 13.9 所示。如果增大尖点长度（sLen）变量，添加的表面“金字塔”会更高。然而，在没有阴影的情况下，它们可能显得不真实。将阴影映射添加到程序 13.3 中留作读者练习。

**图 13.9.** 几何着色器：图元添加。

谨慎应用此技术可以模拟尖刺、荆棘和其他细微表面凸起，也可以模拟相反的效果，例如凹痕和坑洞（[DV20]，[KS16]）。

## 13.5 更改图元类型

OpenGL 允许在几何着色器中切换图元类型。此功能的一个常见用途是将输入三角形转换为一个或多个输出线段，以模拟毛发或头发。尽管头发仍然是较难逼真生成的现实世界对象之一，但在许多情况下，几何着色器有助于实现实时渲染。

程序 13.4 展示了一个几何着色器，它将每个传入的三顶点三角形转换为一条朝外的两顶点线段。它首先通过对三角形顶点位置求平均来计算一缕头发的起点，从而生成三角形的质心。然后，它使用程序 13.3 中相同的“尖点”作为头发的终点。输出图元被指定为包含两个顶点的线条带，第一个顶点是起点，第二个顶点是终点。结果如图 13.10 所示，其中圆环以七十二个切片的维度实例化。

![](img/1695de1bc7486362f86c143285f3fb40_327_0.png)

当然，这只是生成完全逼真头发的起点。让头发弯曲或移动需要若干修改，例如为线条带生成更多顶点，并计算它们沿曲线的位置和/或引入随机性。由于线段缺乏明显的表面法线，光照会变得复杂；在此示例中，我们只是将法线指定为与原始三角形的表面法线相同。

### 程序 13.4 几何着色器：更改图元类型

```glsl
layout (line_strip, max_vertices=2) out;
...
void main(void)
{
    vec3 op0 = gl_in[0].gl_Position.xyz;            // original triangle vertices
    vec3 op1 = gl_in[1].gl_Position.xyz;
    vec3 op2 = gl_in[2].gl_Position.xyz;
    vec3 ep0 = gl_in[0].gl_Position.xyz + varyingNormal[0]*sLen;    // offset triangle vertices
    vec3 ep1 = gl_in[1].gl_Position.xyz + varyingNormal[1]*sLen;
    vec3 ep2 = gl_in[2].gl_Position.xyz + varyingNormal[2]*sLen;

    // compute the new points comprising a small line segment
    vec3 newPoint1 = (op0 + op1 + op2)/3.0;          // original (start) point
    vec3 newPoint2 = (ep0 + ep1 + ep2)/3.0;          // end point

    gl_Position = proj_matrix * vec4(newPoint1, 1.0);
    varyingVertPosG = newPoint1;
    varyingLightDirG = light.position - newPoint1;
    varyingNormalG = varyingNormal[0];
    EmitVertex();

    gl_Position = proj_matrix * vec4(newPoint2, 1.0);
    varyingVertPosG = newPoint2;
    varyingLightDirG = light.position - newPoint2;
    varyingNormalG = varyingNormal[1];
    EmitVertex();

    EndPrimitive();
}
```

## 补充说明

几何着色器的吸引力之一在于它们相对易于使用。尽管许多使用几何着色器的应用*本来可以*通过曲面细分实现，但几何着色器的机制通常使其更易于实现和调试。当然，几何着色器与曲面细分相比的相对适用性取决于具体应用。

生成令人信服的头发或毛发具有挑战性，并且根据应用不同会采用多种技术。在某些情况下，简单的纹理映射就足够了，和/或使用曲面细分或几何着色器，例如本章展示的基本技术。当需要更高的真实感时，运动（动画）和光照会变得棘手。用于生成头发和毛发的两个专用工具是 *HairWorks*（NVIDIA GameWorks 套件的一部分 [GW20]）和 *TressFX*（由 AMD 开发 [TR20]）。前者同时适用于 OpenGL 和 DirectX，而后者仅适用于 DirectX。使用 TressFX 的示例可在 [GP14] 中找到。

