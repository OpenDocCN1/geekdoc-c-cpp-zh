
```csharp
class Program
{
    static void Main(string[] args)
    {
        int monthlyWage = 1234;
        int months = 12, bonus = 1000;

        bool isActive = true;
        double rating = 99.25;

        double ratePerHour = 12.34;
        int numberOfHoursWorked = 165;

        double currentMonthWage = ratePerHour * numberOfHoursWorked;
        Console.WriteLine(currentMonthWage);

        Console.ReadLine();
    }
}
```

我将创建另一个变量，命名为`currentMonthWage`，并将其赋值为`ratePerHour`和`numberOfHoursWorked`的乘积。你可以看到，IntelliSense会自动提示我使用`ratePerHour`，我将其与`numberOfHoursWorked`相乘。现在右侧是一个简单的算术运算，其结果被赋给这个变量。所以我们并不总需要立即指定值；它也可以是赋值运算符右侧的一个计算结果，一个算术运算的结果。这里我们同样使用了一个运算符，之前我们已经不知不觉地用过它。现在，我可以通过`Console.WriteLine`看到结果，我将输出`currentMonthWage`。如果我们运行这段代码，就会看到结果，我认为结果会是正确的。根据你所在的位置和设置，其格式可能会有所不同。C#非常聪明。例如，如果我在这里添加一个`+ bonus`，它会知道必须先计算这两个数的乘积，然后再加上bonus。如果我们再次运行，应该会看到多了1000。这似乎是正确的。

还有其他赋值运算符。我特别喜欢的一个如下。假设我想给`ratePerHour`加上3，也就是增加每小时费率。我可以这样做：输入`+=`，然后写3。这等同于说`ratePerHour =`当前值`ratePerHour`加上3的结果。这个赋值运算符是我经常使用的快捷方式。它是一种简单地将`ratePerHour`变量的当前值增加3的方法。

我们也可以在C#中使用相等运算符。例如，我可以使用`currentMonthWage`的值，通过`if`语句检查该值是否大于2000。基于此，我将再次向控制台输出一些内容。另一个常用运算符是双加号或双减号。

```csharp
namespace BethanysPieShopHRM
{
    class Program
    {
        static void Main(string[] args)
        {
            int monthlyWage = 1234;
            int months = 12, bonus = 1000;

            bool isActive = true;
            double rating = 99.25;

            double ratePerHour = 12.34;
            int numberOfHoursWorked = 165;

            double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

            Console.WriteLine(currentMonthWage);

            Console.ReadLine();
        }
    }
}
```

假设我们有`numberOfEmployees`，这次我将其设置为整数类型，因为我认为我们可以增长很多。假设我们目前有15名员工。如果你想增加或减少这个值，可以使用双加号或双减号。假设有人离开了公司，我们都为此感到难过，我们可以在`numberOfEmployees`后面加上双减号。这将减少`numberOfEmployees`的当前值。如果我在这里设置一个断点，你还会看到如何操作，我可以在调试器中查看`numberOfEmployees`的值。我们试试。现在Visual Studio会命中断点，注意`numberOfEmployees`现在是14。该值减少了1。

```csharp
static void Main(string[] args)
{
    int monthlyWage = 1234;
    int months = 12, bonus = 1000;

    bool isActive = true;
    double rating = 99.25;

    double ratePerHour = 12.34;
    int numberOfHoursWorked = 165;

    double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

    Console.WriteLine(currentMonthWage);

    ratePerHour += 3; // ratePerHour = ratePerHour + 3;

    if (currentMonthWage > 2000)
    {
        Console.WriteLine("Top paid employee");
    }

    int numberOfEmployees = 15;
    numberOfEmployees--;

    bool a;
    int b;

    Console.ReadLine();
}
```

每种类型都有其默认值，对于布尔类型是`false`，对于整数类型是`0`。这些原始类型都内置了默认值，如果我们不赋值，就会使用默认值。我们现在已经看到了如何执行非常简单的操作，但我们对数据类型能做的事情远不止这些。

