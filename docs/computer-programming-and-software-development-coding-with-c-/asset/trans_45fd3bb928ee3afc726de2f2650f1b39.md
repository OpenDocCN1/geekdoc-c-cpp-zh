

一个重要的旁注，静态字段不能通过对象访问。你必须始终通过类来访问。我会在演示中向你展示这一点。创建静态成员并不仅限于静态字段，所以我们可以做的不止于静态变量。

```
public class Employee
{
    public static double bonusPercentage = 0.15;
    public static void IncreaseBonusPercentage(double newPercentage)
    {
        bonusPercentage = newPercentage;
    }
}
```

在这里你可以看到我正在创建一个静态方法。这是一个有趣的方面。为什么我们要这样做呢？好吧，记住我之前说过的关于 static 的，它是定义在类上，而不是定义在对象上。这意味着该方法本身可以直接通过类使用，所以我不需要实例化一个对象来访问这个方法，我可以直接在类上调用它。这就是这里发生的事情。我现在正在调用静态方法，并且请注意，我是在 Employee 上调用它的，也就是类名、类型，而没有先实例化对象。这不是我们迄今为止所做的事情。通常，我们首先创建类型的对象。

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        PrintAllEmployeeList();
    }

    public static void PrintAllEmployeeList()
    {
        ...
    }
}
```
```

在定义静态方法时，你直接在类上调用该方法。我确实答应过你一个解释，关于为什么我们在本书前面使用的那些方法使用了 static。好吧，这里就是了。我们创建了可以从 Main 调用的方法。请注意，Main 方法，也就是由 C# 自动调用的那个方法，也是静态的。这其实相当合乎逻辑。该方法需要在没有创建对象的情况下由运行时调用。从静态方法中，你不能调用方法。原因相同，没有对象可以调用它。所以我们有静态的 Main，并且从中我们直接调用了一些方法。由于 Main 是静态的，我们在 Program 类上调用的方法也必须为静态。从静态方法中，我们可以直接调用其他静态方法。或者，正如我们在本书中经常做的那样，我们也可以创建一个对象并在这些对象上调用方法。static 可能有点令人困惑，所以让我们回到 Visual Studio 看看实际效果。我将向你展示如何添加静态字段以及静态方法。然后我们将使用这些静态成员。Static

意味着共享。它指向存储在类级别而不是对象级别的数据。它在该类的所有对象之间共享。例如，想想 taxRate。taxRate 并不是绑定到某个特定员工的。它绑定到所有员工。是一样的。

```
9   public class Employee
10  {
11      private string firstName;
12      private string lastName;
13      private string email;
14
15      private int numberOfHoursWorked;
16      private double wage;
17      private double hourlyRate;
18      private DateTime birthDay;
19
20      private EmployeeType employeeType;
21
22      public string FirstName
23      {
24          get
25          {
26              return firstName;
27          }
28          set
29          {
30              firstName = value;
31          }
32      }
33
34      public string LastName
35      {
```

它在所有员工之间共享。让每个 Employee 实例都包含该值是没有用的。我们更希望该值在类级别共享，而这正是我们可以做到的。它是静态的。所以我要引入一个 public static double taxRate，并将其设置为 0.15。我将更新 ReceiveWage 方法。在 ReceiveWage 中，我现在不是直接计算工资，我将引入一个本地的 wageBeforeTax。然后我将计算 taxAmount。最后，我说 Wage，也就是属性，等于是 wageBeforeTax 减去 taxAmount。ReceiveWage 方法现在使用了该 taxRate。所以这是静态数据，我们在这里定义的静态 double 值。

它已经在类级别定义，并且在对象之间共享。我还将更新 DisplayEmployeeDetails 方法。我将更新它，使其也显示 taxRate。我会在一分钟后向你展示原因。现在让我们回到 Program 类。在这里，我们仍然有大约两个对象，Bethany 和 George，我们在 Bethany 对象上调用 PerformWork 几次，然后调用 ReceiveWage，然后执行 DisplayEmployeeDetails。

```
19
20 private EmployeeType employeeType;
21 public static double taxRate = 0.15;
22
23 4 references
24 public string FirstName
25 {
26     get
27     {
28         return firstName;
29     }
30     set
31     {
32         firstName = value;
33     }
34 }
```

ReceiveWage 也将使用该 taxRate，而该 taxRate 在所有对象之间共享，即在 Bethany 和 George 之间。这些对象将使用同一个 taxRate，它存储在类上。我不会在员工本身上指定 taxRate。所以让我们运行它，我们现在确实看到 Bethany 和 George 的 taxRate 都是 0.15，并且在 Wage 计算中，这个值也被使用了。静态数据如我所说，是定义在类上，而不是在对象上，这意味着我不能说 bethany.taxRate。你会看到，这个字段 taxRate 不能通过对象使用。如果我想更改它，我仍然可以这样做，如果它是 public 的，这种数据可以被更改。如果我想这样做，我需要调用 employee.taxRate。Employee 是类型的名称，并且确实证明静态数据是定义在类型上的。所以我现在将 taxRate 设置为 0.02。这现在适用于所有对象，对 Bethany、George 以及其他员工都适用。所以，如果我引入一点代码，它会再次要求 Bethany 和 George 执行一些工作，我们会看到这个新的 taxRate 在设置后立即对他们两人适用。所以让我们再次运行应用程序。最初，taxRate 是 0.15，然后我更改它，现在对两个对象都是 0.02。静态数据如前所述，是存储在类上而不是对象上，但它也可以包含静态方法。静态方法也基本上可以通过类类型使用。让我们再次引入一个静态方法。我们之前见过它们，对吧？所以在这里，我引入了一个静态方法，如你所见，它只是一个普通方法，但它再次具有 static 关键字。在这种情况下，它只是返回 void，并且不接受任何参数。它只会向控制台写入一些内容。在静态方法中，我可以使用静态数据。如你所见，我正在访问 taxRate。然而，我不能访问例如 firstName。这里是因为这是一个静态方法。它是定义在类上而不是在对象上。可能没有对象可以查看其 firstName。我不能在这里使用对象数据。我只能使用静态数据。但是我现在可以做的，是通过类调用这个静态方法。所以我可以调用 Employee.DisplayTaxRate，并且它可以在没有创建对象的情况下被调用。所以你会看到，在不使用 Bethany 或 George 对象的情况下，我仍然可以访问静态方法。静态方法只能使用静态数据，并且它也只能调用静态方法，这现在可能让你想起一件事。如果你回顾 Program 类，在这里，我们有 Static void Main。这对 C# 来说是一个已知的方法，并且它实际上是静态的，因为此时实际上还没有对象。

![](img/0155736aec718cf18821e9f10a5d308d_806_0.png)

当应用程序启动时，Main 将在 Program 类上被调用。它实际上是一个在没有对象实例的情况下被调用的静态方法。从这里，我实际上只能调用其他静态方法。这就是为什么，在本书前面，当我们从静态的 Main 调用方法时，这些方法需要是静态的。在这里，我们创建对象。并且在这些对象上，我们可以调用我们的常规方法。在 C# 中我们也可以声明一个常量变量值。常量字段确实如其名所示，是一个变量，其值不能被更改。值需要在声明时设置。你之后不能指定值。这样的变量可以使用 const 关键字创建。

```
public class Employee
{
    public const double bonusPercentage = 0.15;//We never want this to change!
}
```

我在这里提到这些的原因是 const 字段在隐式上也是静态的。它们也在类级别声明，因此在类的所有实例之间共享。在这里你可以看到我如何定义一个常量值。定义常量与静态变量非常相似，但现在我们使用 const 关键字。一旦

