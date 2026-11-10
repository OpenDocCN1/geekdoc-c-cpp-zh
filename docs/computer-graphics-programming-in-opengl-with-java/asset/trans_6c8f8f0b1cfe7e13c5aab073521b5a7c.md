
### 修订后的顶点着色器：

```glsl
#version 430

layout (location=0) in vec3 position;
uniform mat4 mv_matrix;
uniform mat4 p_matrix;

out vec4 varyingColor;

void main(void)
{
    gl_Position = p_matrix * mv_matrix * vec4(position,1.0);
    varyingColor = vec4(position,1.0) * 0.5 + vec4(0.5, 0.5, 0.5, 0.5);
}
```

### 修订后的片元着色器：

```glsl
#version 430

in vec4 varyingColor;

out vec4 color;
uniform mat4 mv_matrix;
uniform mat4 p_matrix;

void main(void)
{
    color = varyingColor;
}
```

请注意，由于颜色是通过顶点属性（varyingColor）从顶点着色器输出的，*它们也会被光栅化器插值*！其效果可以在图4.6中看到，其中从一角到另一角的颜色在整个立方体上明显被平滑地插值。

还要注意，顶点着色器中的“out”变量 varyingColor 也是片元着色器中的“in”变量。两个着色器知道顶点着色器中的哪个变量供给片元着色器中的哪个变量，因为它们在两个着色器中具有相同的名称——“varyingColor”。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_98_0.png)

**图4.6**
带插值颜色的立方体。

我们可以像程序2.6中那样使用Animator类来为立方体制作动画，方法是基于经过的时间，使用变化的平移和旋转来构建模型矩阵。例如，程序4.1中display()函数里的代码可以按如下方式修改（更改部分已突出显示）：

```
gl.glClear(GL_DEPTH_BUFFER_BIT);
gl.glClear(GL_COLOR_BUFFER_BIT);

// use system time to generate slowly-increasing sequence of floating-point values
elapsedTime = System.currentTimeMillis() - startTime;  // elapsedTime, startTime, and tf
tf = elapsedTime / 1000.0;  // would all be declared of type double.
...
// use tf (time factor) to compute different translations in x, y, and z
mMat.identity();
mMat.translate((float)Math.sin(.35f*tf)*2.0f, (float)Math.sin(.52f*tf)*2.0f, (float)Math.sin(.7f*tf)*2.0f);
mMat.rotateXYZ(1.75f*(float)tf, 1.75f*(float)tf, 1.75f*(float)tf);  // the 1.75 adjusts the rotation speed
```

在模型矩阵中使用经过的时间（以及各种三角函数）会使立方体看起来在空间中翻滚。请注意，添加此动画说明了每次通过display()时清除深度缓冲区以确保正确隐藏面消除的重要性。这也需要像所示那样清除颜色缓冲区；否则，立方体在移动时会留下拖尾。

translate()和rotateXYZ()函数是JOML库的一部分。请注意，在代码中，translate()在rotate()之前调用。这导致两个变换的连接，其中平移在左侧，旋转在右侧。当顶点随后乘以该矩阵时，计算是从右到左的，这意味着先进行旋转，然后进行平移。变换的应用顺序很重要，改变顺序会导致不同的行为。图4.7显示了为立方体制作动画后显示的一些帧。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_99_0.png)

**图4.7**
动画（“翻滚”）3D立方体。

## 4.6 渲染对象的多个副本

在我们处理在单个场景中渲染各种模型的一般情况之前，先考虑同一模型的*多次出现*这一更简单的情况。例如，假设我们希望扩展前面的示例，使其渲染由24个翻滚立方体组成的“蜂群”。我们可以通过将`display()`中构建MV矩阵和绘制立方体的代码部分（如下所示）移入一个执行24次的循环来实现。我们将循环变量纳入立方体的旋转和平移中，以便每次绘制立方体时构建不同的模型矩阵。（我们还将相机沿正Z轴进一步下移，以便看到所有立方体，并将乘数从2.0增加到8.0以将它们分散开。）得到的动画场景如图4.8所示。

