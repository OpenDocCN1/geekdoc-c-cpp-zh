

## 1. 多态与继承概念

在本示例中，`Manager` 记录包含一个其基类中不存在的方法，即 `Manage()`。同样，`Worker` 记录包含一个其基类 `Employee` 中不存在的方法，即 `Work()`。

这两个方法的实现相当“平凡”。它们仅仅返回（不同的）字符串。但即便如此，它们仍然说明了面向对象编程中的一个重要概念。

`Manage()` 方法使用了属性 `Salary`，并且使用了重写的 `Manager` 实现 `Manager.Salary`。同样，`Work()` 使用了在 `Worker` 记录中重写的 `Salary` 实现。即使我们使用 `Employee` 类型的变量，这一说法依然成立，我们将在本课中进一步讨论。

### 2. 组织层级结构

现在转到“组织”，我们在 `Organization` 一侧也有类似的类型继承结构。

`Organization` 是一个 `abstract`（抽象）类。它包含一个只读属性 `Name`，并定义了一个受保护的构造函数。受保护的构造函数、字段、属性和方法只能在其子类（或“子记录”）中使用或被重写。

与之前一样，冒号 (:) 在类声明中表示父子关系。例如，类 `Management` : `Organization` 意味着 `Management` 类继承自 `Organization` 类。同样，`RankAndFile` 也继承自 `Organization`。

在自定义类型层级中，子类型的构造函数必须调用其父类型构造函数之一。我们已经见过在（位置）记录中使用特殊语法的例子。

对于类，我们使用 `base` 关键字。例如，对于 `Management` 和 `RankAndFile`，我们都显式地“调用”了 `base(name)`（至少在语法上，位于冒号之后），这对应于受保护的 `Organization(string name)` 构造函数。

如果我们调用的是无参默认构造函数，则可以省略这种显式调用基类构造函数的语法。如果在基类没有默认构造函数的情况下省略 `base(...)` 调用，将导致编译错误。（例如，`Organization` 类没有默认构造函数。）

### 3. 虚方法和抽象方法

请注意，在本示例中，`Employee? GetEmployeeName(string)` 受保护方法被声明为 `virtual`（虚方法），并且包含一个实现（这与抽象方法或属性不同）。

类/记录中的 `Virtual`（虚方法）以及 `abstract`（抽象）属性和方法可以在其子类型中使用 `override` 关键字进行重写。（出于显而易见的原因，`virtual` 或 `abstract` 方法和属性不能是 `private`（私有的）。否则，它们无法从子类型中被重写。）

根据运行时使用的实际具体类型，将调用相应的方法/属性。

本示例代码中的 `Organization` 类除了 `GetEmployeeByName()` 外，还包含一个独立的方法 `GetEmployee()`，用于演示目的。（实际上这种划分可能并非必要。）

`GetEmployee()` 方法不是 `virtual`（虚方法），但它调用了 `virtual`（虚方法）`GetEmployeeByName()`。

```csharp
public Employee? GetEmployee(string name) => GetEmployeeByName(name);
```

虽然这个实现看起来调用了 `Organization.GetEmployeeByName()`，但这种解释并不完全正确。

由于 `GetEmployeeByName()` 是一个 `virtual`（虚方法），取决于运行时变量（类型为 `Organization`）的实际类型，将调用不同的 `GetEmployeeByName()` 方法。也就是说，在运行时，将调用 `Management.GetEmployeeByName()` 或 `RankAndFile.GetEmployeeByName()`。

（请注意，由于 `Organization` 是一个抽象类型，因此不能直接创建其实例。）

对于初学者来说，理解面向对象编程风格的这一概念可能比较困难，但我们强调，在对这些概念接触足够多之后，它会显得自然而然。关键不在于“理解”，而在于“熟悉”它们。

“抽象/虚方法”和“重写”的整套机制都是为了支持这种多态行为。重申一下，对于抽象和虚方法及属性，取决于对象的运行时类型（例如，基于用于创建对象的实际构造函数），可能会使用重写的方法或属性（如果有的话），来替代其父/基类型中定义的方法或属性，而无论对象的类型在源代码中是如何声明的。

在这个例子中，值得注意的是，如果我们声明 `GetEmployeeName()` 为 `abstract`（抽象）而不是 `virtual`（虚方法），这种特定的方案（例如，依赖于多态行为）可能无法正常工作。抽象方法和属性只能用于其他抽象方法或属性中。

