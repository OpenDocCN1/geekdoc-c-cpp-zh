
# ISO/IEC 14882:2017(E)

```cpp
struct S { /* ... */ 
};

A<B> b;
// 格式错误：A 没有访问 B:: 的权限
// 示例结束;
```

当使用模板参数或默认模板参数时，模板参数列表可以为空。空的 `<>` 括号应被用作模板参数列表。[示例：`templateClass T = char String; String<*> p; // OK: String<char> String; // 语法错误 templateClass Tuple<*> t; // OK: Elements 是空的 // 语法错误 // 示例结束`]

对于类型为类模板对象的显式析构函数可以显式地指定模板参数。[示例：`template<T> struct A { ~A(); void f(A* p, A* q) { p->~A(); // OK: 调用析构函数 q->~A(); // OK: 调用析构函数 } // 示例结束`]

如果对模板参数的使用导致模板特化实例化产生了格式错误的结构，则该程序是格式错误的。

当模板标识符是一个重载函数模板时，则重载集合中的非模板函数以及重载集合中模板参数与模板参数不匹配的函数模板均被忽略。如果没有这些函数具有匹配的模板参数，则该程序是格式错误的。

当一个简单的模板参数没有名称时，当需要默认参数的值时，会隐式实例化一个默认模板参数（17.7.1）。[示例：`templatetypename T, typename U = int* struct S { }; Sbool* p; // p 的类型是 Sbool, int*`]

对于 `U` 的默认参数，在省略号处是为了包展开（17.5.3）。

### 17.3.1 模板类型参数

对于类型为类型的模板参数的模板参数是一个类型标识符。

示例：
```cpp
template <class T> class X {};
template <class T> void f(T t) {}
struct { } unnamed_obj;
void f() {
struct A {};
enum { el }; };
```

17.3.1 ©/IECIEC2017 – 保留所有权利 350

```cpp
typedef struct { } B;
B b;
X<4> x1; // OK
X<4> x2; // OK
X<B> x3; // OK
f(el1); // OK
f(unnamed_obj); // OK
f(b); // OK
```

> [注：模板类型参数可以是不完整类型（6.9）。-- 注释结束]

### 17.3.2 模板非类型参数

- 如果非模板参数的类型通过模板推导包含一个占位符类型（10.1.7.4, 17.1），则推导出的参数根据模板参数的类型通过模板推导来确定（10.1.7.4.1）。如果推导出的参数类型在模板参数声明中是不允许的（17.1），则它是格式错误的。
- 对于非类型模板参数的模板参数应当是模板参数值的经过转换的常量表达式（8.2）。对于引用或指针类型的非类型模板参数，常量表达式的值不应引用以下对象的地址：
  - 主体（4.5），
  - 临时对象（15.2），
  - 字符串字面量（5.13.5），
  - 类型表达式的结果（8.2.8），或
  - 预命名的 `__func__` 变量（11.4.1）。

> [注：如果模板参数代表一组重载函数（或指向此类函数的指针或指针成员），则从集合中选择匹配的函数（16.4）。-- 注释结束]

