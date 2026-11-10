
屏幕分成两半，每只眼睛对应一侧。最终输出如图 17.6 所示。在本示例中，我们还像在程序 17.1 中那样，将清除颜色设置为雾的颜色。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_495_0.png)

**图 17.6** 程序 17.2（雾示例）的并排渲染。（最好通过立体头显观看）。

通过比较图 17.5 和图 17.6，我们可以看到图 17.6 中的图像明显在水平方向被压缩了。由于每幅图像只有一半的屏幕宽度可用于渲染，应用程序需要通过改变视场或宽高比来考虑这一点。在这个简单示例中，我们忽略了这一点。

## 17.6 校正头显中的镜头畸变

用于观看并排图像的头显采用高视场角镜头，这类镜头通常会产生镜头畸变。镜头中两种重要的畸变类型是*桶形畸变*，即直线向外凸出；以及*枕形畸变*，即直线向内收缩。图 17.7 展示了一个简单网格，以及同一网格在枕形畸变和桶形畸变下的效果。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_496_0.png)

**图 17.7** 简单网格（左），以及同一网格在枕形（中）和桶形（右）畸变下的效果。

大多数头显使用会产生枕形畸变的高视场角镜头。例如，考虑流行的立体头显 Google Cardboard® [GC20]，用户将手机放入带有两个镜片的纸板框架中。如果手机显示并排立体图像，就可以通过 Google Cardboard 以 3D 方式观看。图 17.8 展示了 Google Cardboard 头显，以及图 17.7 中最左侧的网格，但该网格实际上是通过 Google Cardboard 的一个镜头拍摄的。可以清楚地观察到枕形畸变。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_496_1.png)

**图 17.8** Google Cardboard 头显（左）以及通过其一个镜头观察到的简单网格（右），显示出枕形畸变。

由于头显通常使用会产生枕形畸变的镜头，面向虚拟现实头显的应用通常试图预先考虑枕形畸变，并通过施加反向畸变（具体而言是桶形畸变）来校正它。由于不同头显的镜头可能具有不同特性，这种*畸变校正*最好能针对不同头显进行调校。

测量和校正镜头畸变很复杂，完整研究超出了本书的范围。相反，我们逐步讲解一个典型示例的步骤。具体来说，我们对雾示例应用桶形畸变校正，并大致针对 Google Cardboard 头显进行调校。我们还会沿途指出一些可调参数。更全面的内容可在互联网上找到 [BS16]。

对渲染场景应用畸变校正可以通过多种方式完成。最高效的方法之一称为*顶点位移*，其中场景中的每个元素在渲染时都对顶点应用所需的畸变校正 [BS16]。为简单起见，本章使用一种更简单但效率较低的*基于片段着色器*的方法。步骤如下：

- 1. 从左眼视角将整个场景渲染到帧缓冲纹理。
- 2. 使用该纹理将一个矩形区域渲染到屏幕左半部分（此步骤中片段着色器应用桶形畸变）。
- 3. 对右眼重复该过程，渲染到屏幕右半部分。

我们已经研究过如何将场景渲染到帧缓冲纹理，例如在学习阴影时。我们刚刚学习了如何使用 `glViewport()` 渲染到屏幕的左半部分和右半部分。现在我们需要学习如何获取帧缓冲纹理，并在渲染它的同时对其中包含的图像进行畸变。

渲染（并为其添加纹理）一个矩形对象现在应该很简单，使用六个顶点组成两个三角形即可。然后，通常会在片段着色器中使用 `texture()` 函数应用相应的纹理，该函数需要 *X* 和 *Y* 纹理坐标参数。由于我们的矩形填满整个视口，*无畸变*渲染只需将纹理坐标缩放到视口尺寸即可实现，例如

```
fragColor = texture(gl_FragCoord.x / (sizeX/2), gl_FragCoord.y / sizeY);
```

相反，我们需要修改 *X* 和 *Y* 纹理查找值，使它们访问不同的纹素，具体来说，就是如果纹理经过桶形畸变后位于该位置 (X,Y) 的纹素。桶形畸变的数学推导可追溯到 100 多年前 Conrady [C19] 的工作，后由 Brown [B66] 进一步完善。VR 系统中常用的一种简化模型（来自 [W20]）如下：

$$x_u = x_d / (1 + K_1 r^2 + K_2 r^4)$$

