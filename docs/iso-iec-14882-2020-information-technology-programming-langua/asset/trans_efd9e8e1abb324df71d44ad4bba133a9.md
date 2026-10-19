

## ISO/IEC 14882:2020(E)

2 此类特化是不同的函数，不违反单一定义规则（6.3）。

3 函数模板的签名在第 3 条款中定义。模板参数的名称仅对建立模板参数与其余签名之间的关系有意义。

> [Note 1: 两个不同的函数模板可以具有相同的函数返回类型和函数参数列表，即使仅靠重载决议也无法区分它们。
```
template<class T> void f();
template<int I> void f();    // OK: overloads the first template
                         // distinguishable with an explicit template argument list
```
— end note

4 当在函数模板的声明中函数参数列表或返回类型中使用引用模板参数的表达式时，该引用模板参数的表达式是函数模板签名的一部分。这是为了允许在一个翻译单元中声明的函数模板与另一个翻译单元中声明的同一函数模板进行链接，反之亦然，并确保本应不同的函数模板不会相互链接。

> [Example 2:
```
template <int I, int J> A<I+J> f(A<I>, A<J>);    // #1
template <int K, int L> A<K+L> f(A<K>, A<L>);    // same as #1
template <int I, int J> A<I-J> f(A<I>, A<J>);    // different from #1
```
— end example

> [Note 2: 大多数使用模板参数的表达式使用非类型模板参数，但表达式可能引用类型参数。例如，模板类型参数可用于 sizeof 运算符中。 — end note]

5 如果两个包含表达式的函数定义满足单一定义规则（6.3），则涉及模板参数的两个表达式被认为等价，除非用于命名模板参数的标记可能不同，只要在其中一个表达式中用于命名模板参数的标记被另一个表达式中命名同一模板参数的标记替换即可。两个不涉及模板参数的未求值操作数如果在两个包含该表达式的函数定义中满足单一定义规则，则被认为等价，除非用于命名类型和声明的标记可能不同，只要它们命名相同的实体，并且用于形成概念-id 的标记可能不同，只要两个 template-id 相同（13.6）。

> [Note 3: 例如，A<42> 和 A<40+2> 命名相同的类型。 — end note]

两个 lambda 表达式永远不被认为等价。

> [Note 4: 其意图是避免 lambda 表达式出现在具有外部链接的函数模板的签名中。 — end note]

对于确定两个依赖名称（13.8.3）是否等价，仅考虑名称本身，而不考虑在模板上下文中进行名称查找的结果。如果同一函数模板的多个声明在该名称查找的结果上不同，则使用第一个声明的结果。

> [Example 3:
```
template <int I, int J> void f(A<I+J>);          // #1
template <int K, int L> void f(A<K+L>);          // same as #1

template <class T> decltype(g(T())) h();
int g(int);
template <class T> decltype(g(T())) h()          // redeclaration of h() uses the earlier lookup...
{ return g(T()); }                              // ... although the lookup here does find g(int)
int i = h<int>();                               // template argument substitution fails; g(int)
                                                // was not in scope at the first declaration of h()
```
```
// ill-formed, no diagnostic required: the two expressions are functionally equivalent but not equivalent
template <int N> void foo(const char (*s)[([{}], N)]);
template <int N> void foo(const char (*s)[([{}], N)]);
```
```
// two different declarations because the non-dependent portions are not considered equivalent
template <class T> void spam(decltype([]{}) (*s)[sizeof(T)]);
template <class T> void spam(decltype([]{}) (*s)[sizeof(T)]);
```

## 13.8 Name resolution [temp.res]

### 13.8.1 General [temp.res.general]

3 *concept-definition* 必须出现在命名空间作用域（6.4.6）。

4 concept 不应具有关联约束（13.5.3）。

5 concept 不会被实例化（13.9）。

> [Note 1: concept-id（13.3）作为表达式求值。concept 不能被显式实例化（13.9.3）、显式特化（13.9.4）或部分特化。 — end note]

6 *concept-definition* 的 *constraint-expression* 是未求值操作数（7.2.3）。

7 concept 定义的第一个声明的模板参数是其 *prototype parameter*。*type concept* 是其原型参数为类型 *template-parameter* 的 concept。

1 模板定义中可以使用三种名称：
- (1.1) — 模板本身的名称，以及在模板本身内声明的名称。
- (1.2) — 依赖于 *template-parameter*（13.8.3）的名称。
- (1.3) — 在模板定义内可见的作用域中的名称。

2 在模板声明或定义中使用的且依赖于 *template-parameter* 的名称，除非适用的名称查找找到类型名或该名称由关键字 `typename` 限定，否则假定不命名类型。
```
template<C T>    // C, as a type-constraint, constrains f2(T)
T f2(T x) { return x; }
```
```
[Example 1:
// no B declared here

class X;

template<class T> class Y {
    class Z;    // forward declaration of member class
    void f() {
        X* a1;    // declare pointer to X
        T* a2;    // declare pointer to T
        Y* a3;    // declare pointer to Y<T>
        Z* a4;    // declare pointer to Z
        typedef typename T::A TA;
        TA* a5;    // declare pointer to T's A
        typename T::A* a6;    // declare pointer to T's A
        T::A* a7;    // error: no visible declaration of a7
                    // T::A is not a type name; multiplication of T::A by a7
        B* a8;    // error: no visible declarations of B and a8
                // B is not a type name; multiplication of B by a8
    }
};
— end example]
```
```
typename-specifier:
    typename nested-name-specifier identifier
    typename nested-name-specifier template_opt simple-template-id
```

3 *typename-specifier* 表示通过省略关键字 `typename` 形成的 *simple-type-specifier*（9.2.9.3）所表示的类型或类模板。即使在 `typename` 存在的情况下，也使用通常的限定名称查找（6.5.4）来查找 *qualified-id*。
```
[Example 2:
struct A {
    struct X { };
    int X;
};
```

[Example 4:
```
template <class T> void f(int i) {
    T::x * i;        // expression, not the declaration of a variable i
}
```
```
struct Foo {
    typedef int x;
};
```
```
struct Bar {
    static int const x = 5;
};
```
```
int main() {
    f<Bar>(1);        // OK
    f<Foo>(1);        // error: Foo::x is a type
}
```
— end example]

7 在类模板的定义内或在类模板成员的定义内在 declarator-id 之后，引用当前实例化（13.8.3.2）的成员时不需要关键字 typename。
[Example 5:
```
template<class T> struct A {
    typedef int B;
    B b;              // OK, no typename required
};
```
— end example]

8 模板的有效性可在任何实例化之前进行检查。

[Note 2: 知道哪些名称是类型名使得可以以这种方式检查每个模板的语法。 — end note]

程序格式错误，无需诊断，如果：
- (8.1) — 无法为模板或模板内的 constexpr if 语句（8.5.2）内的子语句生成有效特化，且模板未被实例化，或
- (8.2) — 将模板参数替换为类型约束或 requires-clause 中不会产生有效表达式，或
- (8.3) — 每个有效特化都要求可变参数模板的参数包为空，或
- (8.4) — 在其定义之后立即对模板进行假设实例化会因不依赖于模板参数的构造而格式错误，或
- (8.5) — 在假设实例化中对该构造的解释与在模板的任何实际实例化中对应构造的解释不同。

[Note 3: 这可能发生在包括以下情况：
- (8.5.1) — 在模板定义点处在非依赖名称中使用的类型不完整，但在实例化点处完整，或
- (8.5.2) — 在模板定义中对名称的查找找到了 using-declaration，但在实例化中对应作用域的查找未找到任何声明，因为 using-declaration 是包展开且对应包为空，或
- (8.5.3) — 实例化使用在模板定义点尚未定义的默认参数或默认模板参数，或
- (8.5.4) — 模板实例化中的常量表达式求值（7.7）使用
- (8.5.4.1) — 积分或无作用域枚举类型的 const 对象的取值，或
- (8.5.4.2) — constexpr 对象的取值，或
- (8.5.4.3) — 引用的取值，或
- (8.5.4.4) — constexpr 函数的定义，

