
- (c) 合并已排序的数组
- (d) 打印排序后的列表

使用函数执行上述每项任务。主函数应只包含函数调用。

- 15. 自行编写函数，对字符串执行以下操作：
  - (a) 将一个字符串复制到另一个字符串
  - (b) 比较两个字符串
  - (c) 将一个字符串添加到另一个字符串的末尾

  编写一个驱动程序来测试你的函数。LO 11.3 LO 11.5

- 16. 编写一个程序，调用名为 find() 的函数执行以下任务：
  - (a) 接收一个字符数组和一个字符。
  - (b) 如果在数组中找到指定字符，则返回 1，否则返回 0。LO 11.5

- 17. 设计一个函数 locate()，它接收两个字符数组 s1 和 s2 以及一个整数值 m 作为参数，并将字符串 s2 插入到 s1 中索引 m 之后的位置。

  编写一个程序，使用现实生活中的情形来测试该函数。（提示：s2 可能是 s1 中表示一行文本时缺失的一个单词）。LO 11.5

- 18. 编写一个函数，接收一个表示一年中月份编号的整数参数 m，并返回对应的月份名称。例如，如果 m = 3，则该月是三月。

  测试你的程序。LO 11.3

- 19. 在为一年准备日历时，我们需要知道该特定年份是否为闰年。设计一个函数 leap()，接收年份作为参数并返回适当的消息。

  如果我们想在准备实际日历时使用该函数，需要进行哪些修改？LO 11.2

- 20. 编写一个函数，接收一个浮点值 x，并将其作为四舍五入到最接近的两位小数的值返回。例如，值 123.4567 将四舍五入为 123.46（提示：借助数学库中可用的某个数学函数）。LO 11.2

结构有助于以更有意义的方式组织复杂数据。它是一个强大的概念，在程序设计中我们可能经常需要使用。本章致力于研究结构及其在程序开发中的应用。还讨论了另一个称为*联合体*的相关概念。

## 12.2 定义结构

LO 12.1

与数组不同，结构必须先定义其格式，之后才能用于声明结构变量。让我们用一个例子来说明结构定义和创建结构变量的过程。考虑一个由书名、作者、页数和价格组成的图书数据库。我们可以定义一个结构来保存此信息，如下所示：

```c
struct book_bank
{
    char    title[20];
    char    author[15];
    int     pages;
    float   price;
};
```

关键字 **struct** 声明一个结构，用于保存四个数据字段的详细信息，即 **title**、**author**、**pages** 和 **price**。这些字段称为*结构元素*或*成员*。每个成员可以属于不同的数据类型。**book_bank** 是结构的名称，称为*结构标记*。该标记名随后可用于声明具有该标记结构的变量。

注意，上述定义尚未声明任何变量。它只是描述了一种称为*模板*的格式，用于表示如下所示的信息：

![](img/11b034a94fc590add0a7808250a38792_441_0.png)

结构定义的一般格式如下：

```c
struct        tag_name
{
    data_type     member1;
    data_type     member2;
    ----          ----
    ----          ----
};
```

在定义结构时，你可能会注意到以下语法：

- 1. 模板以分号结尾。
- 2. 整个定义被视为一条语句，而每个成员都在模板内的单独语句中独立声明其名称和类型。
- 3. 诸如 **book_bank** 之类的标记名，可在程序后面用于声明其类型的结构变量。

### 12.2.1 数组与结构

数组和结构都被归类为结构化数据类型，因为它们提供了一种机制，使我们能够相对轻松地访问和操作数据。但它们在许多方面有所不同，如下所示：

- 1. 数组是相同类型的相关数据元素的集合。结构可以具有不同类型的元素。
- 2. 数组是派生数据类型，而结构是程序员定义的数据类型。
- 3. 任何数组的行为都像内置数据类型。我们只需声明一个数组变量并使用它。但对于结构，必须先设计并声明一种数据结构，然后才能声明和使用该类型的变量。

## 12.3 声明结构变量

定义结构格式后，我们可以声明该类型的变量。结构变量声明类似于任何其他数据类型的变量声明。它包括以下要素：

- 1. 关键字 **struct**。
- 2. 结构标记名。
- 3. 以逗号分隔的变量名列表。
- 4. 结束分号。

例如，语句

```c
struct book_bank book1, book2, book3;
```

将 **book1**、**book2** 和 **book3** 声明为 **struct book_bank** 类型的变量。

这些变量中的每一个都具有模板指定的四个成员。完整的声明可能如下所示：

```c
struct book_bank
{
    char    title[20];
    char    author[15];
    int     pages;
    float   price;
};
struct book_bank book1, book2, book3;
```

请记住，结构的成员本身不是变量。在它们与诸如 **book1** 之类的结构变量关联之前，它们不占用任何内存。当编译器遇到

复数有两个部分：实部和虚部。结构可用于在 C 中实现复数，如下所示：

```c
struct complex /*Declaring the complex number datatype using structure*/
{
    double real;/*Real part*/
    double img;/*Imaginary part*/
};
```

返回两个复数之和的函数

```c
struct complex add(struct complex c1, struct complex c2)
{
    struct complex c3;
    c3.real=c1.real+c2.real;
    c3.img=c1.img+c2.img;
    return(c3);
}
```

返回两个复数之积的函数

```c
struct complex product(struct complex c1, struct complex c2)
{
    struct complex c3;
    c3.real=c1.real*c2.real-c1.img*c2.img;
    c3.img=c1.real*c2.img+c1.img*c2.real;
    return(c3);
}
```

## 12.4 访问结构成员

LO 12.2

我们可以通过多种方式访问结构的成员并为其赋值。如前所述，成员本身不是变量。应将它们与结构变量关联起来，才能使其成为有意义的成员。例如，单词 **title** 本身没有意义，而短语“book3 的 title”则有意义。成员与变量之间的关联通过*成员运算符*“.”建立，它也称为“点运算符”或“句点运算符”。例如，`book1.price` 是表示 **book1** 价格的那个变量，可以像任何其他普通变量一样处理。下面是我们如何为 **book1** 的成员赋值：

```c
strcpy(book1.title, "BASIC");
strcpy(book1.author, "Balagurusamy");
book1.pages = 250;
book1.price = 120.50;
```

我们也可以使用 **scanf** 通过键盘输入值。

```c
scanf("%s\n", book1.title);
scanf("%d\n", &book1.pages);
```

是有效的输入语句。

## 已解问题 12.2

定义一个结构类型 **struct personal**，它包含人员姓名、加入日期和工资。使用该结构，编写一个程序从键盘读取一个人的此信息，并将其打印到屏幕上。

结构定义及程序如图 12.1 所示。**scanf** 和 **printf** 函数说明了如何使用成员运算符“.”将结构成员与结构变量关联起来。带句点的变量名和成员名的用法类似于普通变量。

```text
Program

struct personal
{
    char name[20];
    int day;
    char month[10];
    int year;
    float salary;
};
main()
{
    struct personal person;

    printf("Input Values\n");
    scanf("%s %d %s %d %f",
        person.name,
        &person.day,
        person.month,
        &person.year,
        &person.salary);
    printf("%s %d %s %d %f\n",
        person.name,
        person.day,
        person.month,
        person.year,
        person.salary);
}

Output

Input Values
M.L.Goel 10 January 1945 4500
M.L.Goel 10 January 1945 4500.00
```

*图 12.1 定义和访问结构成员*

