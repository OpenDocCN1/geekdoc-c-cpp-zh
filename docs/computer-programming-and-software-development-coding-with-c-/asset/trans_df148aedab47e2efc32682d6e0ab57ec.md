

```
public class Manager: Employee
{
    public Manager(string first, string last, string em, DateTime bd, double? rate):base(first, last, em, bd, rate)
    { }
}
```

此时，我的 Manager 类已经存在，并且由于它继承自 Employee，我已经可以用它做很多事情了。让我们来试试看。我们仍然可以像之前那样创建一个 Employee，这就是这里看到的。我正在创建一个新的 Employee，同样是 Bethany。而我现在可以以非常相似的方式创建一个新的 Manager。那是我的新类型，我们就叫它 Mary。我现在将简单地通过调用 Manager 构造函数来创建一个新的 Manager 对象，它接受的参数，嗯，几乎相同，所以我需要为这些参数传递值。现在我们已经创建了一个新的 Manager 对象，一个新的 Manager 实例，并且我们将该对象命名为 Mary。在原来的 Employee 类型上，我们可以像之前那样做。我们可以显示员工详情。我们可以要求我们的 Bethany 对象执行工作，并且我们也可以在其上调用 ReceiveWage 方法。但现在，由于每个经理实际上都是一个员工，我也可以在 Mary 对象上拥有该经理，也就是说，例如，调用 DisplayEmployeeDetails。如果我现在在此处执行转到定义，它将显示与 Employee 类中相同的 DisplayEmployeeDetails，正如你在这里看到的那样。

```
```csharp
public double ReceiveWage()
{
    double wageBeforeTax = NumberOfHoursWorked * HourlyRate.Value;
    double taxAmount = wageBeforeTax * taxRate;

    Wage = wageBeforeTax - taxAmount;

    Console.WriteLine($"The wage for {NumberOfHoursWorked} hours of work is {Wage}.");
    NumberOfHoursWorked = 0;

    return Wage;
}

public void DisplayEmployeeDetails()
{
    Console.WriteLine($"\nFirst name: {FirstName}\nLast name: {LastName}\nEmail: {Email}\nBirthday: {BirthDay.ToShortDateString()}\n");
}
```
```

此方法现在可用。它现在也可以在 Manager 类上被知晓。并且以非常相似的方式，我们也可以要求执行工作。我们也可以调用 ReceiveWage 方法。如果运行它，我们将看到 Bethany 执行了一些工作，并且我们可以看到 Mary 的详情。Mary 做了一些工作，现在 Mary 领取工资。你可能在此时想，嗯，这没问题，但有什么附加价值呢？Mary 可以做与 Bethany 完全相同的事，我们的员工，所以经理在此时与员工并没有什么不同。正确，但我现在可以扩展我的 Manager 类型。我可以在 Manager 类上添加员工所没有的东西。经理做什么呢？例如，一个封装在方法内的附加功能，那就是参加管理会议。可能是我们的经理需要执行员工不可用的操作，例如参加管理会议。管理会议往往会开得很长，所以我将把工作小时数增加 10。通过这样做，我引入了一些你可能还没有注意到的东西。

NumberOfHoursWorked 现在在 Manager 类型中使用，但它也在基类上可用，也就是 Employee。

```
{
public class Manager : Employee
{
    public Manager(string first, string last, string em, DateTime bd, double? rate) : base(first, last, em, bd, rate)
    { }
    public void AttendManagementMeeting()
    {
        NumberOfHoursWorked += 10;
    }
}
```

并且由于 Employee 类中它是 public，我可以直接在 Manager 类型中与之交互，就像它定义在 manager 本身上一样。让我们在这里添加一些控制台输出以显示我们的经理正在参加管理会议。我在这里对 FirstName 和 LastName 做的事情也差不多。这两个是在基 Employee 类上定义的。我可以回到 Program 类，并且我实际上可以让我们的经理，也就是 Mary，参加一次管理会议。那是现在仅对经理可用的功能。的确，我不能要求 Bethany 参加管理会议。正如你在这里看到的，Visual Studio 会抱怨并说，嗯，employee 不知道 AttendManagementMeeting。的确，这仅在派生类型上可用，也就是 Manager 类型上。让我再回到 Manager，并让我们多谈谈访问修饰符。在这里，我可以直接访问 number of hours worked。那是一个 public 属性，我可以从派生类型中与之交互。在 Employee 上，我也有 firstName、lastName、email，以及 numberOfHoursWorked 的私有字段。我不能在派生类型中访问这些私有字段。所以如果我想访问

```
```csharp
public class Manager : Employee
{
    public Manager(string first, string last, string em, DateTime bd, double? rate) : base(first, last, em, bd, rate)
    {
    }

    public void AttendManagementMeeting()
    {
        NumberOfHoursWorked += 10;

        numberOfHoursWorked
    }
}
```

但仍然从 Program 类中，我无法访问它。如果我现在再次回到我的 bethany 类型并想要访问 NumberOfHoursWorked，你会看到我只能得到大写的那个，也就是作为 public 属性。受保护的数据仍然不可访问。我现在已将我的 numberOfHoursWorked 设置回 private，因为我可以通过属性在我的派生类型中工作。使用这些访问修饰符也适用于方法。

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        Employee bethany = new Employee("Bethany", "Smith", "bethany@snowball.be", new DateTime(1979, 1, 16), 25);

        Manager mary = new Manager("Mary", "Jones", "mary@snowball.be", new DateTime(1965, 1, 16), 30);

        bethany.DisplayEmployeeDetails();
        bethany.PerformWork();
        bethany.PerformWork();
        bethany.ReceiveWage();

        mary.DisplayEmployeeDetails();
        mary.PerformWork();
        mary.PerformWork();
        mary.ReceiveWage();

        mary.AttendManagementMeeting();
        bethany.numberOfHoursWorked;

        Console.ReadLine();
    }
}
```
```

假设我希望 StopWorking 不对派生类型可用，那么我可以将其设为 private，这会很奇怪。但假设我现在想从 Manager 类型访问 StopWorking 方法。我将无法再访问它，因为它是私有的，Visual Studio 也会在这里说。

![](img/0155736aec718cf18821e9f10a5d308d_832_0.png)

由于其保护级别而无法访问。如果我将其设为 public 或 protected，那么它在我的草稿类型上再次可用。让我们将其设置回 public。

## 第 22 章 Is-A 关系基础

C# 中的继承带来的就是有时被称为关系的东西。的确，即使在口语中，我们也会说经理是一个员工。关系正是继承带给我们的，也体现在我们的 C# 代码行为中。

```
Manager m1 = new Manager();//Manager derives from Employee
Researcher r2 = new Researcher();//Researcher derives from Employee
m1.PerformWork(); //will call PerformWork() on the base Employee class
r2.PerformWork(); //will call PerformWork() on the base Employee class
```

当我们定义一个 Manager 实例，其中 Manager 类派生自 Employee 时，基 Employee 类上定义的所有 public 或 protected 成员都将对 Manager 可用。如果 PerformWork 是 Employee 类上的 public 或 protected 方法，由于经理是一个员工，它就对经理可用。Manager 类可以像我们在演示中所见的那样添加新功能，这仅对 Manager 实例可用，而不对 Employee 实例可用。并且多个类型可以从基 Employee 类继承。如果 Researcher 2 继承自基 Employee 类，每个 Researcher 2 都是一个 Employee，因此 Researcher 实例也会获得对 PerformWork 的访问权限。

