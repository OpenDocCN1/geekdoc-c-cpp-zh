
# 第 10 章 继承简介

## 理解继承

继承是一项原则，你可以将对通用类别的知识应用于更具体的对象上。你从各种情况下都熟悉继承的概念。当你使用“继承”一词时，你可能会想到遗传继承。你从生物学中知道，你的血型和颜色是遗传基因的产物。你可以说关于你的许多其他事实（你的属性）也是遗传的。同样，你通常也可以将你的行为归因于继承；例如，你处理钱的方式可能和你奶奶处理的方式相似，你的步态可能和你的父亲一样——所以你的方法也是被继承的。

你可能还会根据遗传属性来选择种植植物和动物。你在房子旁边种植植物是因为它们在阴影处生长得良好；你领养一只贵宾犬是因为你知道贵宾犬不掉毛。每种植物和宠物都有略有不同的特征，但在一个物种内部，你可以依靠一致的遗传属性和行为。换句话说，你可以重用从通用类别中获得的知识，并将其应用于特定类别。同样，你在面向对象编程语言中创建的类可以从现有类继承数据和方法。当你通过从另一个类创建一个类时，系统会自动为你提供数据字段和方法；你可以重用已经编写并测试过的字段和方法。

你已经知道如何创建类以及如何从这些类实例化对象。例如，考虑图 10-1 中的 `Employee` 类。该类包含两个数据字段 `idNum` 和 `salary`，以及包含每个字段访问器的属性，以及一个创建员工问候语的方法。

```csharp
class Employee {
    private int idNum;
    private double salary;
    public int IdNum {
        get {
            return idNum;
        }
        set {
            idNum = value;
        }
    }
    public double Salary {
        get {
            return salary;
        }
        set {
            salary = value;
        }
    }
    public string GetGreeting() {
        string greeting = "Hello. I am employee #" + IdNum;
        return greeting;
    }
}
```

**图 10-1** Employee 类

在你创建 `Employee` 类之后，可以创建特定的 `Employee` 对象，如下所示：

```csharp
Employee receptionist = new Employee();
Employee deliveryPerson = new Employee();
```

这些 `Employee` 对象最终可能拥有不同的编号和工资，但它们都是 `Employee` 对象，你知道每个都拥有某些 ID 编号和工资。

假设你雇了一种新类型的 `Employee`，他们赚取的薪水不同。例如，该类包含两个数据字段 `idNum` 和 `salary`，以及包含每个字段访问器的属性，以及一个创建员工问候语的方法。

在你创建 `Employee` 类之后，可以创建特定的 `Employee` 对象，如下所示：

```csharp
Employee receptionist = new Employee();
Employee deliveryPerson = new Employee();
```

这些 `Employee` 对象最终可能拥有不同的编号和工资，但它们都是 `Employee` 对象，你知道每个都拥有某些 ID 编号和工资。

假设你雇了一种新类型的 `Employee`，他们赚取的薪水不同。

## 继承层次结构

`DomesticPet` 以及来自 `Animal` 的 `DomesticPet`。子类所派生的父类完整列表构成了子类的祖先。

在你创建了 `Spruce` 类之后，你可能准备好创建 `Spruce` 对象了。例如，你可能会创建一个 `TreeInMyBackYard`，或者为树木地图创建一个包含 1000 个 `Spruce` 对象的数组。同样，一个 `Poodle` 对象可以是 `myPetDogFifi`。

继承是传递的，这意味着子类继承了其祖先的所有成员。换句话说，当你声明一个 `Spruce` 对象时，它包含了 `Evergreen` 和 `Tree` 的所有属性和方法。在使用 C# 时，你会遇到许多此类传递性继承链的示例。

当你创建自己的继承链时，你希望将字段和方法放在最通用的级别。换句话说，名为 `Grow()` 的方法理所应当属于 `Tree` 类，而 `LeavesTurnColor()` 则不然，因为该方法只适用于某些 `Tree` 类。同样，`LeavesTurnColor()` 方法放置在 `Deciduous` 类中比单独放在 `Oak` 或 `Maple` 类中要好。

### 两个真相一个谎言：理解继承

