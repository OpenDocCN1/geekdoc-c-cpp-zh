
`template <U> U(U) requires C<typename T>; // #2`

};

```cpp
template <class U> class U : int<U> requires C<U> { return u; }; // OK，实例化了 #2
```

替换 `C<typename T>` 产生无效表达式，因此实例化不匹配 `#1`。替换匹配 `#2`。示例结束

# 13.5.4 约束归一化 [temp.constr.normal]

1 表达式 `E` 的规范形式是 `E` 的规范形式，定义如下：
- (1.1) 表达式 `E` 的规范形式是 `E`
- (1.2) 表达式 `E1 || E2` 的规范形式是 `E1` 和 `E2` 的规范形式的析取 (13.5.2.2)
- (1.3) 概念-`C1 && E2` 的规范形式是 `C1` 的规范形式与 `E2` 的合取。

概念-`C1(A1, ..., An)` 的规范形式是在每个原子表达式的参数映射中用 `A1, ..., An` 替换其相应的模板参数后，其约束表达式的规范形式。如果任何替换导致无效的类型或表达式，程序是非格式的；需要诊断。

[示例 1]
```cpp
template<typename> concept A = T::value;
template<typename> concept B = A<U>;
template<typename> V concept C = B<V>;
```

# ISO/IEC 14882:2020(E)

2 获取约束表达式的范式的过程称为规范化。

> 注意 1：在确定声明的关联约束 (13.5.2) 以及评估命名为约束特化的 id-表达式的值 (7.5.4) 时，会对约束表达式进行规范化。 — 结束注释

3 [示例 2]:

```
template<T> C1 = sizeof(T) == 1;
template<T> C2 = C1 && == 2;
template<T> C3 = { template T:: };
template<T> C4 requires (T x) { ++x };
```

`#1` 的关联约束是 `sizeof(T) == 1`（映射 `T -> U`）和 `&& == 2`。
`#2` 的关联约束需要 `{ template T:: }`（映射 `T -> U`）。
`#3` 的关联约束需要 `(T x) { ++x }`（映射 `T -> U`）。 — 结束示例

# 13.5.5 按约束排序

[temp.constr.order]

1 `P` 订阅 `Q`，当且仅当，对于 `Q` 的析言标准范式¹⁰⁵ 中的每个析言子句 `Pj`，`P` 订阅每个析言子句 `Qj`，当且仅当 `P` 中存在一个原子 `Qj`。

+ (1.1) 一个析言子句 `P` 订阅一个析言子句 `Qj`，当且仅当 `P` 中存在一个原子 `Qj`，对于该 `Qj`，存在一个原子 `C` 订阅 `Qj`，

+ (1.2) 一个原子 `C` 订阅一个原子约束 `B`，当且仅当 `A` 和 `B` 使用 13.5.2 中的规则是等同的。

> [示例 1：假设 `A` 和 `B` 为约束 (13.5.2.3)。约束 `A ∧ B` 订阅 `A`，但 `A` 不订阅 `A ∧ B`。模板订阅 `A ∧ B`，但 `B` 不订阅 `A`。注意，每个约束本身。 — 结束示例]

> 注意 2：包含关系定义了约束的偏序关系。该偏序关系被用于确定：
+ (2.1) 非模板函数的最佳候选者 (12.4.4)，
+ (2.2) 非模板的地址 (12.5)，
+ (2.3) 模板类型参数的匹配 (13.4.4)，
+ (2.4) 类模板特化的偏序 (13.7.6.3) 以及
+ (2.5) 函数模板的偏序 (13.7.7.3)。
— 结束注释

3 如果满足以下条件，声明 `D1` 至少约束为 `D2`：
+ (3.1) `D1` 和 `D2` 均为约束声明，且 `D1` 的关联约束订阅 `D2` 的关联约束；或
+ (3.2) `D2` 没有关联约束。

4 当 `D1` 至少约束为 `D2` 且 `D2` 不至少约束为 `D1` 时，声明 `D1` 比约束 `D2` 更具约束。

[示例 2]:
```
template<C> void f(T); // #1
template<C> void f(T); // #2
template<T> void g(T); // #3
template<C> void g(T); // #4
```

134) 当一个约束是子句的析言，且每个子句都是原子约束的合言时，该约束处于析言标准范式。对于原子约束 `A`、`B` 和 `C`，`A ∧ (B ∨ C)` 的析言标准范式是 `(A ∧ B) ∨ (A ∧ C)`。它的析言子句是 `(A ∧ B)` 和 `(A ∧ C)`。

135) 当一个约束是子句的合言，且每个子句都是原子约束的析言时，该约束处于注入标准范式。对于原子约束 `A`、`B` 和 `C`，约束 `A ∧ (B ∨ C)` 是注入标准范式。它的注入子句是 `A` 和 `(B ∨ C)`。

