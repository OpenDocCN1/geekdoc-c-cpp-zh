
你还可以对 `ProfilingComponent` 类做一个进一步的修改：使其透明地记录分析结果。首先，你需要将秒表代码抽象到一个接口之后，以便可以提供多个实现，包括装饰器。这是朝着更好的职责分离重构时常见的第一步。清单 5-28 显示了这一中间步骤。

### LISTING 5-28 在实现装饰器之前，必须用接口替换具体实现。

Click here to view code image

``` 
public class ProfilingComponent : IComponent
{
    public ProfilingComponent(IComponent decoratedComponent, IStopwatch stopwatch)
    {
        this.decoratedComponent = decoratedComponent;
        this.stopwatch = stopwatch;
    }
    public void Something()
    {
        stopwatch.Start();
        decoratedComponent.Something();
        var elapsedMilliseconds = stopwatch.Stop();
        Console.WriteLine("The method took {0} seconds to complete", elapsedMilliseconds
/
1000);
    }
    private readonly IComponent decoratedComponent;
    private readonly IStopwatch stopwatch;
}
```

现在 `ProfilingComponent` 类不再直接依赖 `System.Diagnostics.Stopwatch` 类，你可以改变 `IStopwatch` 类的实现方式。创建了一个 `LoggingStopwatch` 装饰器，如清单 5-29 所示，以为任何进一步的 `IStopwatch` 实现增强日志功能。

### LISTING 5-29 LoggingStopwatch 装饰器是一个实现 IStopwatch 并进行日志记录和委托的实现。

Click here to view code image

``` 
public class LoggingStopwatch : IStopwatch
{
    public LoggingStopwatch(IStopwatch decoratedStopwatch)
    {
        this.decoratedStopwatch = decoratedStopwatch;
    }
    public void Start()
    {
        decoratedStopwatch.Start();
        Console.WriteLine("Stopwatch started...");
    }
    public long Stop()
    {
        var elapsedMilliseconds = decoratedStopwatch.Stop();
        Console.WriteLine("Stopwatch stopped after {0} seconds", TimeSpan.FromMilliseconds(elapsedMilliseconds).TotalSeconds);
        return elapsedMilliseconds;
    }
    private readonly IStopwatch decoratedStopwatch;
}
```

当然，你需要一个非装饰器的 `IStopwatch` 接口实现——一个充当真实秒表的作用。这只是委托给 `.NET Framework` 的 `System.Diagnostics.Stopwatch` 类的情况，如清单 5-30 所示。

### LISTING 5-30 主要的 IStopwatch 实现使用 Stopwatch 类。

Click here to view code image

``` 
public class StopwatchAdapter : IStopwatch
{
    public StopwatchAdapter(Stopwatch stopwatch)
    {
        this.stopwatch = stopwatch;
    }
    public void Start()
    {
        stopwatch.Start();
    }
    public long Stop()
    {
        stopwatch.Stop();
        var elapsedMilliseconds = stopwatch.ElapsedMilliseconds;
        stopwatch.Reset();
        return elapsedMilliseconds;
    }
    private readonly Stopwatch stopwatch;
}
```

请注意，你本可以选择将 `IStopwatch` 实现为 `System.Diagnostics.Stopwatch` 类的子类并使用现有的 `Start` 和 `Stop` 方法。然而，`Start` 方法的作用是在秒表停止时恢复其功能，但你需要做的是在调用 `Stop` 之后调用 `Reset`，并在两者之间获取 `ElapsedMilliseconds` 属性值。这又是适配器模式的另一个例子。

#### 异步装饰器

异步方法是指在与客户端不同的线程上运行的方法。当方法执行时间较长时，这很有用，因为在同步执行期间，客户端在等待被调用方法返回时会阻塞。例如，在使用 `Windows Presentation Foundation (WPF)` 和 `Model-View-ViewModel (MVVM)` 模式的桌面应用程序中，`ViewModels` 绑定到 `View`，并且执行的任何命令都由那些 `ViewModels` 在用户界面线程上同步处理。实际上，这意味着长时间运行的命令会阻塞用户界面，直到命令完成其工作。清单 5-31 显示了这种行为的一个片段。

### LISTING 5-31 在 UI 线程上处理的命令会阻塞它，使 UI 无响应。

