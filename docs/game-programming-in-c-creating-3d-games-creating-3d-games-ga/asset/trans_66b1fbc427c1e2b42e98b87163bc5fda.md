

```
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER,
GL_LINEAR);
```

请注意，您仍然使用 GL_LINEAR 作为放大的过滤函数，因为当纹素密度低于 1:1 时，mipmaps 没有帮助。若要改为对缩小使用最近邻 mipmapping，您会将 GL_LINEAR_MIPMAP_NEAREST 作为 GL_TEXTURE_MIN_FILTER 调用的最后一个参数传入。

mipmapping 的另一个优势是，由于纹理缓存的工作方式，它提高了渲染性能。就像 CPU 缓存一样，显卡也有其内存的缓存。小的 mip 级别非常缓存友好，这意味着整体渲染性能会提升。

## 各向异性过滤

尽管 mipmapping 在大多数情况下大大减少了采样伪影，但相对于摄像机以倾斜角度查看的纹理会显得非常模糊。这一点在地板纹理上尤其明显，如图 13.6(b) 所示。各向异性过滤通过在以倾斜角度查看纹理时对纹理采样额外点来缓解这一问题。例如，16x 各向异性过滤意味着纹素颜色有 16 个不同的采样点。

图形硬件使用一系列数学函数执行各向异性计算。
本章不介绍这些函数，但您可以查阅本章末尾“进一步阅读”部分中的 OpenGL Extensions Registry 以获取更多信息。

尽管最新的 OpenGL 规范将各向异性过滤作为默认功能包含在内，但在 OpenGL 3.3 中，各向异性过滤是一个扩展。这意味着您在启用该功能之前应验证图形硬件是否支持各向异性。在大多数情况下，这属于学术问题，因为过去十年制造的每张显卡都支持各向异性过滤。但一般来说，在使用某个 OpenGL 扩展之前，测试该扩展是否可用是个好主意。

要启用各向异性过滤，您需要将纹理设置为使用 mipmapping，然后添加以下代码行：

点击此处查看代码图像

```
if (GLEW_EXT_texture_filter_anisotropic)
{
    // Get the maximum anisotropy value
    GLfloat largest;
    glGetFloatv(GL_MAX_TEXTURE_MAX_ANISOTROPY_EXT, &largest);
    // Enable it
    glTexParameterf(GL_TEXTURE_2D, GL_TEXTURE_MAX_ANISOTROPY_EXT, largest);
}
```

这段代码测试是否可用各向异性过滤，如果可用，则向 OpenGL 请求最大各向异性值。然后您设置纹理参数以使用各向异性过滤。

图 13.6 显示了本章游戏项目中不同设置下的地面。图 13.6(a) 显示了仅使用双线性过滤的地面；请注意地面在砖块边缘有许多采样伪影。图 13.6(b) 显示了启用三线性过滤；这是一种改进，但远处的地面是模糊的。最后，图 13.6(c) 显示了同时启用三线性过滤和各向异性过滤，这三种选择中它产生的视觉质量最好。

![](img/e9afcec1487716b0ef80d7e7c09869c8_849_0.png)

图 13.6 使用不同过滤方法查看地面：(a) 双线性过滤，(b) 三线性过滤，(c) 三线性和各向异性过滤

## 将内容渲染到纹理

到目前为止，您一直将多边形直接绘制到颜色缓冲区。然而，这个颜色缓冲区并不特殊；它只是一个您在特定坐标处写入颜色的 2D 图像。事实证明，您也可以将场景绘制到任何任意纹理，即**渲染到纹理**。虽然这可能看起来不必要，但有很多原因您可能希望渲染到纹理。

例如，一款赛车游戏可能有一辆带有后视镜的汽车。如果您希望后视镜看起来准确，您可以将游戏世界从后视镜的角度渲染到纹理，然后在场景中将纹理绘制到后视镜上。此外，一些图形技术在计算最终输出到颜色缓冲区之前，使用纹理作为临时存储。

本节探讨如何将内容渲染到纹理，然后在屏幕上显示此纹理。这需要对整体渲染代码进行一些更改，该代码之前假设所有内容都直接写入颜色缓冲区。您还需要添加从不同摄像机角度渲染场景的支持。

**注释**
对于高质量反射，例如大镜子，您必须从表面的角度渲染场景。但是，如果游戏场景包含许多需要低质量反射的表面，从每个表面的角度渲染场景代价太高。在这种情况下，您可以改为为整个场景生成单个**反射贴图**。然后，对于每个低质量反射表面，您从该反射贴图中采样以营造反射的错觉。尽管质量远低于从反射表面角度渲染，但对于只需要低质量反射的表面来说，这已经足够。
本书不介绍如何实现反射贴图，但您可以查阅本章末尾“进一步阅读”部分以获取该主题的更多信息。

### 创建纹理

要将内容渲染到纹理，您首先需要创建一个纹理。您可以向 `Texture` 类添加一个新函数，以支持创建用于渲染的纹理。创建纹理的代码（如清单 13.1 所示）与第 5 章中创建纹理的代码类似。但是，不再假设您需要 RGBA 格式（这将导致每个分量 8 位、每个像素 32 位），而是使用参数来指定格式。其次，纹理没有初始数据，这就是为什么 `glTexImage2D` 的最后一个参数是 `nullptr`。如果最后一个参数是 `nullptr`，则倒数第二个和倒数第三个参数会被忽略。最后，您故意不在纹理上启用 mipmapping 或双线性过滤。您希望从纹理中采样的数据能精确匹配实际输出。

### 清单 13.1 创建用于渲染的纹理

点击此处查看代码图像

```
void Texture::CreateForRendering(int width, int height,
unsigned int format)
{
mWidth = width;

mHeight = height;

// Create the texture id
glGenTextures(1, &mTextureID);

glBindTexture(GL_TEXTURE_2D, mTextureID);

// Set the image width/height with null initial data
glTexImage2D(GL_TEXTURE_2D, 0, format, mWidth, mHeight, 0, format, GL_FLOAT, nullptr);

// For a texture we'll render to, just use nearest
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_NEAREST);
}
```

### 创建帧缓冲对象

就像 OpenGL 使用顶点数组对象来包含有关顶点的所有信息（包括顶点缓冲区、顶点格式和索引缓冲区）一样，**帧缓冲对象**（FBO）包含有关帧缓冲区的所有信息。FBO 包括与帧缓冲区关联的任何纹理、关联的深度缓冲区（如果存在）以及其他参数。然后您可以选择用于渲染的帧缓冲区。

OpenGL 提供一个 ID 为 0 的默认帧缓冲对象，即您到目前为止一直在绘制的帧缓冲区。但是，您也可以创建其他帧缓冲区，并根据需要切换到其他帧缓冲区。

目前，您将使用自定义帧缓冲对象来实现后视镜，并在屏幕上的 HUD 中显示它。首先，您必须向 Renderer 类添加两个新的成员变量：

点击此处查看代码图像

```
// Framebuffer object for the mirror
unsigned int mMirrorBuffer;
// Texture for the mirror
class Texture* mMirrorTexture;
```

您将创建的帧缓冲对象的 ID 存储在 mMirrorBuffer 中，并将与帧缓冲区关联的纹理对象存储在 mMirrorTexture 中。

接下来，您需要一个创建和配置镜像帧缓冲对象的函数，如清单 13.2 所示。这里需要几个步骤。首先，glGenFramebuffers 创建帧缓冲对象并将 ID 存储在 mMirrorBuffer 中。然后 glBindFramebuffer 调用将此帧缓冲区设置为活动状态。CreateMirrorTexture 的接下来几行代码创建一个深度缓冲区并

