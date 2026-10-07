
> 87) 从 `switch` 语句条件跳转到 `case` 标签在这方面被视为一种跳转。

+ 4 带有 `void` 类型表达式的 `return` 语句只能用于返回类型为 `void` 的函数；该表达式在函数返回其调用者之前求值。

+ 5 从函数末尾流出等于无值的返回；这在返回值的函数会导致未定义行为。

## 6.8 歧义性 [stmt.ambig]

+ 1 表达式语句与声明之间存在歧义：带有类型转换（7.0）的表达式语句与以类型开头的声明是无法区分的。

# ISO/IEC 14882:2011(E)

## 7 声明 [dcl.dcl]

- 声明通常指定名称如何被解释。声明的形式为：`declaration-seq`: `declaration` `declaration-seq` `block-declaration` `function-definition` `template-declaration` `explicit-instantiation` `explicit-specialization` `linkage-specification` `namespace-definition` `empty-declaration` `attribute-declaration` `block-declaration`: `simple-declaration` `asm-definition` `namespace-alias-definition` `using-declaration` `using-directive` `static_assert-declaration` `alias-declaration` `opaque-enum-declaration` `alias-declaration`: `using` `identifier` `attribute-specifier-seq_opt` `=` `type` `id` `;` `simple-declaration`: `decl-specifier-seq_opt` `init-declarator-list_opt` `;` `attribute-specifier-seq` `decl-specifier-seq_opt` `init-declarator-list` `;` `static_assert-declaration`: `static_assert` `(` `constant-expression` `,` `string-literal` `)` `;` `empty-declaration`: `attribute-declaration`: `attribute-specifier-seq`

[注：`asm-definitions` 在 7.4 中描述，`linkage-specifications` 在 7.5 中描述。`function-definitions` 在 8.4 中描述，`template-declarations` 在第 14 节。`namespace-definitions` 在 7.3.1 中描述，`using-declarations` 在 7.3.3 中描述，`using-directives` 在 7.3.4 中描述。—— 注结束]

`simple-declaration` `attribute-specifier-seq_opt` `decl-specifier-seq_opt` `init-declarator-list_opt`; 被分为三部分。属性在 7.6 中描述。`decl-specifiers`（`decl-specifier-seq` 的主要部分）在 7.1 中描述。`declarators`（`init-declarator-list` 的组件）是在第 8 节中被声明的实体。`simple-declaration` 中的 `attribute-specifier-seq` 作用于 *init-declarator-list* 的每个 `declarator`。[注：在用于属性的声明中，属于该实体的属性可能出现在声明的开头以及该声明的 *declarator-id*。—— *节点结束* [示例]：

```cpp
[[noreturn]] void f ([[noreturn]]);
```
```cpp
// 示例结束
```

除非另有规定，*attribute-declaration* 的含义由实现定义。

- 2 声明发生在作用域内（3.3)；作用域规则在 3.4 中是明确的。声明函数或定义类、命名空间、模板或函数的声明具有一个或多个嵌套的作用域。这些嵌套作用域又在其内部嵌套了声明。除非另有说明，第 7 节中关于声明内或由声明或子组件包含的引用仅指声明中未嵌套在相同作用域内的那些元素。

- 在 `simple-declaration` 中，只有在声明类（第 9 节）或枚举（7.2）时，才能省略可选的 *init-declarator-list*；也就是说，当 `decl-specifier` 包含 `class-specifier`、带有类键（9.1）的详细类型（`elaborated-type`）或 `enum-specifier` 时。在这些情况下，当存在 `class-specifier` 或 `enum-specifier` 时，这些修饰符中的标识符是声明赋予的名称（类名、枚举名或枚举常量）。在这些情况下，以及对于未命名位域字段（9.6）的声明，*decl-specifier-seq* 可能会程序中引入一个或多个名称，或对之前的声明重新声明一个名称。[示例]：

```cpp
enum {
typedef class {}; // 格式错误
};
```
```cpp
// 示例结束
```

- 4 在 `static-declaration` 中，`declarator-expression` 是一个常量表达式（5.19），在概念上可以转换为 `bool`（第 4 节）。如果表达式转换后的值为 `true`，则该声明不起作用。否则，程序是格式错误的，且生成的诊断信息（1.4）应包含 *string-literal* 的文本，但基本源字符集（2.3）中的字符不需要出现在声明中。[示例]：

```cpp
static_assert(sizeof(long) >= 8, "64-bit code generation required for this library.");
```
```cpp
// 示例结束
```

- 6 *init-declarator-list* 中的每个-`declarator` 包含包含一个 `declarator`，该 `declarator` 是该-`declarator` 赋予的名称以及声明赋予的名称之一。`decl-specifier-seq` 中的 *type-specifiers*（7.1.6）和 *init-declarator* 的递归 `declarator` 结构描述了一个类型（8.3），该类型与 *init-declarator* 赋予的名称相关

