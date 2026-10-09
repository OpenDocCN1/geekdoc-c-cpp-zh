
```
const int i = 10, &ci, *const cp = pc, **pc;
int *p = "*const cp = ci;
```

声明 `ci`，一个常量整数；`pc`，一个指向常量整数的指针；`cpc`，一个指向常量整数的常量指针；`ppc`，一个指向指向常量整数的指针；`i`，一个整数；一个指向整数的指针；`cp` 以及一个指向整数的常量指针。`ci`、`cpc` 和 `pc` 的值初始化后不能更改。`pc` 的值可以更改，`pc` 所指向的对象也可以。正确的修正示例为：

```
i = ci;
*cp = ci;
```

`pc++`;

`pc = cpc`;

`pc = p`;

`ppc = &pc`;

错误的操作示例：

```
ci = 1; // 错误
ci++; // 错误
pc = 2; // 错误
cp = &ci; // 错误
cpc++; // 错误
p = pc; // 错误
pp = &p; // 错误
```

每一个都是不可接受的，因为它们会改变声明为 `const` 的对象的值，或者之后可以通过 `cv` 未限定指针进行更改，例如：

```
ppc = &ci; // 正确，但由于之前的错误使 p 指向 ci
p = 5; // 覆盖 ci
```

- 示例结束

2 在声明 `attribute-specifier-seq_opt T D` 中，是一个未命名的标识符，该标识符的类型为 "`T`"。

3 在声明 `T D` 中，如果 `D` 具有形式

`( D1`

包含的声明符-`id` 的类型与声明 `T D1` 中包含的声明符-`id` 的类型相同。括号不改变嵌入的声明符-`id` 的类型，但它们可以改变复杂声明符的绑定。

4 注：形成指向引用类型的指针是格式错误的；参见 `9.3.4.3`。如果函数具有 `cv` 限定符或 `ref` 限定符，则形成功能性指针类型是格式错误的；参见 `9.3.4.6`。由于无法获取位域（`11.4.10`）的地址，指针永远无法指向位域。 — 注结束

# ISO/IEC 14882:2020(E)

```cpp
struct X {
  void f(int);
  int a;
};
struct Y {
  int X::* pmi = &X::a;
  void (X::* pmf)(int) = &X::f;
  char Y::* pmc = pmd;
};
```

将 `pmi`、`pmf` 和 `pmc` 分别声明为 `X` 类型成员的指针、指向 `void(int)` 类型 `X` 类型成员的指针、指向 `double` 类型成员的指针以及指向 `char` 类型成员的指针。尽管语法上如此，但 `pmc` 的声明是合法的，且从未拥有 `double` 类型的成员。同样，尽管 `Y` 是一个不完整类型，但 `pmc` 的声明也是合法的。`pmi` 和 `pmf` 可以如下所示使用：

```cpp
X obj;
// 给整数对象赋值 7
obj.**pmi = 7;
(obj.**pmf)(7);
// 使用参数 7 调用 obj 的成员函数
```

- 3 指针不应指向类的静态成员 (`11.4.9`)、引用类型的成员，或 "`cv void`"。

> [注 1: 参见 `7.6.2` 和 `7.6.4`。类型 "`pointer`" 与类型 "`pointer`" 是不同的，即：一个仅通过指向成员指针声明语法声明的指针，另一个通过指针声明语法声明。C++ 中没有“指向成员的引用”类型。]

# 9.3.4.5 数组

- 1 在声明 `D` 的形式为：

```cpp
D1 { [constant-expression,opt] attribute-spec-seq}
```

其中 `D1` 中声明符-`id` 的类型是“派生声明列表类型”，`D` 中声明符的类型是“派生声明列表的 N 个元素的数组”。该常量表达式应为类型 `std::size_t` (`7.7`) 的转换表达式。它的值指定了数组的边界，即数组中的元素个数；N 不应大于

- 2 在声明 `D` 的形式为：

```cpp
D1 { } attribute-spec-seq
```