$$y_u = y_d / (1 + K_1 r^2 + K_2 r^4)$$

其中 $(x_d, y_d)$ 是原始（畸变）纹理坐标位置，$(x_u, y_u)$ 是场景未畸变（校正后）版本中对应的纹理坐标，$r$ 是从 $(x_d, y_d)$ 到图像中心的直线距离，$K_1$ 和 $K_2$ 是可调常数。即使在这个简单模型中，$r$、$K_1$ 和 $K_2$ 的取值也需要根据观看设备进行调校，有时甚至需要根据观看者本人进行调校。Google Cardboard 的常用取值为 $K_1$ 取 -0.55，$K_2$ 取 0.34。对于 $r$，我们直接使用勾股定理计算距离，然后通过反复试验缩放该距离，以得到相当有效的结果。此后，我们将这种桶形畸变称为*镜头畸变校正*。

程序 17.3 展示了对程序 17.2 所做的修改，以便在带镜头畸变校正的情况下渲染每个半屏，并大致针对 Google Cardboard 调校。请注意，现有着色器（未更改）现在渲染到帧缓冲纹理，并且新增了第二组着色器，用于将这些帧缓冲纹理最终进行镜头畸变校正后输出到各自的半屏。代码之后还有补充讨论。最终输出如图 17.9 所示。

### 程序 17.3 带镜头畸变校正的并排渲染

Java/JOGL 应用程序

```java
// only the changes to Program 17.2 are shown here
...
// the 4th VBO (vbo[3]) is the rectangular region for drawing the texture buffer to half of the screen
private int vbo[] = new int[4];

private int renderingProgram, distCorrectionProgram;
private int leftRightBuffer, leftRightTexture;

private void setupVertices() {
    …
    // rectangular region for drawing half of the screen (these vertices are placed in vbo[3])
    float[] lensQuad =
    {
        -1.0f, 1.0f, 0.0f, -1.0f, -1.0f, 0.0f, 1.0f, 1.0f, 0.0f,
         1.0f, 1.0f, 0.0f, -1.0f, -1.0f, 0.0f, 1.0f, -1.0f, 0.0f
    };
    gl.glBindBuffer(GL_ARRAY_BUFFER, vbo[3]);
    FloatBuffer quadBuf = Buffers.newDirectFloatBuffer(lensQuad);
    gl.glBufferData(GL_ARRAY_BUFFER, quadBuf.limit()*4, quadBuf, GL_STATIC_DRAW);
}

private void setupLeftRightBuffer() {
    GL4 gl = (GL4) GLContext.getCurrentGL();

    // Initialize Framebuffer for rendering a screen half
    gl.glGenFramebuffers(1, bufferId, 0);
    leftRightBuffer = bufferId[0];
    gl.glBindFramebuffer(GL_FRAMEBUFFER, leftRightBuffer);
    gl.glGenTextures(1, bufferId, 0);      // this is for the color buffer
    leftRightTexture = bufferId[0];
    gl.glBindTexture(GL_TEXTURE_2D, leftRightTexture);
    gl.glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, myCanvas.getWidth() / 2, myCanvas.getHeight(),
        0, GL_RGBA, GL_UNSIGNED_BYTE, null);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_BORDER);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_CLAMP_TO_BORDER);
    float[] blackColor = { 0.0f, 0.0f, 0.0f, 1.0f };
    gl.glTexParameterfv(GL_TEXTURE_2D, GL_TEXTURE_BORDER_COLOR, blackColor, 0);
    gl.glFramebufferTexture2D(GL_FRAMEBUFFER, GL_COLOR_ATTACHMENT0, GL_TEXTURE_2D,
        leftRightTexture, 0);
    gl.glDrawBuffer(GL_COLOR_ATTACHMENT0);
    gl.glGenTextures(1, bufferId, 0);      // this is for the depth buffer
    gl.glBindTexture(GL_TEXTURE_2D, bufferId[0]);
    gl.glTexImage2D(GL_TEXTURE_2D, 0, GL_DEPTH_COMPONENT24, myCanvas.getWidth() / 2,
        myCanvas.getHeight(), 0, GL_DEPTH_COMPONENT, GL_FLOAT, null);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    gl.glFramebufferTexture2D(GL_FRAMEBUFFER, GL_DEPTH_ATTACHMENT, GL_TEXTURE_2D,
        bufferId[0], 0);
}
```
