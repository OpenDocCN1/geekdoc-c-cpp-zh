

# ISO/IEC 14882:2020(E)

7 已声明但未定义的类名可以在extern声明中使用。这样的声明只能以不要求完整类类型的方式使用。

[示例2：

```
struct S;
extern S a;
extern S f();
extern void g(S);

void h() {
    g(a);        // error: S is incomplete
    f();         // error: S is incomplete
}
```

— 结束示例]

8 mutable说明符只能出现在非静态数据成员（11.4）的声明中，该成员的类型既不是const限定类型也不是引用类型。

[示例3：

```
class X {
    mutable const int* p;    // OK
    mutable int* const q;    // error
};
```

— 结束示例]

> 9 [注4：类数据成员上的mutable说明符会使应用于包含该类成员的对象上的const说明符失效，并允许修改该mutable类成员，即使对象的其余部分是const的。(6.8.4, 9.2.9.2) — 结束注]

## 9.2.3 函数说明符 [dcl.fct.spec]

1 函数说明符只能用于函数声明中。

```
function-specifier:
    virtual
    explicit-specifier

explicit-specifier:
    explicit ( constant-expression )
    explicit
```

2 virtual说明符只能用于非静态成员函数的初始声明中；参见11.7.3。

3 explicit-specifier只能用于类定义中构造函数或转换函数的声明；参见11.4.8.2和11.4.8.3。

4 在explicit-specifier中，如果提供了constant-expression，它必须是bool类型（7.7）的按语境转换的常量表达式。没有常量表达式的explicit-specifier explicit等价于explicit(true)。如果常量表达式求值为true，则该函数是显式的。否则，该函数不是显式的。位于explicit之后的(记号将被解析为explicit-specifier的一部分。

## 9.2.4 typedef说明符 [dcl.typedef]

1 包含decl-specifier typedef的声明所声明的标识符，可随后用于命名基本（6.8.2）或复合（6.8.3）类型。typedef说明符在decl-specifier-seq中不得与除defining-type-specifier之外的任何其他种类的说明符组合，并且不得用于参数声明（9.3.4.6）的decl-specifier-seq中，也不得用于函数定义（9.5）的decl-specifier-seq中。如果typedef说明符出现在没有声明符的声明中，则程序非良构。

```
typedef-name:
    identifier
    simple-template-id
```

使用typedef说明符声明的名称成为typedef名称。typedef名称命名与标识符（9.3）或simple-template-id（13.1）关联的类型；因此，typedef名称是另一类型的同义词。typedef名称不会像类声明（11.3）或枚举声明（9.7.1）那样引入新类型。

[示例1：在
typedef int MILES, *KLICKSP;
之后，构造
MILES distance;
extern KLICKSP metricp;
都是正确的声明；distance的类型是int，metricp的类型是“指向int的指针”。— 结束示例]

2 typedef名称也可以通过别名声明引入。using关键字后的标识符成为typedef名称，该标识符后的可选attribute-specifier-seq从属于该typedef名称。这样的typedef名称具有如同由typedef说明符引入的语义。特别是，它不定义新类型。

[示例2：

```
using handler_t = void (*)(int);
extern handler_t ignore;
extern void (*ignore)(int);    // redeclar e ignore
using cell = pair<void*, cell*>;    // error
```

— 结束示例]

如果别名声明是模板声明的声明，则defining-type-id的defining-type-specifier-seq不得定义类或枚举。

3 在给定的非类作用域中，typedef说明符可用于重新声明在该作用域中声明的任何类型的名称，以引用它已经引用的类型。

[示例3：

```
typedef struct s { /* ... */ } s;
typedef int I;
typedef int I;
typedef I I;
```

— 结束示例]

4 在给定的类作用域中，typedef说明符可用于重新声明该作用域中声明的、同时不是typedef名称的任何类名，以引用它已经引用的类型。

[示例4：

```
struct S {
    typedef struct A { } A;    // OK
    typedef struct B B;    // OK
    typedef A A;    // error
};
```

— 结束示例]

5 如果typedef说明符用于在给定作用域中重新声明可通过elaborated-type-specifier引用的实体，则该实体可以继续通过elaborated-type-specifier引用，或分别在枚举或类定义中作为枚举名或类名引用。

[示例5：

```
struct S;
typedef struct S S;
int main() {
    struct S* p;    // OK
}
struct S { };    // OK
```

— 结束示例]

6 在给定作用域中，typedef说明符不得用于重新声明该作用域中声明的任何类型的名称，以引用不同的类型。

[示例6：

```
class complex { /* ... */ };
typedef int complex;    // error: redefinition
```

— 结束示例]

7 类似地，在给定作用域中，不得声明与在该作用域中声明的、引用除类或枚举本身之外的类型的typedef名称同名的类或枚举。

[*示例7：*]

```cpp
typedef int complex;
class complex { /* ... */ };    // error: redefinition
```

— *结束示例*

8 simple-template-id仅当其template-name命名别名模板或模板模板参数时才是typedef名称。

> [*注1：*命名类模板特化的simple-template-id是类名（11.3）。如果typedef名称用于标识elaborated-type-specifier（9.2.9.4）、类定义（第11条）、构造函数声明（11.4.5）或析构函数声明（11.4.7）的主题，则程序非良构。— *结束注*]

[*示例8：*]

```cpp
struct S {
    S();
    ~S();
};

typedef struct S T;

S a = T();                         // OK
struct T * p;                      // error
```

— *结束示例*

9 如果typedef声明定义了未命名类或枚举，则该声明声明的第一个为该类型的typedef名称仅用于链接（linkage）目的（6.6）来表示该类型。

> [*注2：*涉及lambda表达式的typedef声明本身并不定义相关联的闭包类型，因此该闭包类型在链接目的上没有名称。— *结束注*]

[*示例9：*]

```cpp
typedef struct { } *ps, S;       // S is the class name for linkage purposes
typedef decltype([]{}) C;         // the closure type has no name for linkage purposes
```

— *结束示例*

10 具有用于链接目的的typedef名称的未命名类不得

- (10.1) — 声明除非静态数据成员、成员枚举或成员类之外的任何成员，
- (10.2) — 拥有任何基类或默认成员初始化器，或
- (10.3) — 包含lambda表达式，

并且所有成员类也应满足这些要求（递归地）。

[*示例10：*]

```cpp
typedef struct {
    int f() {}
} X;                              // error: struct with typedef name for linkage has member functions
```

— *结束示例*

## 9.2.5 friend说明符

friend说明符用于指定对类成员的访问权限；参见11.9.4。

## 9.2.6 constexpr和consteval说明符

constexpr说明符只能应用于变量或变量模板的定义，或函数或函数模板的声明。consteval说明符只能应用于函数或函数模板的声明。使用constexpr或consteval说明符声明的函数或静态数据成员隐式地是内联函数或内联变量（9.2.8）。如果函数或函数模板的任何声明具有constexpr或consteval说明符，则其所有声明都应当包含相同的说明符。

> [*注1：*显式特化可以在constexpr或consteval说明符方面与模板声明不同。— *结束注*]

