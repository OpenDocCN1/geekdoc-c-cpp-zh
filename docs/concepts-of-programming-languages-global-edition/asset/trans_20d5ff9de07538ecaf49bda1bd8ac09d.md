

## 摘要

大小写敏感性和下划线的使用是名称设计的两个问题。

变量可以用六元组属性来表征：名称、地址、值、类型、生命周期和作用域。

别名是指两个或多个变量绑定到同一存储地址的情况。它们被认为不利于可靠性，但很难完全从一种语言中消除。

绑定是将属性与程序实体关联起来的过程。了解属性绑定到实体的绑定时间对于理解编程语言的语义至关重要。绑定可以是静态的也可以是动态的。声明，无论是显式的还是隐式的，都提供了一种指定变量与类型静态绑定的方式。一般来说，动态绑定允许更大的灵活性，但以可读性、效率和可靠性为代价。

通过考虑它们的生命周期，标量变量可以分为四类：静态、栈动态、显式堆动态和隐式堆动态。

静态作用域是 ALGOL 60 及其一些后继语言的核心特性。它提供了一种简单、可靠且高效的方法，使子程序中非局部变量的可见性成为可能。动态作用域比静态作用域提供更大的灵活性，但同样以可读性、可靠性、效率为代价。

大多数函数式语言允许用户使用 let 构造创建局部作用域，从而限制其所定义名称的作用域。

语句的引用环境是所有对该语句可见的变量的集合。

命名常量本质上只是变量，它们的值仅绑定一次。

## 复习问题

- 1. 什么是保留字？
- 2. 在 Java 和 C# 中，名称可以有多长？
- 3. 变量的地址是什么？
- 4. 如何表征一个变量？
- 5. 什么是类型推断？举例说明。
- 6. 内存单元的释放是什么？
- 7. 在语言设计和实现之后，程序中绑定可以发生的四个时间是什么？
- 8. 变量的生命周期是什么？
- 9. 栈动态变量的用途是什么？
- 10. 动态类型绑定的优点和缺点是什么？
- 11. 定义静态、栈动态、显式堆动态和隐式堆动态变量。它们的优点和缺点是什么？
- 12. 什么是块结构化语言？
- 13. 在静态作用域程序中，对非局部变量的引用如何连接到其定义？
- 14. 静态作用域的一般问题是什么？
- 15. 语句的引用环境是什么？
- 16. 子程序的静态祖先是什么？子程序的动态祖先是什么？
- 17. 什么是块？
- 18. 函数式语言中 let 构造的目的是什么？
- 19. ML let 构造中定义的名称与 C 块中声明的变量有什么区别？
- 20. 描述 F# let 在函数内部和函数外部的封装。
- 21. 我们何时可以称一个子程序是活动的？
- 22. 什么是变量初始化？

## 问题集

- 1. 以下哪种标识符形式最可读？支持你的决定。
  - FirstName
  - First_Name
  - firstname
- 2. 某些编程语言具有静态变量。拥有静态变量的明显优点和缺点是什么？
- 3. 在你熟悉的某种语言中写一个包含一个算术运算符的简单赋值语句。对于语句的每个组成部分，列出确定执行时语义所需的各种绑定。对于每个绑定，指出该语言使用的绑定时间。
- 4. 动态类型绑定与隐式堆动态变量密切相关。解释这种关系。
- 5. 描述一种动态作用域使程序难以阅读的情况。
- 6. 考虑以下 JavaScript 骨架程序：

```
// The main program
var x;
function sub1() {
var x;
function sub2() {
    ...
}
}
function sub3() {
    ...
}
```

假设该程序的执行顺序如下：

- main calls sub1
- sub1 calls sub2
- sub2 calls sub3

a. 假设使用静态作用域，在以下情况下，对 x 的引用正确的声明是什么？
  - i. sub1
  - ii. sub2
  - iii. sub3

b. 重复 a 部分，但假设使用动态作用域。

7. 假设以下 JavaScript 程序使用静态作用域规则解释。在函数 sub1 中显示的 x 的值是多少？在动态作用域规则下，在函数 sub1 中显示的 x 的值是多少？

```
var x;
function sub1() {
    document.write("x = " + x + "");
}
function sub2() {
    var x;
    x = 10;
    sub1();
}
x = 5;
sub2();
```

8. 考虑以下 JavaScript 程序：

