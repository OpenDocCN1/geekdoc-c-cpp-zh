

联合的定义形式与结构定义相同，只是用关键字 union 代替关键字 struct。例如，下面的声明创建了一个名为 val 的联合变量：

```
union
{
    char key;
    int num;
    double price;
} val;
```

如果 val 是一个结构，它将由三个成员组成。然而作为一个联合，val 包含一个单一的成员，该成员可以是名为 key 的字符变量、名为 num 的整数变量，或名为 price 的双精度变量。实际上，联合为其最大成员的数据类型预留了足够多的内存位置。然后根据当前存储在预留位置中的值的类型，通过不同的变量名引用这一组位置。每个存储的值都会覆盖前一个值，使用预留内存区域中所需的字节数。

联合成员的引用方式与结构成员相同。例如，如果 val 联合当前用于存储一个字符，则访问存储字符的正确变量名是 val.key。类似地，如果联合用于存储一个整数，则通过名称 val.num 访问该值，双精度值则通过名称 val.price 访问。在使用联合成员时，程序员有责任确保为联合中当前存储的数据类型使用正确的成员名。

通常，使用第二个变量来跟踪联合中当前存储的数据类型。例如，以下代码可用于选择 val 的适当成员进行显示。uType 变量中的值决定了 val 联合中当前存储的数据类型：

```
switch(uType)
{
    case 'c': cout << val.key;
        break;
    case 'i': cout << val.num;
        break;
    case 'd': cout << val.price;
        break;
    default : cout << "Invalid type in uType : " << uType;
}
```

与结构类似，可以将数据类型与联合关联。例如，声明

```
union DateTime
{
    int days;
    double time;
};
```

提供了一种联合数据类型，而并未实际为其预留任何存储位置。然后可以使用该数据类型定义任意数量的变量。例如，定义

```
DateTime first, second, *pt;
```

创建了一个名为 first 的联合变量、一个名为 second 的联合变量，以及一个可用于存储任何具有 DateTime 形式的联合地址的指针。在声明了指向联合的指针之后，可以使用访问结构成员的相同记法来访问联合成员。例如，如果进行赋值 pt = &first;，则 pt->date 引用名为 first 的联合的 date 成员。

联合可以是结构的成员或数组的成员，结构、数组和指针也可以是联合的成员。在每种情况下，用于访问成员的记法必须与所使用的嵌套一致。例如，在由以下内容定义的<|message|>

```
struct
{
    char uType;
    union
    {
        char *text;
        float rate;
    } uTax;
} flag;
```

变量 rate 的引用方式为

```
flag.uTax.rate
```

类似地，存储在指针 text 中的地址的字符串的第一个字符引用如下：

```
*flag.uTax.text
```

## EXERCISES 16.5

- 1. (Practice) 假设已做出以下定义：

```
union
{
    double rate;
    double taxes;
    int num;
} flag;
```

对于此联合，编写 cout 语句以显示联合的成员。
- 2. **(Practice)** 定义一个名为 `car` 的联合变量，其中包含一个名为 `year` 的整数、一个名为 `name` 的 10 个字符的数组，以及一个名为 `model` 的 10 个字符的数组。
- 3. **(Practice)** 定义一个名为 `factors` 的联合变量，允许通过变量名 `watts` 和 `power` 引用一个双精度数。
- 4. **(Practice)** 定义一个名为 `Amt` 的联合数据类型，其中包含一个名为 `intAmt` 的整数变量、一个名为 `dblAmt` 的双精度变量，以及一个指向字符变量的指针名为 `ptKey`。
- 5. **(Desk check)** a. 你认为以下代码段会显示什么？

```cpp
union
{
    char ch;
    double btype;
} alt;
alt.ch = 'y';
cout << alt.btype;
```

b. 将练习 5a 中的代码包含在一个程序中，并运行程序以验证你对练习 5a 的答案。

## 16.6 Common Programming Errors

在使用结构或联合时常犯的三个常见错误：

- 1. 结构和联合作为完整实体，不能在关系表达式中使用。例如，即使 `TeleType` 和 `PhoneType` 是相同类型的两个结构，表达式 `TeleType == PhoneType` 也是无效的。当然，如果结构或联合的成员是相同数据类型，可以使用 C++ 的任何关系运算符进行比较。
- 2. 当指针用于“指向”一个结构或一个联合，或是结构或联合的成员时，要注意使用指针中的地址来访问正确的数据类型。如果对指针指向的内容感到困惑，请记住：“有疑问，就打印出来。”
- 3. 因为联合一次只能存储其一个成员，所以必须小心跟踪当前存储的变量。在联合中存储一种数据类型却用错误变量名访问它，可能会导致特别难以定位的错误。

## 16.7 Chapter Summary

- 1. 结构允许在同一个变量名下对变量进行分组。结构中的每个变量都通过其结构变量名、后跟一个点以及其变量名来访问。数据结构的另一个术语是记录。声明结构变量的一种形式如下：
```
struct
{
    // member declarations in here
} structureName;
```

- 2. 可以通过使用以下声明形式从结构创建命名数据类型：
```
struct DataType
{
    // member declarations in here
};
```
然后可以将结构变量定义为此 DataType。按照惯例，DataType 名称的首字母始终大写。

- 3. 结构作为数组元素特别有用。以这种方式使用时，每个结构都成为记录列表中的一条记录。

- 4. 完整的结构可以用作函数参数，在这种情况下，被调用函数接收结构中每个元素的副本。结构地址也可以作为引用或指针传递，这使被调用函数可以直接访问该结构。

- 5. 结构成员可以是任何有效的 C++ 数据类型，包括其他结构、联合、数组和指针。当指针作为结构成员包含时，可以创建链表。该列表使用一个结构中的指针“指向”列表中下一个逻辑结构。

- 6. 联合的声明方式与结构相同。联合的定义创建了一个内存覆盖区域，每个联合成员都使用相同的内存存储位置。因此，联合中一次只能有一个成员处于活动状态。

## Table A.1 Summary of C++ Operators (continued)

| Operator | Description | Associativity |
|---|---|---|
| ++ | Increment | Right to left |
| -- | Decrement |  |
| - | Unary minus |  |
| ! | Logical negation |  |
| ~ | One's complement |  |
| (type) | Type conversion (cast) |  |
| sizeof | Storage size |  |
| & | Address of |  |
| * | Indirection |  |
| * | Multiplication | Left to right |
| / | Division |  |
| % | Modulus (remainder) |  |
| + | Addition | Left to right |
| - | Subtraction |  |
| << | Left shift | Left to right |
| >> | Right shift |  |
| < | Less than | Left to right |
| <= | Less than or equal to |  |
| > | Greater than |  |
| >= | Greater than or equal to |  |
| == | Equal to | Left to right |
| != | Not equal to |  |
| & | Bitwise AND | Left to right |
| ^ | Bitwise exclusive OR | Left to right |
| | | Bitwise inclusive OR | Left to right |
| && | Logical AND | Left to right |
| || | Logical OR | Left to right |
| ?: | Conditional expression | Right to left |
| = | Assignment | Right to left |
| += -= *= | Assignment |  |
| /= %= &= | Assignment |  |
| ^= |= | Assignment |  |
| <<= >>= | Assignment |  |
| , | Comma | Left to right |

