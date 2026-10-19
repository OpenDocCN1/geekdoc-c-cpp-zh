

示例 2：

```
void f(int n) {
    [] { n = 1; };                // error: n is not odr-usable due to intervening lambda-expression
    struct A {
        void f() { n = 2; }         // error: n is not odr-usable due to intervening function definition scope
    };
    void g(int = n);               // error: n is not odr-usable due to intervening function parameter scope
    [=](int k = n) {};             // error: n is not odr-usable due to being
                                   // outside the block scope of the lambda-expression
    [&] { [n]{ return n; }; };     // OK
}
```

—— 示例结束

10 对于在该程序中、在丢弃语句（8.5.2）之外被 odr-used 的每个非内联函数或变量，程序应恰好包含一个定义；不需要诊断。该定义可以显式地出现在程序中，可以在标准库或用户自定义库中找到，或者（在适当情况下）被隐式定义（见 11.4.5.2、11.4.5.3、11.4.7 和 11.4.6）。

示例 3：

```
auto f() {
    struct A {};
    return A{};
}
decltype(f()) g();
auto x = g();
```

包含此翻译单元的程序是非良构的，因为 g 被 odr-used 但没有定义，并且它无法在任何其他翻译单元中定义，因为局部类 A 不能在此翻译单元之外被命名。—— 示例结束

11 定义域是私有模块片段或翻译单元中排除其私有模块片段（如果有）的部分。内联函数或变量的定义，应当在该函数或变量于丢弃语句之外被 odr-used 的每个定义域结束时可达。

12 类的定义应当在该类以需要类类型完整的方式被使用的每个语境中可达。

示例 4：以下完整翻译单元是良构的，即使它从未定义 X：

```
struct X;          // declare X as a struct type
struct X* x1;      // use X in pointer formation
X* x2;             // use X in pointer formation
```

—— 示例结束

注 3：关于声明和表达式的规则描述了在哪些语境中需要类类型完整。类类型 T 在以下情况下必须是完整的：

- (12.1) —— 定义了类型 T 的对象（6.2），或
- (12.2) —— 声明了类型 T 的非静态类数据成员（11.4），或
- (12.3) —— T 被用作 new 表达式中的分配类型或数组元素类型（7.6.2.8），或
- (12.4) —— 对引用类型 T 对象的 glvalue 应用了左值到右值转换（7.3.2），或
- (12.5) —— 表达式被（隐式或显式地）转换为类型 T（7.3、7.6.1.4、7.6.1.7、7.6.1.9、7.6.3），或
- (12.6) —— 一个不是空指针常量且类型不是 cv void* 的表达式被使用标准转换（7.3）、dynamic_cast（7.6.1.7）或 static_cast（7.6.1.9）转换为指向 T 的指针或指向 T 的引用，或
- (12.7) —— 对类型 T 的表达式应用了类成员访问运算符（7.6.1.5），或
- (12.8) —— typeid 运算符（7.6.1.8）或 sizeof 运算符（7.6.2.5）应用于类型 T 的操作数，或
- (12.9) —— 定义（6.2）或调用（7.6.1.3）了一个返回类型或实参类型为 T 的函数，或
- (12.10) —— 定义了以类型 T 为基类的类（11.7），或
- (12.11) —— 对类型 T 的左值进行了赋值（7.6.19），或
- (12.12) —— 类型 T 是 alignof 表达式的对象（7.6.2.6），或
- (12.13) —— 异常声明具有类型 T、对 T 的引用或指向 T 的指针（14.4）。

—— 注结束

13 在一个程序中，可以有多个

- 类类型（第 11 条），
- 枚举类型（9.7.1），
- 内联函数或变量（9.2.8），
- 模板实体（13.1），
- 参数的默认实参（对于给定作用域中的函数）（9.3.4.7），或
- 默认模板实参（13.2）

的定义，前提是每个定义出现在不同的翻译单元中，并且这些定义满足以下要求。

给定这样一个在多个翻译单元中定义的实体 D，对于 D 的所有定义，或者，如果 D 是未命名枚举，对于在任何给定程序点可达的 D 的所有定义，应满足以下要求。