```
var x, y, z;
function sub1() {
    var a, y, z;
function sub2() {
    var a, b, z;
    ...
}
...
}
function sub3() {
    var a, x, w;
    ...
}
```

列出在 sub1、sub2 和 sub3 的主体中可见的所有变量，以及它们在程序单元中的声明位置，假设使用静态作用域。

## 9. 考虑以下 Python 程序：

```
x = 1;
y = 3;
z = 5;
def sub1():
    a = 7;
    y = 9;
    z = 11;
    ...
def sub2():
    global x;
    a = 13;
    x = 15;
    w = 17;
    ...
def sub3():
    nonlocal a;
    a = 19;
    b = 21;
    z = 23;
    ...
...
```

列出在 sub1、sub2 和 sub3 的主体中可见的所有变量，以及它们在程序单元中的声明位置，假设使用静态作用域。

## 10. 考虑以下 C 程序：

```
void fun(void) {
    int a, b, c; /* definition 1 */
    ...
    while (...) {
        int b, c, d; /*definition 2 */
        ... <-- ---------- 1
        while (...) {
        int c, d, e; /* definition 3 */
        ... <-- ---------- 2
        }
        ... <-- ---------- 3
    }
    ... <-- ---------- 4
}
```

对于该函数中标记的四个点，列出每个可见变量，以及定义它的定义语句编号。

## 11. 考虑以下骨架 C 程序：

```
void fun1(void);  /* prototype */
void fun2(void);  /* prototype */
void fun3(void);  /* prototype */
void main() {
    int a, b, c;
    ...
}
void fun1(void) {
    int b, c, d;
    ...
}
void fun2(void) {
    int c, d, e;
    ...
}
void fun3(void) {
    int d, e, f;
    ...
}
```

给定以下调用序列并假设使用动态作用域，最后调用的函数执行期间可见哪些变量？每个可见变量都包含它被定义的功能名称。

- a. main calls fun1; fun1 calls fun2; fun2 calls fun3.
- b. main calls fun1; fun1 calls fun3.
- c. main calls fun2; fun2 calls fun3; fun3 calls fun1.
- d. main calls fun3; fun3 calls fun1.
- e. main calls fun1; fun1 calls fun3; fun3 calls fun2.
- f. main calls fun3; fun3 calls fun2; fun2 calls fun1.

12. 考虑以下用 JavaScript-like 语法编写的程序：

```
// main program
var x, y, z;

function sub1() {
var a, y, z;
...
}
function sub2() {
var a, b, z;
...
}
function sub3() {
var a, x, w;
...
}
```

给定以下调用序列并假设使用动态作用域，最后激活的子程序执行期间可见哪些变量？每个可见变量都包含它被声明的单元名称。

- a. main calls sub1; sub1 calls sub2; sub2 calls sub3.
- b. main calls sub1; sub1 calls sub3.
- c. main calls sub2; sub2 calls sub3; sub3 calls sub1.
- d. main calls sub3; sub3 calls sub1.
- e. main calls sub1; sub1 calls sub3; sub3 calls sub2.
- f. main calls sub3; sub3 calls sub2; sub2 calls sub1.

- 1. Perl 允许静态和一种动态作用域。编写一个 Perl 程序同时使用这两种作用域，并清楚地显示两种作用域效果的差异。清楚地解释本章中描述的动态作用域与 Perl 中实现的那种之间的区别。
- 2. 编写一个 Common Lisp 程序，清楚地显示静态作用域和动态作用域之间的区别。
- 3. 编写一个 JavaScript 脚本，其中子程序嵌套三层深，并且每个嵌套子程序引用其所有封闭子程序中定义的所有变量。
- 4. 使用 Python 重复编程练习 3。
- 5. 编写一个 C99 函数，其中包含以下语句序列：

```
x = 21;
int x;
x = 42;
```

运行程序并解释结果。用 C++ 和 Java 重写相同的代码并比较结果。
- 6. 在 C++、Java 和 C# 中编写测试程序，以确定 for 语句中声明的变量的作用域。具体来说，代码必须确定 for 语句体之后是否可见该变量。
- 7. 在 C 或 C++ 中编写三个函数：一个静态声明一个大数组，一个在栈上声明同一个大数组，一个从堆中创建同一个大数组。多次调用每个子程序（至少 100,000 次）并输出每个所需的时间。解释结果。

