

# 第 3 章

# 值与变量

在本章中，我们将探索用于开发 C++ 程序的某些构建模块。我们将对以下概念进行实验：

- 数值
- 变量
- 声明
- 赋值
- 标识符
- 留关键字

在下一章中，我们将在结合其他数据类型的背景下重新回顾这些概念。

## 3.1 整数值

数字 (4) 是数值的一个示例。在数学中，4 是一个整数值。整数是整数，这意味着它们没有小数部分，且整数可以是正数、负数或零。整数的示例包括 4、19 和 -1005。相比之下，4.5 不是整数，因为它不是整数。

C++ 支持多种数值和非数值。特别是 C++ 程序可以使用整数值。编写一个显示数字四的 C++ 程序非常简单，如列表 3.1 (number4.cpp) 所示。

```cpp
Listing 3.1: number4.cpp
#include <iostream>
using namespace std;

int main() {
    cout << 4 << endl;
}
```

注意，与我们之前看到的程序不同，列表 3.1 (number4.cpp) 没有使用引号 ("")。将列表 3.1 (number4.cpp) 与列表 3.2 (number4-alt.cpp) 进行比较。

```cpp
Listing 3.2: number4-alt.cpp
#include <iostream>
using namespace std;

int main() {
    cout << "4" << endl;
}
```

两个程序的行为完全相同，但列表 3.1 (number4.cpp) 打印的是数字四的值，而列表 3.2 (number4-alt.cpp) 打印的是包含该数字的消息。这里的区别并不重要，但我们将在 3.2 节中看到，引号的存在与否会对输出产生巨大影响。

在 C++ 源代码中，整数不能包含逗号。这意味着我们必须将数字二千四百六八写成 2468，而不是 2,468。在数学中，整数是无界的；另一种说法，数学整数集是无限的。在 C++ 中，整数的范围是有限的，因为所有计算机的内存都是有限的。支持的整数精确范围取决于系统和特定的编译器。在大多数 32 位系统上的 C++ 可以表示范围从 -2,147,483,648 到 +2,147,483,647 的整数。

如果你超过 C++ 整数的范围会发生什么？尝试在你的系统上运行列表 3.3 (exceed.cpp)。

```cpp
Listing 3.3: exceed.cpp
#include <iostream>

using namespace std;

int main() {
    cout << -30000000000 << endl;
}
```

然而，负十亿对于32位整数来说太大了，程序的输出是错误的：

```
1294967296
```

打印的值并不是负数！大多数 C++ 编译器会对该语句发出警告。`expression::expressionarithmetic` 详细地探讨了错误与警告的区别。如果编译器在源代码中发现错误，它将不会生成代码。警告表示潜在的问题，并且不会阻止编译器生成可执行文件。在这里我们看到程序员应该重视此警告，因为程序的执行产生了无意义的输出。

这种有限的值范围在编程语言中很常见，因为每个整数都存储在固定量的内存中。较大的数字需要更多的内存。要模拟数学整数的无限集，将无限的内存！正如我们后面看到的，C++ 支持一种范围更大的整数类型。

附录 D.1 提供了关于 C++ 整数实现的一些细节。

## 3.2 变量与赋值

在代数中，变量被用来表示数字。C++ 中也是如此，但 C++ 变量还可以表示数字以外的值。列表 3.4 (variable.cpp) 使用变量来存储整数值，然后打印该变量的值。

```cpp
Listing 3.4: variable.cpp
#include <iostream>

using namespace std;

int main() {
    int x;
    x = 10;
    cout << x << endl;
}
```

列表 3.4 (variable.cpp) 中的 main 函数包含三个语句：

- `int x;`

这是一个声明语句。C++ 程序中的所有变量都必须声明。声明指定了变量的类型。`int` 单词表示变量是整数。整数的名字是 `x`。变量 `x` 的类型是 `int`。C++ 支持整数以外的类型，某些类型在计算机内存中需要更多或更少的空间。编译器使用声明来留出适当内存来存储变量的值。由于编译器，它还可以检查变量是否被正确使用；例如，我们看到它可以像数学中一样相加。然而，对于其他某些类型，加法是不可能的，因此也是不允许的。编译器可以确保加法中的变量与声明兼容。如果不兼容，它会返回错误。

如果程序员尝试使用未声明的变量，编译器将发出错误。

- `x = 10;`

这是一个赋值语句。赋值将右侧的值与左侧的变量关联。使用的符号是 `=`。变量在其生命周期内可以被重新赋值多次。列表 3.5 (multipleassignment.cpp) 显示了这一点。

```cpp
Listing 3.5: multipleassignment.cpp
#include <iostream>

using namespace std;

int main() {
    int x;
    x = 10;
    cout << x << endl;
    x = 20;
    cout << x << endl;
    x = 30;
    cout << x << endl;
}
```

变量可以在声明时赋予一个值；例如，列表 3.6 (variable-init.cpp) 是 3.4 (variable.cpp) 的变体。

```cpp
Listing 3.6: variable-init.cpp
#include <iostream>

using namespace std;

int main() {
    int x = 10;
    cout << x << endl;
}
```

注意，在列表 3.6 (variable-init.cpp) 中，变量的声明和赋值在一个语句中完成。这种组合的声明和立即赋值被称为初始化。C++ 在列表 3.7 (alt-variable-init.cpp) 中支持另一种初始化变量的语法。

```cpp
Listing 3.7: alt-variable-init.cpp
#include <iostream>

using namespace std;

int main() {
    int x{10};
    cout << x << endl;
}
```

这种形式不常用于简单变量，但在初始化复杂的对象时是必要的。我们在第 13 章和第 14 章中介绍对象。

