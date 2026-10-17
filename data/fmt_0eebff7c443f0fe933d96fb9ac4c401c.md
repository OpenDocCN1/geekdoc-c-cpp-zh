
这两个特化都比主模板更特化。#1 更特化是因为从模板参数列表中推导其模板参数成功，而反之不然。#2 更特化是因为模板参数相等，但部分特化具有更多约束（13.5.5）。

类模板部分特化可以在主模板可以定义的任何作用域声明（9.8.2.3, 11.4, 13.7.3）。

[示例 4:
```cpp
template<class T> struct A {
struct C {
template<class T2> struct B {};
template<class T2> struct B<T2*> {}; // 部分特化 #1
}; // // A<T*>::C::B<T2> 的部分特化
template<class T> template<class T2> struct A<T*>::C::B<T2*>; {}; // #2
```
]

# ISO/IEC 14882:2020(E)

`A<short>:::B<int> absig;` // 使用部分特化 #2
end example;

部分特化声明本身不会通过名称查找找到。当使用主模板时，任何之前声明的主模板的部分特化版本也会被考虑在内。结果之一是，使用 声明（using-declaration）指向一个类模板不会限制通过该使用 声明可能找到的部分特化集合。

[示例:
```
namespace N {
    template<class T1, class T2> class A { }; // 主模板
}
using N::A; // 指向主模板
namespace N {
    template<class T> A<T, T> { }; // 部分特化
}
A<int,int> a; // 使用了部分特化，该特化通过使用 声明找到
    // 指向主模板
end example;
```

如果一个非类型参数是一个非类型参数的名称，则它是未特化化的。所有其他非类型参数都是特化化的。

在类部分特化的参数列表中，适用以下限制：

- (9.1) 对应于特化非类型参数的模板参数类型不应依赖特化的参数。

[示例:
```
template <<class T, T> struct C {};
template <class T> struct CT1, // 错误
```
]
```
template<int, X, (array_ptr[X])> class A {};
int array[5]; // 错误
template<int, X> A<X, &X> {};
```
- (9.2) 特化应该比主模板更特化 (13.7.6.3)。
- (9.3) 特化的模板列表不包含默认模板值¹¹³
- (9.4) 参数不应包含展开的包。如果一个参数是包展开 (13.7.4)，则它应该是模板参数列表中的最后一个参数。

访问规则不适用于用于指定部分特化的 simple-template-id 模板名称的非类型参数。

> [注 2: 模板可以是私有类型或通常情况下可以访问的对象。在声明部分特化时无法检查依赖名称，但在替换到部分特化时将进行检查。 -- 附结束]

# 13.7.6.2 类模板部分特化的匹配 [temp.class.spec.match]

- 1 当类模板用在需要类实例化的上下文中时，有必要确定该实例化是通过使用主模板还是其中一个部分特化生成的。这是通过匹配类模板特化的模板参数与部分特化的模板参数列表来完成的。

- (1.1) 如果仅找到一个匹配的特化，则实例化由该特化生成。

- (1.2) 如果找到多个匹配的特化，则使用偏序规则 (13.7.6.3) 来确定其中哪一个特化比其他更特化。如果没有一个特化比所有其他匹配的特化都特化，则该类模板的使用是歧义的，程序是格式错误的。

138 在这种情况下没有使用的语境。

§ 13.7.6.2

©ISO/IEC 2020 – 版权所有 391

(1.3) — 如果未找到匹配项，则实例化从主模板推导。

2 如果部分特化的模板参数可以从实际模板参数列表中推导 (13.10.3)，且推导出的模板参数满足部分特化的相关约束（如果有，13.5.3），则该部分特化匹配给定的实际模板参数列表。

[示例 1:]
```
template<class T1, class T2, int I> class A {
};\ // #1
template<class T, int I>
class A<T, I> {
};\ // #2
template<class T1, class T2, int I>
class A<T1, T*, I> {
};\ // #3
template<class T>
class A<int, T>> {
};\ // #4
template<class T1, class T2, int I>
class A<T1, T2, I> {
};\ // #5
A<int, int, I> a1; // 使用 #1
A<int, int, I> a2; // 使用 #2, T 是 int, I 是 1
A<int, char, S> a3; // 使用 #3
A<int, char, S> a4; // 使用 #4
A<int*, int, I> a5; // 使用 #5, T1 是 int, T2 是 char, I 是 // 歧义：匹配 #3 和 #5
// 示例结束
```

[示例 2:]
```
template<typename T> concept C = requires (T t) { t.f(); };
template<typename T> struct S {
};\ // #1
template<class C> struct S {
};\ // #2
struct Arg { void f(); };
S<int> s1; // 使用 #1; 不满足 #2 的约束
S<Arg> s2; // 使用 #2; 约束都满足，但 #2 更特化
// 示例结束
```

3 如果因为模板参数列表和模板 ID 的结构而无法推导部分特化的模板参数，则程序是格式错误的。

[示例 3:]
```
template <int I, int J> struct A {};
template <int I> struct A<I, I2> {}; // 错误
template <int I> struct A<I, int> {}; // OK
template <int I, int J, int K> struct B {};
template <int I> B<I, I2, 2> {}; // OK
// 示例结束
```

4 在类型名称引用类特化时（例如，`A<int, int, I>`），参数列表必须匹配主模板的模板参数列表。特化的模板参数是从主模板推导的。

# 13.7.6.3 类模板特化的排序 [temp.class.order]

1 对于两个类模板特化，根据以下类似于两个函数模板的配方，第一个函数模板根据函数模板规则 (13.7.7.3) 比第二个更特化，则此类推：

- 每个函数模板都具有与对应特化相同的模板参数和相关约束 (13.5.3)。每个函数模板都有一个函数参数，其类型为类特化，其中模板参数是函数模板中每个模板参数对应的模板参数。对于部分特化的 simple-template-id 的模板参数列表。

[示例 1:]
```
template<int, int, class T> class X {};
X<int, int> {}; // #1
```
```
template<int I> class X<I, int> {}; // #2
```
```
template<int I> void f(X<I, int>); // A
template<int I> void f(X<int, int>); // B
```
根据函数模板的规则，B 比 A 更特化。因此，部分特化 #2 比 #1 更特化。示例结束

[示例 2:]
```
template<typename T> class C = requires (T t) { t.f(); };
template<typename T> class D = CC && requires (T t) { t.f(); };
```
```
template<typename T> class S { // #1
template<class T> class S<T> {}; // #2
```
```
template<class T> void f(S<T>); // A
template<class D> void f(S<T>); // B
```
部分特化 #2 比 #1 更特化，因为 B 比 A 更特化。示例结束

# 13.7.6.2 类模板特化的成员 [temp.class.spec.mfunc]

- 类部分特化的成员模板参数列表应匹配部分特化的参数列表。类模板特化成员的模板参数是一个独立的特化。类部分特化是一个独立的模板。该类部分特化的成员与主模板无关。在需要定义的情况下使用的类部分特化成员应当被定义；主模板成员的定义绝不用作类部分特化成员的定义。类部分特化成员的显式特化声明方式与显式类相同：

[示例 1:]
```
// 主类模板
template<class T, int I> struct A {
    void f();
};
```
// 主类模板的成员
```
template<class T, int I> void A<T,I>::f() {
```
```
// 类部分特化
template<class T> struct A<T,2 {
    void f();
    void g();
    void h();
};
```
// 类部分特化的成员
```
template<class T> void A<T,2>::g() {
```
// 显式特化
```
template<> void A<char,2>::h() {
```
```cpp
int main() {
  A<char,0> a0;
  A<char,2> a2;
  a0.f();
  a2.g();
  // OK, uses definition of primary template's member
  // OK, uses definition of partial specialization's member
  // OK, uses definition of explicit specialization's member
  // error: no definition of f for Kt2; the primary template is not used here
}
```

如果成员模板被部分特化，则这些成员模板的部分特化是包含它的类模板的成员：如果该类模板被实例化（13.9.2, 13.9.3），则每个成员部分特化的声明也会作为创建类模板特化成员的一部分被实例化。如果主成员针对外部模板的某个（隐式）特化进行了显式特化，则对于该类模板的该次特化，成员模板的部分特化将被忽略。如果成员模板的部分特化针对外部类模板的某个（隐式）特化进行了显式特化，则主成员模板及其其他部分特化对于该类模板的该次特化仍然被考虑。

```cpp
Example 2:
template<class T> struct A {
  template<class T2> struct B {}; // #1
  template<class T2> struct B<T2> {}; // #2
};
template<class T> template<class T2> struct A::short:B {}; // #3
A<int>:B<int>
Ashort:B<int*> abcip; // uses #2
A<int>:B<int*> abci; // uses #3
end example; // #1
```

## 13.7.7 函数模板 [temp.fct]

### 13.7.7.1 通用

函数模板定义了一组无界的相关的函数。

[示例 1：一组排序函数可以如下所示声明：
```cpp
template<class T> class Array {
  template<class T> void sort(Array<T>);
};
// end example; // (9.3.4.6)
```

函数模板可以与其他函数模板以及非函数模板进行重载（即：它永远被视为一个特化版本），即使它的名称和类型与一个可能生成的函数模板相同。[1.99]

## 13.7.7.2 函数重载 [temp.overload]

可以重载函数模板，使得两个不同的函数模板具有相同的类型。

[示例 1：
```cpp
// translation unit 1: // translation unit 2:
template<class T>      template<class T>
void f(T);            void f(T);
void g(int* p) {      void h(int* p) {
  f(p);                 f(p); // calls f<int>(int*)
}
}
 // end example;
```

> 139) 也就是说，非函数模板的声明不允许解析具有相同名的函数模板特化。如果非函数模板在程序中被 odr 定义（6.3），则它必须被定义；否则它将使用函数模板定义进行隐式实例化。

ISO/IEC 14882:2020(E)

2 特化是不同的函数，且不违反违反规则 (6.3)。

3 函数模板的签名在第 3 节中定义。模板参数的名称仅对于建立模板参数与签名其余部分之间的关系具有意义。

> [注意 1：两个不同的函数可以具有相同的返回类型和函数模板列表，即使重载解析无法区分它们。]

```cpp
template <class T> void f(I); // 重载了第一个模板
template<int I> void f(); // 通过显式模板参数列表可以区分
// end
```

4 当引用模板参数的表达式用在函数模板声明的参数列表或返回类型中时，该引用参数的表达式是该函数模板签名的一部分。这种设计是为了允许一个编译单元中的函数模板声明与另一个编译单元中的函数模板声明进行链接，反之，也确保函数模板之间不会局限于彼此。

[示例 2：]
```cpp
template <int I, int J> void f(A<I>, A<J>); // #1
template <int K, int L> void f(A<K>, A<L>); // 与 #1 相同
template <int I, int J> void f(A<J>, A<I>); // 与 #1 不同
// end example
```

> [注意 2：大多数使用模板的表达式使用非类型模板参数，但表达式也可以引用类型参数。类型参数可以使用 sizeof 表达式。——结束注意]

5 涉及参数的两个表达式如果包含这些表达式的函数满足定义规则 (6.3)，则被视为等价，但命名模板参数的标记可以不同，或者一个表达式中命名模板参数的标记被另一个标记替换。不涉及模板参数的未求值表达式如果包含这些表达式的函数满足相同的定义规则，则被视为等价，但类型和声明的标记可以不同（只要实体名称相同），且形成内容 ID 的标记可以不同，因为模板 ID 是相同的 (13.6)。

> [注意 3：例如，`A<4>` 和 `A<0>` 具有相同的类型。]

# ISO/IEC 14288:2020(E)

部分序选择通过依次转换每个模板（见下一段）并使用函数类型进行参数推导，来选择哪个函数模板比另一个更特化（more specialized）。推导过程决定了两个模板中是否一个比另一个更特化。如果是，则更特化的那个是部分序选择过程选中的模板。如果两者都成功，则部分序选择将确定的最约束的模板（如果存在）选为结果。

为了生成转换后的模板，对于其中的每个类型、非类型或模板参数（包括模板参数包 (13.7.4)），将分别合成一个唯一的值或类类型，并确保它在模板类型中对应的该函数类型的每个实例中都出现。

> [Note: 1] 为非类型模板参数合成的数值类型中的替换占位符，也是一个唯一的合成类型 — 尾注。

每个在类中且是函数的模板 M 都被认为在其函数列表中定义了一个类型为 X(M) 的第一个参数（定义如下）。如果任何模板在重载解析中通过重写候选者 (12.2.4.3) 以反转的参数顺序被考虑，则其转换后模板中的函数参数顺序被反转。对于具有 cv 修饰符 cv 且为类的成员函数 M：

- 如果 M 的可选 ref-修饰符为 &&，或者如果 M 没有 ref-修饰符且另一个转换后模板在位置上对应的参数具有值引用（value reference），则 X(M) 为“对 A 的值引用”；此判定取决于 X(M) 是否为 r 引用类型，此处不考虑

- 否则，X(M) 为“对 A 的无效引用”。

> [Note: 2] 这允许非静态成员相对于非成员函数进行排序，并使结果等同于两个等效非成员的的顺序 — 尾注。

```
[Example:
struct A {};
template<class T> struct B {
    template<class R> int operator*(const R&); // #1
};
template<class T, class R> int operator*(const T&, R&); // #2
// B::operator* 的推导被转换等同于
// template<class R> int operator*(B<A>, R); // #1a
```
```
int main() {
 A a;
 B<A> b;
 b * a;
 // 调用 #1
}
 end example]
```

使用转换后的函数模板的函数类型，按照 13.10.5 述，针对另一个模板进行推导。

```
[Example 2:
