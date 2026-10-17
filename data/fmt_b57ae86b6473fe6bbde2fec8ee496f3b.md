
```cpp
constexpr T area_of_circle(T radius)
{
    auto area = pi<T> * radius * radius;
    return area;
}

int main()
{
    auto area = area_of_circle(5.78);
    std::cout << area << std::endl;
}

// output
104.956
```

# 现代 C++：constexpr 函数 (C++14)

C++14 允许在 `constexpr` 函数体内包含更多表达式：

- 在 `constexpr` 函数内部允许进行局部变量声明，只要它们不是 `static` 或 `thread_local` 声明。局部变量必须初始化。
- 在 `constexpr` 函数内部允许 `if`、`switch`、`for`、`while`、`do-while` 表达式。

# 现代 C++：二进制字面量 (C++14)

C++14 允许声明二进制字面量。二进制字面量以 `0B` 或 `0b` 前缀开头，后面跟着一系列 1 和 0：

```cpp
auto y = 0b00000101; // 整数5 的二进制（二进制）字面量
```

二进制字面量具有整型。

# 现代 C++：数字分隔符 (C++14)

C++14 允许使用单引号分隔整数字面量，以提高可读性：

```cpp
12345'67890'1245LL
cout << 12345'67890'1245LL
std::cout << 12345'67890'1245LL
std::cout << 12345'67890'1245LL
```

# 现代 C++：[[deprecated]] 属性 (C++14)

`[[deprecated]]` 关键字用于警告某个表达式、函数或类已过时，但不建议使用。语法如下：

```cpp
[[deprecated]]
```

`[[deprecated]]` 编译器会输出项目过时的警告。可以通过以下方式附加可选的消息：

```cpp
[[deprecated("message")]]
```

示例：

```cpp
// 识别过时的函数
[[deprecated("sqlConnect is obsolete")]]
int sqlConnect() {
```

```cpp
// 识别过时的类
#include <iostream>
using std;
int main() {
class [[ deprecated("Foo is obsolete") ]] Foo {
public:
  Foo() { cout << "in constructor" << endl; }
};
Foo foo;
}
```

```
// 返回
warning: 'Foo' is obsolete
```

# 现代 C++：类型推断 (C++17)

## 函数模板参数推断

模板参数推断是指编译器推导函数模板参数类型的能力。

在函数模板中，参数推断实现如下。考虑以下函数模板声明：

```cpp
template<typename T>
void foo(const T& data)
```

在 C++17 中，可以使用类参数推断（CTAD）来避免指定类的模板参数。

## 类模板参数推断

在 C++17 中，可以使用类参数推断（CTAD）来避免指定类的模板参数。

```cpp
template <typename A, typename B>
struct MyPair
{
  MyPair() {}
  MyPair(const A&, const B&) {}
};

int main()
{
  MyPair p1 {11, 22}; // 推断为 MyPair<int, int>
  // MyPair p2; // 错误：没有匹配的构造函数
}
```

# 现代 C++：非模板类型参数 (C++17)

在 C++11 和 C++14 中，只要我们可以自动推断模板参数或函数返回类型，就可以使用类型 `auto`。`auto` 也可以用于泛型 lambda。

在此之前，非模板参数的类型必须在类模板或函数模板中显式声明，因为编译器不会推断这些参数的类型。

### 非模板类型参数总结

以下是在模板中使用非类型参数的示例：

```cpp
#include <iostream>

// size是非模板类型参数
template<class T, int size>
class Foo
{
  T array[size];
public:
  Foo() {}
  ~Foo() {};
  int getSize() const
  {
    return size;
  }
};

int main(){
  Foo<double, 29> foo;
  auto size = foo.getSize();
  std::cout << size << std::endl;
}

// output
29
```

在本示例中，非模板类型参数的大小是模板声明的一部分。
值 20 在编译时被替换到 `Foo` 类的特化版本中。

非模板类型参数是一种特殊的参数类型，在类模板或函数模板特化时，它会被具体值替换。

C++ 要求非模板类型参数的参数必须是以下类型之一：

- 具有整数类型或为枚举的值
- 指向类对象的指针或引用
- 指向函数的指针或引用
- 指向类成员函数的指针或引用
- `nullptr`

**注意**，我们不能将 `double` 或 `float` 类型作为非模板参数。

### Auto 非模板参数

在 C++17 中，我们可以在模板声明中声明类型为 `auto` 的非模板参数，前提是我们可以在特化中推导出该非模板参数的类型。

