
图 8.5
阴影映射 pass 1 顶点和片元着色器。

## 8.4.2 阴影映射（中间步骤）——将 Z 缓冲区拷贝到纹理

OpenGL 提供了两种方法将 Z 缓冲区深度数据放入纹理单元。第一种方法是生成一个空的阴影纹理，然后使用 `glCopyTextureImage2D()` 命令将活动深度拷贝到阴影纹理中。

第二种方法是在 pass 中构建一个“自定义帧缓冲区”（而不是使用默认的 Z 缓冲区），并使用 `glFramebufferTexture()` 将阴影纹理附加到上面。该命令被引入 OpenGL 3.0 以进一步支持阴影映射。使用这种方法时，没有必要“拷贝”Z 缓冲区到纹理，因为缓冲区已经附加了纹理，深度信息由 OpenGL 自动放入纹理。这是我们在实现中中使用的方法。

## 8.4.3 阴影映射（第二阶段 PASS）——带阴影的场景渲染

pass 的大部分将与我们在第 7 章看到的相似。具体来说，是在这里我们渲染整个场景及其中的所有项目，以及光照、材质和任何纹理。我们还需要添加必要的代码来确定每个像素是否处于阴影中。

pass two 的重要特性是它利用了 MVP 矩阵。一个是将对象坐标转换为屏幕坐标的标准 MVP 矩阵（如大多数示例所示）。另一个是在 pass one 中生成的用于从光源位置渲染的 `shadowMVP` 矩阵——在 pass two 中尝试查找纹理中的像素时会出现问题。相机利用 [-1,1] 空间，而纹理映射利用 [0,1] 空间。一种常见的解决方案是构建一个额外的变换矩阵，称为 `B`，它将相机空间转换为纹理空间。推导 `$B$` 非常简单——先乘以半，再乘以半。`$B$` 矩阵如下：

$$
B = \begin{bmatrix} 0.5 & 0 & 0.5 \\ 0 & 0.5 & 0.5 \\ 0 & 0 & 1 \end{bmatrix}
$$

`$B$` 然后连接到用于 pass two 的 `shadowMVP` 矩阵：

```
shadowMVP = B * shadowMVP_{(pass1)}
```

假设我们使用将阴影纹理附加到自定义帧缓冲区的方法，OpenGL 提供以下是 pass two 中处理的细节总结：

- 构建从光到纹理空间的“B”变换矩阵（实际上是在 `init()` 中完成的）。
- 用于查找的阴影纹理。
- 启用颜色输出。
- 启用包含顶点和片元着色器的 GLSL pass two 程序。
- 根据相机位置（如法线）构建对象的 MVP 矩阵。
- 构建 `shadowMVP` 矩阵（结合 `B` 矩阵）——着色器需要在阴影纹理中查找像素。
- 将变换发送到 uniform 变量。
- 启用包含顶点、法线纹理坐标的缓冲区（如果使用）。
- 调用 `glDrawArrays()`。除了渲染职责，顶点和片元着色器还有额外任务：

- 顶点着色器将顶点位置从相机空间转换为光源空间，并将结果发送到片元着色器以便进行插值。这使得从阴影纹理检索正确值成为可能。
- 片元着色器调用 `textureProj()` 函数，通过不包含漫反射和光谱贡献来输出较暗的像素。

阴影映射是 GLSL 提供的一种特殊类型采样器变量，称为 `sampler2Shadow`（前所述），它可以附加到 OpenGL 应用中的阴影纹理上。`textureProj()` 函数用于从阴影纹理中查找值，与我们在第 5 章看到的 `texture()` 类似，但它使用 `vec3` 而不是通常的 `vec2`。由于像素坐标是 `vec4`，因此需要投影到 2D 纹理空间以查找纹理图中的深度值。正如我们将看到的，`textureProj()` 为我们完成了这一切。

顶点和片元着色器代码剩余实现了 Blinn-Phong 着光。这些着色器位于图 8.6 和 8.7，其中高亮了阴影映射的代码。

让我们仔细检查如何使用 OpenGL 在正在渲染的像素与阴影纹理中的值之间执行深度比较。我们在顶点着色器中从模型空间的顶点开始，乘以 `shadowMVP2` 以产生投影到光源空间（之前从光源视角生成）的阴影纹理坐标。插值的（3D）光坐标 $(x,y,z)$ 用于：

