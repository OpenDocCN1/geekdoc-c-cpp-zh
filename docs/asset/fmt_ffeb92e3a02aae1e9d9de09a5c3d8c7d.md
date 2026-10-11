
- C++ Weekly Ep 178: C++14 的重要部分（9分钟）⁴

- C++ Weekly Ep 190: C++17 的重要部分（10分钟）⁵

²https://youtu.be/T8Y_LZPVR

³https://youtube.be/D5n6xUKU

⁴https://youtube.be/mXxvaEdNH

⁵https://youtube.be/QpFJOlz1r

## 42. 不要对简单类型使用 initializer_list

“初始化列表（Initializer List）”是 C++ 中的一个加载术语。“初始化列表”用于直接初始化值。`initializer_list` 用于将值列表传递给函数或构造函数。

## 练习：理解开销

使用 Andreas Fertig 的 `cppinsights.io`¹ 来理解这两个示例的作用。使用 `shared_ptr` 的 `initializer_list` 构造函数。

```cpp
#include <vector>
#include <memory>

std::vector<std::shared_ptr<int>> vec{
    std::make_shared<int>(4), std::make_shared<int>(2)
};
```

不要对简单类型使用 `initializer_list`

使用 `shared_ptr` 的 `array` 构造。

```cpp
#include <array>
#include <memory>
```

```cpp
std::array<std::shared_ptr<int>, 2> data{
    std::make_shared<int>(4), std::make_shared<int>(2)
};
```

并解释区别。如果你能做到这一点，你比大多数 C++ 开发者懂得多。

## 练习：理解为什么不编译

使用 `unique_ptr` 的 `initializer_list` 构造。

```cpp
#include <vector>
#include <memory>
```

```cpp
std::vector<std::unique_ptr<int>> data{
    std::make_unique<int>(4), std::make_unique<int>(2)
};
```

## Resources

- C++ Now 2018: Jason Turner “初始化列表坏了，让我们修复它们”²（深入探讨这些主题的问题）

- C++ Insights³

²https://youtu.be/sSlmmMMFX

³https://cppinsights.io/

## 43. 使用工具：构建生成器

- `CMake`¹

- `Meson`²

- `Bazel`³

- 其他⁴

原始的 `make` 文件或 Visual Studio 项目会让实现上述任何内容都变得过于复杂。使用构建工具来帮助维护跨平台和编译器的移植性。

将你的构建脚本像其他代码一样对待。它们有自己的最佳实践，编写不可维护的构建脚本和编写不可维护的 C++ 一样容易。

构建生成器还通过 `cmake --build` 等工具抽象并简化了持续构建环境，无论使用什么平台，都能执行正确的操作。

> ¹https://cmake.org

²https://mesonbuild.com/

³https://bazel.build/

⁴https://github.com/lefticus/cpppractices/blob/master/02-Use_the_Tools_Available.md

## 练习：调查你的构建系统。

- 你的项目目前使用构建生成器吗？

- 你的构建脚本有多旧了？

看看是否有你需要应用的当前最佳实践。是否有类似 `tidy` 的格式化工具可以运行在你的构建脚本上？

回顾书中之前的最佳实践，看它们如何适用于你的构建脚本。

- 你是否在重复自己？

- 是否有更高级的抽象？

> 最近版本的 `CMake` 添加了如 `--profiling-output` 等工具，帮助你查看生成器花时间在的地方。

## Resources

- Professional CMake: A Practical Guide⁵

- `cmake-tidy`⁶

- C++ Now 2017: Daniel Pfeiffer “Effective CMake”⁷

- CopCon 2017: Mathieu Roper “Using Modern CMake”⁸

⁵https://crascit.com/professional-cmake

⁶https://github.com/MaciejPatro/cmake-tidy

⁷https://youtube.be/bsXLMQg

⁸https://youtube.be/eC9-iRN2

## 使用工具：构建生成器

- CppCon 2018: Jussi Pakkanen “使用 Meson 构建系统轻松编译百万行代码”⁹

- Bazel 2019¹⁰

- CppCon 2019: Mathieu Rupert “Cato the Elder”¹¹ - 关于构建质量的吐槽

- C++ Weekly Ep 218 - Ultimate CMake 快速入门¹²

- 关于 CMake 的讨论¹³

> https://youtu.be/SCZLnopmY

¹⁰https://www.youtube.com/playlist?list=PLNXygaZ8Rsf7g43Z8

¹¹https://youtu.be/D07ILP4Km

¹²https://youtube.be/YbGH7yat-Jo

¹³https://twitter.com/Cor3nt/status/13109904491503206

## 44. 使用工具：包管理器

近年来对 C++ 包器的兴趣异常增长。这两个最受欢迎：

- `Vcpkg`¹

- `Conan`²

