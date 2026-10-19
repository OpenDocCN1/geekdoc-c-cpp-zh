
// 从 C<T, std::type_identity_t<U>> 推导 C<V *, V*> 的参数会将 T 推导为 V *;
// f2' 是通过上述过程对 f2 进行转换得到的。
template<class V, class U>
  requires deduces_A<C<V *, std::type_identity_t<U>>>
  auto f2_prime(V *, U) -> C<V *, std::type_identity_t<U>>;

// 下面的概念确保 B 的特化会被推导。
template <class> class BB;
template <class V> class BB<B<V>> { };
template <class T> concept deduces_B = requires { sizeof(BB<T>); };

// 从上述针对 A 的 f1' 和 f2' 推导出的 B 的指南如下：
template<std::integral W>
  requires deduces_A<C<W *, W *>> && deduces_B<C<W *, W *>>
  auto f1_prime_for_B(W *, W *) -> C<W *, W *>;

template<std::integral W, class U>
  requires deduces_A<C<W *, std::type_identity_t<U>>> &&
    deduces_B<C<W *, std::type_identity_t<U>>>
  auto f2_prime_for_B(W *, U) -> C<W *, std::type_identity_t<U>>;
— end example

## 12.4.3 可行函数 [over.match.viable]

1 从为给定上下文构造的候选函数集合（12.4.2）中，选择一组可行函数，从中将通过比较参数转换序列和相关约束（13.5.3）来选择最佳函数（12.4.4）。可行函数的选择考虑相关约束（如果有）以及参数与函数参数之间的关系，而不仅仅是转换序列的排序。

2 首先，要成为可行函数，候选函数必须具有足够多的参数以与列表中的参数数量一致。

- (2.1) — 如果列表中有 m 个参数，所有恰好有 m 个参数的候选函数都是可行的。
- (2.2) — 具有少于 m 个参数的候选函数只有在其参数列表中具有省略号时才是可行的（9.3.4.6）。对于重载决议的目的，任何没有对应参数的参数都被认为“匹配省略号”（12.4.4.2.4）。
- (2.3) — 具有多于 m 个参数的候选函数只有当第 m 个参数之后的所有参数都有默认参数时才是可行的（9.3.4.7）。对于重载决议的目的，参数列表在右侧被截断，以便恰好有 m 个参数。

3 其次，对于一个函数要可行，如果它具有相关约束（13.5.3），这些约束必须得到满足（13.5.2）。

4 第三，对于 F 要成为可行函数，对于每个参数，都必须存在一个隐式转换序列（12.4.4.2），该序列将该参数转换为 F 的对应参数。如果参数具有引用类型，则隐式转换序列包括绑定引用的操作，并且左值引用到非 const 不能绑定到右值以及右值引用不能绑定到左值这一事实会影响函数的可行性（参见 12.4.4.2.5）。

## 12.4.4 最佳可行函数 [over.match.best]

### 12.4.4.1 通用 [over.match.best.general]

1 定义 ICSi(F) 如下：

- (1.1) — 如果 F 是静态成员函数，则 ICS1(F) 被定义为使得 ICS1(F) 对于任何函数 G 都既不比 ICS1(G) 好也不比 ICS1(G) 差，并且对称地，ICS1(G) 对于 ICS1(F) 既不比好也不比差；127 否则，
- (1.2) — 令 ICSi(F) 表示将列表中第 i 个参数转换为可行函数 F 的第 i 个参数类型的隐式转换序列。12.4.4.2 定义了隐式转换序列，并且

> 127) 如果一个函数是静态成员函数，则该定义意味着第一个参数，即隐含的对象参数，在确定函数是否比其他函数更好或更差时没有影响。

12.4.4.3 定义了何为一个隐式转换序列比另一个隐式转换序列更好或更差。

2 根据这些定义，可行函数 F1 被定义为比另一个可行函数 F2 更好的函数，如果对于所有参数 i，ICSi(F1) 不比 ICSi(F2) 更差，并且然后

- (2.1) — 对于某个参数 j，ICSj(F1) 比 ICSj(F2) 是更好的转换序列，或者，如果不是这样，

