

# ISO/IEC 9899:2011 (E)

# 语义

5 **typedef** 限定符仅为了语法上的方便而被称为“存储类限定符”；它在 6.7.8 中进行了讨论。各种链接和存储生存期的含义已在 6.2.2 和 6.2.4 中讨论过。

6 对具有存储类限定符 **register** 的对象的标识符进行声明，建议对该对象的访问尽可能快。这种建议的有效程度取决于具体实现。¹²¹

7 对具有块作用域的函数的标识符进行声明除 **extern** 外，不应有显式的存储类限定符。

8 如果用非 **typedef** 的存储类限定符声明聚合对象或联合体对象，则存储类限定符产生的属性（链接除外）也适用于对象的成员，并对任何聚合或联合体成员对象递归地进行此处理。

**前向引用**：类型定义 (6.7.8)。

> 121) 实现可以将任何 **register** 声明简单地视为 **auto** 声明。然而，无论实际上是否使用了可寻址存储空间，对于用存储类限定符 **register** 声明的对象的任何部分，都无法显式地（通过 6.5.3.2 中讨论的使用 **&** 运算符）或隐式地（通过 6.2.1 中讨论将数组名转换为指针）计算地址。因此，可以应用于用存储类限定符声明的数组的唯一运算符是 **sizeof**。

110

语言

§6.7.1

## 6.7.2 类型限定符

语法

+ 1 类型限定符:
    void
    char
    short
    int
    long
    float
    double
    signed
    unsigned
    _Bool
    _Complex
    atomic-type-specifier
    struct-or-union-specifier
    enum-specifier
    typedef-name

### 2 约束

+ 2 约束 在每个声明的声明限定符中，以及每个结构体声明和类型名中的限定符-限定符列表中，应至少给出一个类型限定符。每个类型限定符列表应为以下子集之一（当每个项目有多个多集时，用逗号分隔）；类型限定符可以任何顺序出现，并可能与其他声明限定符混合出现。

+ — void
— char
— signed char
— unsigned char
— short, signed short, short int, or signed short int
— unsigned short, or unsigned short int
— int, signed, or signed int
— unsigned, or unsigned int
— long, signed long, long int, or signed long int
— unsigned long, or unsigned long int

§6.7.2 语言 111

+ - long long, signed long long, long long int, or signed long long int
- unsigned long long, or unsigned long long int
- float
- double
- long double
- _Bool
- float _Complex
- double _Complex
- long double _Complex
- atomic type specifier
- struct or union specifier
- enum specifier
- typedef name

如果实现不支持复合类型，则不应使用类型限定符 _Complex（见 6.10.8.3）。

# 语义

结构体、联合体、名称和原子类型的限定符在 6.7.2.1 至 6.7.2.4 中进行了讨论。typedef 名称的声明在 6.7.8 中进行了讨论。其他类型的特征在 6.7.2.5 中进行了讨论。

每个逗号分隔的多集指定相同的类型，但位域除外，struct int 指定与 signed int 相同的类型还是指定 unsigned int 类型取决于具体实现。

前向引用：原子类型限定符 (6.7.2.4)、枚举限定符 (6.7.2.2)、结构体和联合体限定符 (6.7.2.1)、标记 (6.7.2.3)、类型定义 (6.7.8)。

## 6.7.2.1 结构体和联合体限定符

# 语法

```
struct-or-union-specifier:
  struct-or-union identifier_opt { struct-declaration-list }
  struct-or-union identifier
```

```
struct-or-union;
struct
union
struct-declaration-list:
struct-declaration
struct-declaration-list struct-declaration
struct-declaration:
specifier-qualifier-list struct-declarator-list_opt ;
static_assert-declaration
specifier-qualifier-list:
type-specifier specifier-list_opt
type-qualifier specifier-qualifier-list_opt
struct-declarator-list:
struct-declarator
struct-declarator-list , struct-declarator
struct-declarator:
declarator
declaratoropt : constant-expression
```

# # 约束

+ 2 不声明匿名结构体或匿名联合体的 A-声明应包含一个 struct-declarator-list。

+ 3 结构体或联合体不应包含不类型或函数类型的成员（因此，结构体不包含自身的实例，但具有多个命名成员的结构体的最后一个成员可以是不完全类型；此类结构体（以及任何可能递归包含此类结构体成员的联合体）不应是结构体的成员或数组的元素）。

+ 4 指定位域宽度的表达式是一个整数常量表达式，其值为非负，且不超过在核心和表达式产生时将指定的类型对象的宽度¹¹²²。如果值为零，则声明不应有声明符。

+ 5 位域的类型是 _Bool、signed int、unsigned int 或其他取决于实现的类型的限定或未限定版本。是否允许原子取决于具体实现。

> 122 虽然 _Bool 对象的位数至少为 CHAR_BIT，但 _Bool 的宽度（符号位和数值位）可能仅为 1。

# 语义

如 6.2.5 所示，结构体是由序列组成的类型，而联合体可以重叠。`struct` 和 `union` 关键字分别指示指定的类型是结构体类型或联合体类型。

在 struct-or-union-specifier 中存在 struct-declaration-list 在翻译单元内声明了一个新的。struct-declaration-list 是结构体或联合体成员的声明序列。在列表之后类型是不完整的。

如 6.7.2 所示，如果实际类型为 int 或定义为 int 的 typedef-name，则位域是符号还是无符号取决于具体实现。

位域被解释为具有指定位数的符号或无符号类型。如果在类型 _Bool 的非零位域中存储 0 或 1，位域的值应与值比较；_Bool 具有 _Bool 的语义。

实现可以分配任何可寻址存储单元来存放位域。如果空间足够，结构中紧随另一个位域的位域应打包在同一个单元的相邻位中。如果空间不足，位域是进入下一个单元还是重叠相邻单元取决于具体实现。单元内位域分配顺序（高位到低位或低位到高位）取决于具体实现。可寻址存储单元的对齐未指定。

没有声明符但只有冒号和宽度的位域声明表示未命名位域。在特殊情况下，位域的宽度为 0

> 123 结构体或联合体不能包含变修改类型成员，成员名称在 6.2.3 中不是普通标识符。

> 124 一元运算符 &（取地址）不能应用于位域对象；因此，不存在指向位域数组的指针。

> 125 如 6.7.2 所示，如果实际类型为 int 或定义为 int 的 typedef-name，则位域是符号还是无符号取决于具体实现。

> 126 未命名位域结构体成员有助于符合外部施加的布局。

114

# 语言

# 6.7.2.1

