
![](img/bfd978e7e9b192bab46ec2a89e481263_1288_0.png)

**图 27.18** 球从顶墙弹开。

左侧。如果球向右运动，将其 x 值乘以 −1 会改变符号并反转方向。我们用同样的方法来改变垂直方向。我们游戏中的碰撞是相当简单的情况，因此我们保持逻辑简单。有一些完整的库专门用于处理碰撞和物理，例如 Open Dynamics Engine（ODE，www.ode.org/）、Bullet（www.continuousphysics.com/Bullet/）、Newton Game Dynamics（www.newtondynamics.com/）和 PhysX（www.ageia.com/）。这些库在 Ogre 社区插件页面上有可用的 Ogre 绑定。

![](img/bfd978e7e9b192bab46ec2a89e481263_1289_0.png)

**图 27.19** 球从左球拍弹开。

### 27.4.7 声音

现在我们讨论在 Ogre 程序中导入声音和播放声音文件，我们将用它们来“给”我们的 Pong 游戏“增添活力”。每当球撞到墙时，我们播放一个“boing”声音；每当球撞到球拍时，我们播放另一个不同的“boing”声音；每当玩家得分时，我们播放欢呼声。

addResourceLocation 函数（图 27.5，第 79–80 行）接受三个 Ogre::String 参数。第一个是资源的位置。我们将所有资源放在示例目录下一个名为 resources 的文件夹中。通常你会按类型将资源组织到不同文件夹中，例如 materials、models 和 overlays。但为简单起见，我们只维护一个文件夹来存放游戏所需的所有资源。第二个参数是资源所在的文件类型。第三个是这些文件所属的资源组。我们将这些文件放入 "Pong" 组。现在，我们加载刚刚添加位置中的资源（第 81 行）。

### 27.4.9 Pong 驱动程序

最后一步是编写 main 函数（图 27.20）。Ogre 支持各种平台，因此应尽量避免编写平台特定代码。预处理器 if else 包装（第 8–17 行）将确定程序是否运行在 Windows 平台上。如果是，它将包含 windows.h 头文件并定义 WinMain 函数。如果不是，它将定义普通的 main 函数。这使代码无需修改即可在各种平台上运行。你可能以前没见过 Windows 特定代码。包含 windows.h 头文件的预处理指令使程序能够必要地访问 Windows API 来运行我们的程序。定义 WIN32_LEAN_AND_MEAN（第 9 行）将排除 windows.h 头文件中很少使用的头文件。这将加快程序的编译时间。

```cpp
// PongMain.cpp
// Driver program for the game of Pong
#include <iostream>
#include "Pong.h" // Pong class definition
using namespace std;

// If running on Windows, include windows.h and define WinMain function
#if OGRE_PLATFORM==PLATFORM_WIN32 || OGRE_PLATFORM==OGRE_PLATFORM_WIN32
#define WIN32_LEAN_AND_MEAN
#include "windows.h"

int WINAPI WinMain( HINSTANCE hInst, HINSTANCE, LPSTR strCmdLine, INT )

// If not, define normal main function
#else
int main()
#endif
{
    try
    {
        Pong game; // create a Pong object
        game.run(); // start the Pong game
    } // end try
    catch ( runtime_error &error )
    {
#if OGRE_PLATFORM==PLATFORM_WIN32 || OGRE_PLATFORM==OGRE_PLATFORM_WIN32
        MessageBoxA( NULL, error.what(), "Exception Thrown!",
                     MB_OK | MB_ICONERROR | MB_TASKMODAL );
```

**图 27.20** Pong 游戏的驱动程序。（第 1 部分，共 2 部分。）

```cpp
#else
    cerr << "Exception Thrown: " << error.what() << endl;
#endif
} // end catch
} // end main
```

**图 27.20** Pong 游戏的驱动程序。（第 2 部分，共 2 部分。）

main 函数在 try 块中创建初始 Pong 对象（第 19–23 行）。回想一下，如果用户取消 Ogre 配置对话框，Pong 构造函数会抛出异常。如果用户在该对话框上点击“确定”，则创建 Pong 对象，并调用 run 成员函数（第 22 行）。类 Pong 的成员函数 Run（图 27.5，第 172–176 行）首先创建游戏场景（第 174 行），然后调用类 Root 的 startRendering 成员函数（第 175 行）来反复渲染场景，直到 frameStarted 或 frameEnded 函数返回 false。

## 27.5 小结

在本章中，你学习了使用 Ogre 创建计算机游戏的基础知识。我们讨论了图形学的基本概念，简要描述了模型、光照和颜色。你了解了如何使用免费的 Ogre 3D 渲染引擎来制作 3D 游戏。我们展示了如何使用 SceneManager 创建和管理场景。你学习了如何使用 Camera 查看场景。我们讨论了使用 OIS 响应键盘用户输入。我们演示了如何以恒定速度移动对象。我们涵盖了碰撞检测的基础知识，并说明了它对游戏编程的重要性。你学习了如何使用 Overlay 在屏幕上显示文本。我们展示了 Ogre 如何使用脚本管理材质和 Overlay，而无需每次更改时重新编译。我们还展示了如何使用 OpenAL 的 OgreAL 包装器向游戏中添加声音。

