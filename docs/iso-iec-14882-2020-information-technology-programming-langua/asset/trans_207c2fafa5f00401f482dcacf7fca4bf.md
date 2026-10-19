

2 类声明将类名引入到其声明所在的作用域中，并隐藏外围作用域（6.4）中该名称的任何类、变量、函数或其他声明。如果类名在与同名变量、函数或枚举量相同的作用域中声明，则当两个声明都在作用域内时，该类只能使用 elaborated-type-specifier（6.5.5）来引用。

[示例2：

```cpp
struct stat {
    // ...
};

stat gstat;                // use plain stat to define variable

int stat(struct stat*);    // redeclare stat as function

void f() {
    struct stat* ps;       // struct prefix needed to name struct stat
    stat(ps);              // call stat()
}
```

— 结束示例]

3 仅由 class-key identifier; 组成的声明，要么是当前作用域中名称的重新声明，要么是将该标识符作为类名的前向声明。它将类名引入当前作用域。

[示例3：

```cpp
struct s { int a; };

void g() {
    struct s;              // hide global struct s with a block-scope declaration
    s* p;                  // refer to local struct s
    struct s { char* p; }; // define local struct s
    struct s;              // redeclaration, has no effect
}
```

— 结束示例]

[注记1：这样的声明允许定义相互引用的类。

[示例4：

```cpp
class Vector;

class Matrix {
    // ...
    friend Vector operator*(const Matrix&, const Vector&);
};

class Vector {
    // ...
    friend Vector operator*(const Matrix&, const Vector&);
};
```

友元的声明在11.9.4中描述，运算符函数在12.6中描述。— 结束示例]

— 结束注记]

4 [注记2：elaborated-type-specifier（9.2.9.4）也可以作为声明的一部分用作 type-specifier。它与类声明的区别在于，如果带有详细名称的类在作用域内，则该详细名称将引用它。— 结束注记]

[示例5：

```cpp
struct s { int a; };

void g(int s) {
    struct s* p = new struct s;  // global s
    p->a = s;                    // parameter s
}
```

— 结束示例]

5 [注记3：类名的声明在类定义或 elaborated-type-specifier 中看到标识符后立即生效。例如，

```cpp
class A * A;
```

首先指定 A 为一个类的名称，然后将其重新定义为指向该类对象的指针的名称。这意味着必须使用详细形式 class A 来引用该类。这种名称上的技巧可能会引起混淆，最好避免使用。— 结束注记]

6 如果 simple-template-id 的 template-name 命名的是一个类模板，那么它才是 class-name。

## 11.4 类成员 [class.mem]

### 11.4.1 一般规定 [class.mem.general]

```text
member-specification:
  member-declaration member-specificationopt
  access-specifier : member-specificationopt

member-declaration:
  attribute-specifier-seqopt decl-specifier-seqopt member-declarator-listopt ;
  function-definition
  using-declaration
  using-enum-declaration
  static_assert-declaration
  template-declaration
  explicit-specialization
  deduction-guide
  alias-declaration
  opaque-enum-declaration
  empty-declaration

member-declarator-list:
  member-declarator
  member-declarator-list , member-declarator

member-declarator:
  declarator virt-specifier-seqopt pure-specifieropt
  declarator requires-clause
  declarator brace-or-equal-initializeropt
  identifieropt attribute-specifier-seqopt : constant-expression brace-or-equal-initializeropt

virt-specifier-seq:
  virt-specifier
  virt-specifier-seq virt-specifier

virt-specifier:
  override
  final

pure-specifier:
  = 0
```

1 类定义中的 member-specification 声明了类的完整成员集合；任何成员都不能在其他地方添加。类 X 的直接成员是在 X 的 member-specification 中首次声明的 X 的成员，包括匿名联合对象（11.5.2）及其直接成员。类的成员包括数据成员、成员函数（11.4.2）、嵌套类型、枚举量、成员模板（13.7.3）及其特化。

[注记1：静态数据成员模板的特化是静态数据成员。成员函数模板的特化是成员函数。成员类模板的特化是嵌套类。— 结束注记]

2 如果 member-declaration 是以下情况，则不声明类的新成员：

- (2.1) — 友元声明（11.9.4），
- (2.2) — static_assert 声明，
- (2.3) — using 声明（9.9），或
- (2.4) — 空声明。

对于任何其他 member-declaration，每个声明的实体如果不是未命名位域（11.4.10），都是类的成员，并且每个这样的 member-declaration 要么声明至少一个类的成员名，要么声明至少一个未命名位域。

3 数据成员是由 member-declarator 引入的非函数成员。成员函数是作为函数的成员。嵌套类型是在类中声明的类（11.3, 11.4.11）和枚举（9.7.1），以及通过 typedef 声明（9.2.4）或 alias-declaration 声明为成员的任意类型。在类中定义的无作用域枚举（9.7.1）的枚举量是类的成员。

4 数据成员或成员函数可以在其 member-declaration 中声明为 static，在这种情况下，它是类的静态成员（见11.4.9）（分别为静态数据成员（11.4.9.3）或静态成员函数（11.4.9.2））。任何其他数据成员或成员函数都是非静态成员（分别为非静态数据成员或非静态成员函数（11.4.3））。

[注记2：非引用类型的非静态数据成员是类对象（6.7.2）的成员子对象。— 结束注记]

5 在 member-specification 中，成员不得声明两次，除非：

- (5.1) — 嵌套类或成员类模板可以先声明，然后再定义，且
- (5.2) — 枚举可以通过 opaque-enum-declaration 引入，之后再用 enum-specifier 重新声明。

[注记3：一个名称可以表示多个成员函数，只要它们的类型有足够的不同（12.2）。— 结束注记]

6 类的完整类上下文（complete-class context）是类 member-specification 内的以下之一：

- (6.1) — 函数体（9.5.1），
- (6.2) — 默认实参（9.3.4.7），
- (6.3) — noexcept 说明符（14.5），或
- (6.4) — 默认成员初始化器。

[注记4：如果嵌套类定义在外围类的 member-specification 内，则嵌套类的完整类上下文也是任何外围类的完整类上下文。— 结束注记]

7 在 class-specifier 的右花括号 } 处，类被认为是完全定义的对象类型（6.8）（或完整类型）。在类的完整类上下文内，该类被视为完整类型；否则，在其自身的类 member-specification 内被视为不完整类型。

8 在 member-declarator 中，紧随 declarator 之后的 = 被解释为引入 pure-specifier，如果 declarator-id 具有函数类型；否则，它被解释为引入 brace-or-equal-initializer。

[示例1：

```cpp
struct S {
    using T = void();
    T * p = 0;      // OK: brace-or-equal-initializer
    virtual T f = 0;  // OK: pure-specifier
};
```

— 结束示例]

9 在位域的 member-declarator 中，constant-expression 被解析为与 constant-expression 语法匹配的最长记号序列。

[示例2：

```cpp
int a;
const int b = 0;
struct S {
    int x1 : 8 = 42;               // OK, "= 42" is brace-or-equal-initializer
    int x2 : 8 { 42 };             // OK, "{ 42 }" is brace-or-equal-initializer
    int y1 : true ? 8 : a = 42;    // OK, brace-or-equal-initializer is absent
    int y2 : true ? 8 : b = 42;    // error: cannot assign to const int
    int y3 : (true ? 8 : b) = 42;  // OK, "= 42" is brace-or-equal-initializer
    int z : 1 || new int { 0 };    // OK, brace-or-equal-initializer is absent
};
```

— 结束示例]

