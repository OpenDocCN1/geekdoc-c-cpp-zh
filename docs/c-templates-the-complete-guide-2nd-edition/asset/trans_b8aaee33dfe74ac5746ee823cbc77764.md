

```cpp
template<typename T1, typename T2>
class MyClass {
...
};
```

以下偏特化是可能的：点击此处查看代码图片

```cpp
// partial specialization: both template parameters have same type
template<typename T>
class MyClass<T,T> {
...
};
```

```cpp
// partial specialization: second type is int
template<typename T>
class MyClass<T,int> {
...
};
```

```cpp
// partial specialization: both template parameters are pointer types
template<typename T1, typename T2>
class MyClass<T1*,T2*> {
...
};
```

以下示例展示了哪个模板被哪个声明使用：点击此处查看代码图片

```cpp
MyClass<int, float> mif; // uses MyClass<T1,T2>
MyClass<float, float> mff; // uses MyClass<T,T>
MyClass<float, int> mfi; // uses MyClass<T,int>
MyClass<int*, float*> mp; // uses MyClass<T1*,T2*>
```

如果有多个偏特化匹配得同样好，则声明是二义的：点击此处查看代码图片

```cpp
MyClass<int, int> m; // ERROR: matches MyClass<T,T>
// and MyClass<T,int>
MyClass<int*, int*> m; // ERROR: matches MyClass<T,T>
// and MyClass<T1*,T2*>
```

要解决第二个二义性，你可以为相同类型的指针提供一个额外的偏特化：点击此处查看代码图片

```cpp
template<typename T>
class MyClass<T*,T*> {
...
};
```

关于偏特化的详细信息，请参见第347页的16.4节。

## 2.7 默认类模板实参

与函数模板一样，你可以为类模板参数定义默认值。例如，在类Stack<>中，你可以将用于管理元素的容器定义为第二个模板参数，并使用std::vector<>作为默认值：点击此处查看代码图片

basics/stack3.hpp

```cpp
#include <vector>
#include <cassert>

template<typename T, typename Cont = std::vector<T>>
class Stack {
private:
    Cont elems; // elements

public:
    void push(T const& elem); // push element
    void pop(); // pop element
    T const& top() const; // return top element
    bool empty() const { // return whether the stack is empty
        return elems.empty();
    }
};

template<typename T, typename Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem); // append copy of passed elem
}

template<typename T, typename Cont>
void Stack<T,Cont>::pop ()
{
    assert(!elems.empty());
    elems.pop_back(); // remove last element
}

template<typename T, typename Cont>
T const& Stack<T,Cont>::top () const
{
    assert(!elems.empty());
    return elems.back(); // return copy of last element
}
```

注意，我们现在有两个模板参数，因此每个成员函数的定义都必须使用这两个参数来定义：点击此处查看代码

![](img/0d5072d8203dcaf6ef50e76a3d9a3203_73_0.png)

```cpp
template<typename T, typename Cont>
void Stack<T,Cont>::push (T const& elem)
{
    elems.push_back(elem); // append copy of passed elem
}
```

