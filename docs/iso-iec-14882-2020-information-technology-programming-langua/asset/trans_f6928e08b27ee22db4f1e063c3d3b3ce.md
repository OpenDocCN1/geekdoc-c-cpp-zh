

cv-qualifier:
    const
    volatile

ref-qualifier:
    &
    &&

declarator-id:
    ... opt id-expression

## 9.3.2 类型名称

为了显式指定类型转换，以及作为 sizeof、alignof、new 或 typeid 的参数，类型名称应当被指定。这可以通过 type-id 来完成，其语法上是一个声明该类型变量或函数的声明，但省略了实体的名称。

```
type-id:
    type-specifier-seq abstract-declaratorₒₚₜ

defining-type-id:
    defining-type-specifier-seq abstract-declaratorₒₚₜ

abstract-declarator:
    ptr-abstract-declarator
    noptr-abstract-declaratorₒₚₜ parameters-and-qualifiers trailing-return-type
    abstract-pack-declarator

ptr-abstract-declarator:
    noptr-abstract-declarator
    ptr-operator ptr-abstract-declaratorₒₚₜ

noptr-abstract-declarator:
    noptr-abstract-declaratorₒₚₜ parameters-and-qualifiers
    noptr-abstract-declaratorₒₚₜ [ constant-expressionₒₚₜ ] attribute-specifier-seqₒₚₜ
    ( ptr-abstract-declarator )

abstract-pack-declarator:
    noptr-abstract-pack-declarator
    ptr-operator abstract-pack-declarator

noptr-abstract-pack-declarator:
    noptr-abstract-pack-declarator parameters-and-qualifiers
    noptr-abstract-pack-declarator [ constant-expressionₒₚₜ ] attribute-specifier-seqₒₚₜ
    ...
```

可以唯一地识别出 abstract-declarator 中标识符出现的位置，如果该构造是一个声明中的声明符。命名的类型随后与假设的标识符的类型相同。

> [示例 1:
> 
> ```cpp
> int                 // int i
> int *               // int *pi
> int *[3]            // int *p[3]
> int (*)[3]           // int (*p3i)[3]
> int (*)()            // int *f()
> int (*)(double)      // int (*pf)(double)
> ```
> 
> 分别命名类型“int”、“指向 int 的指针”、“3 个指向 int 的指针的数组”、“指向 3 个 int 的数组的指针”、“(无参数)函数返回指向 int 的指针”，以及“指向 (double) 返回 int 的函数的指针”。——示例结束]

类型也可以通过使用 typedef（9.2.4）来命名（通常更容易）。

## 9.3.3 歧义消除

在 8.9 中提到的函数式转换与声明之间的相似性所产生的歧义，也可能出现在声明的上下文中。在该上下文中，选择是在参数名称周围具有冗余括号的函数声明与具有函数式转换作为初始化器的对象声明之间。正如 8.9 中提到的歧义的解决方式一样，解决办法是将任何与声明语法匹配的构造都视为声明。

[注意 1：可以通过在参数周围添加括号来明确消除声明的歧义。歧义可以通过使用拷贝初始化或列表初始化语法，或使用非函数式转换来避免。——注意结束]

# [示例 1:

```
struct S {
    S(int);
};

void foo(double a) {
    S w(int(a));        // function declaration
    S x(int());         // function declaration
    S y((int(a)));      // object declaration
    S y((int)a);        // object declaration
    S z = int(a);       // object declaration
}
```

——示例结束]

2 歧义可能源于函数式转换与 type-id 之间的相似性。解决办法是任何与 type-id 语法匹配的构造都被解释为 type-id。

# [示例 2:

```
template <class T> struct X {};
template <int N> struct Y {};
X<int()> a;            // type-id
X<int(1)> b;          // expression (ill-formed)
Y<int()> c;           // type-id (ill-formed)
Y<int(1)> d;          // expression

void foo(signed char a) {
    sizeof(int());            // type-id (ill-formed)
    sizeof(int(a));           // expression
    sizeof(int(unsigned(a))); // type-id (ill-formed)

    (int())+1;                // type-id (ill-formed)
    (int(a))+1;               // expression
    (int(unsigned(a)))+1;     // type-id (ill-formed)
}
```

——示例结束]

