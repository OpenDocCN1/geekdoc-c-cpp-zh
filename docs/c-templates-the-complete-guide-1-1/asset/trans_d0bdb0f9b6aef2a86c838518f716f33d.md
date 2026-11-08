
## 12.4.2 包展开可以出现在哪里？

到目前为止，我们的示例都聚焦于使用包展开来产生一系列模板实参。事实上，只要语言的语法提供了以逗号分隔的列表，包展开基本上就可以用在任何地方，包括：

-   基类列表中
-   构造函数中的基类初始化器列表中
-   调用实参列表中（实参表达式的模式）
-   初始化器列表中（例如，在花括号初始化器列表中）
-   类模板、函数模板或别名模板的模板参数列表中
-   函数可以抛出的异常列表中（在 C++11 和 C++14 中已弃用，在 C++17 中不允许）
-   属性内部，如果该属性本身支持包展开（尽管 C++ 标准没有定义这样的属性）
-   指定声明的对齐方式时
-   指定 lambda 的捕获列表时
-   函数类型的参数列表中

我们已经见过其中三种（见第 63 页 4.4.2 节）。我们还提到过一种用法，它出现在一种包展开机制中，该机制不产生列表，而是产生以逗号分隔的列表（见第 175 页 6.2 节）。

这些包展开语境中，有些只是为了完整性而列出，因为我们将把注意力集中在仅出现在模板参数列表中的那些包展开上。在许多情况下，一旦你理解了上一节中的所有情形，就应该能够自己完成本节这里的示例。我们觉得有必要给出一个更明确的包展开语境。

基类列表中的包展开会展开为若干个直接基类。这种展开尤其有用：当聚合类需要展开为若干基类，并且其主要用途是继承一组混入（mixin）时（见第 206 页 12.4.1 节）。例如，下面的类模板会展开为针对每个模板参数列出的那组基类，且后面没有附加的基类：

```cpp
template<typename... Mixins>
class Point: public Mixins... { // base class pack expansion
  ...
};
```

```cpp
template<typename... Ts>
struct Values {
  template<Ts... Vs>
  struct Holder {
  };
};

int i;
Values<char, int, ...> values;
```

注意，一旦指定了 `Values` 的类型实参，传递给 `Values<...>::Holder` 的类型实参就应当具有固定长度；因此，参数包 `Vs` 不是变长参数包。

`Vs` 是一个非类型模板参数包，其中每个实际模板实参都可以具有不同的类型，具体由为模板类型参数包 `Ts` 提供的类型指定。注意，`Vs` 声明中的省略号具有双重作用：既声明模板参数包 `Vs`，又展开模板参数包 `Ts`。后一个参数包是一次包展开。

## 12.4.3 函数参数包

函数参数包是一种函数参数，它匹配零个或多个函数调用实参。与模板参数包类似，函数参数包通过在函数参数名之前（或代替函数参数名）使用省略号（...）来引入；同样与模板参数包类似，函数参数包在使用时必须由包展开来展开。模板参数包和函数参数包合称为参数包。

与模板参数包不同，函数参数包始终是包展开，因此其声明类型必须表示至少一个参数。在下面的示例中，我们引入一个新的 `Point` 构造函数，它用提供的构造函数实参分别复制初始化 `x`、`y` 和 `z` 成员：

```cpp
template<typename... T>
class Point : public Mixin<T...> {
  double x, y, z;
public:
  // Default constructor, virtual functions, etc. elided
  Point(Mixin<T...> mixins, ...)
    : x(...), y(...), z(...)
  { }
};

struct Color { char red, green, blue; };
struct Label { char const* string; };
Point<Color, Label> p(Color(?, ?, ?), Label("center"));
```

函数模板的函数参数包可以依赖于该模板中声明的非模板参数包，这使函数模板能够接受任意数量的调用实参而不丢失类型信息：

```cpp
template<typename... Types>
void print(Types... values);

int main()
{
  std::string welcome("Welcome to ");
  print(welcome, "2011", 2011, 17); // calls
  print<std::string, char const*, int, int>(welcome, "2011", 2011, 17);
}
```

当用若干实参调用函数模板 `print()` 时，实参的类型将被放入一个实参包，用于替换模板类型参数包 `Types`；而实际的实参值将被放入一个实参包，用于替换函数参数包 `values`。根据调用确定实参的过程在第 15 章中描述。目前只需注意，`Types` 中的类型就是 `values` 中值的类型，并且这两个参数包都可在函数模板 `print()` 的函数体内使用。

