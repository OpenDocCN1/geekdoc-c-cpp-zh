
表示使用参数 `150` 和 `35` 调用函数 `gcd`，并将该函数返回的值存储在变量中。

如果省略了函数的返回类型声明，编译器将假设函数将返回一个整数——如果它确实返回了值。许多程序员利用这一事实，省略了返回整数的函数的返回类型声明。

## 声明返回类型和参数类型

与方法不同，我们之前提到编译器假设函数返回 `int`。

一种万无一失的编写原型声明的方法是直接复制函数定义中的第一行。记得在末尾加上一个分号。

如果函数接受可变数量的参数（例如 `NSLog` 和 `scanf` 的情况），必须告知编译器。

```objc
void NSLog (NSString *format, ...);
```

告诉编译器 `NSLog` 接受一个 `NSString` 对象作为第一个参数，后面跟着任意数量的额外参数（`...` 的用法）。`NSLog` 在特殊文件 `Foundation.h` 中声明，这就是为什么你在每个程序的开头都放置以下行的原因：

```objc
#import <Foundation/Foundation.h>
```

如果没有这一行，编译器会假设 `NSLog` 接受固定数量的参数，这可能导致生成错误的代码。

当调用函数时，编译器会自动将数值参数转换为相应的类型，前提是你已经声明了该函数。

考虑一些关于函数的提醒和建议：

- 默认情况下，编译器假设函数返回 `int`。
- 定义返回 `int` 的函数时，应将其声明为此。
- 定义不返回值的函数时，应定义为 `void`。
- 只有在你之前声明过的情况下，编译器才会转换参数以与预期的类型一致。

函数默认是外部的。也就是说，函数的默认作用范围是它可以被与之链接的范围内任何函数或方法调用。你可以通过将函数设置为 `static` 来限制其作用范围。通过在函数声明前放置 `static` 关键字来实现，如下：

```c
static int gcd (int u, int v)
{
  ..
}
```

静态函数只能由包含其定义的文件的其他函数或方法调用。

### 函数、方法与数组

要将单个数组元素传递给函数或方法，你可以按照常规方式将数组元素作为参数。例如，如果你有一个计算平方根的 `squareRoot` 函数，想要计算 `averages[i]` 的平方根并将结果赋值给变量 `sq_root_result`，那么这样的语句就是有效的：

```objc
sq_root_result = squareRoot (averages[i]);
```

将整个数组传递给函数或方法是完全另一回事。要传递数组，你需要在函数调用或方法调用的内部仅列出数组的名称，而不带任何下标。例如，假设 `grade_scores` 已被声明为一个包含 100 个元素的数组，那么表达式

```
minimum (grade_scores)
```

将 `grade_scores` 数组中包含的全部 100 个元素传递给名为 `minimum` 的函数。自然地，`minimum` 函数必须预期接收一个整个数组作为参数，并必须进行适当的形式参数声明。

此函数在包含指定数量元素的数组中寻找最小整数值：

```objc
// 寻找数组中最小值的函数
int minimum (int values[], int numElements)
{
    int minValue = values[0];
    for ( i = 1; i < numElements; ++i )
        if ( values[i] < minValue )
            minValue = values[i];
    return (minValue);
}
```

`minimum` 函数定义为接收两个参数：首先是你想要找到最小值的数组，其次是数组中的元素数量。函数头中紧随 `values` 之后的左右方括号告诉 Objective-C 编译器 `values` 是一个整数数组。编译器并不关心它有多大。

形式参数 `numElements` 充当 `for` 语句内部的上限。因此，该语句遍历了从 `values[1]` 到数组末尾元素（即 `values[numElements - 1]`）的数组。

如果函数或方法更改了数组元素的值，该更改将作用于传递给函数或方法的原始数组上。即使在函数或方法执行完毕后，该更改仍然有效。

数组的行为与简单变量或数组元素（函数或方法无法更改其值）不同，这值得稍作解释。我们曾提到过，当调用函数或方法时，作为参数传递的值会被复制到对应的形式参数中。这一说法仍然有效。然而，在处理数组时，数组的全部内容并没有复制到形式参数数组中。相反，传递的是一个指向数组在计算机内存位置的指针。因此，对形式参数数组的任何更改实际上都是对原始数组进行的，而不是对数组的副本。因此，当函数或方法返回时，这些更改仍然有效。

# Blocks（代码块）

`Blocks` 是 C 语言的一个最新扩展。它们不是标准 ANSI C 定义的一部分，而是由 Apple 公司添加到语言中的。`Blocks` 的外观和行为与函数非常相似。其语法需要一些时间适应。你可以像向函数传递参数一样向块传递参数。你也可以从块中返回一个值。