1. 当你使用继承创建一个类时，你可以节省时间，因为你可以复制粘贴已经为原始类创建的字段、属性和方法。
2. 当你使用继承创建一个类时，你减少了错误的概率，因为原始类的属性和方法已经过使用和测试。
3. 当你使用继承创建一个类时，你让任何使用过原始类的人更容易理解新类，因为这些用户可以集中在新功能上。

错误的陈述是 #1。当你使用继承创建一个类时，你并没有复制这些类成员；原始类已经为你创建好了，因为你不需要重新创建你所继承的字段、属性和方法。

## 扩展类

当你创建一个作为另一个类的扩展或子类的类时，你需要在派生类名和其基类名之间使用单个冒号。例如，以下类头在 `CommissionEmployee` 和 `Employee` 之间创建了子类-父类关系。

```csharp
class CommissionEmployee : Employee
```

每个 `CommissionEmployee` 对象自动包含基类的字段和方法；然后你可以向新的派生类添加新的字段和方法。图 10-3 显示了一个 `CommissionEmployee` 类。

```csharp
class CommissionEmployee : Employee
{
    private double commissionRate;
    public double CommissionRate
    {
        get {
            return commissionRate;
        }
        set {
            commissionRate = value;
        }
    }
}
```

**图 10-3** CommissionEmployee 类

尽管你在图 10-3 的 `CommissionEmployee` 类中只看到了一个字段，但它包含了三个字段：从 `Employee` 继承的 `idNum` 和 `salary`，以及在 `CommissionEmployee` 类中定义的 `commissionRate`。同样，`CommissionEmployee` 类包含了三个属性和一个方法——两个和一个方法继承自 `Employee`，一个属性在 `CommissionEmployee` 内部定义。当你使用以下语句编写实例化对象的程序时，可以使用接下来的任何语句为销售人员设置字段值：

```csharp
CommissionEmployee salesperson = new CommissionEmployee();
salesperson.IdNum = 234;
salesperson.Salary = Convert.ToDouble(ReadLine());
salesperson.CommissionRate = 0.07;
```

销售人员对象可以访问三个 setter 访问（两个来自它的父类和一个来自它自己的类），因为它既是 `CommissionEmployee` 也是 `Employee`。同样，该对象可以访问三个 getter 访问和 `GetGreeting()` 方法。图 10-4 显示了一个 `Main()` 方法声明了 `Employee` 和 `CommissionEmployee` 对象，并显示了每个对象可以使用的所有属性和方法。图 10-5 显示了程序的输出。

```csharp
using static System.Console;
class DemoEmployees
{
    static void Main()
    {
        Employee clerk = new Employee();
        CommissionEmployee salesperson = new CommissionEmployee();
        clerk.IdNum = 123;
        clerk.Salary = 30000.00;
        salesperson.IdNum = 234;
        salesperson.Salary = 20000.00;
        salesperson.CommissionRate = 0.07;
        WriteLine("\n" + clerk.GetGreeting());
        WriteLine("Clerk {0} salary: {1} per year", clerk.IdNum, clerk.Salary.ToString("C"));
        WriteLine("\n" + salesperson.GetGreeting());
        WriteLine("Salesperson {0} salary: {1} per year", salesperson.IdNum, salesperson.Salary.ToString("C"));
        WriteLine("...plus {0} commission on all sales", salesperson.CommissionRate.ToString("P"));
    }
}
```

**图 10-4** DemoEmployees 类声明了 `Employee` 和 `CommissionEmployee` 对象

![](img/b0a31988f44670d0728c4f372d8dab77_455_0.png)

**图 10-5** DemoEmployees 程序的输出

继承只向一个方向工作：类继承自父类——反之亦然。如果程序在以下语句中实例化了一个 `Employee` 对象，那么 `Employee` 对象无法访问 `CommissionEmployee` 的属性或方法。

```csharp
Employee clerk = new Employee();
clerk.CommissionRate = 0.1;
```

