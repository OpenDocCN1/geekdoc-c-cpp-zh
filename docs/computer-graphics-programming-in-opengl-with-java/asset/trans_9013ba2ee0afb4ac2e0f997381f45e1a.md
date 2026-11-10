
恢复部分丢失细节的一种方法是使用*各向异性过滤*（AF）。标准 mipmapping 会在各种正方形分辨率（例如 256x256、128x128 等）下对纹理图像进行采样，而 AF 还会在若干矩形分辨率下对纹理进行采样，例如 256x128、64x128 等。这使得在从各种角度观察时，能够尽可能多地保留纹理中的细节。

各向异性过滤比标准 mipmapping 的计算开销更大，并且不是 OpenGL 的必需部分。然而，大多数显卡支持 AF（这被称为 *OpenGL 扩展*），并且 OpenGL 确实提供了查询显卡是否支持 AF 的方法，以及在其支持时访问 AF 的方法。相关代码紧接在生成 mipmap 之后添加：

```
...
// if mipmapping
gl.glBindTexture(GL_TEXTURE_2D, textureID);
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
gl.glGenerateMipmap(GL_TEXTURE_2D);

// if also anisotropic filtering
if (gl.isExtensionAvailable("GL_EXT_texture_filter_anisotropic"))
{
    float anisoSetting[] = new float[1];
    gl.glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, anisoSetting, 0);
    gl.glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT, anisoSetting[0]);
}
```

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_144_0.png)

调用 gl.isExtensionAvailable() 会测试显卡是否支持 AF。如果支持，我们就将其设置为受支持的最大 mipmapping 程度，该值通过所示的 glGetFloatv() 获取。然后使用 glTexParameterf() 将其应用到活动纹理对象。结果如图 5.13 所示。注意，图 5.8 中丢失的许多细节已经恢复，同时还去除了闪烁伪影。

**图 5.13**
各向异性过滤。

## 5.10 环绕与平铺

到目前为止，我们一直假设纹理坐标都落在范围 (0,1) 内。然而，OpenGL 实际上支持任意值的纹理坐标。有若干选项可用于指定当纹理坐标落在范围 (0,1) 之外时会发生什么。所需行为通过 glTexParameteri() 设置，其中一些选项如下：

- **GL_REPEAT**：纹理坐标的整数部分被忽略，生成重复或“平铺”图案。这是默认行为。
- **GL_MIRRORED_REPEAT**：整数部分被忽略，但当整数部分为奇数时坐标会反转，因此重复图案会在正常和镜像之间交替。
- **GL_CLAMP_TO_EDGE**：小于 0 和大于 1 的坐标分别被设置为 0 和 1。
- **GL_CLAMP_TO_BORDER**：(0,1) 之外的纹素将被赋予某个指定的边框颜色。

例如，考虑一个金字塔，其纹理坐标定义在范围 (0,5) 而不是范围 (0,1)。使用前面图 5.2 所示的纹理图像时，默认行为（GL_REPEAT）会导致纹理在表面上重复五次（有时称为“平铺”），如图 5.14 所示。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_145_0.png)

**图 5.14**
使用 GL_REPEAT 的纹理坐标环绕。

要使平铺块的外观在正常和镜像之间交替，我们可以指定以下内容：

```
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_MIRRORED_REPEAT);
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_MIRRORED_REPEAT);
```

指定小于 0 和大于 1 的值分别设置为 0 和 1，可以通过将 **GL_MIRRORED_REPEAT** 替换为 **GL_CLAMP_TO_EDGE** 来完成。

指定小于 0 和大于 1 的值产生“边框”颜色，可以按如下方式完成：

```
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_BORDER);
gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_CLAMP_TO_BORDER);
float[] redColor = new float[] { 1.0f, 0.0f, 0.0f, 1.0f };
gl.glTexParameterfv(GL_TEXTURE_2D, GL_TEXTURE_BORDER_COLOR, redColor, 0);
```

这些选项（镜像重复、钳制到边缘和钳制到边框）在纹理坐标范围为 −2 到 +3 时的效果，分别（从左到右）如图 5.15 所示。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_146_0.png)

