
- 你正在初始化的变量类型，
- 变量名，以及
- 变量第一个值的表达式。

表达式的类型通常与变量的类型相同。有时你让编译器执行*隐式转换*。不过，你通常可以省去再次指定表达式类型的工作。你可以改用 `auto`。然后编译器会采用表达式的类型来确定变量类型。这称为*类型推导*：

```cpp
auto number = 10;
auto value = 3.1415 * sin(alpha);
for(auto it = container.begin(); ... ) ...
```

这里的变量 `number` 变为 `int`，而 `value` 变为 `double`，其类型就是 `begin()` 返回的类型，很可能是变量容器的迭代器。

不过，从 C++20 起，你可以用*概念*进一步限制类型。这允许你指定变量类型必须满足某些条件。标准库为此提供了许多概念，例如 `integral` 和 `floating_point`：

```cpp
integral auto number = get_number();
floating_point auto pointy_number = get_ampere();
```

如果这里只写 auto number，那么 number 也可能是 double——这在后续计算过程中可能会给 number 带来问题。另一方面，如果你用 int number 完全定义类型，就会失去将 get_number() 的返回值扩展为 long 的选项。此外，相关代码行也可能位于泛型代码中，其中 get_number() 的返回类型可以是 int 或 long，但你希望防止 get_number() 返回 double。

概念与 auto 结合使用的优点是提供文档说明，并防止意外。

除了标准库中的内置概念，你也可以定义自己的概念。

无论是否使用概念，auto 都会像你显式写出类型一样定义变量类型。绝不是说 auto 本身就是一种可变类型。一旦设定，变量就保持其类型。

编译器为 val 确定类型 int。之后赋予文本字面量是错误的：

```cpp
auto val = 12;
val = "Name";    // ✕ Error: Assignment of "const char*" to "int"
```

你可以在*第12章第12.12节*中确切了解 auto 的工作原理。

## 4.2.12 include 指令详解

include 始终以井号 # 开头。行首的这种字符表示给预处理器的一条指令。如果你还记得第2章图2.1，那么你已经熟悉翻译的这个阶段。

这里通过 #include 包含的文件会被预处理器几乎像复制粘贴一样插入到你的程序中。其效果是，该文件中的所有声明现在都成为你程序的一部分。

还有其他预处理器指令，但 #include 对你来说是最重要的。其他指令见第21章。

include 始终应放在源文件顶部。在代码清单4.2中，我使用了其中两个。

```cpp
#include <iostream>  // cin, cout
#include <string>    // stoi
```

`<iostream>` 和 `<string>` 都是 C++ 标准库的一部分。因此，它们包含不属于核心语言的内容。像 int 这样的东西在所有系统上始终存在，无需 include。标准库通常会存在——我们在本书中假定如此——但并非总是如此。

由于你用 #include 将许多标识符引入当前源代码，因此添加注释来指出你在此翻译单元中使用了其中哪些标识符会很有帮助。这使读者只需搜索文件就能找出未知标识符来自哪里。有些模块名不言自明。例如，`#include <vector>` 导入 vector；无需解释。

你可以通过名称没有 .h 之类的扩展名来识别标准库的 include。惯例是只使用没有扩展名的标准库头文件。如果你创建自己的头文件，则追加 .h、.hpp、.H、.hh 或 .hxx。实践中，.h 最常见，即使有些程序员不喜欢这样，因为该头文件从外部看与 C 头文件没有区别。.hpp 文件扩展名常被选作替代。无论使用哪种扩展名，都要在 #include 指令中写出它：

```cpp
#include <iostream>          // Module of the standard library
#include <asteroids.h>       // Module of a third-party provider
#include "myModule.hpp"      // Module of the current project
#include "algo/myModule.h"   // in a subdirectory
```

如果头文件已安装在你系统上，就把头文件名写在尖括号中；编译器应搜索它。如果头文件是你当前项目的一部分，并未安装在某个位置，则使用引号 "..."。有些编译器随后会先在当前项目中搜索该文件。

### include 的禁忌

命名文件时要注意大小写，因为某些系统会区分大小写，亲爱的 Windows 用户！如果头文件位于子目录中，始终使用 `/` 分隔：

