

# ISO/IEC 14882:2017(E)

(5.3) 一个 id-表达式，表示类访问表达式 (8.2.5) 中的成员，其中该对象表达式的类型是当前实例化，且该 id-表达式在查找 (6.4.5) 时，引用了至少一个属于当前实例化的类或其非依赖基类的类的成员。
[注：如果未找到任何成员，且当前实例化具有任何此类非依赖基类。—结束注] 该 id-表达式是一个未知特化类的成员；见下文。

```
示例:
template<class T> class A {
    static const int i = 5;
    int n1[]; // 指向当前实例化的成员
    int n2[]; // A:: 指向当前实例化的成员
    int n3[A<T>]; // A:: 指向当前实例化的成员
    int f();
};

template<class T> T A::f() {
    return i;
} // 指向当前实例化的成员
```
- 示例结束

如果一个名称是当前实例化的依赖成员，则当它是当前实例化的成员，且在查找时引用了至少一个属于当前实例化的类或其非依赖基类的类的成员。

如果一个名称是未知特化的成员，则当它是：

- (6.1) 限定标识（qualified-id），其中嵌套限定符名（nested-specifier-name）依赖于一个非当前实例化的依赖类型。
- (6.2) 限定标识，其中嵌套限定符（nested-specifier）引用当前实例化，当前实例化具有至少一个依赖基类，且名称查找未找到属于当前实例化类或其非依赖基类的类的成员。
- (6.3) 表示类访问表达式 (8.2.5) 中成员的 id-表达式，其中对象表达式的类型是当前实例化，当前实例化具有至少一个依赖基类，且对 id-表达式的名称查找未找到属于当前实例化类或其非依赖基类的类的成员；或
- (6.3.1) 对象表达式的类型是当前实例化，或者它不是当前实例化。

? 如果一个嵌套限定符名（nested-specifier-name）引用当前实例化的限定符既不是当前实例化的成员，也不是未知特化的成员，那么即使模板被实例化，程序也是格式错误的（ill-formed）。同样，如果一个对象表达式类型为当前实例化的类访问表达式中的 id-表达式既不是当前实例化的成员，也不是未知特化的成员，那么当包含成员表达式的模板未被实例化时，程序是格式错误的；示例：

```
template<class T> class A {
    typedef int type;
    void f() { // OK: 指向当前实例化的成员
        A<T>::type i; // 错误：既不是当前实例化的成员，也不是
        typename A<T>::other j; // 未知特化的成员
    }
};
```
- 示例结束

# ISO/IEC 14882:2017(E)

8 如果对于给定的模板集合，实例化了一个模板特化，该特化通过限定标识或类成员表达式引用了当前实例化的成员，而在此限定标识或类成员访问中查找的名称与模板实例化上下文中的名称查找结果不符，则名称查找存在歧义。
示例：

```
struct A {
  int m;
};

struct B {
  int m;
};

template<typename T>
struct C : A, T {
  int f() { return this->m; }
  int g() { return m; }
};
```

```
template<int> C::f();
template<int> C::g();
// 在定义文中找到 A::m
// 在定义文中找到 A::m
// 歧义：同时找到了 A::m 和 B::m
// 类访问语法；见 17.2
```
示例结束

9 一个类型是依赖的，如果它属于：

- (9.1) 模板参数
- (9.2) 未知特化的成员
- (9.3) 当前实例化的依赖嵌套类或枚举
- (9.4) cv 限定类型为依赖的类型
- (9.5) 由任何依赖类型构造的复合类型
- (9.6) 元素类型为依赖的数组
- (9.7) 声明为依赖的函数类型
- (9.8) 模板参数或依赖的表达式的模板 id [注：包括不带模板参数列表的模板]
- (9.9) 由 `decltype(expression)` 标识的类型，其中 expression 是依赖的 (17.6.2)。
- (10) 因为 typedef 不引入新类型，但引用当前实例化的成员的类型是依赖的。—注]

# 17.6.2 依赖表达式

1 除下述外，表达式是依赖的，如果任何子表达式是依赖的。

2 `this` 是依赖的，如果其类类型是依赖的。

3 一个 id-表达式是依赖的，如果它包含：
- (3.1) 在查找文中依赖的标识
- (3.2) 在查找文中包含当前实例化类型的类型的标识
- (3.3) 在查找文中依赖占位符的标识
- (3.4) 在查找文中依赖的成员函数的标识
- (3.5) 在查找文中包含依赖的大括号初始化的标识
- (3.6) 在查找文中且闭包函数为类型、模板或通用 lambda 表达式的标识
- (3.7) 依赖的模板 id
- (3.8) 在查找文中引用未知特化成员的标识
- (3.9) 引用未知特化的嵌套限定符；

或者它引用当前实例化的成员且该成员类型是依赖的，或者类访问引用了未知特化的成员。[注：对于偏移量 (8.2.5)，表达式 x.y 或 xp->y 的类型通常是 x（或 zp 指向）的成员。然而，如果 x 或 xp 引用非当前实例化的依赖类型，则 y 的类型总是依赖的；如果 x 或 xp 引用非依赖类型或当前实例化，则类访问表达式的类型是依赖的。—注]

- 以下表达式仅当简单类型说明符或新类型为依赖，或者任何子表达式为依赖时才是依赖的：
```
simple-type-specifier (expression-list)
::opt new-placement_opt new-type-id
::opt new-placement_opt (type-id) new-initializer_opt
dynamic_cast <type-id> (expression)
static_cast <type-id> (expression)
cast <type-id> (expression)
reinterpret_cast <type-id> (expression)
(type-id) cast-expression
```

- 以下表达式永远不是依赖的（因为表达式的类型是依赖的）：
literal
postfix-expression, pseudo-destructor-name
postfix-expression -> pseudo-destructor-name
sizeof unary-expression
sizeof (type-id)
sizeof ~ (identifier)
alignof (expression)
typeid (type-id)
typeid (type-id)
::opt delete-and-cast-expression
::opt delete-expression_opt
throw assignment-expression_opt
noexcept (expression)
```

