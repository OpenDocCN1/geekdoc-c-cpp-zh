
# ISO/IEC 14882:2011(E)

声明了三个函数模板。下标函数可能定义如下：

```cpp
template<class T> T& Array<>::operator[](int i) {
    if (i<0 || i==sz) error("Array: range error");
    return v[i];
}
```

-- 示例结束

类模板的成员函数的模板参数由调用该成员的对象的类型的模板参数决定。[示例：对于 `Array<T> : operator ()`，模板参数将由应用该操作的 `Array` 决定。]

```cpp
Array<int> v1(20);
Array<complex> v2(30);
```

```cpp
v1[3] = 7; // Array<int>::operator[]
v2[3] = dcomplex(7,8); // Array<complex>::operator()
```

## 14.5.2 类模板的成员类 [temp.mem.class]

类模板的成员可以在它的类模板定义之外定义。[注意：类成员必须在第一次第一个需要实例化的使用之前定义 (14.7.1)。例如，

```cpp
template<class T> struct A {
    class B;
    Array<int> b1;
    template<class T> class A<T> : B {
    Array<int> b2; // OK: 需要 A 已定义，但不需要 A::B
    }; // OK: 需要 A::B 已定义
```

-- 备注结束

## 14.5.3 类模板的静态数据成员 [temp.static]

静态数据成员的定义可以在包含该静态成员所属的类模板定义的命名空间作用域内。[示例：

```cpp
template<class T> class X {
    static T s;
};
template<class T> T X<T>::s = 0;
```

-- 示例结束

声明为未知边界数组的静态数据成员的显式特化，其边界（如果有的话）可以与定义不同。[示例：

```cpp
template<class T> struct A {
    static int i[];
};
template<class T> int A<T>::i[4]; // elements
template<int> int A<int>::i[] = { 1 }; // OK: 1 个元素
```

-- 示例结束

## 14.5.1.4 类模板的枚举成员

类 T 的枚举可以在类模板定义之外定义。[示例：

```cpp
template<class T> struct A {
  enum E : T;
};
A<int> a;
template<class T> enum A<T>::E { e1, e2 };
A<int>::E e = A<int>::e1;
```

-- 示例结束

## 14.5.2 成员模板

模板可以在类或类模板内部声明；此类模板被称为成员模板。成员模板可以在其类定义或模板定义内部或外部定义。对于在类定义之外定义的类的成员模板，应通过类模板的模板参数后跟成员模板的模板参数来指定。[示例：

```cpp
template<class T> struct string {
  template<class T2> int compare(const T2&);
  template<class T2> string(const T2& s) { /* ... */ };
};
template<class T> template<class T2> int string<T>::compare(const T2& s) {
```

-- 示例结束

类不应有成员模板。访问控制规则（第 11 节）适用于成员模板。析构函数不应该是成员模板。在类中可以声明具有给定名称和类型的普通（非模板）成员函数，以及同名的成员函数模板，后者可用于生成相同类型的特化。当该名称存在时，除非提供了显式参数列表，否则对该名称的使用将指向非模板成员。[示例：

```cpp
template<class T> struct A {
  void f(int);
  template<class T2> void f(T2);
};
template<> void A<int>::f(int) { // 非模板成员
template<class T> void A<int>::f(T f) { // 模板成员
```

```cpp
int main() {
  A<char> ac;
  ac.f(1); // 非模板
  ac.f('c'); // 模板
  ac.f(1); // 模板
}
```

-- 示例结束

## § 14.5.2

3 成员函数模板不应是虚函数。[示例：
```cpp
template <class T> struct AA {
    template <class C> virtual void g(C); // 错误
    virtual void f(); // OK
};
```
示例结束]:

4 成员函数模板的特化不会覆盖基类中的虚函数。[示例]：
```cpp
class B {
    virtual void f(int);
};
class D : public B {
    template <class T> void f(T); // 未覆盖 B::f(int)
    void f(int i) { B::f(i); } // 调用模板的函数
};
```
示例结束]:

5 转换模板的特化的引用方式与转换为该类型的非模板转换函数相同。[示例]：

```cpp
struct A {
    template <class T> operator T();
};
template <class T> A::operator T() { return 0; } // 特化
template <> A::operator char() { return 0; } // 实例化
int main() {
    A a;
    int *ip;
    ip = a.operator int(); // 显式调用模板
    ip = a.operator void();
}
```
[备注：显式参数列表紧跟函数名之后，由于转换函数模板是在没有函数名的情况下调用的，因此无法为这些模板提供显式参数列表。——备注结束]

6 转换模板的特化不是通过名称找到。相反，会考虑使用范围内可见的任何转换函数。对于每个运算符，如果参数推导成功 (14.8.2)，生成的特化将如同通过名称找到一样被使用。

7 类中的使用声明不能引用基类中转换模板的特化。

## 14.5.2

重载解析 (13.3.3) 和部分排序 (14.5.6.2) 用于在多个转换模板的特化版本和/或非模板转换函数之间选择最佳转换函数。

## 14.5.3 变参模板 [temp.variadic]

变参模板是一个包含多个参数的模板包。[示例：

```cpp
template<class T> struct A {
  enum E : T;
};
A<int> a;
template<class T> enum A<T>::E { e1, e2 };
A<int>::E e = A<int>::e1;
```

-- 示例结束

## 14.5.4 友元 [temp.friend]

1 类或类模板的友元可以是一个函数模板或类模板、函数模板或类模板的特化版本，或者普通的（非模板）函数或类。对于不是模板声明的友元声明：

- * 如果友元的名称是限定或未限定的模板标识（template-id），则友元声明指向函数模板的特化版本；否则
- * 如果友元的名称是限定标识（qualified-id）且在指定的类或命名空间中找到了匹配的非模板函数，则友元声明指向该函数；否则
- * 如果友元的名称是限定标识（qualified-id）且在指定的类或命名空间中找到了匹配的函数模板，则友元声明指向该函数模板的归约特化 (14.8.2.6)，否则；
- * 名称应当是一个未限定标识（unqualified-id），并声明（或重新声明）一个普通的（非模板）函数。

[Example:

```cpp
template<class T> class task;
template<class T> task<T> preempt(task<T>*);
template<class T> class task {
    friend void next_time();
    friend void process();
    friend task<T>* preempt(task<T>*);
    template<class C> friend int func(C);
    friend class<int>; template<class P> friend class fd;
};
```

在这里，task 模板的每个特化版本都将 `next_time` 函数作为友元；因为它没有显式的模板参数，task 类模板的每个特化版本都将相应类型的函数作为友元，且这不是函数模板特化；因为友元 `preempt` 具有显式模板 `<T>`，task 类模板的每个特化版本都将函数 `preempt` 的相应特化版本作为友元；task 的每个特化版本都将函数 `func`的所有特化版本作为友元。同样，task 类模板的每个特化版本都将模板特化 `task<int>` 作为友元，task 类的所有特化版本都将友元 `fd` 作为友元。 — example;

2 友元模板可以在类或类模板内部声明。友元函数模板可以在类或类模板内部定义，但友元类模板不能在类或类模板内部定义。在这些情况下，友元类或友元函数模板的所有特化版本都是授予友元权的类或类模板的友元。[Example:

```cpp
class A {
    template<class T> friend class B; // OK
    template<class T> void f(T){ /* ... } // OK
};
```]

3 模板友元声明指定该模板的所有特化版本，无论是隐式实例化的 (14.7.1)、部分特化的 (14.5.5) 还是显式特化的 (14.7.3)，都是包含该模板友元声明类的友元。[Example:

```cpp
class X {
    template<class T> friend struct A;
    class Y { };
};
template<class T> struct A {X::Y ab; }; // OK
template<class T> struct A<T> {X::Y ab; }; // OK
```
— end example ]

4 当在类模板的友元声明中定义函数时，该函数在被定义使用（od-used）时实例化。适用于非模板函数声明和定义的多次声明与定义的限制也适用于这些隐式定义。

5 类模板的成员可以被声明为非模板类的友元。在这种情况下，该类模板每个特化版本的相应成员都是授予友元权的类的友元。对于显式特化，相应的成员是与通常情况下会生成的类实例化中的成员具有相同名称（类型、函数、类模板或函数模板）、模板参数和签名的成员（如果有）。[Example:

```cpp
template<class T> struct A {
    struct B {
        void f();
        struct D {
            void g();
        };
    };
};
template<> struct A<int> {
    struct B {
        int f();
        struct D {
            void g();
        };
    };
};
class C :
template<class T> friend struct A<T>::B; // 即使它不是 A<T>::B 的特化版本，也向 A<int>::B 授予友元权
template<class T> friend void A<T>::f(); // 不向 A<int>::f() 授予友元权
// 因为它的返回类型不匹配
template<class T> friend void A<T>::D::g(); // 不向 A<int>::g() 授予友元权
// 因为 A<int>::D 不是 A<T>::D 的特化版本
};
```
— end example ]

6 [Note: 友元声明可以首先声明嵌套命名空间范围成员 (14.6.5)。 — end note]

7 友元模板不应在局部类中声明。

8 友元声明不应声明部分特化。[Example:

# § 14.5.4

© ISO/IEC 2011 – All rights reserved

# ISO/IEC 14882:2011(E)

```cpp
template<class T> class A {
}
```