你可以像以前一样使用这个栈。因此，如果你只传递第一个参数作为元素类型，就会使用一个vector来管理该类型的元素：[点击此处查看代码图片](#)

```cpp
template<typename T, typename Cont = std::vector<T>>
class Stack {
private:
    Cont elems; // elements
...
};
```

此外，你可以在程序中声明Stack对象时指定用于元素的容器：[点击此处查看代码图片](#)

basics/stack3test.cpp

```cpp
#include "stack3.hpp"

#include <iostream>

#include <deque>
int main()
{

    // stack of ints;
    Stack<int> intStack;

    // stack of doubles using a std::deque<> to manage the elements
    Stack<double, std::deque<double>> dblStack;

    // manipulate int stack
    intStack.push(7);
    std::cout << intStack.top() << '\n';
    intStack.pop();

    // manipulate double stack
    dblStack.push(42.4);
    std::cout << dblStack.top() << '\n';
    dblStack.pop();
}
```

使用声明类型别名时的语法。

## 别名模板

与`typedef`不同，别名声明可以被模板化，为一系列类型提供方便的名称。这也是自C++11起可用的，被称为*别名模板*。

以下别名模板DequeStack以元素类型T为参数，展开为一个将其元素存储在`std::deque`中的Stack：[点击此处查看代码图片](#)

```cpp
template<typename T>
using DequeStack = Stack<T, std::deque<T>>;
```

因此，类模板和别名模板都可以用作参数化类型。但同样，别名模板只是给现有类型起一个新名称，现有类型仍然可以使用。DequeStack<int>和Stack<int, std::deque<int>>表示相同的类型。

再次注意，一般来说，模板只能在全局/命名空间作用域内或类声明内部进行声明和定义。

### 成员类型的别名模板

别名模板对于为类模板的成员类型定义快捷方式尤其有用。在[点击此处查看代码图片](#)

```cpp
struct C {
typedef … iterator;
…
};
```

或：

[点击此处查看代码图片](#)

```cpp
struct MyType {
using iterator = …;
…
};
```

这样的定义

[点击此处查看代码图片](#)

```cpp
template<typename T>
using MyTypeIterator = typename MyType<T>::iterator;
```

允许使用

[点击此处查看代码图片](#)

```cpp
MyTypeIterator<int> pos;
```

而不是以下形式：⁵

点击此处查看代码图片

```cpp
typename MyType<T>::iterator pos;
```

### 类型特征后缀_t

自C++14起，标准库使用这种技术为标准库中所有产生类型的类型特征定义快捷方式。例如，为了能够编写点击此处查看代码图片

```cpp
std::add_const_t<T> // since C++14
```

而不是

点击此处查看代码图片

```cpp
typename std::add_const<T>::type // since C++11
```

标准库定义了：

点击此处查看代码图片

```cpp
namespace std {
template<typename T> using add_const_t = typename add_const<T>::type;
}
```

## 2.9 类模板实参推导

在C++17之前，你总是必须将所有模板参数类型传递给类模板（除非它们有默认值）。自C++17起，总是必须显式指定模板实参这一约束被放宽了。相反，如果构造函数能够推导出所有模板参数（那些没有默认值的参数），你可以跳过显式定义模板实参。例如，在之前所有的代码示例中，你可以在不指定模板实参的情况下使用拷贝构造函数：点击此处查看代码图片

```cpp
Stack<int> intStack1; // stack of ints
Stack<int> intStack2 = intStack1; // OK in all versions
Stack intStack3 = intStack1; // OK since C++17
```

通过提供传递一些初始实参的构造函数，你可以支持推导栈的元素类型。例如，我们可以提供一个可以用单个元素初始化的栈：点击此处查看代码图片

```cpp
template<typename T>
class Stack {
private:
    std::vector<T> elems; // elements
public:
    Stack () = default;
    Stack (T const& elem) // initialize stack with one element
        : elems({elem}) {
    }
};
```

这允许你如下声明一个栈：点击此处查看代码图片

```cpp
Stack intStack = 0; // Stack<int> deduced since C++17
```

通过用整数0初始化栈，模板参数T被推导为int，因此实例化了一个Stack<int>。

注意以下几点：

- 由于int构造函数的定义，你必须请求默认构造函数以其默认行为可用，因为默认构造函数只有在没有定义其他构造函数时才可用：`Stack() = default;`
- 实参elem在传递给elems时带有花括号，以便用初始化器列表初始化vector elems，其中elem是唯一的实参：`: elems({elem})`

vector没有能够直接将单个参数作为初始元素的构造函数。⁶

注意，与函数模板不同，类模板实参不能仅部分推导（即只显式指定部分模板实参）。详细信息请参见第314页的15.12节。

### 使用字符串字面量的类模板实参推导

原则上，你甚至可以用字符串字面量初始化栈：点击此处查看代码图片

```cpp
Stack stringStack = "bottom"; // Stack<char const[7]> deduced since C++17
```

但这会引起很多麻烦：一般来说，当按引用传递模板类型T的实参时，参数不会发生退化（decay），退化是指将原始数组类型转换为相应原始指针类型的机制。这意味着我们实际上初始化了一个Stack<char const[7]>，并在使用T的任何地方使用char const[7]类型。例如，我们可能无法

