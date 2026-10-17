
`void (*pf1)();`      // 无异常规格说明

`void (*pf2)() throw(A);`

```cpp
void f() {
    pf1 = pf2;      // OK: pf1 的限制更少
    pf2 = pf1;      // error: pf2 的限制更严格
}
```

— 示例结束

6 在赋值或初始化中，返回类型和参数类型的异常规格应该是兼容的。在其他赋值或初始化中，异常规格也应该是兼容的。

7 异常可以多次具有相同的类型，并可以包含通过继承关系相关的类，尽管这样做是冗余的。[注：异常规格也可以包含类 `std::bad_alloc`(18.8.2) — 注释；]

8 如果一个函数的 `noexcept` 规格中的常量表达式求值为 `false`，或者其动态异常规格包含一个类型 `T`，使得类型为 `T` 的处理器可以匹配类型 `E` 的异常 (15.3)，则称该函数允许类型 E。

9 每当抛出异常且对处理器的搜索 (15.3) 遇到带有不允许异常的异常规格的函数外层块时，
   - 如果该异常规格是动态异常规格，则调用函数 `std::unexpected()` (15.5.2)，
   - 否则，调用函数 `std::terminate()` (15.5.1)。

[示例：

```cpp
class X {};
class Y {};
class Z : public X {};
class W {};
```

```cpp
void f() throw(X, Y) {
    int n = 0;
    if (n) throw X();      // OK
    if (n) throw Z();      // 也是 OK
    throw W();            // 将调用 std::unexpected()
}
```

— 示例结束

> [注：函数可以有多个带有非抛出异常规格的声明；为此目的，使用函数定义上的规格。 — 注释；

10 函数 `expected()` 可能会抛出一个满足其调用时对应的异常规格的异常，在这种情况下，对于另一个处理器将继续带有该异常规格的函数调用 (15.5.2)，或者可能会调用 `std::terminate()`。

11 实现不应仅仅因为一个表达式在执行时可能抛出一个包含函数不允许的异常而拒绝该表达式。[示例：

# ISO/IEC 14882:2011(E)

```cpp
extern void f() throw(X, Y);
void g() throw(X) {
    f();
} // OK
```

对 `f` 的调用即使在调用时也是构造良好的；`f` 可能会抛出 `g` 不允许的异常 `Y`。
— 示例结束 —

12 没有异常规格说明或异常规格形式为 `noexcept(constant-expression)` 且该常量表达式求值为 `false` 的函数允许所有异常。如果异常规格的形式为 `throw()`、`noexcept` 或常量表达式求值为 `true` 的 `noexcept(constant-expression)`，则该异常规格是非抛出的。一个具有非抛出异常规格的函数不允许任何异常。

13 异常规格不被视为函数类型的一部分。

14 隐式声明的成员函数（第12节）应该有一个异常规格说明。如果 `f` 是隐式声明的默认构造函数、拷贝构造函数、拷贝赋值运算符或移动赋值运算符，其隐式异常规格指定类型 ID `T`，且仅当 `T` 被 `f` 的隐式定义中直接调用的函数的异常规格所允许时；如果 `f` 直接调用的任何函数允许异常，则 `f` 应该允许所有异常；如果 `f` 直接调用的每个函数都不允许异常，则 `f` 不允许任何异常。

```cpp
struct A {
    A();
    A(const A&) throw();
    A(A&&) throw();
    ~A() throw(X);
};
struct B {
    B();
    B(const B&) throw();
    B(B&&) throw();
    ~B() throw(Y);
};
struct D : public A, public B {
    // D 的隐式声明：D();
    // D 的隐式声明：D(const D&) throw();
    // D 的隐式声明：D(D&&) throw();
    // D 的隐式声明：~D() throw(X, Y);
}
```

此外，如果 `A::A()` 和 `B::B()` 是虚函数，则 `D::D()` 的限制不会像 `A::"A"` 那样严格，并且如果基类中的此类虚函数的异常规格至少与基类一样严格，则程序是构造良好的。
— 示例结束 —

15 没有显式异常规格说明的释放操作 (3.7.4.2) 被处理为指定了 `noexcept(true)`。

16 在动态异常规格中，类型 ID 后跟一个省略号 `...` 是一个包展开 (14.5.3)。

17 [注：动态异常规格的使用已弃用（附录 D）。— 注 ]

## § 15.4

## 15.5 特殊函数

函数 `terminate()` (15.5.1) 和 `std::unexpected()` (15.5.2) 用于异常处理机制。函数 `std::current_exception()` (18.8.5) 和 `std::nested` (18.8.6) 用于捕获异常。

### 15.5.1 std::terminate() 函数

实现在以下情况下调用 `std::terminate()`：
- 当处理器的搜索 (15.3) 遇到带有不允许异常的异常规格的函数外层块时，
- 在程序退出抛出异常时，
- 在构造时抛出异常时，
- 在拷贝时抛出异常时，
- 在赋值时抛出异常时，
- 在移动时抛出异常时，
- 在移动赋值时抛出异常时，
- 在析构时抛出异常时，
- 在初始化处理器抛出异常时，
- 在处理器的激活抛出异常时，
- 在处理器的执行抛出异常时，
- 在处理器的析构抛出异常时，
- 在内存内存抛出异常时，
- 在处理器的释放抛出异常时，
- 在 `std::terminate()` 抛出异常时，
- 在 `std::unexpected()` 抛出异常时，
- 在 `std::uncaught_exception()` 抛出异常时，
- 在 `std::current_exception()` 抛出异常时，
- 在 `std::terminate_exception()` 抛出异常时，
- 在 `std::nested_exception()` 抛出异常时，
- 在 `std::bad_exception()` 抛出异常时，
- 在 `std::bad_alloc()` 抛出异常时，
- 在 `std::bad_variant()` 抛出异常时，
- 在 `std::bad_type_info()` 抛出异常时，
- 在 `std::bad_cast()` 抛出异常时，
- 在 `std::bad_function_access()` 抛出异常时，
- 在 `std::out_of_range()` 抛出异常时，
- 在 `std::bad_index_range()` 抛出异常时，
- 在 `std::length_error()` 抛出异常时，
- 在 `std::bad_mutex()` 抛出异常时，
- 在 `std::bad_lock()` 抛出异常时，
- 在 `std::bad_lock_lock()` 抛出异常时，
- 在 `std::system_error()` 抛出异常时，
- 在 `std::runtime_error()` 抛出异常时，
- 在 `std::logic_error()` 抛出异常时，
- 在 `std::overflow_error()` 抛出异常时，
- 在 `std::invalid_argument()` 抛出异常时，
- 在 `std::invalid_range()` 抛出异常时，
- 在 `std::domain_error()` 抛出异常时。

### 15.5.2 std::unexpected() 函数 [except.unexpected]

如果带有默认或动态异常规格的函数抛出了未在动态异常规格中列出的异常，在完成前函数的栈回溯后立即调用函数 `std::unexpected()` (D.11)。

[注：默认情况下，`std::unexpected()` 调用 `std::terminate()`；但程序可以安装自己的处理器函数 (D.11.2)。在任何情况下，均适用以下段落。— 注释]

`std::unexpected()` 函数不返回，但它可以抛出（或重新抛出）异常。如果它抛出的之前违反规格的异常，且动态异常规格不允许，则发生以下情况：如果动态异常规格不包含类 `std::bad_exception` —— 实现定义 (18.8.2)，则调用函数 `std::terminate()`，否则异常被替换为类型为 `std::bad_exception` 的实现定义，并且将在违反异常规格的函数调用处继续搜索另一个处理器。

因此，动态异常规格保证了只会抛出列出的异常。如果动态异常规格包含了类型 `std::bad_exception`，则任何不在列表中的异常都可以在 `std::unexpected()` 函数中被 `std::bad_exception` 替换。

### 15.5.3 std::uncaught_exception() 函数 [except.uncaught]

函数 `std::uncaught_exception()` 在完成异常对象的处理器的初始化 (15.1) 后直到完成异常的激活 (15.3, 18.8.4) 返回 `true`。这包括栈回溯。如果异常被重新抛出 (15.1)，`std::uncaught_exception()` 从重新抛出点到重新抛出的异常再次被捕获为止返回 `true`。

## 16 预处理指令 [cpp]

预处理指令由一个预处理标记标记序列组成，该序列满足以下翻译约束：序列中的第一个标记是 `#` 预处理标记（在翻译阶段 4 开始时），它要么是源文件的第一个字符（可选地紧跟在不包含换行符的空白之后），要么紧跟在包含至少一个换行符的空白之后。序列中的最后一个标记是紧跟在序列中第一个标记之后的第一个行字符。换行符会结束预处理指令，即使它出现在本应是函数形式宏调用的内部。

``` 
preprocessing-file:
  group:
    group-part
    group-part group-part
  group-part:
    if-section
      control-line
      text-line
      # non-directive
if-section:
  if-group elif-groups_opt else-group_opt endif-line
if-group:
  # if constant-expression new-line-group_opt
  # ifdef identifier new-line-group_opt
  # ifdef identifier new-line-group_opt
elif-groups:
  elif-group
  elif-groups elif-group
if-group:
  # elif
```

``` 
constant-expression new-line-group_opt
else-group:
  # else new-line-group_opt
```

``` 
endif-line:
  # endif new-line
```

146) 因此，预处理指令通常被称为“行”（lines）。“行”没有其他语法意义，因为在预处理期间的某些情况下之外，所有空白都是等价的（例如 16.3.2 中的 `#` 字符串字面量创建运算符）。

``` 
control-line:
# include pp-tokens new-line
# define identifier iparen replacement-list new-line identifier replacement-list-new-line
# define identifier iparen ... ) replacement-list-new-line
# define identifier iparen identifier-list, ... replacement-list-new-line
# undef pp-tokens new-line
# line pp-tokens_opt new-line
# error pp-tokens_opt new-line
# pragma pp-tokens_opt new-line
# new-line
text-line:
pp-tokens_opt new-line
non-directive:
pp-tokens new-line
lparen:
a a ( character not immediately preceded by white-space
identifier-list:
identifier
identifier-list , identifier
replacement-list:
pp-tokens_opt
pp-tokens:
preprocessing-token
pp-tokens preprocessing-token
new-line:
t new-line character
```

2 行不应以 `#` 预处理标记开头。非指令不能以语法中出现的任何指令名称开头。

3 当在被跳过的组（16.1）中时，指令语法被放宽，允许在指令名称和随后的换行符之间出现任何序列的预处理标记。

4 在预处理指令内部，预处理标记之间（从指令标记之后到终止换行符 之前）出现的唯一空白字符是空格（space）和水平制表符（包括在翻译阶段 3 中替换了注释或可能的其他空白字符的空格）。

5 实现可以且应当跳过源文件的部分内容，包含其他源文件，并替换宏。这些能力被称为预处理，因为从概念上说，它们发生在生成的翻译单元进行翻译之前。

6 除非另有说明，预处理指令内的预处理标记不受宏展开的影响。

> 示例：输入：
```
#define EMPTY
EMPTY # include <file.h>
```
第二行上的预处理标记序列不是预处理指令，因为它不是在翻译阶段 4 开始时以 `#` 开头的，尽管在宏 `EMPTY` 被替换后它会变成 `#` 开头。 — 示例结束

## 16.1 条件包含 [cpp-cond]

+ 1 包含条件包含的表达式应该是整表达式表达式，标识符（那些与关键字词法相同的标识符）将按照下文¹⁴⁷ 进行解释，并且它可能包含如下形式的一元运算符表达式：
```
defined identifier
```
或者
```
defined (identifier)
```
如果标识符当前被定义为宏名称（即它前面有前缀，或者它是 `#define` 指令的主体且中间没有具有相同标识符的 `#undef` 指令），则评估为 1；否则评估为 0。

+ 2 在所有宏替换发生后，剩余的（将成为控制表达式的预处理标记列表）每个预处理标记都应以标记的字面形式（2.7）存在。

+ 3 以下的预处理指令
```
# if constant-expression-new-group_opt
# elif constant-expression-new-group_opt
```
检查控制表达式评估值是否非零。

+ 4 在评估之前，将成为控制表达式的预处理标记列表中的宏调用将被替换（那些被 `defined` 一元运算符修改的除外），就像正常情况一样。如果定义的标记是由于此过程而生成的，或者如果 `defined` 一元运算符在宏替换之前不符合指定的两种形式之一，则行为是未定义的。如果由于宏展开执行了 `defined` 一元运算符，则除 `true` 和 `false` 之外的所有剩余的标识符和关键字¹⁴⁸ 都被替换为 pp-number 0，然后每个预处理都评估为一个标记。生成的标记包含控制表达式，该表达式根据规则进行评估。（此处省略了大量重复的句子描述）

5 实现可以且应当跳过源文件的部分内容，包含其他源文件，并替换宏。这些能力被称为预处理，因为从概念上说，它们发生在生成的翻译单元进行翻译之前。

6 预处理指令内的预处理标记除非另有说明，不受宏展开的影响。

## 16.2 源文件包含 [cpp.include]

1 指令应识别一个可以处理头文件。

2 形式如下预处理指令
```
# include <h-char-sequence> new-line
```
在一组实现的定义处根据 < > 分隔符之间的指定序列搜索头文件，并将该指令替换为头文件的完整内容。搜索的位置由实现定义。

3 形式如下预处理指令
```
# include "q-char-sequence" new-line
```
将指令替换为由 " 分隔符指定的源文件的完整内容。源文件的搜索取决于实现。如果不支持，或搜索失败，则对指令进行重新处理，类似于
```
# include <h-char-sequence> new-line
```
使用原始指令中相同的序列（包括任何字符）。

4 形式如下的预处理指令
```
# include pp-tokens new-line
```
