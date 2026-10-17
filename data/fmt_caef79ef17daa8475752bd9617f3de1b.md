
程序 9.1 的输出如图 9.7 所示，用于不同的立方体映射纹理。

如前所述，天空盒在纹理图像汇合处容易出现畸变和缝隙。图 9.8 显示了立方体上部分的缝隙示例。避免缝隙需要仔细构建立方体映射图像并分配精确的纹理坐标。存在一些工具可以减少图像边缘的缝隙；此主题超出本书范围。

## 9.3.2 使用 OpenGL立方体映射

构建天空盒的另一种方法是使用 OpenGL 立方体映射。OpenGL 立方体映射比我们之前看到的简单方法复杂一些，但使用立方体映射也有优点，例如减少缝隙以及对环境映射的支持。

OpenGL 纹理映射与 3D 纹理类似，稍后将使用纹理坐标（通常标记为 `s`, `t`, `r`）进行访问——而不是我们一直所做的。OpenGL 立方体映射的另一个特征是它们中的图像朝向为 `(0,0,0)`，而不是普通的左侧；这通常是困惑的来源。

程序 9.1 使用的方法读取单个图像，程序 9.2 显示的 `loadCubeMap` 函数读取六个独立的文件。如第 5 章所示，加载纹理有许多方法；我们选择使用 `SOIL` 库。在这里，`SOIL` 对于实例化和加载 OpenGL 立方体映射非常方便。在 OpenGL 中，不需要翻转顶点，因为 OpenGL 会自动翻转它们。我们在 `"Utils.cpp"` 文件中的 `loadCubeMap()` 函数现在包含了启用立方体相邻边缘的调用。在 `Display()` 中，顶点发送到流水线，但在禁用深度测试后绘制立方体。然后对剩余场景重新启用深度测试。

完成的 OpenGL 立方体映射通过整数标识符引用。对于阴影映射的情况，可以通过将纹理包装模式设置为“边缘限制”（clamp to edge）来减少边界缝隙。这种情况下有助于减少缝隙。注意这适用于所有纹理坐标：`s`、`t` 和 `f`。在片元着色器中使用特殊类型的采样器从原点沿方向向量 `(s,t,r)` 获取值。作为结果，我们可以简单地使用顶点位置。在顶点着色器中，我们将立方体顶点位置分配给输出纹理，以便它们被插值为 3x3，然后回到 4x4。这个“技巧”有效地移除了变换矩阵第四列中的平移分量。这将立方体映射固定在相机位置。

## 天空与背景

### 程序 9.2 OpenGL 立方体映射天空盒

```cpp
private int brickTexture, skyboxTexture;

private int renderingProgram, renderingCubeMap;

void init(GLFWwindow* window) {

    renderingProgram = Utils::createShader("vertShader.glsl","fragShader.glsl");

    renderingCubeMap = Utils::createShaderProgram("vertShader.glsl","fragShader.glsl");

    setupVertices();

    brickTexture = Utils::loadTexture("brick.jpg"); // 用于场景中的圆环

    skyboxTexture = Utils::loadCubeMap("cubemap"); // 天空盒纹理的文件夹

    glBind(GL_TEXTURE_MAP, SEAMLESS);

}

void display(GLFWwindow* window, double currentTime) {

    // 像之前一样清除颜色和深度缓冲区、投影和相机视图矩阵。

// 先绘制立方体映射 - 注意它需要不同的渲染程序

glUseProgram(renderingCubeMap);

// 设置立方体的顶点（不需要纹理坐标缓冲区）

glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);

glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);

glVertexVertexAttribArray(0);

// 将立方体映射设为激活纹理

glActiveTexture(GL_TEXTURE_0);

glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);

// 禁用深度测试，然后绘制立方体映射

glEnable(GL_CULL_FACE);

glFrontFace(CCW);

glDisable(GL_DEPTH_TEST);

glDrawArrays(GL_TRIANGLES, 0, 36);

glEnable(GL_DEPTH_TEST);

// 将 P 和 V 矩阵放入相应的 uniform 中。

// 绘制剩余场景

}

GLuint Utils:loadCubeMap(const char *mapDir) {

    GLuint textureRef;

// 假设六个纹理文件命名为 xp, xn, yp, yn, zn 且为 JPG

    string xp = mapDir; xp = xp + "xp.jpg";

    string xn = mapDir; xn = xn + "xn.jpg";

    string yp = mapDir; yp = yp + "py.jpg";

    string yn = mapDir; yn = yn + "yn.jpg";

    string zn = mapDir; zn = zn + "zn.jpg";

    textureRef = SOIL_OGL_cubemap(xp_str, xn_str, yp_str, yn_str, zn_str, zp_str, SOIL_LOAD_AUTO, SOIL_CREATE_NEW_ID, SOIL_FLAG_MIPMAPS);

    if(textureRef == 0) cout << "未找到立方体映射文件" << endl;

    glBindTexture(GL_TEXTURE_CUBE_MAP, textureRef);

    // 减少缝隙

    glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_EDGE);

    glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_T, GL_CLAMP_TO_EDGE);

    glTexParameteri(GL_TEXTURE_CUBE_MAP, GL_TEXTURE_WRAP_R, GL_CLAMP_TO_EDGE);

    return textureRef;

}
```

# 第 9 章 · 天空与背景 ■ 231

```glsl
片元器

#version 430

in vec3 tc;

out vec4 fragColor;

uniform mat4 v_matrix;

uniform uniform mat4 proj_matrix;

layout (binding = 0) uniform samplerCube samp;

void main(void) {

  fragColor = texture(samp, tc);

}
```

