
像前面那样封装数据有两个缺点。第一，你必须编写更多代码，因为现在必须实现额外的方法。第二，该类型的使用者现在必须调用方法，而不能简单地引用单个字段名。

```csharp
e.SetName("Jeffrey Richter");       // Updates the employee's name
String EmployeeName = e.GetName(); // Retrieves the employee's name
e.SetAge(48);                       // Updates the employee's age
e.SetAge(-5);                       // Throws ArgumentOutOfRangeException
Int32 EmployeeAge = e.GetAge();     // Retrieves the employee's age
```

个人认为，这些缺点相当轻微。尽管如此，编程语言和 CLR 提供了一种称为属性的机制，它稍微缓解了第一个缺点，并完全消除了第二个缺点。

这里展示的类使用属性，并且在功能上与前面展示的类完全相同。

```csharp
public sealed class Employee {
   private String m_Name;
   private Int32   m_Age;

   public String Name {
      get { return(m_Name); }
      set { m_Name = value; }  // The 'value' keyword always identifies the new value.
   }

   public Int32 Age {
      get { return(m_Age); }
      set {
         if (value < 0)    // The 'value' keyword always identifies the new value.
            throw new ArgumentOutOfRangeException("value", value.ToString(),
               "The value must be greater than or equal to 0");
         m_Age = value;
      }
   }
}
```

如你所见，属性会稍微复杂化类型的定义，但它们允许你像下面这样编写代码，这足以补偿额外的工作。

```csharp
e.Name = "Jeffrey Richter";   // "Sets" the employee name
String EmployeeName = e.Name; // "Gets" the employee's name
e.Age = 48;                   // "Sets" the employee's age
e.Age = -5;                   // Throws ArgumentOutOfRangeException
Int32 EmployeeAge = e.Age;    // "Gets" the employee's age
```

你可以把属性看作智能字段：其背后带有额外逻辑的字段。CLR 支持静态、实例、抽象和虚拟属性。此外，属性可以用任何可访问性修饰符标记（第 6 章“类型和成员基础”中讨论），并可以在接口中定义（第 13 章“接口”中讨论）。

实现之后，任何访问该属性的代码都不必重新编译。然而，如果你将 Name 声明为字段，之后又将其改为属性，那么所有访问该字段的代码都必须重新编译，以便现在访问属性方法。

- 个人而言，我不喜欢编译器的 AIP 功能，因此通常出于以下原因避免使用它：字段声明的语法可以包含初始化，因此你可以在同一行代码中声明并初始化字段。然而，没有方便的语法将 AIP 设置为初始值。因此，你必须在每个构造函数方法中显式初始化每个 AIP。

- 运行时序列化引擎会将字段名持久化到序列化流中。AIP 的支撑字段名称由编译器决定，而且每次重新编译代码时，编译器实际上可能会更改此支撑字段的名称，从而使包含 AIP 的任何类型的实例无法反序列化。不要对任何打算序列化或反序列化的类型使用 AIP 功能。

- 调试时，你无法在 AIP 的 get 或 set 方法上设置断点，因此无法轻松检测应用程序何时获取或设置此属性。你可以对手动实现的属性设置断点，这在跟踪 bug 时非常方便。

你还应该知道，使用 AIP 时，属性必须是可读写的；也就是说，编译器必须生成 get 和 set 方法。这是合理的，因为只写字段如果无法读取其值就没有用；同样，只读字段将始终具有其默认值。此外，由于你不知道编译器生成的支撑字段的名称，你的代码必须始终使用属性名来访问属性。而且，如果你决定显式实现其中一个访问器方法，那么你必须显式实现两个访问器方法，并且你不再使用 AIP 功能。对于单个属性，AIP 功能是全有或全无的。

### 明智地定义属性

个人而言，我不喜欢属性，我希望 Microsoft .NET Framework 及其编程语言不支持属性。原因是属性看起来像字段，但它们是方法。众所周知，这会造成极大的混乱。当程序员看到看起来在访问字段的代码时，程序员会做出许多假设，而这些假设对属性而言可能并不成立。例如：

