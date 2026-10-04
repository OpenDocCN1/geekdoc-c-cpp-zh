

![](img/6df7bb88e9302e98442acc219cfbd7fc_404_0.png)

图 10-1:
解决方案管理器中的新库。

## 向现有解决方案中添加第二个项目

如果你有一个现有的解决方案——无论是一个正在运行的应用程序，还是像上一节中描述的那种类库项目——你都可以轻松地向解决方案中添加第二个项目：可以是类库项目或可执行项目（例如驱动程序）。按照以下步骤操作：

1. 在 Visual Studio 中打开现有解决方案后，在解决方案管理器中右键点击解决方案节点（顶层节点）。
2. 从弹出的菜单中，选择“添加（Add）”→“新建项目（New Project）”。
3. 在“新建项目”对话框中，选择你想要添加的项目类型。
   在对话框右侧选择类库、控制台应用程序、Windows Forms 应用程序或其他可用类型。
4. 使用“位置（Location）”框导航到你想要放置项目的文件夹。
   你导航到的位置取决于你想要如何组织解决方案。你可以将新项目文件夹放在两个地方之一：

- *合一文件夹（All-in-one-folder）：* 进入主项目文件夹，使添加的项目成为子文件夹。（参见图 10-2。）
- *并排布局（Side-by-side）：* 导航到包含主项目文件夹的文件夹，使两个项目处于同一层级。（参见图 10-3。）

## 5. 命名你的项目并点击确定。

如果新项目是库项目，请仔细选择其名称——它将成为库的 .DLL 文件的名称，以及包含项目类的类的命名空间名称。

如果你需要让类库项目与另一个项目甚至主项目具有相同的名称，可以通过添加后缀 `Lib` 来区分，例如 `MyConversionLib`。

如果你要添加的项目旨在独立运行并在其他程序中使用，请使用并排布局的方法。

本节节中的 `ClassLibrary` 示例（如本书中的大多数示例一样）采用了合一文件夹的方法。要点在于，虽然文件夹不必非在同一个地方，但将它们放在那里会很方便。

选择位置的任务与直接将新项目添加到 `ClassLibrary` 解决方案是独立的。两个项目文件夹可以在同一个解决方案中，但位于不同的地方。

![](img/6df7bb88e9302e98442acc219cfbd7fc_405_0.png)

## 图 10-2: 在合一文件夹中组织两个项目。

![](img/6df7bb88e9302e98442acc219cfbd7fc_405_1.png)

## 图 10-3: 并排组织两个项目。

![](img/6df7bb88e9302e98442acc219cfbd7fc_405_2.png)

## 为库创建类

创建好类库项目后，创建组成库的类。下面的 `ClassLibrary` 示例展示了一个简单的类库——我会在示例之后向你展示一些用于它的驱动代码：

```csharp
// ClassLibrary -- 位于类库项目中

// 文件：ClassLibraryDriver 项目中的 Program.cs
// ClassLibrary -- 一个简单的类库及其驱动程序
using System;
namespace ClassLibrary
{
    public class MyLibrary
    {
        public void LibraryFunction1()
        {
            Console.WriteLine("This is LibraryFunction1()");
        }
        public static int LibraryFunction2(int input)
        {
            Console.WriteLine("This is LibraryFunction2(), returning " + input);
            return input; // 仅返回输入。
        }
    }
}
```

库可以包含任何 C# 类型：类、结构体、委托、接口和枚举。我在第 4 章中介绍了结构体（structs），在第 9 章中介绍了委托，在第 8 章中介绍了接口，并在“枚举枚举（Enumerating Enums）”文章中介绍了枚举（enums）。

在类库代码中，通常你不应该捕获异常。让它们从库冒泡到调用它的客户端代码。客户端需要知道这些异常并以它们自己的方式处理它们。我在第 1 章中涵盖了异常。

## 使用驱动程序测试库

类库本身什么都不做，因此你需要一个驱动程序——一个较小的可执行程序，它通过调用库的方法来“驱动”库并对其进行测试。换句话说，编写一个使用库中的类和方法的程序。你在本节稍后的示例（以及本书中的其他程序）中可以看到这种行为——例如，当你调用 .NET 类库中 `Console` 类的 `WriteLine()` 方法时（`Console` 位于 `System` 命名空间）。

下面的代码块接上之前的列表。它添加了一个包含 `Main()` 方法的类的新项目，你可以在 `Main()` 内部编写代码来测试你的库：

```csharp
// ClassLibrary 驱动程序

// 在单独的 Console 项目中：
// 文件：ClassLibraryDriver 中的 Program.cs
using System;
using ClassLibrary;
namespace ClassLibraryExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 创建库对象并使用其方法。
            MyLibrary ml = new MyLibrary();
            ml.LibraryFunction1();
            // 通过类调用其静态方法。
            int result = MyLibrary.LibraryFunction2(27);
            Console.WriteLine(result.ToString());
            // 等待用户确认结果。
            Console.WriteLine("按回车键退出...");
            Console.Read();
        }
    }
}
```

库通常只提供静态方法。在这种情况下，你不需要实例化库对象。只需通过类调用它们。

## 在程序中使用类库

对于编写的任何程序，只需包含库命名空间的 `using` 指令，并对库的 .DLL 文件添加引用（提供它位于何处的路径）。要运行并测试库，请在驱动程序项目中引用它（如在“可执行文件”节所述），并将驱动程序项目标记为启动项目，然后运行控制台应用程序。

你也可以用另一种更好的方法测试库——使用单元测试。本书包含了一些单元测试的示例，你可以找到 NUnit。这里是输出：

```
This is LibraryFunction1()
This is LibraryFunction2(), returning 27
```

## 突破 public 和 private：更多访问修符

将程序分为多个程序集（如前面的节所述）会影响你从 AssemblyA 访问 AssemblyB 中的代码。

本书第 5 章的访问控制示例很好地（我希望）说明了 `public` 和 `private` 关键字。但该章没有介绍其他访问修符：`protected`、`internal` 以及组合 `protected internal`。我在本节中纠正了这个问题，假设你已经理解继承和方法重写。

为了确保本节有意义，你可能需要阅读（或重读）第 5 章。

## internal：仅限 CIA 内部

假设一个程序有两个项目：

- InternalLimitsAccess：一个可执行文件，其类包含启动执行的 `Main()` 方法。（没有法律要求 `Main()` 类命名为 `Program`。）
- CIAAssembly：类库项目。

你可以在网络上的 InternalLimitsAccess 示例中看到这种设置。

在现实生活中，美国国会习惯于要求中央情报局（CIA）公开其秘密——仅对国会成员和参议员。（“我们不会泄露你们的秘密——诚实。”与此同时，那些过度秘密的间谍拥有他们想要保留的秘密（他们可能知道可口乐的秘密配方或桑德斯上的秘密草香料，或者更阴暗的实体）。具体的 Secret X 并不重要，但 CIA 想要严守秘密。在 InternalLimitsAccess 示例中，CIA 被分为几个类——例如 `GroupA` 类和 `GroupB` 类。把它们想象成 CIA 的不同部门，它们（有时）会通信并共享各

