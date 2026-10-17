
- 任何命名空间作用域的友函数或函数模板（`11.9.4`）如果在关联实体集中具有可达定义的类中声明，它们在各自的命名空间内是可见的，即使通过普通查找（`9.8.2.3`）不可见。

§ `6.5.3`

© ISO/IEC 2020 – 保留所有权利

在命名模块 `M` (`10.2`) 范围内声明的任何导出 `D` 在此处是可见的，如果 `M` 附加了一个关联实体，该实体具有相同的最内层非内联命名空间 `D`。

如果查找的是依赖名（`13.8.3`, `13.8.5.2`），则 `N` 中的任何声明 `D` 是可见的，如果 `D` 在查找的实例化上下文（`10.6`）的任何点对于限定查找（`6.5.4.3`）是可见的，除非 `D` 声明在另一个编译单元中，附加到全局模块，并且属于以下情况

[示例 3:

```cpp
编译单元 #1:
export module M;
namespace R {
    export struct X {};
    export void f(X);
}
namespace S {
    export void f(R::X, R::X);
}
```

```cpp
编译单元 #2:
export module N;
import M;
export R::X make();
namespace R {
    export template<typename T, typename U> void apply(T t, U u) {
        f(t, u);
        g(t);
    }
}
```

```cpp
module Q;
import N;
namespace S {
    struct Z {template<typename T> operator T();
    Z() {
        auto x = make(); // OK, decltype(x) 在 module M 中是 R::X
        // 错误：R 和 R::f 在此处可见
        R::f(x);\ // OK, 调用 M 接口中的 R::f
        f(x);\ // 错误：未考虑 module M 中的 S::f
        // 尽管 S 是关联命名空间
        // 错误：S::f 在实例化上下文中可见
        // 错误：R::f 具有内部链接，无法在 TU #2 外部使用
    }
}
apply(x, S::Z());
```

示例结束

### 6.5.4 限定名查找

[basic.lookup.qual]

#### 6.5.4.1 通用

类、命名空间或枚举值的名称可以通过 `::` 解析运算符（`7.5.4.3`）应用于表示其类、命名空间或枚举的嵌套指定符来引用。如果嵌套名称指定符中的 `::` 解析运算符前面没有 `decltype`-指定符，则对该名称的查找仅考虑其特化为类型的命名空间、类型和模板。如果该名称未指定类、命名空间或依赖类型，则程序是格式错误的。

[示例 1:

```cpp
class A {
public:
    static int n;
};
```

```cpp
int main() {
int A;
A::n = 42; // OK
错误：A 不是类型
```

[注意 1：重限定名称，如 `N1::B2::N3`，可以引用成员。]

示例 2:

```cpp
class X {
class C {
static int number = 50;
static X arr;
};
X::number; // 等于 C::number
```

示例结束

示例 3:

```cpp
struct C {
int I1;
int I2;
};
C::I1; // OK
C::I2; // OK
```

示例结束

```cpp
struct A {
  A();
};
struct B : public A { B(); };

A();
```

```cpp
namespace Y {
void f(float);
void h(int);
}

namespace Z {
void h(double);
}

namespace A {
using namespace Y;
void f(int);
void g(int);
int i;
}

namespace B {
using namespace Z;
void f(char);
int i;
}

namespace AB {
using namespace A;
using namespace B;
void g(int);
}

void h() {
// g 直接声明在 AB 中，因此 S 是 {AB::g()} 且选了 AB::g()
AB::g();();
// f 没有直接声明在 AB 中，因此规则递归地应用于 A 和 B；
// 不会搜索命名空间 Y，Y::f(float) 不被考虑；
// S 是 {A::f(int), B::f(char)} 且重载解析选择了 A::f(int)
AB::f('c');
// 如上所述，解析选择了 B::f(char)
AB::x++;
// x 没有直接声明在 AB 中，也没有在 A 或 B 中声明，因此规则
// 递归应用于 Y 和 Z，S 为 {} 所以程序格式不正确
AB::i++;
// i 没有直接声明在 AB 中，因此规则递归地应用于 A 和 B；
// S 是 {A::i, B::i} 所以该使用是歧义的，程序格式不正确
AB::h(16.8);
// h 没有直接声明在 AB 中，也没有在 A 或 B 中声明，因此规则
// 递归应用于 Y 和 Z，S 是 {Y::h(int), Z::h(double)} 且
// 重载解析选择了 Z::h(double)
```

结束示例

注 1：多次发现的相同声明不是歧义（因为它们仍然是一个唯一的声明）。

示例 2：

```cpp
namespace A {
int a;
}

namespace B {
using namespace A;
}

namespace C {
using namespace A;
}
```

### 6.5.4.3

```cpp
namespace BC {
    using namespace B;
    using namespace C;
}
```

```cpp
void f() {
    BC::a++; // OK: S 是 {A::a, A::a}
}
```

```cpp
namespace D {
    using A::;
}
```

```cpp
namespace BD {
    using namespace B;
    using namespace D;
}
```

```cpp
void g() {
    BD::a++; // OK: S 是 {A::a, A::a}
}
```

- 结束示例

- 结束注

- 5 [示例 3：由于每个引用的命名空间最多被搜索一次，以下是有定义的：

```cpp
namespace B {
    int b;
}
namespace A {
    using namespace B;
    int a;
}
namespace B {
    using namespace A;
}
void f() {
    A::a++; // OK: a 直接声明在 A 中，S 是 {A::a}
    B::a++; // OK: A 和 B 都被搜索（一次），S 是 {A::a}
    A::b++; // OK: A 和 B 都被搜索（一次），S 是 {B::b}
    B::b++; // OK: b 直接声明在 B 中，S 是 {B::b}
}
```

结束示例]

- 6 在查找限定成员名时，如果查找找到了该成员的一个声明，且如果一个声明引入了类名或枚举名，而其他声明引入了相同的变量、相同的枚举器成员或一组函数，则非类型隐藏该类名或枚举名，当当且仅当这些声明来自同一个命名空间时；否则（如果声明来自不同的命名空间），程序格式不正确。

[示例 4：

```cpp
namespace A {
    struct x { };
    int x;
    int y;
}
```

```cpp
namespace B {
  struct y { };
}
```

```cpp
namespace C {
  using namespace A;
  using namespace B;
  int i = C::x; // OK, A::x（类型为 int）
  int j = C::y; // 歧义，A::y 或 B::y
}
```

- 在命名空间成员声明中，如果声明符-id 是限定 id，给定该命名空间的限定 id 形式为

- 嵌套-名称-指定符 未限定-id

该未限定-id 应命名由嵌套-名称-指定符指定的命名空间的成员，或该命名空间的内联命名空间集合（`9.8.2`）的元素。

[示例 5：

```cpp
namespace A {
  namespace B {
    void f1(int);
  }
  using namespace B;
}
void A::f1() {} // 错误：f1 不是 A 的成员
```

- 结束示例

然而，在此类命名空间声明中，嵌套-名称-指定符可以依赖使用指令来隐式提供嵌套-名称-指定符的初始部分。

[示例 6：

```cpp
namespace A {
  namespace B {
    void f1(int);
  }
}
namespace C {
  namespace D {
    void f1(int);
  }
}
using namespace A;
using namespace C::D;
void B::f1(int) {} // OK，定义了 B::f1(int)
```

- 结束示例

### 6.5.5 详述类型符（Elaborated type specifiers）

详述类型符（`9.2.4`）可能用于引用之前定义的类名或枚举名，尽管该名被非类型隐藏（`6.4.10`）。如果详述类型符没有指定符，除非详述类型符出现在以下形式的声明中：

类-键 属性-符 标识符

根据 `6.3.5` 查找标识符，忽略任何非类型名。如果详述类型符由类-键引入且该查找没有找到之前定义的类型，则详述类型符格式不正确。如果详述类型符出现在：

类-键 属性-符 标识符;

详述类型符是根据 `6.4.2` 引入的类名。

如果详述类型符具有指定符，则按照 `6.5.4` 执行限定名查找，忽略任何非类型名。如果名称未找到之前定义的类型，则详述类型符格式不正确。

4 [示例 1：

```cpp
struct Node {
    struct Node*; // OK：引用注入类名
    struct Data*; // OK：在全局作用域声明 Data
};
    struct Node*; // OK：引用全局作用域的 Node
    friend struct Glob; // 错误：无法引入限定类型（9.2.4）
    struct Base::Data; // 错误：无法引入限定类型（9.2.4）
```

```cpp
 Data {
    struct Node*; // OK：引用全局作用域的 Node
    friend struct Glob; // 错误：Glob 未声明，无法引入限定类型（9.2.4）
    friend struct Glob; // OK：引用全局作用域（尚未声明的）Glob
    /* ... */
};
```

```cpp
structcpp
struct Base {
    struct Data; // OK：声明 Data
    struct Base::Data; // OK：全局 Data 是 friend
``````

# 6.5.6 类成员访问 [basic.lookup.classref]

1 在跟随 `x` (`7.6.1`) 的类成员访问中，如果 `->` 标记紧跟一个标识符后跟一个 `<`，则确定它是参数列表（`13.3`）的开始还是小于运算符。标识符首先在对象的作用域（`11.8`）中查找。如果未找到标识符，则在整个后缀表达式的作用域中查找，并应命名为一个具有特化版本的模板。

2 如果类成员访问 (`7.6.5`) 中的 id-expression 是未限定 id，且对象的类型是类 `C`，则在类 `C` 的作用域（`11.8`）中查找未限定 id。

3 如果未限定 id 是 `~类型名`，则在整个后缀表达式的上下文中查找类型名。如果对象的 `T` 是类 `C`，则在类 `C` 的作用域中也查找类型名。至少其中一次查找会找到一个引用 `C` 的名称。

[示例 1：

```cpp
struct A { };

struct B {
    struct A {};
    void (::* a);

    void B::(::* a) {\ OK：在 *a 中查找找到了注入类名
    a->A();
    }; // 结束示例
```

4 如果类成员访问中的 id-expression 是形式如下的限定 id：

ISO/IEC 14882:2020(E)

类名-或命名空间名:::

紧随 `.` 或 `~` 运算符后的类名-或命名空间名在对象的作用域（`11.8`）中作为名称查找（如果找到）。否则，在整个后缀表达式的上下文中查找。

> [注 1：参见 `6.5.4`，它描述了 `::` 之前的名称查找，这只会找到类型或命名空间名。]

5 如果限定 id 形式为

`::类名-或命名空间名::...`

类名-或命名空间名在全局作用域中作为类名或命名空间查找。

6 如果嵌套-名称-指定符包含简单模板 id [`13.3`]，其模板参数中的名称在整个后缀表达式的上下文中查找。

7 如果 id-expression 是转换 id，则其转换类型 id 首先在对象的作用域（`11.8`）中作为名称查找（如果找到）。否则，在整个后缀表达式的上下文中查找。在这些查找中，只考虑表示类型或模板的名称。

示例 2：

```cpp
struct A {
namespace N {
    struct A {
        void g() {
            template <class T> operator T();
        }
    }
}
int main() {
N::a,
a.operator();
}
```

结束示例

# ISO/IEC 14882:2020(E)

(`3.2.2`) — 它是内联的或导出的，或者

(`3.2.3`) — 它之前已经声明过，且之前的声明没有具有内部链接；或者

(`3.3`) — 匿名联合体的数据成员。

> [注意 1：具有 `const` 限定类型的实例化变量模板可以具有外部链接或内部链接，前提是未被声明为 `extern`。—结束注释]

4 无命名命名空间或直接或在匿名命名空间内声明的命名空间具有内部链接。所有其他命名空间均具有外部链接。命名空间作用域未被赋予内部链接，且该名称是：

(4.1) — 一个变量；

(4.2) — 一个函数；或

(4.3) — 一个具名的类 (`11.1`)，或者在 `typedef` 声明中定义的匿名类，其中该类为了链接目的具有 `typedef` 名称 (`9.2.4`)；或者

(4.4) — 一个具名的枚举 (`9.7.1`)，或者在 `typedef` 声明中定义的匿名枚举，其中该枚举为了链接目的具有 `typedef` 名称 (`9.2.4`)；或者

(4.5) — 一个以枚举器作为链接目的名称的匿名枚举 (`9.7.1`)；或

(4.6) — 一个模板

其定义的链接方式为：

(4.7) — 如果外层层命名空间具有内部链接，则该名称具有内部链接；

(4.8) — 否则，如果该名称的声明附加到一个具名的模块 (`10.1`) 且未被导出 (`10.2`)，则该名称具有模块链接

(4.9) — 否则，该名称具有外部链接。

5 除成员、函数、数据成员、具名的类或类类型的枚举，或在 `typedef` 声明中定义的匿名类或匿名枚举（其中该类或枚举为了链接目的具有 `typedef` 名称 (`9.2.4`)）外，它们与其作为成员的类名称具有相同的链接（如果有的话）。

6 在块作用域内声明的函数名称和通过块声明声明的变量名称具有外部链接。如果声明附加到一个具名的模块，则程序是非良法的（ill-formed）。如果存在具有链接的实体的可见声明（忽略在最内层命名空间作用域外声明的实体），如果这两个声明出现在同一个声明区域内，该块作用域声明将成为（可能是不良法的）重定义，该块声明声明的同一实体接收前一个声明的链接。如果存在多个此类实体，则程序是非良法的；如果未找到匹配的实体，则块作用域接收外部链接。在一个编译单元内，如果同一实体同时具有内部链接和外部链接，则它是非良法的。

示例 1:

```
static void f();
extern "C" void h(); // #1
static int i = 0;
void g() {
    extern void f(); // 内部链接
    extern void h(); // C语言链接
                                     // #2: i 没有链接
    int i {
        extern void f(); // 内部链接
        extern int i; // #3: 外部链接，是非良法的
    }
}
```

如果没有第 `#2` 行的声明，第 `#3` 行的声明将与名称 `#1` 链接。然而，由于具有内部链接的声明被隐藏了，`#3` 被赋予了外部链接，导致程序是非良法的。—结束示例

7 当发现具有链接的实体的块作用域声明未引用其他声明时，则该实体是最内层命名空间作用域的成员。然而，此类声明不会在其命名空间作用域中引入成员名称。

© ISO/IEC 2020 – 版权所有

# ISO/IEC 14882:2020(E)

示例 2:

```cpp
namespace X {
  void p() {
    q(); // 错误：q 尚未声明
    extern void q(); // q 是声明
  }

  void middle() {
    q(); // 错误：尚未声明
  }

  void q() { /* ... }
  void q() { /* ... }
}
```