```
#version 430

layout(location=0) in vec3 vertPos;

layout(location=1) in vec3 vertNormal;

out vec3 varyingNormal, varyingLightDir, varyingVertPos, varyingHalfVec;

out vec4 shadow_coord;

struct PositionalLight {vec4 ambient, diffuse, specular; vec3 position;};

struct Material {vec4 ambient, diffuse, specular; float shininess};

uniform vec4 ambient;

uniform PositionalLight light; // 假设光源位置在眼部空间

uniform Material material;

uniform mat4 mv_matrix;

uniform mat4 prj_matrix;

uniform mat4 norm_matrix;

uniform mat4 shadowMVP2;

layout(binding=8) uniform sampler2DShadow shadowTex;

void main() {

    varyingVertPos = mv_matrix * vec4(vertPos, 1.0).xyz;

    varyingLightDir = light.position - varyingVertPos;

    varyingNormal = (norm_matrix * vec4(vertNormal, 1.0)).xyz;

    varyingHalfVec = varyingLightDir - varyingVertPos.xyz;

    shadow_coord = shadowMVP2 * vec4(vertPos, 1.0);

    gl_Position = prj_matrix * mv_matrix * vec4(vertPos, 1.0);

}
```

图 8.6
阴影映射 pass 2 顶点着色器。

# 198 使用 C++ 的 OpenGL 图形编程

```cpp
#version 430

vec3 varyingNormal, varyingLightDtr, varyingVertPos, varyingHalfVec;

out vec4 shadow_coord;

out vec4 fragColor;

// 顶点着色器中相同的结构体和 uniform

void main(void) 

{

    vec3 L = normalize(varyingLightDtr);

    vec3 N = normalize(varyingNormal);

    vec3 V = normalize(varyingVertPos);

    vec3 H = normalize(varyingHalfVec);

    float shadow = textureProj(shadowMap, shadow_coord);

    fragColor = globalAmbient * material.ambient + light.ambient * material.ambient;

    if(shadow == 1.0) {

        fragColor += light.diffuse * material.diffuse * max(dot(LN,N),0.0) +

        + light.specular * material.specular

        pow(max(dot(H,N),0.0),material.shininess,3.0);

    }

}
```

图 8.7

阴影映射着色器 2 片段着色器。

片段着色器如下。z 分量表示从光源到像素的距离。(xy) 分量用于从 (2D) 阴影纹理中检索存储的深度信息。检索到的值（距离光源最近对象的距离）将与 z 进行比较。这种比较产生一个“二进制”结果，告诉我们正在渲染的像素是否比距离光源最近的点远（即该像素是否处于阴影中）。

在 OpenGL 中，我们像之前描述的那样使用 `glFramebuffer()`，并启用深度测试，如片段着色器（图 8.7）所示，使用 `sampler2D` `shadow` 和 `textureProj()` 将恰好完成我们需要的功能。它将根据深度比较输出 0.0 或 1。根据此值，我们随后可以在片段着色器中，当像素比距离光源最近的物体远时，省略漫反射和高光部分的贡献，从而在适当的情况下创建阴影。图 8.8 显示了概览。

我们现在准备好构建我们的 C++/OpenGL 应用，以与之前描述的着色器配合工作。

texCoord:

![](img/5f029c1d57776416a7d2524f3734d7cf_198_0.png)

图 8.8
自动深度比较。

## 8.5 阴影映射示例

考虑图 8.9 所示场景，它包含一个圆环和一个金字塔。一个位置光源被放置在左侧（注意高光点亮）。金字塔应该在圆环上投下阴影。

![](img/5f029c1d57776416a7d2524f3734d7cf_198_1.png)

图 8.9
没有阴影的光照场景。

为了明确示例的开发，我们的第一步将将其渲染到屏幕上以确保它正常工作。为了做到这一点，我们将临时添加一个简单的片段着色器（它不会包含在最终版本中），以通过一个输出常数颜色（例如红色）的着色器；例如：

```cpp
#version 430

out vec4 fragColor;

void main(void) {

    fragColor = vec4(1.0, 0.0, 0.0, 0.0);

}
```

![](img/5f029c1d57776416a7d2524f3734d7cf_199_0.png)

**图 8.10**
第一阶段：从光源视角（右侧）的场景（左侧）。

带有光照和阴影映射的两阶段式 C++/OpenGL 代码如程序 8.1 所示。

### 程序 8.1 阴影映射

```cpp
// 与我们之前看到的大部分相同。支持阴影的新部分已高亮。

// 光照等所需的导入将包含在开头，与之前相同，

// 在此处未显示。

// // 渲染程序、缓冲区、着色器源等的变量声明将放在这里。

ImportModel pyramid("pyr.obj");

Torus myTorusLoc(0.6f, 0.4f, 48);

int numPyramidVertices, numTorusVertices, numTorusIndices;

// 圆环、相机和光照的位置

glm::vec3 torusLoc(1.6f, 0.1f, -0.3f);

glm::vec3 pyrLoc(-1.0f, 0.1f, 0.3f);

glm::vec3 cameraLoc(0.2f, 0.2f, 0.6f);

glm::vec3 lightLoc(-3.8f, 2.2f, 1.1f);

// 白色光的属性（全局和位置）

float globalAmbient[4] = {0.7f, 0.7f, 0.7f, 1.0f};

float lightAmbient[4] = {0.2f, 0.2f, 0.2f, 1.0f};

float materialAmbient[4] = {0.2f, 0.2f, 0.2f, 1.0f};

float materialDiffuse[4] = {0.3f, 0.3f, 0.3f, 1.0f};

float materialSpecular[4] = {0.5f, 0.5f, 0.5f, 1.0f};

float materialShininess = 32.0f;

// ... (其余代码省略)
```

# 使用 C++ 在 OpenGL 中进行图形图形

```cpp
void passTwo() {

    glUseProgram(renderingProgram2);

    // 传递顶点和片元着色器

    // 绘制环面 - 这我们需要包含光照、材质、法线等

    // 我们还需要为相机空间和光照空间提供 MVP 变换

    mvLoc = glGetUniformLocation(renderingProgram2, "mv_matrix");

    projLoc = glGetUniformLocation(renderingProgram2, "proj_matrix");

    modelLoc = glGetUniformLocation(renderingProgram2, "model_matrix");

    slLoc = glGetUniformLocation(renderingProgram2, "shadowMVP");

    // 绘制环面

    curArr[0] = bronzeMatAlb[0]; curArr[1] = bronzeMatAlb[1]; curArr[2] = bronzeMatAlb[2];

    curDiff[0] = bronzeMatDiff[0]; curDiff[1] = bronzeMatDiff[1];

    curSpe[0] = bronzeMatSpec[0]; curSpe[1] = bronzeMatSpec[1]; curSpe[2] = bronzeMatSpec[2];

    vMat = glm::translate(glm::mat4(1.0), glm::vec3(-cameraLoc.x,-cameraLoc.y, -cameraLoc.z));

    currentLightPos = glGetUniformLocation(renderingProgram2, "light");

    installLights(renderingProgram2, vMat);

    modelMat = glm::translate(glm::mat4(1.0), torusLoc);

    // 为了便于观察进行微旋转

    modelMat = glm::rotate(modelMat, glm::toRadians(25.0), glm::vec3(1.0, 0.0, 0.0));

    // 从相机视角为环面构建 MVP

    mvMat = modelMat;

    invTrMat = glm::transpose(glm::inverse(mvMat));

    // 从光照视角为环面构建 MVP

    shadowMVP2 = b * lightMatrix * matrix * mvMat;

    // 将 MV 和 PROJ 矩阵放入相应的 uniforms 中

    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvMat));

    glUniformMatrix4fv(projLoc, 1, GL_FALSE, glm::value_ptr(projMat));

    glUniformMatrix4fv(modelLoc, 1, GL_FALSE, glm::value_ptr(invTrMat));

    glUniformMatrix4fv(slLoc, 1, GL_FALSE, glm::value_ptr(shadowMVP2));

    // * 

    // * 环面法线

    // 设置顶点和法线缓冲区（如果使用了纹理坐标缓冲区）

    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);

    glVertexAttributePointer(0, 3, GL_FLOAT, FALSE, 0, 0);

    EnableVertexAttribArray(0);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[1]);

    glVertexAttributePointer(1, 3, GL_FLOAT, FALSE, 0, 0);

    EnableVertexAttribArray(1);

    glClear(GL_DEPTH_BUFFER);

    glEnable(GL_CULL_FACE);

    glFrontFace(GL_CCW);

    glEnable(GL_DEPTH_TEST);

    glDepthFunc(GL_LEQUAL);

    glBindBuffer(GL_ELEMENTARY_ARRAY_BUFFER, vbo[4]); // vbo[4] 包含环面索引

    DrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);

    // 对金色金字塔重复操作

}
```
