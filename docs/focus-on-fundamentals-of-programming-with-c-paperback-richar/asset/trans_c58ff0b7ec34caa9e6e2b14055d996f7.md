

- 结构体简介
- 操作整个结构体
- 结构体示例：今天的日期和明天的日期
- 结构体数组
- 嵌套结构体
- 结构体作业
- 数据库实验

## 结构体简介

我们之前已使用数组来存储同一类型（且指定大小）的数据集合，并使用单个名称：

```
int num[10];
```

![](img/0603fdf2eefeabaf26542250cc2fb439_419_0.png)

我们学习了如何使用下标（如 num[1] 或 num[i]）来引用数组的单个元素。

![](img/0603fdf2eefeabaf26542250cc2fb439_419_1.png)

通常，我们需要创建不同类型的相关数据集合。例如，如果我想收集学生信息，可能会关注以下信息：

- 学生姓名（字符串）
- 学生绩点（double）
- 学生预计毕业年份（整数）

我们可以在 C 中使用名为 struct 的数据类型来建模此类集合。结构体是用户定义数据类型的示例，即我们可以定义自己的结构体来建模想要的任何数据。

## ...

例如：

```
typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;
```

这充当创建名为 Student 的新数据类型的蓝图或模板。此新用户定义数据类型 Student 可用于声明变量，就像任何内置数据类型一样：

```
// struct1.c

typedef struct {
   char name[30];
   double gpa;
   int year;
} Student;

int main(void) {
   Student s1, s2, s3;
   ...
   return 0;
}
```

我们上面的声明创建了三个 Student 类型的变量：s1、s2 和 s3。这些变量中的每一个现在在内存中都有用于存储字符串、double 和 int 的空间。请注意，我们新数据类型的名称以大写字母开头。虽然不是必须的，但遵循此规则是个好习惯。

还要注意，结构体在 main() 之外的全局作用域中声明。这允许结构体对程序的所有部分可见。如果结构体仅在 main() 内声明，那么它将局部于 main() 且仅在 main() 内可见。

## 引用结构体的元素

结构体可以如下描述：

| name | gpa | year |
|---|---|---|
| Sammie | 3.85 | 2016 |

我们现在与结构体有与数组相同的问题。如何引用结构体的单个元素（称为组件或字段）？对于数组，我们使用下标。对于结构体，我们使用句点，也称为直接组件选择运算符（或者更简单地说，简称选择运算符）。

例如，我们可以如下为 `struct` 的每个字段赋值：

```c
// struct2.c
s1.gpa = 3.85;
s1.year = 2016;
strcpy(s1.name, "Sammie");
```

## 示例：日期结构体

假设我们需要跟踪各种日期。我们可以如下定义 Date 数据类型：

```c
// struct3.c
typedef struct {
    int month;
    int day;
    int year;
} Date;
```

一旦定义了 `Date` 数据类型，我们就可以如下创建 `Date` 变量：

```
// struct4.c
typedef struct {
    int month;
    int day;
    int year;
} Date;

int main(void) {
    Date yesterday, today, tomorrow, appointment, birthday;
    ...
    return 0;
}
```

## 结构体初始化

结构体初始化与数组初始化类似，只是被初始化的数据类型对每个成员可能不同。例如：

```
// struct5.c
Date birthday = { 8, 23, 96 };
```

请注意，括号内列出的元素由逗号分隔。如果初始化器少于成员，则其余成员将初始化为零。

## 操作整个结构体

整个结构体可以被操作，但方式有限。

- 一种类型的 `struct` 可以赋值给同一类型的 `struct`。
- `struct` 可以按值或按引用传递给函数。
- `struct` 可以从函数返回（使用 return 语句）。

请记住，但是，你不能做诸如显示整个 `struct` 或将数据读入整个 `struct` 之类的事情，除非使用函数来完成工作。

## 赋值结构体

结构体可以在表达式中如下赋值：

```
// struct6.c
typedef struct {
    int month;
    int day;
    int year;
} Date;

int main(void) {
    Date today, appt;

    today.month = 5;
    today.day = 27;
    today.year = 2013;

    appt = today;
    ...
    return 0;
}
```

语句：

```
appt = today;
```

等效于以下三条语句：

```
appt.month = today.month;
appt.day = today.day;
appt.year = today.year;
```

## 按值将结构体传递给函数

结构体也可以作为函数参数传递，并作为函数值返回。当结构体作为函数参数时，它们按值传递。会创建结构体的局部副本，所有更改都针对局部副本。（请注意，这意味着可以通过将数组作为结构体成员来按值传递数组。）

```
// struct7.c

#include <stdio.h>

typedef struct {
    int month;
    int day;
    int year;
} Date;

void foo(Date now);

int main( void ) {
    Date today = { 5, 27, 2013 };
    foo(today);
    return 0;
}

void foo(Date now) {
    printf("month = %d day = %d year = %d\n", now.month,
           now.day, now.year);
}
```

## 按引用将结构体传递给函数

结构体也可以按引用传递给函数。因此，对在传递给该函数的函数中所做的结构体的任何更改都将反映回调用函数。

```
// struct8.c

#include <stdio.h>

typedef struct {
    int month;
    int day;
    int year;
} Date;

void foo(Date *now);

int main(void) {
    Date today = { 5, 27, 2013 };
    printf("month = %d day = %d year = %d\n", today.month,
           today.day, today.year);
    foo(&today);
    printf("month = %d day = %d year = %d\n", today.month,
           today.day, today.year);

    return 0;
}

void foo(Date *now) {
    (*now).month = 7;
    (*now).day = 29;
    (*now).year = 2014;
}
```

以下是输出示例：

```
month = 5 day = 27 year = 2013
month = 7 day = 29 year = 2014
```

请注意，如果 `struct` 按引用传递，则必须使用解引用运算符 `*` 来访问每个字段中的值。因为选择运算符（句点）的优先级高于解引用运算符，所以必须在结构体名称和解引用运算符周围使用括号。

但是，将选择运算符（句点）与括号一起使用变得非常笨拙，因此 C 专门为此目的添加了一个新的、更简单的运算符。它被称为箭头运算符，由连字符和大于号组成：->

我们可以将上面示例中的函数重写如下：

```c
// struct9.c
void foo(Date *now) {
    now->month = 7;
    now->day = 29;
    now->year = 2014;
}
```

因此，选择运算符（ . ）用于访问 `struct` 的成员，而箭头运算符（ -> ）用于访问由指针引用的 `struct` 的成员。

## 结构体示例：今天的日期和明天的日期

让我们构建一个程序，接受今天的日期作为输入并输出明天的日期。我们可以为程序的控制流开发一个通用算法，如下所示：

```
Input todays date.
Calculate tomorrow's date.
Output today's date.
Output tomorrow's date.
```

由于我们的程序将处理日期，因此将日期的概念建模到程序中似乎很自然，方法是创建一个名为 Date 的新数据类型，这将允许我们创建多个 Date 结构体。

```
// date1.c
typedef struct {
	int month;
	int day;
	int year;
} Date;
```

我们上面的算法现在成为 main() 函数的代码：

```
// date2.c
int main(void) {
	Date today, tomorrow;
	getTodaysDate(&today);
	getTomorrowsDate(today, &tomorrow);
	printf("Today: ");
	outputDate(today);
	printf("Tomorrow: ");
	outputDate(tomorrow);
	return 0;
}
```

