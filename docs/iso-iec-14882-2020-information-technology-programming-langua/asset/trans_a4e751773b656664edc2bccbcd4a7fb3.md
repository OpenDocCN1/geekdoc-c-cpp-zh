

## 13.7.2.3 推导指引 [temp.deduct.guide]

1 推导指引用于当模板名作为推导类类型（9.2.9.7）的类型说明符出现时。推导指引不是通过名称查找找到的。相反，在执行类模板参数推导（12.4.2.9）时，会考虑为该类模板声明的任何推导指引。

```
deduction-guide:
    explicit-specifieropt template-name ( parameter-declaration-clause ) -> simple-template-id ;
```

2 [示例 1：

```
template<class T, class D = int>
struct S {
    T data;
};
template<class U>
S(U) -> S<typename U::type>;

struct A {
    using type = short;
    operator type();
};
S x{A()};        // x is of type S<short, int>
```

— 结束示例]

3 推导指引的参数声明子句适用与函数声明（9.3.4.6）相同的限制。simple-template-id 必须命名一个类模板特化。template-name 必须与 simple-template-id 的 template-name 相同标识符。一个 deduction-guide 必须在与对应类模板相同的范围内声明，并且对于成员类模板，具有相同的访问权限。同一翻译单元中针对同一类模板的两个 deduction guide 声明不得具有等价的参数声明子句。

## 13.7.2.4 类模板的成员类 [temp.mem.class]

1 类模板的成员类可以在其被声明的类模板定义之外定义。

> [注 1：成员类必须在其首次使用且需要实例化之前被定义（13.9.2）。例如，
>
> ```
> template<class T> struct A {
>     class B;
> };
> A<int>::B* b1;                // OK: requires A to be defined but not A::B
> template<class T> class A<T>::B { };
> A<int>::B b2;                // OK: requires A::B to be defined
> ```
>
> — 结束注]

## 13.7.2.5 类模板的静态数据成员 [temp.static]

1 可以在静态成员的类模板定义所包含的命名空间范围内为静态数据成员或静态数据成员模板提供定义。

[示例 1：

```
template<class T> class X {
    static T s;
};
template<class T> T X<T>::s = 0;
```

[示例 2：Array<T>::operator[] 的模板参数将由进行下标操作的 Array 决定。

```
Array<int> v1(20);
Array<dcomplex> v2(30);

v1[3] = 7;                // Array<int>::operator[]
v2[3] = dcomplex(7,8);    // Array<dcomplex>::operator[]
```

— 结束示例]

— 结束示例]

2 非闭包类型的局部类不得具有成员模板。访问控制规则（11.9）适用于成员模板名。析构函数不得是成员模板。具有给定名称和类型的非模板成员函数（9.3.4.6）以及可以用于生成相同类型的特化的同名成员函数模板都可以声明在一个类中。当两者都存在时，对该名称和类型的引用指的是非模板成员，除非提供了显式的模板参数列表。

[示例 3：

```
template <class T> struct A {
    void f(int);
    template <class T2> void f(T2);
};

template <> void A<int>::f(int) { }    // non-template member function
template <> template <> void A<int>::f<>(int) { }    // member function template specialization

int main() {
    A<char> ac;
    ac.f(1);    // non-template
    ac.f('c');  // template
    ac.f<>(1);  // template
}
```

— 结束示例]

3 成员函数模板不得为虚函数。

[示例 4：

```
template <class T> struct AA {
    template <class C> virtual void g(C);    // error
    virtual void f();    // OK
};
```

— 结束示例]

4 成员函数模板的特化不会覆盖来自基类的虚函数。

[示例 5：

```
class B {
    virtual void f(int);
};

class D : public B {
    template <class T> void f(T); // does not override B::f(int)
    void f(int i) { f<>(i); }    // overriding function that calls the template instantiation
};
```

— 结束示例]

5 转换函数模板的特化以与转换到相同类型的非模板转换函数相同的方式被引用。

[示例 6：

```
struct A {
    template <class T> operator T*();
};
template <class T> A::operator T*() { return 0; }
template <> A::operator char*() { return 0; }    // specialization
template A::operator void*();    // explicit instantiation

int main() {
    A a;
    int* ip;
    ip = a.operator int*();    // explicit call to template operator A::operator int*()
}
```

— 结束示例]

> [注 1：没有语法可以通过提供显式模板参数列表（13.10.2）来形成转换函数模板（11.4.8.3）的 template-id（13.3）。 — 结束注]

6 转换函数模板的特化不是通过名称查找找到的。相反，会考虑在使用的上下文中可见的任何转换函数模板。对于每个这样的 operator，如果参数推导成功（13.10.3.4），则由此产生的特化就好像是通过名称查找找到的一样使用。

7 派生类中的 using-declaration 不能引用基类中转换函数模板的特化。

