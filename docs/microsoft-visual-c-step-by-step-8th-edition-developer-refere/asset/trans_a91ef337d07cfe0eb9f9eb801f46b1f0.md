

IDisposable 接口，如下所示以粗体显示：

Click here to view code image

```
class Calculator : IDisposable
{
    ...
}
```

3. 在 Calculator 类的末尾添加以下方法（名为 Dispose）。该方法由 IDisposable 接口定义：

Click here to view code image

```
class Calculator : IDisposable
{
    ...
    public void Dispose()
    {
        Console.WriteLine("Calculator being disposed");
    }
}
```

你通常会在 Dispose 方法中添加释放对象持有的资源的代码。在本例中没有此类资源，而此方法中 Console.WriteLine 语句的目的只是让你看到 Dispose 方法何时运行。然而，你可以看到在实际应用中，析构函数和 Dispose 方法之间很可能会有代码重复。为了消除这种重复，你通常会将此代码放在一处并从另一处调用它。但由于你不能从 Dispose 方法中显式调用析构函数，因此更合理的做法是从析构函数中调用 Dispose 方法，并将释放资源的逻辑放在 Dispose 方法中。

4. 修改析构函数，使其调用 Dispose 方法，如以下代码中以粗体所示。（在终结器中保留显示消息的语句，以便你可以看到垃圾回收器何时运行它）。

Click here to view code image

```
~Calculator()
{
    Console.WriteLine("Calculator being finalized");
    this.Dispose();
}
```

当你想在应用程序中销毁 Calculator 对象时，Dispose 方法不会自动运行；你的代码必须显式调用它（例如使用 calculator.Dispose() 语句）或在 using 语句中创建 Calculator 对象。在你的程序中，你将采用后一种方法。

## 5. 在代码和文本编辑器窗口中显示 Program.cs 文件。修改 Main 方法中创建 Calculator 对象并调用 Divide 方法的语句，如下所示以粗体显示：

Click here to view code image

```
static void Main(string[] args)
{
    using (Calculator calculator = new Calculator())
    {
        Console.WriteLine($"120 / 15 = {calculator.Divide(120, 15)}");
    }

    Console.WriteLine("Program finishing");
}
```