## 9.4 环境映射 (ENVIRONMENT MAPPING)

当我们考虑光照和材质时，考虑的是对象的“光泽度”。然而，我们从未模拟过非常光亮的物体，例如镜子或由铬制成的物体。这类物体不仅具有高光反射；它们实际上还反射了周围的环境。当我们观察它们时，可以看到房间里的东西，有时甚至看到我们自己的倒影。ADS 光照模型并没有提供模拟这种效果的方法。

然而，纹理映射（Texture maps）提供了一种相对简单的模拟反射表面的方法——至少是部分。技巧在于使用立方体贴图（cube map）对反射物体本身进行纹理化！为了使其看起来真实，需要获取纹理坐标，这些坐标对应于从我们的观察点来看，物体中应该看到的环境各个部分。

图 9.9 展示了结合视向量（view vector）和法向量（normal vector）来计算反射向量的策略，然后使用该反射向量从立方体贴图中查找纹素（texel）。反射向量可以直接访问纹理立方贴图。当立方体贴图执行此功能时，它被称为环境映射（environment map）。

我们在学习 Blinn-Phong 光照时曾计算过向量。这里的概念很简单，不同在于现在我们使用反射向量从纹理映射中查找值。这种技术被称为*环境映射*。如果立方体贴图是用上描述的第二方法（在第 9.3.2 节；即作为 OpenGL 的 `GL_TEXTURE_CUBE`）实现的，那么 OpenGL 就可以像处理纹理化本身的方式一样执行环境映射查找。

> ¹ 这种技巧在使用穹顶（skydome）代替天空盒（skybox）的情况下也是可行的，通过用穹顶纹理图像对反射物体进行纹理化来实现。

![](img/5f029c1d57776416a7d2524f3734d7cf_231_0.png)

**图 9.3**
环境映射概述。

我们使用视向量和表面法线来计算视向量在物体表面的反射。然后可以使用反射向量来采样纹理立方贴图图像。查找过程由 OpenGL `samplerCube` 辅助；回想上一节，`samplerCube` 是通过视方向向量索引的。因此，反射向量非常适合查找所需的纹素。

实现过程只需要少量的额外代码。程序 9.3 显示了在（显示）和 `init()` 函数以及相关的着色器中为了环境映射渲染“反射性”圆环时所做的更改。这些更改已高亮显示。值得注意的是，如果存在 Blinn-Phong 光照，事实上，它最初可能看起来就像程序 9.3 中高亮的代码（即黄色部分）根本不是新东西。事实上，我们之前见过几乎完全相同的代码。然而，在这种情况下，法向量和反射向量用于完全不同的用途。之前它们被用于实现 ADS 光照模型，而在这里它们被用于计算环境映射的纹理坐标。我们高亮了这些行代码，以便读者轻松跟踪为此目的而对法线和反射计算的使用。

结果显示了一个环境映射的“铬制”圆环，如图 9.10 所示。

![](img/5f029c1d57776416a7d2524f3734d7cf_232_0.png)

**图 9.10**
使用环境映射创建反射圆环的示例。

## 程序 9.3 环境映射

```cpp
public void display(GLFWwindow window, double currentTime) {

    // 绘制立方体贴图的代码保持不变。

    //

    // 更改都在绘制圆环的部分：

    glUseProgram(renderingProgram);

    // 矩阵变换的统一变量位置，包括用于法线的变换

    mvLoc = glGetUniformLocation(renderingProgram, "mv_matrix");

    projLoc = glGetUniformLocation(renderingProgram, "proj_matrix");

    normLoc = glGetUniformLocation(renderingProgram, "norm_matrix");

    // 像之前一样构建模型-视图矩阵 

    mat = glm::translate(mat4(1.0), glm::vec3(torLocX, torLocY, torLocZ));

    // 像之前一样构建模型-视图矩阵

    mvMat = vMat * mat;

    invMat = glm::inverse(mvMat);

    // 法线变换现在包含在统一变量中：

    glUniformMatrix4fv(mvLoc, 1, GL_FALSE, mvMat);

    glUniformMatrix4fv(projLoc, 1, GL_FALSE, projMat);

    glUniformMatrix4fv(normLoc, 1, GL_FALSE, invMat);

    // 像之前一样激活顶点缓冲区

    glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);

    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0);

    glVertexAttribArray(0);

    // 我们需要激活纹理法线：

    glBindBuffer(GL_ARRAY_BUFFER, vbo[2]);

    glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 0);

    glVertexAttribArray(1);

    // 激活纹理法线

    glActiveTexture(GL_TEXTURE0);

    glBindTexture(GL_TEXTURE_CUBE_MAP, skyboxTexture);

    // 绘制立方体贴图的代码保持不变

    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

    glEnable(GL_CULL_FACE);

    glFrontFace(GL_CCW);

    glDepthFunc(GL_EQUAL);

    glBindBuffer(GL_ARRAY_BUFFER, vbo[3]);

    glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);

}
```

顶点着色器

```glsl
#version 430

layout (location = 0) in vec3 position;

layout (location = 1) in vec3 normal;

out vec3 tc;

uniform mat4 mv_matrix;

uniform mat4 proj_matrix;

uniform mat4 norm_matrix;

void main() {

  gl_Position = proj_matrix * mv_matrix * vec4(position, 1.0);

  tc = vec3(norm_matrix * vec4(normal, 0.0));

}
```

片元着色器

```glsl
#version 430

in vec3 tc;

out vec4 fragColor;

uniform samplerCube samp;

void main() {

    vec3 r = reflect(-normalize(tc), normalize(tc));

    fragColor = texture(samp, r);

}
```
