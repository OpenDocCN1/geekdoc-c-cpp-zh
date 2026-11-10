
基于时间。例如，程序 4.1 中 `display()` 函数里的代码可以按如下方式修改（改动部分已高亮）：

```cpp
glClear(GL_DEPTH_BUFFER_BIT);
glClear(GL_COLOR_BUFFER_BIT);
...
// use current time to compute different translations in x, y, and z
mat4 m = glm::translate(glm::mat4(1.0f),
    glm::vec3(0.5f*currentTime*2.0f, 0.5f*currentTime*2.0f, 0.0f));
m = glm::rotate(m, 1.75f*float(currentTime), glm::vec3(0.0f, 0.0f, 1.0f));
m = glm::rotate(m, 1.75f*float(currentTime), glm::vec3(0.0f, 1.0f, 0.0f));
// the 1.75 adjusts the rotation speed
mMat = tMat * rMat;
```

在模型矩阵中使用当前时间（以及各种三角函数）会使立方体看起来在空间中翻滚。请注意，添加此动画说明了每次通过 `display()` 时清除深度缓冲区以确保正确隐藏面消除的重要性。这还要求如所示清除颜色缓冲区；否则，立方体移动时会留下拖影。

`translate()` 和 `rotate()` 函数是 GLM 库的一部分。另外，请注意最后一行的矩阵乘法——`tMat` 和 `rMat` 在运算中的列出顺序很重要。它计算两个变换的拼接，其中平移在左侧，旋转在右侧。当随后将一个顶点乘以该矩阵时，计算是从右到左进行的，这意味着先进行旋转，然后进行平移。变换的应用顺序很重要，改变顺序会导致不同的行为。图 4.7 显示了动画立方体之后显示的一些帧。

![](img/1695de1bc7486362f86c143285f3fb40_97_0.png)

**图 4.7**
动画（“翻滚”）的 3D 立方体。

## 4.6 渲染对象的多个副本

现在我们将所学内容扩展到渲染多个对象。在着手处理在单个场景中渲染各种模型的通用情况之前，让我们先考虑*同一模型的多个实例*这一更简单的情况。例如，假设我们希望扩展上一个示例，使其渲染由 24 个翻滚立方体组成的“一群”立方体。为此，我们可以将 `display()` 中构建 MV 矩阵和绘制立方体的代码部分（如下方蓝色所示）移入一个执行 24 次的循环中。我们将循环变量纳入立方体的旋转和平移中，以便每次绘制立方体时都构建不同的模型矩阵。（我们还将相机沿正 Z 轴进一步后移，以便看到所有立方体。）由所得动画场景生成的一帧如图 4.8 所示。

```cpp
void display(GLFWwindow* window, double currentTime) {
    ...
    for(int i=0;i<24;i++)
    {   tf = currentTime + i;    // tf == "time factor", declared as type float
        tfMat = glm::translate(glm::mat4(1.0f), glm::vec3(sin(35.0f * tf) * 8.0f, cos(52.0f * tf) * 8.0f,
                                                         sin(70.0f * tf) * 8.0f));
        rMat = glm::rotate(glm::mat4(1.0f), 1.75f*tf, glm::vec3(0.0f, 1.0f, 0.0f));
        rMat = glm::rotate(rMat, 1.75f*tf, glm::vec3(1.0f, 0.0f, 0.0f));
        rMat = glm::rotate(rMat, 1.75f*tf, glm::vec3(0.0f, 0.0f, 1.0f));
        mMat = tfMat * rMat;
        mvMat = vMat * mMat;

        glUniformMatrix4fv(mvLoc, 1, GL_FALSE, glm::value_ptr(mvMat));
        glUniformMatrix4fv(projLoc, 1, GL_FALSE, glm::value_ptr(pMat));

        glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
        glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0);
        glEnableVertexAttribArray(0);

        glEnable(GL_DEPTH_TEST);
        glDepthFunc(GL_LEQUAL);
        glDrawArrays(GL_TRIANGLES, 0, 36);
    }
}
```

![](img/1695de1bc7486362f86c143285f3fb40_99_0.png)

### 4.6.1 实例化

*实例化*提供了一种机制，可以告诉图形卡仅使用一次 C++/OpenGL 调用就渲染对象的多个副本。这可以带来显著的性能优势，特别是当正在绘制的对象有数千或数百万个副本时——例如渲染田野中的许多花，或军队中的许多僵尸。

我们首先将 C++/OpenGL 应用程序中的 `glDrawArrays()` 调用改为 `glDrawArraysInstanced()`。现在，我们可以要求 OpenGL 绘制任意数量的副本。我们可以如下指定绘制 24 个立方体：

