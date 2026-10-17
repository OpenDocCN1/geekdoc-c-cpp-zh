
# C++ 现代 CMake：轻松构建前沿技术

## 第1章：CMake 入门

![](img/e6336a3dbaf851248da5111d0f386cb1_0_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_0_1.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_1_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_1_1.png)

## 第2章：CMake 语言

```
message("hello" world)
name      arguments
```

```
argument\ent\1 arguments
a single argument three arguments
```

![](img/e6336a3dbaf851248da5111d0f386cb1_2_0.png)

## 第3章：在流行 IDE 中使用 CMake

![](img/e6336a3dbaf851248da5111d0f386cb1_3_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_3_1.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_4_0.png)

### Visual Studio 安装程序

Visual Studio Community 2022 - 17.8

负载

- 独立组件
- 语言包
- 安装位置
- 使用 C++ 的桌面开发
  - 使用你选择的工具（包括 MSVC、Clang、MSBuild）生成、运行和调试 Windows 应用程序
- 使用 C++ 的移动开发
  - 为 iOS、Android 或使用 C++ 构建跨平台应用程序
- 通用 Windows 平台开发
  - 使用 C#、VB 或 C++ 构建 Windows 平台应用程序

安装详细

- Visual Studio 核心编辑器
- ASPNET 和 Web 开发
- .NET 开发
- 使用 C++ 的桌面开发
  - C++ 核心功能
  - MSVC v143 - VS 2022 C++ x64/x86 生成工具...
  - 安全分析
  - 运行时调试器
  - Windows 的 C++ 工具
- Git 适配器

### 游戏 (2)

- 使用 C++ 的游戏开发
  - 使用 Unity 构建游戏，Unity 是一个强大的跨平台开发环境
- 使用 C++ 的游戏开发
  - 利用 C++ 的强大功能基于 DirectX、Unreal 或 Cocos2d 构建专业游戏

![](img/e6336a3dbaf851248da5111d0f386cb1_5_0.png)

### 其他工具 (5)

位置

`C:\Program Files\Microsoft Visual Studio\2022\Community`

这是你所选择的 Visual Studio 版本的位置。我们还提供通过 Visual Studio 安装其他功能的能力。如许可证通知或其附带许可证所述，该软件是单独许可的。继续操作即表示你同意这些条款。

![](img/e6336a3dbaf851248da5111d0f386cb1_5_1.png)

移除不再支持的组件

所需总空间：2.8 GB

下载时安装 关闭

## 第4章：建立你的第一个 CMake 项目

![](img/e6336a3dbaf851248da5111d0f386cb1_6_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_7_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_8_0.png)

## 第5章：与目标 (Targets) 操作

![](img/e6336a3dbaf851248da5111d0f386cb1_9_0.png)

```
digraph "BankApp" {
  node = "
  fontsize = 1;
  [
    node0 [label = "calculations", shape = octagon];
    node1 [label = "checksum", shape = box];
    node2 [label = "calculation", shape = egg];
    node3 [label = "node0", style = dotted];
    node4 [label = "drawing", shape = octagon];
    node5 [label = "node3", style = dotted];
    node6 [label = "node5", style = dotted];
    node7 [label = "terminal_app", shape = egg];
    node8 [label = "node0", style = dotted] // terminal_app -> calc
    node9 [label = "checksum" -> terminal_app];
  ];
  node1 -> "node4"
}
```

![](img/e6336a3dbaf851248da5111d0f386cb1_9_1.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_10_0.png)

## 第6章：使用生成器表达式 (Generator Expressions)

![](img/e6336a3dbaf851248da5111d0f386cb1_10_1.png)

## 第8章：链接可执行文件和库

![](img/e6336a3dbaf851248da5111d0f386cb1_11_0.png)

## Doxygen

主页 类 文件 搜索

### RandomNumberGeneratorMt19937 类引用

`RandomNumberGeneratorMt19937` 的继承图：

![](img/e6336a3dbaf851248da5111d0f386cb1_18_0.png)

`RandomNumberGeneratorMt19937` 的协作图：

![](img/e6336a3dbaf851248da5111d0f386cb1_18_1.png)

### 公有成员函数

`int Get() override`

该类的文档由以下文件生成：

- `src/rng_mt19937.h`
- `src/rng_mt19937.cpp`

由 doxygen 1.9.1 生成

### Calc 类引用

`#include <calc.h>`

### 公有成员函数

- `Calc(RandomNumberGenerator *mg)`
- `Set(int a, int b)`
- `Multiply(int a, int b)`
- `AddRandomNumber(int a, int b)`

### 详细描述

该类执行一些简单的计算

### 成员函数文档

- `AddRandomNumber()`
- `Calc::AddRandomNumber(int a, int b)`

将随机生成的数字添加到参数中

## 第14章：安装与打包

![](img/e6336a3dbaf851248da5111d0f386cb1_19_0.png)

## 第 15章：创建您的专业项目

![](img/e6336a3dbaf851248da5111d0f386cb1_20_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_21_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_22_0.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_22_1.png)
![](img/e6336a3dbaf851248da5111d0f386cb1_23_0.png)

## 第16章：编写 CMake Presets

![](img/e6336a3dbaf851248da5111d0f386cb1_24_0.png)