### 4. 协变返回值

关于这个 `GetEmployeeName()` “虚方法”的一个有趣之处是，重写的方法具有略微不同的方法签名。

对于 Organization：
```csharp
virtual Employee? GetEmployeeName(string) { }
```

对于 Management：
```csharp
override Manager? GetEmployeeName(string) { }
```

对于 RankAndFile：
```csharp
override Worker? GetEmployeeName(string) { }
```

这在 C# 中是允许的，因为 Manager 继承自 Employee，而 Worker 也继承自 Employee。你可以返回父类的虚方法/属性所返回类型的子类型。这被称为“协变返回值”。

通常，子类/记录中重写的方法和属性应具有完全相同的签名。“协变返回值”是这一规则的例外。

### 5. 运行时类型解析

在主程序中，我们创建 Employee 对象和 Organization 对象。

它们在静态上被声明为 Employees 和 Organizations。

```csharp
var allEmployees = new List<Employee>();
var allOrgs = new List<Organization>();
```

然而，在运行时，使用正确的实现记录/类，并调用适当的重写属性和方法。

例如，在“总费用”计算中，Manager 和 Worker 使用了正确的 Salary 值。

即使我们更明确地声明它们，也没有区别。例如，

```csharp
Employee m1a = new Manager("M1a");
Employee m1b = new Manager("M1b");
Employee w1m = new Worker("W1m");
Employee w1n = new Worker("W1n");
Employee w2x = new Worker("W2x");
Employee w2y = new Worker("W2y");
Employee w2z = new Worker("W2z");
Organization managerOrg1 = new Management("M1") { m1a, m1b };
Organization workerOrg1 = new RankAndFile("W1") { w1m, w1n };
Organization workerOrg2 = new RankAndFile("W2") { w2x, w2y, w2z };
```

尽管所有这些对象都以它们各自的基类（分别是 Employee 和 Organization）在静态上声明，但在运行时使用的是正确的类型。

从某种意义上说，这就是多态的本质。例如，变量 m1a 在源程序中被声明为 Employee 类型，但由于它在运行时被创建为 Manager，因此它更具体地是一个子类型 Manager 的变量。

同样，类型为 Employee 的 w1m，更具体地说，确实是一个子类型 Worker 的变量。

变量 m1a 和 w1m 一方面都是 Employee 类型，但另一方面，由于它们是不同的子类型的实例，它们可以表现出不同的行为（例如，当我们调用 GetEmployee() 时）。

例如，`managerOrg1[0].GetType()`（来自 `object.GetType()`）将返回更具体的类型 `Corporation.Manager`，而不是父类 `Corporation.Employee`（尽管 `managerOrg1[0]` 被声明为 Employee）。

C# 和 .NET 包含许多运算符来帮助管理程序中的类型。例如，可以使用 `is` 运算符来测试对象是否属于给定类型（或类型继承层级中的某一类型）。

```csharp
Console.WriteLine($"{managerOrg1[0] is Employee}");
Console.WriteLine($"{managerOrg1[0] is Manager}");
```

这两个语句都打印出 `true`，而 `managerOrg1[0] is Worker` 的求值结果为 `false`。（在这个说明中，我们可以使用 `m1a` 变量代替 `managerOrg1[0]`，结果相同。）

请注意，对于任何非空变量 `v`，表达式 `v is object` 的值始终为 `true`，无论 `v` 的类型如何，因为在 C# 中每种类型都继承自基类型 `object`。

另一个有用的与类型相关的运算符是 `cast`（强制转换）运算符 `as`。它将引用类型的变量强制转换为指定类型。如果指定类型与变量不兼容，即如果变量不是给定类型（在类型继承层级中），则其值评估为 `null`。

表达式 `managerOrg1[0] as Manager` 将成功将 `managerOrg1[0]` 强制转换为 `Manager` 类型，而 `managerOrg1[0] as Worker` 的结果将是 `null`。

现代 C# 允许在 `is` 表达式中指定强制转换变量的名称。例如，

```csharp
Console.WriteLine($"{((managerOrg1[0] is Manager mgr)) ? mgr.Manage() : "I am not a manager"}");
Console.WriteLine($"{((managerOrg1[0] is Worker wkr)) ? wkr.Work() : "I am not a worker"}");
```

这两个语句将输出以下内容：

I just manage and I get paid 1000000 dollars.
I am not a worker

