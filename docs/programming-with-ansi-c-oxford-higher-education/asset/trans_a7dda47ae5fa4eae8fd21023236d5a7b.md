
# 表 2.1 C++ 关键字

| asm | do | if | return | typedef |
| auto | double | inline | short | typeid |
| bool | dynamic_cast | int | signed | typename |
| break | else | long | sizeof | union |
| case | enum | mutable | static | unsigned |
| catch | explicit | namespace | static_cast | using |
| char | export | new | struct | virtual |
| class | extern | operator | switch | void |
| const | false | private | template | volatile |
| const_cast | float | protected | this | wchar_t |
| continue | for | public | throw | while |
| default | friend | register | true |  |
| delete | goto | reinterpret_cast | try |  |

粗体字是 ANSI C 关键字。普通字体单词是最初的 C++ 关键字（来自 Stroustrup），斜体字是 ANSI C++ 对早期 C++ 关键字集的补充。

## 2.3 数据类型

C++ 中的数据类型可分为三类。第一类表示直接从 C 借用的数据类型，构成了最大的一组。第二类表示在 C 中可用且在 C++ 中也可用、但含义有所扩展的数据类型。第三类表示 C++ 中引入的新数据类型，在 C 中不可用。

### 2.3.1 借用自 C

数据类型 void、int、char、float 和 double，以及这些数据类型的修饰符，即 signed、unsigned、long 和 short，其行为方式与 C 中相同。此外，除了 void 指针之外，指针以及数组（除非包含新增数据类型的数据）也与在 C 中的行为方式相同。

### 2.3.2 借用自 C 但有所修改

C++ 中包含的某些 C 数据类型已经过调整，以兼容 C++ 的特性与编译器要求。这些数据类型是结构体、联合体、枚举和指针。

在 C++ 中，struct（结构体）被扩展以兼容 class 数据类型。class 数据类型以及 C++ 中 class 与 struct 之间的区别将在第 3 章讨论。union（联合体）的适用范围在 C++ 中也有所扩展，并将在第 3 章详细讨论。

在 C 中，enum（枚举）字面量即使是在局部定义的，也是全局可见的；但在 C++ 中，它们仅对定义它们的类（或结构体）可见。

C++ 中的指针定义与 C 中的行为方式相同，但 void 指针以及两种新指针类型——常量指针和指向常量的指针——除外。C++ 中的指针将在第 2.4 节详细讨论。

### 2.3.3 新增数据类型

本节介绍 C++ 中新增的一些数据类型。类是 C++ 的核心构造。类能够以真实的方式表示现实世界中的实体。类将在第 3 章详细讨论。

C++ 中的字符串比 C 中更容易使用。在 C 中，字符串被视为字符数组，但 C++ 有一个特殊的 string 类来定义字符串。本书通篇使用字符串，并将在第 15 章详细讨论。严格来说，字符串对于 C++ 程序而言仍然是一个外部实体，需要包含 `<string>` 文件才能提供对字符串的操作。还有少数其他类，如 queue 和 vector，它们是标准模板库（STL）的一部分。这些将在第 16 章介绍。

## 抽象数据类型

有人可能会说，字符串、队列和栈并不是原生或内置数据类型，而是用户自定义的。在 C 中，内置数据类型和用户自定义数据类型之间的区别是明确的，但在 C++ 中则相当模糊。此外，这些数据类型由标准给出，因此对于最终用户而言，它们与内置数据类型非常相似。它们有时被称为抽象数据类型，并且只能出现在基于对象的语言中。

C++ 中新增的一个有趣数据类型是 bool（布尔）。它只有两个值：true 或 false，二者都是 C++ 中的关键字。

请考虑以下程序。它测试输入，如果输入为零则退出程序。

```
//TestBool.cpp
#include <iostream>
using namespace std;
void main()
{
    bool flag;
    flag = true;
    int test;
    while(flag)
    {
        cin >> test;
        if(!test)
            flag = false;
    }
}
```

注意将“flag”用作 bool 变量。bool 变量可以用于任何关系表达式或逻辑表达式的位置。在 C 中，提供布尔运算是赋给整型变量的额外任务。在 C++ 中，如果我们的目的仅仅是为了测试真假，就可以省去整型变量。使用 bool 变量使这种测试更加容易，也使程序更加可读。它可以具有 true 或 false 的值，如程序所示。