- 7 如果 *decl-specifier* 包含 *typedef* 关键字，则该声明被称为 *type-declaration*，每个 *init-declarator* 的名称被声明为 *type-name*，并与其类型相关（7.1.3）。如果 `decl-specifier` 不包含 *typedef*，如果与名称相关的类型是函数（8.3.5），则该声明被称为函数声明，或对象声明

- 8 在声明通用形式之外的语法组件被添加到函数声明中，以形成一个 *function-definition*。然而，对象声明除非它包含 *extern* 修饰符且没有初始化器（3.1），否则也是一种定义。定义会导致保留相应数量的存储并完成任何 *初始化*（8.5）。

- 9 只有在构造函数、析构函数和类型转换的函数声明中，才能省略 `decl-specifier-seq`。

## 7.1 修饰符 [dcl.spec]

- 1 可以在声明中使用的存储类修饰符：

| decl-specifier |
| :--- |
| storage-class-specifier |
| type-specifier |
| function-specifier |
| friend |
| typedef |

| decl-specifier-seq |
| :--- |
| decl-specifier |
| attribute-specifier-seq |

`decl-specifier-seq` 中可选的 `attribute-specifier-seq` 作用于由前面的修饰符（8.3）确定的类型。`attribute-specifier-seq` 仅影响它所在声明的类型，而不影响具有相同类型的其他声明。

- 2 如果在解析 `decl-specifier-seq` 时遇到 `type-name`，如果除 `const` 或 `volatile` 之外没有之前的 `type-specifier`，则它被解释为 `decl-specifier-seq` 的一部分。该序列将按如下所述保持自恰。[示例]：

```cpp
typedef char* Pc;
static; // 错误：缺少名称
```

在这里，声明 `static` 是格式错误的，因为没有为 `static` 变量指定名称。为了获得一个变量，`decl-specifier` 必须包含 `const` 或 `volatile` 以外的类型修饰符。例如：

```cpp
void f(const Pc*);
void g(int)
```

- 3 在解析 `decl-specifier-seq` 时遇到 `type-name`，如果除 `const` 或 `volatile` 之外没有之前的 `type-specifier`，则它被解释为 `decl-specifier-seq` 的一部分。该序列将按如下所述保持自恰。[注：对于 `signed`, `unsigned`, `long` 和 `short` 修饰符，默认情况下 `type-name` 是被声明的名称。示例]：

```cpp
void h(unsigned Pc);
void k(unsigned int)
```
—— 注结束]

## 7.1.1 存储类修饰符 [dcl.stc]

- 1 存储类修饰符包括：

| storage-class-specifier |
| :--- |
| register |
| static |
| thread_local |
| extern |
| mutable |

C 的“隐式”规则不再支持。在给 `decl-specifier-seq` 中最多出现一个 `storage-class-specifier`，`thread_local` 可以与 `static` 或 `extern` 出现。如果它出现在变量的声明中，则必须存在。在 `decl-specifier-seq` 中出现 `storage-class-specifier`，除非是匿名 `declarator`（9.5）或在全局命名空间中，否则被声明为 `static`。`storage-class-specifier` 作用于声明的每个 `init-declarator`，而不作用于声明的任何名称。

- 2 `register` 修饰符仅应用于块（6.3）中声明的变量名称或函数参数（8.4）。它指定该名称具有自动存储期（3.7.3）。块或作为函数参数没有 `storage-class-specifier` 的变量默认具有自动存储期。

- 3 `register` 类是对实现的提示，变量将被频繁。[注：该提示可以被忽略，在大多数实现中，如果获取了变量的地址，它将被忽略。]

- 4 `thread_local` 修饰符指示命名的实体具有存储期（3.7.2）。它仅应用于命名空间或块的变量名称，或静态成员的名称。当 `thread_local` 应用块变量时，如果没有出现 `storage-class-specifier`，则隐含 `static`。

- 5 `static` 修饰符只能应用于变量名称和匿名联合（9.5）。块内不能有静态函数声明，任何静态函数都没有存储期（3.7.1）。用于变量声明的 `static` 修饰符声明该变量具有静态存储期（3.7.2）。用于类成员声明的 `static` 修饰符；9.4 描述其影响。对于类成员的声明变量。

- 6 `extern` 修饰符只能应用于变量和函数的名称。[注：**extern** 关键字也可以用于显式实例化和链接修饰符，但在这些上下文中它不是存储类修饰符。] —— 注结束

