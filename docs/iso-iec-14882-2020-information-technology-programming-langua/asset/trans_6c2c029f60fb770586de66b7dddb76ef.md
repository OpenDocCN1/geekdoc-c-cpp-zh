

## ISO/IEC 14882:2020(E)

[Example 1:

```
// - File 1 -
#include "a.h"
#include "b.h"
B b;
A::A(){
  b.Use();
}
```

```
// - File 2 -
#include "a.h"
A a;
```

```
// - File 3 -
#include "a.h"
#include "b.h"
extern A a;
extern B b;

int main() {
  a.Use();
  b.Use();
}
```

It is implementation-defined whether either `a` or `b` is initialized before `main` is entered or whether the initializations are delayed until `a` is first odr-used in `main`. In particular, if `a` is initialized before `main` is entered, it is not guaranteed that `b` will be initialized before it is odr-used by the initialization of `a`, that is, before `A::A` is called. If, however, `a` is initialized at some point after the first statement of `main`, `b` will be initialized prior to its use in `A::A`. — end example]

6 它是实现定义的，非局部内联变量的动态初始化是否在 `main` 的第一个语句之前排序，或是否被推迟。如果被推迟，它在该变量的任何非初始化 odr-use 之前强发生。实现定义此类推迟的动态初始化在程序的哪些线程和哪些点发生。

7 它是实现定义的，非局部非内联变量的线程存储期动态初始化是否在线程的初始函数的第一个语句之前排序，或是否被推迟。如果被推迟，与线程 `t` 关联的初始化在 `t` 对在与待初始化变量相同的翻译单元中定义的任何非内联线程存储期变量的首次非初始化 odr-use 之前排序。实现定义此类推迟的动态初始化在程序的哪些线程和哪些点发生。

8 如果具有静态存储期或线程存储期的非局部变量的初始化通过异常退出，则调用函数 `std::terminate`（14.6.2）。

### 6.9.3.4 Termination [basic.start.term]

1 具有静态存储期的已构造对象（9.4）在调用 `std::exit`（17.5）作为其一部分时被销毁，并调用使用 `std::atexit` 注册的函数。对 `std::exit` 的调用在销毁和已注册函数之前排序。

> [Note 1: 从 `main` 返回会调用 `std::exit`（6.9.3.1）。 — end note]

2 给定线程内的具有线程存储期的已构造对象在从该线程的初始函数返回时以及该线程调用 `std::exit` 时被销毁。在该线程内所有具有线程存储期的已构造对象的销毁在销毁任何具有静态存储期的对象之前强发生。

3 如果一个具有静态存储期的对象的构造函数或动态初始化的完成在另一个之前强发生，则第二个对象的析构函数的完成在第一个对象的析构函数的启动之前排序。如果一个具有线程存储期的对象的构造函数或动态初始化的完成在另一个之前排序，则第二个对象的析构函数的完成在第一个对象的析构函数的启动之前排序。如果对象是静态初始化的，则对象按与对象被动态初始化时相同的顺序销毁。对于数组或类类型的对象，在构造子对象期间初始化的所有块作用域具有静态存储期的对象被销毁之前，该对象的所有子对象都被销毁。如果具有静态存储期或线程存储期的对象的销毁通过异常退出，则调用函数 `std::terminate`（14.6.2）。

## 7.2 Properties of expressions

### 7.2.1 Value category

Expressions are categorized according to the taxonomy in Figure 1.

![](img/f00894146489220e5849acc131e0a0e1_102_0.png)

Figure 1: Expression category taxonomy [fig:basic.lval]

- (1.1) — A glvalue is an expression whose evaluation determines the identity of an object, bit-field, or function.
- (1.2) — A prvalue is an expression whose evaluation initializes an object or a bit-field, or computes the value of an operand of an operator, as specified by the context in which it appears, or an expression that has type `cv void`.
- (1.3) — An xvalue is a glvalue that denotes an object or bit-field whose resources can be reused (usually because it is near the end of its lifetime).
- (1.4) — An lvalue is a glvalue that is not an xvalue.
- (1.5) — An rvalue is a prvalue or an xvalue.

Every expression belongs to exactly one of the fundamental classifications in this taxonomy: lvalue, xvalue, or prvalue. This property of an expression is called its value category.

> [Note 1: The discussion of each built-in operator in 7.6 indicates the category of the value it yields and the value categories of the operands it expects. For example, the built-in assignment operators expect that the left operand is an lvalue and that the right operand is a prvalue and yield an lvalue as the result. User-defined operators are functions, and the categories of values they expect and yield are determined by their parameter and return types. — end note]

> [Note 2: Historically, lvalues and rvalues were so-called because they appeared on the left- and right-hand side of an assignment (although this is no longer generally true); glvalues are “generalized” lvalues, prvalues are “pure” rvalues, and xvalues are “eXpiring” lvalues. Despite their names, these terms classify expressions, not values. — end note]

