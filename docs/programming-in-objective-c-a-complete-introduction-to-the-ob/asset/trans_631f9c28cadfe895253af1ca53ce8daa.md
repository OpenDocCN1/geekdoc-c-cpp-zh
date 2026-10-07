

# 指针

指针允许你有效地表示复杂的数据结构，更改作为方法参数传递的值，并更简洁、高效地处理数组。在本章的末尾，我们还将阐述指针对于 Objective-C 语言中对象的实现是多么重要。

在第 8 章“继承”中，当我们谈到 Point 和 Rectangle 类时，我们已经引入了指针的概念，并指出你可以对同一个对象拥有多个引用。

要理解指针是如何运作的，你必须首先理解**间接性（indirection）**的概念。我们在日常生活中就能见证这一概念。例如，假设我需要为我的打印机买一个新的墨盒。在我工作的公司，采购部负责所有的购买工作。所以我会给采购部的 Jim 打电话，让他为订购新的墨盒。然后 Jim 会给当地的供应商店订购墨盒。为了得到我的新墨盒，我采取的是间接的方法，因为我……

这种间接的概念也适用于 Objective-C 中指针的工作方式。指针提供了一种访问特定数据项值的间接手段。正正如通过采购部门订购新墨盒是有道理的（例如，我不知道是从哪个具体的地点订购的），在 Objective-C 中有时使用指针也有充分的理由。

但话说了，是时候看看指针实际上是如何运作的了。假设你如下所示定义了一个变量 `count`：

```
int count = 10;
```

你可以定义另一个变量 `int intPtr`，通过以下声明可以让你间接访问 `count` 的值：

```
int *intPtr;
```

星号 `*` 告知 Objective-C 系统变量 `intPtr` 的类型是指向 `int` 的指针。这意味着程序将使用 `intPtr` 来访问一个或多个整数变量的值。

你已经在之前的程序 `scanf` 调用中见过 `&` 运算符。这个一元运算符被称为**地址运算符（address operator）**，它在 Objective-C 中创建一个指向变量的指针。所以如果 `x` 是特定类型的变量，那么表达式 `&x` 就是该变量的指针。如果你愿意，可以将表达式 `&x` 赋值给任何已声明为与 `x` 类型相同的指针变量。

因此，根据给出的 `count` 和 `intPtr` 的定义，你可以编写如下语句：

```
intPtr = &count;
```

来建立 `intPtr` 和 `count` 之间的间接引用。地址运算符赋值给变量 `intPtr` 的不是 `count` 的值，而是指向变量 `count` 的指针。

图 13.1 展示了 `intPtr` 和 `count` 之间的链接。直线表示 `intPtr` 不直接包含 `count` 的值，而是包含一个指向变量 `count` 的指针。

![](img/9a03a17dbf1900dce936c9665ab15c26_287_0.png)

图 13.1 指向整数的指针

要通过指针变量 `intPtr` 引用 `count` 的内容，你需要使用间接运算符（indirection operator），即星号 `*`。如果 `x` 被定义为 `int` 类型，语句 `x = *intPtr;` 将通过 `intPtr` 间接引用的值赋值给变量 `x`。由于 `intPtr` 之前被设置为 `count`，这条语句的效果是将变量 `count` 中包含的值（即 10）赋值给变量 `x`。程序 13.11 结合了之前的语句，并说明了两个基础指针运算符：地址运算符 (`&`）和间接运算符 (`*`）。

# 程序 13.11

```
// 用于说明指针的程序

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc init];
    int count = 10, x;
    int *intPtr;

    intPtr = &count;
    x = *intPtr;

    NSLog("@count = %i, x = %i", count, x);

    [pool drain]
    return 0;
}
```

# 程序 13.11 输出

count = 10, x = 10

变量 `count` 和 `x` 以通常方式声明为整数变量。在下一行，变量 `intPtr` 被声明为类型“指向 int 的指针”。请注意，这两行声明可以合并为一行：

```
int count = 10, x, *intPtr;
```

# 276 第 13 章 底层 C 语言特性

接下来，地址运算符被应用于变量 `count`，其效果是创建一个指向该变量的指针，程序将其赋值给变量 `intPtr`。程序中下一语句的执行：

```
x = *intPtr;
```

执行过程如下：间接运算符告诉 Objective-C 系统将变量 `intPtr` 视为包含指向另一个数据项的指针。然后使用该指针来访问所需的项，其类型由指针变量的声明指定。因为你在声明变量 `intPtr` 时告诉编译器它指向整数，所以编译器知道表达式 `*intPtr` 所引用的值是一个整数。此外，由于你在上一条语句中将 `intPtr` 设置指向整数变量 `count`，此表达式直接访问了 `count` 的值。

程序 13.12 展示了指针变量的一些有趣属性。该程序使用了一个指向字符的指针。

# 程序 13.12

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSautoreleasePool *pool = [[NSautorelease alloc] init];
    char *c = 'Q';
    char *charPtr = &c;

    NSLog("%@c %c", c, *charPtr);
    c = '/';
    NSLog("%@c %c", c, *charPtr);

    *charPtr = '(';
    NSLog("%@c %c", c, *charPtr);

    [pool drain];
    return 0;
}
```

# 程序 13.12 输出

Q Q
/\(

字符变量 `c` 被定义并初始化为字符 'Q'。在程序的下一行中，变量 `charPtr` 被定义为类型“指向 char 的指针”，这意味着在该变量内部的任何值都应被视为对字符的间接引用（指针）。注意，你可以以通常方式为该变量赋初值。你在程序中赋值给 `charPtr` 的值是指向变量 `c` 的指针，这是通过对变量 `c` 应用地址运算符得到的。（注意，如果 `c` 在此语句之后定义，那么这种初始化将产生编译器错误，因为变量在表达式引用其值之前必须先声明。）

变量 `charPtr` 的声明及其初始值的赋值可以用两个独立的语句等价表示，如下：

```
char *charPtr;
charPtr = &c;
```

（而不是通过以下语句）

```
char *charPtr;
*charPtr = &c;
```

因为在 Objective-C 中，指针的值在设置为某个值之前是没有意义的。

下一个 `NSLog` 调用显示了变量 `c` 的内容以及 `charPtr` 所引用变量的内容。因为你将 `charPtr` 设置指向变量 `c`，所以显示的值是 `c` 的内容，这正如程序输出的第一行所验证的。

在程序的下一行中，字符 `/` 被赋值给变量 `c`。由于 `charPtr` 仍然指向变量 `c`，在随后的 `NSLog` 调用中显示 `*charPtr` 正确显示了 `c` 的新值。除非 `charPtr` 的值改变，否则表达式 `*charPtr` 始终访问 `c`。因此，随着 `c` 的值的改变，`*charPtr` 的值之改变。

之前的讨论可以帮助你理解程序中后续语句是如何工作的。我们提到，除非 `charPtr` 改变，表达式 `*charPtr = '('` 将始终引用 `c` 的值。因此，在表达式

```
*charPtr = '(';
```

中，括号字符被赋值给 `c`。此外，字符 '(' 被正式赋值给 `charPtr` 所指向的变量。你知道这个变量就是 `c`，因为你在程序开头就在 `charPtr` 中放置了指向 `c` 的指针。

之前的概念是你理解指针操作的关键。如果它们仍然显得有些模糊，请在此处复习。

# 指针与结构

你已经看到过如何定义指向 `int` 或 `char` 等基本类型的指针。但你也可以定义指向结构的指针。在本章早些时候，你定义的日期结构如下所示：

```
struct date
{
  int month;
  int day;
  int year;
}
```

