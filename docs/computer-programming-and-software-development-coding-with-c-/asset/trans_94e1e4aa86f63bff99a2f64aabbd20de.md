
```csharp
int intMaxValue = int.MaxValue;
int intMinValue = Int32.MinValue;

char userSelection = 'a';
char upperVersion = char.ToUpper(userSelection);
bool isDigit = char.IsDigit(userSelection);
bool isLetter = char.IsLetter(userSelection);

DateTime hireDate = new DateTime(2021, 3, 28, 14, 30, 0);

Console.WriteLine(hireDate);

DateTime exitDate = new DateTime(2021, 12, 11);

//DateTime invalidDate = new DateTime(2021, 15, 11);

DateTime startDate = hireDate.AddDays(15);

Console.WriteLine(startDate);

DateTime currentDate = DateTime.Now;
bool areWeInDst = currentDate.IsDaylightSavingTime();

Console.ReadLine();
```

我提到 DateTime 类型通常用于表示某个具体的时间点，但如果我们想要表达一个时间跨度、一段持续时间，那么就可以使用 TimeSpan。假设我创建了 DateTime startHour 并将其设置为 DateTime.Now。如果我想表达一个工作日的持续时间，我可以用 TimeSpan 来做到这一点。我在这里创建 TimeSpan，并称之为 workTime，并将其设置为一个新的 TimeSpan，我们也必须以这种方式初始化时间跨度，并将其设置为 8 小时 35 分钟 0 秒。现在我可以计算该员工何时停止工作。所以 endHour 将是 startHour，然后我将向其添加一个 TimeSpan，那就是我的 workTime。现在注意这里的区别。这里我使用了 AddDays，它期望一个 double 值。这里我使用的是 Add 方法，它期望一个 TimeSpan。那么让我们来看一下 startHour 和 endHour 的值。

![](img/0155736aec718cf18821e9f10a5d308d_656_0.png)

所以 startHour 是 3 月 22 日，20 点 56 分，而 endHour 将在第二天大约凌晨 5:30 左右，所以 C# 实际上在这里添加了这个 TimeSpan。现在我在调试器中向你展示这些值，但我也可以使用 TimeSpan 和 DateTime 的漂亮字符串表示形式。这些类型自带大量内置功能。这里我使用 startHour 上的 ToLongDateString 和 endHour 上的 ToShortTimeString。这些是 DateTime 类型的成员，我可以用它们以可读的格式表示日期。现在你可以看到，它确实向我展示了一个可读的 DateTime 和一天中可读的时间。在这一部分，我想谈谈如何在 C# 中在不同类型之间进行转换。

```csharp
int a = 3;
a = "Hello world";
```

你可能会想，我刚才不是说过变量的类型一旦确定就无法更改吗？那你为什么又提这个问题呢？好吧，让我来解释一下。在这里，截图上显示的内容根本行不通。它实际上会导致编译时错误。我们首先声明 a 为整数值并赋值为 3，然后在下一行我将一个字符串赋给我们的变量。错误，错误到处都是，至少在这一行。尽管我们不能在声明后更改变量的类型，但可以将值从一种类型转换为另一种类型，然后将该值赋给目标类型的新变量。为此，我们使用转换，实际上有几种选项可以用来转换。我们可以进行隐式转换、显式转换，也称为强制转换，或者使用一个帮助器。让我们来看一下。

```csharp
int a = 123456789;

long l = a;

double d = 123456789.0;
int a = (int) d;

double d = 12345.0;
int a =
(int)Convert.ChangeType(d, typeof(int));
```