## 6. 在 Debug 菜单上，单击 Start Without Debugging。验证程序现在是否显示以下一系列消息：

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
Calculator being finalized
Calculator being disposed
```

using 语句会导致在显示“Program finishing”消息的语句之前运行 Dispose 方法。然而，你可以看到 Calculator 对象的析构函数在应用程序结束时仍然运行，并且它再次调用 Dispose 方法。这显然是处理上的浪费。

## 7. 在控制台窗口中，按 Enter 键并返回到 Visual Studio 2015。

多次释放对象持有的资源可能不会造成灾难，但绝对不是良好的做法。解决此问题的推荐方法是向类中添加一个私有 Boolean 字段，以指示 Dispose 方法是否已被调用，然后在 Dispose 方法中检查该字段。

### 防止对象被多次释放

- 1. 在代码和文本编辑器窗口中显示 Calculator.cs 文件。
- 2. 向 Calculator 类添加一个名为 disposed 的私有 Boolean 字段，并将该字段的值初始化为 false，如下所示以粗体显示：

Click here to view code image

```
class Calculator : IDisposable
{
    private bool disposed = false;
```

该字段的目的是跟踪此对象的状态并指示 Dispose 方法是否已被调用。

3. 修改 Dispose 方法中的代码，仅在 disposed 字段为 false 时显示消息。显示消息后，将 disposed 字段设置为 true，如下所示以粗体演示：

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
}
```

4. 在 Debug 菜单上，单击 Start Without Debugging。注意程序现在显示以下一系列消息：

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
Calculator being finalized
```

Calculator 对象现在只被丢弃一次，但析构函数仍然在运行。同样，这是一种浪费；对于已经释放了其资源的对象，运行析构函数意义不大。

5. 在控制台窗口中，按 Enter 键并返回到 Visual Studio 2015。

6. 在 Calculator 类中，在 Dispose 方法的末尾添加以下以粗体显示的语句：

Click here to view code image

```
public void Dispose()
{
    if (!this.disposed)
    {
        Console.WriteLine("Calculator being disposed");
    }
    this.disposed = true;
    GC.SuppressFinalize(this);
}
```

GC 类提供了对垃圾回收器的访问，并实现了多个静态方法，可用于控制其执行的部分操作。使用 SuppressFinalize 方法，你可以指示垃圾回收器不对指定的对象执行终结，从而防止析构函数运行。

### Important

GC 类公开了多个可用于配置垃圾回收器的方法。然而，通常最好让 CLR 自行管理垃圾回收器，因为如果你不慎调用这些方法，可能会严重损害应用程序的性能。你应极其谨慎地对待 SuppressFinalize 方法，因为如果你未能释放对象，就有丢失数据的风险（例如，如果你未能正确关闭文件，内存中缓冲但尚未写入磁盘的任何数据都可能丢失）。只有在你确信对象已被丢弃的情况下，例如本练习中所示的情况，才应调用此方法。

7. 在 Debug 菜单上，单击 Start Without Debugging。注意程序现在显示以下一系列消息：

```
Calculator being created
120 / 15 = 8
Calculator being disposed
Program finishing
```

你可以看到析构函数不再运行，因为 Calculator 对象在程序结束前已被释放。

8. 在控制台窗口中，按 Enter 键并返回到 Visual Studio 2015。

### 线程安全和 Dispose 方法

使用 disposed 字段防止对象被多次丢弃的示例在大多数情况下效果良好，但请记住你无法控制终结器的运行时间。在本章的练习中，它一直是在程序结束时执行，但这可能并非总是如此——它可以在最后一次引用对象消失后的任何时间运行。因此，垃圾回收器可能在自己的线程上调用终结器，而 Dispose 方法正在运行中，尤其是在 Dispose 方法需要执行大量工作时。你可以通过将设置 disposed 字段为 true 的语句移至 Dispose 方法的开头来降低资源被多次释放的可能性，但在这种情况下，如果在设置此变量后但在释放资源之前发生异常，你就有可能根本不释放资源。

为了完全消除两个并发线程同时释放同一对象中相同资源的可能性，你可以通过将代码嵌入到 C# lock 语句中以线程安全的方式编写代码，如下所示：

Click here to view code image

```
public void Dispose()
{
    lock(this)
    {
        if (!disposed)
        {
            Console.WriteLine("Calculator being disposed");
        }
        this.disposed = true;
        GC.SuppressFinalize(this);
    }
}
```

lock 语句的目的是防止同一块代码在不同线程上同时运行。lock 语句的参数（前述示例中的 this）应是对对象的引用。大括号之间的代码定义了 lock 语句的作用域。当执行到达 lock 语句时，如果指定的对象当前已被锁定，则请求锁定的线程将被阻塞，代码在此点暂停。当当前持有锁的线程到达 lock 语句的闭合大括号时，锁将被释放，使阻塞的线程能够获取锁并继续。然而，到那时 disposed 字段将被设置为 true，因此第二个线程不会尝试执行 if (!disposed) 块中的代码。

以这种方式使用锁是安全的，但可能会影响性能。另一种方法是使用本章前面描述的策略，即仅抑制托管资源的重复释放。（多次释放托管资源不是异常安全的；你不会危及计算机的安全，但如果你尝试释放不再存在的托管对象，可能会影响应用程序的逻辑完整性。）该策略实现了 Dispose 方法的重载版本；using 语句调用 Dispose()，它反过来运行语句 Dispose(true)，而析构函数调用 Dispose(false)。仅当重载版本的 Dispose 方法的参数为 true 时，才会释放托管资源。有关更多信息，请参考“从析构函数调用 dispose 方法”部分中的示例。

