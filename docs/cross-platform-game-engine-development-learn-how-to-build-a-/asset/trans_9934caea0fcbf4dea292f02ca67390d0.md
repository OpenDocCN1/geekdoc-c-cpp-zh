

```bash
#!/bin/bash

# check build dir
if [ ! -d build ]
then
    mkdir build
fi

# generate cmake files
cmake -S . -B ./build -DCMAKE_BUILD_TYPE=Debug -DBUILD_SHARED_LIBS=ON

# copy assets files to output dir
cp -R "./resource" "./build/bin/assets"

# compile project
cd build && cmake --build .
echo compilation finished!
```

Shell 脚本是由系统 shell 解释和执行的计算机程序。归根结底，它是一个可执行的文本文件，可以执行用户在命令行界面（例如 Windows 的命令提示符）中可以输入的任何命令。Shell 本身就是一种编程语言，包含变量、循环和决策结构。

要使 **build-linux.sh** 文件在 Linux 机器上可执行，还需要执行一步操作。右键单击该文件并打开 **属性选项卡**。

![](img/2763810ed0a1572c2bec59ee52dd75be_34_0.png)

在权限部分，确保启用以下选项：**允许将文件作为程序执行**，如下图所示。

![](img/2763810ed0a1572c2bec59ee52dd75be_34_1.png)

你也可以直接在脚本文件所在位置运行以下命令：

```bash
sudo chmod +x build-linux.sh
```

两个脚本都会检查项目根目录下是否存在 build 文件夹，如果不存在则创建一个。然后 CMake 将生成当前平台构建项目所需的所有文件。

由于我们将使用音频、纹理和字体等资源，因此希望将 resource 文件夹的内容复制到构建项目的输出文件夹中。

此外，win-build.bat 会确保从 windows/bin 文件夹复制所需的所有 .dll 库文件到输出文件夹中。CMake 将使用之前章节中安装的平台特定编译器继续编译项目。

CMake 需要知道根 CMakeLists.txt 文件的位置，以便为当前平台生成项目文件。这就是为什么我们需要使用 [-S <path to file>] 将该信息作为参数传递给 CMake。

[-B <output dir>] 用于告诉 CMake 将所有生成的构建文件存储在哪里。

符号 BUILD_SHARED_LIBS 用于强制编译器将项目中的所有库构建为共享库，而不是静态库。

## CMakeLists.txt 文件

CMake 可以通过合并各个位置的多个 CMakeLists.txt 文件来生成构建文件。在我们的项目文件树（图 16）中，你可以看到根文件夹以及 "engine" 和 "game" 文件夹中都有 CMakeLists.txt 文件。这些文件定义了 CMake 必须如何为我们的项目生成构建文件。

注意：这些文件必须命名为 "CMakeLists.txt"，因为 CMake 的工作原理如此。

CMake 会在所有目录中搜索该特定文件名，以在生成项目构建文件之前收集所有必要信息。让我们仔细看看每个 CMakeLists.txt 文件。

- Project/CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.16)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)
set(CMAKE_CXX_STANDARD 17)

project(fuse2d)

# output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# add engine and game
add_subdirectory(engine)
add_subdirectory(game)
```

上面描述的 CMakeLists.txt 文件位于项目根目录中。如你所见，我们首先提供允许的 CMake 最低版本（3.16 版）。这一点很重要，因为一些旧版本的 CMake 行为不同。我们还想声明将使用的 C++ 标准版本。在此场景中为 C++17。然后我们创建一个名为 "fuse2d" 的项目（解决方案或工作区），这是我们为游戏引擎取的名称。你可以选择任何喜欢的名称。

我们希望 CMake 将所有生成的构建文件保存在特定目录中，因此使用内置宏 CMAKE_BINARY_DIR，即当前 CMake 构建树顶层的完整路径，基本上就是项目根目录的路径。

最后，我们使用函数“add_subdirectory”将引擎和游戏项目添加到工作区中，以便在 CMake 构建项目之前将它们全部合并。

这就是根 CMakeLists.txt 需要做的全部内容。让我们对引擎 CMakeLists.txt 文件做同样的操作。

- Project/engine/CMakeLists.txt

```cmake
# engine project (shared lib)
project(engine VERSION 0.0.1)

# get all cpp-files
file(GLOB_RECURSE SRC_FILES src/*.cpp CMAKE_CONFIGURE_DEPENDS)
add_library(${PROJECT_NAME} ${SRC_FILES})

# define symbols
add_definitions(-DFUSE_EXPORT)
add_definitions(-D_DEBUG)

# windows platform
if (WIN32)
	target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/windows/includes)
	target_link_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/windows/libs)
endif (WIN32)

# linux platform
if (UNIX)

endif (UNIX)

# precompile headers
target_precompile_headers(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src/pch.h)

# add include directory
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
```

如上所述，引擎的 CMakeLists.txt 文件位于 "Project/engine" 文件夹中。如你所见，我们不需要在此处定义 CMake 版本和 C++ 标准版本，因为它们已在根 CMakeLists.txt 文件中定义。我们只需创建一个名为“engine”的项目，版本号为“0.0.1”。版本号的指定是可选的。

然后我们希望递归搜索引擎项目源文件夹（engine/src）中的所有 .cpp 文件，因为它们都将被编译以生成引擎库。

CMake 允许我们定义符号，这些符号可以影响代码的编译方式。在此场景中，我们定义了 _DEBUG 和 FUSE_EXPORT。_DEBUG 宏指示编译器生成调试数据。FUSE_EXPORT 将用于指示编译器将引擎的哪些模块导出到库中（稍后详细介绍）。我们还希望确保 CMake 知道引擎将使用的外部库在 Windows 上的位置，这就是为什么我们使用 if(WIN32) 语句来检查当前使用的平台是否为 Windows。稍后你会明白为什么不需要为 Linux 做此操作。

预编译头（PCH）是已编译为中间形式的头文件（C/C++），编译器可以更快地解析它。预编译头可以显著减少编译时间，尤其是对于大型头文件、包含许多其他头文件的头文件，或在许多翻译单元中包含的头文件。CMake 通过函数 target_precompile_headers() 让我们能够将预编译头添加到项目中。

在“engine”文件夹中有一个名为“pch.h”的文件，它是引擎库的预编译头。它将用于包含所有重要的 C++ 标准库以及其他将全局可访问的自定义代码。这将显著减少编译引擎库所需的时间。

注意：使用预编译头的唯一要求是，我们必须在引擎的所有 .cpp 文件中包含 pch.h 头文件。

我们调用函数“target_include_directories”来附加所有包含目录，以便编译器在编译过程中知道包含哪些头文件。

我们将讨论的最后一个 CMakeLists.txt 文件是位于“game”中的文件。

- Project/game/CMakeLists.txt

```cmake
# runtime project (.exe)
project(game VERSION 0.0.1)

# get all cpp-files
file(GLOB_RECURSE SRC_FILES src/*.cpp CMAKE_CONFIGURE_DEPENDS)
add_executable(${PROJECT_NAME} ${SRC_FILES})

# link libraries
target_link_libraries(${PROJECT_NAME} engine)

# includes directories
include_directories(${CMAKE_SOURCE_DIR}/engine/src)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
```

上面的代码展示了游戏可执行文件的 **CMakeLists.txt** 文件是如何定义的。需要注意的是，我们将引擎作为库进行链接，并且还将其源目录作为包含目录，以便游戏项目也可以访问引擎库中的代码。

在首次编译代码之前，我们必须安装一些库，以便为游戏引擎添加一些功能。

