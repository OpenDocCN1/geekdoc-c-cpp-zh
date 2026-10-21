

## 为数据类型定义同义词

typedef 关键字使你能够为现有类型定义自己的类型名。使用 typedef，你可以将类型名 BigOnes 定义为与标准 long int 类型等价，声明如下：

```
typedef long int BigOnes;      // Defining BigOnes as a type name
```

这将 BigOnes 定义为 long int 的替代类型说明符，因此你可以用以下声明将变量 mynum 声明为 long int：

```
BigOnes mynum = 0L;           // Define a long int variable
```

此声明与使用内置类型名的方式没有区别。你同样可以使用：

```
long int mynum = 0L;          // Define a long int variable
```

得到完全相同的结果。事实上，如果你定义了自己的类型名如 BigOnes，你可以在同一个程序中使用两种类型说明符来声明不同的变量，这些变量最终将具有相同的类型。

由于 typedef 仅为现有类型定义同义词，它看起来可能有点肤浅，但并非如此。你稍后会看到，它在使你能够通过定义一个代表 somewhat 复杂类型说明的名称来简化更复杂的声明方面发挥了非常有用的作用，这可以使你的代码更具可读性。

## 具有特定值集的变量

你有时会面临需要变量具有可通过标签有意义引用的有限可能值的需求——例如一周中的天数，或一年中的月份。C++ 中有一种专门用于处理这种情况的设施，称为枚举。举一个我刚刚提到的例子——一个可以假设对应于一周中天数的值的变量。你可以按如下方式定义它：