使用包管理器有明显的优势。包管理器有助于移植性并减少开发者的维护负担。

## 练习：你的依赖有哪些？

花时间清理项目的依赖项。将你的依赖与上述包管理器提供的进行对比。是否有包管理器包含了你所有的依赖？你现在的包过时了多久？你错过了哪些安全修复？

¹https://github.com/Microsoft/vcpkg

²https://conan.io/

## Resources

- Unity 编译指南¹

- 使用 Meson 进行 Unity 编译²

- 使用 CMake 进行 Unity 编译³

- 使用 Meson 使用 PCH（预编译头）⁴

- 使用 CMake 使用 PCH⁵

- `ccache`⁶

- CMake 编译器启动器⁷

- Clang 构建分析器⁸

- C++ Build Insights 入门⁹

- 介绍使用 `vcperf/timetrace` 进行 C++ 编译时间分析¹⁰

¹https://onqtam.com/programming/2018-07-07-unity-builds/

²https://mesonbuild.com/Unity-builds.html

³https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD.html

⁴https://mesonbuild.com/Precompiled-headers.html

⁵https://cmake.org/cmake/help/latest/command/target_precompile_headers.html

⁶https://ccache.dev/

⁷https://cmake.org/cmake/help/latest/prop_tgt/LANG_COMPILER_LAUNCHER.html?highlight=ccache

⁸https://github.com/aras-p/ClangBuildAnalyzer

⁹https://docs.microsoft.com/en-us/cpp/build-insights/get-started-with-cpp-build-insights?view=vs-2019

¹⁰https://devblogs.microsoft.com/cppblog/introducing-vcperf-timetrace-for-cpp-build-time-analysis/

## 46. 使用工具：多个编译器

在你的平台上支持*至少 2 个* 编译器。每个编译器都执行不同的分析，并以略不同的方式实现标准。

如果你使用 Visual Studio，你应该能够相对容易地在 `clang` 和 `cl.exe` 之间切换。你也可以使用 `WSL` 并启用远程 Linux 构建。

如果你使用 Linux，你应该能够在 `GCC` 和 `Clang` 之间进行切换。

> 在 MacOS 上，请确保你正在使用的编译器确实是你认为的那个一个。`gcc` 命令很可能是指向 Apple 安装的 `clang` 的软链接。

要在你的平台上安装较新版本或不同的编译器，可以使用以下方法：

Ubuntu / Debian

- `GCC`¹

Windows

- `GCC MinGW`²

- `Clang` 官方下载³

MacOS

- Homebrew / MacPorts⁴

¹https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/ppa

²https://apt.llvm.org/

³http://mingw.org/

⁴https://releases.llvm.org/download.html

## 练习：添加另一个编译器

由于你已经开启了系统的持续构建，现在是时候添加另一个编译器了。

你当前所需的编译器的新版本总是一个好主意。但如果你只支持 `GCC`，请考虑添加 `Clang`。如果你只支持 `Clang`，考虑添加 `GCC`。如果你在 Windows 上，除了 `MSVC` 之外，再添加 `MinGW` 或 `Clang`。

## 练习：添加另一个操作系统

希望你的项目至少有一部分可以移植到另一个操作系统。让项目的部分代码在另一个操作系统和工具链上编译的练习将让你学到很多关于代码本质的知识。

## Resources

- C++ Now 2015: Jason Turner "思考移植性：如何以及为什么要让你的 C++ 跨平台"⁵

⁵https://youtu.be/cb3WIL96N-o

## 47. 模糊测试 (Fuzzing) 与变异 (Mutating)

你的想象力限制了你所创建的测试。当你调用 API 时会尝试进行恶意操作吗？你会故意向输入传递格式错误的数据吗？你会处理来自未知或不可信源的输入吗？

要为所有组合下的所有函数调用生成所有可能的输入是不可能的。幸运的是，存在工具可以解决这个问题。

### 模糊测试 (Fuzzing)

模糊测试器生成各种长度的随机数据字符串。你编写的测试框架（test harness）消耗这些数据字符串，并以适用于应用程序的方式进行处理。模糊测试器分析由测试执行生成的覆盖率数据，并利用这些信息移除冗余测试并生成新的独特测试。

从理论上说，如果运行足够的时间，模糊测试最终将达到测试代码的100% 覆盖率。结合 `AddressSanitizer`，这使其成为寻找你代码中 bug 的强大工具。2015年的一篇有趣文章描述了模糊测试和 `AddressSanitizer` 的结合如何在少于6 小时内发现 OpenSSL 中的安全漏洞“heartbeat”。

> 模糊测试主要发现内存和安全漏洞。

存在许多不同的模糊测试工具。为了本节内容，我将仅涵盖 LLVM 的 `libFuzzer`。所有的模糊测试器都在相同的前提下运行。

