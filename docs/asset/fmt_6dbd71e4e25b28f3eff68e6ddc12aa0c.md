
声明一个整数 `i`，一个指向整数的指针 `pi`，一个接受 `int` 参数并返回 `int` 的函数 `f`，一个接受 `int` 参数并返回 `int` 指针的函数 `fpi`，一个接受 `const char*` 和 `const char` 参数的函数 `(*fppi)`，一个接受 `int` 参数并返回 `int` 的函数 `(*fppi)(int)`。

注：原文提供的文本中存在大量重复的段落，根据指令“不要重复输出原文”的原则，译文已对重复内容进行了精简或合并，确保了逻辑的连贯性并避免了冗余。

当省略号出现在没有逗号的参数声明末尾时，存在语法歧义。在这种情况下，如果参数类型名为未展开的模板包，则将其解析为抽象声明符的一部分；否则，它被解析为参数声明的一部分。

1. 包含省略号的声明符的函数类型 `typedef` 仅用于函数声明的函数类型。

# ISO/IEC 14882:2011(E)

```cpp
typedef void Fv(); // OK：等同于 fv;
F fv;               // 非良的
F fv() { // OK：fv 的定义
void fv() {
```

# 8.3.6 默认参数 [dcl.default]

- 如果在参数声明中指定了初始化句，则该初始化句用作默认参数。默认参数将在缺失参数的调用中使用。

- 示例：声明

```cpp
void print(int, int i = 4);
```

声明了一个可以接受零、一个或两个 `int` 参数的函数。它可以以以下任何方式调用：

```cpp
point(1,2); point(1);
```

后两种分别等同于 `point(1,4)` 和 `point(3,4)`。—— 示例结束

- 默认参数应在函数声明的参数声明句或模板参数 `14.1` 中指定；对于后者，初始化句应为赋值表达式。不应为参数包指定默认参数。如果在参数声明句中指定，它不应出现在参数声明的声明符或抽象声明符内。101

100 人可以通过引入一个逗号（使省略号被解析为参数声明句的一部分）或为参数引入一个名称（使省略号被解析为声明符 ID）来消除解析歧义。

101 这意味着默认参数不能出现在（例如）函数指针、函数引用或 `typedef` 声明中。

# ISO/IEC 14882:2011(E)

4. 对于非模板函数，可以在同一作用域内的函数后继声明中添加默认参数。不同作用域的声明具有完全不同的默认参数集。也就是说，内层作用域的声明不会从外层作用域的声明获取默认参数，反之亦然。在给定的函数声明中，在带有默认参数的参数之后的每个参数都应该在此声明或之前的声明中提供默认参数，或者是一个函数参数包 `function parameter pack`。默认参数不应随后的声明重新定义（即使值相同也不行）。[示例：

```cpp
void g(int) = 0, ...);
// OK，省略号不是参数，它可以位于
// 带有默认参数的参数之后
void f(int);
void f(int, int) = 7);
f(3); // OK，调用 f(3, 7)
void f(int, int = 1);
// 错误没有使用
// 外围作用域的默认值
void m() {
    void f(int, int);
    // 无默认参数
    f(4); // 错误：参数数量错误
    void f(int, int = 5);
    // OK，调用 f(4, 5)
    f(4); // 错误：不能重新定义，即使
    void f(int, int = 5);
    // 相同的值
}
void n() {
    f(6);
    // OK，调用 f(6, 7)
}
```

— ] — 对于在不同翻译单元中定义的内联函数，在翻译单元结束时累计的默认参数集应该是相同的；参见 `3.2`。如果声明指定了默认参数表达式，该声明应为定义，并且应该是该翻译单元中函数或模板的唯一声明。

