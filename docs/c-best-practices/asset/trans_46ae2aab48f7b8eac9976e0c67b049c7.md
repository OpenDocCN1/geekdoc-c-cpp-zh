
## 46. 使用工具：多个编译器

在你的平台上支持*至少* 2 个编译器。每个编译器执行不同的分析，并以略有不同的方式实现标准。

如果你使用 Visual Studio，应该能够相对容易地在 clang 和 cl.exe 之间切换。你也可以使用 WSL 并启用远程 Linux 构建。

如果你使用 Linux，应该能够轻松地在 GCC 和 Clang 之间切换。

在 MacOS 上，请确保你使用的编译器是你所认为的那个。gcc 命令很可能是 Apple 安装的 clang 的符号链接。

要在你的平台上安装更新或不同的编译器，可以使用以下内容：

Ubuntu / Debian

- GCC - Toolchain PPA¹
- Clang - apt 软件包²

Windows

- GCC MinGW³
- Clang 官方下载⁴

MacOS

- Homebrew / MacPorts

¹ https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/ppa
² https://apt.llvm.org/
³ https://mingw.org/
⁴ https://releases.llvm.org/download.html

### 练习：添加另一个编译器

既然你已经为你的系统启用了持续构建，现在是时候添加另一个编译器了。

使用你当前所需编译器的新版本总是一个好主意。但如果你只支持 GCC，考虑添加 Clang。或者如果你只支持 Clang，添加 GCC。如果你在 Windows 上，在 MSVC 之外添加 MinGW 或 Clang。

### 练习：添加另一个操作系统

希望你的项目至少有一部分可以移植到另一个操作系统。让项目的部分内容在另一个操作系统和工具链上编译的练习，将教会你很多关于代码本质的东西。

### 资源

- C++Now 2015：Jason Turner “Thinking Portable: How and Why to make your C++ Cross Platform”^5

^5 https://youtu.be/cb3WIL96N-o

## 47. 模糊测试与变异测试

你的想象力限制了你所能创建的测试。你在调用 API 时是否尝试过恶意行为？你是否故意向输入传递格式错误的数据？你是否处理来自未知或不可信来源的输入？

生成所有可能的函数调用的所有可能输入的所有可能组合是不可能的。幸运的是，已有工具可以解决这个问题。

### 模糊测试

模糊测试器会生成各种长度的随机数据字符串。你编写的测试框架会消费这些数据字符串，并以适合你的应用程序的某种方式处理它们。模糊测试器会分析测试执行生成的覆盖率数据，并利用该信息删除冗余测试，生成新的、新颖且独特的测试。

理论上，如果运行足够长时间，模糊测试最终会达到被测代码 100% 的代码覆盖率。与 AddressSanitizer 结合使用时，这将成为发现代码中 bug 的强大工具。[2015 年的一篇有趣文章](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html)描述了模糊测试器与 AddressSanitizer 的组合如何能在不到 6 小时内发现 OpenSSL 中的安全漏洞“heartbleed”。

![](img/60cb742bacdfc38724280b0dae4597e3_113_0.png)

模糊测试主要发现内存和安全缺陷。

