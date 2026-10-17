
```objc
    @autoreleasepool {

        struct date {

            int month;

            int day;

            int year;

        }

        struct date today;

        today.month = 9;

        today.day = 25;

        today.year = 2011;

        NSLog ("@Today's date is %i/%i/%.2i.",

        today.month,

        today.day, today.year % 100);

    }

    return 0;

}
```

# 程序 13.10 输出

今天的日期是 9/25/11。

`main` 内部的第一条语句定义了名为 `date` 的结构，它包含三个整数成员，称为 `month`、`day` 和 `year`。在第二条语句中，变量 `today` 被声明为 `date` 类型。因此，第一条语句只是定义了 Objective-C 编译器看来 `date` 结构是什么子的，并没有在计算机内部保留任何存储。第二条语句声明一个变量为 `struct date` 类型，因此确实为存储结构变量 `today` 的三个整数成员预留了内存。

赋值后，适当的 `NSLog` 调用显示了结构内部包含的值。`today.year` 除以 100 的余数在传递给 `NSLog` 函数之前计算，因此年份只显示 11。`NSLog` 调用中的 `%.2i` 格式字符指定了至少显示两个字符，从而强制显示年份前的导零。

在表达式表达式求值时，结构成员遵循与 Objective-C 语言中普通变量相同的规则。整数结构成员除以另一个整数形成整数除法，如下所示：

```
century = today.year / 100 + 1;
```

假设你想写一个简单的程序，接受今天的日期作为输入并向用户显示明天的日期。一看，这似乎是一个非常简单的任务。你可以要求用户输入今天的日期，然后通过以下语句计算明天的日期并显示给用户：

```
tomorrow.month = today.month;
tomorrow.day = today.day + 1;
tomorrow.year = today.year;
```

当然，如果 `today.day` 是 31，你可能需要处理进位：

```
if ( tomorrow.day > 31 ) {
    tomorrow.day = 1;
    tomorrow.month = today.month + 1;
    if ( tomorrow.month > 12 ) {
        tomorrow.month = 1;
        tomorrow.year = today.year + 1;
    }
}
```

当然，这只是假设每个月都有 31 天。在实际应用中，逻辑会更复杂。

```c
struct CGRect {
    CGPoint origin;
    CGSize size;
};
typedef struct CGRect CGRect;
```

这些 `typedef` 提供了一种方便的变量声明方式，而无需使用 `struct` 关键字。`CGFloat` 只是基本浮点数类型的别名。如果你想声明一个 `CGPoint` 变量并将其 `x` 成员设置为 100，将 `y` 成员设置为 200，你可以编写以下代码序列：

```
CGPoint startPt;
startPt.x = 100;
startPt.y = 200;
```

记住 `startPt` 是一个结构体而不是对象（一个很好的标志是变量名前通常没有星号 `*`）。Apple 还提供了用于创建 `CGRect`、`CGSize` 和 `CGRect` 结构的便利函数。例如：

```
CGPoint startPt = CGPointMake(100.0, 200.0);
```

还有 `CGSizeMake` 和 `CGRectMake` 函数，它们执行的任务正如名称所示。

现在，假设你想定义一个新的矩形，并将其尺寸设置为 200 x 100。你可以通过这种方式指定其尺寸：

```
CGSize rectSize;
```

```
rectSize.width = 200;
rectSize.height = 100;
```

或者你可以像这样使用 `CGSizeMake` 函数：

```
CGSize rectSize = CGSizeMake (200.0, 100.0);
```

现在，让我们创建一个具有指定尺寸和原点的矩形：

```
CGRect theFrame;
```

```
theFrame.origin = startPt;
theFrame.size = rectSize;
```

（我们在这里不会展示 `CGRectMake` 函数的使用。）

假设稍后你想获取矩形的宽度（可能它已经改变了？）。你可以通过编写此表达式来实现：

```
theFrame.size.width
```

要将其宽度更改为 175，你可以写道：

```
theFrame.size.width = 175;
```

最后，要将矩形的原点设置为 (0,0)，这些语句就能解决问题：

```
theFrame.origin.x = 0.0;
theFrame.origin.y = 0.0;
```

这些只是使用这些结构体的一些例子。正如所指出的，你可能会在应用程序中频繁使用它们。

### 关于结构体的额外细节

我们应该提到，在定义结构体时具有灵活性。首先，你可以在定义结构体的同时声明一个特定结构体类型的变量。你只需要在结构体定义的末尾分号之前包含变量名（名）即可。例如，以下语句定义了结构体 `date`，并声明了 `todaysDate` 和 `purchaseDate` 变量为该类型：

```
struct date
  int month;
  int day;
  int year;
} todaysDate, purchaseDate;
```

你可以按照正常方式为变量分配初始值。因此，以下语句定义了结构体 `date` 以及具有如文所示初始值的变量 `todaysDate`：

```
struct date
  int month;
  int day;
  int year;
} todaysDate = { 9, 25, 2011 } ;
```

