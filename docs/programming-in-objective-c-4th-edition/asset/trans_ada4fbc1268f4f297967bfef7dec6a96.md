

```
block int foo = 10;
```

运行程序，你将得到以下两行输出：

```
foo = 15
foo = 20
```

第一行显示 `foo` 的值现在是调用该块时的值。第二行验证了该块能够将 `foo` 的值改为 20。

到这里我们对块（blocks）的介绍结束。在第15章中，你将找到更多关于如何使用的示例。

# 结构 (Structures)

Objective-C 语言除了数组之外还提供了另一种分组元素的工具。你也可以使用结构（structures），它们是本节讨论的基础。

假设你想在程序内部存储一个日期——例如 7/18/11——可能用于某些程序输出的标题，甚至用于计算目的。存储日期的自然方法是简单将月份赋值给整数变量 `month`，将日期赋值给整数变量 `day`，将年份赋值给整数变量 `year`。因此，语句

```
int month = 7, day = 18, year = 2011;
```

可以正常工作。这是一个完全可以接受的方法。但如果你的程序还需要存储多个日期呢？通过某种方式将这些三变量组组合在一起会好得多。

你可以在 Objective-C 语言中定义一个名为 `date` 的结构，它由代表月份、日期和年份三个部分组成。这种定义的语法非常直观：

```
struct date
{
    int month;
    int day;
    int year;
};
```

刚刚定义的 `date` 结构包含三个整数成员，分别称为 `month`、`day` 和 `year`。本质上，`date` 的定义在语言中定义了一个新类型，因为此后可以声明变量为 `struct date` 类型，如下面的定义所示：

```
struct date today;
```

你也可以通过一个单独的定义来定义一个名为 `purchaseDate` 的变量，具有相同的类型：

```
struct date purchaseDate;
```

或者你可以简单地将两个定义写在同一行：

```
struct date today, purchaseDate;
```

与 `int`、`float` 或 `char` 类型的变量不同，在处理结构变量时需要特殊的语法。结构成员的访问是通过指定变量名、后跟一个点（.）、然后是成员名来实现的。例如，要将变量 `today` 中 `day` 的值设置为 21，你会这样写：

```
today.day = 21;
```

注意，变量名、点和成员名之间不允许有空格。

现在，等一下！这不就是我们访问对象属性时使用的同一个运算符吗？回想一下，我们可以写

```statement
myRect.width = 12;
```

来调用 `Rectangle` 对象的 setter 方法（名为 `initWith:`），并传递参数值 12。这里没有产生混乱：编译器会确定点运算符左侧是结构还是对象，并妥善处理该情况。

回到 `struct date` 示例，要将 `today` 中的 `year` 设置为 2011，可以使用这个表达式：

```
today.year = 2011;
```

最后，为了测试 `month` 的值以检查它是否等于 12，可以使用如下这样的语句：

```
if ( today.month == 12 )
next_month = 1;
```

程序 13.10 将前面的讨论整合到一个实际程序中。

# 程序 13.10

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
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

