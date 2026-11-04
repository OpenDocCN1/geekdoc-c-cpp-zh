
```
49   $"gross sales: {grossSales:C}\n" +
50   $"commission rate: {commissionRate:F2}\n" +
51   $"base salary: {baseSalary}";
52 }
```

Fig. 11.9 | BasePlusCommissionEmployee 继承自 CommissionEmployee 并可访问 CommissionEmployee 的受保护成员。 (第 2 部分，共 2 部分.)

## 测试类 BasePlusCommissionEmployee

本示例项目中的 BasePlusCommissionEmployeeTest 类与图 11.7 中的类相同，并产生相同的输出，因此此处不展示代码。尽管图 11.6 中的 BasePlusCommissionEmployee 类版本不使用继承，而图 11.9 中的版本使用了继承，但这两个类都提供相同的功能。图 11.9 中的源代码（52 行）比图 11.6 中的源代码（97 行）短得多，因为该类的很大一部分功能现在是从 CommissionEmployee 继承而来——CommissionEmployee 的功能现在只有一个副本。这使得代码更易于维护、修改和调试，因为与 CommissionEmployee 相关的代码仅存在于该类中。

## public 与 protected 数据

我们本可以将基类 CommissionEmployee 的实例变量 grossSales 和 commissionRate 声明为 public，以便派生类 BasePlusCommissionEmployee 访问基类的实例变量。然而，将实例变量声明为 public 是糟糕的软件工程做法，因为它允许类的任何客户端不受限制地访问实例变量，大大增加了错误和不一致的可能性。使用 protected 实例变量时，派生类可以访问实例变量，但未从基类派生的类无法直接访问其变量。

## protected 实例变量的问题

在本例中，我们将基类实例变量声明为 protected，以便派生类可以访问它们。继承 protected 实例变量使你能够在派生类中直接访问变量，而无需调用相应属性的 set 或 get 访问器，从而违反了封装。在大多数情况下，最好使用 private 实例变量并通过属性访问它们，以鼓励良好的软件工程实践。你的代码将更易于维护、修改和调试。

使用 protected 实例变量会产生几个潜在问题。首先，由于派生类对象可以直接设置继承变量的值，而无需使用属性的 set 访问器，因此派生类对象可能会为变量分配无效值。例如，如果我们将 CommissionEmployee 的实例变量 grossSales 声明为 protected，则派生类对象（例如 BasePlusCommissionEmployee）可以直接为 grossSales 分配负值，使其无效。

protected 实例变量的第二个问题是，派生类方法更可能被编写为依赖于基类的数据实现。实际上，派生类应仅依赖于基类服务（即非 private 方法和属性），而不是基类数据实现。如果基类实现发生变化，在基类中使用 protected 实例变量时，我们可能需要修改基类的所有派生类。例如，如果出于某种原因我们要更改实例变量 grossSales 和 commissionRate 的名称，那么我们就必须对派生类直接引用基类实例变量 grossSales 和 commissionRate 的所有出现位置进行更改。在这种情况下，软件被认为很脆弱或很易碎，因为基类的小改动可能会“破坏”派生类的实现。你应该能够在仍向派生类提供相同服务的同时更改基类实现。当然，如果基类服务发生变化，我们必须重新实现派生类。

> **软件工程观察 11.4**
> 将基类实例变量声明为 private（而不是 protected）可以使这些实例变量的基类实现发生变化，而不会影响派生类的实现。

## 11.4.5 使用 private 实例变量的 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构

## 基类 CommissionEmployee

类 CommissionEmployee（图 11.10）再次将实例变量 grossSales 和 commissionRate 声明为 private（第 10–11 行）。方法 Earnings（第 65 行）和 ToString（第 68–72 行）不再直接访问这些实例变量——而是使用属性 GrossSales 和 CommissionRate 来访问数据。如果我们决定更改实例变量的名称，Earnings 和 ToString 的声明将不需要修改——只有直接操作实例变量的属性 GrossSales 和 CommissionRate 的主体需要更改。这些更改仅发生在基类中——派生类不需要更改。将此类更改的影响本地化是一种良好的软件工程实践。派生类 BasePlusCommissionEmployee（图 11.11）继承自 CommissionEmployee，并可通过继承的公共属性访问私有基类成员。

// Fig. 11.10: CommissionEmployee.cs
// CommissionEmployee class represents a commission employee.
using System;

public class CommissionEmployee
{
    public string FirstName { get; }
    public string LastName { get; }
    public string SocialSecurityNumber { get; }
    private decimal grossSales; // gross weekly sales
    private decimal commissionRate; // commission percentage

    // five-parameter constructor
    public CommissionEmployee(string firstName, string lastName,
        string socialSecurityNumber, decimal grossSales,
        decimal commissionRate)
    {

Fig. 11.10 | CommissionEmployee 类表示一个佣金员工。 (第 I 部分，共 3 部分.)

```csharp
71        $"gross sales: {GrossSales:C}\n" +
72        $"commission rate: {CommissionRate:F2}";
73    }
```

Fig. 11.10 | CommissionEmployee 类表示一个佣金员工。 (第 3 部分，共 3 部分.)

## 派生类 BasePlusCommissionEmployee

类 BasePlusCommissionEmployee（图 11.11）在其方法实现上有一些变化，使其与图 11.9 中的版本有所区别。方法 Earnings（图 11.11，第 43 行）和 ToString（第 46–47 行）各自调用属性 BaseSalary 的 get 访问器来获取基本工资值，而不是直接访问 baseSalary。如果我们决定重命名实例变量 baseSalary，则只需要更改属性 BaseSalary 的主体。

```csharp
 1   // Fig. 11.11: BasePlusCommissionEmployee.cs
 2   // BasePlusCommissionEmployee inherits from CommissionEmployee and has
 3   // controlled access to CommissionEmployee's private data via
 4   // its public properties.
 5   using System;
 6
 7   public class BasePlusCommissionEmployee : CommissionEmployee
 8   {
 9       private decimal baseSalary; // base salary per week
10
11       // six-parameter derived-class constructor
12       // with call to base class CommissionEmployee constructor
13       public BasePlusCommissionEmployee(string firstName, string lastName,
14           string socialSecurityNumber, decimal grossSales,
15           decimal commissionRate, decimal baseSalary)
16           : base(firstName, lastName, socialSecurityNumber,
17               grossSales, commissionRate)
18       {
19           BaseSalary = baseSalary; // validates base salary
20       }
21
22       // property that gets and sets
23       // BasePlusCommissionEmployee's base salary
24       public decimal BaseSalary
25       {
26           get
27           {
28               return baseSalary;
29           }
30           set
31           {
32               if (value < 0) // validation
```

Fig. 11.11 | BasePlusCommissionEmployee 继承自 CommissionEmployee 并可通过其公共属性访问 CommissionEmployee 的私有数据。 (第 1 部分，共 2 部分.)
