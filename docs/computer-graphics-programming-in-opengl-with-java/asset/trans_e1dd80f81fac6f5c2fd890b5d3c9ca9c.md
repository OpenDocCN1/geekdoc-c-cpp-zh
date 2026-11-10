
例如，如果源像素为红色，不透明度为 75%（[1, 0, 0, 0.75]），而目标像素包含完全不透明的绿色（[0, 1, 0, 1]），那么放入帧缓冲的结果将是

```
srcPixel * srcAlpha = [0.75, 0, 0, 0.5625]
destPixel * (1-srcAlpha) = [0, 0.25, 0, 0.25]
resulting pixel = [0.75, 0.25, 0, 0.8125]
```

也就是说，主要是红色，带有一些绿色，并且大部分为实色。这些设置的整体效果是让目标像素按照源像素透明度所对应的程度透出。在此示例中，帧缓冲中的像素是绿色，而传入的像素是红色，透明度为 25%（不透明度为 75%）。因此，一些绿色得以透过红色显示出来。

事实证明，这些混合函数和混合方程设置在多种情况下都能很好地工作。让我们把它们应用到一个实际示例中：场景包含两个 3D 模型，一个圆环体以及位于圆环体前方的一个棱锥。图 14.4 展示了这样的场景，左侧是不透明的棱锥，右侧是将棱锥的 alpha 值设为 0.8 的效果。场景中添加了光照。

对于许多应用——例如在房屋模型中创建一扇平面的“窗户”——这种简单的透明实现可能已经足够。然而，在图 14.4 所示的示例中，存在一个相当明显的不足。尽管棱锥模型现在实际上已透明，但真正透明的棱锥不仅应显示出其后面的物体，还应显示出自身的背面。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_339_0.png)

**图 14.4**
alpha=1.0（左）和 alpha=0.8（右）的棱锥。

实际上，棱锥的背面没有出现，是因为我们启用了背面剔除。一个合理的想法可能是在绘制棱锥时禁用背面剔除。然而，这通常会产生其他伪影，如图 14.5（左侧）所示。简单禁用背面剔除的问题在于，混合效果取决于表面渲染的顺序（因为这决定了源像素和目标像素），而我们并不总能控制渲染顺序。通常有利的做法是，先渲染不透明对象以及位于后面的对象（例如圆环体），然后再渲染任何透明对象。这对棱锥的表面同样成立；在此情况下，构成棱锥底面的两个三角形看起来不同的原因是，其中一个在棱锥正面之前渲染，另一个在之后渲染。此类伪影有时称为“顺序”伪影，并且会在透明模型中显现，因为我们无法总是预测其三角形的渲染顺序。

我们可以通过自行分别渲染正面和背面，并从背面开始，来解决棱锥示例中的问题。程序 14.2 展示了实现这一点的代码。我们通过 uniform 变量将棱锥的 alpha 值传递给着色器程序，然后在片元着色器中将其应用：把指定的 alpha 代入计算出的输出颜色中。

另请注意，为使光照正常工作，在渲染背面时必须翻转法线向量。我们通过向顶点着色器发送一个标志来实现这一点，然后在顶点着色器中翻转法线向量。

### 程序 14.2 用于透明效果的两遍混合

*JOGL/Java 应用程序——在 display() 中渲染棱锥：*

```java
...
gl.glEnable(GL_CULL_FACE);
...
gl.glEnable(GL_BLEND);             // configure blend settings
gl.glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
gl.glBlendEquation(GL_FUNC_ADD);

gl.glCullFace(GL_FRONT);
gl.glProgramUniform1f(renderingProgram, alphaLoc, 0.3f); // back faces very transparent
gl.glProgramUniform1f(renderingProgram, flipLoc, -1.0f); // flip normals on back faces
gl.glDrawArrays(GL_TRIANGLES, 0, numPyramidVertices);
```

## 14.3 用户定义的裁剪平面

OpenGL 具备指定超出视图视锥所定义范围的裁剪平面的能力。用户定义裁剪平面的一个用途是剖切模型。这样，可以从一个简单模型开始，并从中切掉若干部分，从而创建复杂形状。

裁剪平面根据平面的标准数学定义来定义：

ax + by + cz + d = 0

其中 a、b、c 和 d 是参数，用于定义 3D 空间中相对于 X、Y、Z 轴的一个特定平面。这些参数表示一个垂直于该平面的向量 (a, b, c)，以及从原点到该平面的距离 d。这样的平面可以在顶点着色器中使用 vec4 来指定，如下所示：