存在许多不同的模糊测试工具。出于本节的目的，我将只介绍 [LLVM 的 libFuzzer](https://llvm.org/docs/LibFuzzer.html)。所有模糊测试器都基于相同的前提运行。

你必须提供某种入口点。入口点通常采用如下函数的形式：

```cpp
// tested in a real test
auto [newDataPtr, remainingSize, Obj1]
  = createStruct<Type1>(Data, Size);
auto [lastDataPtr, lastSize, Obj2]
  = createStruct<Type2>(newDataPtr, remainingSize);

functionToTest(Obj1, Obj2);
}
```

¹ https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html
² https://www.llvm.org/docs/LibFuzzer.html

模糊测试器将很快了解到，任何 Size > sizeof(Type1) + sizeof(Type1) 的新数据输入都不会生成新的代码路径，并会将重点放在适当数量的数据上。

### 变异测试

变异测试通过修改被测代码中的条件语句和常量来工作。

*伪代码示例。*

```cpp
bool greaterThanFive(const int value) {
    return value > 5; // comparison
}

void tests() {
    assert(greaterThanFive(6));
    assert(!greaterThanFive(4));
}
```

变异测试器可以修改常量 5 或 >，因此结果代码可能变成

*变异后的代码。*

```cpp
bool greaterThanFive(const int value) {
    return value < 5; // mutated
}
```

任何继续通过的测试都是“存活下来的变异体”，表明测试有缺陷或代码中有 bug。

### 练习：创建模糊测试框架。

应用此处演示的示例，为你的代码创建模糊测试器。你会遇到哪些挑战？

查看 FuzzedDataProvider.h³ 以获取更多辅助函数

### 练习：研究变异测试。

本书作者没有变异测试的直接经验。它是否可用于你的项目？你找到了哪些有趣的资源？

### 资源

- C++Now 2018：Marshall Clow “Making Your Library More Reliable with Fuzzing”⁴
- C++ Weekly 第 85 集：模糊测试⁵
- CppCast：Alex Denisov “Mutation Testing With Mull”⁶
- NDC TechTown 2019：Seph De Busser “Testing The Tests: Mutation Testing for C++”⁷
- CppCon 2017：Kostya Serebryany “Fuzz or lose…”⁸
- CppCon 2020：Barnabás Bágyi “Fuzzing Class Interfaces for Generating and Running Tests with libFuzzer”⁹ - 关于以新颖方式使用模糊测试的启发式演讲。视频尚未在 YouTube 上发布，但本书出版后可以查找。
- Autotest¹⁰ - 与“Fuzzing Class Interfaces for Generating and Running Tests with libFuzzer”演讲相关的库。

⁵ https://youtu.be/gOOKBoqKoOU
⁶ https://cppcast.com/alex-denisov/
⁷ https://youtu.be/M-5_M8qZXaE
⁸ https://youtu.be/k-Cv8Q3zWNQ
⁹ https://cppcon2020.sched.com/event/e7An/fuzzing-class-interfaces-for-generating-and-running-tests-with-libfuzzer?iframe=no
¹⁰ https://gitlab.com/wilzegers/autotest/

这些会议和用户组中的许多现在都在线上聚会。现在我们可以参加彼此的用户组。例如，[北丹佛都会区 C++ Meetup](https://www.meetup.com/North-Denver-Metro-C-Meetup/)^4^ 每月定期有一位来自泰国的参会者。

^4^ https://www.meetup.com/North-Denver-Metro-C-Meetup/

### C++ Weekly

本书通篇引用 C++ Weekly 作为资源，以便回顾更多信息和示例并与同事分享。目前，该节目已连续播出 235 周，包含许多特别版、附加内容和直播。

### cppreference.com

这个网站非常棒，但你可能不知道你可以创建一个账户，并将内容定制为你正在使用的 C++ 版本。此外，你还可以[执行示例](https://en.cppreference.com/w/Cppreference)并[下载离线版本](https://en.cppreference.com/w/Cppreference)^5^

^5^ https://en.cppreference.com/w/Cppreference

### 聘请培训师到贵公司现场培训

团队培训能让你的团队以新方向思考，提升士气，并提高员工留存率。既然你已经读到这里，我将为你提供一张优惠券。

如果你提及本书，就可以从我这里获得贵公司现场培训费用 10% 的折扣。（差旅费用不打折）。希望旅行限制不会持续太久。

### YouTube

- Andreas Fertig 的频道⁶
- C++ Weekly（作者频道）⁷
- CopperSpice⁸

⁶ https://www.youtube.com/channel/UCxJfSPGHFS3_nRDv1u-Q8g
⁷ https://www.youtube.com/c/JasonTurner-lefticus
⁸ https://www.youtube.com/copperspice

## 49. 感谢

### 赞助者

感谢我所有的 Book Supporter 赞助者！

### 当前

- Adam Albright
- Adam P Shield
- Alexander Roper
- Andrei Sebastian Cîmpean
- Anton Smyk
- Arman Imani
- Björn Fahller
- Clint Rajaniemi
- Corentin Gay
- David C Black
- Dennis Börm
- Fedor Alekseev
- Florian Sommer
- Gwendolyn Hunt
- Jack Glass
- Jaewon Jung
- Jeff Bakst
- Kacper Kołodziej
- Lars Ove Larsen
- Magnus Westin
- Martin Hammerchmidt
- Matt Godbolt
- Matthew Guidry

