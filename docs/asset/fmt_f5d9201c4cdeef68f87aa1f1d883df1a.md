
对于 `max2` 函数，参数在进入函数之前就会求值。因此，开销较大的 `sin()` 和 `cos()` 计算在之前完成。在 `max2` 中，只需要对简单的数值进行比较。

然而，`MAX2` 宏会展开为如下内容：

```cpp
double e = ((sin(3.141592/2)) > (cos(3.141592/2)) \
? (sin(3.141592/2)) : (cos(3.141592/2));
```

现在，`sin()` 和 `cos()` 是编译器无法预计算的复杂函数。编译器足够智能到能够避免执行两次 `sin()` 或 `cos()` 的概率极大。在这里，函数显然是更好的选择。

比单纯浪费时间更灾难的是，在展开参数时可能会获得的多次执行：

```cpp
// https://godbolt.org/zYYz3x1xzx
#include <iostream>
#define MAX(a,b) ((a) > (b) ? (a) : (b))
int main() {
    int x = 0;
    int y = 0;
    int z = MAX(++x, ++y); // // 参数被多次展开
    std::cout << "x:" << x << " y:" << y << " z:" << z << '\n';
}
```

这里的输出是什么？请注意，这是一个陷阱题！对我来说，输出是：

`x:1 y:2 z:2`

宏将表达式展开为 `((++x) > (++y) ? ((++x) : (++y))`。因此，`++y` 在比较中执行了一次，在结果中又执行了一次。你希望这样吗？绝对不，因为在同一个表达式中对同一个变量执行两个副作用操作符是未定义行为。所以，如果你看到不同的输出或程序崩溃，那是“允许”的。

## 21.6 宏的类型变异性

然而，`MAX2` 宏的实现相比 `max2` 函数有一个优势。你还可以将宏用于 `double` 以外的类型。由于宏是在调用处使用的，变量的类型在使用时确定。因此，`MAX2` 也适用于 `int` 甚至 `string`：

```cpp
// https://godbolt.org/z/ZrfvovaW
#include <string>
#include <cmath> // sin
```

不过，在 C++ 中通过重载可以更好地实现类型变异性。你可以为你使用的每个类型定义 `max2`：

```cpp
// https://godbolt.org/z/6zTx83zE
#include <string>
#include <cmath> // sin, cos
constexpr double max2(double a, double b) { return a > b ? a : b; }
constexpr int max2(int a, int b) { return a > b ? a : b; }
std::string max2(const std::string& a, const std::string& b) {
    return a > b ? a : b;
}
int main() {
    double e = max2(sin(3.14159/2), cos(3.14159/2));
    int i = max2(10+12+45, 100/5+20);
    std::string s = max2("Ernie", "Bert");
}
```

## 21.7 总结

为了清晰起见，表 21.1 再次列出了最重要的预处理器指令。我额外添加了一些简要说明。

| 指令 | 解释 |
| --- | --- |
| `#include` | 包含另一个文件 |
| `#define` | 定义标识符或宏 |
| `#undef` | 取消定义 |
| `#ifdef` | 检查预处理器标识符是否定义 |
| `#ifndef` | 检查预处理器标识符是否未定义 |
| `#elif` | 检查标识符是否定义 (C++23) |
| `#elifndef` | 检查标识符是否未定义 (C++23) |
| `#if` | 检查预处理器表达式 |
| `#else` | 对应一个预处理器 `#if` 的备选代码 |
| `#elif` | 备选代码和另一个检查 |
| `#endif` | 备选代码的结束 |
| 指令 | 解释 |
| --- | --- |
| `#line` | 为编译器错误信息设置当前行号和文件名 |
| `#error` | 带有错误消息并终止 |
| `#pragma` | 给编译器的特殊指令；高度依赖于编译器 |

**表 21.1** 可能的预处理器指令概述。

# 第 22 章 Telegram 章（接口）

- 带有 C 接口的 C 库

