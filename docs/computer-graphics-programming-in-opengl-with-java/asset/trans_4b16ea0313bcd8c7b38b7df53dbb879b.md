
OpenGL纹理，例如第9章中的纹理立方体贴图和第14章中的3D纹理。下一个命令glTexParameteri()可用于调整一些纹理设置，例如生成mipmap。当loadTextureAWT()完成时，它返回现在可用的OpenGL纹理对象的整数ID，正如我们在程序5.1中所做的那样。

假设我们已经将所有相关代码放在Utils.java工具类中，那么下面这一行对loadTextureAWT()的单次调用就会创建OpenGL纹理对象的整数ID：

```java
int brickTexture = Utils.loadTextureAWT("brick1.jpg");
```

### 程序5.2 用于加载纹理图像的Java AWT例程

```java
public static int loadTextureAWT(String textureFileName)
{   GL4 gl = (GL4) GLContext.getCurrentGL();
    BufferedImage textureImage = getBufferedImage(textureFileName);
    byte[] imgRGBA = getRGBAPixelData(textureImage, true);
    ByteBuffer rgbaBuffer = Buffers.newDirectByteBuffer(imgRGBA);

    int[] textureIDs = new int[1];                              // array to hold generated texture IDs
    gl.glGenTextures(1, textureIDs, 0);
    int textureID = textureIDs[0];                              // ID for the 0th texture object
    gl.glBindTexture(GL_TEXTURE_2D, textureID);                 // specifies the active 2D texture
    gl.glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA,                   // MIPMAP level, color space
        textureImage.getWidth(), textureImage.getHeight(), 0,   // image size, border (ignored)
        GL_RGBA, GL_UNSIGNED_BYTE,                              // pixel format and data type
        rgbaBuffer);                                            // buffer holding texture data
    gl.glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    return textureID;
}

private static BufferedImage getBufferedImage(String fileName)
{   BufferedImage img;
    try { img = ImageIO.read(new File(fileName)); }
    catch (IOException e)
    {   System.err.println("Error reading " + fileName + ""); throw new RuntimeException(e); }
    return img;
}

private static byte[] getRGBAPixelData(BufferedImage img, boolean flip)
{   byte[] imgRGBA;
    int height = img.getHeight(null);
    int width = img.getWidth(null);

    WritableRaster raster =
        Raster.createInterleavedRaster(DataBuffer.TYPE_BYTE, width, height, 4, null);
    ComponentColorModel colorModel = new ComponentColorModel(
        ColorSpace.getInstance(ColorSpace.CS_sRGB),
        new int[] { 8, 8, 8, 8 }, true, false,
        ComponentColorModel.TRANSLUCENT,          // bits, has Alpha, isAlphaPremultiplied
        DataBuffer.TYPE_BYTE);                    // transparency
                                                  // data transfer type

    BufferedImage newImage = new BufferedImage(colorModel, raster, false, null);
    Graphics2D g = newImage.createGraphics();

    // use an affine transform to "flip" the image to conform to OpenGL orientation.
    // In Java the origin is at the upper left. In OpenGL the origin is at the lower left.
    if (flip)
    {   AffineTransform gt = new AffineTransform();
        gt.translate(0, height);
        gt.scale(1, -1d);
        g.transform(gt);
    }
    g.drawImage(img, null, null);
    g.dispose();

    DataBufferByte dataBuf = (DataBufferByte) raster.getDataBuffer();
    imgRGBA = dataBuf.getData();
    return imgRGBA;
}
```

### 补充说明

研究人员已经开发出纹理单元的多种用途，而不仅仅是在场景中为模型添加纹理。在后续章节中，我们将看到如何使用纹理单元来改变光线在物体上的反射方式，使其看起来凹凸不平。我们还可以使用纹理单元存储“高度图”以生成地形，以及存储“阴影图”以高效地在场景中添加阴影。这些用途将在后续章节中描述。

着色器也可以写入纹理，从而允许着色器修改纹理图像，甚至将一个纹理的一部分复制到另一个纹理的某个部分。

Mipmap和各向异性过滤并不是减少纹理中锯齿伪影的唯一工具。例如，全场景抗锯齿（FSAA）和其他超采样方法也可以改善3D场景中纹理的外观。虽然它们不是OpenGL核心的一部分，但许多显卡通过OpenGL的扩展机制[OE21]支持它们。