`Employee` 是父类，`clerk` 是父类的对象。`Employee` 对象无法访问 `CommissionEmployee` 的属性或方法。当你创建父类时，你不知道会创建多少个类，或者它们的数据或方法会是什么样。此外，子类是具体的。`HeartSurgeon` 类和 `Obstetrician` 类是 `Doctor` 类。你不期望通用 `Doctor` 类拥有 `HeartSurgeon` 的 `RepairValve()` 方法或 `Obstetrician` 的 `DeliverBaby()` 方法。然而，通用 `Doctor` 类拥有 `CheckBloodPressure()` 和 `AdmitPatients()`。正如医生一样，方便认为派生类的字段和方法比基类更具体。

> **不要这样做**
>
> 该语句是无效的——`Employee` 对象没有 `CommissionRate`。

![](img/b0a31988f44670d0728c4f372d8dab77_456_0.png)

观看视频：继承。

### 两个真相一个谎言：扩展类

1. 当你使用继承创建一个类时，以下类头表示 `Dog` 是 `Pet` 的子类：`public class Pet : Dog`
2. 如果 `X` 有四个字段且类 `Y` 派自 `X`，那么类 `Y` 也包含至少四个字段。
3. 继承只向一个方向工作：子类继承自父类——反之亦然。

错误的陈述是 #1。以下类头表示 `Dog` 是 `Pet` 的子类：

```csharp
public class Dog : Pet
```

## 你要做

在本节中，我们将创建一个继承的运行示例。分四个部分创建此示例：

- 创建通用的 `Loan` 类，存储与银行贷款相关的数据——贷款号、姓名和借款金额。
- 在创建通用的 `Loan` 类后，编写一个程序来实例化并使用 `Loan` 对象。
- 创建一个更具体的 `CarLoan` 派生类，它继承 `Loan` 类的属性，并添加有关贷款抵押的汽车信息。
- 修改 `Loan` 演示程序以添加 `CarLoan` 对象并演示其用法。

### 创建 Loan 类和使用它的类的程序

1. 打开一个名为 `DemoLoan` 的新项目，然后输入 `Loan` 类的几行代码。该类包含三个自动实现的属性，分别用于贷款号、客户姓氏和贷款价值。

```csharp
class Loan
{
    public int LoanNumber { get; set; }
    public string LastName { get; set; }
    public double LoanAmount { get; set; }
}
```

2. 在文件顶部，输入以下代码以添加一个包含 `Main()` 方法的 `DemoLoan` 类。该类声明了一个 `Loan` 对象并显示了如何设置每个字段以及显示结果。

```csharp
using static System.Console;
class DemoLoan
{
    static void Main()
    {
        Loan aLoan = new Loan();
        aLoan.LoanNumber = 2239;
        aLoan.LastName = "Mitchell";
        aLoan.LoanAmount = 1000.00;
        WriteLine("Loan #{0} for {1} is for {2}", aLoan.LoanNumber, aLoan.LastName, aLoan.LoanAmount.ToString("C2"));
    }
}
```

3. 保存文件，然后编译并执行程序。输出结果如图 10-6 所示。该类或其运行方式并没有特殊之处；它与你在学习继承之前在上一章中看到的许多类相似。

```
C:\Chapter.10>DemoLoan
Loan #2239 for Mitchell is for $1000.00
C:\Chapter.10>
```

**图 10-6** DemoLoan 程序的输出

### 扩展一个类

接下来，你创建一个名为 `CarLoan` 的类。`CarLoan` “是一种” 类型的 `Loan`。因此，它拥有 `Loan` 的所有属性，但同时也包含了客户用作贷款押品的车辆的年份和品牌。因此，`CarLoan` 是 `Loan` 的子类。

1. 将 `DemoLoan` 文件保存为 `DemoCarLoan`。将 `DemoLoan` 的名称更改为 `DemoCarLoan`。在 `Loan` 类的大括号之后开始定义 `CarLoan` 类。`CarLoan` 继承自 `Loan`，并包含两个持有车辆年份和品牌的属性。

```csharp
class CarLoan : Loan
{
    public int Year { get; set; }
    public string Make { get; set; }
}
```

2. 在 `DemoCarLoan` 类的 `Main()` 方法中，按照如下方式在 `Loan` 的声明之后声明 `CarLoan`：

```csharp
CarLoan aLoan = new CarLoan();
```
