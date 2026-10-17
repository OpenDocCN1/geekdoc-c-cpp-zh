
`00000000` `T_DoSomething`

`00000118` `S_DoSomething.ch`

`U__ZN0lsEPFRSoS_E`

`U__ZNSTios_base4Initv`

`U__ZNSTios_baseInitEv`

`U__ZStcout`

第二列中的字符指定符号类型，其中 `T` 指代在该库中定义的文本段（text section），而 `U` 指代被库引用但未定义的定义的符号。大写字母表示外部符号，而小写字母表示内部符号。第三列中的字符串提供了修饰后的符号名称（mangled symbol name）。可以使用 `c++filt` 命令进行反修饰，例如：

```
c++filt __ZNSTios_base4InitEv
```

```
std::ios_base::Init()
```

另一个命令是 `ldd`。它可以用于显示可执行文件所依赖的动态库列表。因为它将显示每个库的完整路径，无论操作系统是否找到了任何动态库。例如，对于一个简单的可执行文件会产生如下输出：

```
% ldd userapp
linux-so.2 => (0x77a000)
libstdc++.so.6 => /usr/lib/libstdc++.so.6 (0x764500)
libm.so.6 => /lib/x86_64/libm.so.6 (0x761f00)
libgcc_s.so.1 => /lib/libgcc_s.so.1 (0x760000)
libc.so.6 => /lib/x86_64/libc.so.6 (0x74bb00)
```

使用静态选项链接的可执行文件将不依赖于任何动态库。在 Linux 上对此类可执行文件运行 `ldd` 会得到如下输出：

```
% ldd userapp
not a dynamic
```

最后，如果你有一个静态库，可以将其转换为动态库（`.so`）。记住，静态归档（`.a`）只是对象文件（`.o`）的打包。因此，你可以使用 `ar` 命令提取单个对象文件，并将它们重新链接为动态库。例如：

```
ar -x libapi.a
g++ -shared -o libapi.so *.o
```

## A.5 在 Linux 上加载插件

在 Linux 上，你可以使用 `dlopen()` 函数将 `.so` 文件加载到当前进程中。然后你可以使用 `dlsym()` 访问该库中的符号。这让你能够创建如前文描述的插件接口。例如，考虑以下非常简单的插件接口：

```cpp
#ifndef PLUGIN_H
#define PLUGIN_H
#include <string>
extern "C"
void DoSomething(const std::string& name);
#endif
```

你可以为这个 API 构建一个动态库，例如 `libplugin.so`。接下来的代码演示了如何加载这个动态库并调用 `.so` 文件中的 `DoSomething()` 函数：

```cpp
typedef void (*FuncPtrT)(const std::string&);
const char *error;
// 打开动态库
void *handle = dlopen("libplugin.so", RTLD_LOCAL | RTLD_LAZY);
if (!handle) {
    std::cout << "Cannot load plugin!" << std::endl;
    exit(1);
}
dlerror();
// 从插件中获取 DoSomething() 函数
FuncPtrT fptr = (FuncPtrT) dlsym(handle, "DoSomething");
if ((error = dlsym(handle))) {
    std::cout << "Cannot find function in plugin: " << error;
    std::cout << std::endl;
    dlclose(handle);
    exit(1);
}
// 调用 DoSomething() 函数
(*fptr)("Hello There!");
// 关闭动态库
dlclose(handle);
```

```bash
g++ -dynamiclib -o libmy.so -fPIC file1.o file2.o file3.o \
-headerpad_max_install_names
```

此外，请注意 `-headerpad_max_install_names` 选项的使用。在 Mac 上构建动态库时，强烈建议使用此标志，我稍后会解释原因。
需要注意的是，Mac OS 上无法使用 `ld` 命令。相反，你可以使用 `otool` 来列出执行文件所依赖的动态库集合，即 `otool -L userapp`。

## A.4.3 Mac OS X 框架

Mac OS X 引入了框架（Framework）的概念，将编译和链接 API 所需的所有文件封装在一个包中。框架本质上是一个以 `.framework` 扩展的目录，其中可以包含动态库、头文件和参考文档等资源。它本质上是一个包（NSBundle 意义上的 bundle）。这种将所有必要的开发文件封装在一个包中的做法使得库的安装和卸载变得更加容易。此外，框架可以在同一个包中包含多个版本的库，以维护对旧应用程序的后兼容性。

下面的目录列表给出了框架包的布局示例，其中 `-` 符号符号链接。

```
+   MyAPI.framework/
Headers -> Versions/Current/Headers
MyAPI -> Versions/Current/MyAPI
Versions/
A/
Headers/
MyHeader.h
MyAPI
B/
Headers/
MyHeader.h
MyAPI
Current -> B
```

大多数 API 都以框架的形式分发，包括 Cocoa、Foundation 和 Core Services。如果你已经安装了 Mac OS X 开发环境，可以在 `/Developer/SDK` 目录下找到它们。因此，你可能希望将你的 API 分发为 Mac 框架，使其更像一个原生库。

你可以使用 Apple 的 Xcode 开发环境将 API 构建为框架。这可以通过选择 `File -> New Project`，然后在左侧面板中选择 `Framework`（见图 A.5）来实现。默认情况下，你可以选择将项目设置为使用 Carbon 或 Cocoa 框架。如果你不需要它们中的任何一个（即你正在编写纯 C++ 库），只需简单删除 Xcode 为你创建的这些框架即可。

![](img/170b148e5ba8f4b05aa8234f929ebba6_401_0.png)

**图 A.5**
使用 Apple 的 Xcode IDE 创建框架项目。

客户端可以通过向 `g++` 或 `ld` 提供 `-framework` 选项来链接你的框架。他们还可以指定 `-F` 选项来指定查找你框架包的目录。

## A.4.4 在运行时查找动态库

Linux 查找动态库的原理同样适用于 Mac OS 下的应用程序，但有细微差异。首先，用于管理库搜索路径的环境变量被称为 `DYLD_LIBRARY_PATH`，尽管较版本的 Mac OS 现在也支持 `LD_LIBRARY_PATH`。

此外，Mac OS 不支持 Linux 的 `-rpath` 链接器选项。相反，它提供了“安装名称”（install names）的概念。安装名称是固入 Mach-O 二进制文件的路径，用于指定搜索动态库的路径。在链接执行文件时，可以使用特殊字符串 `@executable_path` 来指定此路径。

你可以在构建动态库时指定安装名称，但你的客户端也可以使用 `install_name` 工具更改此路径。然而，他们不能指定比 `.dylib` 中原始路径更长的路径。在 Mac 上构建动态库时，使用 `-headerpad_max_install_names` 选项始终是建议的做法：让客户端能够灵活地将库的安装名称更改。

以下命令演示了客户端如何更改你库的安装名称以及更改其执行文件的安装名称：

```bash
install_name_tool -id @executable_path/../Libs/libmyapi.dylib \
libmyapi.dylib
```

```bash
install_name_tool -change libmyapi.dylib \
@executable_path/../Libs/libmyapi.dylib \
UserApp.app/Contents/MacOS/executable
```
