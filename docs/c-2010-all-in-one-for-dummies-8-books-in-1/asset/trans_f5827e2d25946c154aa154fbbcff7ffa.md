
如果我们需要相加两个数字，可以轻松做到。

```csharp
int answer = add(10, 4),
```

如果我们需要相加四个数字，我们也没有问题。

```csharp
int answer = add(10, 4, 5, 12);
```

那么，为什么可选参数是危险的呢？因为有时默认值会产生意想不到的后果。例如，你不想写一个除法方法并将参数默认设为 0。有人会调用它并得到一个未定义的除以零的错误。在 `addall` 方法内部将 `v` 的可选值设置为 1 将是糟糕的。

```csharp
public static int add(int z, int y, int x = 0, int w = 0,
    int v = 1)
    // 显然不想这样做
    return z + y + x + w + v;
```

而且有时问题可能非常微妙，所以请谨慎使用可选参数。例如，假设你有一个基类，然后有一个实现该基类的派生类，如下：

```csharp
public abstract class Base
{
    public virtual void SomeFunction(int x = 0)
    {{...}}
}
```

```csharp
public sealed class Derived
{
    public override void SomeFunction(int x = 1)
    {{...}}
}
```

如果声明一个新实例会发生什么？

```csharp
Base ex1 = new Base();
ex1.SomeFunction();                  // SomeFunction (0)
Base ex2 = new Derived();
ex2.SomeFunction();                  // SomeFunction (0)
Derived ex3 = new Derived();
ex3.SomeFunction();                  // SomeFunction (1)
```

## 784 可选参数

这里发生了什么？取决于你如何实现类，可选参数的默认值设置方式不同。第一个例子 `ex1` 是 `Base` 的实现，默认可选参数为 0。在第二个例子中，`ex2` 被强制转换为 `Derived` 类型（这是合法的，`Derived` 是 `Base` 的子类），默认值也是 0。然而，在第三个例子中，`Derived` 直接被实例化，默认值为 1。这并不是特别符合预期的行为，尽管我必须承认，我不确定在这种情况下**预期的行为**到底是什么。无论你如何看待，这都是一个陷阱，是需要注意。

## 引用类型

新的引用类型通过以下方式实现：

- 类 (Class)
- 接口 (Interface)
- 委托 (Delegate)

在使用它们之前需要先构建它们；类本身不是引用类型，但 `Calendar` 类是。

.NET Framework 中有三种内置引用类型：

- String（谁知道为什么它不是静态类型）
- Object
- Dynamic

你可以像传递静态类型一样将引用类型传递给方法。在方法内部，你仍然像使用其他变量一样使用它。

但引用类型可以像静态类型一样被传递吗？让我们试试。例如，如果我们为 `Calendar` 类编写了一个 `Schedule` 方法，我们可以传递 `CourseId`，也可以传递整个 `Course`。这完全取决于我们如何构建应用程序。

```csharp
public class Course {
    public int CourseId;
    public string Name;
    public void Course(int id, string name)
{
  CourseId = id;
  Name = name;
}
public class Calendar
{
    public static void Schedule(int course)
    {
    }
    public static void Schedule(Course course)
    {
      // 这里发生了一些有趣的事情
    }
}
```

在这个示例中，我们为 `Schedule` 编写了一个重载方法——一个接受 `CourseId`，另一个接受 `Course` 引用类型。后者是引用类型，因为 `Course` 是一个类，而不是像 `CourseId` 的 `Integer` 那样的静态类型。

我们希望第二个 `Schedule` 方法支持一个可选的 `Course` 参数吗？例如，如果我省略了参数，我想默认创建一个新课程（New Course）。这应该类似于将一个静态整数设置为“0”或任何其他值，不是吗？

```csharp
public static void Schedule(Course course) = New
{
  // 在此处实现
}
```

然而，这是不允许的。Visual Studio 允许在静态类型上使用可选参数，编译器会提示你。如果我想这样做，我必须在方法中接受 `CourseId`。

## 输出参数

正如我所讨论的，输出参数会改变变量的值。输出参数在方法签名中用 `out` 关键字标记。（此处省略了原文中大量重复的句子）
