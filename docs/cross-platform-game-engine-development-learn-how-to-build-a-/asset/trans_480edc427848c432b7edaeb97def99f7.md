

## 设置 SDL2 库

简单直接媒体层（SDL）是一个跨平台开发库，旨在通过 OpenGL 和 Direct3D 为音频、键盘、鼠标、操纵杆和图形硬件提供低级访问。它被视频播放软件、模拟器以及包括 Valve 的获奖游戏目录和许多 Humble Bundle 游戏在内的热门游戏所使用。

SDL 官方支持 Windows、Mac OS X、Linux、iOS 和 Android。其他平台的支持可以在源代码中找到。SDL 使用 C 编写，原生支持 C++，并且有多种其他语言的绑定可用，包括 C# 和 Python。SDL 2.0 在 zlib 许可证下分发。该许可证允许您在任何软件中免费使用 SDL。[18]

## 在 Windows 上安装 SDL

在 Windows 上安装 SDL 就像将文件复制粘贴到正确位置一样简单。但是，我们必须谨慎行事，因为这往往是项目无法成功编译的根本原因。

- 步骤 1：下载

https://www.libsdl.org/download-2.0.php 是 SDL 官方下载页面的链接。我们可以下载 SDL 的源代码并自行编译，但我们不想让事情变得更复杂。我们将只需下载并链接已构建的二进制文件到我们的项目中。

![](img/2763810ed0a1572c2bec59ee52dd75be_40_0.png)

根据所使用的编译器，Windows 上有两个版本的开发库可用。有一个 Visual C++ 编译器版本和一个 MinGW 编译器版本。我们之前安装了 Microsoft Visual C++ 编译器工具集。这就是为什么我们将下载 Visual C++ 版本。

- 步骤 2：解压

使用 WinRAR、Zip 或您选择的任何其他包管理器解压下载的包。在解压后的目录中，有两个主要子目录：“include”和“lib”。所有头文件都在 include 文件夹中，库的二进制文件位于 lib 文件夹中。SDL 分别在 x86 和 x64 文件夹下提供 32 位和 64 位版本。使用 32 位或 64 位版本不会影响我们的编码体验；只有最终产品会有所不同。使用 32 位允许您在 32 位和 64 位系统上运行最终软件，但反之则不然。本书将使用 64 位版本。

```
SDL2-2.x.x
|--- lib
|    |--- x86 <--- 32-bit binaries
|    |--- x64 <--- 64-bit binaries
|--- include
```

- 步骤 3：复制

将 SDL2-2.x.x/include/ 中的所有头文件复制到您项目的 Project/windows/includes/SDL2/ 文件夹中。

将以下 .lib 文件 SDL2.lib、SDL2main.lib 从 SDL2-2.x.x/lib/x64 复制到您的 Project/windows/libs 文件夹中。

还要确保将 SDL2.dll 文件从 SDL2-2.x.x/lib/x64 复制到文件夹：Project/windows/bin。

我们现在已正式安装好 SDL2 并可供使用，但我们仍需将其链接到项目中。但在进行此操作之前，我们将首先安装所有 SDL 扩展库。

- 步骤 4：安装 SDL_image、SDL_ttf、SDL_mixer

仅 SDL2 不足以让我们在游戏引擎中实现前面提到的所有功能。这就是为什么我们还将使用 SDL 的其他扩展库：SDL_image、SDL_mixer 和 SDL_ttf。

- SDL_image

SDL_image [12] 是一个图像文件加载库。它将图像加载为 SDL 表面和纹理，并支持以下格式：BMP、GIF、JPEG、LBM、PCX、PNG、PNM、SVG、TGA、TIFF、WEBP、XCF、XPM、XV。在此处下载：https://www.libsdl.org/projects/SDL_image/ 。

![](img/2763810ed0a1572c2bec59ee52dd75be_41_0.png)

- SDL_mixer

SDL_mixer [13] 是一个简单的多声道音频混音库。它支持任意数量的同时播放的 16 位立体声音频声道，加上单声道音乐，由流行的 FLAC、MikMod Mod MOD、Timidity MIDI、Ogg Vorbis 和 SMPEG MP3 库混合：https://www.libsdl.org/projects/SDL_mixer/.

### Windows
SDL2_mixer-devel-2.0.4-VC.zip (Visual C++ 32/64-bit)
SDL2_mixer-devel-2.0.4-mingw.tar.gz (MinGW 32/64-bit)

- SDL_ttf

