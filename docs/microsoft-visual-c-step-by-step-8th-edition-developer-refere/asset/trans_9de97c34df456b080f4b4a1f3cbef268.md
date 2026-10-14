

{
    return true;
}
else
{
    return this.methodToDetectCanExecute();
}
}

请注意，如果 ViewModel 为构造函数中的 *methodToDetectCanExecute* 参数提供 *null* 引用，则默认操作是假设命令可以运行，并且 *CanExecute* 方法返回 *true*。

## 8. 向 Command 类添加公共 CanExecuteChanged 事件：

Click here to view code image

```
public Command : ICommand
{
    ...
    public bool CanExecute(object parameter)
    {
        ...
    }

    public event EventHandler CanExecuteChanged;
}
```

当将命令绑定到控件时，控件会自动订阅此事件。如果 ViewModel 的状态已更新并且 *CanExecute* 方法返回的值发生变化，则应由 *Command* 对象引发此事件。最简单的策略是使用计时器每隔一秒左右引发一次 *CanExecuteChanged* 事件。然后控件可以调用 *CanExecute* 来确定命令是否仍可执行，并根据结果采取步骤启用或禁用自身。

## 9. 在文件顶部的列表中添加下面所示的 using 指令：

```
using Windows.UI.Xaml;
```

## 10. 在构造函数上方以粗体显示的以下字段添加到 Command 类中：

Click here to view code image

```
public class Command : ICommand
{
    ...
    private Func<bool> methodToDetectCanExecute = null;
    private DispatcherTimer canExecuteChangedEventTimer = null;

    public Command(Action methodToExecute,
        Func<bool> methodToDetectCanExecute)
```

```
{
    ...
}
}
```

DispatcherTimer 类定义在 Windows.UI.Xaml 命名空间中，实现了一个可以在指定间隔引发事件的计时器。你将使用 canExecuteChangedEventTimer 字段以一秒间隔触发 CanExecuteChanged 事件。

## 11. 将以下代码中以粗体显示的 canExecuteChangedEventTimer_Tick 方法添加到 Command 类的末尾：

Click here to view code image

```
public class Command : ICommand
{
    ...
    public event EventHandler CanExecuteChanged;

    void canExecuteChangedEventTimer_Tick(object sender, object e)
    {
        if (this.CanExecuteChanged != null)
        {
            this.CanExecuteChanged(this, EventArgs.Empty);
        }
    }
}
```

此方法仅在至少有一个控件绑定到命令时引发 CanExecuteChanged 事件。严格来说，此方法在引发事件之前还应检查对象的状态是否已更改。但是，你将把计时器间隔设置为较长的时间，以最大程度地减少不检查状态更改而产生的任何效率低下。

## 12. 在 Command 构造函数中添加以下以粗体显示的语句。

Click here to view code image

```
public class Command : ICommand
{
    ...
    public Command(Action methodToExecute, Func<bool> methodToDetectCanExecute)
    {
        this.methodToExecute = methodToExecute;
        this.methodToDetectCanExecute = methodToDetectCanExecute;

        this.canExecuteChangedEventTimer = new DispatcherTimer();
        this.canExecuteChangedEventTimer.Tick += canExecuteChangedEventTimer_Tick;
        this.canExecuteChangedEventTimer.Interval = new TimeSpan(0, 0, 1);
        this.canExecuteChangedEventTimer.Start();
    }
```

```
}
...
}
```

此代码启动 *DispatcherTimer* 对象并将计时器事件的间隔设置为一秒，然后启动计时器。

- 13. 在 Build 菜单上，单击 Build Solution 并确保你的应用在没有错误的情况下构建。

你现在可以使用 *Command* 类向 *ViewModel* 类添加命令。在下一个练习中，你将定义命令以使用户能够在视图中在客户之间移动。

# 向 *ViewModel* 类添加 *NextCustomer* 和 *PreviousCustomer* 命令

- 1. 在 Visual Studio 中，在代码和文本编辑器窗口中打开 ViewModel.cs 文件。

- 2. 在文件顶部添加以下 *using* 指令，并修改 *ViewModel* 类的定义以实现 *INotifyPropertyChanged* 接口。

Click here to view code image

```
...
using System.ComponentModel;

namespace Customers
{
    public class ViewModel : INotifyPropertyChanged
    {
        ...
    }
}
```

