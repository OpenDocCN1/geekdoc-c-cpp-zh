
# 3.19.2 进一步说明运算符

请注意，不要假设子表达式具有特殊的评估顺序。例如，以下依赖关系应避免：

int f( int & x )
{
    return x += 2;
}

int g( int & x )
{
    return x *= 3;
}

void h( void )
{
    int x = 10;
    int p = f( x ) + g( x ); // 可能是 48 也可能是 42
    // ...
}

`p` 的结果取决于 `f` 是否在 `g` 之前被调用，或者 `g` 在 `f` 之前被调用，这在 C++ 标准中是未定义的。另一方面，逻辑运算符 `&&`（与）和 `||`（或），以及 `,`（逗号），保证左侧操作在右侧操作之前执行。例如，

f( x ) && g( x )
```

is guaranteed to call function `f` before `g`. But for built-in types, the `&&` operator's second operand is _not_ evaluated if the first operand has been evaluated to `false` (since the result is obviously `false` in such a case). Similarly, the `||` operator's second operand is evaluated only if the first one returned `false` (this is known as short-circuit evaluation). This is especially useful to check for null pointers before accessing objects, as in the following function:

bool check_if_not_empty_string( char * p )
{
    // the second cond is evaluated only if first is true
    if( p != nullptr && * p != 0 )
        return true;
    else
        return false;
}

In this `if` statement, the pointer `p` is first checked to see if it is a null pointer (denoted by `0` in C/ C++ or `nullptr` in C++11). If it is `nullptr`, then we cannot evaluate its dereferencing expression `* p`, since it would throw a software exception. However, if `p` is a valid pointer, we check the first letter of the text pointed to by `p`; if it is not zero, we return `true` to indicate that the text is not empty. Otherwise, we return `false`.

Since this short-circuit evaluation feature is guaranteed _only_ for the built-in types, we cannot rely on it if we call a class's overloaded `&&` and `||` operators. Therefore, if we really need to overload these operators, we should do so carefully (Section 4.4).

## 3.20 总结

## 需牢记的要点

- 学习所有运算符的方面。检查其优先级和结合性
- 试图不要在表达式中混合类型 – 不要依赖隐式类型转换
- 只有 `&&`（与）、`||`（或）和 `,`（逗号）运算符具有严格的左到右评估顺序。不要假设其他运算符的特定顺序
- 对于内置类型，`&&` 运算符的第二个操作数在第一个操作数的值为 false 时不会被评估。同样，`||` 运算符的第二个操作数在第一个操作数的值为 true 时不会被评估
- 如果可能，将表达式拆分而非使用复杂的表达式。使用括号增强可读性
- 对于间接访问对象，优先使用引用而非指针
- 将代码拆分为相对较小的片段 – 函数 – 每个函数拥有明确的目的、有意义的名称以及短小的参数列表。如果需要更多参数，可以将它们组合成类或结构体
- 将数据与其相关的函数封装在类中。设计一组简洁的函数作为类的公共接口。将其余内容放入类的私有部分。确保使用初始化列表 { } 和/或构造函数初始化所有数据成员
- 优先使用标准库中的容器（如 vector、string、array）和算法（如 find、copy、accumulate、transform）而非自行编写
- 在设计之前，先深入分析问题。在实现之前先进行设计

软件设计和编程的大部分困难源于需要满足的要求、域的复杂性以及软件行为和使用所产生的影响。我们可以通过建模来简化这一过程，通过关注系统中最重要的方面。通过将系统划分为较小、概念上更易处理的模块，我们可以逐一处理每个模块的细节。

在本章中，我们将深入探讨面向对象（OO）软件设计和面向对象编程（OOP）的领域，这有助于软件系统建模。核心概念是类及其实例 –  – 对象。对象可以表示真实事物或操作。面向对象范式是基于这一概念形成的，我们将在讨论中展开；它们是全球编程社区数十年的经验积累的结果。

OOP 在许多成功的项目中已被证明其有效性。另一方面，我们可能会发现虽然使用了 OO 方法但项目仍然失败。因此，OO 方法并非万能圣杯，不conditional 保证成功。OOP 仅仅是一套原则、编程技术、模式和建议。因此，理解 OOP 的基本概念并利用其最佳特性来改进我们的软件设计和实现至关重要。改进软件意味着在使用 OOP 时，软件会比未使用 OOP 时更好。然而，这并非一种意识形态问题 –  – 关键在于成功结果：可靠、行为良好、易于理解、使用直观、易于维护和扩展的软件。令人惊讶的是，类似于集成电路中模块封装的概念启动了集成电路的电子革命？硬件与软件这两个领域的协同作用使我们达到了当前的人工智能（AI）和物联网（IoT）突破。

OOP 的原则可以追溯到 1960 年代和 1970 年代，当时 Simula 和 Smalltalk 等编程语言的发展。大多数现代编程语言都源自这一传统。C++ 编程语言，源自 Simula 和 C 的原则，是 OOP 队伍中最早的玩家之一。本章将从 OOP 概念入手，进而探讨代码示例。

1970 年代的一个成功软件工程范式是著名的等式 _Algorithms+Data structures = Programs_，由教授 Niklaus Wirth 在其著名的编程书籍标题中提出（Wirth 1976）。多年来，算法与数据结构被视为独立的部分。

