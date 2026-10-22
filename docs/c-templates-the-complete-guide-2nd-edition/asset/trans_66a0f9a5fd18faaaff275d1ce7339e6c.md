
```
Stack<Stack< int> > intStackStack; // OK with all C++ versions
```

如果你没有这样做，就会使用运算符 >>，从而导致语法错误：点击此处查看代码图片

```
Stack<Stack< int>> intStackStack; // ERROR before C++11
```

旧行为的原因在于，它有助于C++编译器的第一遍扫描在不依赖代码语义的情况下对源代码进行词法分析。然而，由于缺少空格是一个典型错误，需要相应的错误消息，因此无论如何都越来越需要考虑代码的语义。因此，在C++11中，通过“尖括号技巧”（详见第226页第13.3.1节）移除了两个闭合模板尖括号之间必须留空格的规则。

## 2.3 类模板的部分使用

类模板通常会对其实例化所针对的模板参数执行多种操作（包括构造和析构）。这可能会让人以为这些模板参数必须提供类模板所有成员函数所需的全部操作。但事实并非如此：模板参数只需提供实际需要的所有必要操作（而不是可能需要的操作）。

例如，如果类 `Stack<>` 提供了一个成员函数 `printOn()` 来打印整个栈的内容，该函数会对每个元素调用 `operator<<`：

```
template<typename T>
class Stack {
...
void printOn(std::ostream& strm) const {
for (T const& elem : elems) {
strm << elem << ' '; // call << for each element
}
}
};
```

你仍然可以将这个类用于没有定义 `operator<<` 的元素：

```
Stack<std::pair< int, int>> ps; // note: std::pair<> has no operator<< defined
ps.push({4, 5}); // OK
ps.push({6, 7}); // OK
std::cout << ps.top().first << '\n'; // OK
```

```
std::cout << ps.top().second << '\n'; // OK
```

只有当你对这样的栈调用 `printOn()` 时，代码才会产生错误，因为它无法为这种特定元素类型实例化 `operator<<` 的调用：点击此处查看代码图片

```
ps.printOn(std::cout); // ERROR: operator<< not supported for element type
```

### 2.3.1 概念

这就引出了一个问题：我们如何知道一个模板要能够被实例化需要哪些操作？术语“概念”（concept）通常用来表示模板库中反复要求的一组约束。例如，C++ 标准库依赖于随机访问迭代器（random access iterator）和可默认构造（default constructible）等概念。

目前（即截至 C++17），概念或多或少只能通过文档（例如代码注释）来表达。这可能成为一个严重的问题，因为不遵循约束会导致糟糕的错误消息（详见第143页第9.4节）。

多年来，一直有各种方法和尝试，希望将概念的定义和验证作为一种语言特性来支持。然而，直到 C++17，还没有任何一种方法被标准化。

自 C++11 起，你至少可以使用 `static_assert` 关键字和一些预定义的类型特征（type traits）来检查一些基本约束。例如：点击此处查看代码图片

```
template<typename T>
class C
{
static_assert(std::is_default_constructible<T>::value, "Class C requires default-constructible elements");
...};
```

如果没有这个断言，当需要默认构造函数时，编译仍然会失败。然而，此时的错误消息可能会包含从实例化的最初原因到检测到错误的实际模板定义的整个模板实例化历史（详见第143页第9.4节）。

然而，要检查例如类型 T 的对象是否提供了特定的成员函数，或者是否可以使用 `operator <` 进行比较，则需要更复杂的代码。有关此类代码的详细示例，请参见第436页第19.6.3节。

关于 C++ 概念的详细讨论，请参见[附录 E](#)。

## 2.4 友元

与其使用 `printOn()` 打印栈内容，不如为栈实现 `operator<<`。然而，像往常一样，`operator<<` 必须作为非成员函数实现，然后它可以内联调用 `printOn()`：

```cpp
template<typename T>
class Stack {
...
void printOn(std::ostream& strm) const {
...
}
friend std::ostream& operator<< (std::ostream& strm,
Stack<T> const& s) {
s.printOn(strm);
return strm;
}
};
```

注意，这意味着类 `Stack<>` 的 `operator<<` 不是函数模板，而是一个在需要时随类模板一起实例化的“普通”函数。²

然而，当试图*声明*友元函数并在之后*定义*它时，事情就变得更加复杂了。实际上，我们有两种选择：1. 我们可以隐式声明一个新的函数模板，它必须使用不同的模板参数，例如 U：

```cpp
template<typename T>
class Stack {
...
template<typename U>
friend std::ostream& operator<< (std::ostream&, Stack<U> const&);
};
```

无论是再次使用 T 还是跳过模板参数声明都是行不通的（要么内部的 T 隐藏了外部的 T，要么我们在命名空间作用域中声明了一个非模板函数）。

2. 我们可以将 `Stack<T>` 的输出运算符前置声明为一个模板，但这意味着我们必须首先前置声明 `Stack<T>`：

```
template<typename T>
class Stack;

template<typename T>
std::ostream& operator<< (std::ostream&, Stack<T> const&);
```

然后，我们可以将这个函数声明为友元：点击此处查看代码图片

```
template<typename T>
class Stack {
...
friend std::ostream& operator<< <T> (std::ostream&,
Stack<T> const&);
};
```

注意“函数名” `operator<<` 后面的 `<T>`。因此，我们将非成员函数模板的一个特化声明为友元。如果没有 `<T>`，我们将声明一个新的非模板函数。详见第211页第12.5.2节。

无论如何，你仍然可以将这个类用于没有定义 `operator<<` 的元素。只有对这个栈调用 `operator<<` 才会导致错误：点击此处查看代码图片

```
Stack<std::pair< int, int>> ps; // std::pair<> has no operator<<
defined
ps.push({4, 5}); // OK
ps.push({6, 7}); // OK
std::cout <<
ps.top().first << '\n'; // OK
std::cout <<
ps.top().second << '\n'; // OK
std::cout << ps << '\n'; // ERROR: operator<< not supported
// for element type
```

## 2.5 类模板的特化

你可以针对特定的模板参数对类模板进行特化。与函数模板的重载类似（见第15页第1.5节），特化类模板允许你针对某些类型优化实现，或者修复某些类型在类模板实例化时的错误行为。然而，如果你特化了一个类模板，你也必须特化所有的成员函数。虽然可以特化类模板的单个成员函数，但一旦你这样做了，就不能再特化该特化成员所属的整个类模板实例。

要特化一个类模板，你必须使用前导的 `template<>` 以及类模板所特化的类型说明来声明该类。这些类型用作模板参数，并且必须直接跟在类名后面：点击此处查看代码图片

```
template<>
class Stack<std::string> {
...;
};
```

对于这些特化，任何成员函数的定义都必须定义为“普通”成员函数，其中每次出现的 T 都被替换为特化类型：点击此处查看代码图片

```
void Stack<std::string>::push (std::string const& elem)
{
elems.push_back(elem); // append copy of passed elem
}
```

下面是一个针对类型 std::string 的 Stack<> 特化的完整示例：点击此处查看代码图片

basics/stack2.hpp

```
#include "stack1.hpp"
#include <deque>
#include <string>
#include <cassert>

template<>
class Stack<std::string> {
private:
std::deque<std::string> elems; // elements

public:
void push(std::string const&); // push element
void pop(); // pop element
std::string const& top() const; // return top element
bool empty() const { // return whether the stack is empty
return elems.empty();
}
};

void Stack<std::string>::push (std::string const& elem)
{
elems.push_back(elem); // append copy of passed elem
}

void Stack<std::string>::pop ()
```