8 重载决议（12.4.4.3）和偏序（13.7.7.3）用于在多个转换函数模板特化和/或非模板转换函数之间选择最佳转换函数。

## 13.7.4 可变参数模板 [temp.variadic]

1 模板参数包是一个接受零个或多个模板参数的模板参数。

> [示例 1：
>
> ```
> template<class ... Types> struct Tuple { };
> 
> Tuple<> t0;                // Types contains no arguments
> Tuple<int> t1;            // Types contains one argument: int
> Tuple<int, float> t2;     // Types contains two arguments: int and float
> Tuple<0> error;           // error: 0 is not a type
> ```
>
> — 结束示例]

2 函数参数包是一个接受零个或多个函数参数的函数参数。

> [示例 2：
>
> ```
> template<class ... Types> void f(Types ... args);
> 
> f();        // args contains no arguments
> f(1);      // args contains one argument: int
> f(2, 1.0); // args contains two arguments: int and double
> ```
>
> — 结束示例]

3 初始化捕获包是 lambda 捕获，它为其初始化器的包展开中的每个元素引入一个初始化捕获。

> [示例 3：
>
> ```
> template <typename... Args>
> void foo(Args... args) {
>     [...xs=args]{
>         bar(xs...);    // xs is an init-capture pack
>     };
> }
> 
> foo();   // xs contains zero init-captures
> foo(1);  // xs contains one init-capture
> ```
>
> — 结束示例]

4 包是模板参数包、函数参数包或初始化捕获包。模板参数包或函数参数包的元素数量是为该参数包提供的参数数量。初始化捕获包的元素数量是其初始化器的包展开中的元素数量。

5 包展开由一个模式和省略号组成，其实例化会产生零个或多个模式的实例化列表（如下所述）。模式的形式取决于展开发生的上下文。包展开可以在以下上下文中出现：

- (5.1) — 在函数参数包（9.3.4.6）中；模式是省略省略号的参数声明。
- (5.2) — 在 using-declaration（9.9）中；模式是一个 using-declarator。
- (5.3) — 在作为包展开的模板参数包（13.2）中：
    - (5.3.1) — 如果模板参数包是参数声明；模式是省略省略号的参数声明；

- (8.1) — 如果包是模板参数包，则元素是对应种类的模板参数（13.2）指定第 i 个对应的类型或值模板参数；
- (8.2) — 如果包是函数参数包，则元素是 id-expression 指定由函数参数包声明实例化产生的第 i 个函数参数；否则
- (8.3) — 如果包是初始化捕获包，则元素是 id-expression 指定由初始化捕获包实例化产生的第 i 个初始化捕获引入的变量。

所有 Eᵢ 都成为包含列表中的项。

> [注 1：列表的种类随上下文而变化：expression-list、base-specifier-list、template-argument-list 等。 — 结束注]

当 N 为零时，展开的实例化会产生一个空列表。这样的实例化不会改变包含构造的语法解释，即使在省略列表本身原本会不 well-formed 或会导致语法歧义的情况下也是如此。

> [示例 6：
>
> ```
> template<class... T> struct X : T... { };
> template<class... T> void f(T... values) {
>   X<T...> x(values...);
> }
> 
> template void f<>();    // OK: X<> has no base classes
> // x is a variable of type X<> that is value-initialized
> ```
>
> — 结束示例]

9 sizeof... 表达式（7.6.2.5）的实例化会产生一个包含其展开的包中元素数量的积分常量。

10 fold-expression 的实例化会产生：

- (10.1) — ((E₁ op E₂) op ...) op Eₙ 用于一元左折叠，
- (10.2) — E₁ op (... op (Eₙ₋₁ op Eₙ)) 用于一元右折叠，
- (10.3) — (((E op E₁) op E₂) op ...) op Eₙ 用于二元左折叠，以及
- (10.4) — E₁ op (... op (Eₙ₋₁ op (Eₙ op E))) 用于二元右折叠。

在每种情况下，op 是 fold-operator，N 是包展开参数中的元素数量，每个 Eᵢ 是通过实例化模式并将每个包展开参数替换为其第 i 个元素而生成的。对于二元 fold-expression，E 是通过实例化未包含未展开包的 cast-expression 而生成的。

> [示例 7：
>
> ```
> template<typename ...Args>
>   bool all(Args ...args) { return (... && args); }
> 
> bool b = all(true, true, true, false);
> ```
>
> 在 all 的实例化中，返回的表达式展开为 ((true && true) && true) && false，其求值为 false。 — 结束示例]

如果一元 fold-expression 的 N 为零，则表达式的值如表 17 所示；如果运算符未列在表 17 中，则实例化为 ill-formed。

**表 17：折叠空序列的值 [tab:temp.fold.empty]**

| 运算符 | 当包为空时的值 |
| --- | --- |
| && | true |
| || | false |
| , | void() |