```cpp
glDrawArraysInstanced(GL_TRIANGLES, 0, 36, 24);
```

使用实例化时，顶点着色器可以访问内置变量 `gl_InstanceID`，这是一个整数，表示当前正在处理的是对象的哪个数字实例。

为了使用实例化复现之前翻滚立方体的示例，我们需要将构建不同模型矩阵的计算（之前在 `display()` 中的循环内）移入顶点着色器。由于 GLSL 不提供 `translate` 或 `rotate` 函数，并且我们无法在着色器内部调用 GLM，因此需要使用程序 3.1 中的工具函数。我们还需要通过 uniform 将“时间因子”从 C++/OpenGL 应用程序传递给顶点着色器。由于旋转计算已移至顶点着色器，我们还需要在单独的 uniform 变量中传递视图矩阵。这些修订包括 C++/OpenGL 应用程序中的修订和新顶点着色器中的修订，如程序 4.2 所示。

### 程序 4.2 实例化——二十四个动画立方体

顶点着色器：

```glsl
#version 430
layout (location=0) in vec3 position;
uniform mat4 v_matrix;
uniform mat4 proj_matrix;
uniform float tf;            // time factor for animation and placement of cubes

out vec4 varyingColor;

mat4 buildRotateX(float rad);    // declaration of matrix transformation utility functions
mat4 buildRotateY(float rad);    // (GLSL requires functions to be declared prior to invocation)
mat4 buildRotateZ(float rad);
mat4 buildTranslate(float x, float y, float z);

void main(void)
{  float i = gl_InstanceID + tf;      // value based on time factor, but different for each cube instance
   float a = sin(2.0 * i) * 8.0;      // these are the x, y, and z components for the translation, below
   float b = sin(3.0 * i) * 8.0;
   float c = sin(4.0 * i) * 8.0;

   // build the rotation and translation matrices to be applied to this cube's model matrix
   mat4 localRotX = buildRotateX(1000*i);
   mat4 localRotY = buildRotateY(1000*i);
   mat4 localRotZ = buildRotateZ(1000*i);
   mat4 localTrans = buildTranslate(a,b,c);

   // build the model matrix and then the model-view matrix
   mat4 newM_matrix = localTrans * localRotX * localRotY * localRotZ;
   mat4 mv_matrix = v_matrix * newM_matrix;

   gl_Position = proj_matrix * mv_matrix * vec4(position,1.0);
   varyingColor = vec4(position,1.0) * 0.5 + vec4(0.5, 0.5, 0.5, 0.5);
}
```

```cpp
// utility function to build a translation matrix (from Chapter 3)
mat4 buildTranslate(float x, float y, float z)
{  mat4 trans = mat4(1.0, 0.0, 0.0, 0.0,
                    0.0, 1.0, 0.0, 0.0,
                    0.0, 0.0, 1.0, 0.0,
                    x, y, z, 1.0);
   return trans;
}
// similar functions included for rotation around the X, Y and Z axes (also from Chapter 3)
. . .
```

C++/OpenGL 应用程序（在 `display()` 中）

```cpp
. . .
// computations that build (and transform) mMat have been moved to the vertex shader.
// there is no longer any need to build an MV matrix in the C++ application.
glUniformMatrix4fv(vLoc, 1, GL_FALSE, glm::value_ptr(vMat));        // shader needs the V matrix
timeFactor = ((float)currentTime);                                  // uniform for the time factor
tfLoc = glGetUniformLocation(renderingProgram, "tf");               // (the shader needs that too)
glUniform1f(tfLoc, float(timeFactor));
. . .
glDrawArraysInstanced(GL_TRIANGLES, 0, 36, 24);
```

程序 4.2 的最终输出与上一个示例的输出相同，并可在前面的图 4.8 中看到。

实例化使得大幅扩展对象的副本数量成为可能；在此示例中，即使对于普通的 GPU，对 *100,000* 个立方体进行动画仍然可行。代码的改动——主要只是修改几个常量，让大量立方体分布得更开——如下所示：

顶点着色器：

```glsl
. . .
float a = sin(203.0 * i / 8000.0) * 403.0;
float b = cos(301.0 * i / 4001.0) * 401.0;
float c = sin(400.0 * i / 6003.0) * 405.0;
. . .
```

C++/OpenGL 应用程序

```cpp
. . .
cameraZ = 420.0f;   // move camera further down the Z axis to view the increased number of cubes
. . .
glDrawArraysInstanced(GL_TRIANGLES, 0, 36, 100000);
```

