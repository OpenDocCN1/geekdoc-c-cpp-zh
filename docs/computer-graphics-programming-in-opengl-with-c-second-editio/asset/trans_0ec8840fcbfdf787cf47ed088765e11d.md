
17.3 将程序12.5（镶嵌化月球表面）转换为红蓝立体和并排立体渲染两种形式。为相机运动制作动画，使其贴近月球表面掠过。

## 参考文献

- [B66] D. Brown（1966），*透镜偏心畸变*，Photogrammetric Engineering 32 (3)。
- [BS16] B. Smus（2016），*VR镜头畸变的三种方法*。博客文章，访问于2020年7月。https://smus.com/vr-lens-distortion/
- [C19] A. Conrady（1919），*偏心透镜系统*，Monthly Notices of the Royal Astronomical Society 79（1919）。
- [GC20] Google Cardboard——访问于2020年7月。https://arvr.google.com/cardboard
- [K16] B. Kehrer（2016），使用顶点位移进行VR畸变校正（博客），访问于2020年7月。https://www.ustwo.com/blog/vr-distortion-vertex-displacement
- [N10] S. Gateau、S. Nash（2010），*在应用程序中实现立体3D*，NVIDIA，GPU技术大会，加利福尼亚州圣何塞，访问于2020年7月，https://www.nvidia.com/content/GTC-2010/pdfs/2010_GTC2010.pdf
- [S16] Scratchapixel 2.0（2016），*透视与正交投影矩阵*，访问于2020年7月，https://www.scratchapixel.com
- [W20] G. Wetzstein（2020），*头戴式显示器光学1*，访问于2020年7月，https://stanford.edu/class/ee267/lectures/lecture7.pdf
- [WSE] 维基百科——立体视觉，访问于2020年7月，https://en.wikipedia.org/wiki/Stereoscopy
- [WSS] 维基百科——双眼立体视觉，访问于2020年7月，https://en.wikipedia.org/wiki/Stereopsis
- [WST] 维基百科——立体镜，访问于2020年7月，https://en.wikipedia.org/wiki/Stereoscope
- [WX20] WiredXDisplay（手机应用）——Splashtop.com，访问于2020年7月，https://www.splashtop.com/wiredxdisplay

## 附录A

## PC（Windows）的安装与设置

- A.1 *安装库与开发环境* ......... 481
- A.2 *在MS Visual Studio中开发和部署OpenGL项目* ......... 485

如第1章所述，为了在您的机器上使用OpenGL和C++，必须完成许多安装和设置步骤。这些步骤因您希望使用的平台而异。本书中的代码示例设计为在PC（Windows）上按原样运行；本附录提供Windows平台的设置说明。库和工具经常变化，因此这些步骤可能过时。我们在以下网址维护更新的安装和设置说明：http://ecs.csus.edu/~gordonsv/textC2E.html。

### A.1 安装库与开发环境

#### A.1.1 安装开发环境

由于我们在本书过程中实现多个项目，并且OpenGL中有如此多的库需要协调，因此以最小化每个新建项目所需配置步骤数量的方式设置C++开发环境将很有用。这里，我们假设使用*Visual Studio 2019* [VS20]；其他IDE可能可以采取类似步骤。

第一步是在您的机器上下载并安装Visual Studio 2019。完成此操作后，我们的方法是将尽可能多的库安装到一个共享位置，然后创建Visual Studio *自定义模板*，这样我们创建的每个新项目都已具备必要的库和依赖项，而无需重新定义。我们在A.2.1节描述创建此类模板。

#### A.5.4 准备GLEW

第1章概述了GLEW“扩展管理”库。从glew.sourceforge.net [GE17]下载64位二进制文件。我们特别需要获取的项目是：

- **glew32.lib**（位于“lib”文件夹中）——是的，名称包含“32”，但目前这些仍是64位安装的正确文件
- **glew32.dll**（位于“release”文件夹中）
- **GL** 文件夹，其中包含若干头文件（位于“include”文件夹中）

