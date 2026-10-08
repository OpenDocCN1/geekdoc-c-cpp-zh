
此行将参数包展开为独立的参数（并用逗号分隔），然后使用展开后的参数列表调用 `processValues()` 函数。模板始终至少一个模板参数 `T`。递归调用带有 `args...` 的 `processValues()` 的行为每次调用都是一个模板参数。

由于 `processValues()` 函数的实现是递归的，你需要一种停止递归的方法。这是通过实现一个只接受单个参数的 `processValues()` 模板来实现的。

你可以如下测试 `processValues()` 变长模板：

```cpp
processValues(1, 2, 3.56, "test", 1.1f);
```

此示例生成的递归调用如下：
`processValues(1, 2, 3.56, "test", 1.1f);`
`handleValue(1);`
`processValues(2, 3.56, "test", 1.1f);`
`handleValue(2);`
`processValues(3.56, "test", 1.1f);`
`handleValue(3.56);`
`processValues("test", 1.1f);`
`handleValue("test");`
`processValues(1.1f);`
`handleValue(1.1f);`

重要的是，这种变长参数列表的方法是完全类型安全的。`processValues()` 函数会根据实际类型自动调用正确的 `handleValue()` 重载。自动类型转换可以在 C++ 中像常一样发生。例如，前一个示例中的 `1.1f` 是 `float` 类型。`processValues()` 函数调用 `handleValue(double value)`，因为从 `float` 转换为 `double` 不产生任何损失。然而，当你用某种类型的参数调用 `processValues()` 时，如果该类型没有定义 `handleValue()`，编译器将发出错误。

但上述实现存在一个问题。由于它是递归实现，由于参数在每次对 `processValues()` 的递归调用中都会被复制。取决于参数的类型，这可能会代价很高。你可能会认为可以通过向 `processValues()` 传递引用而不是按值传递来避免。遗憾的是，这意味着不能再用字面量调用 `processValues()`，因为不允许对字面量取引用，除非你使用 const 引用。

为了使用非 const 引用并允许字面量，可以使用第10章中讨论的值引用。下面的实现使用了值引用和 `std::forward()` 来完美转发所有参数。如果将值引用传递给 `processValues()`，

```cpp
template<typename T1, typename... Tn>
void processValues(T1 arg, Tn&&... args) {
    handleValue(std::forward<T1>(arg));
    (processValues(std::forward<Tn>(args)), ...);
}

template<typename T>
void processValues(T&& arg) {
    handleValue(std::forward<T>(arg));
}
```

## Mixin 类

变长模板允许你创建类型安全的变长参数列表。下面的示例定义了一个名为 `processValues()` 的变长模板，使其能够以类型安全的方式接受任意数量不同类型的参数。`processValues` 函数处理变长参数列表中的每个值，并为每个单独的参数执行函数 `handleValue()`。这意味着你为你想要处理的每种类型准备一个 `handleValue()` 函数；在此例中为 `int`、`double` 和 `string`：

```cpp
class Mixin {
public:
    Mixin(int i) : mValue(i) {}
    void MixinFunc() { cout << "Mixin: " << mValue << endl; }
private:
    int mValue;
};

class Mixin2 {
public:
    Mixin2(int i) : mValue(i) {}
    void Mixin2Func() { cout << "Mixin2: " << mValue << endl; }
private:
    int mValue;
};

template<typename... Mixins>
class MyClass : public Mixins... {
public:
    MyClass(Mixins&&... mixins) : Mixins(mixins)... {}
    virtual ~MyClass() {}
};
```

```cpp
MyClass<Mixin, Mixin2> a(Mixin(11), Mixin2(22));

a.MixinFunc();

a.Mixin2Func();

MyClass<Mixin> b(Mixin(33));

b.MixinFunc();

// b.Mixin2Func(); // 错误：无法编译。
```

模板元编程的目标是在编译时执行某些计算，而不是运行时。它基本上是 C++ 之上的层编程语言。接下来的章节将通过一个简单的示例，讨论如何在编译时计算数字的阶乘，并使结果在运行时作为一个简单的常量可用。

