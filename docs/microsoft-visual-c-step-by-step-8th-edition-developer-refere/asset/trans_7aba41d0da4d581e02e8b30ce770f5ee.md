

Dispose 方法，但至少你可以确定它会被调用，即使只是程序关闭时。你将在本章末尾的练习中详细研究此功能，但这里有一个如何实现 IDisposable 接口的示例：

Click here to view code image

```
class Example : IDisposable
{
    private Resource scarce;      // scarce resource to manage and dispose
    private bool disposed = false; // flag to indicate whether the resource
                                    // has already been disposed
    ...
    ~Example()
    {
        this.Dispose(false);
    }

    public virtual void Dispose()
    {
        this.Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (!this.disposed)
        {
            if (disposing)
            {
                // release large, managed resource here
                ...
            }
            // release unmanaged resources here
            ...
            this.disposed = true;
        }
    }

    public void SomeBehavior() // example method
    {
        checkIfDisposed();
        ...
    }

    ...

    private void checkIfDisposed()
    {
        if (this.disposed)
        {
            throw new ObjectDisposedException("Example: object has been disposed of");
        }
    }
```

注意 Example 类的以下特性：

- 该类实现了 IDisposable 接口。
- 公共的 Dispose 方法可以随时由你的应用程序代码调用。
- 公共的 Dispose 方法调用受保护的并重载的 Dispose 方法，该方法接受一个布尔参数，并将值 true 作为参数传递。此方法实际执行资源释放。
- 析构函数调用受保护的并重载的 Dispose 方法，该方法接受一个布尔参数，并将值 false 作为参数传递。析构函数仅由垃圾回收器在你的对象被终结时调用。
- 你可以安全地多次调用受保护的 Dispose 方法。变量 disposed 指示该方法是否已运行，是一个安全特性，用于防止该方法在并发调用时多次尝试释放资源。（你的应用程序可能会调用 Dispose，但在方法完成之前，你的对象可能会被垃圾回收，并且 Dispose 方法会再次由 CLR 从析构函数中运行。）资源仅在方法首次运行时被释放。
- 受保护的 Dispose 方法支持托管资源（如大型数组）和非托管资源（如文件句柄）的释放。如果 disposing 参数为 true，则此方法必须是从公共 Dispose 方法调用的。在这种情况下，托管资源和非托管资源都会被释放。如果 disposing 参数为 false，则此方法必须是从析构函数调用的，并且垃圾回收器正在终结对象。在这种情况下，无需（或不安全）释放托管资源，因为它们将被垃圾回收器处理，或者可能已经被处理，因此仅释放非托管资源。
- 公共的 Dispose 方法调用静态 GC.SuppressFinalize 方法。此方法阻止垃圾回收器对该对象调用析构函数，因为该对象已经完成终结。
- 类的所有常规方法（如 SomeBehavior）都会检查对象是否已被丢弃。如果已丢弃，它们会抛出异常。

## 实现异常安全的释放

在以下练习集中，你将研究 using 语句如何帮助确保应用程序中对象使用的资源即使在应用程序代码中发生异常时也能及时释放。最初，你将实现一个简单的类，该类实现析构函数并检查垃圾回收器何时调用此析构函数。

> Note
> 
> 在这些练习中创建的 *Calculator* 类仅用于说明垃圾回收的基本原理。该类实际上并未消耗任何重要的托管或非托管资源。对于如此简单的类，你通常不会创建析构函数或实现 *IDisposable* 接口。

### 创建一个使用析构函数的简单类

- 1. 如果尚未运行，请启动 Microsoft Visual Studio 2015。
- 2. 在 File 菜单上，指向 New，然后单击 Project。
  New Project 对话框打开。
- 3. 在 New Project 对话框中，在 Templates 下的左侧窗格中，单击 Visual C#。在中间窗格中，选择 Console Application 模板。在对话框底部附近的 Name 框中，键入 **GarbageCollectionDemo**。在 Location 字段中，指定你的 Documents 文件夹中 Microsoft Press\VCSBS\Chapter 14 文件夹，然后单击 OK。

