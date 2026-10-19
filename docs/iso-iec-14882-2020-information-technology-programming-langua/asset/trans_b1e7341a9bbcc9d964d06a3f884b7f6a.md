

## 13.7.5 友元 [temp.friend]

1 类或类模板的友元可以是函数模板或类模板、函数模板或类模板的特化，或者非模板函数或类。对于不是模板声明的友元函数声明：

- (1.1) 如果友元的名称是有限定或未限定的模板标识，则友元声明指代函数模板的一个特化；否则，
- (1.2) 如果友元的名称是限定标识，并且在指定的类或命名空间中找到匹配的非模板函数，则友元声明指代该函数；否则，
- (1.3) 如果友元的名称是限定标识，并且在指定的类或命名空间中找到匹配的函数模板，则友元声明指代该函数模板的推导特化（13.10.3.7）；否则，
- (1.4) 该名称应为声明（或重新声明）非模板函数的未限定标识。

[示例 1：

```
template<class T> class task;
template<class T> task<T>* preempt(task<T>*);

template<class T> class task {
    friend void next_time();
    friend void process(task<T>*);
    friend task<T>* preempt<T>(task<T>*);
    template<class C> friend int func(C);

    friend class task<int>;
    template<class P> friend class frd;
};
```

此处，`task` 类模板的每个特化都将函数 `next_time` 作为友元；由于 `process` 没有显式模板实参，`task` 类模板的每个特化都将适当类型的函数 `process` 作为友元，并且该友元不是函数模板特化；由于友元 `preempt` 具有显式模板实参 `T`，`task` 类模板的每个特化都将函数模板 `preempt` 的适当特化作为友元；并且 `task` 类模板的每个特化都将函数模板 `func` 的所有特化作为友元。同样，`task` 类模板的每个特化都将类模板特化 `task<int>` 作为友元，并将类模板 `frd` 的所有特化作为友元。——示例结束]

2 友元模板可以在类或类模板中声明。友元函数模板可以在类或类模板中定义，但友元类模板不能在类或类模板中定义。在这些情况下，友元类模板或友元函数模板的所有特化都是授予友元关系的类或类模板的友元。

[示例 2：

```
class A {
    template<class T> friend class B;          // OK
    template<class T> friend void f(T){ /* ... */ }  // OK
};
```

——示例结束]

3 模板友元声明规定，该模板的所有特化——无论是隐式实例化（13.9.2）、部分特化（13.7.6）还是显式特化（13.9.4）——都是包含模板友元声明的类的友元。

[示例 3：

```
class X {
    template<class T> friend struct A;
    class Y { };
};

template<class T> struct A { X::Y ab; };          // OK
template<class T> struct A<T*> { X::Y ab; };        // OK
```

——示例结束]

## ISO/IEC 14882:2020(E)

```
template<int I>          class X<I, I, int> { };          // #2
```

```
template<int I0, int J0> void f(X<I0, J0, int>);
template<int I0>         void f(X<I0, I0, int>);          // B
```

```
template <auto v>   class Y { };
template <auto* p>   class Y<p> { };                 // #3
template <auto** pp> class Y<pp> { };                 // #4
```

```
template <auto* p0>   void g(Y<p0>);                 // C
template <auto** pp0> void g(Y<pp0>);                 // D
```

根据函数模板的排序规则，函数模板 B 比函数模板 A 更特化，函数模板 D 比函数模板 C 更特化。因此，部分特化 #2 比部分特化 #1 更特化，部分特化 #4 比部分特化 #3 更特化。——示例结束]

[示例 2：

```
template<typename T> concept C = requires (T t) { t.f(); };
template<typename T> concept D = C<T> && requires (T t) { t.f(); };
```

```
template<typename T> class S { };
template<C T> class S<T> { };   // #1
template<D T> class S<T> { };   // #2
```

```
template<C T> void f(S<T>);   // A
template<D T> void f(S<T>);   // B
```

部分特化 #2 比 #1 更特化，因为 B 比 A 更特化。——示例结束]

## 13.7.6.4 类模板特化的成员 [temp.class.spec.mfunc]

类模板部分特化的成员的模板形参列表应与该类模板部分特化的模板形参列表相匹配。类模板部分特化的成员的模板实参列表应与该类模板部分特化的模板实参列表相匹配。类模板部分特化是一个独立的模板。类模板部分特化的成员与主模板的成员无关。以需要定义的方式使用的类模板部分特化成员应被定义；主模板成员的定义永远不会作为类模板部分特化成员的定义使用。类模板部分特化成员的显式特化，应以与主模板显式特化相同的方式声明。

[示例 1：

```
// 主类模板
template<class T, int I> struct A {
    void f();
};
```

```
// 主类模板的成员
template<class T, int I> void A<T,I>::f() { }
```

```
// 类模板部分特化
template<class T> struct A<T,2> {
    void f();
    void g();
    void h();
};
```

```
// 类模板部分特化的成员
template<class T> void A<T,2>::g() { }
```

```
// 显式特化
template<> void A<char,2>::h() { }
```

```
int main() {
    A<char,0> a0;
    A<char,2> a2;
    a0.f();        // OK，使用主模板成员的定义
    a2.g();        // OK，使用部分特化成员的定义
    a2.h();        // OK，使用显式特化成员的定义
    a2.f();        // error：A<T,2> 的 f 没有定义；此处不使用主模板
}
```

——示例结束]

2 如果类模板的成员模板被部分特化，则成员模板的部分特化是外围类模板的成员模板；如果外围类模板被实例化（13.9.2、13.9.3），则在创建类模板特化的成员时，每个成员模板部分特化的声明也会作为其中一部分被实例化。如果主成员模板针对外围类模板的某个给定（隐式）特化进行了显式特化，则对于该外围类模板特化，将忽略成员模板的部分特化。如果成员模板的某个部分特化针对外围类模板的某个给定（隐式）特化进行了显式特化，则对于该外围类模板特化，仍会考虑主成员模板及其其他部分特化。

[示例 2：

```
template<class T> struct A {
    template<class T2> struct B {};
    template<class T2> struct B<T2*> {};
};

template<> template<class T2> struct A<short>::B {};

A<char>::B<int*> abc ip;    // 使用 #2
A<short>::B<int*> absip;    // 使用 #3
A<char>::B<int> abci;       // 使用 #1
```

——示例结束]

## 13.7.7 函数模板 [temp.fct]

### 13.7.7.1 一般规定 [temp.fct.general]

1 函数模板定义了一个无界的相关函数集合。

[示例 1：排序函数族可以如下声明：

```
template<class T> class Array { };
template<class T> void sort(Array<T>&);
```

——示例结束]

2 函数模板可以与其他函数模板以及非模板函数（9.3.4.6）重载。非模板函数与函数模板无关（即它永远不会被视为函数模板的特化），即使它与可能生成的函数模板特化具有相同的名称和类型。139

### 13.7.7.2 函数模板重载 [temp.over.link]

1 可以对函数模板进行重载，使两个不同的函数模板特化具有相同的类型。

[示例 1：

```
// 翻译单元 1：
template<class T>
    void f(T*);
void g(int* p) {
    f(p); // 调用 f<int>(int*)
}

// 翻译单元 2：
template<class T>
    void f(T);
void h(int* p) {
    f(p); // 调用 f<int*>(int*)
}
```

——示例结束]

139) 也就是说，非模板函数的声明并不只是引导具有相同名称的函数模板特化进行重载决议。如果程序中对这样的非模板函数进行了按定义规则使用（odr-use）（6.3），则必须对其进行定义；不会使用函数模板定义对其进行隐式实例化。