```
enum Week{Mon, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

这声明了一个名为 Week 的枚举类型和变量 thisWeek，它是枚举类型 Week 的实例，只能假设在大括号之间指定的常量值。如果你尝试将 thisWeek 分配除指定集合中的值之外的任何值，它将导致错误。大括号之间列出的符号名称为枚举数。事实上，每天的每个名称都将被自动定义为代表一个固定的整数值。列表中的第一个名称 Mon 的值为 0，Tues 为 1，以此类推。

你可以按如下方式将枚举常量之一分配为变量 thisWeek 的值：

```
thisWeek = Thurs;
```

## 数据、变量和计算

请注意，你不需要用枚举名限定枚举常量。thisWeek 的值将为 3，因为枚举定义符号常量默认按类型 int 从 0 开始按顺序分配值。

默认情况下，每个后续枚举数比前一个的值大一，但如果你希望隐式编号从不同的值开始，你只需写：

```
enum Week {Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

现在枚举常量将等价于 1 到 7。枚举数甚至不需要具有唯一的值。例如，你可以将 Mon 和 Tues 都定义为值为 1，使用语句：

```
enum Week {Mon = 1, Tues = 1, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

由于变量 thisWeek 的类型为 int，它将占用四个字节，所有枚举类型的变量也将如此。

在定义了枚举的形式后，你可以这样定义另一个变量：

```
enum Week nextWeek;
```

这定义了一个变量 nextWeek，它是一个枚举，可以假设先前指定的值。你也可以在声明变量时省略 enum 关键字，因此，代替前面的语句，你可以写：

```
Week next_week;
```

如果你愿意，可以为所有枚举数分配特定值。例如，你可以定义此枚举：

```
enum Punctuation {Comma = ',', Exclamation = '!', Question = '?'} things;
```

在这里，你已将变量 things 的可能值定义为相应符号的数值等价物。如果你查看附录 B 中的 ASCII 表，你会看到这些符号在十进制中分别为 44、33 和 63。正如你所见，分配的值不必按升序排列。如果你没有显式指定所有值，每个枚举数将从上一个指定的值递增 1 进行赋值，就像我们第二个 Week 示例一样。

如果你不需要稍后定义此类型的其他变量，可以省略枚举类型。例如：

```
enum {Mon, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek, nextWeek, lastWeek;
```

在这里你声明了三个变量，可以假设从 Mon 到 Sun 的值。由于未指定枚举类型，你无法引用它。请注意，你根本不能为此枚举定义其他变量，因为你不被允许重复定义。 doing so would imply that you were redefining values for Mon to Sun, and this isn’t allowed.

## 指定枚举常量的类型

枚举常量默认类型为 int，但你也可以通过在声明中在枚举类型名之后添加冒号和常量类型名来显式指定类型。你可以指定枚举常量的类型为任何有符号或无符号整数类型：short、int、long 和 char，或类型 bool。

因此，你可以将代表一周中天数的枚举定义为：

```
enum Week: char{ Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };
```

这里枚举常量将为类型 char，第一个常量为 0。然而，使用类型为 char 的常量时，你可能更喜欢显式初始化它们，像这样：

```
enum Week : char{ Monday='M', Tuesday='T', Wednesday='W',
    Thursday='T', Friday='F', Saturday='S', Sunday='S'};
```

现在常量的值更能反映它们所代表的内容，尽管它们无法区分星期四和星期二或星期六和星期日。常量具有重复值并没有问题，但当然，所有名称必须是唯一的。

这里有一个枚举常量为 bool 的例子：

```
enum State : bool { On = true, Off };
```

由于 On 的初始值为 true，Off 将为 false。如果有后续的枚举常量指定，它们将默认交替取值。

## 基本输入/输出操作

在这里，你只会查看足够的原生 C++ 输入输出，以便你学习 C++。这并不是说它很困难——事实上恰恰相反——但对于 Windows 编程，你根本不需要它。C++ 输入/输出围绕数据流的概念展开，你可以将数据插入到输出流中或从输入流中提取数据。你已经看到 ISO/ANSI C++ 标准输出流到命令行屏幕上被称为 cout。相应的来自键盘的输入流被称为 cin。

## 从键盘输入

你通过流 cin 使用提取运算符 >> 从键盘获取输入。要从键盘读取两个整数值到整数变量 num1 和 num2，你可以写此语句：

```
cin >> num1 >> num2;
```

提取运算符 >> “指向”数据流动的方向——在本例中，从 cin 到两个变量中的每一个。任何前导空白将被跳过，你键入的第一个整数值将被读入 num1。这是因为输入语句从左到右执行。任何空白

行。因为输出语句从左到右执行，第二个输出语句显示 num1 的值后跟 num2 的值。

当你编译并执行此操作时，你将得到输出：

```
12345678
```

输出是正确的，但并不十分有帮助。你确实需要两个输出值之间至少有一个空格分隔。流输出的默认值只是输出输出值中的数字，这不提供将连续输出值很好地分隔开以便区分的间距。如是，你无法判断第一个数字何时结束第二个数字何时开始。

## 格式化输出

你可以通过在两个值之间输出一个空格来很容易地解决数据项之间没有空格的问题。你可以通过替换原始程序中的以下行来做到这一点：

```
cout << num1 << num2;            // Output two values
```

只需替换语句：

```
cout << num1 << ' ' << num2;            // Output two values
```

当然，如果你有几行输出想要在列中对齐，你需要一些额外的能力，因为你不知道每个值会有多少位数字。你可以通过使用所谓的操纵符来处理这种情况。操纵符修改数据输出到（或输入自）流的方式。

操纵符在头文件 <iomanip> 中定义，因此你需要为其添加 #include 指令。你将使用的操纵符是 setw(n)，它将输出的值右对齐在宽度为 n 个空格的字段中，因此 setw(6) 导致下一个输出值以宽度为六个空格的字段呈现。让我们看看它是如何工作的。

## 试一试    使用操纵符

为了获得更接近你想要的输出，你可以将程序更改为以下内容：

```
// Ex2_03.cpp
// Exercising output
#include <iostream>
#include <iomanip>

using std::cout;
using std::endl;
using std::setw;

int main()
{
    int num1 = 1234, num2 = 5678;