首先，让我向你展示隐式转换，也称为隐式强制转换。假设我们创建一个整数变量并赋予它一个值。如果我们现在创建一个 long 类型的另一个变量并将 a 赋给它，基本上我们在这里做的是取出 a 的值并将其传递给我们的新变量。我们确实是在处理值。C# 不会对此抱怨，因为数据转换，嗯，只是可以正常工作。Long 可以包含比整数更大的数字，所以不会丢失任何东西。实际上不需要特殊的语法来进行隐式强制转换。其次，让我们尝试做同样的事情，从 double 到 integer。如果我们以同样的方式尝试这样做，C# 编译器会抱怨，因为现在可能会丢失数据。确实，double 可以包含比整数更多的内容；因此，我们需要告诉 C#，嗯，我们知道自己在做什么，并且需要指定我们希望值被转换成的类型。这是通过在 d 之前加上目标类型放在括号中来完成的。现在你会看到并非所有转换基本上都能工作，因此它们可能会导致运行时异常，从而使复制简单地崩溃。最后，如前所述，可以使用帮助器。C# 提供了 Convert.ChangeType，这是一种允许在类型之间进行转换的方法。在这里你可以看到我正在使用 Convert.ChangeType 将 d 的值更改为整数值。在下一个演示中，让我向你展示如何在类型之间进行转换。C# 类型系统会检查我们分配的值是否与类型匹配并且也在允许的范围内。但它也会在我们从一种类型转换到另一种类型时检查该转换是否会自动进行，或者是否存在可能的数据丢失。在这里我们创建了 numberOfHoursWorked。那是一个整数值。

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

        long veryLongMonth = numberOfHoursWorked;

        double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

        //Console.WriteLine(currentMonthWage);

        ratePerHour += 3;//ratePerHour = ratePerHour + 3;

        if (currentMonthWage > 2000)
        {
            //Console.WriteLine("Top paid employee");
        }
    }
}
```

假设我创建一个 long 变量。long 类型的变量可以包含比整数大得多的值，所以我实际上可以说我要创建一个变量 veryLongMonth，并将 numberOfHoursWorked 赋给它。所以我现在将 numberOfHoursWorked 转换为 long。

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

        long veryLongMonth = numberOfHoursWorked;
        double d = 123456789.0;
        int x = (int)d;

        double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

        //Console.WriteLine(currentMonthWage);

        ratePerHour += 3; //ratePerHour = ratePerHour + 3;

        if (currentMonthWage > 2000)
        {
            //Console.WriteLine("Top paid employee");
        }

        int numberOfEmployees = 15;
        numberOfEmployees--;
    }
}
```

由于 long 变量实际上可以包含比整数更大的值，C# 会允许此操作自动进行。没有数据丢失的风险。但假设我做以下操作。我将创建一个 double，并暂时称之为 d，并将其赋值为这里的值。现在如果我现在创建一个整数值，暂时称之为 x，并说，嗯，我将把这个 x 设置为 d，那么在这种情况下，我将把 d 中当前的值赋给 x。但现在，注意红色波浪线。Visual Studio 会说它无法进行隐式转换，这就是它在这里实际所做的。它无法为我们进行此转换，因为我们必须明确同意可能会发生一些数据丢失，而为此我需要进行显式强制转换。通过在转换前在类型前加上括号，我基本上是在告诉 C#，嗯，我知道我要将其转换为整数，我可以接受可能发生的任何数据丢失。但是，隐式和显式强制转换在 C# 中是非常常见的事情。让我们在这里再做一个。假设我做一个 int intVeryLongMonth，然后我再次将 long 版本赋给它。你认为会发生什么？

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

        long veryLongMonth = numberOfHoursWorked;
        double d = 123456789.0;
        int x = (int)d;

        int intVeryLongMonth = veryLongMonth;

        double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

        //Console.WriteLine(currentMonthWage);

        ratePerHour += 3;//ratePerHour = ratePerHour + 3;

        if (currentMonthWage > 2000)
        {
            //Console.WriteLine("Top paid employee");
        }

        int numberOfEmployees = 15;
    }
}
```

好吧，你可能已经看到 Visual Studio 再次说它不会自动执行此操作。可能会发生数据丢失，long 变量可以包含比整数更大的值。所以如果我真的想这样做，我需要再次在 long 之前加上 int 类型放在括号中。除了转换之外，还有