# 编译时计算阶乘

模板元编程允许你在编译时进行计算，而不是运行时。以下代码是一个在编译时计算某个数字阶乘的小型示例。该代码使用了模板递归（在本章较早部分解释过），它需要一个递归模板和一个用于停止递归的基模板。根据数学定义，0 的阶乘是 1，因此它被用作基础情况。

```cpp
template<unsigned char f>
class Factorial {
  public:
    static const unsigned long long val = (f * Factorial<f - 1>::val);
};

template<> class Factorial<0> {
  public:
    static const unsigned long long val = 1;
};

int main() {
  cout << Factorial<6>::val << endl;
  return 0;
}
```

这计算了 6 的阶乘，数学上写为 6!，即 1x2x3x4x5x6 或 720。

> 注意：请记住，阶乘计算是在编译时发生的。在运行时，你只需要通过 `:val` 访问编译时计算的值，它仅仅是一个静态常量值。

# 循环展开

模板元编程的另一个示例是在编译时展开循环，而不是在运行时执行循环。注意，循环展开应该只在确实需要时才进行，因为编译器通常足够智能，能够自动展开那些可以展开的循环。

这个示例再次使用了模板递归，因为它需要在编译时在循环中执行执行某些操作。对于模板递归，你需要模板的递归实现以及用于停止递归的基模板。在每次递归中，`Loop` 模板使用 `i-1` 实例化它自己。当它遇到 0 时，递归停止。

```cpp
template<int i>
class Loop
{
public:
    template <typename FuncType>
    static inline void Do(FuncType func) {
        Loop<i - 1>::Do(func);
        func(i);
    }
};
```

```cpp
template<int i>
class Loop<0>
{
public:
    template <typename FuncType>
    static inline void Do(FuncType /* func */) { }
};
```

`Loop` 可以像下面所示使用：

```cpp
void DoWork(int i) { cout << "DoWork " << i << endl; }

{
    Loop<3>::Do(DoWork);
}
```

这段代码会导致编译器展开循环并连续调用三次 `DoWork()` 函数。程序的输出为：

```
DoWork(1)
DoWork(2)
DoWork(3)
```

使用 `std::bind()` 来使用接受多个参数的 `DoWork()` 版本：

```cpp
void DoWork2(string str, int i)
{
    cout << "DoWork2 " << str << " " << i << endl;
}

int main() {
    Loop<2>::Do(bind(DoWork2, "TestStr", placeholders::_1));
}
```

代码首先实现了一个接受字符串和整数的函数。`main()` 函数使用 `std::bind()` 将 `DoWork2()` 的第一个参数绑定到固定字符串 "TestStr"。有关 `std::bind()` 的细节请参阅第 17 章。如果你编译并运行这段代码，输出如下：

```
DoWork2(TestStr, 1)
DoWork2(TestStr, 2)
```

# 打印元组

此示例使用模板元编程打印 `std::tuple` 的各个元素。元组在第 19 章中介绍。它们允许存储任意数量的值，每个值都有其特定的类型。`tuple` 具有固定的大小和固定的类型，这些是在编译时确定的。然而，元组没有内置机制来遍历它们的元素。以下示例展示了如何使用模板元编程在编译时遍历 `tuple` 的元素。

正如模板元编程中常见的情况，此示例再次使用了模板递归。`tuple_print` 类有两个模板参数：元组类型以及一个初始化为元组大小的整数。它在构造函数中递归地实例化自己，并在每次调用时递减该整数。`tuple_print` 的部分特化在整数变为零时停止递归。`main()` 函数展示了如何使用这个 `tuple_print` 类。

（注：由于原文中包含大量重复的 OCR 错误文本和混乱描述，译文已根据核心逻辑进行了清理和整合，以确保技术内容的准确与连贯。）

# 元编程 | 701

```cpp
typedef integral_constant<T,V> type;
constexpr operator value_type() const noexcept { return value; }
constexpr operator_type() const noexcept { return value; }
typedef integral_constant<bool, true> true_type;
typedef integral_constant<bool, false> false_type;
```

