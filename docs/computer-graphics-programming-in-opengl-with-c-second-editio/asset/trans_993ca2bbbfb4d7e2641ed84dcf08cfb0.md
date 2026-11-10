
- **GL_LINEAR_MIPMAP_NEAREST** 选择分辨率与被纹理化像素区域最相似的 mipmap。然后，它对最接近纹理坐标的四个纹素进行插值。这称为“线性过滤”。
- **GL_NEAREST_MIPMAP_LINEAR** 选择分辨率与被纹理化像素区域最接近的两个 mipmap。然后，它从每个 mipmap 中获取最接近纹理坐标的纹素，并对它们进行插值。这称为“双线性过滤”。
- **GL_LINEAR_MIPMAP_LINEAR** 选择分辨率与被纹理化像素区域最接近的两个 mipmap。然后，它在每个 mipmap 中对最接近的四个纹素进行插值，并对这两个结果进行插值。这称为“三线性过滤”，如图 5.11 所示。

![](img/1695de1bc7486362f86c143285f3fb40_138_0.png)

![](img/1695de1bc7486362f86c143285f3fb40_138_1.png)

三线性过滤通常更可取，因为较低层级的混合常常会产生伪影，例如 mipmap 层级之间可见的分离。图 5.12 展示了棋盘格的特写，其中启用了 mipmapping 但仅启用了线性过滤。请注意圈出的伪影：在 mipmap 边界处，竖线突然从粗变细。相比之下，图 5.9 中的示例使用了三线性过滤。

OpenGL 对 mipmapping 提供了丰富支持。它提供了用于构建自己的 mipmap 层级或让 OpenGL 为你构建这些层级的机制。大多数情况下，OpenGL 自动构建的 mipmap 就足够了。这可以通过在 Utils::loadTexture() 函数（前面 5.1 节中描述过）中，紧接在 getTextureObject() 函数调用之后添加以下代码行来实现：

```
glBindTexture(GL_TEXTURE_2D, textureID);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glGenerateMipmap(GL_TEXTURE_2D);
```

这告诉 OpenGL 生成 mipmap。通过 glBindTexture() 调用使砖块纹理变为活动状态，然后 glTexParameteri() 函数调用启用前面列出的某个缩小过滤选项，例如上面调用中显示的 GL_LINEAR_MIPMAP_LINEAR，它会启用三线性过滤。

mipmap 构建完成后，可以通过再次调用 glTexParameteri() 来更改过滤选项（尽管很少需要这样做），例如在显示函数中。甚至可以通过选择 GL_NEAREST 或 GL_LINEAR 来禁用 mipmapping。

对于关键应用，可以使用你偏好的任何图像编辑软件自行构建 mipmap。然后，在创建纹理对象时，可以通过为每个 mipmap 层级重复调用 OpenGL 的 glTexImage2D() 函数，将它们作为 mipmap 层级添加。对这种方法的进一步讨论超出了本书范围。

## 5.9 各向异性过滤

mipmap 纹理有时会比非 mipmap 纹理显得更模糊，尤其是当带纹理的对象以严重倾斜的视角渲染时。我们在图 5.9 中见过一个例子，其中使用 mipmapping 减少伪影导致细节减少（与图 5.8 相比）。

这种细节损失之所以发生，是因为当对象倾斜时，其图元沿一个轴（即宽度与高度）看起来比沿另一个轴更小。当 OpenGL 对图元进行纹理化时，它会选择适合两个轴中较小轴的那个 mipmap（以避免“闪烁”伪影）。在图 5.9 中，表面相对于观察者严重倾斜，因此每个渲染的图元将使用适合其缩小后高度的 mipmap，而其分辨率很可能低于适合其宽度的分辨率。

恢复部分丢失细节的一种方法是使用*各向异性过滤*（AF）。标准 mipmapping 以各种正方形分辨率（例如 256x256、128x128 等）对纹理图像进行采样，而 AF 还会以多种矩形分辨率（例如 256x128、64x128 等）对纹理进行采样。这使得可以在各种角度下查看，同时尽可能保留纹理中的细节。

各向异性过滤比标准 mipmapping 的计算开销更大，并且不是 OpenGL 的必需部分。然而，大多数显卡支持 AF（这称为 *OpenGL 扩展*），并且 OpenGL 确实既提供了一种查询显卡是否支持 AF 的方法，也提供了一种在其支持时访问 AF 的方法。代码紧接在生成 mipmap 之后添加：