本章应仅视为入门介绍。我们向你展示了一个 Pong 的基本示例。请以它为基础开发你自己的版本。走出去寻找你自己的声音来使用。向游戏添加新功能。探索 Ogre 的其他能力，并创建一些酷炫的视觉效果。真正让这个游戏成为你自己的作品。游戏编程的关键就在于发挥创造力。

## 27.6 Ogre Web 资源

- **www.ogre3d.org/**  
  Ogre 主页。在这里你可以找到最新的 Ogre 新闻、下载 Ogre 或 Ogre 相关工具、浏览文档，或查看使用 Ogre 的项目。

- **www.ogre3d.org/index.php?option=com_content&task=view&id=411&Itemid=131**  
  预构建 SDK 下载页面。有适用于 Code::Blocks + MinGW C++ Toolbox、Visual C++ .Net 2003 和 Visual C++ .Net 2005（必须安装 Service Pack 1）的 SDK。

- **www.ogre3d.org/index.php?option=com_content&task=view&id=412&Itemid=132**  
  Ogre 源代码下载页面。源代码适用于 Windows、Linux 和 Mac OS X。还可下载适用于你平台的第三方依赖包。页面上还有从源代码构建 Ogre 的指南链接。

- **www.ogre3d.org/index.php?option=com_content&task=view&id=415&Itemid=144**  
  有关从 CVS 目录获取 Ogre 源代码的说明。

- **www.ogre3d.org/wiki/index.php/Installing_An_SDK**  
  Ogre SDK 在 Windows 上使用 Visual C++、Code::Blocks + MinGW、Code::Blocks + MinGW + STLPort、Eclipse + MinGW + STLPort 和 GCC & Make/Any IDE 的安装说明。Linux、Debian、Gentoo、Fedora 和 Ubuntu。Mac OS X。

- **www.ogre3d.org/wiki/index.php/Building_From_Source**  
  在 Windows 上使用 Visual C++、Visual C++ Toolkit 2003 & Code::Blocks 和 GCC 构建 Ogre 源代码的说明。Linux 上使用 GCC & Make、Debian、Fedora、Gentoo、Ubuntu/Kubuntu。Mac OS X 上使用 Xcode。

- **www.ogre3d.org/wiki/index.php/BuildFAQ**  
  从源代码构建时常见错误的解决方案。错误包括无法找到文件、未解析的外部符号以及其他类型的错误。

- **www.ogre3d.org/wiki/index.php/SettingUpAnApplication**  
  在 Visual C++、Code::Blocks、GCC、Autotools、Scons、Eclipse、Anjuta IDE、KDevelop IDE 上设置 Ogre 应用程序项目的指南。

- **www.ogre3d.org/phpBB2addons/viewtopic.php?t=3293**  
  OgreAL 下载和安装说明。

- **developer.creative.com/landing.asp?cat=1&sbc_at=31&top=38**  
  OpenAL 下载和安装链接。

- **www.openal.org/downloads.html**  
  OpenAL 下载页面。

- **www.wreckedgames.com/wiki/index.php/WreckedLibs:OIS**  
  面向对象输入系统（OIS）wiki 页面包含 OIS 手册和 API 参考的链接。

- **www.tayloredmktg.com/rgb/**  
  颜色代码图表。以十六进制和十进制给出 RGB 值。颜色分为一般颜色范围（例如灰色、蓝色、绿色、橙色）。

- **www.htmlcenter.com/tutorials/tutorials.cfm/89/General/**  
  颜色图表给出 RGB 和十六进制颜色值。

### 教程

- **www.ogre3d.org/wiki/index.php/Ogre_Tutorials**  
  Ogre 教程页面。教程从基础到高级，主题包括 Ogre 入门、FrameListener、动画、多个 SceneManager 和内容创建。

- **www.blender.org/tutorials-help/**  
  Blender 教程页面。

- **en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro**  
  “Blender 3D: Noob to Pro”维基教科书引导新 Blender 用户完成 3D 建模过程。教你如何使用模型、光照、渲染、动画、粒子和软体。还有关于 Python 脚本和高级动画的高级教程。

- **www.cegui.org.uk/wiki/index.php/Tutorials**  
  许多关于使用 Crazy Eddie 的 GUI 系统（CEGUI）的教程，Ogre 支持该系统。

### 工具

- **www.ogre3d.org/index.php?option=com_content&task=view&id=413&Itemid=133**  
  下载适用于 Blender、Maya、Softimage XSI 和 3DS Max 的模型导出工具。

- **usa.autodesk.com/adsk/servlet/index?siteID=123112&id=7639525**  
  Autodesk Maya Personal Learning Edition 页面。Maya 的免费版本。

- **www.softimage.com/downloads/default.aspx**  
  SoftImage XSI 下载页面。提供免费 30 天试用版。

