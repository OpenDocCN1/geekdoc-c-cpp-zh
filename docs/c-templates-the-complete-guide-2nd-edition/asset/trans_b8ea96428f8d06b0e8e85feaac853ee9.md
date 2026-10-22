

## 可变参数模板的完美转发

完美转发与可变参数模板结合得很好，允许一个函数模板接受任意数量的函数调用参数并将每个参数转发给另一个函数：Click here to view code image

```
template<typename... Ts> void forwardToG(Ts&&... xs)
{
g(std::forward<Ts>(xs)...); // forward all xs to g()
}
```

对 forwardToG() 的调用会（独立地）为参数包 Ts 推导出连续的值（参见第 15.5 节第 275 页），从而捕获每个参数的类型以及左值或右值属性。调用 g() 中的参数包展开（参见第 12.4.1 节第 201 页）然后使用上面解释的完美转发技术转发这些参数中的每一个。

尽管其名称如此，完美转发实际上并非“完美”，因为它并不能捕获表达式的所有有趣属性。例如，它无法区分左值是否为位域左值，也无法捕获表达式是否具有特定常量值。后者在使用空指针常量时尤其会造成问题，空指针常量是求值为常量值零的整型值。由于表达式的常量值未被完美转发捕获，因此以下示例中对 g() 的直接调用与对 g() 的转发调用的重载决议行为会不同：Click here to view code image

```
void g(int*);
void g(...);

template<typename T> void forwardToG(T&& x)
{
g(std::forward<T>(x)); // forward x to g()
}

void foo()
{
g(0); // calls g(int*)
forwardToG(0); // eventually calls g(...)
}
```

这又是使用 nullptr（在 C++11 中引入）而不是空指针常量的另一个原因：Click here to view code image

```
g(nullptr); // calls g(int*)
forwardToG(nullptr); // eventually calls g(int*)
```

resolution.⁷

例如，考虑一对函数模板，用于提取容器或数组的开始迭代器：Click here to view code image

```
template<typename T, unsigned N>
T* begin(T (&array)[N])
{
return array;
}

template<typename Container>
typename Container::iterator begin(Container& c)
{
return c.begin();
}

int main()
{
std::vector<int> v;
int a[10];

::begin(v); // OK: only container begin() matches, because the first deduction fails
::begin(a); // OK: only array begin() matches, because the second substitution fails
}
```

对 begin() 的第一次调用，其中参数为 std::vector<int>，会尝试对两个 begin() 函数模板进行模板参数推导：
- 对数组 begin() 的模板参数推导失败，因为 std::vector 不是数组，因此被忽略。
- 对容器 begin() 的模板参数推导成功，Container 推导为 std::vector<int>，因此函数模板被实例化并调用。

对 begin() 的第二次调用，其中参数为数组，也会部分失败：
- 对数组 begin() 的推导成功，T 推导为 int，N 推导为 10。
- 对容器 begin() 的推导确定 Container 应被替换为 int[10]。虽然通常这种替换是可以的，但产生的返回类型 Container::iterator 是无效的，因为数组类型没有名为 iterator 的嵌套类型。在任何其他上下文中，尝试访问不存在的嵌套类型都会导致立即的编译时错误。在模板参数的替换期间，SFINAE 将此类错误转换为推导失败，并将函数模板从

考虑中移除。因此，第二个 begin() 候选被忽略，并调用第一个 begin() 函数模板的特化。

## 15.7.1 立即上下文

SFINAE 保护免受在函数模板替换的立即上下文中形成无效类型或表达式的尝试，包括由于歧义或访问控制违规而导致的错误。定义函数模板替换的立即上下文最容易通过定义其不在该上下文中的内容来完成。⁸ 具体来说，在为推导目的进行函数模板替换期间，以下内容中的任何事情都不是该函数模板替换的立即上下文的一部分：
- 类模板的定义（即其“主体”和基类列表），
- 函数模板的定义（“主体”以及在构造函数的情况下，其构造函数初始值设定项），
- 变量模板的初始值设定项，
- 默认参数，
- 默认成员初始值设定项，或
- 异常规范