还有一种配置和管理纹理与采样器的替代机制。OpenGL 3.3版本引入了*采样器对象*（有时称为“*采样器状态*”——不要与采样器变量混淆），它可以用来保存一组与实际纹理对象无关的纹理设置。采样器对象附加到纹理单元上，可以方便高效地更改纹理设置。本教科书中的示例足够简单，因此我们决定不介绍采样器对象。对于感兴趣的读者，采样器对象的使用很容易学习，而且有许多优秀的在线教程（例如[GE11]）。

JOGL的Texture类直接提供了许多与OpenGL纹理相关的函数，而不需要像本章那样提取实际的OpenGL纹理对象。例如，其中有bind()和setTexParameter()函数，它们会调用OpenGL函数glBindTexture()和glTexParameter()。在本书后面研究立方体贴图和3D纹理时，我们将进一步探索JOGL纹理类中的更多功能。关于JOGL的Texture、TextureIO和TextureData类，其详尽的Javadoc页面是一个很好的信息来源。

### 习题

- **5.1** 修改程序5.1，按照5.11节的描述，向纹理坐标顶点属性添加“noperspective”声明。然后重新运行程序，并将输出与原始程序进行比较。是否存在明显的透视失真？
- **5.2** 使用简单的“画图”程序（如Windows“画图”或GIMP [G16]），绘制一幅自己设计的手绘图。然后使用你的图像为程序5.1中的金字塔添加纹理。
- **5.3** *（项目）* 修改程序4.4，使“太阳”、“行星”和“月亮”具有纹理。你可以继续使用已有的形状，也可以使用任何你喜欢的纹理。这将要求你为立方体构建纹理坐标。

### 参考文献

- [BL21] Blender，Blender基金会，访问于2021年3月，https://www.blender.org/
- [GE11] Geeks3D，“OpenGL采样器对象：控制你的纹理单元”，2011年9月8日，访问于2021年3月，http://www.geeks3d.com/20110908/
- [GI21] GNU图像处理程序，访问于2021年3月，http://www.gimp.org
- [HT12] J. Hastings-Trew，*JHT的行星像素商场*，访问于2021年3月，http://planetpixelemporium.com/
- [LU16] F. Luna，*DirectX 12 3D游戏编程入门*，第2版（Mercury Learning，2016）。
- [MA21] Maya，AutoDesk公司，访问于2021年3月，http://www.autodesk.com/products/maya/overview
- [OE21] OpenGL注册表，Khronos集团，访问于2021年3月，https://www.khronos.org/registry/OpenGL/index_gl.php
- [OP14] OpenGL图形系统：规范（4.4版），M. Segal 和 K. Akeley，2014年3月19日，访问于2021年3月，https://www.khronos.org/registry/OpenGL/specs/gl/glspec44.core.pdf
- [OP21] OpenGL 4.5参考页面，访问于2021年3月，https://www.khronos.org/registry/OpenGL-Refpages/gl4/
- [SP16] 透视校正插值与顶点属性。Scratchapixel，©2016，访问于2021年3月。https://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation
- [TU18] J. Turberville，Studio522 Productions，亚利桑那州斯科茨代尔，www.studio522.com（海豚模型开发于2021年3月）。
- [WI83] L. Williams，“金字塔参数化”，*计算机图形学* 17卷，第3期（1983年7月）。

## 第6章：3D模型

- **6.1** *程序化模型——构建球体* ... 134
- **6.2** *OpenGL索引——构建环面* ... 142
- **6.3** *加载外部生成的模型* ... 148
- *补充说明* ... 158

到目前为止，我们只处理了非常简单的3D对象，例如立方体和金字塔。这些对象非常简单，以至于我们可以在源代码中显式列出所有顶点信息，并直接将其放入缓冲区。

然而，大多数有趣的3D场景包含的对象过于复杂，无法继续像我们之前那样手工构建。在本章中，我们将探索更复杂的对象模型、如何构建它们，以及如何将它们加载到我们的场景中。

3D建模本身就是一个广泛的领域，我们在这里的讨论必然非常有限。我们将重点关注以下两个主题：

- *程序化构建模型*
- *加载外部生成的模型*

虽然这只是触及了3D建模这一丰富领域的皮毛，但它将使我们能够将各种复杂且具有真实细节的对象包含到场景中。