3 在 parameter-declaration-clause 中，类型名嵌套在括号中时也会产生另一种歧义。在这种情况下，选择是在指向函数的指针类型的参数声明与在 declarator-id 周围具有冗余括号的参数声明之间。解决办法是将类型名视为 simple-type-specifier 而不是 declarator-id。

# [示例 3:

```
class C {};
void f(int(C)) { }      // void f(int(*fp)(C c)) { }
                       // not: void f(int C) { }

int g(C);

void foo() {
    f(1);   // error: cannot convert 1 to function pointer
    f(g);   // OK
}
```

对于另一个示例，

```
class C {};
void h(int *(C[10]));   // void h(int *(*_fp)(C _parm[10]));
                       // not: void h(int *C[10]);
```

——示例结束]

## 9.3.4 声明符的含义 [dcl.meaning]

## 9.3.4.1 通用 [dcl.meaning.general]

1 声明符包含恰好一个 declarator-id；它命名了被声明的标识符。出现在 declarator-id 中的 unqualified-id 应当是一个 simple identifier，除了某些特殊函数的声明（11.4.5、11.4.8、11.4.7、12.6）以及模板特化或偏特化的声明（13.9）之外。当 declarator-id 被限定时，声明应当引用限定符所指的类或命名空间中先前声明的成员（或在命名空间的情况下，引用该命名空间的内联命名空间集合（9.8.2）中的元素），或其特化；该成员不得仅仅通过在被 nested-name-specifier 指定的类或命名空间的作用域中引入的 using-declaration 而引入。限定 declarator-id 的 nested-name-specifier 不得以 decltype-specifier 开始。

> [注意 1：如果限定符是全局 :: 作用域解析运算符，则 declarator-id 引用在全局命名空间作用域中声明的名称。——注意结束]

跟随在 declarator-id 之后的 optional attribute-specifier-seq 属于被声明的实体。

2 static、thread_local、extern、mutable、friend、inline、virtual、consteval 或 typedef 说明符或 explicit-specifier 直接适用于 init-declarator-list 或 member-declarator-list 中的每个 declarator-id；每个 declarator-id 指定的类型取决于 decl-specifier-seq 和其声明符。

3 因此，某个特定标识符的声明具有形式

T D

其中 T 的形式为 attribute-specifier-seq_opt decl-specifier-seq 且 D 是一个声明符。以下是确定此类声明中包含的 declarator-id 所指定的类型的递归过程。

4 首先，decl-specifier-seq 确定一个类型。在声明

T D

中，decl-specifier-seq T 确定类型 T。

> [示例 1：在声明中
> 
> int unsigned i;
> 
> 类型说明符 int unsigned 确定类型“unsigned int”（9.2.9.3）。——示例结束]

5 在声明 attribute-specifier-seq_opt T D 中，其中 D 是一个未修饰的标识符，该标识符的类型为“T”。

6 在声明 T D 中，其中 D 的形式为

( D1 )

包含的 declarator-id 的类型与声明

T D1

中包含的 declarator-id 的类型相同。括号不会改变嵌入声明符-id 的类型，但它们可以改变复杂声明符的绑定。

## 9.3.4.2 指针 [dcl.ptr]

1 在声明 T D 中，其中 D 的形式为

* attribute-specifier-seq_opt cv-qualifier-seq_opt D1

并且在声明 T D1 中标识符的类型为“derived-declarator-type-list T”，则 D 的标识符的类型为“derived-declarator-type-list cv-qualifier-seq 指向 T 的指针”。cv-qualifier 应用于指针而不是指向的对象。类似地，可选的 attribute-specifier-seq（9.12.1）属于指针而不是指向的对象。

> [示例 1：声明
> 
> const int ci = 10, *pc = &ci, *const cpc = pc, **ppc;
> int i, *p, *const cp = &i;
> 
> 声明了 ci，一个常量整数；pc，一个指向常量整数的指针；cpc，一个指向常量整数的常量指针；ppc，一个指向指向常量整数的指针的指针；i，一个整数；p，一个指向整数的指针；以及 cp，一个指向整数的常量指针。ci、cpc 和 cp 的值在初始化后不能被更改。pc 的值可以被更改，cp 指向的对象的值也可以被更改。一些正确操作的示例是
> 
> i = ci;
> *cp = ci;

