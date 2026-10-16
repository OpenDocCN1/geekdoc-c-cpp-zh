

> **注意** 只要类型是委托，你就可以在任何地方使用 lambda 表达式。lambda 表达式的另一种用途是当类型为 Expression 或 Expression<T> 时，此时编译器会创建表达式树。此特性将在第13章“语言集成查询”中讨论。

## 事件

事件基于委托，并为委托提供发布/订阅机制。在整个框架中，事件无处不在。在 Windows 应用程序中，Button 类提供了 Click 事件。这类事件是一个委托。需要定义一个处理程序方法，该方法在 Click 事件被触发时调用，其参数由委托类型定义。

在本节所示的代码示例中，事件用于连接 CarDealer 和 Consumer 类。CarDealer 类在新车到达时提供一个事件。Consumer 类订阅该事件，以便在新车到达时得到通知。

### 事件发布者

首先从一个基于事件提供订阅的 CarDealer 类开始。CarDealer 使用 event 关键字定义了名为 NewCarInfo 的事件，其类型为 EventHandler<CarInfoEventArgs>。在 NewCar 方法内部，通过调用 RaiseNewCarInfo 方法来触发 NewCarInfo 事件。该方法的实现会验证委托是否为非空，然后引发事件（代码文件 EventsSample/CarDealer.cs）：

```csharp
using static System.Console;
using System;

namespace Wrox.ProCSharp.Delegates
{
    public class CarInfoEventArgs: EventArgs
    {
        public CarInfoEventArgs(string car)
        {
            Car = car;
        }

        public string Car { get; }
    }

    public class CarDealer
    {
        public event EventHandler<CarInfoEventArgs> NewCarInfo;

        public void NewCar(string car)
        {
            WriteLine($"CarDealer, new car {car}");

            NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
```

> **注意** 上一个示例中使用的 null 传播运算符 ?. 是 C# 6 的新特性。该运算符在第8章“运算符和强制转换”中讨论。

CarDealer 类提供了类型为 EventHandler<CarInfoEventArgs> 的 NewCarInfo 事件。按照约定，事件通常使用带有两个参数的方法；第一个参数是 object 类型，包含事件的发送者；第二个参数提供有关事件的信息。第二个参数因事件类型而异。.NET 1.0 为所有不同数据类型的事件定义了数百个委托。有了泛型委托 EventHandler<T>，就不再需要这样做了。EventHandler<TEventArgs> 定义了一个返回 void 且接受两个参数的处理程序。对于 EventHandler<TEventArgs>，第一个参数必须是 object 类型，第二个参数是 T 类型。EventHandler<TEventArgs> 还对 T 定义了一个约束；它必须派生自基类 EventArgs，CarInfoEventArgs 正是如此：

```csharp
public event EventHandler<CarInfoEventArgs> NewCarInfo;
```

委托 EventHandler<TEventArgs> 定义如下：

```csharp
public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e)
    where TEventArgs : EventArgs;
```

用一行定义事件是 C# 的简写形式。编译器会创建一个委托类型 EventHandler<CarInfoEventArgs> 的变量，并添加用于订阅和取消订阅该委托的方法。下面显示了该简写形式的完整写法。这与自动属性和完整属性非常相似。对于事件，使用 add 和 remove 关键字来向委托添加和移除处理程序：

```csharp
private EventHandler<CarInfoEventArgs> newCarInfo;
public event EventHandler<CarInfoEventArgs> NewCarInfo
{
    add
    {
        newCarInfo += value;
    }
    remove
    {
        newCarInfo -= value;
    }
}
```

> **注意** 如果除了添加和移除事件处理程序之外还需要做更多事情，例如为多线程访问添加同步，那么定义事件的完整写法很有用。WPF 控件使用完整写法为事件添加冒泡和隧道功能。你可以在第29章“核心 XAML”中阅读更多关于事件冒泡和隧道事件的内容。

`CarDealer` 类通过调用委托的 `Invoke` 方法来触发事件。这会调用订阅该事件的所有处理程序。请记住，如前面对多播委托所展示的，调用方法的顺序是不保证的。为了对调用处理程序方法有更多控制，可以使用 `Delegate` 类的 `GetInvocationList` 方法来访问委托列表中的每一项，并单独调用每一项，如前所示。

```csharp
NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
```

触发事件仅需一行代码。然而，这只有 C# 6 才有。在 C# 6 之前，触发事件要更复杂。下面是 C# 6 之前实现的相同功能。触发事件之前，你需要检查事件是否为 null。由于在 null 检查和触发事件之间，事件可能被另一个线程设置为 null，因此使用了一个局部变量，如下例所示：

```csharp
EventHandler<CarInfoEventArgs> newCarInfo = NewCarInfo;
if (newCarInfo != null)
{
    newCarInfo(this, new CarInfoEventArgs(car));
}
```

使用 C# 6，所有这些都可以通过 null 传播替换为一行代码，正如你之前所看到的。

在触发事件之前，有必要检查委托 `NewCarInfo` 是否为 `null`。如果没有人订阅，该委托就是 `null`：

```csharp
protected virtual void RaiseNewCarInfo(string car)
{
    NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
}
```

### 事件监听器

`Consumer` 类用作事件监听器。该类订阅 `CarDealer` 的事件，并定义了 `NewCarIsHere` 方法，该方法满足 `EventHandler<CarInfoEventArgs>` 委托的要求，参数类型为 `object` 和 `CarInfoEventArgs`（代码文件 `EventsSample/Consumer.cs`）：

```csharp
using static System.Console;

namespace Wrox.ProCSharp.Delegates
{
    public class Consumer
```

使用事件时，发布者和监听器是直接连接的。这可能会给垃圾回收带来问题。例如，如果某个监听器不再被直接引用，发布者仍然持有对它的引用。垃圾回收器无法清理监听器的内存，因为发布者仍然持有引用并向监听器触发事件。

这种强连接可以通过使用弱事件模式，并使用 `WeakEventManager<T>` 作为发布者和监听器之间的中介来解决。

本节对前面的以 `CarDealer` 为发布者、`Consumer` 为监听器的示例进行了修改，以使用弱事件模式。

`WeakEventManager<T>` 定义在 `System.Windows` 程序集中，该程序集不属于 .NET Core。此示例是使用 .NET Framework 4.6 控制台应用程序完成的，不能在其他平台上运行。

> **注意** 对于动态创建的订阅者，为了避免资源泄漏的危险，你需要特别注意事件。也就是说，你需要确保在订阅者超出作用域（不再需要）之前取消订阅事件，或者使用弱事件。事件通常是应用程序中内存泄漏的一个原因，因为订阅者的作用域很长，因此源对象也无法被垃圾回收。

使用弱事件时，事件发布者（示例代码中的 `CarDealer` 类）不需要更改。无论使用紧密耦合的事件还是弱事件，实现都是相同的。不同的是消费者的实现。消费者需要实现接口 `IWeakEventListener`。该接口定义了方法 `ReceiveWeakEvent`，当事件到达时，弱事件管理器会调用该方法。该方法实现充当代理，进而调用 `NewCarIsHere` 方法（代码文件 `WeakEvents/Consumer.cs`）：

```csharp
using System;
using static System.Console;
using System.Windows;

namespace Wrox.ProCSharp.Delegates
{
    public class Consumer: IWeakEventListener
    {
        private string _name;

        public Consumer(string name)
        {
            this._name = name;
        }

        public void NewCarIsHere(object sender, CarInfoEventArgs e)
```