- 7 命名空间作用域内带有 `storage-class-specifier` 的名称具有外部链接，除非它由于之前的声明具有内部链接且未声明为 `const`。未显式声明 **extern** 的对象具有内部链接。

- 8 连续声明暗示的链接应保持一致。也就是说，在给定的作用域内，使用相同变量名称或相同重载函数名的每个声明都暗示相同的链接。然而，一组重载函数中的每个函数可以具有不同的链接。

# ISO/IEC 14882:2011(E)

```cpp
void l0(); // external linkage
inline void m(); // external linkage
extern void m();
static void n(); // internal linkage
inline void n();
static int a; // a has internal definitions
int a; // error: two definitions
static int b; // b has internal linkage
extern int b; // b still has internal linkage
int c; // c has external linkage
static int c; // error: inconsistent linkage
extern int d; // d has external linkage
static int d; // error: inconsistent linkage
```
// - 示例结束

9 已声明但未定义的类名可以在 *extern* 声明中使用。此类声明只能在不需要完整类类型的方式中使用。[示例：]

```cpp
struct S;
extern S s;
extern S f();
extern void g(S);
void h() {
g(a); // error: S is incomplete
f();  // error: S is incomplete
}
```
// - 示例结束

10 `mutable` 限定符只能应用于类成员名 (9.2)，不能应用于声明为 *const* 或 *static* 的名，也不能应用于引用成员名。[示例]：

```cpp
class X {
mutable const* p; // OK
mutable int* const q; // ill-formed
}
```
// - 示例结束

11 类成员上的 `mutable` 限定符会使应用于它的 *const* 限定符失效，并允许即使对象的其他部分是 *const* 时修改该 `mutable` 类成员 (7.1.6.1)。

# 7.1.2 函数指定符 [dcl.fct.spec]

- 1 函数指定符只能用于函数声明。

- 函数指定符：
`inline`
`virtual`
`explicit`

§ 7.1.2

2 带有 `inline` 指定符的函数声明 (8.5, 9.3, 11.3) 声明一个内联函数。`inline` 标识符指示实现，在调用点处对函数进行内联替换优于通常的函数调用机制。实现并不被要求在调用点处执行这种内联替换；然而，即使省略了内联替换，仍应遵守 7.1.2 定义的内联函数的其他规则。

3 在类定义内部定义的函数是内联函数。`inline` 指定符不应出现在块范围声明中。如果 `inline` 指定符用于 `friend` 声明中，除非该函数之前已经声明，否则该声明将被省略。

4 内联函数应在其被 `odr-used` 的每个翻译单元中定义，并应具有 [注意：该内联函数可能在其定义出现在翻译单元中之前被遇到。 — 注意] 如果函数的定义出现在翻译单元中且先于其首次声明，则它是格式不正确的。如果在一个翻译单元中声明了具有外部链接的函数，则它应该在其出现的所有翻译单元中进行声明；不需要诊断信息。具有外部链接的内联函数在所有翻译单元中具有相同的地址，并引用同一个对象。`extern inline` 函数体中的字符串字面量在不同的翻译单元中是同一个对象。[注意：出现在默认参数中的字符串字面量不在内联函数体中，因为该表达式是在从该函数发起的函数调用中使用的。 — 注意] 在 `extern inline` 内联函数体内部定义的类型在每个翻译单元中都是相同类型。

5 `virtual` 指定符只能用于非静态类成员成员函数的初始声明；参见 10.3。

6 `explicit` 指定符只能用于在其类定义内对构造函数或转换函数的声明；12.3.1 和 12.3.2。

### 7.1.3 类型指定符

- 1 包含 `decl-typespecifier` 的声明声明了可用于后续命名基础 (3.9.1) 或复合 (3.9.2) 类型的标识符。类型指定符应在 `declifier-seq` 中与类型指定符以外的任何类型的指定符组合，且不应在参数声明 (8.3.5) 的 `decl-specifier-seq` 中或函数定义 (8.4) 的 `declifier-seq` 中。

```cpp
typedef-name:
identifier
```

用类型指定符声明的名称成为 `typedef-name`。在其声明的作用范围内，`typedef-name` 在语法上等同于关键字以及与标识符相关的类型。`typedef-name` 不会像类声明 (9.1) 或枚举声明那样引入新类型。[示例：在 

```cpp
typedef int distance, metric;
const distance;
extern metric;
```

都是正确的声明；`distance` 的类型是 int，`metric` 的类型是“指向 int 的指针。”]

- 2 `typedef-name` 也可以通过别声明引入。`using` 关键字后面的标识符成为 `typedef-name`，其语义与通过 `typedef` 指定符引入相同。特别地，它没有定义新类型，且不应出现在 `type-id` 中。[示例：]

```cpp
using handler_t = void (*);
extern handler_t; // redeclare int
```