```cpp
#include "MY_MODULE.H"             // ⚡ not good if the file is called "myModule.h"
#include "algo\\myModule.h"          // also use "/" under Windows
#include "c:/project/myModule.h"     // no absolute paths
#include "../algo/myModule.h"         // no relative paths with ".."
```

不要使用绝对路径或 `..`，而应把头文件存放在项目中的其他位置，和/或必须在编译器选项中调整头文件搜索路径。这样在必要时移动和重新组织项目会更容易。

关于尖括号与引号再说明一点：最初，`<...>` 与 `"..."` 的区别意味着头文件可能是编译器的一部分，而根本不是文件。然而，现在人们已经接受：如果只是一个预期已安装在系统上的头文件，也使用尖括号。因此，只对属于你当前项目、并且应优先于其他库的文件使用 `"..."`。这种优先级是否有效取决于所用编译器。

## 4.2.13 模块

*模块*是随 C++20 引入的。与其将文本形式的 `#include` 指令“复制”到翻译单元中，不如将代码划分为接口区和实现区。为此，使用新关键字 `module` 和 `import`。你可以在 C++ 参考以及 Dos Reis 的教程（如 https://youtu.be/tjSuKOz5HK4）中找到确切用法。然而，目前仍没有“最佳实践”，标准库也尚未划分为模块。C++23 引入了两个标准模块 `std` 和 `std.compat`，它们包含标准库中的*所有内容*。`std` 模块包含可通过 `std::` 访问的符号，例如 `std::vector`。`std.compat` 模块包含全局命名空间的标识符，例如 `::fclose`。

但在 2024 年的今天，这些内容在主要的 g++ 13、clang++ 18 和 msvc++ 19.37 编译器中并没有实现多少，而且有些实现与其他实现不兼容。只要还无法预见模块对你来说触手可及，如果你感兴趣，我建议你参考非常前沿的资料。

不过，我想简要转述 Nico Josuttis 的一些建议，说明如何最好地配合新兴惯例，并在移植到另一个平台时尽可能少出问题。⁴

- *接口文件*应使用 `.cppm` 扩展名（不要使用 `.ixx`；MSVC 使用 `/interface`）。⁵
- 将*模块实现文件*保留为 `.cpp`。
- *内部分区实现文件*应使用 `.cppp` 或 `.cppm` 扩展名。

但如果你使用它们，模块和 include 并不互斥。只要遵循某些模式，就可以并行使用两者——而且很可能在很长一段时间内都必须如此，因为即使模块是更好的替代方案，由于历史原因，include 仍会存在很久。

## 4.2.14 输入与输出

现在你已经了解了程序中所有重要的元素，除了——有人会说——最重要的那些元素。毕竟，没有*输入*和*输出*的程序还叫程序吗？

你已经看到 `<<` 被用作输出运算符。而 `#include <iostream>` 也是因为 `std::cout` 才包含的。下面是代码清单4.2中的一段摘录，主要涉及输出：

```cpp
std::cout << "Divisors of " << n << " are:\n";
for(int divider=1; divider <= n; ++divider) {
    if(n % divider == 0)
        std::cout << divider << ", ";
}
std::cout << std::endl;
```

你可以看到，可以直接把多个 `<<` 串接起来。更具体地说，`std::cout << "divisors of "` 是一个表达式，它作为副作用执行输出，然后再次返回 `std::cout`。这实际上会执行 `std::cout << n`，同样进行输出并得到结果 `std::cout`。最后同样重要的是，语句的第三个运算符开始发挥作用，执行 `std::cout << " are:\n"`。这个运算符的特殊之处在于它包含一个*换行符*。在 C++ 字符串中，这由 `\n` 表示。正是这个换行符在循环内的输出中被省略了；因此，这些数字显示在同一行。

使用 `std::cout << std::endl` 时，程序会在列表末尾输出换行。可是，哎呀，`\n` 在哪里？这一次，清单中出现的是 `std::cout` 的一个特殊元素，即*操纵器* `std::endl`。它确保换行，并且保证系统不会缓冲输出。它会强制把你到目前为止放入的内容真正显示到屏幕上。这是因为（屏幕）输出很耗时，而且

⁴ C++20：完整指南，Nico Josuttis，https://leanpub.com/cpp20，Leanpub，2022
⁵ Cppmodules，Nico Josuttis，https://github.com/josuttis/cppmodules，2023年11月30日