> [Note 3: An expression is an xvalue if it is:
>
> - (4.1) — the result of calling a function, whether implicitly or explicitly, whose return type is an rvalue reference to object type (7.6.1.3),
> - (4.2) — a cast to an rvalue reference to object type (7.6.1.4, 7.6.1.7, 7.6.1.9, 7.6.1.10, 7.6.1.11, 7.6.3),
> - (4.3) — a subscripting operation with an xvalue array operand (7.6.1.2),
> - (4.4) — a class member access expression designating a non-static data member of non-reference type in which the object expression is an xvalue (7.6.1.5), or
> - (4.5) — a `.*` pointer-to-member expression in which the first operand is an xvalue and the second operand is a pointer to data member (7.6.4).
>
> In general, the effect of this rule is that named rvalue references are treated as lvalues and unnamed rvalue references to objects are treated as xvalues; rvalue references to functions are treated as lvalues whether named or not. — end note]

[Example 1:

```
struct A {
    int m;
};
A&& operator+(A, A);
A&& f();

A a;
A&& ar = static_cast<A&&>(a);
```

The expressions `f()`, `f().m`, `static_cast<A&&>(a)`, and `a + a` are xvalues. The expression `ar` is an lvalue. — end example

5 The result of a glvalue is the entity denoted by the expression. The result of a prvalue is the value that the expression stores into its context; a prvalue that has type `cv void` has no result. A prvalue whose result is the value V is sometimes said to have or name the value V. The result object of a prvalue is the object initialized by the prvalue; a non-discarded prvalue that is used to compute the value of an operand of a built-in operator or a prvalue that has type `cv void` has no result object.

> [Note 4: Except when the prvalue is the operand of a `decltype`-specifier, a prvalue of class or array type always has a result object. For a discarded prvalue that has type other than `cv void`, a temporary object is materialized; see 7.2.3. — end note]

6 Whenever a glvalue appears as an operand of an operator that expects a prvalue for that operand, the lvalue-to-rvalue (7.3.2), array-to-pointer (7.3.3), or function-to-pointer (7.3.4) standard conversions are applied to convert the expression to a prvalue.

> [Note 5: An attempt to bind an rvalue reference to an lvalue is not such a context; see 9.4.4. — end note]

> [Note 6: Because cv-qualifiers are removed from the type of an expression of non-class type when the expression is converted to a prvalue, an lvalue of type `const int` can, for example, be used where a prvalue of type `int` is required. — end note]

> [Note 7: There are no prvalue bit-fields; if a bit-field is converted to a prvalue (7.3.2), a prvalue of the type of the bit-field is created, which can then be promoted (7.3.7). — end note]

7 Whenever a prvalue appears as an operand of an operator that expects a glvalue for that operand, the temporary materialization conversion (7.3.5) is applied to convert the expression to an xvalue.

8 The discussion of reference initialization in 9.4.4 and of temporaries in 6.7.7 indicates the behavior of lvalues and rvalues in other significant contexts.

9 Unless otherwise indicated (9.2.9.5), a prvalue shall always have complete type or the `void` type; if it has a class type or (possibly multi-dimensional) array of class type, that class shall not be an abstract class (11.7.4). A glvalue shall not have type `cv void`.

> [Note 8: A glvalue can have complete or incomplete non-void type. Class and array prvalues can have cv-qualified types; other prvalues always have cv-unqualified types. See 7.2.2. — end note]

10 An lvalue is modifiable unless its type is const-qualified or is a function type.

> [Note 9: A program that attempts to modify an object through a nonmodifiable lvalue or through an rvalue is ill-formed (7.6.19, 7.6.1.6, 7.6.2.3). — end note]

11 If a program attempts to access (3.1) the stored value of an object through a glvalue whose type is not similar (7.3.6) to one of the following types the behavior is undefined:55

- (11.1) — the dynamic type of the object,
- (11.2) — a type that is the signed or unsigned type corresponding to the dynamic type of the object, or
- (11.3) — a `char`, `unsigned char`, or `std::byte` type.

If a program invokes a defaulted copy/move constructor or copy/move assignment operator for a union of type `U` with a glvalue argument that does not denote an object of type `cv U` within its lifetime, the behavior is undefined.

> [Note 10: Unlike in C, C++ has no accesses of class type. — end note]

### 7.2.2 Type [expr.type]

1 If an expression initially has the type “reference to T” (9.3.4.3, 9.4.4), the type is adjusted to T prior to any further analysis. The expression designates the object or function denoted by the reference, and the expression is an lvalue or an xvalue, depending on the expression.

> [Note 1: Before the lifetime of the reference has started or after it has ended, the behavior is undefined (see 6.7.3). — end note]

2 If a prvalue initially has the type “cv T”, where T is a cv-unqualified non-class, non-array type, the type of the expression is adjusted to T prior to any further analysis.

3 The composite pointer type of two operands p1 and p2 having types T1 and T2, respectively, where at least one is a pointer or pointer-to-member type or `std::nullptr_t`, is:

