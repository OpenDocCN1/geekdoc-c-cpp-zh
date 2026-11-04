

## 静态与实例

不同类型的成员可以与类型的实例或类型本身相关联。这正是 static 修饰符发挥作用的地方，它允许将成员与类型而非各个实例关联。或者换个角度看，类型的静态成员在所有实例之间共享，而实例成员可以与单个实例关联并对其进行操作。事实上，这种共享视角正是 Visual Basic 呈现静态成员的方式，它使用 Shared 关键字而不是 C# 的 static。

如前所述，类允许将状态和操作捆绑在一个概念中，这与面向对象编程原则紧密一致。在考虑共享静态成员的概念时，这两方面同样适用。到目前为止，我们编写的每个程序的入口点都使用了 static 关键字来表示操作：

```csharp
class Program
{
    static void Main(string[] args)
    {
        ...
    }
}
```

## 用于常见任务的代码片段

Visual Studio 有一个名为“代码片段”的功能，允许通过快捷键插入模板化的代码片段。由于声明 Main 方法很常见，产品中包含针对不同 Main 方法定义的代码片段。例如，要插入“static void Main”，可以键入 `svm` 并按两次 Tab 键。而 `sim` 片段用于插入返回类型为 int 的 Main 方法。

对于 Main 方法的声明来说，此功能的价值相当有限；毕竟，创建可执行项目从一开始就包含了入口点声明。然而，对于其他模式，例如各种语句或成员，代码片段非常方便。例如，你可以使用 `ctor` 在类型上插入构造函数。

注意，Main 方法上省略访问修饰符是允许的，因为它会受到运行时的特殊对待。在我们的示例中，关键重要的一点是 Main 方法在 Program 的所有实例之间共享。事实上，你通常甚至不会创建 Program 类的实例。现在让我们尝试向 Program 类添加另一个方法并从 Main 调用它，如下所示：

```csharp
class Program
{
    static void Main(string[] args)
    {
        if (args.Length != 1)
        {
            PrintUsage();
            return;
        }
    }

    void PrintUsage()
    {
        Console.WriteLine("Usage:  sample.exe <file*>");
    }
}
```

上述代码无法编译，因为 PrintUsage 未声明为 static。由于静态成员与实例无关，它们无法访问实例成员（如果未指定目标实例）。图 9.17 在错误列表中指出了这个代码缺陷。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_520_0.png)

图 9.17 静态成员不能直接调用实例成员。

将 PrintUsage 方法声明为 static 将解决此问题。对于存储状态（保存在所谓的字段中）的使用，也有类似的说明。我们将在后面更详细地介绍方法、字段和其他成员，但可以说，字段涵盖类型的数据和状态方面，而方法处理操作行为。下面是一个利用静态字段的单例类示例。这使我们能够同时解释多个概念。

- 类实例的概念
- 使用构造函数创建实例
- 回顾成员的可见性方面
- 静态成员和字段的使用

由于此示例仅用于为后续探索做铺垫，我们不会深入探讨面向对象的概念（这些将在第 14 章中介绍）。

```csharp
sealed class PaymentService
{
    private static PaymentService s_service;
    private Queue<Payment> _payments;

    private PaymentService()
    {
        // This is a private constructor; therefore it can only
        // be called from inside the PaymentService type.
        _payments = new Queue<Payment>();
    }

    public static PaymentService Service
    {
        get
        {
            // Create service the first time it's requested. For
            // the remainder of the program's lifetime we'll be
            // using this singleton instance.
            if (s_service == null)
            {
                s_service = new PaymentService();
            }

            return s_service;
        }
    }

    public void SchedulePayment(int fromAccount, int toAccount, decimal amount)
    {
        _payments.Enqueue(new Payment(fromAccount, toAccount, amount));
    }
}
```

PaymentService 的设计意图是成为一个单例，这意味着程序中只能存在它的一个实例。在稍微灵活的设置中，你可能希望控制给定类型可创建的实例数量。要避免创建类的任意实例，首先要确保没有人可以调用构造函数。实例构造函数是创建类实例的一种方式；稍后你会看到静态构造函数也存在，允许初始化静态状态。

```csharp
private PaymentService()
{
    // This is a private constructor; therefore it can only
    // be called from inside the PaymentService type.
    _payments = new Queue<Payment>();
}
```

它们看起来像方法，但根据你的视角，它们要么缺少名称，要么缺少返回类型。一种看法是，它是一个与包含类同名的方法。或者，你也可以说它没有名称，而返回类型就是包含类。

由于前面的构造函数上没有 static 关键字，它是一个实例构造函数，可以使用 new 关键字调用，正如我们在 Service 属性中看到的那样。由于它声明为 private 访问修饰符，因此唯一有效的调用位置是在同一个类内部。注意，构造函数确实会初始化保存在 _payments 字段中的每个实例状态。下划线前缀的命名约定是一种广泛使用的模式，用于识别字段（而不是局部变量或参数等）。

```csharp
private Queue<Payment> _payments;
```

Service 属性声明为 public 和 static，因此调用它的方式如下，“点入类型”：

```csharp
PaymentService theOneAndOnlyInstance = PaymentService.Service;
```

在内部，此属性通过检查静态字段 s_service 来判断是否已经创建了该类型的单个实例。在类型的所有实例中，这样的字段只有一个，这正是允许我们强制执行单例策略的原因：

```csharp
public static PaymentService Service
{
    get
    {
        // Create service the first time it's requested. For
        // the remainder of the program's lifetime we'll be
        // using this singleton instance.
        if (s_service == null)
        {
            s_service = new PaymentService();
        }

        return s_service;
    }
}
```

同样，使用 s_ 前缀来表示静态字段纯粹是一种约定，你可以选择采用或不采用（但如果采用，请在整个代码库中保持一致）。

从用户的角度来看，处理单例并调用 SchedulePayment 现在看起来像这样：

```csharp
// Static members are called with the type (name) as the left-hand side.
var service = PaymentService.Service;
```

```csharp
// Instance members are called with an instance as the left-hand side.
service.SchedulePayment(123, 321, 456.78m);
```

通过调用 Service 属性创建了我们唯一的权威支付服务实例后，我们可以调用实例成员，例如这里显示的方法：

```csharp
public void SchedulePayment(int fromAccount, int toAccount, decimal amount)
{
    _payments.Enqueue(new Payment(fromAccount, toAccount, amount));
}
```

该方法现在操作的是实例数据（在此特定情况下是 _payments 字段）。在 PaymentService 的每个实例中（在我们的例子中，被小心地控制为仅一个），都存在这样一份 _payments 数据。

几乎所有类型的成员都可以用于静态级别或实例级别。在前面的示例中，我们看到了一个实例构造函数和一个实例方法，以及一个静态属性。

### 为什么要使用单例？

你可能会想，如果可以把所有操作和状态都设为静态，为什么还要费心使用单例实例呢？例如，在我们的代码中，我们可以创建一个静态的 SchedulePayment 方法，在内部使用一个静态字段来存储支付信息。虽然确实如此，但在某些情况下，使用单例可以带来更清晰的整体设计。一种情况是，你希望返回的单例对象遵守某个接口契约，而该契约只存在于实例成员中。因此，在这种情况下，你必须有一个实例。

与此相关的是工厂模式，即你想要创建一个静态方法来构造给定类型的对象。然而，由于面向对象的原则，你可以在工厂方法内部返回一个子类型的实例：

```csharp
static Animal CreateAnimal(int legs, ...)
{
    if (legs == 0 && ...) return new Fish();
    else ...
}
```

