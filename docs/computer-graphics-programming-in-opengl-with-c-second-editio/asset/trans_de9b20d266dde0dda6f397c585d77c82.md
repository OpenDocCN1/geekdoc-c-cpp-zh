

```cpp
glViewport(0, 0, sizeX/2, sizeY);
copyFramebufferToViewport(window, 0.0f);

// draw right viewport to framebuffer texture
clearBuffer();
glBindFramebuffer(GL_FRAMEBUFFER, leftRightBuffer);
glViewport(0, 0, sizeX/2, sizeY);
display(window, glfwGetTime(), 1);

// transfer right viewport framebuffer to the screen
glBindFramebuffer(GL_FRAMEBUFFER, 0);
glViewport(sizeX/2, 0, sizeX/2, sizeY);
copyFramebufferToViewport(window, 1.0f);

glViewport(0, 0, sizeX, sizeY);
glfwSwapBuffers(window);
glfwPollEvents();
}
glfwDestroyWindow(window);
glfwTerminate();
exit(EXIT_SUCCESS);
}
```

### 顶点着色器（"vertDistCorrShader.glsl"）

```glsl
// these shaders are for the final rendering of the completed framebuffer texture
// the vertex shader is just a simple pass-through to the fragment shader
#version 430
layout(location=0) in vec3 position;
uniform int leftRight;
uniform float winSizeX;
uniform float winSizeY;
layout(binding=0) uniform sampler2D lensTex;

void main(void)
{ gl_Position = vec4(position, 1.0);
}
```

### 片元着色器（"fragDistCorrShader.glsl"）

```glsl
// The fragment shader does all of the lens distortion correction computations
#version 430
out vec4 fragColor;
uniform int leftRight;        // -1 for left, +1 for right
uniform float winSizeX;
uniform float winSizeY;
layout (binding=0) uniform sampler2D lensTex;    // this is the previously rendered framebuffer texture

void main(void)
{ float K1 = -0.55; // distortion parameters for Google Cardboard
  float K2 = 0.34;

  // compute the location in the half window scaled to (-0.5,+0.5) with (0,0) center
  float xd = (gl_FragCoord.x-winSizeX*leftRight) / winSizeX - 0.5;
  float yd = gl_FragCoord.y / winSizeY - 0.5;

  // compute the distance to the center of the half window
  float ru = sqrt(pow(xd,2.0) + pow(yd,2.0));

  // tune conversion from screen units to physical millimeters
  float mmRatio = 1.3; // ratio of ru/d, where d is the distance to the lens
  float m = ru * mmRatio;

  // compute the undistorted corresponding location
  float distortionFactor = 1 + K1 * pow(m,2.0) + K2 * pow(m,4.0);
  float xu = xd / distortionFactor;
  float yu = yd / distortionFactor;

  // move the resulting point by (+0.5, +0.5) to convert to texture space
  fragColor = texture(lensTex, vec2(xu+0.5, yu+0.5));
}
```

在程序17.3中，具体来说是在C++/OpenGL应用程序中，帧缓冲纹理的创建（即设置leftRightBuffer及其关联的纹理leftRightTexture）与程序15.3中的水面示例完全相同。在那里，该缓冲用于存储反射（之后第二个缓冲用于存储折射）。在这里，它用于存储整个场景，其尺寸与半屏窗口视口相同。我们创建了第二个渲染程序（称为distCorrectionProgram）用于将该缓冲显示到屏幕上，这发生在函数copyFramebufferToViewport()中，该函数先为左眼调用一次，再为右眼调用一次。其余大部分C++代码保持不变，包括渲染场景的display()函数。main()函数被扩展为管理两个帧缓冲（屏幕缓冲或leftRightBuffer）中哪一个处于激活状态。

实际的失真校正发生在distCorrectionProgram的片元着色器中。该GLSL着色器代码实现了（1）计算当前渲染位置到半屏视口中心的距离，（2）镜头失真校正计算，以及（3）在leftRightTexture中进行的最终纹素查找。