```java
public void display(GLAutoDrawable drawable)
{
   ...
   timeFactor = elapsedTime/1000.0;

   for (i=0; i<24; i++)
   {
      x = timeFactor * i;
      mMat.identity();
      mMat.translate((float)Math.sin(.35f*i)*8.0f, (float)Math.sin(.52f*i)*8.0f, (float)Math.sin(.70f*i)*8.0f);
      mMat.rotateXYZ(1.75f*(float)i, 1.75f*(float)i, 1.75f*(float)i);

      mvMat.identity();
      mvMat.mul(vMat);
      mvMat.mul(mMat);

      gl.glUniformMatrix4fv(mvLoc, 1, false, mvMat.get(vals));
      gl.glUniformMatrix4fv(pLoc, 1, false, pMat.get(vals));

      gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[0]);
      gl.glVertexAttribPointer(0, 3, GL_FLOAT, false, 0, 0);
      gl.glEnableVertexAttribArray(0);

      gl.glEnable(GL_DEPTH_TEST);
      gl.glDepthFunc(GL_LEQUAL);
      gl.glDrawArrays(GL_TRIANGLES, 0, 36);
   }
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_101_0.png)

**图4.8**
多个翻滚的立方体。

### 4.6.1 实例化

实例化提供了一种机制，可以只使用一次Java调用就告诉图形卡渲染对象的多个副本。这可以带来显著的性能优势，特别是当正在绘制的对象有数千或数百万个副本时——例如渲染田野中的许多花朵，或军队中的许多僵尸。

我们首先将Java/JOGL应用程序中的glDrawArrays()调用更改为glDrawArraysInstanced()。现在我们可以要求OpenGL绘制任意数量的副本。我们可以如下指定绘制24个立方体：

```
glDrawArraysInstanced(GL_TRIANGLES, 0, 36, 24);
```

使用实例化时，顶点着色器可以访问一个内置变量gl_InstanceID，这是一个整数，表示当前正在处理的是对象的哪个数字实例。

要使用实例化复现我们之前的翻滚立方体示例，我们需要将构建不同模型矩阵的计算（之前位于display()中的循环内）移到顶点着色器中。由于GLSL不提供translate或rotate函数，并且我们不能在着色器内部调用JOML，我们将需要使用程序3.1中的实用函数。我们还需要通过uniform将“时间因子”变量从Java/JOGL应用程序传递到顶点着色器。我们还需要在单独的uniform变量中传递视图矩阵，因为旋转计算已移到顶点着色器。这些修订，包括Java/JOGL应用程序中的修订和新顶点着色器中的修订，如程序4.2所示。

### 程序4.2 实例化：24个动画立方体

*顶点着色器：*

```glsl
#version 430
layout (location=0) in vec3 position;

uniform mat4 v_matrix;             // only the P and V matrices are sent from the application
uniform mat4 p_matrix;
uniform float tf;                  // time factor for animation and placement of cubes

out vec4 varyingColor;

mat4 buildRotateX(float rad);      // declaration of matrix transformation utility functions
mat4 buildRotateY(float rad);      // (GLSL requires functions to be declared prior to invocation)
mat4 buildRotateZ(float rad);
mat4 buildTranslate(float x, float y, float z);

void main(void)
{
    float x = gl_InstanceID + tf;  // value based on time factor, but different for each cube instance

    float a = sin(.35 * x) * 8.0;  // these are the x, y, and z components for the translation, below
    float b = sin(.52 * x) * 8.0;
    float c = sin(.70 * x) * 8.0;

    // build the rotation and translation matrices to be applied to this cube’s model matrix
    mat4 localRotX = buildRotateX(1.75*x);
    mat4 localRotY = buildRotateY(1.75*x);
    mat4 localRotZ = buildRotateZ(1.75*x);
    mat4 localTrans = buildTranslate(a,b,c);

    // build the model matrix and then the model-view matrix
    mat4 newM_matrix = localTrans * localRotX * localRotY * localRotZ;
    mat4 mv_matrix = v_matrix * newM_matrix;

    gl_Position = p_matrix * mv_matrix * vec4(position, 1.0);
    varyingColor = vec4(position,1.0) * 0.5 + vec4(0.5, 0.5, 0.5, 0.5);
}

// utility function to build a translation matrix (from Chapter 3)
mat4 buildTranslate(float x, float y, float z)
{  mat4 trans = mat4( 1.0, 0.0, 0.0, 0.0,
```

