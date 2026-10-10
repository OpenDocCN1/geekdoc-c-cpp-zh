
输出：
5 4 3 2 1

上述初始化 `IntArray array { 5, 4, 3, 2, 1 };` 无法编译，因为 `IntArray` 类没有处理初始化列表的构造函数。

在 C++11 中，当编译器使用大括号初始化列表时，它会隐式地转换为 `std::initializer_list<T>`。所有 STL 容器都有接受初始化列表作为参数的构造函数。这使得向量支持大括号初始化。

在 C++11 之前，初始化向量的唯一方法是这样的：

```cpp
std::vector<int> vec1;
for(int i = 0; i < 5; i++)
vec1.push_back(i);
```

但自 C++11 起，`std::vector` 包含了初始化列表构造函数，因此我们可以这样初始化向量：

```cpp
// C++11 之前错误
std::vector<int> vec = {1,2,3,4,5};
```

或者：

```cpp
std::vector<int> vec {1,2,3,4,5};
```

每当编译器看到大括号初始化列表 `{1,5,6,9,4}`，它都会隐创建一个 `std::initializer_list<T>` 对象，其中 `T` 是列表的数据类型。

我们可以这样创建 `std::initializer_list<T>` 的轻量对象：

```cpp
#include <initializer_list>
std::initializer_list<int> data = {1,2,3,4,5};
```

`std::initializer_list<T>` 是一个类似数组的容器。它具有以下函数：

- `size()`：返回列表的大小
- `begin()`：返回列表起始的迭代器
- `end()`：返回列表结束的迭代器

# 现代 C++：explicit 关键字 (C++11)

C++ 编译器会在需要时隐式执行类型转换。示例：

```cpp
int x = 3;
float y = x + 5.5;
```

在执行加法之前，`x` 会被转换为浮点数类型。隐式类型转换通常涉及类型扩展。

我们可以使用 `explicit` 关键字防止编译器隐式转换类型。`explicit` 常用于修饰构造函数。考虑以下示例：

```cpp
class Array {
    public:
        explicit Array(size_t x);
};
```

这将防止构造函数中参数 `x` 的隐式类型转换。

# 现代 C++：基于范围的循环 (C++11)

C++11 引入了一种新的循环类型，它可以遍历范围中的所有元素。范围是指任何具有迭代器的集合。基于范围的循环的语法如下：

```cpp
for (type item : collection) {
  statements
}
```

`item` 是从集合中接收的元素。`item` 必须声明一个类型。对于集合中的每个元素，循环体中的语句都会被执行：

```cpp
for (int item : { 2, 3, 5, 7, 9, 13, 17, 19 }) {
  std::cout << item << std::endl;
}
```

注意，在例示例中，我们正在遍历 `{2, 3, 5...}`，这是一个 `std::initializer_list` 对象。

假设我们想将 `double` 类型向量 `vec` 的每个元素乘以 3，我们可以这样编写程序：

```cpp
std::vector<double> vec { 1.4, 5.34, 7.9 };
...
for (auto& element : vec) {
  element *= 3;
}
```

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>
int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
// 输出
1 2 3 4 5 6 7 8 9 10
```

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

# 现代 C++：Lambda 表达式 (C++11)

Lambda 在 C++11 中引入的。Lambda 是一个无名或匿名函数。匿名函数没有函数名。

Lambda 可以赋值给变量、存储在变量中或用函数参数。如果我们想重用一个 Lambda，可以将其保存在变量中。

Lambda 非常用于创建短促的内联函数。

一个极简的 Lambda 函数没有参数，只需执行某些操作。这里是这样一个 Lambda 的示例：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们可以直接调用 Lambda，如下所示：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们还可以将 Lambda 赋值给变量，然后通过该变量调用 Lambda：

```cpp
#include <iostream>
int main() {
  auto my_var = []() {
    std::cout << "hello world" << std::endl;
  };
  my_var();
}
// 输出
hello world
```

Lambda 总是有一个 Lambda 引入符（lambda introducer）。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

## Lambda 规范

1. Lambda 引入符：强制性（也称为捕获句）
2. 参数列表：可选（也称为声明符）
3. `mutable` 规范：可选。
4. 异常规范：可选。
5. 尾随返回类型：可选。
6. Lambda 实体。

## Lambda 参数

在 Lambda 引入符和 Lambda 实体之间，我们可以在括号中指定 Lambda 将接收的参数。Lambda 引入符之后是 Lambda 实体。
