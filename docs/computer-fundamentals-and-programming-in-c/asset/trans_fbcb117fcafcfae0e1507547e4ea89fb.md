
```c
struct date                 /* the tag */
{
    /* start of struct date template */
    int day;                    /* a member */
    int month;                  /* a member */
    int year;                   /* a member */
    float sensex;               /* a member */
}dates, today, next;            /* instances */
```

这个声明有三个结构体变量 dates、today 和 next。它们也被称为实例，持有种类和数量相似的变量，这些变量可能包含不同的值。

已经看到，结构体的实例可以在定义结构体的同时声明。例如，

```c
struct myStruct {
    int a;
    int b;
    int c;
} s1, s2;
```

在 32 位机器上，这将生成 myStruct 的两个实例：s1 占用文件的前 12 个字节（三个整数各占四个字节），myStruct 的 s2 占用接下来的 12 个字节。因此，根据成员声明，编译器可以确定所需的内存空间，并识别结构体中的不同成员。

请注意，结构体声明构造是一个模板，它向 C 编译器传达结构体如何映射到内存，并给出成员名称的细节。一个（带标签的）模板不会保留结构体的任何实例；它只是向编译器传达其含义。下面的例子对此进行了说明：

```c
struct date {
    int month;
    int day;
    int year;
};
```

这声明了一个名为 date 的新数据类型。date 结构体由三个基本数据元素组成，全部为整数类型。它不创建任何存储空间，也不能用作变量。本质上，它是一个新的数据类型关键字，就像 int 和 char 一样，现在可以用来创建变量。其他数据结构可以定义为由与 date 结构体相同的组成构成。

结构体类型和变量声明可以是局部的或全局的，取决于它们在代码中的位置，就像任何其他声明一样。结构体可以被赋值、用作形式函数参数，并作为函数值返回。此类操作会导致编译器生成加载和存储指令序列，这可能带来效率问题。特别关注程序速度的 C 程序员会避免这类做法，只使用函数指针。

与对结构体成员的操作不同，能对结构体本身执行的实际操作很少。可以正确与结构体关联的运算符只有“=”（简单赋值）和“&”（取地址）。不能使用“==”比较结构体是否相等，也不能对结构体执行算术运算。此类操作需要根据结构体成员的操作显式编写代码。

结构体成员的声明遵循与普通变量声明相同的语法。结构体成员名称应遵循与普通变量名称相同的语法。但是，同一个名称可以用于结构体标签、结构体实例和结构体成员。就结构体成员的命名而言，每个结构体定义各自独立的内存空间。

下面这些相当怪异且令人困惑的代码是完全有效的。

```c
(a) struct a                  (b) struct b
{
    int a;                     {
    int b;                         char b;
} b;                             char a;
                                 } a;
```

结构体成员可以是任何有效的数据类型，包括其他结构体、聚合类型和指针，包括指向结构体的指针和指向函数的指针。显然，结构体不能包含其自身的实例，但可以包含指向其自身实例的指针。

## 要点

- 结构体可以定义为一种用户定义的数据类型，能够保存基本数据类型的异构数据。
- 结构体只是一个类型模板，没有关联的存储。
- 结构体声明的合适位置是在程序中 `main()` 之前的全局区域。
- 不能使用“==”比较结构体是否相等，也不能对结构体执行算术运算。

## 14.2.2 访问结构体的成员

结构体的成员可以通过三种方式访问。其中一种方式是使用“.”，它被称为“点运算符”。通过点运算符将成员与结构体变量关联起来，从而访问成员。访问结构体成员的语句的一般形式如下：

```c
< structure_variable > . < member_name > ;
```

“.”（点）运算符从结构体中选择特定成员。它与 () 和 [ ] 具有相同的优先级，高于任何一元或二元运算符。与 () 和 [ ] 一样，它从左到右结合。例如，在

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_415_0.png)

```c
struct myStruct
{
    int a;
    int b;
    int c;
} s1, s2;
```

第一个成员可以通过如下构造访问：
s1.a

对于结构体的任何其他成员，访问它的构造将类似。因此，要将值 12 赋给由变量 s2 标识的结构体的成员 b，编写以下语句

```c
s2.b = 12;
```

要在屏幕上打印赋给该成员的这个值，编写以下代码。

```c
printf("%d", s2.b);
```

类似地，在前面的示例中，结构体 s2 的成员 b 的行为将完全像 int 类型的普通变量，尽管它被表示为
s2.b

现在，考虑如下给出的结构体。

```c
struct personal_data
{
    char name[100];
    char address[200];
    int year_of_birth;
    int month_of_birth;
    int day_of_birth;
};
```

而结构体变量 monish、venkat 和 naresh 的声明语句如下

```c
struct personal_data monish, venkat, naresh;
```

要输入 monish 的地址，使用以下代码。

```c
scanf("%s", monish.address);
```

结构体 personal_data 的成员 address 将完全像普通的 char 数组一样行为。然而，它被表示为 monish.address。

在下面的示例中，将年份 1982 赋给类型为 struct personal_data 的结构体变量 monish 的 year_of_birth 成员。类似地，将月份 5 赋给 month_of_birth 成员，将日期 4 赋给 day_of_birth 成员。以下语句展示了向属于结构体变量 monish 的成员变量赋值。

```c
monish.year_of_birth = 1982;
monish.month_of_birth = 5;
monish.day_of_birth = 4;
```

因此，结构体的每个成员都可以像普通变量一样使用，但它的名称会稍长一些。因此，“点”是一个将成员与结构体分开的运算符。这只是访问结构体中任何成员的方式之一。另外两种方式将在后续章节中描述。

## 14.2.3 结构体的初始化

结构体的初始化方式与任何其他数据类型大致相同。这包括向结构体的成员分配一些常量。程序员未显式初始化的结构体，默认由系统初始化。对于整数和浮点数据类型成员，默认值为零。对于 char 和字符串类型成员，默认值为‘\0’。

初始化结构体的一般构造可以是如下两种形式中的任意一种：

```c
struct <structure_tag_name>
{
    <data_type member_name1>;
    <data_type member_name2>;
} <structure_variable1> = {constant1, constant2, . . .};
or
struct <structure_tag_name> <structure_variable>
    = {constant1, constant2, . . .};
```

以下是一些使用这两种初始化形式的示例。

### 示例

- 5. 使用第一种构造初始化结构体。

```c
#include <stdio.h>
struct tablets
{
    int count;
    float average_weight;
    int m_date, m_month, m_year;
    int ex_date, ex_month, ex_year;
} batch1={2000,25.3,07,11,2004};

int main()
{
    ...
```

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_415_1.png)
