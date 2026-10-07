

## 1.2 与 C 的兼容性

第 01 章：迈向现代 C++

```cpp
}
#endif
```

```cpp
// foo.c
int add(int x, int y) {
    return x+y;
}
```

```cpp
// 1.1.cpp
#include "foo.h"
#include <iostream>
#include <functional>
```

```cpp
int main() {
    auto out = std::ref(std::cout << "Result from C code: " << add(1,2));
    out.get() << "\n";
    return 0;
}
```

你应该首先使用 gcc 编译 C 代码：

```
gcc -c foo.c
```

编译并输出 foo.o 文件，然后使用 clang++ 将 C++ 代码链接到 .o 文件（或者将都编译为 .o 然后将它们链接在一起）：

```cpp
clang++ 1.1.cpp -std=c++2a -o 1.1
```

当然，你可以使用 Makefile 来编译上述代码：

```makefile
C = gcc
CXX = clang++
SOURCE_C = foo.c
OBJECTS_C = foo.o
SOURCE_CXX = 1.1.cpp
TARGET = 1.1
LDFLAGS_COMMON = -std=c++2a
```

## 延伸阅读

all:

```makefile
$$(C) -c $(SOURCE_C)
$(CXX) $(SOURCE_CXX) $(OBJECTS_C) $(LDFLAGS_COMMON) -o $(TARGET)
```

clean:

```makefile
rm -rf *. $(TARGET)
```

注意：Makefile 中的缩进是 Tab 键而不是空格字符。如果你将此代码复制到编辑器，Tab 可能会被自动替换。请确保 Makefile 中的缩进正确。它是通过 Tab 完成的。

如果你不知道 Makefile 的用法，没关系。在在本教程中，你不需要构建过于复杂的代码。你也可以简单地在命令行上使用 `clang++-std=c++2a` 来阅读这本书。

如果你是现代 C++ 的初学者，你可能仍然不理解上面那小段代码：

```cpp
auto out = std::ref(std::cout << "Result from C code: " << add(1, 2));
out.get() << "\n";
```

现在不要担心，我们将在后面的章节中遇到它们。

## 延伸阅读

- 《C++ 语言之旅》（第2版）Bjarne Stroustrup
- C++ 历史
- C++ 编译器支持
- ISO C 与 ISO C++ 之间的不兼容性

## 第 02 章：语言可用性增强

当我们在运行时声明、定义变量或常量，并控制代码流、面向对象的函数、模板编程等时，这些可能会在编写代码或编译器编译代码时发生。我们通常称这为语言可用性，指的是发生在运行之前的语言行为。

## 2.1 常量

### nullptr

`nullptr` 的出现是为了替代 NULL。在某种意义上，传统的 C++ 将 NULL 和 0 视为相同，这取决于编译器如何定义 NULL，某些编译器将 NULL 定义为 `((void*)0)`，而有些直接将其定义为 0。

C++ 不允许将 `void *` 隐式转换为其他类型。但如果编译器尝试将 NULL 定义为 `((void*)0)`，那么在以下代码中：

```cpp
char *ch = NULL;
```

C++ 没有通过 `void *` 隐式转换将 NULL 定义为 0。这仍然产生了一个问题。将 NULL 定义为 0 会导致 C++ 的重载功能变得混乱。考虑以下两个函数：

```cpp
void foo(char*);
void foo(int);
```

那么 `foo(NULL)` 语句将调用 `foo(int)`，这会导致代码违背直觉。

为了解决这个问题，C++11 引入了 `nullptr` 关键字，专门用于区分空指针。`nullptr` 的类型是 `nullptr_t`，它可以隐式转换为任何指针或指针类型，并可以与它们进行相等或不等的比较。

你可以尝试使用 clang++ 编译以下代码：

```cpp
#include <iostream>
#include <type_traits>

void foo(char *);
void foo(int);

int main() {
    if (std::is_same<decltype(NULL), void(*)>::value) {
        std::cout << "NULL = 0" << std::endl;
    }
    if (std::is_same<decltype(NULL), void(*)>::value) {
        std::cout << "NULL = (void*)0" << std::endl;
    }
    if (std::is_same<decltype(NULL), nullptr_t>::value) {
        std::cout << "NULL = nullptr" << std::endl;
    }

    foo(0);              // 会调用 foo(int)
    foo(NULL);      // 不编译
    foo(nullptr);      // 会调用 foo(char*)
    return 0;
}

void foo(int i) {
    std::cout << "foo(int) is called" << std::endl;
}

// 输出是：
foo(int) is called
foo(char*) is called
```

从输出可以看出 NULL 不同于 0。因此，养成直接使用 `nullptr` 的习惯。此外，在代码中使用的 `decltype` 和 `std::is_same` 是现代 C++ 的语法。简单来说，`decltype` 用于类型推导，`std::is_same` 用于比较两个类型的相等性。我们将在 `constexpr` 部分详细讨论。

### constexpr

C++ 本身已经有了常量表达式的概念，例如 `1+2`、`3*4`。这类表达式总是产生相同的结果。如果编译器可以在编译时直接嵌入这些表达式，将会提高性能。一个非常明显的例子是在数组定义：

```cpp
#include <iostream>
#define LEN 10

int len_foo() {
    int i = 2;
    return i;
}

constexpr int len_foo() {
    return 5;
}

constexpr int fibonacci(int n) {
    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}

int main() {
    char arr1[10]; // 合法
    char arr2[LEN]; // 合法
    int len = 10;
    // arr3[len];               // 非法

    const int len2 = len + 1;
    constexpr int len2c = len + 2 + 3;
    // arr4[len2];              // 非法，但在大多数编译器中可以
    char arr4[len2c];         // 合法

    // arr5[len_foo()];          // 非法
    char arr6[len_foo() = 2 ? 1]; // 合法

    // 1, 2, 3, 5, 8, 13, 21, 34, 55
    std::cout << fibonacci(10) << std::endl;

    return 0;
}
```

在上面的示例中，`arr4[len2]` 可能会让人困惑，因为 `len2` 被定义为常量。为什么 `arr4[len2]` 是法的？因为 C++ 标准规定数组长度必须是常量表达式，对于 `len2`，它是一个 const 常量而不是常量表达式（尽管大多数编译器支持，但它是非法行为）。我们需要使用 C++11 引入的 `constexpr` 特性来解决这个问题；在 C++98 中，编译器不知道 `len_foo()` 在运行时返回常量，这导致了错误的产生。注意，大多数编译器现在都有自己的优化。许多非法行为在编译优化下变成了合法的。如果你需要重现错误，需要使用旧版本的编译器。C++11 允许用户显式声明函数或对象构造将在编译时变为常量表达式。`constexpr` 关键字显式告诉编译器 `len_foo` 应该是一个编译时表达式。

此外，`constexpr` 函数可以使用递归：

```cpp
constexpr int fibonacci(int n) {
    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

从 C++14 开始，`constexpr` 函数内部可以使用简单语句作为局部变量、循环和分支。例如，代码在 C++11 标准下无法编译。

## 2.2 变量与初始化

```cpp
constexpr int fibonacci(int n) {
    if(n == 1) return 1;
    if(n == 2) return 1;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

对于此，我们可以写一个简化版本使其从 C++11 开始可用：

```cpp
constexpr int fibonacci(int n) {
  return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

### if-switch

在传统的 C++ 中，变量的声明可以声明一个临时 int，尽管它可以位于任何地方，即使是一个语句，但在 `if` 和 `switch` 语句中没有办法声明临时变量。例如：

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
```

```cpp
int main() {
  std::vector<int> vec = {1, 2, 3, 4};

  // 从 c++17 开始，可以使用 auto 简化
  const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 2);
  if (itr != vec.end()) {
    *itr = 3;
  }

  if (const std::vector<int>::iterator itr = std::find(vec.begin(), vec.end(), 3);
      itr != vec.end()) {
    *itr = 4;
  }

  // 应该输出：1, 4, 3, 4。可以使用 auto 简化
  for (std::vector<int>::iterator element = vec.begin(); element != vec.end(); ++element) {
    std::cout << *element << std::endl;
  }
}
```

