

```csharp
using static System.Console;
class DemoStudents
{
    static void Main()
    {
        Student payingStudent = new Student();
        ScholarshipStudent freeStudent = new ScholarshipStudent();
        payingStudent.Name = "Megan";
        payingStudent.Credits = 15;
        freeStudent.Name = "Luke";
        freeStudent.Credits = 15;
        WriteLine("{0}'s tuition for {1} credits is {2}",
            payingStudent.Name, payingStudent.Credits,
            payingStudent.Tuition.ToString("C"));
        WriteLine("{0}'s tuition for {1} credits is {2}",
            freeStudent.Name, freeStudent.Credits,
            freeStudent.Tuition.ToString("C"));
    }
}
```

图 10-13 DemoStudents 程序

两个阴影区域的计算学费值不同，因为每个对象都使用了 `Credits` 属性的不同版本。图 10-14 显示了程序的执行情况。

如果基类和派生类具有名称相同但参数列表不同的方法，则派生类方法不会重写基类方法；而是重载基类方法。例如，如果基类包含一个标头为 `void Display()` 的方法，而其子类包含一个标头为 `Display(string s)` 的方法，那么子类将可以访问这两个方法。（你已经在“高级方法概念”章节中学习过方法重载）

7516c1fec7be7af209b17ae3_465.png

图 10-14 DemoStudents 程序的输出

## 从派生类访问基类方法和属性

当派生类包含重写了父类方法或属性的方法或属性时，你可能需要在子类中使用父类版本。如果是这样，你可以使用关键字 `base` 来访问父类方法或属性。例如，调用图 10-7 中 `Employee` 类中的 `GetGreeting()` 方法。如果它的子类 `CommissionEmployee` 一个 `GetGreeting()` 方法，如图 10-15 所示，那么在 `CommissionEmployee` 中你可以

## 第 10 章 继承简介

```csharp
class CommissionEmployee : Employee
{
    private double commissionRate;
    public double CommissionRate
    {
        get
        {
            return commissionRate;
        }
        set
        {
            commissionRate = value;
        }
    }
    new public string GetGreeting()
    {
        string greeting = base.Greeting();
        greeting += "\n on commission.";
        return greeting;
    }
}
```

方法标头中的关键字 `new` 消除了重写基类时的编译器警告

图 10-15 带有 `GetGreeting()` 方法的 CommissionEmployee 类

使用 `base.Greeting()` 来访问方法的基类版本。图 10-16 显示了一个使用 `CommissionEmployee` 对象调用该方法的应用程序。图 10-17 显示了输出。

```csharp
using static System.Console;
class DemoCommission2
{
    static void Main()
    {
        CommissionEmployee salesperson = new CommissionEmployee();
        salesperson.Id = 345;
        WriteLine(salesperson.GetGreeting());
    }
}
```

图 10-16 DemoCommission2 程序

7516c1fec7be7af209b17ae3_466_0.png

图 10-17 DemoCommission2 程序的输出

## 重写基类成员

在图 10-15 中，子类 `GetGreeting()` 方法在它的标头中使用关键字 `new` 来消除编译器警告。然后，在方法内部调用了父类的 `GetGreeting()` 版本。返回的字符串存储在 `greeting` 变量中，并在将完整消息返回给调用程序之前，拼接了 `on commission`。通过在子类中重写基类方法，消除了重复的类型输入。此外，如果将来修改消息的第一部分，它将只在一个处被修改——即基类中。

### 两个真话一个谎言 基类成员

- 当你在子类中重写父类方法时，这些方法具有相同的名称。
- 当你在子类中重写父类方法时，这些方法具有相同的参数列表。
- 当你在子类中重写父类方法并随后使用子类方法时，基类方法首先执行，然后执行子类方法，而不是父类版本。
- 随后使用子类方法时，执行子类方法。错误的陈述是 #3。当你在子类中重写父类方法时

## 你来做

在之前的章节中，你创建了 `Loan` 和 `CarLoan` 类和对象。假设银行采用以下规则：

- 普通贷款金额不低于 $5,000。
- 对于任何超过 2008 年车型的汽车都不提供汽车贷款。
- 虽然 `Loans` 可能有更长的贷款编号，但 `CarLoans` 的贷款编号将超过三位数。如果提供了较大的贷款编号，程序将仅使用最后三位作为贷款编号。

## 在派生类中使用基类成员

1. 打开 `CarLoan` 文件，并将其另存为 `Loan2`。同时将类名从 `CarLoan` 改为 `CarLoan2`。
2. 在 `Loan` 类中，添加一个代表最小贷款值的新常量：
`public const double MINIMUM_LOAN = 5000;`
3. 为 `LoanAmount` 添加一个字段，因为 `LoanAmount` 属性（之前是自动实现属性）将需要使用它：
`protected double LoanAmount;`
该字段是受保护的，以便 `CarLoan` 对象也能像 `Loan` 对象一样访问它。
4. 将 `Loan` 类中 `LoanAmount` 的自动实现属性替换为如下 `get` 和 `set` 访问器。此更改确保了任何贷款都不会低于允许的最小值：
```csharp
public double LoanAmount
{
    set
    {
        if(value < MINIMUM_LOAN)
            LoanAmount = MINIMUM_LOAN;
        else
            LoanAmount = value;
    }
    get
    {
        return LoanAmount;
    }
}
```
5. 在 `CarLoan` 类中，添加两个新常量用于保存提供汽车贷款的最早年份和最低允许编号：
`private const int EARLIEST_YEAR = 2008;`
`private const int LOW_INVALID_NUM = 1000;`
6. 同样在 `CarLoan` 类中，添加一个汽车年份的字段，并将现有的自动实现 `Year` 属性替换为包含

## 重写基类成员（续）

和 `set` 访问器。`Year` 属性设置器不仅设置年份字段，当汽车年份小于 2008 时，还将 `loanAmount` 设置为 0。

```csharp
private int year;
public int Year
{
    set
    {
        if(value < EARLIEST_YEAR)
        {
            year = value;
            loanAmount = 0;
        }
        else
            year = value;
    }
    get
    {
        return year;
    }
}
```

如果 `loanAmount` 在父类 `Loan` 中是私有的，你将无法像在这里在子类中设置它。你可以使用 `LoanAmount` 属性设置值，但父类访问器会将值强制设为 5000。

7. 假设贷款编号有唯一规则。在 `CarLoan` 类中，在最后一个大括号之前，更改继承的 `LoanNumber` 属性以适应新规则。如果贷款编号为三位或少，将其传递给基类。如果不是，通过计算贷款编号除以 1000 的余数获取最后三位，并将新编号传递给基类。在 `Make` 属性定义后添加以下属性。

```csharp
public new int LoanNumber
{
    return base.LoanNumber;
}
```

（继续）

8. 保存文件。编译它，并修正任何错误。当你执行程序时，输出如图 10-18 所示。将输出与图 10-7 进行比较。注意 $1000 的银行贷款被强制变为 $5000。此外，注意汽车贷款编号已缩短为三位数，由于汽车年龄的原因，贷款价值为 $0。

> 调用它自身的方法是递归方法。递归方法有时很有用，但它们需要特殊的代码来避免无限循环，并且在这种情况下并不适用。

