

brackets.

无论这些参数本身是否依赖于模板参数，模板名称后跟尖括号中的参数的组合称为 *template-id*。

这个名称可以像对应的非模板实体一样使用。例如：Click here to view code image

```
int main()
{
ArrayInClass<double,10>
ad; ad.array[0] = 1.0;
}
```

必须区分 *template parameters* 和 *template arguments*。简而言之，可以说“*parameters* 由 *arguments* 初始化。”⁴

- *Template parameters* 是在模板声明或定义中 `template` 关键字之后列出的那些名称（在我们的示例中为 T 和 N）。
- *Template arguments* 是替换模板参数的项（在我们的示例中为 `double` 和 `10`）。与模板参数不同，模板参数不仅仅是“名称”。

模板参数被模板参数替换在用 template-id 指示时是显式的，但在各种情况下替换是隐式的（例如，如果模板参数被其默认参数替换）。

一个基本原则是，任何模板参数都必须是可以在编译时确定的量或值。正如后面会变得清楚的那样，这一要求转化为模板实体的运行时间成本的巨大好处。因为模板参数最终会被编译时值替换，所以它们本身就可以用来形成编译时表达式。这在 `ArrayInClass` 模板中被用来确定成员数组 `array` 的大小。数组的大小必须是 *constant-expression*，而模板参数 N 符合这一条件。

我们可以将这一推理再推进一步：因为模板参数是编译时实体，所以它们也可以用来创建有效的模板参数。以下是一个示例：Click here to view code image

```
template<typename T>
class Dozen {
public:
ArrayInClass<T,12> contents;
};
```

注意在这个示例中，名称 T 既是模板参数也是模板参数。因此，有一种机制可以使我们从更简单的模板构建更复杂的模板。当然，这与允许我们组装类型和函数的机制在根本上并没有什么不同。

# 10.6 Summary

- 对类、函数和变量分别使用 *class template*、*function template* 和 *variable template*，如果它们是模板。
- *Template instantiation* 是通过用具体的 *arguments* 替换模板 *parameters* 来创建常规类或函数的过程。 resulting entity is a *specialization*。
- 类型可以是完整的或不完整的。
- 根据单一定义规则（ODR），非内联函数、成员函数、全局变量和静态数据成员在整个程序中只能定义一次。

1 在 C++ 中，`class` 和 `struct` 之间的唯一区别是 `class` 的默认访问权限为 `private`，而 `struct` 的默认访问权限为 `public`。然而，我们更喜欢对使用新 C++ 特性的类型使用 `class`，而对可作为“普通旧数据”（POD）使用的普通 C 数据结构使用 `struct`。

2 默认函数是特殊的成员函数，编译器会为其提供默认实现，例如默认拷贝构造函数。

3 自 C++17 起，全局变量、静态变量和数据成员可以定义为 `inline`。这消除了它们必须在恰好一个翻译单元中定义的要求。

4 在学术界，*arguments* 有时被称为 *actual parameters*，而 *parameters* 被称为 *formal parameters*。

• 具有重载 operator() 的类类型（有时称为仿函数），包括 lambda • 具有产生指向函数指针或引用到函数的转换函数的类类型 统称为函数对象类型，这类类型的值是函数对象。157

C++ 标准库引入了稍广的概念 callable type，即函数对象类型或指向成员的指针。callable 类型对象是 callable object，我们为方便起见称之为 callable。

通用代码通常受益于能够接受任何类型的 callable，而模板使得做到这一点成为可能。

# 11.1.1 Supporting Function Objects

让我们看看标准库的 for_each() 算法是如何实现的（使用我们自己的名称“foreach”以避免名称冲突，并且为简单起见跳过返回任何内容）：Click here to view code image

basics/foreach.hpp

```
template<typename Iter, typename Callable>
void foreach (Iter current, Iter end, Callable op)
{
while (current != end) { //as long as not reached the end
op(*current); // call passed operator for current element
++current; // and move iterator to next element
}
}
```

以下程序演示了此模板与各种函数对象的用法：Click here to view code image

basics/foreach.cpp

```
#include <iostream>
#include <vector>
#include "foreach.hpp"

// a function to call:
void func(int i)
{ std::cout << "func() called for: " << i << '\n';
}

// a function object type (for objects that can be used as functions):
```

```
```cpp
class FuncObj {
public:
void operator() (int i) const { //Note: const member function
std::cout << "FuncObj::op() called for: " << i << '\n';
}
};

int main()
{
std::vector<int> primes = { 2, 3, 5, 7, 11, 13, 17, 19 };
foreach(primes.begin(), primes.end(), // range
func); // function as callable (decays to pointer)
foreach(primes.begin(), primes.end(), // range
&func); // function pointer as callable
foreach(primes.begin(), primes.end(), // range
FuncObj()); // function object as callable
foreach(primes.begin(), primes.end(), // range
[] (int i) { //lambda as callable
std::cout << "lambda called for: " << i << '\n';
});
}
```
```

让我们详细查看每种情况：• 当我们将函数名作为函数参数传递时，我们实际上并没有传递函数本身，而是传递指向它的指针或引用。与数组一样（参见第 7.4 节第 115 页），函数参数在按值传递时会 *decay* 为指针，并且在参数类型为模板参数的情况下，会推导出指向函数的指针类型。

与数组一样，函数也可以通过引用传递而不会衰减。然而，函数类型实际上不能用 const 限定。如果我们将 `foreach()` 的最后一个参数声明为类型 `Callable const&`，const 只是会被忽略。一般来说，函数引用在主流 C++ 代码中很少使用。• 我们的第二次调用通过传递函数名的地址显式地采用函数指针。这与第一次调用（函数名隐式衰减为指针值）等价，但可能更清晰一些。

• 当传递仿函数时，我们将类类型对象作为 callable 传递。通过类类型调用通常相当于调用其 `operator()`。因此调用 `op(*current);` 通常被转换为

[Click here to view code image](#)

```
```cpp
op.operator()(*current); // call operator() with parameter
                         // *current for op
```
```

注意在定义 `operator()` 时，你通常应该将其定义为

```
#include <functional>

template<typename Iter, typename Callable, typename... Args>
void foreach (Iter current, Iter end, Callable op, Args const&... args)
{
while (current != end) { //as long as not reached the end of the elements
std::invoke(op, //call passed callable with
args..., //any additional args
*current); // and the current element
++current;
}
}
```

在这里，除了 callable 参数之外，我们还接受任意数量的额外参数。foreach() 模板然后使用给定的 callable，后跟给定的额外参数以及引用的元素调用 std::invoke()。std::invoke() 按如下方式处理：• 如果 callable 是指向成员的指针，它使用第一个额外参数作为 this 对象。所有剩余的额外参数只是作为参数传递给 callable。

• 否则，所有额外参数只是作为参数传递给 callable。

注意我们不能在这里为 callable 或额外参数使用完美转发：第一次调用可能会“窃取”它们的值，导致在后续迭代中调用 op 时出现意外行为。

有了这个实现，我们仍然可以编译上面对 foreach() 的原始调用。现在，此外，我们还可以向 callable 传递额外参数，并且 callable 可以是成员函数。¹ 以下客户端代码说明了这一点：Click here to view code image

# basics/foreachinvoke.cpp

```
#include <iostream>
#include <vector>
#include <string>
#include "foreachinvoke.hpp"

// a class with a member function that shall be called
class MyClass {
public:
void memfunc(int i) const {
std::cout << "MyClass::memfunc() called for: " << i << '\n';
}
};
```

