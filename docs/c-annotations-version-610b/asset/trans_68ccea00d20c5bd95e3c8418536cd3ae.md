
```cpp
        // process myString
}
```

上面的示例需要进一步说明。通常可以有益地为变量赋予局部作用域，但在其初始化之后需要立即进行额外检查。初始化和测试不能合并到一个表达式中。相反，需要两个嵌套语句。因此，下面的示例也无法编译：

```cpp
if ((int c = getchar()) && strchr("aeiou", c))
    printf("Saw a vowel\n");
```

如果出现这种情况，要么使用两个嵌套的 if 语句，要么使用嵌套的复合语句将 int c 的定义局部化：

```cpp
if (int c = getchar())                 // nested if-statements
    if (strchr("aeiou", c))
        printf("Saw a vowel\n");

{
    int c = getchar();                  // nested compound statement
    if (c && strchr("aeiou", c))
        printf("Saw a vowel\n");
}
```

### 2.5.12 关键字 ‘typedef’

关键字 `typedef` 在 C++ 中仍在使用，但在定义 `union`、`struct` 或 `enum` 时不再需要。下面的示例说明了这一点：

```cpp
struct SomeStruct
{
    int       a;
    double    d;
    char      string[80];
};
```

当定义 `struct`、`union` 或其他复合类型时，该类型的标签可以用作类型名（在上面的示例中就是 SomeStruct）：

```cpp
SomeStruct what;

what.d = 3.1415;
```

### 2.5.13 函数作为 struct 的一部分

在 C++ 中，我们可以将函数定义为 struct 的成员。这里我们遇到对象的第一个具体示例：如前所述（见第 2.4 节），对象是包含数据的结构，同时存在专门用于操作这些数据的函数。

下面的代码片段提供了 `struct Point` 的定义。在这个结构中，声明了两个 `int` 数据字段和一个函数 `draw`。

```cpp
struct Point              // definition of a screen-dot
{
    int x;              // coordinates
    int y;              // x/y
    void draw();        // drawing function
};
```

类似的结构可以是绘图程序的一部分，并且例如可以表示一个像素。关于这个 struct，应注意以下几点：

- 结构定义中提到的函数 `draw` 只是一个 *声明*。定义函数所执行操作的实际函数代码在别处（第 3.2 节将进一步讨论 struct 内函数的概念）。

- struct `Point` 的大小等于其两个 int 的大小。在结构内部声明的函数不会影响其大小。编译器通过仅允许函数 `draw` 在 `Point` 的上下文中可用来实现这种行为。

`Point` 结构可按如下方式使用：

```cpp
Point a;              // two points on
Point b;              // the screen

a.x = 0;              // define first dot
a.y = 10;             // and draw it
a.draw();

b = a;                // copy a to b
b.y = 20;             // redefine y-coord
b.draw();             // and draw it
```

如上面的示例所示，可以使用点（.）选择作为结构一部分的函数（当有指向对象的指针时，使用箭头（->）运算符）。因此，这与选择结构数据字段的方式相同。

这种语法构造背后的思想是，多个类型可以包含具有相同名称的函数。例如，表示圆的结构可能包含三个 int 值：两个值用于圆心的坐标，一个值用于半径。与 `Point` 结构类似，`Circle` 现在可以有一个函数 `draw` 来绘制圆。

## 第 3 章 C++ 初印象

本章进一步探讨 C++。通过各种示例说明了在 struct 中声明函数的可能性；引入了类的概念；详细介绍了类型转换；引入了许多新类型，并讨论了 C 的若干重要记法扩展。

### 3.1 对 C 的扩展

在继续介绍‘真正的’面向对象编程方法之前，我们先介绍 C 编程语言的一些扩展：这些不只是 C 与 C++ 之间的差异，而是 C 中没有的语法构造和关键字。

### 3.1.1 命名空间

C++ 引入了 *命名空间* 的概念：所有符号都定义在一个更大的上下文中，称为命名空间。命名空间用于避免名称冲突，例如当程序员想定义一个像 `sin` 这样以度为单位的函数，但又不想失去使用以弧度为单位的标准 `sin` 函数的能力时，就可能出现这种冲突。

第 4 章将广泛介绍命名空间。目前应注意，大多数编译器要求显式声明标准命名空间：`std`。因此，除非另有说明，需要强调，注解中的所有示例现在都隐式使用