5. 默认参数被隐式转换（第 `4` 节）为参数类型。默认参数具有与在声明为该参数类型的变量时该参数相同的语义约束，并使用转换语义 `8.5`。默认参数中的名称被绑定，并在默认参数出现的位置处检查语义约束。函数模板和类模板成员函数中默认参数的查找和语义约束检查按照 `14.7.1` 节描述执行。[示例：在以下代码中，`g` 将使用值 `f(2)` 被调用：

```cpp
int a = 1;
int f(int);
int g(int x = f(a)); // 默认参数：f(::)
void h() {
    a = 2;
    int a = 3;
    g();
    // g(f(::))
}
```

— ] [注：在成员函数声明中，默认参数中的名称按照 `3.4.1` 节描述进行查找。访问检查按照第 `11` 节描述应用于默认参数中的名称。—注

§ 8.3.6

6. 类模板成员函数外，出现在类定义之外的成员函数中的默认参数将被添加到类定义中成员函数声明所提供的默认参数集中。类模板成员函数的默认参数应在类模板内对该成员函数的初始声明中指定。[示例：

```cpp
class C {
    void f(int i = 3);
    void g(int i, int j = 99);
};
```

```cpp
void C::f(int i = 3) { // 错误：默认参数已经在
} 类作用域内指定
void C::g(int i = 88, int j) { // 在此翻译单元中，
// C::g 可以不带参数被调用
```

- 示例结束

7. 默认参数中不应使用局部变量。[示例：

```cpp
void f() {
    int i;
    extern void g(int x = i); // 错误
    ...
}
```

- 示例结束

8. 默认参数中不应使用关键字 `this`。[示例：

```cpp
class A {
    void f(A* p = this) {} // 错误
}
```

- 示例结束

9. 默认参数每次调用函数时都会求值。函数参数的求值顺序是不确定的。因此，函数在默认参数之前声明的函数参数，即使它们未被求值，也会隐藏命名空间和类成员。[示例：

```cpp
int a;
int f(int a, int b = a); // 错误：参数 a 用于默认参数
int f;
g(float i, int i = i)); // 错误：参数 i 在
h(int a, int b = sizeof(a)); // 错误：参数 a 在
```

- 示例结束 同样，非静态成员不应用于默认参数，除非它作为标识符表达式 `5.2` 或被用于形成成员的指针 `5.3`。`X::mem(i)` 的声明是无效的，因为为非静态成员 `X::a` 未提供对象。

```cpp
int b;
class X {
    int a;
    int mem(int i = a); // 错误：非静态用于默认参数
```

§ 8.3.6

ISO/IEC 14882:2011(E)

```cpp
int mem2(int i = b);
    static int b;
// OK；使用 X::b
```

`X::mem2()` 的声明是有意义的，但不需要对象来访问静态成员 `X::b`。类、对象和成员在第 `9` 节描述。默认参数不是函数类型的一部分。[示例：

```cpp
int f(int = 0);
void h() {
    int j = f(1); // OK，意味着 f(0)
    int k = f(0) 
}
```

```cpp
int (*p)(int) = &f;
int (*p2)() = &f; // 错误：类型不匹配
```

- 示例结束 当通过使用声明 `7.3` 引入函数声明时，与声明相关的任何默认参数都是知的。如果在命名空间中重声明带有额外参数的函数，这些额外参数在重声明后的任何点都是知的。

10. 虚函数使用由指针或引用定义的声明中的默认参数。派生类中的覆盖函数不会从它所覆盖的函数获取参数。[示例：

```cpp
struct A {
    virtual void f(int a = 7);
};
struct B : public A {
    void f(int a);
};
void m() {
    B* pb = new B;
    A* pa = pb;
    pa->f(0); // OK，调用 A::f(0)
    pb->f(); // 错误：B::f() 参数数量错误
}
```

- 示例结束

## 8.4 函数定义 [dcl.ft.def]

## 8.4.1 一般 [dcl.ft.def.general]

函数定义的形式如下：

```cpp
function-definition:
    attribute-specifier-seq_opt decl-specifier-seq_opt declarator virt-specifier-seq_opt function-body;
function-body:
    declaration-initializer-seq_opt compound-statement
    function-try-block
    = default;
    = delete;
```

## § 8.4.1

对函数体的任何形式引用都应解释为对非终端 `function-body` 的引用。函数定义中的可选 `attribute-specifier-seq` 属于函数。`virt-specifier-seq` 只有当它是成员指定符 `9.2` 时才能作为函数定义的一部分

4. 函数定义中的声明符应具有形式：

```cpp
D1 ( parameter-declarator-clause ) cv-specifier-seq_opt
    virt-specifier-seq_opt exception-specifier-seq_opt attribute-specifier-seq_opt trailing-return-type_opt
```

如 `8.3.5` 所示。函数应仅在命名空间或类作用域内定义。

3. [示例：一个完整函数定义的简单示例

```cpp
int max(int a, int b, int c) {
    int m = (a > b) ? a : b;
    return (m > c) ? m : c;
}
```

这里是 `declar-specifier-seq`：`max(int a, int b, int c)` 是声明符；{ /* ... } 是 `function-body`。
- 示例结束]

4. 声明初始化仅在构造函数中使用；参见 `12.1` 和 `12.6`。

5. `cv-qualifier-seq` 或 `ref-qualifier`（或两者）都可以作为非静态函数声明、非静态函数定义或指向成员函数的指针 `8.3.5` 的一部分；参见 `9.3.2`。

6. [注：未使用的参数不需要命名。例如，

```cpp
void print(int a, int /*) {
    std::printf("a = %d\n",a);
}
```

--- 注结束]

7. 在函数体内，函数局部预定义变量隐式定义了一个具有静态存储期的块作用域对象（参见 `3.3.3`）。

8. 函数局部预定义变量 `__function__` 的定义类似于提供了如下形式的定义

```cpp
static const char __function__ = "function-name";
```

其中 `function-name` 是一个实现字符串。不确定变量是否与程序中的其他对象具有不同的地址。

[示例]

```cpp
struct S {
    S() : __function__() {} // OK
    const char *s = __function__;
};
void f(const char *s = __function__); // 错误：__function__ 未声明
```
