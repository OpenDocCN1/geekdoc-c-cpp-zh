
假设我们使用这样一种方法：已将阴影纹理附加到自定义帧缓冲区，那么 OpenGL 提供了一些相对简单的工具，用于在我们绘制对象时判断每个像素是否处于阴影中。以下是第二遍中处理的细节摘要：

-   构建用于从光照空间转换到纹理空间的“B”变换矩阵（实际上，在 init() 中做这件事更合适）。
-   启用阴影纹理以进行查找。
-   启用颜色输出。
-   启用 GLSL 第二遍渲染程序，其中包含顶点着色器和片段着色器。
-   根据相机位置（像通常一样）为正在绘制的对象构建 MVP 矩阵。
-   构建 shadowMVP2 矩阵（如前所述，纳入 B 矩阵）——着色器将需要它来查找阴影纹理中的像素坐标。
-   将矩阵变换发送到着色器 uniform 变量。
-   像通常一样，启用包含顶点、法向量和纹理坐标（如果使用）的缓冲区。
-   调用 glDrawArrays()。

除了渲染职责外，顶点着色器和片段着色器还有额外任务：

-   顶点着色器将顶点位置从相机空间转换到光照空间，并将得到的坐标通过顶点属性发送给片段着色器，以便它们被插值。这使得从阴影纹理中检索正确的值成为可能。
-   片段着色器调用 textureProj() 函数，该函数返回 0 或 1，指示像素是否处于阴影中（该机制稍后解释）。如果处于阴影中，着色器通过不包含其漫反射和高光贡献来输出更暗的像素。

阴影映射是一项非常常见的任务，因此 GLSL 提供了一种特殊类型的采样器变量，称为 sampler2DShadow（如前所述），它可以附加到 C++/OpenGL 应用程序中的阴影纹理上。textureProj() 函数用于从阴影纹理中查找值，它类似于我们在第 5 章中见过的 texture()，不同之处在于它使用 vec3 来索引纹理，而不是通常的 vec2。由于像素坐标是 vec4，因此需要将其投影到 2D 纹理空间，以便在阴影纹理贴图中查找深度值。正如我们将在下面看到的，textureProj() 为我们完成了所有这些工作。

顶点和片段着色器代码的其余部分实现了 Blinn-Phong 着色。这些着色器如图 8.6 和图 8.7 所示，其中新增的用于阴影映射的代码已突出显示。

让我们更仔细地研究如何使用 OpenGL 在正在渲染的像素与阴影纹理中的值之间执行深度比较。我们从顶点着色器中的模型空间顶点坐标开始，将其乘以 shadowMVP2，生成与投影到光照空间中的顶点坐标相对应的阴影纹理坐标，这些坐标先前是从光源视角生成的。插值后的（3D）光照空间坐标 (x,y,z) 在片段着色器中按如下方式使用。

```glsl
#version 430
layout (location=0) in vec3 vertPos;
layout (location=1) in vec3 vertNormal;

out vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;
out vec4 shadow_coord;

struct PositionalLight { vec4 ambient, diffuse, specular; vec3 position; };
struct Material { vec4 ambient, diffuse, specular; float shininess; };
uniform vec4 globalAmbient;
uniform PositionalLight light;       // light's position is assumed to be in eye space
uniform Material material;
uniform mat4 mv_matrix;
uniform mat4 proj_matrix;
uniform mat4 norm_matrix;
uniform mat4 shadowMVP2;
layout (binding=0) uniform sampler2DShadow shTex;

void main(void)
{
    varyingVertPos = (mv_matrix * vec4(vertPos,1.0)).xyz;
    varyingLightDir = light.position - varyingVertPos;
    varyingNormal = (norm_matrix * vec4(vertNormal,1.0)).xyz;
    varyingHalfVec = (varyingLightDir + varyingVertPos).xyz;
    shadow_coord = shadowMVP2 * vec4(vertPos,1.0);
    gl_Position = proj_matrix * mv_matrix * vec4(vertPos,1.0);
}
```

**图 8.6**  
阴影映射第二遍顶点着色器。

```glsl
#version 430
in vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;
in vec4 shadow_coord;
out vec4 fragColor;

// same structs and uniforms as in the vertex shader
. . .
void main(void)
{  vec3 L = normalize(varyingLightDir);
   vec3 N = normalize(varyingNormal);
   vec3 V = normalize(varyingVertPos);
   vec3 H = normalize(varyingHalfVec);

   float notInShadow = textureProj(shTex, shadow_coord);
   fragColor = globalAmbient * material.ambient + light.ambient * material.ambient;
   if(notInShadow == 1.0)
   {  fragColor += light.diffuse * material.diffuse * max(dot(L,N),0.0)
         + light.specular * material.specular
         * pow(max(dot(H,N),0.0),material.shininess*3.0);
   }
}
```

**图 8.7**  
阴影映射第二遍：片段着色器。

z 分量表示从光源到该像素的距离。(x,y) 分量用于检索存储在（2D）阴影纹理中的深度信息。这个检索到的值（到最靠近光源的对象的距离）会与 z 进行比较。该比较产生一个“二元”结果，告诉我们正在渲染的像素是否比最靠近光源的对象离光源更远（即该像素是否处于阴影中）。

如果在 OpenGL 中我们像前面所述使用 glFramebufferTexture()，并且启用*深度测试*，那么如片段着色器（图 8.7）所示使用 sampler2DShadow 和 *textureProj()* 将正好完成我们所需的工作。也就是说，*textureProj()* 将根据深度比较输出 0.0 或 1.0。基于这个值，我们随后可以在片段着色器中，当像素比最靠近光源的对象离光源更远时，省略漫反射和高光贡献，从而在适当的时候有效地创建阴影。概览如图 8.8 所示。

现在，我们已准备好构建 C++/OpenGL 应用程序，以配合前面描述的着色器工作。

![](img/1695de1bc7486362f86c143285f3fb40_219_0.png)

## 8.8 阴影映射示例

考虑图 8.9 中的场景，其中包括一个圆环体和一个金字塔。一个位置光源已放置在左侧（注意高光）。

金字塔*应该*在圆环体上投下阴影。

![](img/1695de1bc7486362f86c143285f3fb40_219_1.png)

为阐明该示例的开发过程，我们的第一步将是*将第一遍渲染到屏幕*，以确保它正常工作。为此，我们将临时向第一遍添加一个简单的片段着色器（它不会包含在最终版本中），该着色器仅输出一种恒定颜色（例如红色）；例如：

```glsl
#version 430
out vec4 fragColor;
void main(void)
{ fragColor = vec4(1.0, 0.0, 0.0, 0.0);
}
```

假设前一个场景的原点位于图形中心，即金字塔和圆环体之间。在第一遍中，我们将相机放置在光源位置（图 8.10 左侧），并将其指向 (0,0,0)。如果我们随后用红色绘制对象，就会产生图 8.10 右侧所示的输出。注意靠近顶部的圆环体——从这个视角看，它部分位于金字塔后面。

![](img/1695de1bc7486362f86c143285f3fb40_220_0.png)

**图 8.10**  
第一遍：场景（左）从光源视角看（右）。

包含光照和阴影映射的完整两遍 C++/OpenGL 代码如程序 8.1 所示。

### 程序 8.1 阴影映射

```cpp
// Much is the same as we have seen before. New sections to support shadows are highlighted.
// The imports necessary for lighting, etc., would be included at the start, as are the same as before,
// and are not shown here.

// variable declarations for rendering programs, buffers, shader sources, etc., would go here.
...
ImportedModel pyramid("pyr.obj");            // define the pyramid
Torus myTorus(0.6f, 0.4f, 48);               // define the torus
int numPyramidVertices, numTorusVertices, numTorusIndices;

...
// locations of torus, pyramid, camera, and light
glm::vec3 torusLoc(1.6f, 0.0f, -0.3f);
glm::vec3 pyrLoc(-1.0f, 0.1f, 0.3f);
glm::vec3 cameraLoc(0.0f, 0.2f, 6.0f);
glm::vec3 lightLoc(-3.8f, 2.2f, 1.1f);

// properties of white light (global and positional) used in this scene
float globalAmbient[4] = { 0.7f, 0.7f, 0.7f, 1.0f };
float lightAmbient[4] = { 0.0f, 0.0f, 0.0f, 1.0f };
float lightDiffuse[4] = { 1.0f, 1.0f, 1.0f, 1.0f };
float lightSpecular[4] = { 1.0f, 1.0f, 1.0f, 1.0f };
```