- [示例：
```cpp
template<const int*> ptr> struct X { /* ... */ };
int ai[];
X(ai); // 数组到指针及限定转换
struct Y {
template<const Y&> struct Z { /* ... */ };
Y y;
// 没有转换，但有额外的 cv 限定
Z(y);
template<int <span>> struct W { /* ... */ };
int b[5];
W(b); // 没有转换
void f(char);
void f(int);
template<void (*)(int)> struct A { /* ... */ };
A&f(int) a; // 选择了 f(int)
template<auto n> struct B { /* ... */ };
B<1 = b1; // OK: 模板参数类型为 int
B<'a'> = b2; // OK: 模板参数类型为 char
B<2.5> = b3; // error: 模板参数类型不能为 double
```
§ 17.3.2
©ISO/IEC 2017 - 保留所有权利 351
- 示例结束

[注：字符串字面量（5.13.5）不是可选模板参数。[示例：
```cpp
template<class T, const char*> class X { /* ... */ };
int x1, "Studebaker"; // error: 字符串字面量作为模板参数
const char* p = "Viveist";
int x2; // OK
```
]

[注：元素或非静态成员的地址不是可选模板参数。[示例：
```cpp
template<int> class X { };
struct S { int m; };
int a[10];
X<&a[0]>; // error: 元素的地址
X<&S::m>; // error: 非静态成员的地址
X<int*>; // OK: 静态成员的地址
```]

[注：当相应的模板参数具有引用类型时，临时对象不是可选模板参数。[示例：
```cpp
template<const int&> struct B { /* ... */ };
B c1;
B(1); // error: 需要临时对象
```]

### 17.3.3 模板参数

对于模板参数的模板参数应当是类模板或别名模板的名称，用 id 表达式表示。当模板参数命名一个类模板时，在将模板与相应参数进行匹配时，只考虑主类；如果其特化的参数列表与模板匹配，则不考虑这些特化。当基于模板参数的特化被实例化时，与主类或变量相关的任何特化都会被考虑在内。如果在实例化点处该特化是不可可见的，且它本应被选中，则需要进行诊断。[示例：
```cpp
template<class T> class A {
int x;
};
template<class T> class A<T*> { // 部分特化
long x;
};
```

此类类型可以取别名，例如通过 `typedef-name`。 — 尾注

## 17.5 模板声明

- 1 模板声明中，`template-id`（即 `template-name` 后接 `template-argument-list`）不应在模板声明中指定。[示例：
```cpp
template<class T1, T2> int Class&T1, T2 {}; // error
template<class T1, int> void sort(T1 data[], T1); // error
```
— [示例]:然而，这在类模板的部分特化（17.5.5）中是允许的。 — 尾注 |
- 2 为了名称查找和实例化，函数模板的默认参数和 `noexcept-specifier`，以及成员函数的默认参数和 `noexcept-specifier`被视为定义；每个默认参数或 `noexcept-specifier` 是一个独立的定义，与函数定义或任何其他默认参数或 `noexcept-specifier` 无关；`constexpr` (9.4.1) 的子语句被视为定义。
- 3 因为别名声明（`alias-declaration`）不能声明 `template-id`，所以无法对别名进行部分特化或显式特化。

## 17.5.1 类模板

- 1 类模板定义了一组无边界相关类型的布局和操作。
[示例]: 单个类模板 `List` 可能会提供一组无边界的类：对于每个类型 `T` 提供 `List<T>`，每个描述一个类型为 `T` 的元素列表。同样，描述连续动态数组的类模板 `Array` 可能会这样定义：
```cpp
template<class T>
Array {
T* v;
int sz;
public:
    explicit Array(int);
    T& operator[](int i) { return v[i]; }
};
```
前缀 `template<class T>` 指定了正在声明一个模板，并且声明中使用了类型名 `T`。换句话说，`Array` 是一个以 `T` 为参数的参数化类型。 — 示例结束 |
- 3 当成员函数、成员类、成员枚举、静态数据成员或类模板的成员在类模板之外定义时，该成员定义被定义为模板定义，其中其模板参数（`template-parameters`）是该类模板的参数。成员定义中使用的模板参数名称可能与类模板中使用的模板参数名称不同。成员定义中类模板名后的模板参数列表中的参数顺序，与模板参数列表中使用的参数顺序一致。[示例]：
```cpp
template<class T1, class T2> struct A {
void f1();
void f2();
};
template<class T2, class T1> void A<T2, T1>::f1() {} // OK
template<class T2, class T1> void A<T1, T2>::f2() {} // error
```
```cpp
template<class ... Types> struct B {
void f3();
void f4();
};
```
```cpp
template<class ... Types> void B<Types..>::f3() {} // OK
template<class ... Types> void B<Types..>::f4() {} // error
// 示例结束];
```
- 4 在类模板的重声明、部分特化、显式特化或显式实例化中，键类（key-class）的类型应与原始类模板声明一致（10.1.7.3）。

### 17.5.1.1 类模板成员函数 [temp.mem.func]

- 1 类模板的成员函数可以在其声明的类定义之外定义。[示例]：
```cpp
template<class T> class Array {
T* v;
int sz;
public:
explicit Array(int);
T operator[](int);
T elem(int i) { return v[i]; };
};
```
声明了三个函数。下标函数可能如下定义：
```cpp
template<class T> T Array<T>::operator[](int i) {
if (i < 0 || i >= sz) throw("Array");
return v[i];
}
// 示例结束];
- 2 类模板成员函数的模板参数由调用该函数的对象的模板参数决定。[示例]：
```cpp
Array<int> v1(2);
Array<complex> v2(3);
```
```
v1 = {}; // Array<int>::operator()
v2 = complex(7,8); // Array<complex>::operator()
// 示例结束];

### 17.5.1.2 类模板成员函数 [temp.mem.func]

- 1 类模板的成员函数可以在其声明的类定义之外定义。[注]：成员类必须在类第一次使用之前定义。例如：
```cpp
template<class T> struct A {
class B;
};
template<int>::B b1; // 需要定义 A
template<class T> class A<T>::B { };
b2; // 需要定义 A::B
// 注结束];

### 17.5.1.3 类模板静态数据成员

- 1 静态数据成员或静态数据成员模板的定义可以在封装该成员的类模板命名空间内提供。[示例]：
```cpp
template<class T> class X {
    static T s;
};
template<class T> X::s = 0;
struct limits {
    template<class T>
    static const T min;
};
// 示例结束
```
- 2 声明为未知数组的静态数据成员的显式特化可以与其定义不同。[示例]：
```cpp
template<class T> struct A {
    static int i[];
};
template<class T> int A<T>::i = {}; // 修正自原文
```
```
template<class T> struct A {
    static int i[];
};
// 元素结束结束
```

### 17.5.1.4 类模板枚举成员

类模板的枚举成员可以在类模板之外定义。[示例]：
```cpp
template<class T> struct A {
    enum E;
};
template<class T> enum A<T>::E { };
// 示例结束

## 17.5.2 成员模板

- 1 模板可以在类内声明；此类模板是成员模板。成员模板可以在其类定义内或外定义，使用类模板的模板参数指定。[示例]：
```cpp
template<class T> struct string {
    template <class T2> int compare(const T2&);
};
template<class T> template <class T2> int string<T>::compare(const T2&) const {
```
非闭包类型的局部类不应有成员模板。访问控制规则（第14节）适用于成员模板。析构函数不应是成员。具有给定名称的非模板成员函数（11.3.5）与相同名称的成员模板函数都可以用于生成相同类型的特化，两者均在类中声明。[示例]：
```cpp
template<class T> struct A {
    void f(int);
    template <class T2> void f(T2);
};
template<class> void A<T>::f(int) // 非模板成员
template<class> template <T> void A<T>::f(int) // 成员模板特化
int main() {
    A<char> ac;
    ac.f(1);    // 非模板
    ac.f('c');  // 模板
    ac.f(1);    // 模板
}
// 示例结束
```
- 3 成员函数模板不应该是虚函数。[示例]：
```cpp
template<class T> struct AA {
    template <class O> virtual void g(C); // error
    virtual void f();                   // OK
};
// 示例结束
```
class D : public B {
    template<class T> void f(T); // 没有重写 B::f(int)
    void f(int i) {f(i); } // 调用模板实例的覆盖函数
};
// 示例结束
```
- 4 成员函数模板的特化不重写基类的虚函数。[示例]：
```cpp
struct A {
    template <class T> operator T*();
};
```
