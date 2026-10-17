
### 5.1.4.4 嵌套要求 [expr.prim.req.nested]

```
nested-requirement:
  requires;
```

`nested-requirement` 可以用于根据局部参数指定额外的约束。它向 `requires-expression` 定义的约束合取中附加一个约束。[示例：

```cpp
template<typename T>
concept C = requires(T x) {
    requires sizeof(x) > 0;
};
```

N4549

表 10 — 简单类型限定符及其指定的类型

| 限制符 (Specifier(s)) | 类型 (Type) |
|---|---|
| `type-name` | 被命名的类型 |
| `simple-template-id` | 14.3 中定义的类型 |
| `end-type` | : |
| `auto` | 待推导类型的占位符 |
| `dectype(expression)` | 下文定义的类型 |
| `constrained-type-specifier` | 待推导的值（类型、非类型、模板）的占位符 |

将第 1 段替换为以下文本：

+   1 类型限定符 `auto`、`dectype(auto)` 和 `constrained-type-specifiers` 指定一个占位符（类型、非类型或模板），该占位符将通过推导或显式指定进行替换。`auto` 和 `dectype(auto)` 类型指定值和模板的占位符。[注：占位符的推导是通过 7.1.6.4 和 8.3.5 中描述的引入模板参数实现的——结束]占位符用于表示泛型 lambda (5.1.2)、函数是一个简写函数模板 (8.3.5)，或复合需求 (5.1.4) 中的尾随返回类型引入了参数推导约束 (14.10.1.6)。注：嵌套限定符也可以包含占位符 (5.1)。`constrained-type-specifiers` 的替换根据本节中的规则确定。[结束注]]

+   2 占位符类型类型可以出现在声明此类占位符的任何上下文中，位于 `decl-specifier-seq`、`type-specifier-seq`、`conversion-function-id` 或 `trailing-return-type` 中的函数声明符。如果函数声明符包含尾随返回类型 (8.3.5)，则将该占位符指定为声明的返回类型。如果函数的声明返回类型包含占位符，则函数的返回类型从函数体推导出来。在包含占位符的来自 `auto D -> T` 的返回语句的函数中，初始 `auto` 不指定占位符。

+   3 修改第 3 段，允许在 lambda 或函数的参数类型中使用 `auto`。

如果 `auto-type-specifier` 占位符作为参数声明的 `decl-specifier-seq` 之一出现在 lambda 的参数类型中，则该 lambda 是一个泛型 lambda (5.1.2)。[示例：

```
auto lambda = (int, auto) { return int; }; // OK：一个泛型 lambda
```

— 示例结束]同样，如果占位符出现在函数声明的参数类型中，则该函数声明声明了一个简写函数模板 (8.3.5)。[示例：

```
void f(const auto, int); // OK：一个简写函数模板
```

— 示例结束]

在第 3 段之后添加以下内容以描述返回类型中的 `constrained-type-specifiers` 指向模板参数。

7.1.6.4

如果一个简写函数声明的声明返回类型引入的约束表达式 (7.1.6.2) 根据 14.6.6.1 中的表达式比较规则被认为与该函数参数声明句中 `constrained-type-specifier C2` 引入的约束表达式等价，则带有占位符的 `constrained-type-specifier C1`。相反，`C1` 被替换为为 `C2` 创建的模板参数 (8.3.5)。示例：

```
template<typename T> const bool C = true;

template Struct T;

const& f1(C); // 相同的模板参数且没有推导返回类型
Tuple<...> f2(C); // 相同的模板参数且没有推导返回类型
```

在声明 `f1` 中，参数声明句和返回类型中的 `constrained-type-specifiers` 引入的约束表达式是等价的；它们都会为某个引入的模板参数 `T` 引入表达式 `C`。在 `f2` 中，在返回类型中使用 `C` 将引入一个约束表达式 (`C`)，它与参数声明句中 `constrained-type-specifier C` 对应的引入的模板参数 (14.1) 是不同的。

(1.2) 否则；将变量或返回类型中的每个占位符替换为新发明的模板参数，具体根据 8.3.5 中为占位符发明模板参数的规则。

根据函数调用 (14.8.2.1) 的模板推导规则，为 `P` 中的每个发明的模板参数推导出一个值，其中 `P` 是函数模板参数类型，且初始化器是对应的参数。如果推导失败，则该声明是非法的（ill-formed）。如果受约束类型限定符（`constrained-type-specifier`）引入了任何占位符，则按如下定义 `C` 为约束表达式：

- (1.3) 如果只有一个受约束类型，则 `C` 是发明的模板约束参数 (14.1) 为该受约束类型限定符引入的约束表达式；