- 每个这样的定义不得附属于具名模块（10.1）。
- 每个这样的定义应由相同的记号序列组成，其中闭包类型的定义被认为由对应 lambda 表达式的记号序列组成。
- 在每一个这样的定义中，根据 6.5 查找的对应名称在重载决议（12.4）和部分模板特化匹配（13.10.4）之后应指代同一实体，但名称可以指代
  - 具有内部链接或没有链接的非 volatile const 对象，如果该对象
    - 在 D 的所有定义中具有相同的字面量类型，
    - 用常量表达式（7.7）初始化，
    - 在 D 的任何定义中均未被 odr-used，并且
    - 在 D 的所有定义中具有相同的值，
    或
  - 一个具有内部链接或没有链接的引用，该引用用常量表达式初始化，使得该引用在 D 的所有定义中指代同一实体。
- 在每一个这样的定义中，除了在 D 的默认实参和默认模板实参内，对应的 lambda 表达式应具有相同的闭包类型（见下文）。
- 在每一个这样的定义中，对应的实体应具有相同的语言链接。
- 在每一个这样的定义中，所引用的重载运算符、对转换函数、构造函数、operator new 函数和 operator delete 函数的隐式调用应指代同一函数。
- 在每一个这样的定义中，由（隐式或显式）函数调用使用的默认实参，或由（隐式或显式）template-id 或 simple-template-id 使用的默认模板实参，被视为其记号序列存在于 D 的定义中；也就是说，默认实参或默认模板实参须遵守本段所述的要求（递归地）。
- 如果 D 是具有隐式声明的构造函数（11.4.5.2、11.4.5.3）的类，则构造函数好像在其被 odr-used 的每个翻译单元中被隐式定义，并且每个翻译单元中的隐式定义应为 D 的子对象调用同一构造函数。

示例 5：

```
// translation unit 1:
struct X {
  X(int, int);
  X(int, int, int);
};
X::X(int, int = 0) { }
class D {
  X x = 0;
};
D d1;
// X(int, int) called by D()
```

## 6.4.3 块作用域 [basic.scope.block]

1 在块（8.4）中声明的名字局部于该块；它具有块作用域。它的潜在作用域始于其声明点（6.4.2），止于其块末尾。在块作用域声明的变量是局部变量。

2 在异常声明中声明的名字局部于处理程序，并且不得在该处理程序的最外层块中重新声明。

3 在 init-statement、for-range-declaration 以及 if、while、for 和 switch 语句的条件中声明的名字局部于该 if、while、for 或 switch 语句（包括受控语句），并且不得在该语句的后续条件中，也不得在受控语句的最外层块（对于 if 语句，则为任一最外层块）中重新声明。

示例 1：

```
if (int x = f()) {
    int x;        // error: redeclaration of x
}
else {
    int x;        // error: redeclaration of x
}
```

—— 示例结束]

## 6.4.4 函数参数作用域 [basic.scope.param]

1 函数参数（包括出现在 lambda-declarator 中的参数）或函数局部预定义变量（9.5）具有函数参数作用域。参数或函数局部预定义变量的潜在作用域始于其声明点。如果最近的外围函数声明符不是函数定义的声明符，则潜在作用域止于该函数声明符的末尾。否则，如果函数具有 function-try-block，则潜在作用域止于最后一个关联的处理程序的末尾。否则，潜在作用域止于函数定义最外层块的末尾。参数名不得在函数定义的最外层块中，也不得在与 function-try-block 关联的任何处理程序的最外层块中重新声明。

## 6.4.5 函数作用域 [basic.funscope]

1 标签（8.2）具有函数作用域，可以在声明它们的函数中的任何位置使用。只有标签具有函数作用域。

## 6.4.6 命名空间作用域 [basic.scope.namespace]

1 命名空间定义的声明性区域是其命名空间体。在命名空间体中声明的实体称为命名空间成员，这些声明引入命名空间声明性区域中的名字称为命名空间成员名。命名空间成员名具有命名空间作用域。其潜在作用域从名字的声明点（6.4.2）起包括其命名空间；对于每个提名该成员命名空间的 using-directive（9.8.4），该成员的潜在作用域包括该 using-directive 潜在作用域中紧随该成员声明点之后的部分。

示例 1：

```
namespace N {
    int i;
    int g(int a) { return a; }
    int j();
    void q();
}
namespace { int l=1; }
// the potential scope of l is from its point of declaration to the end of the translation unit

namespace N {
    int g(char a) { // overloads N::g(int)
        return l+a;   // l is from unnamed namespace
    }

    int i;        // error: duplicate definition
    int j();      // OK: duplicate function declaration
```