#### A.5.5 准备GLM

第1章概述了数学库GLM。访问glm.g-truc.net/0.9.9/index.html [GM20]并下载包含发行说明的最新版本。下载文件夹解压缩后包含一个名为“glm”的文件夹。该文件夹（及其内容）就是我们需要使用的项目。

#### A.5.6 准备SOIL2

第1章概述了图像加载库SOIL2。安装SOIL2 [SO20]需要使用一个名为“premake”的工具 [PM20]。尽管该过程涉及若干步骤，但它们相对直接：

- 1. 下载并解压缩“premake”。其中唯一的文件是“premake4.exe”。
- 2. 下载SOIL2（使用左侧面板底部的“downloads”链接），并解压缩。
- 3. 将“premake4.exe”文件复制到soil2文件夹中。
- 4. 打开命令窗口，导航到soil2文件夹，并输入：

```
premake --platform=x64 vs2012
```

它应显示随后创建的一些文件。

- 5. 在soil2文件夹中，打开“make”文件夹，然后打开“windows”文件夹。双击SOIL2.sln。
- 6. 如果Visual Studio提示升级库，请点击“ok”进行升级。
- 7. 使用顶部附近的下拉框从x86切换到x64，然后在右侧面板中右键单击“soil2-static-lib”并选择“build”。

一旦库安装完毕且自定义模板就位，创建新的OpenGL C++项目就很直接：

- 1. 启动Visual Studio，并点击“创建新项目”。
- 2. 在左上角选择您的OpenGL模板，然后点击“下一步”。
- 3. 为项目命名，然后点击“创建”。
- 4. 使用顶部的下拉框从“x86”切换到“x64”。
- 5. 回到Windows，导航到VS创建的、与新创建项目名称匹配的文件夹。其中应有另一个同名子文件夹。
- 6. 将构成应用程序的任何文件复制到该子文件夹中。这包括应用程序使用的任何 **.cpp** 源文件、**.h** 头文件、**.glsl** 着色器文件、纹理图像文件和 **.obj** 3D模型文件。无需指定模板中已内置的任何头文件。
- 7. 还将“**glew32.dll**”文件放入同一子文件夹。
- 8. 在右侧的解决方案资源管理器中，右键单击“源文件”并选择 *添加 ▶ 现有项* 以加载您的 **main.cpp** 文件。对其他.cpp文件重复该过程。
- 9. 同样在右侧的解决方案资源管理器中，右键单击“头文件”并选择 *添加 ▶ 现有项* 以加载应用程序中的任何头文件（**.h**）。
- 10. 现在您可以构建并执行程序了。

在开发、测试和调试应用程序之后，可以通过以“*发布*”模式构建项目，然后将以下文件放入单个文件夹，将其部署为独立可执行文件：

- 构建项目生成的 **.exe** 文件
- 应用程序使用的所有着色器文件
- 应用程序使用的所有纹理图像和模型文件
- **glew32.dll**

## 参考文献

- [CM20] CMake主页，访问于2020年7月，https://cmake.org
- [GE17] OpenGL扩展管理库（GLEW），访问于2020年7月，http://glew.sourceforge.net/
- [GF20] 图形库框架（GLFW），访问于2020年7月，http://www.glfw.org/
- [GM20] OpenGL数学库（GLM），访问于2020年7月，https://glm.g-truc.net/0.9.9/index.html
- [GV20] GLView，realtech-vr，访问于2020年7月，https://www.realtech-vr.com/home/glview
- [PM20] premake主页，访问于2020年7月，https://premake.github.io/
- [SO20] 简单OpenGL图像库2（SOIL2），*SpartanJ*，访问于2020年7月，https://github.com/SpartanJ/SOIL2
- [SW15] G. Sellers、R. Wright Jr. 和 N. Haemel，*OpenGL超级宝典：综合教程与参考*，第7版（Addison-Wesley，2015）。
- [VS20] Microsoft Visual Studio——下载，访问于2020年7月，https://www.visualstudio.com/downloads/