如果某个特定结构体类型的所有变量在定义结构体时都已经定义，你可以省略结构体名称。因此，以下语句定义了一个名为 `dates` 的数组，包含 100 个元素：

```
struct
  int month;
  int day;
  int year;
} dates[100];
```

每个元素都是一个包含三个整数成员（month、day 和 year）的结构体。由于你没有为结构体提供名称，后续声明相同类型变量的唯一就是显式地再次定义该结构体。

## 不要忘记面向对象编程！

现在你知道如何定义一个结构体来存储日期，并且你编写了各种操作该日期结构的例程。但是面向对象编程呢？你不应该创建一个 `Date` 类，然后开发方法来处理 `Date` 对象吗？那样难道不是更好的方法吗？是的，确实。希望在我们讨论程序中的日期时，这个想法已经进入了你的脑海。

当然，如果你需要在程序中处理大量日期，定义一个类和处理日期的方法是更好的方法。事实上，`Foundation` 框架有两个名为 `NSDate` 和 `NSCalendarDate` 的类，是为此类目的定义的。我们将此留作一项练习练习，让你实现一个 `Date` 类，以对象而不是结构体的方式来处理日期。

## 指针

指针让你能够有效地表示复杂的数据结构，更改作为函数和方法参数传递的值，并更简洁、高效地处理数组。在本章的最后，我们还将向你介绍它们对于 Objective-C 语言中对象的实现有多么重要。

在第 8 章“继承”中，当我们谈到 `Point` 和 `Rectangle` 类时，我们引入了指针的概念，并指出你可以对同一个对象有多个引用。

要理解指针的操作方式，你必须首先理解**间接性**（indirection）的概念。我们在日常生活中就能看到这一概念。例如，假设我需要为我的打印机买一个新的墨盒。在我工作的公司里，采购部门处理所有购买。所以我会给采购部的 Jim 打电话，让他为我订购新墨盒。然后 Jim 会给本地供应商店订购墨盒。为了得到我的新墨盒，我采用的是间接的方法，因为我不会直接从供应商店订购墨盒。

这种间接性的概念也适用于指针。

```
x = *intPtr;
```

执行过程如下：间接操作符告诉 Objective-C 系统将变量 `intPtr` 视为指向另一个数据项的指针。该指针随后被用于访问所需的数据项，其类型由指针变量的声明指定。由于你于声明变量时已告诉编译器 `intPtr` 指向整数，因此编译器知道表达式 `*intPtr` 所引用的值是一个整数。此外，由于你在上一个程序语句中将 `intPtr` 设置为指向整数变量 `count`，因此该表达式间接地访问了 `count` 的值。

程序 13.12 演示了指针变量的一些有趣属性。该程序使用了指向字符的指针。

# 程序 13.12

```c
#import <Foundation/Foundation.h>
int main (int argc, char * argv[])
{
    @autoreleasepool {
        char c = 'Q';
        char *charPtr = &c;
        NSLog ("@"%c %c", c, *charPtr);
        c = '/';
        NSLog ("@"%c %c", c, *charPtr);
        *charPtr = '(';
        NSLog ("@"%c %c", c, *charPtr);
    }
    return 0;
}
```

# 程序 13.12 输出