这段代码定义了两个类型：`true_type` 和 `false_type`。当你调用 `true_type::value` 时，你会得到该值；当调用 `false_type::value` 时，也会得到该值。你也可以调用 `true_type::type`，它返回值的类型。`false_type` 也是如此。`is_integral` 和 `is_class` 等类继承自 `integral_constant`。例如，可以将 `is_integral` 对 `bool` 类型进行特化：

```cpp
template<struct is_integral<bool> : public true_type { };
```

这允许你编写 `is_integral::value`，它返回布尔值。请注意，你不需要自己编写这些；它们是标准库的一部分。

以下代码展示了如何使用类别的简单示例：

```cpp
if (is_integral<int>()) {
    cout << "int is integral" << endl;
} else {
    cout << "int is not integral" << endl;
}
if (is_class<string>()) {
    cout << "string is a class" << endl;
} else {
    cout << "string is not a class" << endl;
}
```

这个示例使用 `is_integral` 来检查 `int` 是否为整数类型，并使用 `is_class` 来检查 `string` 是否为类。输出如下：

```
int is integral
string is a class
```

当然，你可能永远不会以这种方式使用类型属性（type traits）。它们在与模板结合时会变得更有用，可以根据类型的属性生成代码。下面的示例演示了这一点。代码定义了一个重载函数 `process_helper()`，它接受一个类型作为模板参数。该函数的第一个参数是一个值，第二个参数是 `true_type` 或 `false_type` 的实例。`process()` 模板函数接受单个参数并调用 `process_helper()`：

```cpp
template<typename T>
void process_helper(const T& t, true_type)
{
    cout << t << " is an integral type." << endl;
}
```

```cpp
template<typename T>
void process_helper(const T& t, false_type)
{
  cout << t << " is a non-integral type." << endl;
}
template<typename T>
void process(const T& t)
{
  process_helper(t, typename is_integral<T>::type());
}
```

调用 `process_helper()` 时的第二个参数是：`typename is_integral<T>::type`

这使用 `is_integral` 来确定 `t` 是否为整数类型。`::type` 返回结果的 `integral_constant` 类型，可以是 `true_type` 或 `false_type`。`process_helper()` 函数需要一个 `true_type` 或 `false_type` 的实例作为第二个参数，这就是为什么在 `::type` 之前有两个空括号。两个重载的 `process_helper()` 函数使用了类型为 `true_type` 和 `false_type` 的无名参数。它们之所以无名，是因为在函数体内部没有使用这些参数。这些参数仅用于函数重载解析。

代码可以如下进行测试：

```cpp
process(123);
process(2.2);
process(string(*Test));
```

该示例的输出如下：

```
123 is an integral type.
2.2 is a non-integral type.
Test is a non-integral type.
```

之前的示例可以使用仅 `process()` 函数模板来编写，如下所示，但这并没有演示如何编写其中一个参数为 `true_type` 或 `false_type` 的不同重载。

```cpp
template<typename T>
void process(const T& t)
{
  if (is_integral<T>::value) {
    cout << t << " is an integral type." << endl;
  } else {
    cout << t << " is a non-integral type." << endl;
  }
}
```

# 使用类型关系

有三种类型关系可用：`is_same`、`is_base_of` 和 `is_convertible`。本节给出了如何使用 `is_same` 的示例；其他的原理类似。

接下来的 `same ()` 函数模板使用 `is_same` 类型属性来判断两个参数是否为相同类型，并输出适当的消息。在 `main()` 函数中使用 `same ()` 函数模板非常简单：

```cpp
template<typename T1, typename T2>
void same(const T1& t1, const T2& t2)
{
    bool areTypesTheSame = is_same<T1, T2>::value;
    cout << "" << t1 << " and " << t2 << " are " <<
    cout << (areTypesTheSame ? "the same types." : "different types.") << endl;
}

int main() 
{
    same(1, 32);
    same(1, 3.01);
    same(3.01, string("Test"));
}
```