与函数不同，块可以定义在函数或方法内部，这使其能够访问块外部定义但在其作用域内的任何变量。通常情况下，可以访问这些变量，但不能更改它们的值。有一个特殊的 `__block__` 修饰符（注意：在单词 `block` 前面有两个下划线），它允许你从块内部修改变量的值，稍稍后我们将看到它是如何使用的。

块可以作为参数传递给函数和方法，在第二部分“Foundation 框架”中，你将学习到一些期望接收块作为参数的方法。块的优势之一是它们可以由系统分发给其他处理器或应用程序内的其他线程执行。

让我们从一个简单的示例开始。回想我们在本章中写的第一个函数 `printMessage`：

```objc
void printMessage (void)
{
    NSLog("Programming is fun.");
}
```

这里是一个完成相同任务的块：

```objc
^(void)
{
    NSLog("Programming is fun.");
}
```

块通过开头的脱字符字符 `^` 来标识。其后是该块接收的括号参数列表。在我们的案例中，我们的块不接受任何参数，所以我们像在函数定义中那样写了 `void`。

你可以将此块赋值给名为 `printMessage` 的变量，只要该变量被正确声明（这里语法就变得复杂了）：

```objc
void (^printMessage) (void) =
^(void) {
  NSLog("Programming is fun.");
};
```

在等号左侧，我们指定 `printMessage` 是一个指向不接受参数且不返回值的块的指针。注意，赋值语句以分号结束。

执行由变量引用的块与调用函数的方法相同：

```objc
printMessage();
```

程序 13.6 将这些内容整合到了一个示例中。

# 程序 13.6

```objc
#import <Foundation/Foundation.h>
int main (int argc, char * argv[]) {
  @autoreleasepool {
    void (^print_message) (void) =
^(void) {
      NSLog("Programming is fun.");
    }
    printMessage();
  }
  return 0;
}
```

# 程序 13.6 输出

Programming is fun.

程序 13.7 是程序 13.4 的重写，使用了块而不是函数。块可以定义在全局，也可以定义在局部。在这种情况下，我们将在 `main` 外部定义块，使其在作用域上是外部且全局的。

# 程序 13.7

```objc
#import <Foundation/Foundation.h>
// 计算 n 阶三角形数的块
void (^calculateTriangularNumber) (int) = ^(int n) {
    int i, triangularNumber = 0;
    for (i = 1; i <= n; ++i) {
        triangularNumber += i;
    }
    NSLog("@Triangular number %i is %i", n, triangularNumber);
}
int main (int argc, char * argv[]) {
    @autoreleasepool {
        calculateTriangularNumber(10);
        calculateTriangularNumber(20);
        calculateTriangularNumber (50);
    }
  return 0;
}
```

# 程序 13.7 输出

Triangular number 10 is 55
Triangular number 20 is 210
Triangular number 50 is 1275

对比程序 13.4 中的函数语法与程序 13.7 中定义的块。块指针变量 `calculateTriangularNumber` 被定义为接收一个 `int` 参数且不返回值。

正如本节开头提到的，块可以返回一个值。这里是程序 13.5 中 `gcd` 函数重写的块形式：

```objc
int (^gcd) (int, int) = ^(int u, int v){
    int temp;
    while ( v != 0 )
    {
      temp = u % v;
      u = v;
      v = temp;
    }
    return u;
};
```

块可以访问其所在作用域内的变量。该变量的值是块定义时的值。这在程序 13.8 中得到了体现。

# 程序 13.8

```objc
#import <Foundation/Foundation.h>
int main (int argc, char * argv[]) {
    @autoreleasepool {
        int foo = 10;
        void (^printFoo)(void) = 
^(void) {
            NSLog ("foo = %i", foo);
        };
        foo = 15;
        printFoo ();
    }
    return 0;
}
```

# 程序 13.8 输出

foo = 10

`printFoo` 块可以访问局部变量 `foo`。注意显示的值是 10 而不是 15。这是因为它是块定义时的值，而不是执行时的值。

默认情况下，你无法修改块外部变量的值。因此，如果你尝试在块内部更改 `foo` 的值（见程序 13.9），你将收到编译器的错误信息：赋值只读变量 'foo'。

# 程序 13.9

```objc
#import <Foundation/Foundation.h>
int main (int argc, char * argv[])
{
    @autoreleasepool {
        int foo = 10;
        void (^printFoo) (void) =
        ^(void) {
            NSLog ("foo = %i", foo);
            foo = 20; // 这一行会产生编译错误
        }
        foo = 15;
        printFoo();
        NSLog ("foo = %i", foo);
    }
    return 0;
}
```

如果你在程序 13.9 中在局部变量 `foo` 的定义之前插入块修饰符，使其如下所示：

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

### 结构 (Structures)

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