通常由第三方提供的扩展。

- `extern "C"`

标记一个函数使其能够被 C++ 程序使用。

- `void*` 或空指针

一种非类型安全的原始指针类型，所有原始指针类型都可以与它进行转换；通常是 C 接口的一部分。

- 自定义删除函数或自定义删除器

`shared_ptr` 的一个特性，对于释放 C 资源可能非常有用。

如果你正在编写一个使用第三方库的程序，那么这些库很有可能带有一个 C 接口。遗憾的是，C++ 的设计编写方式使得你完全可以包含为 C 语言编写的库。因此，你的选择并不是限制的。

受限制的是你对语言特性的选择。如果你想使用 C 库，你只能使用 C 语言元素。以下是你必须接受的限制详尽列表：

- 你没有类。结构体（Structures）只能包含某些元素；例如，省略了构造函数，且所有内容必须是公共的。为了简单起见，你应该只包含数据元素。

- 没有引用。你传递值或原始指针。

- C++ 标准库中的许多内容都是禁忌。你不能使用标准容器、字符串或流，但 C++ 语言设计者已经考虑了交互的可能性。

- C 函数不抛出异常。你通常将错误码作为返回值或参数来处理。

- C 语言中没有重载函数；每个名称都有固定的参数类型集合（这在 C11 中已部分改变）。也不存在运算符函数（operator functions）。

- 你很少遇到带参数的 `const`。当 `const` 出现时，它更多是为了文档说明。你无法确定 C 函数没有修改你通过指针传递的参数。

在完成这个理论列表之后，我们进入实践阶段。作为一个示例，我选择了 `zlib` [52] C 库，我想将其集成。

`zlib` 库包含了用于压缩数据的函数；它会移除冗余信息，留下一个更小的数据包，你可以将其将其传输到互联网或存储在硬盘上。库中的一组函数用于读取和写入 `*.gz` 文件——这是一种被广泛使用的数据格式。如果你电脑上上有一个用于打包或解压文件的程序（例如 `7zip` 或 `WinZip`），你很可能也可以解压 `*.gz` 文件。`*.gz` 与其他压缩格式的一个区别是，每个压缩文件可能恰好包含一个原始文件。在文件压缩后，直接在原始文件名后追加 `.gz` 是很常见的。

## 22.1 使用库

你包含的 C 库由以下组件组成：

- 库文件

你将你的程序与库文件链接，以使用第三方函数。这些是一个或多个 `*.a`、`*.dll`（Windows）或 `*.so`（Linux）文件。在少数情况下，你还会收到源代码并将 `./*.obj` 对象文件链接到你的程序中。

- 头文件

你通常会获得几个 `*.h` 文件。你需要通过 `#include` 将这些文件包含在你的源代码中。

- 文档

有时你会得到一份独立的文档；有时你只有头文件。

在翻译过程中如何让库和头文件被感知很大取决于编译器。请参考有关如何调整库路径和包含路径，以及如何链接特定库的文档。

使用 `g++` 时，此示例翻译如下：

```
g++ gzpack.cpp -o gzpack.x -lz -Lzlib -Izlib/include
```

你应该已经熟悉 `g++ gzpack.cpp -o gzpack.x` 部分了。其余参数如下：

- `-lz`

`-l` 表示应该链接一个库。这里是 `z` 代表 `libz`。

- `-Lzlib`

`-L` 指定库的搜索路径；这里 `libz.a` 位于 `zlib` 目录中。

- `-Izlib/include`

`-I` 指定头文件的搜索路径；这里 `zlib.h` 位于 `zlib/include` 目录。

## 22.2 C 头文件

演示程序从任何输入文件创建一个压缩的输出文件。这只需要 `zlib` 中的三个函数。文档中包含了许多关于这些函数的信息，我建议你阅读它们。我在这里关注头文件中的信息或来自文档的函数签名（某些内容经过了简化）。为了你自己的实验和复现示例，你当然应该使用原始库：