© ISO/IEC 2020 – 保留所有权利

13.5.5 378

ISO/IEC 14882:2020(E)

```
f(0);
f((int)*0);
g(true);
g(0);
// 选择 #1
// 选择 #2
// 选择 #3
因为 C1<bool> 不满足
// 选择 #4
```

# 13.6 类型等价 [temp.type]

两个模板如果满足以下条件，则是相同的：
+ (1.1) 它们的模板名称、运算符函数或文字运算符引用相同的模板，且
+ (1.2) 它们对应的非类型模板参数相同，且
+ (1.3) 在转换为模板参数后，它们对应的模板参数是等价的（见下文），
+ (1.4) 它们引用相同的模板。两个模板 id 引用相同的类、函数或变量。

两个值如果具有相同的类型且满足，是等价的：
+ (2.1) 它们是整数类型且值相同，或
+ (2.2) 它们是浮点类型且值相同，或
+ (2.3) 它们是 `std::ptr`，或
+ (2.4) 它们是枚举类型且值相同，
+ (2.5) 它们是指针类型且具有相同的指针值，或
+ (2.6) 它们是成员指针类型并引用相同的类成员或空指针值，
+ (2.7) 它们是引用类型并引用相同的类对象、函数，
+ (2.8) 它们是数组类型且对应的元素是等价的⁷
+ (2.9) 它们是联合类型且要么没有成员，要么具有相同的成员且成员是等价的，或
+ (2.10) 它们是类类型且对应的直接成员和引用成员是等价的。

3 [示例]:
```
template<E, int> class buffer { ... };
buffer<char, int> x;
buffer<char, int> y;
声明 x 和 y 为相同类型，
template<T, void (*)()> class list { ... };
list<int, void (*)()> x1;
list<int, void (*)()> x2;
list<int, void (*)()> x3;
list<char, void (*)()> x4;
声明 x2 和 x3 为相同类型。它们的类型与 x1 和 x4 不同。
```
`template<class> struct X { };`
`template<class> struct Y { };`
`template<class> struct Z = Y<T>;`
`X<int> y;`
`X<int> z;`
声明 `y` 和 `z` 为相同类型。 — 结束示例

4 如果一个表达式 `e` 是类型相关的 (13.8.3)，`decltype(e)` 定义了一个唯一的依赖类型。此类 `decltype` 标识符仅在表达式等价 (13.7.7.2) 时引用该类型。

[注意 1：然而，这种类型可以被别名，例如通过 `typedef` 名称。 — 结束注释]

36 标识符的标识性不保留。

37 模板参数退变为指针。

# ISO/IEC 14882:2020(E)

# 13.7 模板声明

# 13.7.1 通用

模板 `id`，即模板名称后的模板参数列表不应在主模板声明中指定。

```
示例 1:
template<class T1, class T2, int> class A<T1, T2, int>; // 错误
template<class T1, int> void sort(T1, int data[int]); // 错误
```

结束示例

[注意：此处语法在类模板特化 (13.7.6) 中允许。] — 结束注释

2. 为了名称查找和实例化，函数模板和类模板成员的默认参数、类型约束、要求子句 (13.1) 以及 `noexcept` 标识符是被考虑的；每个默认参数、类型约束、要求子句或 `noexcept` 标识符都是一个独立的定义，与模板化函数定义或任何其他类型约束、要求子句或 `noexcept` 标识符无关。为了实例化，`const` 模板 (5.5.2) 的子语句被视为已定义。

3. 因为别名声明不能声明模板，因此无法实例化或显式特化别名模板。

# 13.7.2 类模板

# 13.7.2.1 通用

类模板定义了一组相关类型的布局和接口。

示例 2：单个类模板 `List` 可以提供一组无限制类定义：对于每个 `T` 有一个类 `List<T>`，每个类描述一个类型 `T` 元素的链表。一个描述连续动态数组的模板 `Array` 可以这样定义：

```cpp
template<class T> class Array {
T* data;
public:
  explicit Array(int);
  T& operator[](int);
  T& element(int i) { return data[i]; }
};
```

前缀 `template<class T>` 指定了模板被声明，且 type-name `T` 可以在声明中使用。换句话说，`Array` 是以 `T` 为参数的参数化类型。 — 结束示例

当成员函数、类成员、类枚举、静态数据成员或类模板的成员模板在类定义之外时，成员函数被定义为模板定义，其模板头部与类定义等效 (13.7.7.2)。在模板头部使用的成员名称可能与类定义中的模板名称不同，成员定义中的模板名称应指定的模板参数列表应与成员的模板参数列表中使用的顺序相同。每个模板参数都应展开为

