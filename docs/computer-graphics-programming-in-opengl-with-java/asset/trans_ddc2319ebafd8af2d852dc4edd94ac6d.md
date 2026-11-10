
## *片段着色器（"fragDistCorrShader.glsl"）*

```glsl
// The fragment shader does all of the lens distortion correction computations
#version 430
out vec4 fragColor;
uniform float leftRight; // -1 for left, +1 for right
uniform float winSizeX;
uniform float winSizeY;
layout(binding=0) uniform sampler2D lensTex; // this is the previously rendered framebuffer texture

void main(void)
{ float K1 = -0.55; // distortion parameters for Google Cardboard
  float K2 = 0.34;

  // compute the location in the half window scaled to (-0.5,+0.5) with (0,0) center
  float xd = (gl_FragCoord.x - winSizeX*leftRight) / winSizeX - 0.5;
  float yd = gl_FragCoord.y / winSizeY - 0.5;

  // compute the distance to the center of the half window
  float ru = sqrt(pow(xd,2.0) + pow(yd,2.0));

  // tune conversion from screen units to physical millimeters
  float mmRatio = 1.3; // ratio of ru/d, where d is the distance to the lens
  float rn = ru * mmRatio;

  // compute the undistorted corresponding location
  float distortionFactor = 1 + K1 * pow(rn,2.0f) + K2 * pow(rn,4.0f);
  float xu = xd / distortionFactor;
  float yu = yd / distortionFactor;

  // move the resulting point by (+0.5, +0.5) to convert to texture space
  fragColor = texture(lensTex, vec2(xu+0.5, yu+0.5));
}
```

在程序17.3中，具体是Java/JOGL应用程序，帧缓冲纹理的设置（即设置leftRightBuffer及其关联的名为leftRightTexture的纹理）与程序15.3中的水示例完全相同。在那里，该缓冲区用于存储反射（后来，第二个缓冲区用于存储折射）。这里，它用于存储整个场景，尺寸与半屏窗口视口相同。创建第二个渲染程序（称为distCorrectionProgram）用于将此缓冲区显示到屏幕，这发生在函数copyFrameBufferToViewport()中，该函数为左眼调用一次，然后为右眼再次调用。其余大部分Java代码保持不变，包括渲染场景细节的scene()函数。display()函数被扩展以管理启用两个帧缓冲（屏幕缓冲或leftRightBuffer）中的哪一个处于活动状态。

手机，本质上将手机变成计算机显示器。然后将手机放入Google Cardboard头显中，该头显假定显示屏左半部分用于左眼，右半部分用于右眼。图17.10展示了为程序17.3部署此配置的情况。

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_504_0.png)

**图17.10**  
使用Google Cardboard时程序17.3的并排输出。

测试立体图（anaglyph）示例（例如程序17.1中的示例）的硬件要简单得多。我们使用一套廉价的纸板红/青眼镜，可在网上购买。

## 补充说明

本章描述的立体视觉技术仅构成非常基础的介绍。电影院和VR游戏及应用的专业系统通常使用更复杂的模型，并针对所用硬件进行更仔细的调校。我们还忽略了重要的相关主题，例如用于景深渲染的视网膜模糊，这些主题会在完整的专业部署中纳入。尽管如此，使用这里展示的简单方法来以完整的3D深度感知体验教科书中的各种示例仍然很有趣。

在少数情况下，存在一些障碍。教科书中的一些示例出于各种目的使用用户定义的帧缓冲，或渲染到纹理，例如用于构建阴影、生成水效果或进行光线追踪。在这些情况下，需要进一步修改Java代码以管理缓冲区。这在第15章的水示例中尤其棘手，因为反射和折射缓冲区在很大程度上是估算的，如果不加修改，就不适合在两只眼睛之间准确分割。

我们选择雾示例进行渲染，因为雾进一步有助于立体效果，而且该示例没有因红/青立体观看的颜色限制而受到过度妨碍。教科书中的其他一些示例的颜色在红/青立体观看时效果不会那么好。

读者无疑已经注意到，我们的并排渲染在水平方向上被压扁了。为了尽可能保持代码简单，我们没有对此进行校正。更完整的解决方案还会校正视图视锥体，使宽高比不会发生如此剧烈的变化。并排观看的一个缺点是，渲染场景时会损失一半的屏幕实际面积。