```
typedef struct gzFile_s *gzFile;
extern "C" gzopen(const char *path, const char * mode);
extern "C" int gzwrite(gzFile, void* buf, unsigned len);
extern "C" int gzclose(gzFile file);
```

当你在源代码包含包含内容时，这些以及许多其他类型和函数供你使用：

```
#include <zlib.h>
```

首先，`typedef` 引入了新的 `gzFile` 类型。这是一个指向 `struct gzFile_s` 的指针。它的内部细节特意没有提到，因为它们无关。将 `gzFile` 简单地视为一个允许你访问 `*.gz` 文件的句柄（handle）。

这三个函数是自由函数（free functions），所有参数和返回值都是内置类型或原始指针——这在 C 中非常常见。

每个函数都用 `extern "C"` 引入，以便你作为一个 C++ 作者，在包含该头文件时，可以区分 C++ 函数和 C 函数。这是必要的，因为 C++ 使用了不同的机制。如果头文件中缺少了 `extern "C"`，你可以以一种稍微复杂的方式在源代码中包含它：

```
extern "C" {
#include <zlib.h>
}
```

在你拥有头文件后，继续编写程序的其余部分。除了 `<zlib.h>`，你还需要标准库的一些 C++ 头文件。对于 `zlib` 的错误处理，`<errno>` 和 `<cstring>` C 头文件是必要的。前者允许查询错误码变量 `errno`，`zlib` 使用它；这在文档中提到。后者提供了 `strerror` 将错误码转换为可读的文本消息。这两个头文件都是 C 标准库的一部分。因此，每个头文件有两个变体：在 C++ 中你使用 `<errno>` 而不是 `<errno.h>`。同样，对于 C++ 程序，`strings.h` 变为 `<cstring>`。“前加 c，删除 .h”的规则适用于 C 标准库的大多数头文件——但不适用于第三方库。这些 C++ 变体是 C++ 标准库的一部分，并保证例如每个函数都获得 `extern "C"`。此外，通过这种方式导入的所有 C 函数都位于 `std` 命名空间中。因此，你也可以调用 `std::strerror()`。

```cpp
// https://godbolt.org/z/9Tr8h8Mb
#include <string>
#include <vector>
#include <span>                            // C++20
#include <fstream>                       // ifstream
#include <cstdexcept>                    // runtime_error
#include <iostream>                     // cerr
// C-Header:
#include <zlib.h>                        // gzxy; sudo aptitude install lib-dev
#include <errno>                       // errno
#include <cstring>                     // strerror
namespace {
    using std::string; using std::span;  using std::byte;
```

**列表 22.1** "`gzpack.cpp`" 程序使用了 C 库。在这里你看到了包含文件的部分。

在倒数第二行，我以 `namespace` 开始——一个匿名命名空间。这隐藏了此 `*.cpp` 文件中的所有变量、类型和函数，防止与其他发生冲突。对于自由函数，你也可以写 `static`，但对于数据类型，这只能通过匿名命名空间实现，这通常是一个好主意。

通过这两个 `using` 声明，我减少了源代码其余部分的输入工作。匿名命名空间的另一个优势是，这两个 `using` 声明也仅作用于命名空间内部，不会影响外部。

接下来，我定义了一个封装了 C 库主要功能的类。在这个示例中，三个相关的 C 函数都已经被包含在内。根据名称，你可能已经猜出它们的含义和一些操作规则：

- `Gzopen()` 打开一个文件。如果失败，该函数将根据 C 惯例返回一个特殊值。

- `Gzclose()` 关闭一个正确打开的文件。如果 `gz-open` 失败，则无需调用此函数。

- `Gzwrite()` 将数据写入输出。返回值大于 0 表示成功。

