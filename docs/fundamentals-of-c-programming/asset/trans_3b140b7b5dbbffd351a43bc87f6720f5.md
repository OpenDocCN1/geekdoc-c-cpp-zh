

```cpp
bool less_than(T a, T b) {
    return a < b;
}

int main() {
    std::cout << std::boolalpha;
    std::cout << less_than(2, 3) << '\n';
    std::cout << less_than(2.2, 2.7) << '\n';
    std::cout << less_than(2.7, 2.2) << '\n';

    std::string word1 = "ABC", word2 = "XYZ";
    std::cout << less_than(word1, word2) << '\n';
    std::cout << less_than(word2, word1) << '\n';
}
```

清单 19.2 (templatelessthan.cpp) 的输出是

```
true
true
false
true
false
```

在 less_than 函数定义中：

```cpp
template <typename T>
bool less_than(T a, T b) {
    return a < b;
}
```

template 和 typename 是保留字，T 是类型参数。template 关键字表明，其后的函数定义不是普通的函数定义，而是一种模式或模板，编译器可尝试从中生成正确的函数定义。函数模板也称为泛型函数。typename 关键字表明，其后的标识符（在此例中为 T）是 C++ 类型名称的占位符。类型参数 T 代表在其他地方确定的实际类型。T 是一个标识符，因此可以使用任何作为变量、函数或类合法的名称；一些程序员更喜欢更具描述性的名称，例如 CompareType 或 TypeParam。T、S、U 和 V 等单个大写字母是 C++ 程序员中流行的类型参数名称。正如函数或方法的常规参数表示一个值一样，模板参数表示一个类型。

在此上下文中，您可以将保留字 class 与关键字 typename 互换使用：

```cpp
template <class T>
bool less_than(T a, T b) {
    return a < b;
}
```

在清单 19.2 (templatelessthan.cpp) 中，编译器生成三个不同的 less_than 函数：一个接受两个整数，一个接受两个双精度浮点值，一个接受两个字符串对象。尽管程序员在源代码中看不到它们，但编译器实际上会创建以下具体函数定义：

```cpp
bool less_than(int a, int b) {
    return a < b;
}
bool less_than(double a, double b) {
    return a < b;
}
bool less_than(std::string a, std::string b) {
    return a < b;
}
```

当编译器从模板函数生成实际函数定义时，此过程称为模板实例化，切勿与类的对象实例化混淆。

编译器仅在需要时实例化函数。如果清单 19.2 (templatelessthan.cpp) 不包含 std::string 对象，则在处理源代码时，编译器不会实例化接受两个 std::string 对象的 less_than 版本。

出于效率考虑，编写 less_than 的更好方式是

```cpp
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}
```

请注意，参数 a 和 b 是按引用传递，而非按值传递。这意味着调用者仅传递对象 a 和 b 的地址，无需制作副本发送到函数。如果 T 表示大对象，这可能会产生很大影响。由于参数是 const 引用，函数无法更改调用者实际参数的状态；因此，该函数提供了按值调用的安全性，而无需承担复制参数的开销。

如果调用者尝试类似下面的语句

```cpp
std::cout << less_than(2, 2.2) << '\n';
```

编译器会生成一个错误。这是因为模板定义指定其两个类型参数必须相同。字面量 2 是 int，字面量 2.2 是 double。编译器可以自动实例化接受两个 int 或两个 double 的 less_than 函数，但不能处理混合类型。在表达式

```cpp
less_than(2, 2.2)
```

编译器无法知道应该调用模板的哪个实例化版本。

一种解决方案要求程序员如下显式实例化函数：

```cpp
std::cout << less_than<int>(2, 2.2) << '\n';
```

这迫使编译器实例化并调用整数版本。编译器会发出关于截断 2.2 的警告。语句

```cpp
std::cout << less_than<double>(2, 2.2) << '\n';
```

将使用 less_than 的双精度浮点版本，并且可以干净地编译，没有警告，因为将 int 值 2 扩展为 double 是自动的。