```csharp
int intMaxValue = int.MaxValue;

int intMinValue = int.MinValue;

double doubleMaxValue = double.MaxValue;
```

它们实际上非常巧妙。例如，当我们想要使用整数能容纳的最大值时，可以使用一个成员。你可能会问，什么是成员？这是个好问题。记得我说过，当我们使用`int`这个已知关键字时，C#中内置了一个类型`Int32`。这是一个内置了许多功能的类型。成员是类型上数据和行为的统称。在类型名称后面加一个点，这里的`int`，我们就可以访问其成员。当我们在`int`上这样做时，就可以访问`int.MaxValue`和`int.MinValue`。这将把一个变量赋值为整数类型能容纳的最大值或最小值。记住，数据类型也定义了值的可能范围，你在这里看到的就是如此。所有类型都有类似的成员，比如最后一行的`double`。

```csharp
char myChar = 'a';

bool isWhiteSpace = char.IsWhiteSpace(myChar);

bool isDigit = char.IsDigit(myChar);

bool isPunctuation = char.IsPunctuation(myChar);
```

我们还没有经常使用它，但`char`是一个非常有趣的类型，如前所述，用于存储单个Unicode字符。在`char`类型上定义了许多成员。假设我们希望在应用程序中接受输入，并检查用户输入了什么。我们可以使用`char.IsWhiteSpace`，传入字符变量，来检查给定值是否为空白。注意，我将`char`变量`myChar`传递给`IsWhiteSpace`成员（顺便说一下，这是一个方法），而`myChar`中包含的值是`a`。类似地，我们可以检查该值是数字还是标点字符。还有其他成员。在Visual Studio中花点时间尝试一下可用的成员吧。我现在将回到Visual Studio，向你展示`int`和`char`类型的一些成员。

```csharp
int monthlyWage = 1234;
int months = 12, bonus = 1000;

bool isActive = true;
double rating = 99.25;

double ratePerHour = 12.34;
int numberOfHoursWorked = 165;

double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

Console.WriteLine(currentMonthWage);

ratePerHour += 3; // ratePerHour = ratePerHour + 3;

if (currentMonthWage > 2000)
{
    Console.WriteLine("Top paid employee");
}

int numberOfEmployees = 15;
numberOfEmployees--;

int intMaxValue = int.MaxValue;
int intMinValue = int.MinValue;

Console.ReadLine();
```

我们现在还在`static void Main`中，接下来我要看看整数类型以及`char`类型包含哪些成员。假设我想检查整数类型可以容纳的最大值。我将创建一个变量，命名为`intMaxValue`，将其设置为`int`，然后不再创建变量，而是添加一个点，Visual Studio的IntelliSense会向我建议整数类型上可用的选项、成员。这些内容在本书后面会变得清晰，但这些是整数类型所知道的。例如，我可以问它：嘿，你的最大值是多少？同样，我也可以对最小值做同样的事情。这将是大数字。让我们运行应用程序，在调试器中看看它们有多大、多小。所以这是整数变量可以容纳的最大值，这是它的负数版本。这个整数关键字实际上表示`Int32`类型，它是一个结构体，我们稍后会学习结构体。但这实际上是一个快捷方式，避免我们总是键入`System.Int32`。但我仍然可以这样做。实际上我可以写`Int32`，它与`int`关键字具有相同的成员，因为它们指向的是完全相同的东西。这是第一个。我还使用另一种类型，即`char`。`char`通常用于表示一个字符。它只能包含一个Unicode字符。假设我想允许用户输入一个选择，我将捕获它。为简单起见，我将在这里创建一个变量，并为其赋值，`char`总是用单引号分隔。记住这一点，下一章我们学习字符串时会用到。我们总是将char与单引号结合使用。假设我想看看用户选择的字符的大写形式是什么。