> Tip
> 
> 你可以使用 Location 字段旁边的 Browse 按钮导航到 Microsoft Press\VCSBS\Chapter 14 文件夹，而不是手动输入路径。

Visual Studio 创建一个新的控制台应用程序并在 Code and Text Editor 窗口中显示 Program.cs 文件。

- 4. 在 Project 菜单上，单击 Add Class。
  Add New Item – GarbageCollectionDemo 对话框打开。
- 5. 在 Add New Item – GarbageCollectionDemo 对话框中，确保选择了 Class 模板。在 Name 框中，键入 **Calculator.cs**，然后单击 Add。
  *Calculator* 类被创建并在 Code and Text Editor 窗口中显示。
- 6. 向 *Calculator* 类添加以下公共 *Divide* 方法（以粗体显示）：

Click here to view code image

```
class Calculator
{
    public int Divide(int first, int second)
    {
        return first / second;
    }
}
```

这是一个非常直接的方法，它将第一个参数除以第二个参数并返回结果。它仅提供一点可由应用程序调用的功能。

7. 在 Divide 方法上方，添加以下以粗体显示的公共构造函数到 Calculator 类的开头：

Click here to view code image

```
class Calculator
{
    public Calculator()
    {
        Console.WriteLine("Calculator being created");
    }
    ...
}
```

此构造函数的目的是使你能够验证 Calculator 对象是否已成功创建。

8. 在构造函数之后，向 Calculator 类添加以下以粗体显示的析构函数：

Click here to view code image

```
class Calculator
{
    ...
    ~Calculator()
    {
        Console.WriteLine("Calculator being finalized");
    }
    ...
}
```

此析构函数仅显示一条消息，以便你可以看到垃圾回收器何时运行并终结此类实例。在为实际应用程序编写类时，你通常不会在析构函数中输出文本。

9. 在 Code and Text Editor 窗口中显示 Program.cs 文件。

10. 在 Program 类中，向 Main 方法添加以下以粗体显示的语句：

Click here to view code image

```
static void Main(string[] args)
{
    Calculator calculator = new Calculator();
    Console.WriteLine($"120 / 15 = {calculator.Divide(120, 15)}");
    Console.WriteLine("Program finishing");
}
```

此代码创建 Calculator 对象，调用此对象的 Divide 方法（并显示结果），然后在程序结束时输出一条消息。

11. 在 Debug 菜单上，单击 Start Without Debugging。验证程序是否显示以下一系列消息：

```
Calculator being created
120 / 15 = 8
Program finishing
Calculator being finalized
```

请注意，Calculator 对象的终结器仅在应用程序即将结束时运行，在 Main 方法完成后。

12. 在控制台窗口中，按 Enter 键并返回到 Visual Studio 2015。

CLR 保证你的应用程序创建的所有对象都将接受垃圾回收，但你不能总是确定何时会发生。在练习中，程序生命周期很短，Calculator 对象在 CLR 在程序结束时清理时被终结。然而，你也可能会发现，在资源消耗较大的更实质性的应用程序中也是如此，除非你采取必要的步骤提供释放手段，否则你的应用程序创建的对象可能会在应用程序结束之前一直保留其资源。如果资源是文件，这可能会阻止其他用户访问该文件；如果资源是数据库连接，你的应用程序可能会阻止其他用户连接到同一数据库。理想情况下，你希望在完成使用资源后立即释放资源，而不是等待应用程序终止。

在下一个练习中，你将在 Calculator 类中实现 IDisposable 接口并使程序能够在它选择的时机终结 Calculator 对象。

### 实现 IDisposable 接口

- 1. 在 Code and Text Editor 窗口中显示 Calculator.cs 文件。
- 2. 修改 Calculator 类的定义，使其实现