示例 2：
```
template<class T1, class T2> struct A {
void f1(void);
void f2(void);
};
template<class T2, class T1> void A<T2,T1>::f1() {} // OK
template<class T2, class T1> void A<T1,T2>::f2() {} // 错误
template<class ... Types> struct B {
void f3(void);
void f4(void);
};
```

13.7.2.1

ISO/IEC 2020 – 保留所有权利

380

# ISO/IEC 14882:2020(E)

```cpp
template<class Types> void B-Types::f3() { } // OK
template<class Types> void B-Types::f4() { } // error
template<typename T> concept C = true;
template<typename T> concept D = true;
```

```cpp
template<C> struct S {
    void f();
    void g();
    void h();
};
```

```cpp
template<C A> void S<A>::f() { // OK: template-heads match
template<typename T> void S<T>::g() { // error: no matching declaration for S<T>
```

```cpp
template<typename T> requires C<T> // ill-formed, no diagnostic required: template-heads
void S<T>::h() { // functionally equivalent not equivalent
```

```cpp
template<C X> template<D Y>
struct S<X>::Inner { }; // OK
```

在类模板的重声明、部分特化、显式特特化或显式实例化中，类键（class-key）必须与原始类模板声明的类型一致（9.2.9.4）。

## 13.7.2.2 类模板的成员函数 [temp.mem.func]

类模板的成员函数可以在声明它的类模板定义外部定义。

[示例 1:]

```cpp
template<class T> class Array {
    T* v;
    int sz;
public:
    explicit Array(int);
    T& operator[](int);
    T& elem(int i) { return v[i]; };
```

声明了类模板的三个成员函数。下标函数可以这样定义：

```cpp
template<class T> T Array<T>::operator[](int i) {
    if (i < 0 || i >= sz) error("Array: range error");
    return v[i];
}
```

受约束的成员函数可以在此处定义：

```cpp
template<typename T> concept C = requires {
    typename T::type;
};
```

```cpp
template<typename T> struct S {
    void f() requires C<T>;
    void g() requires C<T>;
};
```

```cpp
template<typename T>
void S<T>::f() { // OK
template<typename T>
void S<T>::g() { // error: no matching function in S<T>
```

类模板成员函数的模板参数是由调用该成员函数的对象的模板参数决定的。

§ 13.7.2.2

©ISO/IEC 2020 – 保留所有权利

381

[示例 2：`Array<>::operator[]` 的模板参数将由应用于下标操作的 `Array` 决定。

`Array<int> v1(20);`

`Array<complex> v2(30);`

```cpp
v1[3] = 7;                               // Array<int>::operator[]
v2[3] = dcomplex(7,8);                   // Array<complex>::operator[]
// 示例结束
```

## 13.7.2.3 推导引导 (Deduction guides)

当模板名称作为推导类类型的类型说明符出现时，使用推导引导（9.2.9.7）。推导引导不会通过查找找到。相反，在执行模板参数推导（12.4.2.9）时，会考虑为类模板声明的所有推导引导。

```cpp
deduction-guide:
explicit-specifier template-name ( parameter-declaration-clause ) -> simple-template-id ;
[示例 1:
template<class T, class D = int>
struct S {
    T data;
};
template<class U>
S(U) -> S<typename U::type>;

struct A {
    using type = short;
    operator type();
}
A()); // x 的类型为 S<short, int>
 示例结束

名称限制适用于函数的参数声明（9.3.4.6）。`simple-template-id` 应当与 `template-name` 相同。推导引导应在与类模板相同的作用域内声明，且对于成员类，与类模板位于同一编译文件中声明的推导引导不具有等效的参数。

## 13.7.2.4 类模板的成员类

类模板的成员类可以在声明它的类模板定义外部定义。

```cpp

注 1：成员类必须在首次使用前定义（13.9.2）。

template<class T> struct A {

    class B;

    Array<T>::B* b; // 需要定义 A::B

};

template<class T> class A<T>::B { };

注

```

## 13.7.2.5 类模板的静态数据成员

静态成员或静态成员模板的定义可以在该类模板的命名空间内提供。

[示例 1：
template<class T> class X {
    static T s;
};
template<class T> X::s = 0;

```cpp

struct limits {

template<class T>

  static const min;

}; // 

```

```cpp

template<class T>

struct limits::min = {}; // 定义

```

作为数组定义的静态成员的显式特化可以与其定义不同。

[示例 2：
```cpp

template<class T> struct A {

  static int i[];

};

template<class T> int A<T>::i[]; // 元素

template<int> int A<int>::i = {}; // OK：1 个元素

```
// 示例结束

## 13.7.2.6 类模板的枚举 [temp.mem.enum]

类模板的枚举可以在类模板定义外部定义。

[示例 1：

```cpp

template<class T> struct A {

  enum E : T;

  A *a;

};
```
