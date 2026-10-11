
-- 示例

14 `decltype` 的每次出现都被视为 x 已被转换为对闭包类型对应数据成员的访问（如果 x 是所指实体的 udr，则该成员将被声明）。[示例：

```cpp
void f0() {
  float x, *r = x;
  {
    decltype(x) y1; // y1 类型为 float
    decltype(x) y2 = y1; // y2 类型为 const float，因为此 lambda 不是 mutable 且 x 是左值
    decltype(x) r1 = y1; // r1 类型为 float（考虑转换）
    decltype(x) r2 = y2; // r2 类型为 float const
  }
}
```

-- 示例

15 当 `lambda` 表达式初始化时，捕获的实体被用于析构生成的闭包对象的每个非静态数据成员，并且对应初始化捕获的非静态数据成员由相应的*初始化*（可能是拷贝或析构）初始化。这些初始化按照非静态数据成员声明的（指定的）顺序进行。[注：这确保了析构顺序与构造相反。-- 注结束]

16 [注：如果非引用实体隐式或显式按引用捕获，在实体生命周期结束后调用相应的 *lambda 表达式* 的函数调用可能会导致未定义行为。-- 注结束]

# ISO/IEC 14882:2017(E)

17 简单捕获（simple-capture）后跟省略号（ellipsis）是一个包展开（17.5.3）。内联捕获（in-capture）后跟省略号是格式错误的。[示例: Args]

```cpp
template<class... Args>
void f(Args... args) {
    auto lm = {&args...} { return g(args...); };
    lm();
}
// end example
```

[expr.prim.fold]

### 8.1.6 折叠表达式 (Fold expressions)

1 折叠表达式在二元运算符上对模板参数包（17.5.3）执行折叠。

```
fold-expression:
  ( expression fold-operator ...)
  (.. fold-operator cast-expression ..)
  (cast-expression fold-operator cast-expression ..)
```

```
fold-order: one of
  * / % & | << >> =
  += -= *= /= &= &= <= <= &&=
  != | < > (.. op >=) && || | -*
```

2 形式为 `(op ...)` 的表达式，其中 `op` 是折叠运算符称为单元左折叠。单元左折叠和单元右折叠统称为单元折叠。在单元折叠中，转换表达式（cast-expression）应当包含一个未展开的参数包（17.5.3）。

3 形式为 `(op1 op2)` 的表达式，其中 `op1` 和 `op2` 是折叠运算符称为二元折叠。在二元折叠中，`op1` 和 `op2` 应该是相同的折叠运算符，且 `e1` 包含一个未展开的参数包（17.5.3），或者 `e2` 包含一个未展开的参数包，但不能两者都包含。如果 `e2` 包含未展开的参数包，该表达式称为二元左折叠。如果 `e1` 包含未展开的参数包，该表达式称为二元右折叠。[示例:

```cpp
template<typename Args>
bool f(Args... args) {
    return (true && .. args);
}

template<typename Args>
bool f(Args... args) {
    return (args + ... + args); // 错误：两个操作数都包含未展开的参数包
}
// end example
```

## 8.2 后置表达式 [expr.post]

+ 后置表达式从左到右分组。

```
postfix-expression:
primary-expression
postfix-expression < expr-or-braced-list >
postfix-expression < expression-list-opt >
simple-type-spec < expression-list-opt >
typename-spec < expression-list-opt >
simple-type-spec < braced-list
typename-spec < braced-list
postfix-expression . template_opt id-expression
postfix-expression > template_opt id-expression
postfix-expression . pseudo-destructor-name
postfix-expression - pseudo-destructor-name
postfix-expression ++
postfix-expression --
dynamic_cast < type-id > ( expression )
static_cast < type-id > ( expression )
reinterpret_cast < type-id > ( expression )
const_cast < type-id > ( expression )
typeid ( expression )
typeid ( type-id )
expr-list:
initializer-list
pseudo-destructor-name:
nested-name-specifier_opt type-name :: :: type-name
nested-name-specifier simple-template :: :: type-name
type-specifier
```

> [注：在 `dynamic_cast`, `static_cast`, `reinterpret_cast` 或 `const` 中，`type-id` 之后的 `>` 可能是将 `>>` 替换为两个连续的 `>` 标记导致的结果（17.2）。—— 注结束]

### 8.2.1 下标访问 [expr.sub]

+ 后置表达式后跟方括号中的表达式是一个后置表达式。其中一个表达式应当是 `T` 数组或指向 `T` 的指针，另一个应当是未转义的枚举类型或整数类型的数值。结果类型为 "`T`" 。类型 "`T`" 应当完全定义的对象类型。表达式 `E1[E2]`（根据定义）等同于 `*(E1)(E2)` [注：关于 `*` 和 `+` 的细节见 8.3 和 8.7，关于细节见 11.3.4。]—— 注结束]，除非在操作数为数组的情况下，如果操作数是 xvalue，则结果是内联操作数。表达式 `E1` 应当在表达式 `E2` 之前出现。

不应与内置下标配合大列表（braced-list）。

### 8.2.2 函数调用 [expr.call]

+ 函数调用是一个后置表达式，后跟包含可能为空的、逗号分隔的初始化列表构造，这些构造构成了函数的参数。后置表达式应当具有函数类型或函数指针类型。对于对非成员函数或静态成员的调用，后置表达式应当是引用函数的左值（此时在后置表达式上抑制了函数到指针的标准转换 (7.3)），或者，它应当具有函数指针类型。通过表达式函数类型调用函数是不同的；如果函数类型不匹配，所调用的函数定义的结果是未定义行为（10.5）。对于对非静态成员函数的调用，后置表达式应当是隐式的（12.2, 12.3）或显式的类成员访问（8.2.5），其 `id-expression` 为函数名，或者是选择成员的指针（8.5）；调用作为表达式所指向类的成员进行。在隐式类成员访问的情况下，对象是表达式指向的对象。[注：类的成员调用被解释为 (*) (12.2) 或显式调用——注结束] 如果使用了函数名，它可能会被转换（第10章），在这种情况下根据 10.3 中的规则选择相应的函数。如果表达式中的非静态成员函数是限定的，则调用它。这种调用被称为虚拟调用。[注：类型是对象当前值的类型。15.7 描述了虚拟函数的行为。—— 注结束]

> [注：如果使用了函数成员名，且命名查找（6.4）未找到该名的声明，则程序格式错误。此类调用不隐含函数。—— 注结束]

如果后置表达式指定析构函数（15.4），则函数调用的类型为 `void`；否则，函数调用的类型是静态选择的返回类型（即忽略关键字），即使该类型实际上定义。此返回类型应当的对象、引用或 `void`。

调用函数时，每个参数（11.3.5）应当用相应的参数类型初始化（11.6, 8.5, 15.1）。如果函数是非静态成员，该函数的参数（12.2.1）应当用被调用对象的指针初始化，其转换方式如同显式调用（8.4）。[注：对此转换不进行访问或检查：异常检查和分发与可能的（隐式）类成员访问操作（13.1, 14.2 和 15.1）相同 [注：这允许参数指向...]

# ISO/IEC 14882:2017(E)

## 8.2.4 伪析构函数

通过 `.` 或箭头 `->` 使用的伪析构函数名称表示由 `.` 或 detype-specifier 所指的非类类型的析构函数。该表达式的结果应仅作为函数调用运算符 `~` 的操作数，且此类调用的结果具有类型。其唯一效果是评估点或箭头之前的*后缀-表达式*。

`.` 运算符的左侧是标量类型。`->` 运算符的左侧是指向标量类型的指针。该标量类型是对象类型。该对象去限定符后的版本与由*伪析构函数名称* 所指的类型是同一种类型。此外，*嵌套-specifier_qt type-name :: type-name* 中的两个类型应共享相同的相同的作用域（忽略 cv 修饰符）。

## 8.2.5 类成员访问

一个表达式后跟一个点 `.` 或箭头 `->`，可选地后跟关键字 *template* (17.2)，然后后跟一个 *id-expression*，则评估点或箭头之前的后缀表达式，该评估的结果与 *id-expression* 一起决定了整个后缀表达式的结果。

对于第一种选项（点），第一个表达式应为具有完整类类型的值。对于第二种选项（箭头），第一个表达式应被转换为等效形式 `(*E1).E2`：8.2.5 的结果将仅处理第一种选项（点）。在其他情况下，`id-expression` 应该是该类的成员或其任一基类的成员。[注：类成员的名称被视为类的成员 — 注释结束] [注：6.5 在 `.` 和 `->` 之后如何查找名称 — 注释结束]

通过 `id-expression` `E1, E2` 评估后缀表达式：如果 `E1` 是对象表达式，且 `E2` 是位域字段，则确定 `E1` 和 `E2` 的类型和值。`E1` 的结果表示不存在 cv const，而 `E2` 代表 volatile 或 volatile 的类型。这些 均根据 6.9.3 的定义被保留的。

如果 `E2` 被声明为“对 `T` 的引用”，则 `E1` 是左值；`E2` 是左值。否则，`E1` 和 `E2` 的表达式指定类的类的成员。`E1` 的类型是 `T`。

- (4.1) 如果 `E2` 是静态数据成员且 `E2` 的类型是 `T`，则 `E1` 是左值；`E2` 的类型是 *cv-qt T*。该表达式指定由第一个表达式指定的对象的成员。如果 `E1` 是左值，则 `E2` 是左值；否则 `E2` 是右值。

- (4.2) 如果 `E2` 是一个（可能是重载的）成员函数，使用函数重载解析 (16.3) 来确定 `E2` 是否为非静态成员函数的引用。

- (4.3) 如果它指向静态成员函数且 `E2` 的类型是“返回 `T` 的参数-类型的函数”，则 `E1` 是左值；该表达式指定该静态成员函数。`E1` 的类型与 `E2` 的类型相同，即“返回 `T` 的参数-类型的函数”。

当类成员访问表达式被评估时，即使确定入口后缀表达式的值没有必要，也会发生子表达式评估，例如如果 `id-expression` 指的是一个静态成员。

- (4.3.2) — 否则，如果 `E1` 指向非静态成员函数且 `E2` 的类型是“带有参数-类型列表 cv ref-qualifier cv T 的函数”，则 `E2` 是 prvalue。该表达式指定一个非静态成员函数。该表达式只能作为成员调用的左操作数 (12.2.1)。[注：任何冗余的括号将被忽略 (8.1)。 — 注释结束]：`E2` 的类型是“带有参数-类型-cv cv T 的函数”。

- (4.4) — 如果 `E2` 不是类型，则表达式 `E1` 非法（ill-formed）。

- (4.5) — 如果 `E2` 是非静态枚举器或非静态成员函数，`E2` 的类型是 `T`，表达式 `E1.E2` 是 prvalue。`E2` 的类型是 `T`。

- 5 如果 `E2` 是非静态数据成员或非静态成员函数，如果 `E2` 的类直接是 `E2` 类 (14.2) 的歧义基类 (13.2)，则表达式非法。[注：如果该类是对象的歧义基类，程序也是非法的；14.2.]

## 8.2.6 递增和减

1 后缀 `++` 的值是其原始 [注：原始值 — 注释结束] 的值应该是可修改的值。操作的类型是算术类型或指向完整对象的指针；对象的值通过加 1 来修改。计算的值在对象修改之后按顺序执行。当不确定地引用到函数时，后缀 `++` 的操作是单次评估。[注：因此，函数调用不应在左值到右值的转换与后缀 `++` 相关的副作用之间介入。结果是一个 prvalue。结果的类型是操作数。如果操作数是无法表示递增的位字段，则结果的值由实现定义。见 8.7 和 8.1。

2 后缀 `-- (v)` 的操作数是将 `v` 转换为类型 `T` 的结果。[注：对于前缀递增和减，8.3. — 注释结束]

## 8.2.7 动态转换

1 表达式 `dynamic_cast<T>(v)` 的结果是将 `v` 转换为类型 `T` 的结果。`T` 应该是 prvalue 或指向完整类类型的指针，或者指向 `void` 的指针。`dynamic_cast` 运算符不应产生任何代价 (8.11)。

2 如果 `T` 是指针类型，`v` 应该是完整类类型的 prvalue，结果是 `T` 的 prvalue。如果 `T` 是右值引用，`v` 应该是完整类类型的左值，结果是 `T` 所指类型的左值。如果 `T` 是一个被 `T` 所引用的右值引用，`v` 应该是具有完整类类型的左值；结果是 `T` 所指类型的左值。

3 如果 `v` 的类型与 `T` 相同，或者它与 `T` 中的对象类型相同或具有更多 cv 修饰，则结果是（必要时进行转换）。

4 如果 `v` 是空指针，结果是类型 `T` 的空指针。

5 如果 `T` 是“指向 cv B 的指针”且 `v` 是“指向 cv D 的指针”，且 `D` 是 `B` 的基类，结果是指向 `D` 的指针。同样，如果 `T` 是“对 cv B 的引用”且 `v` 是“对 cv D 的引用”，且 `D` 是 `B` 的基类，结果是 `D` 对象的引用。`D` 是 `B`。示例：

```cpp
class A { virtual void f(); };
class B { virtual void g(); };
class D : public virtual A, private B { };
void f() {
    D* dp;
    B* bp = (B*)dp);    // 转换以打破保护
    A* ap = dp;          // 公有派生，不需要转换
    D& dr = dynamic_cast<D&>(*dp); // 失败
    ap = dynamic_cast<A*>(bp);  // 失败
    bp = dynamic_cast<B*>(ap);  // 失败
    ap = dynamic_cast<A>(*dp); // 成功
    bp = dynamic_cast<D>(*dp); // 非法（不是运行时检查）
}

class E : public D, public B { };
class F : public virtual E, public D { };
void h() {
    F* f;
    A* ap = af;          // 成功：产生唯一的 A
    D* dp = dynamic_cast<D>(*f); // 失败：产生空；f 有两个 D 对象
    E* ep = (E*)ap;      // 非法：从虚基类转换
    E* ep1 = dynamic_cast<E>(*f); // 成功
}
```

// 示例

## 8.2.8 类型识别

- 1. 类型表达式的结果是静态类型 `std::type_info` (21.7.2) 的一个值，动态类型为 `std::type_info` 或实现定义的公派生自类名

# ISO/IEC 14882:2017(E)

`std::type_info` 保留了 21.7.2.70 中描述的行为。该值所引用的对象的生命周期持续到程序结束。在程序结束时，是否对 `std::type_info` 调用析构函数是不指定的。

2 当将 `type` 作用于多态类的 glvalue 表达式（左值）(13.3) 时，结果指向一个 `std::type_info` 对象，代表该 glvalue 所指的最派生对象 (4.5)（即动态类型）的类型。如果该 glvalue 是通过对指针应用一元 *operator* 运算符得到的且该指针为空指针 (71.1)，则类型-标识 (type-id) 表达式抛出一个异常 (18.1)，该异常类型将匹配 `std::bad_exception` 类型的处理程序 (21.7.4)。

3 当将 `type` 作用于除多态类类型的 glvalue 以外的表达式时，结果指向一个表示表达式静态类型的 `std::type_info` 对象。不应用左值转右值 (7.1)、数组转指针 (7.2) 和函数转指针 (7.3) 转换。如果表达式涉及 prvalue（纯右值），则应用临时转换 (7.4)。该表达式是一个不求值的操作数（第 8 节）。

4 当将 `type` 作用于一个 glvalue 时，结果指向一个表示类型-标识的类型的 `std::type_info` 对象。如果类型-标识是对一个 cv-限定类型的引用，则结果指向一个表示该 cv-未限定引用的 `std::type_info`。如果类型-标识是一个类或对类的类的引用，则该类必须是完全定义的（completely-defined）。

5 如果表达式或类型-标识是 cv-限定类型，则类型表达式的结果指向一个表示该 cv-未限定类型的 `std::type_info` 对象。[示例]：