- 3. 将 *PropertyChanged* 事件和 *OnPropertyChanged* 方法添加到 *ViewModel* 类的末尾。这是你在 *Customer* 类中包含的相同代码。

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged != null)
        {
            PropertyChanged(this,
                new PropertyChangedEventArgs(propertyName));
        }
    }
```

}
}

请记住，视图通过数据绑定表达式引用数据，这些表达式用于其包含的各种控件。当 ViewModel 类移动到不同的客户时，它必须引发 PropertyChanged 事件以通知视图要显示的数据已更改。

- 4. 在构造函数之后立即将以下字段和属性添加到 ViewModel 类：

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public ViewModel()
    {
        ...
    }

    private bool _isAtStart;
    public bool IsAtStart
    {
        get { return this._isAtStart; }
        set
        {
            this._isAtStart = value;
            this.OnPropertyChanged(nameof(IsAtStart));
        }
    }

    private bool _isAtEnd;
    public bool IsAtEnd
    {
        get { return this._isAtEnd; }
        set
        {
            this._isAtEnd = value;
            this.OnPropertyChanged(nameof(IsAtEnd));
        }
    }
    ...
}
```

你将使用这两个属性来跟踪 ViewModel 的状态。当 ViewModel 中的 currentCustomer 字段位于 customers 集合的开头时，IsAtStart 属性将被设置为 true，而当 ViewModel 位于 customers 集合的末尾时，IsAtEnd 属性将被设置为 true。

- 5. 修改构造函数以设置 IsAtStart 和 IsAtEnd 属性，如下所示以粗体显示。：

Click here to view code image

```
public ViewModel()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.customers = new List<Customer>
    ...
}
```

- 6. 在 Current 属性之后，将以下以粗体显示的 Next 和 Previous 私有方法添加到 ViewModel 类：

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    ...
    public Customer Current
    {
        ...
    }
    private void Next()
    {
        if (this.customers.Count - 1 > this.currentCustomer)
        {
            this.currentCustomer++;
            this.OnPropertyChanged(nameof(Current));
            this.IsAtStart = false;
            this.IsAtEnd =
                (this.customers.Count - 1 == this.currentCustomer);
        }
    }
    private void Previous()
    {
        if (this.currentCustomer > 0)
        {
            this.currentCustomer--;
            this.OnPropertyChanged(nameof(Current));
            this.IsAtEnd = false;
            this.IsAtStart = (this.currentCustomer == 0);
        }
    }
    ...
}
```

# Note

Count 属性返回集合中的项目数，但请记住，集合中的项目编号从 0 到 Count − 1。

这些方法更新 currentCustomer 变量以引用 customers 列表中的下一个（或上一个）客户。请注意，这些方法维护 IsAtStart 和 IsAtEnd 属性的值，并通过为 Current 属性引发 PropertyChanged 事件来指示当前客户已更改。这些方法是私有的，因为它们不应从 ViewModel 类外部访问。外部类将通过命令运行这些方法，你将在以下步骤中添加这些命令。

- 7. 将 NextCustomer 和 PreviousCustomer 自动属性添加到 ViewModel 类，如下所示以粗体显示：

Click here to view code image

```
public class ViewModel : INotifyPropertyChanged
{
    private List<Customer> customers;
    private int currentCustomer;
    public Command NextCustomer { get; private set; }
    public Command PreviousCustomer { get; private set; }
    ...
}
```

视图将绑定到这些 Command 对象，以便用户可以在客户之间导航。

- 8. 在 ViewModel 构造函数中，将 NextCustomer 和 PreviousCustomer 属性设置为引用新的 Command 对象，如下所示：

Click here to view code image

```
public ViewModel()
{
    this.currentCustomer = 0;
    this.IsAtStart = true;
    this.IsAtEnd = false;
    this.NextCustomer = new Command(this.Next, () =>
        { return this.customers.Count > 1 && !this.IsAtEnd; });
    this.PreviousCustomer = new Command(this.Previous, () =>
        { return this.customers.Count > 0 && !this.IsAtStart; });
    ...
}
```

NextCustomer 命令指定 Next 方法作为在调用 Execute 方法时要执行的操作。lambda 表达式 () =>

