

# ISO/IEC 14882:2017(E)

```cpp
};
template<class T> struct A { X::Y ab; }; // OK
template<class T> struct A<T> { X::Y ab; }; // OK
// 结束
```

类模板的成员可以被声明为非模板类的友。在这种情况下，主类的每个特化版本以及类模板部分特化版本的相应成员都是授予友元关系的类的类的友。对于显式特化版本和部分特化版本的特化版本，相应的成员是与在其他情况下会生成的类模板实例化中的成员具有相同名称、种类（类型、函数、类模板或函数模板）、模板参数和签名的成员（如果有的话）。[示例：

```cpp
template<typename T> struct A {
struct B {
void f();
struct D {
void g();
};
};
template<> struct A<int> {
struct B {
int f();
struct D {
void g();
};
};
```

```cpp
class C {
template<class T> friend struct A<T>::B; // 授予 A<int>::B 友元，即使
template<class T> friend void A<T>::f(); // 它不是 A<T>::B 的特化版本
template<class T> friend void A<T>::D::g(); // 因为它的返回类型不匹配
template<class T> friend void A<T>::D::g(); // 没有授予 A<int>::g() 友元
// 因为 A<int>::D 不是 A<T>::D 的特化版本
};
// 结束示例
```

[注：友元声明可以声明命名空间域内的成员 (17.6.5)。—— 结束注]

友元模板不应在局部类中声明。

友元声明不应声明部分特化。[示例：

```cpp
template<class T> class A {
class X {
template<class T> friend class A<T*>; // 错误
};
// 结束示例
```

当友元声明引用函数模板的特化版本时，函数参数声明不应包含默认参数，不应在此类声明中使用。

# ISO/IEC 14882:2017(E)

## 17.5.5 类模板特化

主模板声明是指类模板名称为标识符的声明。类模板名称为 `simple-template-id`（简单模板标识）的模板声明是名为 `simple-template-id` 的类的部分特化。类模板的部分特化提供了模板的另一种备用定义，当特化版本中的参数与部分特化中的参数匹配时，将使用该定义替代主定义。主模板应在该模板的任何特化版本之前声明。在没有发生诊断的每个编译单元中，部分特化版本应在第一次使用作为显式或隐式实例化结果而使用该部分特化的类模板特化版本之前声明；

- 每个类部分特化版本都是一个不同的模板，并应为该模板部分特化版本中的成员提供定义 (17.5.5.3)。

[示例]

```cpp
template< T1, T2 > class A {
};
template< T1, T2 > class A<class T*, I> {
};
template< T1, T2 > class A<int*, T2, I> {
};
template< T1, T2 > class A<int, T2, S> {
};
```

第一个声明声明了（未指定的）模板。第二个及随后的声明声明了主模板的特化版本。

参数在紧随模板名称的括号列表中进行指定。对于部分特化版本，参数列表显式地写在类模板名称之后。具体而言，模板参数的顺序是它们在模板参数列表中出现的顺序。具体而言，[示例：上述示例中主模板的参数列表为 `<T1, T2, I>`。][注：主模板中不应指定模板参数列表。例如：

```cpp
template<class T1, T2, I>
class A<T1, T2, I> {}; // 错误
```

- 类部分特化版本可以在可以在声明主模板的任何作用域中声明 (10.3.1, 12.2, 17.5.2)。[示例：

```cpp
template<class T> struct A {
struct C {
    template<class T2> struct B {};
    template<class T2> struct B<T2> {}; // 部分特化 #1
};
// 部分特化
template<class T> template<class T2>
struct A<T>::C<T2> {}; // #2
A<int>::C<int> b; // 使用 #2
```

部分声明不通过查找找到。相反，当使用主模板名称时，会考虑之前声明的主模板的任何特化版本。其结果之一是引用类模板的 `using-declaration`（使用声明）不会限制通过该 `using-declaration` 可能找到的特化版本集。[示例：

```cpp
namespace N {
    template<class T1, class T2> class A {}; // 主模板
}
using N::A; // 引用主模板
namespace N {
    template<class T> class A<T, T> {}; // 部分特化
}
A<int, int> a; // 使用部分特化版本，它引用主模板
    // 结束示例]
```

- 7 如果一个非类型参数是非类型参数的名称，则它是未特化化的。所有其他非类型参数都是特化化的。

- 8 在类模板特化版本的参数列表中，适用以下限制：
(8.1) 与非类型参数对应的模板类型不应依赖特化版本的参数。[示例：

```cpp
    template<class T, T> struct C {};
    template<class T> struct C<T> {}; // 错误

    template<int X, int (*array)[X]> class A {
    int array;
    };
    template<int X> {}; // 错误
    // 结束示例
```
(8.2) 特化版本应优于主模板 (17.5.2)。
(8.3) 模板参数列表不应包含默认值。
(8.4) 参数不应包含包。如果一个参数是展开的 (17.5.3)，它应是最后一个参数。

## 17.5.5.1 类模板特化的匹配

当类模板在需要类模板实例化的文中中使用时，需要通过主模板或其特化版本来确定实例化，这是通过匹配特化版本的模板参数列表完成的。

- (1.1) 如果恰好找到一个特化版本，则从该特化版本进行实例化。
- (1.2) 如果找到了多个特化版本，则通过特化版本的顺序 (17.5.5.2) 来确定哪一个特化版本优于其他。如果一个特化版本优于其他，则实例化是歧义的。
- (1.3) 如果没有匹配项，则从主模板进行实例化。

- 2 如果特化版本的参数是从主模板推导出来的，程序是错误的。[示例：

```cpp
template<int, I> struct A {}; // #1
template<int> struct A<I> {}; // #2
template<int, I> struct A<int> {}; // #3
template<int, I> struct A<int, I> {}; // #4
A<int, I> a1; // 使用 #1
A<int, int> a2; // 使用 #2, I 是 int
A<int, int> a3; // 使用 #3, I 是 int
A<int, int> a4; // 使用 #4, 是 int
A<int, int> a5; // 歧义： #3 和 #5
```
// 结束示例
```

- 3 如果特化版本是因为模板的结构推导出来的，程序是错误的。[示例：

```cpp
template<int, I> struct A {};
template<int> struct A<I> {}; // 错误
template<int> struct A<CI> {}; // 正确
```
// 结束示例]

- 4 在引用类特化版本（例如类模板、int, I）的类型中，特化的模板参数是从主模板推导出来的。

## 17.5.5.2 类模板特化的排序

- 1 对于类部分特化版本，如果返回两个函数，则根据函数模板的排序规则 (17.5.6.2)，第一个模板优于第二个：
(1.1) 这两个函数中的每个参数都与相应的部分特化版本相同。
(1.2) 每个函数都有一个类型为类模板特化的函数，其模板参数是部分特化版本简单模板标识的模板参数列表中的对应模板参数。

- 2 [示例：

```cpp
template<int, int, class T> class X {};
template<int, int> class X<XI, int> {}; // #1
template<int> class X<CI, I> {}; // #2
template<int, IO> void f(X<IO, IO, int>); // /A
template<int, IO> void f(X<IO, IO, int>); // /B
template<class T> class Y {};
template<class* p> class Y<class* p>; // #3
template<class** pp> class Y<class** pp>; // #4
template<class* p0> void g(Y<class* p0>); // /C
template<class** pp0> void g(Y<class** pp0>); // /D
```

根据函数模板的排序规则，函数 B 优于函数模板 A，函数模板 D 优于函数 C。