[Click here to view code image](#)

``` 
public class MainWindowViewModel : INotifyPropertyChanged
{
    public MainWindowViewModel(IComponent component)
    {
        this.component = component;
        calculateCommand = new RelayCommand(Calculate);
    }
    public string Result
    {
        get
        {
            return result;
        }
        private set
        {
            if (result != value)
            {
                result = value;
                PropertyChanged(this, new PropertyChangedEventArgs("Result"));
            }
        }
    }
    public ICommand CalculateCommand
{
    get
    {
        return calculateCommand;
    }
}
public event PropertyChangedEventHandler PropertyChanged = delegate {};
private void Calculate(object parameter)
{
    Result = "Processing...";
    component.Process();
    Result = "Finished!";
}
private string result;
private IComponent component;
private RelayCommand calculateCommand;
}
```

通过创建异步装饰器，你可以指示被调用方法在单独的线程上执行。这可以通过将工作委托给 `Task` 类来实现，该类成为你的装饰器的依赖项，如清单 5-32 所示。

### LISTING 5-32 用于 WPF 的异步装饰器，使用 Dispatcher 类。

Click here to view code image

``` 
public class AsyncComponent : IComponent
{
    public AsyncComponent(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }
    public void Process()
    {
        Task.Run((Action)decoratedComponent.Process);
    }
    private readonly IComponent decoratedComponent;
}
```

`AsyncComponent` 类存在一个问题：它对 `Task` 类的依赖是隐式的，这意味着很难测试这个类。使用静态依赖进行单元测试代码很困难，因此最好用起重机替换这个 skyhook。

#### 异步装饰器的局限性

并非所有可想象的方法都可以使用装饰器模式来创建客户端不知道的异步版本。事实上，这种方法适用的唯一异步方法就是 fire-and-forget 方法。

fire-and-forget 方法没有返回值，并且客户端不需要知道此类方法何时返回。当它被实现为异步装饰器时，客户端无法知道方法调用何时真正完成，因为调用会立即返回——而实际执行的工作可能仍在进行中。

请求-响应方法是常见的数据检索方法，通常非常适合异步实现，因为它们往往耗时较长并阻塞 UI 线程。客户端需要知道该方法是异步的，以便它们可以显式编码以在异步方法完成后接受回调。因此，请求-响应方法不能通过使用异步装饰器来实现。

#### 装饰属性和事件

到目前为止，你已经了解了如何装饰接口的方法，但属性和事件呢？只要你不使用自动属性或自动事件，这两种语法元素也可以被装饰：你需要显式定义它们才能正确装饰它们。

清单 5-33 显示了属性的手动创建，但对于 getter 和 setter 而言，它没有使用 backing field，而是将调用委托给接口的被装饰实例。

### LISTING 5-33 属性也可以使用装饰器模式，就像方法一样。

Click here to view code image

``` 
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }
    public string Property
    {
        get
        {
            // We can do some mutation here after retrieving the value
            return decoratedComponent.Property;
        }
    }
    set
    {
        // And/or here, before we set the value
        decoratedComponent.Property = value;
    }
}
private readonly IComponent decoratedComponent;
}
```

清单 5-34 显示了事件的手动创建，但对于 adder 和 remover 而言，它没有使用 backing field，而是将调用委托给接口的被装饰实例。

### LISTING 5-34 事件也可以使用装饰器模式，就像方法一样。

Click here to view code image

``` 
public class ComponentDecorator : IComponent
{
    public ComponentDecorator(IComponent decoratedComponent)
    {
        this.decoratedComponent = decoratedComponent;
    }
    public event EventHandler Event
    {
        add
        {
            // We can do something here, when the event handler is registered
            decoratedComponent.Event += value;
        }
        remove
        {
            // And/or here, when the event handler is deregistered
            decoratedComponent.Event -= value;
        }
    }
    private readonly IComponent decoratedComponent;
}
```

#### 使用策略模式代替 switch

要了解策略模式最适合应用的时机，可以查看条件分支的实例。每当你使用 `switch` 语句时，都可以使用策略模式来简化客户端，使其将复杂性委托给依赖接口。清单 5-35 显示了一个可以使用策略模式替换的 `switch` 语句示例。

### LISTING 5-35 此方法使用 switch 语句，但策略模式会更具适应性。

Click here to view code image

``` 
public class OnlineCart
{
    public void CheckOut(PaymentType paymentType)
    {
        switch(paymentType)
        {
            case PaymentType.CreditCard:
                ProcessCreditCardPayment();
                break;
            case PaymentType.Paypal:
                ProcessPaypalPayment();
                break;
            case PaymentType.GoogleCheckout:
                ProcessGooglePayment();
                break;
            case PaymentType.AmazonPayments:
                ProcessAmazonPayment();
                break;
        }
    }
    private void ProcessCreditCardPayment()
    {
        Console.WriteLine("Credit card payment chosen");
    }
    private void ProcessPaypalPayment()
    {
        Console.WriteLine("Paypal payment chosen");
    }
    private void ProcessGooglePayment()
    {
        Console.WriteLine("Google payment chosen");
    }
    private void ProcessAmazonPayment()
    {
        Console.WriteLine("Amazon payment chosen");
    }
}
```