```cpp
template <class T auto J>
void func(T t, auto x) { }
func("string", 10); // 推导出 J 为 int
```

在此示例中，`auto` 被推导为 `int` 类型。

## 现代 C++：嵌套命名空间 (C++17)

考虑以下嵌套命名空间：

```cpp
namespace A {
    namespace B {
        namespace C {
            int x = 100;
        }
    }
}
```

在 C++17 中，我们可以这样指定嵌套命名空间 C：

```cpp
namespace A::B::C {
    int x = 100;
}
```

这是一个示例：

```cpp
#include <iostream>
namespace A {
    int a = 1;
}
namespace A::B {
    int b = 2;
}
namespace A::B::C {
    int c = 3;
}

int main() {
    std::cout << A::a << " " << A::B::b << " " << A::B::C::c << std::endl;
}

// 输出
1 2 3
```

# 现代 C++：Constexpr If 语句 (C++17)

假设我们有一个可以在编译时评估的 if 语句，那么 C++ 允许我们根据常量 if 表达式的评估结果，在编译时丢弃该 if 语句的分支。使用如下语法：

```cpp
if constexpr(condition) {
    statement1; // 如果条件为假，则丢弃
} else {
    statement2; // 如果条件为真，则丢弃
}
```

这是一个使用该特性的示例（类型特性）：

```cpp
// std::is_integral<T> 谓词函数在 T 为整数类型时返回 true
// 否则返回 false
#include <iostream>
#include <type_traits>

template <typename T>
constexpr bool IntegralTest()
{
    if constexpr (std::is_integral<T>::value) {
        return true;
    }
    else {
        return false;
    }
}

int main()
{
    static_assert(IntegralTest<int>() == true);
    static_assert(IntegralTest<char>() == true);
    // static_assert(IntegralTest<char*>() == true); // 这会导致失败
}
```

# 现代 C++ Auto 类型的初始化 (C++17)

先参阅：`std::initializer_list`

C++ 中的变量初始化有几种形式：

```cpp
默认初始化          std::string s;
默认大括号初始化    std::string s { };
直接初始化           std::string s("hello");
拷贝赋值初始化      std::string s = "hello";
列表初始化          std::string s = {'h', 'e', 'l', 'l', 'o'};

聚合初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};

引用初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};
char& c = s[1];
```

C++11 引入了使用初始化列表的通用语法，通常被称为大括号列表初始化。大括号列表初始化有两种类型：

- 直接列表初始化：`T object {arg1, arg2, ...}`
- 拷贝列表初始化：`T object = {arg1, arg2, ...}`

在 C++17 下，大括号初始化的 `auto` 变量的类型推导遵循类型推导规则：

- 对于直接列表初始化，如果初始化列表有一个类型为 `T` 的单个元素，编译器将为 `auto` 类型变量推导出类型 `T`。如果初始化列表中有多个元素，则是非合法的。
- 对于拷贝列表初始化，如果列表中的所有元素具有相同类型，编译器将从 `std::initializer_list<T>` 推导出 `auto` 变量的类型，否则 `auto` 类型变量将是非法的。

由于这些规则，上述示例变为：

- `auto b {42};` // OK，推导为 int
- `auto d {1, 2};` // 错误，初始化器过多
- `auto a {42};` // OK，std::initializer_list<int>
- `auto c = {1, 2};` // OK，std::initializer_list<int>
- `auto d = {1, 2, 13};` // 错误，初始化列表类型不同

```cpp
auto b {42}; // OK，推导出 int
auto d {1, 2}; // 错误，初始化器过多
auto a {42}; // OK，std::initializer_list<int>
auto c = {1, 2}; // OK，std::initializer_list<int>
auto d = {1, 2, 13}; // 错误，初始化列表类型不同
```

```cpp
#include <iostream>
int main() {
    auto b {42}; // OK，推导出 int
    auto d {1, 2}; // 错误，初始化器过多
    auto a {42}; // OK，std::initializer_list<int>
    auto c = {1, 2}; // OK，std::initializer_list<int>
    // auto d = {1, 2, 13}; // 错误，初始化列表类型不同
    return 0;
}
```

## 现代 C++：结构绑定 (C++17)

结构绑定允许将对象（如结构体、数组或元组）解构为独立的变量。

```cpp
#include <iostream>
struct Point {
    int x;
    int y;
};

int main() {
    Point p{1, 2};
    auto [x, y] = p;
    std::cout << x << " " << y << std::endl;

    int arr[] = {1, 2};
    auto [a, b] = arr;
    std::cout << a << " " << b << std::endl;

    return 0;
}
```
