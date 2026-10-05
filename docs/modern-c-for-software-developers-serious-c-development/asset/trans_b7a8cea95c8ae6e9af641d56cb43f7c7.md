
编译器将其隐式转换为枚举类型，而枚举类型不会被隐式转换为整数类型。因此，以下带有作用域枚举（scoped enum）的程序将无法编译：

```cpp
#include <iostream>
#include <string>

int main()
{
    enum class Color { RED, GREEN, BLUE };
    Color my_color;

    my_color = 1;      // error
    if (my_color == Color::GREEN)
        std::cout << "green color" << std::endl;
}
```

// output
error: cannot convert 'int' to 'main()::Color' in assignment

这种强类型安全也适用于 C++11 中的非作用域枚举。

## 枚举的前向引用

我们可以为作用域枚举和非作用域的枚举指定前向声明：

- # Mood 枚举的前向声明
enum class Mood;

## 定义良好的枚举大小：`<cstdint>`

C 和 C++ 通常不为其原生类型提供固定的的、定义良好的位宽。例如，有时我们需要一个 32 位的整数，而不仅仅是一个 `int` 类型。这是因为 `int` 类型在不同的 CPU 架构上可能有不同的尺寸。C++11 通过 C99 头文件 `std.h` 解决了这个问题。我们通过 `#include <cstdint>` 此头文件来指定具有定义大小的整数类型。

`cstdint` 头文件包含了 `std::int_t`、`std::int16_t`、`std::int32_t` 和 `std::int64_t`（以及带有 `u` 前缀的无符号版本）。例如：`std::uint8_t` 指的是 8 位的无符号整数类型。`cstdint` 头文件中的整数类型指定了各种类型的位宽。

我们可以如下使用这些 `cstdint` 类型：

```cpp
#include <cstdint>
enum class Colour : std::int8_t { RED = 1, GREEN = 2, BLUE = 3 };
```

## 现代 C++：类型别名 (C++11)

### Typedef

C 或 C++ 的 `typedef` 声明引入了一个名称，该名称在它的作用域内成为现有类型的别名。语法为：

```cpp
typedef [existing-type] [our-alias];
```

这里有一个示例：

```cpp
// 将 UL 为 unsigned long 类型的别名。
typedef unsigned long UL;
UL x = 5;
```

字体 使用 using 关键字的类型别名声明 (using =)

我们之前已经看到，可以使用 `using` 关键字将命名空间引入作用域中：

```cpp
using namespace std;
```

在 C++11 中，我们还可以利用 `using` 关键字来声明一个名称是之前声明的类型的别名。语法为：

```cpp
using new_type_name = some_declared_type;
```

新类型名称在新类型的作用域内是现有类型的别名。

这里是一些示例：

```cpp
using iter_t = std::vector<int, std::string>::iterator;
using counter = long;
using Map = std::map<std::string, std::string>;
```

`using` 类型别名也适用于函数指针，但它们比等效的 `typedef` 更具可读性：

```cpp
double adder(int x, double y) {
    double z = x + y;
    return z;
}

// 类型 funcptr 的声明
using funcptr = double(*)(int, double);

// 定义
funcptr f = adder;

这等同于：
void (*)(int, double) f = adder;
```

`typedef` 和 `using` 可以用于为类型赋予语义内容： 

```cpp
using velocity = long;
```

## Using 和模板

类型别名声明相对于 `typedef` 的优势在于，后者不能与模板配合使用。

以下是模板别名的语法：

```cpp
template<class T> using Vec = std::vector<T>;
```

## 现代 C++：用户字面量 (C++11)

在 C++11 中，字面量有四种类型：整数、浮点、字符和字符串。字面量可以通过指定后缀来定义。例如：

```cpp
#include <iostream>
using namespace std;

int main() {
    long a = 100_;
    float b = 3.05f;
    char c = = ""


    


0 
;






}
```