替换过程中触发的特殊成员函数的任何隐式定义也不是该替换的立即上下文的一部分。其余一切都是该上下文的一部分。

因此，如果替换函数模板声明的模板参数需要实例化类模板的主体，因为正在引用该类的成员，则该实例化期间发生的错误不在函数模板替换的立即上下文中，因此是真正的错误（即使另一个函数模板在没有错误的情况下匹配）。例如：

Click here to view code image

```
template<typename T>
class Array {
public:
using iterator = T*;
};

template<typename T>
void f(Array<T>::iterator first, Array<T>::iterator last);

template<typename T>
void f(T*, T*);

int main()
```

```
{
f<int&>(0, 0);// ERROR: substituting int& for T in the first function template
} // instantiates Array<int&>, which then fails
```

此示例与前一个示例的主要区别在于失败发生的位置。在前一个示例中，失败发生在形成类型 typename Container::iterator 时，该类型处于函数模板 begin() 替换的立即上下文中。在此示例中，失败发生在 Array<int&> 的实例化中，虽然它是由函数模板的上下文触发的，但实际上发生在类模板 Array 的上下文中。因此，SFINAE 原则不适用，编译器会产生错误。

下面是一个 C++14 示例——依赖于推导返回类型（参见第 15.10.1 节第 296 页）——涉及在函数模板定义实例化期间发生的错误：Click here to view code image

```
template<typename T> auto f(T p) {
return p->m;
}

int f(...);

template<typename T> auto g(T p) -> decltype(f(p));

int main()
{
g(42);
}
```

调用 g(42) 将 T 推导为 int。在 g() 的声明中进行该替换需要我们确定 f(p) 的类型（其中 p 现在已知为 int 类型），因此需要确定 f() 的返回类型。f() 有两个候选。非模板候选是匹配的，但不是很好的匹配，因为它使用省略号参数匹配。不幸的是，模板候选具有推导返回类型，因此我们必须实例化其定义以确定该返回类型。该实例化失败，因为当 p 为 int 时 p->m 无效，并且由于失败发生在替换的立即上下文之外（因为它在函数定义的后续实例化中），失败会产生错误。因此，我们建议避免使用推导返回类型，如果它们可以很容易地显式指定。

SFINAE 最初旨在消除由于函数模板重载的非预期匹配而导致的令人惊讶的错误，如容器 begin() 示例所示。然而，检测无效表达式或类型的能力使得出色的编译时技术成为可能，允许确定特定语法是否有效。这些技术在第 19.4 节第 416 页中讨论。

请特别参阅第 19.4.4 节第 424 页，了解使类型特征 *SFINAE-friendly* 以避免由于 *immediate context* 问题而产生问题的示例。

## 15.8 推导的限制

模板参数推导是一个强大的功能，消除了在大多数对函数模板的调用中显式指定模板参数的需要，并同时实现了函数模板重载（参见第 1.5 节第 15 页）和部分类模板特化（参见第 16.4 节第 347 页）。然而，使用模板时程序员可能会遇到一些限制，这些限制在本节中讨论。

### 15.8.1 允许的参数转换

通常，模板推导尝试找到函数模板参数的替换，使得参数化类型 *P* 与类型 *A* 相同。然而，当这不可能时，只要 *P* 包含在推导上下文中的模板参数，以下差异是可以容忍的：
- 如果原始参数是用引用声明符声明的，则替换的 *P* 类型可能比 *A* 类型具有更多的 `const/volatile` 限定。
- 如果 *A* 类型是指针或指向成员的类型，则它可以通过限定转换（即添加 `const` 和/或 `volatile` 限定符的转换）转换为替换的 *P* 类型。
- 除非为转换运算符模板进行推导，否则替换的 *P* 类型可以是 *A* 类型的基类类型，或 *A* 为指针类型时所指向的类类型的基类类型的指针。例如：Click here to view code image

```
template<typename T>
class B {
};
```

```
template<typename T>
class D : public B<T> {
};
```