```
vec4 clip_plane = vec4(0.0, 0.0, -1.0, 0.2);
```

这对应于平面

(0.0) x + (0.0) y + (-1.0) z + 0.2 = 0

然后，同样可以在顶点着色器中，通过使用内置 GLSL 变量 gl_ClipDistance[] 来实现裁剪，如下例所示：

```
gl_ClipDistance[0] = dot(clip_plane.xyz, vertPos) + clip_plane.w;
```

在此示例中，vertPos 指通过顶点属性（例如来自 VBO）传入顶点着色器的顶点位置；clip_plane 已在上面定义。然后，我们计算从裁剪平面到传入顶点的有符号距离（第 3 章中已展示）；如果顶点位于平面上，则该距离为 0，否则根据顶点位于平面的哪一侧而为负或为正。gl_ClipDistance 数组上的下标允许定义多个裁剪距离（即多个平面）。可定义的用户裁剪平面最大数量取决于显卡的 OpenGL 实现。

然后，必须在 Java/JOGL 应用程序中启用用户定义裁剪。OpenGL 内置了标识符 GL_CLIP_DISTANCE0、GL_CLIP_DISTANCE1 等，分别对应于每个 gl_ClipDistance[] 数组元素。例如，可以按如下方式启用第 0 个用户定义裁剪平面：

```
gl.glEnable(GL_CLIP_DISTANCE0);
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_343_0.png)

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_343_1.png)

将上述步骤应用到带光照的圆环体后，得到的输出如图 14.6 所示，其中圆环体的前半部分已被裁剪。（还应用了旋转，以提供更清晰的视图。）

看起来圆环体的底部似乎也被裁剪了，但这是因为圆环体的内表面没有被渲染。当裁剪露出形状的内表面时，也必须渲染这些内表面，否则模型会显得不完整（如图 14.6 所示）。

渲染内表面需要第二次调用 glDrawArrays()，并反转绕序。此外，在渲染背面三角形时，必须反转表面法线向量（如上一节所做的那样）。对 Java 应用程序和顶点着色器的相关修改如程序 14.3 所示，输出如图 14.7 所示。

### 程序 14.3 带背面的裁剪

Java/JOGL 应用程序：

```java
public void display(GLAutoDrawable drawable)
{
  ...
  flipLoc = gl.glGetUniformLocation(renderingProgram, "flipNormal");
  ...
  gl.glEnable(GL_CLIP_DISTANCE0);

  // normal drawing of external faces
  gl.glUniform1i(flipLoc, 0);
  gl.glFrontFace(GL_CCW);
  gl.glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);

  // rendering of back faces with normals reversed
  gl.glUniform1i(flipLoc, 1);
  gl.glFrontFace(GL_CW);
  gl.glDrawElements(GL_TRIANGLES, numTorusIndices, GL_UNSIGNED_INT, 0);
}
```

顶点着色器：

```glsl
...
vec4 clip_plane = vec4(0.0, 0.0, -1.0, 0.5);
uniform int flipNormal;        // flag for inverting normal
...
void main(void)
{
...
if(flipNormal==1) varyingNormal = -varyingNormal;
...
gl_ClipDistance[0] = dot(clip_plane.xyz, vertPos) - clip_plane.w;
...
}
```

## 14.4 3D 纹理

2D 纹理包含由两个变量索引的图像数据，而 3D 纹理包含相同类型的图像数据，但位于由三个变量索引的 3D 结构中。前两个维度仍然表示纹理贴图中的*宽度*和*高度*；第三个维度表示*深度*。

由于 3D 纹理中的数据以与 2D 纹理相似的方式存储，因此人们很容易把 3D 纹理看作某种 3D“图像”。然而，我们通常不把 3D 纹理源数据称为 3D 图像，因为这类结构没有常用的图像文件格式（也就是说，没有类似 3D JPEG 的东西，至少没有真正三维的此类格式）。相反，我们建议把 3D 纹理看作一种物质，我们将要为其贴图的对象浸入（或“蘸入”）其中，从而使对象的表面点从纹理中的对应位置获得颜色。或者，可以这样想象也很有用：对象是从 3D 纹理“立方体”中“雕刻”出来的，很像雕塑家从一整块实心大理石中雕刻出一个人像。

OpenGL 支持 3D 纹理对象。为了使用它们，我们需要学习如何构建 3D 纹理，以及如何使用它为对象贴图。