```cpp
using namespace std;
```

声明。因此，如果你确实打算编译 **C++ 注解** 中给出的示例，请确保源文件以上面的 `using` 声明开头。

### 3.1.2 作用域解析运算符 ::

**C++** 引入了几个新运算符，其中包括作用域解析运算符（`::`）。当存在与局部变量同名的全局变量时，可以使用该运算符：

```cpp
#include <stdio.h>

int counter = 50;                     // global variable

int main()
{
    for (int counter = 1;        // this refers to the
        counter < 10;             // local variable
        counter++)
    {
        printf("%d\n",
                ::counter       // global variable
                /                // divided by
                counter);        // local variable
    }
}
```

在上面的程序中，作用域运算符用于访问全局变量，而不是具有相同名称的局部变量。在 C++ 中，作用域运算符被广泛使用，但很少用于访问被同名局部变量遮蔽的全局变量。其主要用途将在第 7 章描述。

### 3.1.3 使用关键字 ‘const’

尽管关键字 `const` 是 C 语法的一部分，但它在 C++ 中的使用比在 C 中更重要，也更常见。

const 关键字是一个修饰符，表示变量或参数的值不可修改。在下面的示例中，意图是更改变量 ival 的值，但这会失败：

```cpp
int main()
{
    int const ival = 3;      // a constant int
                             // initialized to 3

    ival = 4;                // assignment produces
                             // an error message
}
```

这个示例展示了 ival 可以在其定义中初始化为给定值；之后尝试更改该值（在赋值中）是不允许的。

与 C 不同，声明为 `const` 的变量可用于指定数组的大小，如下面的示例所示：

```cpp
int const size = 20;
char buf[size];              // 20 chars big
```

关键字 const 的另一个用途体现在指针的声明中，例如在指针参数中。在声明

```cpp
char const *buf;
```

buf 是一个指向 char 的指针变量。buf 所指向的任何内容都不能通过 buf 更改：这些 char 被声明为 const。然而，指针 buf 本身可以更改。因此，像 *buf = 'a'; 这样的语句是不允许的，而 ++buf 是允许的。

在声明

```cpp
char *const buf;
```

不过，Marshall Cline 的建议可以改进。下面这个配方可以毫不费力地剖析即使是最复杂的声明：

1. 从变量名开始阅读
2. 尽可能远地阅读，直到到达声明的末尾或一个（尚未匹配的）右括号。
3. 回到开始阅读的位置，然后反向阅读，直到到达声明的开头或一个匹配的左括号。
4. 如果到达了一个左括号，则从之前停止的括号之后继续执行第 2 步。

让我们把这个配方应用到下面这个（本身无关紧要的）复杂声明上。小箭头指示每一步应该读到何处，箭头方向指示阅读方向：

```text
    char const *(* const *(*ip)()[])[]

                        ip          Start at the variable's name:
                                    'ip' is

                        ip)         Hitting a closing paren: revert
                        -->

                        (*ip)       Find the matching open paren:
                        <--         'a pointer to'

                        (*ip)()     The next unmatched closing par:
                            -->     'a function (not expecting
                                    arguments)'

                        (*ip)()     Find the matching open paren:
                        <--         'returning a pointer to'

                        (*ip)()[]   The next closing par:
                            -->     'an array of'

                        (* const *(*ip)()[])  Find the matching open paren:
                        <--------   'const pointers to'

                        (* const *(*ip)()[])[] Read until the end:
                            -->     'an array of'

    char const *(* const *(*ip)()[])[] Read backwards what's left:
    <----------                             'pointers to const chars'
```

把所有部分汇总起来，对于 `char const *(* const *(*ip)()[])[]`，我们得到：*ip* 是一个指向函数的指针（该函数不期望参数），该函数返回一个指针，指向一个由 const 指针组成的数组，而这些 const 指针指向一个由指向 const char 的指针组成的数组。这就是 `ip` 所表示的内容；这个配方可用于解析你遇到的任何声明。

### 3.1.4 ‘cout’、‘cin’ 和 ‘cerr’

与 C 类似，C++ 定义了在程序执行时可用的标准输入流和输出流。这些流是：

- cout，类似于 stdout，