SDL_ttf [14] 是一个示例库，允许您在 SDL 应用程序中使用 TrueType 字体。它附带一个示例程序 "showfont"，用于显示给定 TrueType 字体文件的示例字符串。使用以下链接下载：https://www.libsdl.org/projects/SDL_ttf/.

### Windows
SDL2_ttf-devel-2.0.15-VC.zip (Visual C++ 32/64-bit)
SDL2_ttf-devel-2.0.15-mingw.tar.gz (MinGW 32/64-bit)

请确保将每个扩展库的头文件复制到 project/windows/includes/SDL2 目录中，就像我们之前为 SDL 做的那样。您需要分别为每个库的所有 .lib 和 .dll 文件重复相同的过程。

- 步骤 5：链接到项目

既然所有文件都已下载并复制到各自的目录中，我们所要做的就是将它们链接到项目中。

按照以下代码更新引擎的 CMakeLists.txt 文件。

- Project/engine/CMakeLists.txt

```
# . . .

# windows platform
if ( WIN32)
    target_link_libraries(${PROJECT_NAME} SDL2 SDL2main SDL2_image
SDL2_ttf SDL2_mixer)
    target_include_directories(${PROJECT_NAME} PUBLIC C
${CMAKE_SOURCE_DIR}/windows/includes)
    target_link_directories(${PROJECT_NAME} PUBLIC C
${CMAKE_SOURCE_DIR}/windows/libs)
endif ( WIN32)

# . . .
```

如您所见，我们使用函数“target_link_libraries”来指定要链接到项目的哪个库。SDL2、SDL2main、SDL2_image、SDL2_ttf 和 SDL2_mixer 均已链接到我们的引擎。
在 Windows 上将 SDL 库链接到项目就这些。现在让我们在 Linux 上做同样的事情。

## 在 Linux 上安装 SDL

以下安装说明仅适用于基于 Debian/Ubuntu 64 位的发行版。

注意：您需要 root 权限才能安装本节中的所有软件包。

- 步骤 1：更新包管理器

旧版本的包管理器可能不支持当前版本的 SDL2，请确保使用以下命令升级到最新版本。
sudo apt-get update

- 步骤 2：查找当前 SDL 版本

以下命令将搜索我们要安装的当前 SDL2 版本的 apt-get 缓存。
sudo apt-cache search libsdl2

- 步骤 3：下载 SDL2 开发版

libsdl2-dev 是 SDL2 的开发软件包。您可以使用以下命令在系统上安装该软件包。
sudo apt-get install libsdl2-dev

您可以通过导航到以下目录来查看它在系统上的安装位置：“/usr/include/SDL2” 用于头文件，“/usr/lib/x86_64-linux-gnu” 用于二进制文件。

就这样，我们在系统上安装了 SDL2，我们需要做的就是将其链接到项目。但我们也想为 SDL_image、SDL_ttf 和 SDL_mixer 重复此过程。

- 步骤 4：安装 SDL_image、SDL_ttf 和 SDL_mixer

这部分有点棘手，因为我们需要手动创建一些文件来指示 CMake 关于在哪里找到每个扩展库。使用以下命令在系统上安装每个库。这些命令还将把这些库安装在与 SDL2 相同的位置。

```
sudo apt-get install libsdl2-image-dev
sudo apt-get install libsdl2-mixer-dev
sudo apt-get install libsdl2-ttf-dev
```

安装完成后，我们需要为上面安装的每个库创建一个“.cmake”配置文件。这些文件将由 CMake 用于定位库文件。在某些情况下，上述命令会自动为每个库创建所有“.cmake”配置文件，但我们想考虑最坏的情况。那么，让我们看看如何做到这一点。

- SDL_image (sdl2_image-config.cmake)

使用此命令为 SDL_image 创建并打开一个新的“.cmake”文件。

```
cd /usr/x86_64-linux-gnu/cmake/
mkdir sdl2_image
cd sdl2_image
sudo nano sdl2_image-config.cmake
```

将以下代码复制到上面创建的文件中，并使用 Ctrl-X 保存。

```
set(prefix "/usr")
set(exec_prefix "${prefix}")
set(libdir "${prefix}/lib/x86_64-linux-gnu")
set(SDL2_IMAGE_PREFIX_I "/usr")
set(SDL2_IMAGE_EXEC_PREFIX_I "/usr")
set(SDL2_IMAGE_INCLUDE_DIRS "${prefix}/include/SDL2")
set(SDL2_IMAGE_LIBRARIES "-lSDL2_image")
```

- SDL_mixer (sdl2_mixer-config.cmake)

使用以下命令为 SDL_mixer 创建“.cmake”文件。