![](img/1695de1bc7486362f86c143285f3fb40_497_0.png)

**图17.9**
程序17.3的并排渲染效果，包含镜头失真校正（最好通过立体头戴设备观看）

## 17.5 一个简单的测试硬件配置

如今有许多方式可以观看并排场景，例如程序17.3渲染的那种。虽然现代头戴设备可能价格不菲，但作者在准备本章示例时使用的一种简单方法是采用以下一组技术：

- 一部连接电脑的较新的智能手机（如Android或iPhone）
- WiredXDisplay [WX20]（手机应用），可将电脑屏幕内容复制到手机上
- 用Google Cardboard [GC20] 以分屏方式查看手机显示

对于已经拥有智能手机的读者来说，上述方案的总成本不到20美元。手机可以通过USB数据线连接到电脑。WiredXDisplay应用随后将电脑屏幕内容传输到手机上，基本上就是把手机变成电脑显示器。然后将手机放入Google Cardboard头戴设备中，该设备假定显示屏的左半部分用于左眼，右半部分用于右眼。图17.10展示了为程序17.3部署此配置的情况。

![](img/1695de1bc7486362f86c143285f3fb40_498_0.png)

**图17.10**
程序17.3使用Google Cardboard的并排输出

用于测试红/青立体（anaglyph）示例（如程序17.1中的示例）的硬件则要简单得多。我们使用的是一副廉价的纸板红/青眼镜，可以在网上购买。

## 补充说明

本章所述的立体技术仅仅是一个非常基础的介绍。用于电影院和VR游戏及应用程序的专业系统通常会采用更复杂的模型，并且会针对所用硬件进行更细致的调校。我们还忽略了一些重要的相关主题，例如用于景深渲染的视网膜模糊，这在完全专业的部署中会包含。话虽如此，使用这里展示的简单方法来体验整本教材中各种具有完整3D深度感的示例，还是很有趣的。

在少数情况下，会遇到一些障碍。教材中的一些示例出于各种目的使用用户自定义帧缓冲或渲染到纹理，例如构建阴影、生成水面效果或进行光线追踪。在这些情况下，需要进一步修改C++代码来管理缓冲。这在第15章的水面示例中尤其棘手，因为那里的反射和折射缓冲大多是估算出来的，在不进行修改的情况下，很难在两只眼睛之间准确分割。

我们选择雾效示例进行渲染，是因为雾效进一步增强了立体效果，而且该示例受红/青立体观看的色彩限制影响不大。教材中其他一些示例的颜色在红/青立体模式下观看时效果不会那么好。

读者无疑已经注意到，我们的并排渲染在水平方向被压缩了。我们没有对此进行校正，以尽可能保持代码简单。一个更完整的解决方案还应校正视锥体，使宽高比不至于发生如此显著的改变。并排观看的一个缺点是渲染场景时会损失一半的屏幕可用区域。

关于用于校正镜头失真的*顶点位移*方法的详细信息，可在别处找到[K16]，该方法的性能优于本章介绍的基于简单片元着色器的方法。

尽管我们已经介绍了应用于虚拟现实系统的基本立体渲染（和观看）方法，但仍有一大批VR主题我们完全没有讨论。一个完整的VR系统不仅以立体3D方式显示，还包含传感器，使用户能够更自然地移动和交互，例如转头或用手够取物体。我们只专注于图形方面。

本章也没有涵盖如何为偏振或快门技术进行渲染（尽管在章节开头简要提到了它们）。这些技术需要更专门的硬件，其解决方案超出了本入门介绍的范畴。

## 练习

- 17.1 修改程序17.1，尝试多种不同的IOD值。你认为对于这个场景，哪个值范围效果最好？如果IOD设置得太小会发生什么？随着IOD增大会观察到什么？当IOD设置得过大时又会发生什么？
- 17.2 将程序4.2（特别是修改后的包含100,000个立方体的版本）同时转换为红/青立体和并排立体。

