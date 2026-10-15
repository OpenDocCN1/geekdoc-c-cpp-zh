
# 第10章 如何找到正确的方法

我们已经初步了解了如何使用参数将数据传递给方法，但在这方面还有一些额外的选项，所以接下来我们来看看。我们已经知道，方法需要名称、返回类型以及0个或多个参数。当我们请求C#调用某个方法时，它会开始搜索对应的方法。为了找到正确的方法，它不仅仅使用名称。事实上，确实要考虑几个因素来定位正确的方法。方法名称是第一个。然后它还会检查对方法的调用是否传递了与方法要求相同的参数类型。方法可能声明需要一个字符串参数，但如果我们尝试传入一个整数实参，C#就不会匹配它。这是一件好事。C#的类型安全机制会确保在编译时不仅名称匹配，而且参数类型也匹配。此外，在搜索正确方法时也会考虑参数数量。总之，我们可以说，有三个因素用于找到正确的方法：方法名称、参数类型和参数数量。只有当这个组合被找到时，C#才会调用该方法。这还带来了另一件事：需要唯一的是这个组合，而不仅仅是名称。确实，我们可以有多个同名方法。只要该组合在类内保持唯一，那就没问题。在同一个类中可以存在多个同名方法，这一事实称为方法重载。

```
static void Main(string[] args)
{
    DisplaySum(3, 52);
}
```

名称可以相同，但我们需要定义不同数量的参数，或者不同的参数类型，或者这两者的组合。我有两个同名的方法。它们都叫DisplaySum。第一个变体有两个整数参数。

```
public static void DisplaySum
(int a, int b)
{ ... }

public static void DisplaySum
(int a, int b, int c)
{ ... }
```

第二个有三个。C#会接受这一点。这些现在就是重载方法。然后我们现在从Main中调用DisplaySum，正如你在这里看到的，只用了两个参数。高亮显示的版本被选中。C#会匹配这个方法，而且只匹配这一个，因为参数数量匹配。让我们回到Visual Studio，看看方法重载的实际运行。当我们要求C#调用CalculateYearlyWage方法时，它实际上会搜索一个方法，该方法具有那个特定的名称，并且具有相同数量的参数，参数类型也需要匹配。实际上是可以创建重载方法的，也就是具有相同名称的方法，但它们需要包含不同数量的参数或不同类型的参数。这仍然能让C#区分你想要使用哪个方法。那么让我为你演示一下方法重载。

```
static void Main(string[] args)
{
    int monthlyWage = 1234;
    int months = 12;

    int yearlyWage = CalculateYearlyWage(monthlyWage, months);

    Console.WriteLine($"Yearly wage (from main): {yearlyWage}");

    Console.ReadLine();
}

public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//Let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}
```

我要引入一个同名方法。正如你在这里看到的，它也叫做CalculateYearlyWage。它也接受monthlyWage和numberOfMonthsWorked，但现在这个方法接受第三个参数bonus。参数类型是相同的，所以我们不能就这样做然后让Visual Studio说：“嗯，我已经有一个带有这些参数的方法了，所以你不能这样做。”

![](img/0155736aec718cf18821e9f10a5d308d_708_0.png)

我无法区分这两个方法。但这并不是我计划要做的；我实际上是添加了第三个参数，这对C#来说没问题。所以现在只是包含一个整数类型的第三个参数，这里是bonus，然后我在方法内部使用了它。所以这两个方法现在就是重载方法。它们有相同的名称，但参数数量不同。但我也可以做同样的事情，但现在不同之处在于参数类型不同，所以它们现在是double类型。

![](img/0155736aec718cf18821e9f10a5d308d_708_1.png)

所以在这一点上，C#仍然可以根据参数、参数数量或我传递给它的参数类型来区分这三个方法。那么我要去这里，引入一个bonus。我们把它设置为1000。我将像之前一样修改方法调用，并添加bonus。你会自动看到Visual Studio正在向我显示这些重载。

```
0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

1 reference
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}

0 references
public static double CalculateYearlyWage(double monthlyWage, double numberOfMonthsWorked, double bonus)
{
```

这些是同一个方法的不同重载，但参数组合不同，正如你在这里看到的。那么接下来会发生什么？好吧，我要展示实际调用的是哪一个，所以我会设置几个断点，然后运行应用程序，看看哪个会被命中。

```
//int yearlyWage = CalculateYearlyWage(monthlyWage, months, bonus);

//Console.WriteLine($"Yearly wage (from main): {yearlyWage}");

double monthlyWageDouble = 1500.0;
double monthsDouble = 12;
double bonusDouble = 1000;
double yearlyWageWithBonusDouble = CalculateYearlyWage(monthlyWageDouble, monthsDouble, bonusDouble);

Console.ReadLine();
}

0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked)
{
    //Console.WriteLine($"Yearly wage: {monthlyWage * numberOfMonthsWorked}");
    if (numberOfMonthsWorked == 12)//let's add a bonus month
        return monthlyWage * (numberOfMonthsWorked + 1);

    return monthlyWage * numberOfMonthsWorked;
}

0 references
public static int CalculateYearlyWage(int monthlyWage, int numberOfMonthsWorked, int bonus)
{
    Console.WriteLine($"The yearly wage is: {monthlyWage * numberOfMonthsWorked + bonus}");
    return monthlyWage * numberOfMonthsWorked + bonus;
}

1 reference
public static double CalculateYearlyWage(double monthlyWage, double numberOfMonthsWorked, double bonus)
```

你会看到，确实是具有整数参数类型的方法被选中、被使用，那是因为我在那边传递了整数值。现在让我在这里加入一点额外的代码。我已经引入了原始参数的double变体，现在我也要计算年工资，但这次传入这些double类型的变量。你能猜到会调用哪一个吗？我想你猜到了。让我们看看。确实，根据参数类型以及参数数量，C#已经决定需要调用这个方法。

# 第11章 如何按值和按引用传递参数

在C#中，可以通过两种方式向方法传递参数。到目前为止，我们实际上一直使用的是默认方式，也就是按值传递。第二种选项是按引用传递参数，这需要我们在想要以这种方式传递的参数上使用一个新关键字，即ref关键字。让我们更详细地探讨这两个选项。如前所述，默认的传递参数方式是按值传递，这正是我们目前一直在使用而没有真正关注的方式。使用这种方法时，当我们调用方法并向它传递实参（即参数值）时，会创建一个副本供方法使用。方法可以在这些值上任意操作。这些值是工作副本，因此调用者中的值不会被更改，它们不会被触及。假设我们再次拥有AddTwoNumbers方法，并且我定义a为33，b为44。

```
int a = 33;
int b = 44;

AddTwoNumbers(a, b);
```

我将这些值传递给AddTwoNumbers方法。本质上，会创建这些值的副本，然后传递给方法。如果方法现在修改这些值，比如这里给b参数加上10，那么调用者中b的原始值不会受到影响，它仍然是44。方法是在副本上操作的。这就是按值传递。第二种传递方式是按引用传递。

