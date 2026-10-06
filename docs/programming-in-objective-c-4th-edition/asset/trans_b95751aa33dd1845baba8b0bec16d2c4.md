
是有效的。

如果你想让枚举标识符关联一个特定的整数值，可以在定义数据类型时将该整数分配给该标识符。随后出现在列表中枚举标识符将分配从指定的整数值加一开始的顺序整数值。

在下面的定义中，定义了一个名为 `direction` 的枚举数据类型，其值为 `up`、`down`、`left` 和 `right`：

```
enum direction { up, down, left = 10, right };
```

编译器给 `up` 分配值 0，因为它出现在列表第一个；给 `down` 分配 1，因为它在其后；给 `left` 分配 10，因为显式地分配了该值；并给 `right` 分配 11，因为它是列表中上一个枚举的增值。

枚举标识符可以共享相同的值。例如：

```
enum boolean { no = 0, false = 0, yes = 1, true = 1 };
```

给枚举变量赋值值 `no` 或 `false` 都会将其赋值为 0；赋值 `yes` 或 `true` 都会将其赋值为 1。

作为枚举数据类型定义的另一个示例，以下代码定义了 `enum month` 类型，其允许分配给该类型变量的值可以是全年月份的名称：

```
enum month { january = 1, february, march, april, may, june, july, august, september, october, november, december };
```

Objective-C 编译器实际上将枚举标识符视为整数常量。如果你的程序包含以下两行代码，值 2 将分配给 `thisMonth`（而不是名称 `february`）：

```
enum month thisMonth;
...
thisMonth = february;
```

程序 10.3 显示了一个使用枚举数据类型的简单程序。该程序读取一个月份数字，然后进入 `switch` 语句来查看输入的是哪个月份。记住，编译器将枚举值视为整数常量，因此它们是有效的 `case` 分。变量 `days` 被分配为指定月份的天数，并在 `switch` 退出后显示其值。程序中包含一个特殊测试，以检查月份是否为二月。

# 程序 10.3

```
#import <Foundation/Foundation.h>
// 每个月份的天数
int main (int argc, char * argv[]) {
    @autoreleasepool {
        enum month { january = 1, february,
        march, april, may, june,
        july, august, september,
        december };
        enum month amonth;
        int days;

    NSLog("Enter month number: %s");
    scanf("%i", &amonth);

switch (amonth) {
    case january:
    case march:
    case may:
    case july:
    case august:
    case october:
    case december:
        days = 31;
        break;
    case april:
    case june:
    case september:
    case november:
        days = 30;
        break;
    case february:
        days = 28;
        break;
    default:
        NSLog (@"bad month number");
        days = 0;
        break;
}

if ( days != 0 )
    NSLog (@"Number of days is %i", days);

if ( amonth == february )
    NSLog (@"...or 29 if it's a leap
year");
    }
    return 0;
}
```

# 程序 10.3. 输出

Enter month number:
5
Number of days is 31

# 程序 10.3. 输出（重新运行）

Enter month number:
2
Number of days is 28
...or 29 if it's a leap year

你可以显式地为枚举数据类型变量分配整数值；你应该使用类型转换运算符来这样做。因此，如果 `monthValue` 是一个值为 6 的整数变量，例如，这个表达式是允许的：

```
lastMonth = (enum month) (monthValue - 1);
```

如果你不使用类型转换运算符，编译器（遗憾的是）不会对此报错。

在使用带有枚举数据类型的程序时，尽量不要依赖于枚举值被视为整数这一事实。相反，应将它们视为不同的数据类型。枚举数据类型为你提供了一种方法，可以将符号名称与整数关联起来。如果你稍后需要更改该数字的值，你必须在定义枚举的地方更改它。如果你基于枚举数据类型的实际值做出假设，就会失去使用枚举带来的这种好处。

在定义枚举数据类型时，允许某些变体：可以省略数据类型的名称，并在定义类型时将变量声明为特定的枚举数据类型。作为显示这两种选项的示例，语句



```
enum { east, west, south, north } direction;
```

定义了一个具有 `east`、`west`、`south` 或 `north` 值的（匿名）枚举数据类型，并声明变量 `direction` 为该类型。

在块内部定义枚举数据类型会将该定义的作用范围限制在块内。另一方面，在程序开头、任何块之外定义枚举数据类型，将使该定义对文件全局。

在定义枚举数据类型时，你必须确保枚举标识符相对于相同作用域内定义的其他变量名和枚举标识符来说是唯一的。

# typedef 语句

Objective-C 提供了一种功能，允许程序员为数据类型分配一个别名。这是通过名为 `typedef` 的语句实现的。以下语句定义名称 `Counter` 等同于数据类型 `int`：

```
typedef int Counter;
```

你随后可以声明类型为 `Counter` 的变量，如下：

```
Counter j, n;
```

Objective-C 编译器将之前所示的 `j` 和 `n` 的声明视为普通变量。在这种情况下，使用 `typedef` 的主要优势在于为变量增加了可读性。以传统方式将它们声明为 `int` 类型不会使这些变量的意图变得清晰。

以下 `typedef` 定义了类型 `NumberObject` 为 `Number` 对象：

```
typedef Number *NumberObject;
```

随后声明的类型为 `NumberObject` 的变量，如下

NumberObject myValue1, myValue2, myResult;

被处理为像以普通方式声明一样：

Number *myValue1, *myValue2, *myResult;

要使用 `typedef` 定义新类型名称，请遵循此步骤：

- 像声明所需类型的变量一样编写该语句。
- 在通常出现变量名的地方，替换为新的类型名称。
- 在所有内容之前放置关键字 `typedef`。

作为此过程的示例，要定义类型 `Direction` 为由 `east`、`west`、`north` 和 `south` 组成的枚举类型，写出枚举定义并在通常出现变量名的地方替换 `Direction`。在所有内容之前放置 `typedef`：

```
typedef enum { east, west, south, north } Direction;
```

有了这个 `typedef`，你随后可以声明类型为 `Direction` 的变量，如下：

```
Direction step1, step2;
```

# 数据类型转换

第四章“数据类型与表达式”简要介绍了系统在评估表达式时有时会进行转换的事实。你检查了 `float` 和 `int` 数据类型的情况。你看到涉及 `float` 和 `int` 的操作作为浮点运算执行的，其中整数数据项自动转换为浮点。你还看到如何使用强制运算符显式指示转换。因此，假设 `total` 和 `n` 都是整数变量：

```
average = (float) total / n;
```

变量 `total` 的值在执行操作之前转换为 `float` 类型，从而保证除法作为浮点运算执行。

# 转换规则

Objective-C 编译器在评估由不同基本数据类型组成的表达式时遵循非常严格的规则。

以下总结了在表达式两个操作数过程中转换发生的顺序：

