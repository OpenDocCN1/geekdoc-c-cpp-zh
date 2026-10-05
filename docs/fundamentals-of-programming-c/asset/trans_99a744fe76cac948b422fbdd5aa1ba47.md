

## 18.1. 函数模板

```cpp
/*
 * less_than(a, b)
 * 如果 a < b 则返回 true；否则返回
 * false。
 */
template template <typename T>
bool less_than(T a, T b) {
    return a < b;
}

int main() {
    cout << less_than(2, 3) << endl;
    cout << less_than(2.2, 2.7) << endl;
    cout << less_than(2.7, 2.2) << endl;

    string word1 = "ABC", word2 = "XYZ";
    cout << less_than(word1, word2) << endl;
    cout << less_than(word2, word1) << endl;
}
```

列表 18.2 (templatelessthan.cpp) 的输出为：

| 1 |
| 1 |
| 0 |
| 1 |
| 0 |

在 **less_than <typename T>** 函数定义中：

```cpp
template <typename T>
bool less_than(T a, T b) {
    return a < b;
}
```

**template** 和 **typename** 是保留字，而 **T** 是一个 *类型参数*。**template** 关键字表示随后的函数定义不是普通函数，而是一个模式或模板，编译器可以据此生成正确的函数。函数也称为 *泛型函数*。**typename** 关键字表示其其后的标识符（在本例中为 **T**）是 C++ 类型名称的占位符。**T** 代表待确定的实际类型。它是一个标识符，可以取任何符合变量、函数或类法的名称；某些程序员会使用更具描述性的名称，例如 **CompareType** 或 **TypeParam**。像 **T** 和 **U** 这样的大写单个字母是 C++ 程序员中很流行的类型参数名称。就像函数或方法的普通参数代表一个值一样，模板参数代表一个类型。

在此语境下，你可以使用保留字 **class** 互替关键字 **typename**：

```cpp
template <class T>
bool less_than(T a, T b) {
    return a < b;
}
```

在列表 18.2 (templatelessthan.cpp) 中，编译器生成了三个不同的 less_than 函数：一个接受两个整数的，一个接受双双精度浮点值的，以及一个接受两个字符串对象的。尽管程序员在源代码中看不到它们，但编译器实际上创建了以下字面量函数定义：

```cpp
bool less_than(int a, int b) {
    return a < b;
}

bool less_than(double a, double b) {
    return a < b;
}

bool less_than(string a, string b) {
    return a < b;
}
```

当编译器从模板函数生成实际函数定义时，该过程称为模板实例化（template instantiation），不要与从类的实例化混淆。

编译器仅在需要时实例化函数。如果列表 18.2 (templatelessthan.cpp) 不包含 std::string 对象，那么处理源代码时就不会实例化接受两个 std::string 对象的 less_than 版本。

为了效率，编写 less_than 的最佳方式是：

```cpp
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}
```

注意 a 和 b 是通过引用传递的，而不是通过值。这意味着调用者仅传递对象 a 和 b 的地址，不需要为了发送函数而进行拷贝。如果 T 代表大型对象，这将产生巨大的差异。由于参数是 const 的，函数无法更改调用者参数的状态；因此，该函数提供了按值调用安全性，而没有拷贝参数的开销。

如果调用者尝试如下语句：

```cpp
cout << less_than(2, 2.2) << endl;
```

编译器会生成错误。这是因为模板定义指定其两个参数是相同的。字面量 2 是 int，字面量 2.2 是 double。编译器可以自动实例化接受两个 int 或两个 double 的 less_than 函数，但不支持混合类型。在表达式

```cpp
less_than(2, 2.2)
```

中编译器不知道调用哪个实例化的模板版本。

一种解决方案要求程序员显式实例化函数，如下所示：

```cpp
cout << less_than<int>(2, 2.2) << endl;
```

这强制编译器实例化并调用整数版本。编译器将发出关于截断 2.2 的警告。语句

```cpp
cout << less_than<double>(2, 2.2) << endl;
```

将使用 less_than 的双精度浮点值，它可以通过编译没有任何警告，因为将 int 2 视为 double 是自动的。

我们可以重写 less_than 模板函数以避免显式实例化的需要。为了获得最大的灵活性，我们可以将 less_than 模板函数表示为

```cpp
template <typename T, typename V>
bool less_than(const T& a, const V& b) {
  return a < b;
}
```

此版本使用了两个参数 T 和 V，它们可以代表不同的类型。有了这个新定义，以下使得：

当编译器看到如下代码时

```cpp
vector<int> v(10, 20, 30);
cout << sum(v) << endl;
```

它知道 v 的声明类型是 vector<int>；因此它使用模板中的模式实例化以下内容：

```cpp
// 编译器自动生成这个：
int sum(const vector<int>& v) {
    int result = 0;
    for (int elem : v) {
        result += elem;
    }
    return result;
}
```