- (2.2) — 上下文是通过用户定义转换进行的初始化（参见 9.4、12.4.2.6 和 12.4.2.7），并且从 F1 的返回类型到目标类型（即正在初始化的实体的类型）的标准转换序列比从 F2 的返回类型到目标类型的标准转换序列更好

[Example 1:

```
struct A {
  A();
  operator int();
  operator double();
} a;
int i = a;        // a.operator int() followed by no conversion is better than
                  // a.operator double() followed by a conversion to int
float x = a;      // ambiguous: both possibilities require conversions,
                  // and neither is better than the other
```

— end example]

或者，如果不是这样，

- (2.3) — 上下文是通过转换函数进行直接引用绑定的初始化（12.4.2.7），引用类型为函数类型，F1 的返回类型与正在初始化的引用的种类（左值或右值）相同，而 F2 的返回类型不同

[Example 2:

```
template <class T> struct A {
  operator T&();    // #1
  operator T&&();   // #2
};
typedef int Fn();
A<Fn> a;
Fn& lf = a;        // calls #1
Fn&& rf = a;       // calls #2
```

— end example]

或者，如果不是这样，

- (2.4) — F1 不是函数模板特化而 F2 是函数模板特化，或者，如果不是这样，

- (2.5) — F1 和 F2 都是函数模板特化，并且根据 13.7.7.3 中描述的部分排序规则，F1 的函数模板比 F2 的模板更特化，或者，如果不是这样，

- (2.6) — F1 和 F2 是具有相同参数类型列表的非模板函数，并且根据 13.5.5 中描述的约束的部分排序，F1 比 F2 更受约束，或者如果不是这样，

- (2.7) — F1 是类 D 的构造函数，F2 是 D 的基类 B 的构造函数，并且对于所有参数，F1 和 F2 的对应参数具有相同的类型

[Example 3:

```
struct A {
  A(int = 0);
};

struct B: A {
  using A::A;
  B();
};

int main() {
  B b;            // OK, B::B()
}
```

[Example 7:

```
void Fcn(const int*, short);
void Fcn(int*, int);

int i;
short s = 0;

void f() {
    Fcn(&i, s);        // is ambiguous because &i → int* is better than &i → const int*
                       // but s → short is also better than s → int

    Fcn(&i, 1L);       // calls Fcn(int*, int), because &i → int* is better than &i → const int*
                       // and 1L → short and 1L → int are indistinguishable

    Fcn(&i, 'c');      // calls Fcn(int*, int), because &i → int* is better than &i → const int*
                       // and c → int is better than c → short
}
```

— end example]

4 如果最佳可行函数解析为找到多个声明的函数，并且如果其中至少两个声明 — 或在使用声明的情况下它们所引用的声明 — 指定了使函数可行的默认参数，则程序格式错误。

[Example 8:

```
namespace A {
    extern "C" void f(int = 5);
}
namespace B {
    extern "C" void f(int = 5);
}

using A::f;
using B::f;

void use() {
    f(3);    // OK, default argument was not used for viability
    f();     // error: found default argument twice
}
```

— end example]

## 12.4.4.2 隐式转换序列 [over.best.ics]

### 12.4.4.2.1 通用 [over.best.ics.general]

1 隐式转换序列是用于将函数调用中的参数转换为正在调用的函数的对应参数类型的转换序列。转换序列是 7.3 中定义的隐式转换，这意味着它受单个表达式初始化对象或引用规则的约束（9.4、9.4.4）。

2 隐式转换序列只关心参数的类型、cv-限定和值类别，以及这些如何转换为匹配参数的对应属性。

> [Note 1: 其他属性，例如参数的生命周期、存储类、对齐、访问性、参数是否为位域，以及函数是否被删除（9.5.3），都被忽略。因此，尽管可以为给定的参数-参数对定义隐式转换序列，但从参数到参数的转换最终仍可能格式错误。 — end note]

3 一个格式良好的隐式转换序列是以下形式之一：

- (3.1) — 标准转换序列（12.4.4.2.2），
- (3.2) — 用户定义转换序列（12.4.4.2.3），或
- (3.3) — 省略号转换序列（12.4.4.2.4）。

4 然而，如果目标是

- (4.1) — 构造函数的第一个参数或