```cpp
// https://godbolt.org/z/Yh7j1WEGc
// RAII 封装
class GzWriteStream {
public:
    GzFile gz_; // 来自 zlib.h 的 C 结构体
    explicit GzWriteStream(const string& filename)
        : gz_(gzopen(filename.c_str(), "wb")) // 'w': 写, 'b': 二进制，
{
        if(gz_==NULL) throw runtime_error(std::strerror(errno));
    }
    ~GzWriteStream() {
        fclose(gz_);
    }
    GzWriteStream& operator<<=(const span<char> &data) {
        write(data);
        return *this;
    }
private:
    void write(span<char> data) { // C++20
        auto bytes = std::as_bytes(data);
        auto res = gzwrite(gz_, bytes.data(), size(bytes));
        if(res==0) throw std::runtime_error("Error writing");
    }
    GzWriteStream(const GzWriteStream&) = delete; // 禁止拷贝
    GzWriteStream& operator=(const GzWriteStream&) = delete; // 禁止赋值
};
```

**列表 22.2** "`gzpack.cpp`" 的这部分包含了所有用到的 C 函数。

作为一个数据字段，`GzWriteStream` 包含 `gz_` 句柄，作为连接到 `zlib` 以及已打开文件的通道。在构造函数的初始化列表中，`gzopen()` 打开文件并将结果赋值给句柄。文档指出，返回 `NULL` 表示错误。此时，全局变量 `errno` 会显示具体的错误。你可以使用 `strerror` 来解码这些代码。更重要的是，你应该以此方式抛出异常并退出代码，而不是直接跳出并运行到最后。

如果 `gzopen()` 失败，则不需要调用 `gzclose()`。因此，这是使用析构函数的理想用例。如果异常导致构造函数退出而非正常运行结束，则 `GzWriteStream` 对象被视为未创建。因此，析构函数也不会被调用。

`gzopen()` 的第一个参数接收一个 C 字符串格式的文件名。从 `string` 的 `filename` 参数，你可以使用 `c_str()` 方法获取 C 字符串格式的文件名。第二个参数 `"wb9"` 表示以写入模式打开文件（'w' 代表写入）。'b' 代表二进制格式。另一种 't' 代表文本格式可能会转换单个字符。最后的 '9' 代表最大数据压缩率。

## 22.3 C 资源

在类的构造函数和析构函数中将 `gzopen()` 和 `gzclose()` 函数对封装在一起在这里特别合适，因为这两个函数总是需要成对调用的。没有（成功的）`gzopen()` 就没有 `gzclose()`，也没有没有 `gzopen()` way `gzclose()`。

你在许多 C 接口中都会遇到这种配对。无论是初始化整个库，还是为窗框获取并释放画笔——这种函数对很常见，此时使用那一个封装类就是恰恰合适的。

在 `GzWriteStream` 中，我包含了更多的功能。然而，有时你只需要两个函数的配对。在这种情况下，为每一对函数编写单独的封装类可能会很乏味。如果这对你来说工作量太大，你可以退回到熟悉的 `shared_ptr`：你可以在构造函数接收两个参数而非一个的变体中使用它。

这里的第二个参数是一个函数对象，它会在 `shared_ptr` 的析构函数内部调用。`shared_ptr` 此自定义删除器。

在这里我做一个简短的插叙，因为作为一个函数对象，你看到了一个 lambda——一个没有名的函数——并在其中调用了 `gzclose()`：

```cpp
std::shared_ptr<gzFile_s> gz(
  gzopen(fNameOut.c_str(), "wb9"),
  [](gzFile_s* f) { gzclose(f); }
);
if(gz.get() == NULL) throw std::runtime_error("Error");
```

你将在第 23 节第 23.3 节学习更多内容。

对于简单的 C 函数配对，你几乎总是可以使用带有两个参数的 `shared_ptr` 构造函数模式。

## 22.4 “void”指针

第三个函数 `gzwrite()` 取两个参数：指向数据的 `void*` 和数据的长度。返回值是写入的数据量；0 表示错误。