其中 `D1` 中声明符-`id` 的类型是“派生声明列表类型”，`D` 中声明符的类型是“具有未知边界的 T 的派生声明列表数组”，除非另有规定。

- 3 形式为“N 个 U 的数组”或“未知边界的 U 的数组”的类型是数组类型。可选 `attribute-spec-seq` 属于数组类型。

- 4 `U` 用作数组元素类型；该类型不应是占位类型 (`9.2.9.6`)、引用类型、函数类型、未知边界类型或 `cv void`。

> [注 1: 数组可以从任何基本类型（`void` 除外）、指针、指向成员的指针、枚举或已知边界的数组构造。示例结束]

示例 1：

```cpp
float a[17], *f17; // float 数值数组和指向 float 成员的指针数组。示例结束
```

声明了一个 `float` 数值数组和一个指向 `float` 成员的指针数组。

- 5 任何形式为“`cv-qualifier-seq N` 个 `U` 的数组”的形式都会调整为“N 个 `cv-qualifier-seq U` 的数组”，对于“未知边界的 `U` 的数组”也是如此。

示例 2：

```cpp
typedef int A[5], AA[2]; // 类型是“5 个 const int 的数组”
typedef const CA; // 类型是“2 个 const int 的数组”
typedef const AA CAA; // 类型是“3 个 const int 的数组”示例结束
```

> [注 2: “N 个 `cv-qualifier-seq U` 的数组”具有 `cv-qualifier` 类型；参见 `6.8.4`。注结束]

- 6 类型为“N 个元素的数组”的对象包含一组连续分配的、非空的 N 个相同类型的子对象，称为数组的元素，并从 0 到 N-1 编号。

- 7 除了允许使用不完整类型的声明外，在函数参数的声明中，某些情况下可以省略数组边界 (`9.3.4.6`)。当通过初始化器初始化并声明类型为的对象（但不是非静态数据成员）时，也可以省略数组边界 (`9.4`, `11.4`, `7.6.1.4`, `7.6.2.8`)。在这些情况下，数组边界是根据提供的初始元素个数（假设为 N）计算 (`9.4.2`)，且数组的类型是“N 个元素的数组”。

- 8 只要在指定边界的相同作用域内存在该实体的先行声明，省略的数组边界应与之前的声明相同，对于类静态成员的声明也是如此。