- 属性可以是只读或只写的；字段访问始终可读可写。如果定义属性，最好同时提供 get 和 set 访问器方法。

- 属性方法可能抛出异常；字段访问从不抛出异常。

- 属性不能作为 out 或 ref 参数传递给方法；字段可以。例如，以下代码将无法编译。

```csharp
using System;

public sealed class SomeType {
    private static String Name {
```

### 属性与 Visual Studio 调试器

Microsoft Visual Studio 允许你在调试器的监视窗口中输入对象的属性。这样做时，每次命中断点，调试器都会调用属性的 get 访问器方法并显示返回的值。这在跟踪 bug 时非常有用，但也可能导致 bug 发生并损害调试性能。例如，假设你为网络共享上的文件创建了一个 FileStream，然后将 FileStream 的 Length 属性添加到调试器的监视窗口。现在，每次命中断点，调试器都会调用 Length 的 get 访问器方法，而该方法会在内部向服务器发出网络请求，以获取文件的当前长度！

同样，如果你的属性的 get 访问器方法有副作用，那么这个副作用会在每次命中断点时执行。例如，假设你的属性的 get 访问器方法在每次被调用时递增一个计数器；现在，每次命中断点时，这个计数器也会递增。由于这些潜在问题，Visual Studio 允许你关闭监视窗口中显示的属性的属性求值。要在 Visual Studio 中关闭属性求值，请选择“工具”、“选项”、“调试”和“常规”，然后在图 10-1 的列表框中，清除“启用属性求值和其他隐式函数调用”复选框。请注意，即使清除了此项，你仍可以将属性添加到监视窗口，并通过单击监视窗口“值”列中的强制求值圆圈来手动强制 Visual Studio 对其求值。

![](img/857bdf6cef9e242b53a37f88df9a1287_259_0.png)

图 10-1 Visual Studio 常规调试器设置。

现在，我可以让代码构造一个 `Classroom` 对象并按如下方式初始化 `Students` 集合。

```csharp
public static void M() {
    Classroom classroom = new Classroom {
        Students = { "Jeff", "Kristin", "Aidan", "Grant" }
    };

    // Show the 4 students in the classroom
    foreach (var student in classroom.Students)
        Console.WriteLine(student);
}
```

编译此代码时，编译器看到 `Students` 属性的类型是 `List<String>`，并且该类型实现了 `IEnumerable<String>` 接口。现在，编译器假定 `List<String>` 类型提供了一个名为 `Add` 的方法（因为大多数集合类实际上都提供了一个将项添加到集合中的 `Add` 方法）。然后，编译器生成调用集合的 `Add` 方法的代码。因此，前面的代码会被编译器转换为以下代码。

```csharp
public static void M() {
    Classroom classroom = new Classroom();
    classroom.Students.Add("Jeff");
    classroom.Students.Add("Kristin");
    classroom.Students.Add("Aidan");
    classroom.Students.Add("Grant");

    // Show the 4 students in the classroom
    foreach (var student in classroom.Students)
        Console.WriteLine(student);
}
```

如果属性的类型实现 `IEnumerable` 或 `IEnumerable<T>`，但该类型不提供 `Add` 方法，那么编译器不会允许你使用集合初始化器语法向集合添加项；相反，编译器会发出类似以下的消息：error CS0117: 'System.Collections.Generic.IEnumerable<string>' does not contain a definition for 'Add'。

某些集合的 `Add` 方法接受多个参数——例如，`Dictionary` 的 `Add` 方法。

```csharp
public void Add(TKey key, TValue value);
```

你可以通过在集合初始化器中使用嵌套大括号，向 `Add` 方法传递多个参数，如下所示。

```csharp
var table = new Dictionary<String, Int32> {
    { "Jeffrey", 1 }, { "Kristin", 2 }, { "Aidan", 3 }, { "Grant", 4 }
};
```