## 2.4 指针

尽管 C++ 中也有指针，但它们具有一些与 C 中不同的特性，这些特性将在以下各节讨论。

### 2.4.1 void 指针

void 指针是从 C 借用的一种重要指针类型。有人可能会质疑 void 指针的必要性。由于指针必须指向一个变量（即它具有某个变量的地址），void 指针（指向“无”的指针）的想法听起来可能有点讽刺。然而，这类指针在 C 中用于返回未知类型的指针值很有用。malloc() 函数就是一个例子。

> 注意 malloc() 函数可用于为任何数据类型获取内存。这就是为什么它被设计为返回 void 指针，用户可将其强制转换为所需的任何类型。当需要编写一个通用算法时，也需要这样做：将算法定义为在参数中接受 void 指针，从而可以接受任何指针类型。

C++ 中 void 指针的本质用“指向 void 的指针”这一术语来表述更为贴切。void 指针指向一个没有类型的值（例如 int 和 float）。这意味着 void 指针所指向的值具有不确定的长度和不确定的解引用属性。考虑以下代码段，可以说明 C 与 C++ 中 void 指针定义的差异：

```
int* FirstPointer;
void* SecondPointer;
```

语句

```
SecondPointer = FirstPointer;
```

在 C 和 C++ 中都是合法的。然而，反向操作，即

```
FirstPointer = SecondPointer;
```

在 C++ 中却不行，尽管在 C 中它可以正常工作。这是因为 C++ 是一种严格类型化的语言。

> 注意 C++ 是一种严格类型化的语言。若某人编写一个函数 xyz();，并假设它返回整数，于是编写语句 int i = xyz();，这就依赖于 xyz() 返回 int，而这一点在定义时并未明确指定。此类语句依赖于编译器在未指定类型时默认将其视为 int 的行为。当编译器不默认将其视为 int 时，这样的代码会导致难以调试的错误。

为了达到与 C 中相同的效果，必须按以下方式显式转换第二个指针：

```
FirstPointer = (int*) SecondPointer;
```

前一个语句会产生编译错误，而这个语句不会。

### 2.4.2 常量指针

常量指针是一种在定义时只能指向它当时所指向对象、不能指向其他任何对象的指针。它类似于 const int 或 const float 类型：定义时赋的值在整个程序运行期间不能改变。const 指针中存储的值是另一个变量的地址。

使用常量指针时，地址本身不能改变；但必须注意，该地址的内容可以改变。因此，如果我们定义

```
int * const SecondPointer = &Content1;
```

那么下面这样是允许的：

```
*SecondPointer = AnotherContent;
```

```
// Changing the content of the integer pointed to
```

但是，下面这样是不允许的：

```
SecondPointer++;
```

或

```
SecondPointer = &AnotherContent;
```

```
// Changing the pointer value itself
```

请考虑以下代码：

```
void main()
int Content1 = 10;
int Content2 = 20;
int *FirstPointer = &Content1;
// Normal pointer; operation is allowed
int *const SecondPointer = &Content2;
// SecondPointer is a constant pointer
*SecondPointer = 100;
// Operation is allowed; contents can be changed
FirstPointer++;
// Normal pointer, operation is allowed
SecondPointer++;
/* Erroneous statement; not allowed as pointer address itself cannot be changed */
// Error: lvalue specifies const object
// lvalue is a variable-like construct, which can be assigned a value
```

当无法向诸如 const 对象之类的构造赋值时，就会产生错误。根据 C 的知识我们已经知道，指向整数的指针可以这样定义：

```
int* FirstPointer = &Content1;
```

C++ 允许在 * 和指针名之间插入关键字 const。这样的指针就成为常量指针，即它所指向的地址不能被操作。但是，该地址的内容可以被操作。因此，下面的语句是可以接受的：

```
SecondPointer = &Content2;
```

表达式 int* const、int* const 和 int *const 都是正确的，并且含义相同。对于 int &Name、int & Name 和 int& Name 等表达式，情况也是如此。