[示例 3：

```cpp
extern int x[10];
struct S {
    static int y[10];

    int x[];      // OK：边界为 10
    int s[];     // OK：边界为 10
};

void f() {
    extern int x;
    int i = sizeof(x); // 错误：不完整对象类型
}
// 示例结束

[注 3: 当多个“数组”说明连续相邻时，会创建一个多维数组类型；只有第一个元素是五个元素，其中每个元素都是一个数组。整个数组可以被视为具有秩 5x 三维整数数组。表达式 `x[i]`, `x[i][j]`, `x[i][j][k]` 可能出现在表达式中。`x` 通过数组到指针的转换 (`7.3.3`) 变为指向 5x 二维数组的指针指向数组的第一个元素，其中 `i=sizeof(x)`。间接的结果是数组的第 i 个元素（整数）。如果有另一个下标，则同样适用，`x[i][j]` 是第二个数组的第 i 个元素（整数数组），而 `x[i][j][k]` 是第三个数组的第 k 个元素（整数）。示例结束

示例 4：

```cpp

int x[][];

```

[注 10: 影响数组类型的转换参见 `7.3.3`。注结束

[注 11: 大小说明符可以为类进行重载 (`12.6.5`)。参见 `7.6.1`。注结束

### 9.3.4.6 函数

在声明 `D` 中，存在 `D (class) cv-qualifier-seq ref-qualifier-opt noexcept-specifier-opt attribute-specifier-seq`

且声明符-`id` 的类型来自于声明 `D`，声明符的类型是“派生声明列表 `noexcept_opt` 的 `parameter-type-list cv-qualifier-opt ref-qualifier-opt` 返回 `U` 的函数”，

- `parameter-type-list` 根据下述的 `parameter-class` 导出，且仅当异常说明 (`14.5`) 为非抛出时，可选的 `noexcept` 存在。

- 可选的 `specifier-seq` 属于函数类型。

# ISO/IEC 14882:2020(E)

在声明 `T` 中，形式为

```cpp

D1 ( parameter-declaration-clause )opt cv-qualifier-specifier-opt ref-qualifier-specifier-opt noexcept_opt attribute-specifier-opt trailing-return-type T

```

并且声明 `D` 中的声明符类型来自于函数调用；`D1` 是“派生声明列表 `no_opt` 的 `parameter-type-list cv-qualifier-specifier-opt ref-qualifier-opt` 返回 `U` 的函数”，

- `parameter-type-list` 根据下述的 `parameter-declaration-clause` 导出

- `U` 是 `trailing-return-type` 指定的类型，且

- 仅当异常说明为非抛出时，`noexcept` 指定存在。

可选的 `attribute-specifier` 出现在函数调用：

- 3 类型 是函数类型。

```cpp

parameter-declaration-clause:

parameter-declaration-list_opt ...opt

parameter-declaration-list , ...opt

parameter-declaration-list:

parameter-declaration:

parameter-declaration , parameter-declaration

parameter-declaration:

attribute-specifier-opt declarator-spec

attribute-specifier-opt declarator-spec declar = initialize-clause

attribute-specifier-opt declarator-spec abstract-declarator_opt

attribute-specifier-opt declarator-spec abstract-declarator_opt = initialize-clause

```

参数声明中的可选 `attribute-specifier-clause` 出参数：

- 4 `clause` 决定了在调用函数时可以指定什么声明符：

> [注 1: `parameter-declaration-clause` 为空，函数不接受参数。由单个非依赖类型的未命名参数组成的参数列表等于空参数列表。除此特殊情况外，参数的类型不为 `void`。

> `parameter-declaration` 以省略号或函数参数包 (`13.7.4`) 结束，参数个数应大于或等于具有默认参数且不是函数包的参数个数。语法正确且 "..." 不是抽象声明符的一部分时，“...” 等同于 "..."。

> [示例 1: 声明

```cpp

int print(const char*, *);

```

声明了一个可以使用不同数量和类型的声明符调用的函数。

```cpp

print("hello world", "%d", a, b);

```

然而，第一个参数必须是可以转换为 `const char.*` 的类型——示例结束]

> [注 2: 标准头文件 `<utilityarg>` (`13.7.2`) 包含使用省略号 (`13.7.6` 和 `13.7.13`) 访问参数的机制——注结束]

- 5 函数类型使用以下规则确定。每个参数（包括函数包）的类型根据自身的 `decl-specifier` 和声明符确定。在确定每个参数的类型后，任何类型为“`T` 的数组”或类型为 `T` 的调整为指向 `T` 的指针。在参数类型列表之后，在形成函数时，修改参数类型的顶层限定符被删除。生成的参数类型以及省略号或函数包的存在与否即为 `parameter-type-list`。

> [注 3: 此转换不影响参数的类型。例如，`int*(const int type(p*)` 和 `int*(const int*)` 是相同类型。注结束]

91) 正如语法所示，`cv-qualifiers` 是函数返回类型中的重要组成部分。

# ISO/IEC 14882:2020(E)

6 带有 `cv-qualifier-seq` 或 `refqualifier`（包括由 `typedef-name` (`9.2.4`, `13.2`) 命名的类型）的函数类型应仅出现在以下位置：

- (6.1) 非静态成员函数的函数类型，
- (6.2) 成员指针所指向的函数类型，
- (6.3) `typedef` 声明或别名声明的顶层`top-level` 函数类型，
- (6.4) 类型参数 (`13.2`) 默认参数中的 `type-id`，或
- (6.5) 类型参数 (`13.4.2`) 模板参数的 `type-id`。

```

[Example 2:

typedef int FIC const;

FIC f;

struct S {

    // error: does not declare a member function

    FIC f;

    // OK

};

FIC S *p = &f; // OK

-- end example]

```

7 函数声明符中 `cv-qualifier-seq` 的效果与在函数类型上添加 `cv-qualification` 不同。在后者的情况下，`cv-qualifiers` 会被忽略。

> [Note 4: 带有 `cv-qualifier` 的函数类型不是 `cv-qualified` 类型；不存在 `cv-qualified` 的函数类型。
-- note]

```

[Example 3:

typedef void F();

struct S {

    const F f; // OK: equivalent to: void f();

};

-- end example]

```

8 返回类型、参数类型、`refqualifier`、`cv-qualifier-seq` 以及异常规格是函数类型的一部分，但不包括默认参数 (`9.3.4.7`) 或尾随 `requires-clause` (`9.3`)。

> [Note 5: 函数类型在函数指针、函数引用和成员指针的赋值和初始化期间会进行检查。
-- note]

9 如下声明

```

int freile(FILE*, long int);

declares three arguments 声明了三个指定类型的参数，并返回 `int` (`9.2.9`)。 -- end example

```

10 在单个作用域内，一个名称可以用于不同的函数；这就是函数重载（第 12 条）。一个函数的所有声明都具有等效的返回类型、参数类型和 `requires-types` (`13.7.7.2`)。

11 函数的返回类型不会是数组或函数，尽管它们的返回类型可以是此类项的指针或引用。不存在函数的数组，但可以存在函数指针的数组。

12 `volatile-qualified` 的返回类型已弃用：D.6。

13 不应在返回类型或参数类型中定义类型。

14 函数类型的 `typedef` 可用于声明函数，但不应用于定义函数 (`9.5`)。

```

[Example 5:

typedef void F();

F fv; // OK: equivalent to void fv();

F f() { // error

void f() { // OK: definition of fv

-- end example]

```

15 标识符可以作为参数名称；如果出现在函数定义 (`9.5`) 中，则它命名一个参数。

> [Note 6: 参数名在函数定义中也是可选的，且不同声明中的参数与函数定义中的参数名不需要相同。如果在非定义的函数声明中存在参数名，则它不能在它的函数声明之外使用，因为其潜在的作用域范围 (`6.4.4`)。 — end note]

[Example 6: 声明

```

int i;

*f();

*fpi(int);

*fpi(const char*, const char*);

(*fip)(int);

```

声明了一个指向函数 `f` 的 `int` 指针，`f` 不接受参数并返回一个整数；`*fpi(int)` 声明了一个返回 `int` 的函数 `fpi` 的 `int`指针；`*fpi(const char*, const char*)` 声明了一个接收两个 `const char*` 并返回 `int` 的函数 `fpi` 的 `int` 指；`(*fip)(int)` 声明了一个返回 `int` 的函数 `fip` 的 `int` 指针。 

*(注：原文后半部分似乎存在大量乱码或逻辑不通的重复字符，已根据上下文尝试维持语意翻译，并遵循格式要求。)*

# ISO/IEC 14882:2020(E)

参数包。如果它在参数声明中指定，则它不应出现在参数声明的限定符或抽象限定符中。⁵³

4 对于非模板函数，可以在同一作用域内函数的后继声明中添加默认参数。不同作用域内的声明具有完全不同的默认参数集。也就是说，内层作用域的声明不会从外层作用域获取（（此处）默认参数，反之亦然。在给定的函数声明中，每个紧跟在带有默认参数的参数之后的参数，都应该有一个在之前的声明中或从之前的声明中提供默认参数，或者应该是一个函数包。

[注 2: 默认参数不能通过随后的声明重新定义（即使值相同也不行）（6.3）。—— 结束

[示例 2:]

```cpp

void f(int = 0, ...); // 省号不是参数，因此可以跟在其后

void f(int, int); // 带有默认参数的参数

void f(int, int = 7);

void f() {

 f(2); // OK，调用 f(3, 7)

 void f(int = 1, int); // 错误：未源自周围作用域

}