我们可以重写 less_than 模板函数以避免显式实例化的需要。为了最大灵活性，我们可以将 less_than 模板函数表示为

```cpp
template <typename T, typename V>
bool less_than(const T& a, const V& b) {
    return a < b;
}
```

此版本使用两个类型参数 T 和 V，它们可以表示不同的类型。使用此新定义，以下所有语句均可接受：

```cpp
std::cout << less_than(2, 3) << '\n';
std::cout << less_than(2.2, 2.7) << '\n';
std::cout << less_than(2, 2.2) << '\n';
std::cout << less_than(2.2, 2) << '\n';
```

不需要显式模板实例化。给定此调用代码，编译器将自动实例化四个重载的 less_than 函数，如下所示：

- less_than(2, 3) 实例化为 `bool less_than(const int& a, const int& b)`
- less_than(2.2, 2.7) 实例化为 `bool less_than(const double& a, const double& b)`
- less_than(2, 2.2) 实例化为 `bool less_than(const int& a, const double& b)`
- less_than(2.2, 2) 实例化为 `bool less_than(const double& a, const int& b)`

虽然此更灵活的 less than 模板函数允许我们比较混合数值表达式，但通常期望两个参数为相同类型更合理。

回到我们的向量求和函数，我们可以将 sum 泛型地表示为

```cpp
template <typename T>
T sum(const std::vector<T>& v) {
    T result = 0;
    for (T elem : v)
        result += elem;
    return result;
}
```

与泛型 less_than 函数的情况一样，关键字 template 引入模板定义。紧随 template 关键字之后的尖括号 (<>) 包含模板参数声明。

当编译器看到类似下面的调用代码时

```cpp
std::vector<int> v {10, 20, 30};
std::cout << sum(v) << '\n';
```

它知道 v 的声明类型是 std::vector<int>；因此，它使用模板中的模式实例化一个看起来如下的实际函数：

```cpp
// The compiler automatically generates this from the template:
int sum(const std::vector<int>& v) {
    int result = 0;
    for (int elem : v)
        result += elem;
    return result;
}
```

请注意，编译器只是将 int 替换为类型参数 T 的每个出现。如果编译器看到类似下面的代码

```cpp
std::vector<double> v {10, 20, 30};
std::cout << sum(v) << '\n';
```

它再次使用模板实例化以下函数：

```cpp
// The compiler automatically generates this:
double sum(const std::vector<double>& v) {
    double result = 0;
    for (double elem : v)
        result += elem;
    return result;
}
```

在包含类似下面代码的程序中

```cpp
std::vector<double> v {10, 20, 30};
std::vector<int> w {10, 20, 30};
std::cout << sum(v) << '\n';
std::cout << sum(w) << '\n';
```

编译器将实例化 sum 函数的两个版本。编译器会自动且隐秘地生成这些函数。程序员永远看不到这些实例化的模板函数，因为它们不出现在任何源代码中。与将修改后的源代码版本发送到编译器的预处理器不同（参见第 1.2 节，回顾预处理器在程序构建过程中的作用），现代 C++ 编译器直接从程序员的源代码生成这些实例化函数的机器语言版本。

回顾我们来自清单 10.19 (swapwithreferences.cpp) 的 swap 函数。调用者可以使用它来交换两个整数值的值。凭借对 C++ 模板的了解，我们现在可以编写一个泛型版本，用于交换任何类型的两个变量的值：

```
/*
 * swap(a, b)
 *   Interchanges the values of memory
 *   referenced by its parameters a and b.
 *   It effectively interchanges the values
 *   of variables in the caller's context.
 */
```

```cpp
template <typename ElemType>
void swap(ElemType& a, ElemType& b) {
    ElemType temp = a;
    a = b;
    b = temp;
}
```

唯一的限制是两个参数必须是相同的类型。此处类型参数的名称是 ElemType。此 swap 函数工作正常，但我们无需自己编写此类函数；C++ 标准库包含一个 std::swap 模板函数，它的作用与上面所示的 swap 函数相同。

以下函数将打印任何类型的向量的内容：