- (1.4) 否则，`C` 是逻辑与 (5.4)，它按照出现顺序作用于每个受约束类型限定符对应的发明的模板约束参数所引入的约束表达式。

如果声明类型的推导值未满足 `U` 的归一化字符，则该声明是非法的。否则，通过将推导出的 `U` 替换 `P` 中的每个发明的模板参数，得到变量或返回类型的类型。

示例：

```
auto x1 = {1, 2}; // OK: decltype(x1) 是 std::initializer_list<int>
auto x2 = {1, 2, }; // error:无法推导元素类型

// end example
```

在 C++ 标准第 7 段的第一个示例中添加以下内容。

示例：

```
template<typename T> struct Vec { };
template<typename T> Vec<T> make_vec(std::initializer_list<T> l) { return Vec<T>{l}; }
template<typename...> Tuple<...> make_up(Ts... args) { return Tuple<Ts...>{args}; }

auto x3 = *x1.begin(); // OK: decltype(x3) 是 int&
const Vec<auto> v1 = make_vec({1, 2, 3}); // OK: decltype(v1) 是 Vec<int>
Vec<auto> v2 = {1, 2, 3}; // error: 类型推导失败
Tuple<...> v3 = make_up(0, 'a'); // OK: decltype(v3) 是 Tuple<int, char>

// end example
```

在 C++ 标准第 7 段的第二个示例中添加以下内容。

示例：

```
template<typename T, typename U> struct Pair;
template<typename T, typename U> Pair<T, U> make_pair(T, U);

struct S { void mfn(bool); };
int fn(char, double);

Pair<(*)(auto, auto, auto), auto(*S::*)(auto)> p = make_pair(fn, &S::mfn);
```

7.1.6.4.1

N4549

`p` 的声明类型是以下发明的函数模板中类 `g(make_pair(fn, &S::mfn))` 的参数 `x` 的推导类型：

```
template<class T1, class T2, class T3, class T4, class T5, class T6>
void g(Pair<T1>(*T2), T3, (T5::*)(T6)) x);
```

— 示例

[示例]:

```
template<typename T> concept bool C = true;

const C* cv = expr;
```

`cv` 的类型是从以下发明的函数 `f1(expr)` 类中的参数 `p1` 推导出的：

```
template<T> void f1(const T* p1);
```

— 示例

[示例]:

```
auto cf(int) -> Pair<C, C> { return expr; }
```

`cf` 的返回类型是从以下发明的函数 `f2(expr)` 类中的参数 `p2` 推导出的：

```
template<T> void f2(Pair<T, T>);
```

`cf` 返回类型中的两个受约束类型限定符对应于同一个发明的模板参数。 — 示例

将 C++ 标准中 7.1.6.4 的第 8-15 段复制到本节。修改第 8 段（此处为 2）如下：

- 8 如果初始化-声明符-列表包含多于一个初始化-声明符，则它们都应形成变量声明。每个声明变量的类型按上述方式确定，如果替换占位符类型的声明变量类型或返回类型在每次推导中不相同，则程序是非法的。

在段落中添加以下示例：

[示例]:

```
Pair<auto, auto> p1 = make_pair(0, 0);
*p2 = &p1; //替换类型为 Pair<int, int>
Pair<auto, auto> p3 = make_pair(0, 'a');
p4 = make_pair('a', 0); // error: 不同的替换类型 s
```

— 示例

修改第 9 段（此处为 3）。

- 9 如果一个声明返回类型中包含占位符类型的函数有多个返回语句，则为每个返回语句推导返回类型。如果每次推导的类型不相同，则程序是非法的。

修改第 10 段（此处为 4）。

7.1.6.4.1

N4549

如果一个声明返回类型使用占位符的函数没有返回语句，则返回类型是从函数体大括号处的返回语句推导而出的。

修改第 11 段（此处为 5）。

如果需要推导带有占位符实体的类型，则该做法是非法的。

修改第 13 段（此处为 7）。

声明返回类型使用占位符的函数或函数模板的也使用该占位符。如果受约束类型限定符指定了占位符，则在段落中添加以下内容：

```
template<typename> concept C = true;
template<typename> concept C2 = true;

template<typename> auto cf(T) -> C; // #1
template<typename> cf(T); // #2: 重复声明 #1
template<typename> C2(T); // error: 使用了占位符声明
```

修改第 14 段（此处为 8）。

使用占位符作为返回类型的声明函数不应有异常说明。

修改第 15 段（段 8）如下：

显式实例化 (14.8.2) 不导致使用占位符实体的实例化，但也不会阻止该实体以确定其类型。

# 7.1.6.4.2 受约束类型限定符 [dcl.spec.auto]

将此添加到 7.1.6.4。