`print()` 的实际实现使用递归模板实例化，这是一种在第 23 页 6.1 节和第 2 章中描述的模板元编程技术。

出现在参数列表末尾的未命名函数参数包与 C 风格“可变参数”（varargs）参数之间存在语法歧义。例如：

```cpp
template<typename... T>
void print(T... values);

template<typename... T>
void print(T...);
```

在第一种情况下，`...` 被视为函数参数包，因为 `T` 是类型包，并且省略号放在参数名之后。在第二种情况下，`...` 反而被视为 C 风格可变参数：一个类型为 `T` 的未命名参数后面跟着可变参数省略号。可以通过在省略号和 C 风格可变参数之间添加逗号，或者在省略号后跟一个标识符来强制消除歧义，后者会使其成为命名的函数参数包。注意，一般而言，如果参数的类型是包展开，那么尾随的未命名函数参数包就是参数包。

## 12.4.5 零长度包展开

包展开的模式可以任意复杂，并且可以包含多个不同的参数包。实例化包展开时，模式必须以相同的长度展开。结果得到的类型序列或值序列将完全按照我们一直在做的方式形成：把每个参数包的第一个实参放入模式，接着放入每个参数包的第二个实参，依此类推。例如，下面的函数调用是错误的，因为该函数接受两个相同类型的实参：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_157_0.png)

```cpp
template<typename T, typename... Types>
void print(const T& firstArg, const Types&... args) {
    // ...
}
```

调用实参包展开命名了两个参数：`T` 和 `Types`。实例化此模板时，每个实参包的元素类型会替换对应包的元素。结果得到的实参列表由 N-1 个类型为 `T1, ..., TN-1` 的项组成，其中 `T` 是 `firstArg` 的类型。按照包展开的直观解释，三实参函数调用看起来会是这样：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_157_1.png)

```cpp
template<typename T, typename T1, typename T2, typename T3>
void print(const T& firstArg, const T1& arg1, const T2& arg2, const T3& arg3) {
    // ...
}
```

包展开本身也可以嵌套。在每种情况下，参数包的每次出现都由其最近的外围包展开来“展开”（仅由该包展开进行展开）。下面的示例展示了一个涉及三个不同参数包的嵌套包展开：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_157_2.png)

```cpp
template<typename... Types>
class Nested {
    public:
        template<typename... Inner>
        void f(const Inner&... innerValues) {
            g(printInnerValues(innerValues)...);
        }
};
```

在对 `f` 的调用中，模式为 `printInnerValues(innerValues)...` 的包展开是最内层包展开，它同时展开 `Inner` 和 `innerValues`，并产生一个实参序列，用于由 `printInnerValues` 返回的对象进行初始化。外层包展开模式包含内层包展开。因此，外层包展开展开 `Types` 和 `Inner` 两个包，并产生一个以逗号分隔的列表，其中的元素是内层展开产生的实参序列。按照包展开的直观解释，当 `innerValues` 有两个实参且 `Inner` 有三个实参时，下面的代码会更明显：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_157_3.png)

```cpp
template<typename... Types, typename... Inner>
void g(const Types&... args1, const Inner&... args2) {
    // ...
}
```

多重包展开和嵌套包展开是强大的工具（例如，见第 618 页 26.2.4 节）。

包展开的直观解释可以成为有用的工具，用来理解可变参数模板的实例化在实参数量不同时会如何表现。然而，在存在零长度实参包时，这种直观解释会失效。为说明这一点，考虑第 612 页 12.4.1 节中的 `count` 函数，任意地将其替换为零个实参：

```cpp
template<typename... Types>
size_t count() {
    return sizeof...(Types);
}
```

这段代码是对 count 函数的重写，它返回模板参数包中类型的数量。然而，当模板以零个实参实例化时，返回类型……

包展开实际上是语义构造，替换一个（大小为零的）实参包并不会影响该展开在模式中的处理方式。相反，当一个包展开作为单一实体展开时，模式（在语义上）会变成仿佛该列表不存在。实例化 `count<>()` 最终没有实参，因此得到的 `count()` 返回 `0`。然而，这似乎是合理的……

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_157_4.png)

```cpp
template<typename... Types>
void print(const Types&... args) {
    // ...
}
```