Q Q
/ /
( (

字符变量 `c` 被定义并初始化为字符 'Q'。在程序的下一行中，变量 `charPtr` 被定义为类型“指向字符的指针”，这意味着存储在该变量中的任何值都应被视为对字符的间接引用（指针）。请注意，你可以以正常方式为该变量赋一个初始值。你在程序中赋给 `charPtr` 的值是指向变量 `c` 的指针，该值通过对变量 `c` 应用地址操作符得到的。（注意，如果 `c` 在此语句之后才定义，那么这种初始化将产生编译器错误，因为变量在表达式中引用其值之前必须先声明。）

变量 `charPtr` 的声明及其初始值的赋值可以等价地通过两个独立的语句表达，如下

```c
char *charPtr;
charPtr = &c;
```

（而不是通过单行声明可能暗示的语句

```c
*charPtr;
*charPtr = &c;
```

记住，在 Objective-C 中，指针的值在被设置为指向某些内容之前是没有意义的。

第一个 `NSLog` 调用简单地显示了变量 `c` 的内容以及 `charPtr` 所引用变量的内容。由于你将 `charPtr` 设置指向变量 `c`，显示的值就是 `c` 的内容，这通过程序输出的第一行证实了这一点。

在程序的下一行中，字符 '/' 被赋值给字符变量 `c`。由于 `charPtr` 仍然指向 `c`，在随后的 `NSLog` 调用中显示 `*charPtr` 的值将正确地在终端显示 `c` 的这个新值。这是一个重要的概念。除非 `charPtr` 的值发生，否则表达式 `*charPtr` 始终访问 `c` 的值。因此，随着 `c` 的值变化，`*charPtr` 的值也发生变化。

之前的讨论可以帮助你理解下一个程序中出现的语句是如何工作的。我们提到过，除非 `charPtr` 改变，否则表达式 `*charPtr` 将始终引用 `c` 的值。因此，在表达式

```c
*charPtr = '(';
```

中，左括号字符被赋值给 `c`。更正式地说，字符 '(' 被赋值给 `charPtr` 所指向的变量。你知道这个变量是 `c`，因为你在程序开始就在 `charPtr` 中放置了指向 `c` 的指针。

之前的概念是理解指针操作的关键。如果现在这些概念仍然显得有些模糊，请回顾它们。

### 指针与结构体

你已经看到如何定义一个指向 `int` 或 `char` 等基本数据类型的指针。但你也可以定义一个指向结构的指针。在本章前面的部分，你如下定义了日期结构：

```c
struct date
{
  int month;
  int day;
  int year;
};
```

就像你定义类型为 `struct date` 的变量一样，如下

```c
struct date todaysDate;
```

你也可以定义一个指向 `struct date` 变量的指针变量：

```c
struct date *datePtr;
```

然后你就可以按照预期方式使用刚刚定义的变量 `datePtr`。例如，你可以通过以下赋值语句将其设置为指向 `todaysDate`：

```c
datePtr = &todaysDate;
```

在此类赋值后，你可以通过以下方式间接访问 `datePtr` 所指向的日期结构中的任何成员：

```c
(*datePtr).day = 21;
```

该语句将 `datePtr` 指向的日期结构的“天”设置为 21。需要括号是因为结构体成员运算符点 (`.`) 的优先级高于间接操作符星号 (`*`)。

为了测试 `datePtr` 指向的日期结构中存储的 `month` 值，你可以使用如下语句：

```c
if ( (*datePtr).month == 12 )
```

指向结构的指针使用非常频繁，因此语言提供了一个特殊的操作符。结构指针操作符 `->`（一个连字符后跟大于号）允许将原本应写为

```c
(*x).y
```
的表达式更清晰地表达为

```c
x->y
```

详细学习程序 13.14。它通过一个简单的示例说明了在 Objective-C 中处理指针时的关键概念。

### 指针与数组

如果你有一个名为 `values` 的包含100个整数的数组，你可以定义一个名为 `valuesPtr` 的指针，可以使用以下语句访问该数组中包含的整数：

```
int *valuesPtr;
```

当你定义一个将用于指向数组元素的指针时，你不需要将指针指定为“指向数组的指针”类型；相反，你将指针指定为指向数组中包含的元素类型。

如果你有一个名为 `fracts` 的 `Fraction` 对象数组，你可以类似地通过以下语句定义一个指针，用于指向 `fracts` 中的元素：

```
Fraction **fractsPtr;
```

要将 `valuesPtr` 设置为 `values` 数组的第一个元素，你只需要写：

```
valuesPtr = values;
```

在这种情况下不使用地址操作符，因为 Objective-C 编译器将不带下标的数组名视为该数组第一个元素的指针。因此，简单地指定不带下标的 `values` 就会产生一个指向 `values` 第一个元素的指针。

产生指向 `values` 起点的指针的等方法是对数组的第一个元素应用地址操作符。因此，语句

```
valuesPtr = &values[0];
```

具有相同的目的，即将指向 `values` 第一个元素的指针存放在指针变量 `valuesPtr` 中。

要显示 `fractsPtr` 指向的 `fracts` 数组中的 `Fraction` 对象，你会写下这条语句：

使用指针指向数组的真正威力在遍历数组元素时显现出来。如果 `valuesPtr` 如前所述被定义，并被设置为指向 `values` 的第一个元素，你可以使用表达式

```
*valuesPtr
```

来访问 `values` 数组的第一个整数——即 `values[0]`。要通过 `valuesPtr` 变量引用 `values[3]`，你可以给 `valuesPtr` 加上 3，然后应用间接操作符：

```
*(valuesPtr + 3)
```

通常情况下，你可以使用表达式

```
*(valuesPtr + i)
```

来访问 `values[i]` 中包含的值。

所以，要将 `values[10]` 设置为 27，你会写以下表达式：

```
values[10] = 27;
```

或者，使用 `valuesPtr`，你会写：

```
*(valuesPtr + 10) = 27;
```

要将 `valuesPtr` 设置为指向 `values` 数组的第二个元素，你对 `values[1]` 应用地址操作符并将结果赋值给 `valuesPtr`：

```
valuesPtr = &values[1];
```

如果 `valuesPtr` 指向 `values[0]`，你可以通过简单给 `valuesPtr` 的值加 1 来使其指向 `values[1]`：

```
valuesPtr += 1;
```

这在 Objective-C 中是一个完全有效的表达式，可以用于任何数据类型的指针。

通常，如果 `a` 是类型为 `x` 的元素数组，`px` 是“指向 x 的指针”类型，且 `i` 和 `n` 是整数常量变量，语句

```
px = a;
```

将 `px` 设置为指向 `a` 的第一个元素，而表达式语句

```
*(px + i);
```

随后引用 `a[i]` 中包含的值。此外，语句

```
px += n;
```