- 受约束类型限定符指定一个占位符（类型、类型或模板）并引入关联约束 (14.10.2)。

- 受约束类型限定符：

  限定限定的的名称：

    限定限定的限定名称：

      嵌套名称限定符-opt 受约束类型名称

    概念名称：

      部分概念标识符

    概念名称：

      部分概念标识符：

        概念名称 <template-argument-list> 

§ 7.1.6.4.2

N4549

```
template<typename T> concept C1 = false;
template<int N> concept C2 = false;
template<typename X> concept C3 = false;

template<T, int N> class Array { };
template<T, typename> class Stack { };
template<T> class Alloc { };

void f1(C1); // C1 指定占位符类型
void f2(Array<auto, C2>); // C2 指定整数值的占位符
void f3(Stack<auto, C3>); // C3 指定类模板的占位符

-- end example
```

如果标识符指向一组定义集 (7.1.7)，则它是一个概念名称。[注：当概念名称指向变量概念时，概念集合最多有一个这样的成员。 — 注释] [示例]:

```
template<typename T> concept C() { return true; }; // #1
template<T, typename> concept B() { return true; }; // #2
template<T, typename> concept D = true; // #3

void f(C()); // OK: C 所指的概念包含了 #1 和 #2;
void g(D); // OK: 概念名称 D 仅指向 #3

-- example
```

部分概念标识符是一个概念后跟模板参数。[示例]:

```
template<T, int N = D> concept Seq = true;

void f1(Seq<3>); // OK
void f2(Seq<>); // OK

-- end
```

由受约束类型限定符指定的概念是根据 14.10.4 中的概念解析规则选择的那个。

注：受约束名称引入的约束表达式是通过发明受约束名称引入的 (14.10.1)。为变量类型或函数声明类型发明对应模板参数的规则在 7.1.4.1 中描述。为 lambda 表达式 (5.1.2) 的参数声明句或函数声明 (8.3.5) 中的占位符发明模板参数的规则在 8.3.5 中描述。为复合要求的尾随类型中的占位符发明模板参数的规则在 14.10.1 中描述。 — 注释]

# 7.1.7 概念分类器 [dec:Spec.concept]

将此节添加到 7.1.1。

概念限定符应仅应用于函数模板或变量模板的定义，这些定义在命名空间 (3.6) 中。具有概念分类器的函数模板定义称为函数概念。函数概念不应异常说明，并被处理为指定了 `noexcept(true)` (15.4)。当声明函数时

§ 7.1.7

N4549

作为一个概念，它将是该函数的唯一声明。具有概念限定符的变量定义被称为变量概念（variable concept）。概念定义指的是函数概念及其定义，或者变量概念及其初始化器。[示例：

```cpp
template<typename T>
    concept F1() { return true; } // OK 声明了一个概念
template<typename T>
    concept bool F2(); // error: 概念不是一个定义
template<typename T>
    constexpr bool F3()
template<typename T>
    concept bool F3() { return true; } // error: 将函数重重声明为概念
    concept bool V1 = true; // OK 声明了一个变量
template<typename T>
    concept bool V2; // error: 没有初始化值的变量概念
struct S {
    template<typename T>
    static bool C = true; // error: 在类作用域内声明概念
}
```

-- 示例结束

每个概念都隐式定义为 `constexpr` (7.1.5)。概念定义不应使用 `thread_local`、`inline`、`friend` 或 `constexpr` 限定符声明，且概念定义不具有关联约束 (14.10.2)。

函数概念的定义或变量概念的初始化器不应包含对被声明概念引用。[示例：

```cpp
template<typename T>
    concept bool F() { F<typename>::type(); } // error
template<typename T>
    concept bool W = V<T>; // error
```

-- 示例结束

函数概念具有以下限制：

- (5.1) 其声明中不应出现任何函数限定符 (7.1.2)。

- (5.2) 声明的类型应具有类型体。

- (5.3) 声明的参数列表应等同于空参数列表。

- (5.4) 声明应有一个等同于 `{ return E; }` 的函数体，其中 `E` 是一个约束表达式 (14.10.13)，

[注：返回类型推导需要函数定义的实例化，但概念定义不会被实例化；它们是被归一化的 (14.10.2)。-- 注结束] [示例：

```cpp
template<typename T>
    concept int F0() { return 0; } // error: 返回类型不是 bool
template<typename T>
    concept auto F1() { return true; } // error: 返回类型被推导了
template<typename T>
    concept bool F3(T) { return true; } // error: 不是空参数列表
```

§ 7.1.7

19

示例结束

6 变量概念具有以下限制：

- (6.1) 声明的类型应为 `bool`。

- (6.2) 声明应具有一个初始化器。
