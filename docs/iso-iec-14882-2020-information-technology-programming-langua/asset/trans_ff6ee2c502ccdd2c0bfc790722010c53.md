

## ISO/IEC 14882:2020(E)

``` 
f(0);
f((int*)0);
g(true);
g(0);

// selects #1
// selects #2
// selects #3 because C1<bool> is not satisfied
// selects #4
```

— end example]

## 13.6 类型等价 [temp.type]

1 两个模板-id相同，如果

- (1.1) — 它们的模板名、操作符函数-id或字面量操作符-id引用同一个模板，且
- (1.2) — 它们对应的类型模板参数是相同类型，且
- (1.3) — 它们对应的非类型模板参数在转换为模板参数的类型后是模板参数等价的（见下文），且
- (1.4) — 它们对应的模板模板参数引用同一个模板。

两个相同的模板-id引用同一个类、函数或变量。

2 两个值是模板参数等价的，如果它们是相同类型且

- (2.1) — 它们是整型且其值相同，或
- (2.2) — 它们是浮点型且其值相同，或
- (2.3) — 它们是类型 std::nullptr_t，或
- (2.4) — 它们是枚举类型且其值相同，136 或
- (2.5) — 它们是指针类型且具有相同的指针值，或
- (2.6) — 它们是指向成员类型且它们引用同一个类成员或两者都是空成员指针值，或
- (2.7) — 它们是引用类型且它们引用同一个对象或函数，或
- (2.8) — 它们是数组类型且其对应元素是模板参数等价的，137 或
- (2.9) — 它们是联合类型且要么两者都没有活动成员，要么它们具有相同的活动成员且其活动成员是模板参数等价的，或
- (2.10) — 它们是类类型且其对应的直接子对象和引用成员是模板参数等价的。

3 [示例 1：

``` 
template<class E, int size> class buffer { /* ... */ };
buffer<char,2*512> x;
buffer<char,1024> y;
```

声明 x 和 y 为同一类型，且

``` 
template<class T, void(*err_fct)()> class list { /* ... */ };
list<int,&error_handler1> x1;
list<int,&error_handler2> x2;
list<int,&error_handler2> x3;
list<char,&error_handler2> x4;
```

声明 x2 和 x3 为同一类型。它们的类型与 x1 和 x4 的类型不同。

``` 
template<class T> struct X { };
template<class> struct Y { };
template<class T> using Z = Y<T>;
X<Y<int> > y;
X<Z<int> > z;
```

声明 y 和 z 为同一类型。 — end example]

4 如果表达式 e 是类型相关的（13.8.3.3），decltype(e) 表示一个唯一的依赖类型。只有当它们的表达式等价（13.7.7.2）时，这样的两个 decltype-说明符才引用同一类型。

> [注 1：然而，这种类型可以被别名，例如通过 typedef-name。 — end note]

136) 枚举器的标识不被保留。

137) 作为模板参数的数组会衰减为指针。

## 13.7 模板声明 [temp.decls]

### 13.7.1 通用 [temp.decls.general]

1 模板-id，即模板名后跟模板参数列表，不应在主模板声明的声明中指定。

[示例 1：

``` 
template<class T1, class T2, int I> class A<T1, T2, I> { };    // error
template<class T1, int I> void sort<T1, I>(T1 data[I]);    // error
```

— end example]

> [注 1：然而，此语法在类模板偏特化（13.7.6）中是允许的。 — end note]

2 对于名称查找和实例化的目的，函数模板以及类模板的成员函数的默认参数、类型约束、requires-子句（13.1）和 noexcept-说明符被视为定义；每个默认参数、类型约束、requires-子句或 noexcept-说明符都是一个单独的定义，与模板化函数定义或任何其他默认参数、类型约束、requires-子句或 noexcept-说明符无关。对于实例化的目的，constexpr if 语句（8.5.2）的子语句被视为定义。

3 因为别名声明不能声明模板-id，所以不可能对别名模板进行偏特化或显式特化。

### 13.7.2 类模板 [temp.class]

#### 13.7.2.1 通用 [temp.class.general]

1 类模板为一组相关的无界类型定义布局和操作。

2 [示例 1：可以让单个类模板 List 提供一组无界的类定义：对每个类型 T 一个类 List\<T\>，每个类描述类型 T 元素的链表。同样，可以像这样定义描述连续动态数组的类模板 Array：

``` 
template<class T> class Array {
  T* v;
  int sz;
  public:
    explicit Array(int);
    T& operator[](int);
    T& elem(int i) { return v[i]; }
};
```

前缀 template\<class T\> 指定正在声明一个模板并且类型名 T 可以在声明中使用。换句话说，Array 是一个参数化类型，T 是其参数。 — end example]

3 当类模板的成员函数、成员类、成员枚举、静态数据成员或成员模板在类模板定义之外定义时，成员定义被定义为模板定义，其中模板头等价于类模板的模板头（13.7.7.2）。在成员定义中使用的模板参数名可能与类模板定义中使用的模板参数名不同。成员定义中类模板名之后的模板参数列表必须以与成员的模板参数列表中使用的顺序相同的顺序命名参数。每个模板参数包必须在模板参数列表中使用省略号展开。

[示例 2：

``` 
template<class T1, class T2> struct A {
  void f1();
  void f2();
};

template<class T2, class T1> void A<T2,T1>::f1() { }    // OK
template<class T2, class T1> void A<T1,T2>::f2() { }    // error

template<class ... Types> struct B {
  void f3();
  void f4();
};

template<class ... Types> void B<Types ...>::f3() { }    // OK
template<class ... Types> void B<Types>::f4() { }    // error

template<typename T> concept C = true;
template<typename T> concept D = true;

template<C T> struct S {
    void f();
    void g();
    void h();
    template<D U> struct Inner;
};

template<C A> void S<A>::f() { }    // OK: template-heads match
template<typename T> void S<T>::g() { } // error: no matching declaration for S<T>

template<typename T> requires C<T>    // ill-formed, no diagnostic required: template-heads are
void S<T>::h() { }    // functionally equivalent but not equivalent

template<C X> template<D Y>
struct S<X>::Inner { };    // OK
```

— end example]

4 在类模板的重声明、偏特化、显式特化或显式实例化中，class-key 必须与原始类模板声明的种类一致（9.2.9.4）。

#### 13.7.2.2 类模板的成员函数 [temp.mem.func]

1 类模板的成员函数可以在其被声明的类模板定义之外定义。

[示例 1：

``` 
template<class T> class Array {
    T* v;
    int sz;
public:
    explicit Array(int);
    T& operator[](int);
    T& elem(int i) { return v[i]; }
};
```

声明了类模板的三个成员函数。下标函数可以这样定义：

``` 
template<class T> T& Array<T>::operator[](int i) {
    if (i<0 || sz<=i) error("Array: range error");
    return v[i];
}
```

受约束的成员函数可以脱离行定义：

``` 
template<typename T> concept C = requires {
    typename T::type;
};

template<typename T> struct S {
    void f() requires C<T>;
    void g() requires C<T>;
};

template<typename T>
    void S<T>::f() requires C<T> { }    // OK
template<typename T>
    void S<T>::g() { }    // error: no matching function in S<T>
```

— end example]

2 类模板成员函数的模板参数由调用该成员函数的对象的类型模板参数决定。