```cpp
// if mipmapping
glBindTexture(GL_TEXTURE_2D, textureID);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glGenerateMipmap(GL_TEXTURE_2D);

// if also anisotropic filtering
if (glewIsSupported("GL_EXT_texture_filter_anisotropic")) {
    GLfloat anisoSetting = 0.0f;
    glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, &anisoSetting);
    glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT, anisoSetting);
}
```

![](img/1695de1bc7486362f86c143285f3fb40_140_0.png)

**图 5.13** 各向异性过滤。

对 glewIsSupported() 的调用会测试显卡是否支持 AF。如果支持，我们将其设置为支持的最大采样程度，即使用 glGetFloatv() 获取的值，如下所示。然后使用 glTexParameterf() 将其应用到活动纹理对象。结果如图 5.13 所示。请注意，图 5.8 中丢失的许多细节已经恢复，同时仍然去除了闪烁伪影。

## 5.10 环绕与平铺

到目前为止，我们假设纹理坐标都落在 [0..1] 范围内。然而，OpenGL 实际上支持任意值的纹理坐标。对于纹理坐标落在 [0..1] 范围之外时会发生什么，有几种选项可供指定。所需行为使用 glTexParameteri() 设置，其中一些选项如下：

- **GL_REPEAT**：忽略纹理坐标的整数部分，生成重复或“平铺”图案。这是默认行为。
- **GL_MIRRORED_REPEAT**：忽略整数部分，但当整数部分为奇数时坐标会反转，因此重复图案在正常和镜像之间交替。
- **GL_CLAMP_TO_EDGE**：小于 0 和大于 1 的坐标分别设置为 0 和 1。
- **GL_CLAMP_TO_BORDER**：[0..1] 之外的纹素将被赋予某个指定的边界颜色。

例如，考虑一个金字塔，其纹理坐标定义在 [0..5] 范围内而不是 [0..1] 范围内。使用前面图 5.2 中显示的纹理图像时，默认行为（GL_REPEAT）将导致纹理在表面重复五次（有时称为“平铺”），如图 5.14 所示：

![](img/1695de1bc7486362f86c143285f3fb40_141_0.png)

**图 5.14** 使用 GL_REPEAT 的纹理坐标环绕。

要使平铺块的外观在正常和镜像之间交替，我们可以指定以下内容：

```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_MIRRORED_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_MIRRORED_REPEAT);
```

要指定分别处理小于 0 和大于 1 的值，可以通过将 GL_MIRRORED_REPEAT 替换为 GL_CLAMP_TO_EDGE 来实现。

## 5.12 纹理——OpenGL 的其他细节

我们在本书中一直使用的 SOIL2 纹理图像加载库的优点是使用起来相对简单直观。然而，在学习 OpenGL 时，使用 SOIL2 会产生一个意想不到的后果：它屏蔽了一些对学习很有用且重要的 OpenGL 细节。在本节中，我们描述程序员在没有 SOIL2 这类纹理加载库的情况下加载和使用纹理时需要了解的一些细节。

可以使用 C++ 和 OpenGL 函数将纹理图像文件数据直接加载到 OpenGL 中。虽然这要复杂得多，但很常见。一般步骤如下：

- 1. 使用 C++ 工具读取图像文件。
- 2. 生成一个 OpenGL 纹理对象。
- 3. 将图像文件数据复制到纹理对象中。

我们不会详细描述第一步——有很多方法。opengl-tutorials.org 很好地描述了一种方法（具体教程页面是 [OT18]），它使用 C++ 函数 fopen() 和 fread() 将 .bmp 图像文件中的数据读入 unsigned char 类型数组。

步骤 2 和步骤 3 更通用，主要涉及 OpenGL 调用。在步骤 2 中，我们使用 OpenGL glGenTextures() 命令创建一个或多个纹理对象。例如，生成单个 OpenGL 纹理对象（带有一个整数引用 ID）可以按如下方式完成：

```
GLuint textureID;             // or an array of GLuint if making more than one texture object
glGenTextures(1, &textureID);
```

在步骤 3 中，我们将步骤 1 中的图像数据关联到步骤 2 中创建的纹理对象。这是使用 OpenGL glTexImage2D() 命令完成的。以下示例将步骤 1 中描述的 unsigned char 数组（此处记为“data”）中的图像数据加载到步骤 2 中创建的纹理对象中：

```
glBindTexture(GL_TEXTURE_2D, textureID);
glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, width, height, 0, GL_BGR,
             GL_UNSIGNED_BYTE, data);
```

此时，本章前面描述的各种用于设置 mipmap 等的 glTexParameteri() 调用都可以应用于该纹理对象。我们还