¹https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html

²https://www.llvm.org/docs/LibFuzzer.html

你必须提供某种入口点。入口点通常采用如下函数的形式：

libFuzzer 入口点。

```
extern "C" int LLVMFuzzerTestOneInput(const uint8_t *Data, size_t Size);
```

`Data` 指针始终有效，且 `Size` 参数 >=0。

如果你的库仅仅解析输入文件（例如 `libpng`），那么你的工作就非常简单：

libFuzzer 数据正在使用。

```
extern "C" int LLVMFuzzerTestOneInput(const uint8_t *Data, size_t Size)
{
    parseInput(Data, Size);
}
```

如果你的函数接收的是数据结构而不是输入字符串，你的工作会稍微复杂，但是可行的。

高级 libFuzzer 使用。

```
template<typename Type>
std::pair<const uint8_t *, size_t, Type>
createStruct(const uint8_t *Data, size_t Size)
{
    // 我们只允许对平凡类型执行操作
    static_assert(std::is_trivial_v<Type>); // 默认初始化
    Type result{};
    const auto bytesToRead = std::min(sizeof(Type), Size);
    std::memcpy(&result, Data, bytesToRead);
    return {std::next(Data, bytesToRead), bytesToRead, result};
}
```

```
extern "C" int LLVMFuzzerTestOneInput(const uint8_t *Data, size_t Size)
{
    // 此示例旨在提供灵感，它尚未在
    // 实际的数据量下经过测试。
    // 模糊测试器会很快学会任何新的
    auto [newDataPtr, remainingSize, Obj1]
    = createStruct<Type1>(Data, Size);
    auto [lastData, lastSize, Obj2]
    = createStruct<Type2>(newDataPtr, remainingSize);

    functionToTest(Obj1, Obj2);
}
```

### 变异测试 (Mutating)

变异测试通过修改被测试代码中的条件和常量来工作。

伪代码。

```
bool greaterThanFive(int value) {
  return value > 5; // 
```

```
void tests() {
  assert(greaterThanFive(6));
  assert(!greaterThanFive(4));}
```

变异测试器可能会修改 5，导致代码变成：

```
bool greaterThanFive(int value) {
  return value < 5; // 
```

任何持续通过的测试都是“生存的变异”，可能表明测试有问题或代码存在 bug。

## 练习：创建一个模糊框架。

应用此处演示的示例为你的代码创建模糊测试。你遇到了哪些挑战？

- 查看 `FuzDataProvider.h`

## 练习：调查变异测试。

本书作者没有变异测试的直接经验。这是你可以在项目中使用的吗？你发现了什么有趣的资源？

## Resources

- C++ Now 2018: Marshall Clow "通过模糊测试让你的库更可靠"⁴

³https://github.com/llvm-mirror/compiler-rt/master/blob/include/fuzzer/FuzDataProvider.h

⁴https://youtube.be/LILJRHToyUk

- C++ Weekly Ep 85: Fuzz⁵

- CppCast: Alex Denisov “使用 Mull 进行变异测试”⁶

- NDC TechTown 2019: Seph De Busser “测试测试：C++ 的变异测试”⁷

- CppCon 2017: Kostya Serebryany “或是...”

- CppCon 2020: Barnabás Bágyi “使用 libFuzzer 生成和运行类接口测试”⁹ - 关于以新方式使用模糊测试的启发性演讲。视频尚未上线 YouTube，但请在本书出版后寻找。

- Autotest⁰ - 与“使用 libFuzzer 生成和运行类接口测试”演讲相关的库。

⁵https://youtube.be/g00KBqooU

⁶https://cppcast.com/alex-denisov/

⁷https://youtube.be/M-5_M8qZXa

⁸https://youtube.be/k-Cv8Q3zNWQ

⁹https://cppcon2020.sched.com/event/e7An/fuzzing-class-interfaces-for-generating-and-running-tests-with-libfuzzer?iframe=no

⁰https://gitlab.com/wilzegers/autotest/

# 48. 继续你的 C++ 教育

如果你想在你的领域变得更优秀，就必须不断学习，你有很多资源可以用来继续你的 C++ 教育。

## 了解如何提问

Kate Gregory 发表了一篇关于[如何提问的优秀文章](1)。一些关键点包括：

- 不要使用截图

- 使用良好的变量名

- 添加一些测试

- 听听人们在告诉你的什么

## 会议与本地用户小组

你附近几乎肯定有一个。查看[全球 ISO C++ 会议列表](2) 和 [Meeting C++ 用户小组列表](3)。

我是在全球 COVID-19 大流行期间完成这本书的写作的。因此，目前会议和用户小组大多以在线形式举行。但这为许多人提供了一个极佳的机会。
