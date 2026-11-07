

## 15.2 自定义类模板与编译时多态

Google 的 C++ 风格指南建议“避免复杂的模板编程。”^10 同样，C++ 核心指南指出，应该“仅在确实需要时使用模板元编程”，而且它“很难正确实现，……而且通常很难维护。”^11 当开发者在使用 C++20 概念和未来的 C++ 增强功能方面获得更多经验时，这些指南可能会更新。

### 创建类模板 Stack<T>

模板通过泛化地指定能力，然后让编译器实例化模板，按需生成特定于类型的代码特化，从而实现编译时（或静态）多态^12,13。类模板被称为参数化类型，因为它们需要一个或多个参数来告诉编译器如何定制类模板，以形成一个可以从其实例化对象的类模板特化。你编写一个类模板定义。当你需要特定的特化时，你使用简洁、简单的表示法来实例化模板。然后，编译器只为你编写那些特化。例如，一个 Stack 类模板可以成为创建许多类模板特化的基础，例如“double 的 Stack”、“int 的 Stack”、“Employee 的 Stack”、“Bill 的 Stack”或“ActivationRecord 的 Stack”。

要将类型与模板一起使用，该类型必须满足模板的要求。例如，模板可能要求指定类型的对象：

- 可以通过默认构造函数初始化，
- 可复制或可移动，
- 可以与 operator < 进行比较以确定其排序顺序，
- 具有特定的成员函数等等。

当你使用不满足模板要求的类型实例化模板时，通常会发生编译错误。

让我们直接进入自定义 Stack 类模板的编码。独立于你放入栈或从栈中移除的项的种类来理解栈的概念是可能的。栈只是一个后进先出（LIFO）数据结构。类模板通过使编译器能够从单个类模板实例化许多特定于类型的类模板特化来鼓励软件重用——正如你在 13.12.1 节中看到的栈容器适配器那样。这里（图 15.1），我们泛化地定义一个栈，然后实例化并使用类型特定的栈（图 15.2）。图 15.1 的 Stack 类模板定义看起来像一个常规的类定义，但有几个关键区别。

```cpp
// Fig. 15.1: Stack.h
// Stack class template.
#pragma once
#include <deque>

template<typename T>
class Stack {
public:
    // return the top element of Stack
    const T& top() const {return stack.front();}

    // push an element onto Stack
    void push(const T& pushValue) {stack.push_front(pushValue);}

    // pop an element from Stack
    void pop() {stack.pop_front();}

    // determine whether Stack is empty
    bool isEmpty() const {return stack.empty();}

    // return size of Stack
    size_t size() const {return stack.size();}
private:
    std::deque<T> stack{}; // internal representation of Stack
};
```

**图 15.1** | Stack 类模板。

### 模板头

第一个关键区别是模板头（第 6 行），它以 `template` 关键字开头，后跟一对尖括号（< 和 >）括起来的逗号分隔的模板参数列表：

```cpp
template<typename T>
```

每个表示类型的模板参数必须以前缀 typename 或 class 之一开头的可互换关键字。有些程序员更喜欢 typename，因为模板的类型参数可能不是类类型。（在其他情况下，必须使用 typename 而不是 class。^14,15）类型参数 T 是 Stack 元素类型的占位符。类型参数名称可以是任何有效标识符，但必须在模板定义中是唯一的。在 Stack 类模板中，只要我们需要访问 Stack 的元素类型，就会提到 T：

- 声明成员函数返回类型（第 10 行），
- 声明成员函数参数（第 13 行），以及
- 声明变量（第 24 行）。

当你实例化类模板时，编译器将类型参数与**类型实参**相关联。此时，编译器会生成类模板的一个副本，其中类型参数的所有出现都被替换为指定的类型。**编译器只为代码中使用的模板部分生成定义。**

Stack 类模板与我们定义的其他类之间的另一个区别是，我们**没有将类模板的接口与其实现分离**。你在头文件中定义模板，然后将它们 `#include` 到客户端代码文件中。每次用**新的类型实参**实例化模板时，编译器都需要完整的**模板定义**来生成相应的代码。对于类模板，这意味着成员函数也在头文件中定义——通常是在类定义的体内，如图 15.1 所示。

### 类模板 Stack<T> 的数据表示

13.12.1 节表明，标准库的 **stack 适配器类**可以使用各种容器来存储其元素。栈只需要在**顶部**进行插入和删除，因此 **vector** 或 **deque** 可以存储栈的元素。vector 支持在其尾部快速插入和删除。deque 支持在其头部和尾部快速插入和删除。deque 是标准库 stack 适配器的默认表示，因为 **deque 比 vector 增长更高效**：

- **vector** 的元素存储在连续的内存块中。当该块已满并且你添加新元素时，vector 会执行昂贵的**分配更大的连续内存块并将旧元素复制或移动**到该新块的操作。
- **deque** 通常实现为固定大小的内置数组的列表——在必要时添加新的数组。**当向 deque 的头部或尾部添加新项时，不会复制或移动现有元素。**

由于这些原因，我们使用 deque（第 24 行）作为 Stack 类的底层容器。

### 类模板 Stack<T> 的成员函数

类模板的成员函数定义类似于函数模板。**当你在类模板体内定义它们时，不需要在它们前面加上模板头。** 它们仍然使用模板参数 T 来表示元素类型。Stack 类模板没有定义自己的构造函数——**类的默认构造函数调用 deque 数据成员的默认构造函数。**

Stack（图 15.1）提供以下成员函数：

- **top**（第 10 行）返回对 Stack 顶部元素的 const 引用，但不将其移除。你也可以用非 const 版本重载 `top`。

10. “Google C++ Style Guide—Template Metaprogramming。” 访问于 2023 年 4 月 18 日。https://google.github.io/styleguide/cppguide.html#Template_metaprogramming.
11. “C++ Core Guidelines, T.120: Use Template Metaprogramming Only When You Really Need To。” 访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-metameta.
12. “C++—Static Polymorphism。” Wikipedia. Wikimedia Foundation. 访问于 2023 年 4 月 18 日。https://en.wikipedia.org/wiki/C%2B%2B#Static_polymorphism.
13. Kateryna Bondarenko, “Static Polymorphism in C++,” 2019 年 5 月 6 日。访问于 2023 年 4 月 18 日。https://medium.com/@kateolena/static-polymorphism-in-c-9e1ae27a945b.
14. Scott Meyers, “Item 42: Understand the Meanings of typename,” *Effective C++*, 3/e. Pearson Education, Inc., 2005.
15. John Lakos, “1.3 Declarations, Definitions, and Linkage,” *Large-Scale C++*. Addison-Wesley, 2020. 脚注 56 和 57。
16. Andreas Fertig, “Back to Basics: Templates (Part 1 of 2),” 2020 年 9 月 25 日。访问于 2023 年 4 月 18 日。https://www.youtube.com/watch?v=VNJ4wiuxJM4.
17. “13.9.2 Implicit Instantiation [temp.inst]。” 访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/temp.inst#4.
18. “std::stack.” 访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/container/stack.