关于校正镜头畸变的*顶点位移*方法的细节（其性能优于本章介绍的基于片段着色器的简单方法）可在其他地方找到[K16]。

尽管我们介绍了用于虚拟现实系统等的基本立体渲染（和观看）方法，但还有相当大的一组VR主题我们完全没有讨论。完整的VR系统不仅以立体3D显示，还包括传感器，使用户能够更自然地移动和交互，例如通过转头或伸手。我们仅关注图形。

本章也没有涵盖如何为偏振或快门技术进行渲染（尽管在本章开头简要提到了它们）。这些需要更专门的硬件，其解决方案超出了本入门的范围。

## 练习

- 17.1 修改程序17.1，尝试各种不同的IOD值。你认为哪种取值范围最适合此场景？如果IOD设置得太小会发生什么？当IOD增大时你观察到什么，然后当IOD设置得太大时又会发生什么？
- 17.2 将程序4.2（具体是包含100,000个立方体的修改版）转换为立体图和并排立体渲染。
- 17.3 将程序12.5（镶嵌的月球表面）转换为立体图和并排立体渲染。为相机移动设置动画，使其贴近月球表面掠过。

## 参考文献

- [B66] D. Brown（1966），*镜头偏心畸变*，Photogrammetric Engineering 32 (3)。
- [BS16] B. Smus（2016），*VR镜头畸变的三种方法*。博客文章，访问于2020年7月。https://smus.com/vr-lens-distortion/
- [C19] A. Conrady（1919），*偏心镜头系统*，Monthly Notices of the Royal Astronomical Society 79（1919）。
- [GC20] Google Cardboard——访问于2020年7月。https://arvr.google.com/cardboard
- [K16] B. Kehrer（2016），使用顶点位移进行VR畸变校正（博客），访问于2020年7月。https://www.ustwo.com/blog/vr-distortion-vertex-displacement
- [N10] S. Gateau, S. Nash（2010），*在应用程序中实现立体3D*，NVIDIA，GPU Technology Conference，San Jose CA，访问于2020年7月，https://www.nvidia.com/content/GTC-2010/pdfs/2010_GTC2010.pdf
- [S16] Scratchapixel 2.0（2016），*透视与正交投影矩阵*，访问于2020年7月。https://www.scratchapixel.com
- [W20] G. Wetzstein（2020），*头戴式显示器光学1*，访问于2020年7月，https://stanford.edu/class/ee267/lectures/lecture7.pdf
- [WSE] Wikipedia——立体视觉术（Stereoscopy），访问于2020年7月，https://en.wikipedia.org/wiki/Stereoscopy
- [WSS] Wikipedia——立体视觉（Stereopsis），访问于2020年7月，https://en.wikipedia.org/wiki/Stereopsis
- [WST] Wikipedia——立体镜（Stereoscope），访问于2020年7月，https://en.wikipedia.org/wiki/Stereoscope
- [WX20] WiredXDisplay（手机应用程序）——Splashtop.com，访问于2020年7月，https://www.splashtop.com/wiredxdisplay

## PC（Windows）安装与设置

A.1 *安装库和开发环境* . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 487

如第1章所述，要在你的机器上使用OpenGL和Java，必须完成许多安装和设置步骤。这些步骤因你希望使用的平台而异。本书中的代码示例设计为在PC（Windows）上按原样运行；本附录提供Windows平台的设置说明。库和工具经常变化，因此这些步骤可能会过时。我们在以下地址维护更新的安装和设置说明：*http://ecs.csus.edu/~gordonsv/text/J3E.html*。

### A.1 安装库和开发环境

#### A.1.1 安装Java

要将Java用于本书中的示例，你将需要JRE（Java运行时环境）和JDK（Java开发工具包）。要安装它们，请使用Oracle的下载站点*http://www.oracle.com/java/technologies*，并在“Newest Downloads”下单击“Java SE 11 (LTS)”链接。在那里你可以找到下载最新JDK的说明，其中包含Java编译器和JRE。我们假设读者具有Java编程经验，并使用版本11。

#### A.1.2 安装OpenGL/GLSL

不需要“安装”OpenGL或GLSL，但有必要确保你的显卡至少支持OpenGL 4.3版。如果你不知道