在中间示例（钳制到边缘）中，纹理图像边缘的像素会向外复制。注意，作为一个副作用，金字塔面的左下和右下区域分别从纹理图像的左下和右下像素获得颜色。

### 5.5.1 透视畸变

我们已经看到，当纹理坐标从顶点着色器传递到片段着色器时，它们会在经过光栅化器时被插值。我们还看到，这是始终对顶点属性执行的自动线性插值的结果。

然而，对于纹理坐标而言，线性插值会在使用透视投影的 3D 场景中导致明显的畸变。

考虑一个由两个三角形组成、贴有棋盘图像并面向相机的矩形。当矩形绕 *X* 轴旋转时，矩形的顶部会向远离相机的方向倾斜，而矩形的下部会向更靠近相机的方向摆动。因此，我们会预期顶部的方格变小，底部的方格变大。然而，纹理坐标的线性插值反而会使*所有*方格的高度相等。沿着构成矩形的两个三角形的对角线，畸变会加剧。由此产生的畸变如图 5.16 所示。

幸运的是，存在用于校正透视畸变的算法，并且默认情况下，OpenGL 会在光栅化期间应用*透视校正*算法 [OP14, SP16]。图 5.17 展示了同一个旋转棋盘由 OpenGL 正确渲染的结果。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_147_0.png)

**图 5.16**
纹理透视畸变。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_147_1.png)

**图 5.17**
OpenGL 透视校正。

虽然不常见，但可以通过在包含纹理坐标的顶点属性声明中添加关键字“noperspective”来禁用 OpenGL 的透视校正。这必须在顶点着色器和片段着色器中都完成。例如，程序 5.1 的顶点着色器中的顶点属性将按如下方式声明：

```
    noperspective out vec2 tc;
```

片段着色器中对应的属性将声明为：

```
    noperspective in vec2 tc;
```

实际上，正是使用了第二种语法来生成图 5.16 中的畸变棋盘。

## 5.12 使用 JAVA AWT 类加载纹理图像文件

在本教材的其余部分，我们使用本章前面所述的 JOGL Texture、TextureIO 和 TextureData 类，将纹理图像数据加载到 OpenGL 纹理对象中。然而，也可以使用 Java AWT 类和一些额外的 OpenGL 命令，直接将纹理图像文件数据加载到 OpenGL 纹理中。这个过程要复杂得多，因此为了简单和清晰，本书将尽可能使用 JOGL 类。不过，了解可以替代 JOGL 纹理类使用的过程（以及特定命令）是有用的。例如，JOGL 纹理类不支持 3D 纹理，因此正如我们稍后将看到的，构建 OpenGL 3D 纹理对象将需要在 Java 中自行完成许多步骤。在构建天空盒时，我们也会使用其中一些步骤，如第 9 章所述。

程序 5.2 展示了一个不使用 JOGL 类、类似于程序 5.1 中的纹理加载函数。为避免混淆，我们将其称为 loadTextureAWT()。² 它首先调用两个实用函数（也一并展示）。第一个是 getBufferedImage()，它读取指定的图像文件（假定为 .jpg 或 .png 等可识别格式），并返回包含该图像文件数据的 Java BufferedImage。第二个实用函数 getRGBAPixelData() 从指定的 BufferedImage 中提取 RGBA 像素颜色，并以 OpenGL 所期望的形式组织在字节数组中返回。正是在这个函数中，我们可能会也可能不会像前面所述那样垂直翻转图像（由布尔参数指定），具体取决于应用。

然后，loadTextureAWT() 函数继续使用第 4 章所述的 JOGL Buffers.newDirectByteBuffer() 方法，将从 getRGBAPixelData() 返回的字节数组复制到 Java ByteBuffer 中。接着，它以类似于我们创建 VBO 的步骤的方式创建纹理对象。纹理与缓冲区一样，通过调用 glGenTextures() 被赋予整数 ID。这里，变量 textureID 用于保存生成的纹理对象的 ID。接下来，通过调用 glBindTexture() 使纹理对象变为活动状态，然后我们使用 glTexImage2D() 命令将先前读入的图像数据加载到活动纹理对象中。注意，此调用的第一个参数指定纹理对象的类型——在本例中为 GL_TEXTURE_2D（稍后我们将使用此命令创建其他类型的
