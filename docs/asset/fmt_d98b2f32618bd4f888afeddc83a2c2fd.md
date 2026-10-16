
```csharp
        object[] args, out object result)
    {
        dynamic method = _dynamicData[binder.Name];
        result = method((DateTime)args[0]);
        return result != null;
    }
}
```

In this example, you’re overriding three methods: `TrySetMember`, `TryGetMember`, and `TryInvokeMember`.

`TrySetMember` adds the new method, property, or field to the object. In this case, you store the member information in a `Dictionary` object. The `SetMemberBinder` object that is passed into the `TrySetMember` method contains the `Name` property, which is used to identify the element in the `Dictionary`.

The `TryGetMember` retrieves the object stored in the `Dictionary` based on the `GetMemberBinder` `Name` property.

Here is the code that makes use of the new dynamic object just created (code file `DynamicSamples/DynamicSample/Program.cs`):

```csharp
dynamic wroxDyn = new WroxDynamicObject();
wroxDyn.FirstName = "Bugs";
wroxDyn.LastName = "Bunny";
WriteLine(wroxDyn.GetType());
WriteLine($" {wroxDyn.FirstName} {wroxDyn.LastName} ");
```

It looks simple enough, but where is the call to the methods you override? That’s where the .NET Framework helps. `DynamicObject` handles the binding for you; all you have to do is reference the

At first glance it might seem that this is no different from using the `dynamic` type, but there are a couple of subtle differences that are important. First, you can’t just create an empty `dynamic` typed object. The `dynamic` type has to have something assigned to it. For example, the following code won’t work:

```csharp
dynamic dynObj;
dynObj.FirstName = "Joe";
```

As shown in the previous example, this is possible with `ExpandoObject`.

Second, because the `dynamic` type has to have something assigned to it, it reports back the type assigned to it if you do a `GetType` call. For example, if you assign an `int`, it reports back that it is an `int`. This doesn’t happen with `ExpandoObject` or an object derived from `DynamicObject`.

If you have to control the addition and access of properties in your dynamic object, then deriving from `DynamicObject` is your best option. With `DynamicObject`, you can use several methods to override and control exactly how the object interacts with the runtime. For other cases, using the `dynamic` type or the `ExpandoObject` might be appropriate.

Following is another example of using `dynamic` and `ExpandoObject`. Assume that the requirement is to develop a general-purpose comma-separated values (CSV) file parsing tool. You won’t know from one execution to another what data will be in the file, only that the values will be comma-separated and that the first line will contain the field names.

First, open the file and read in the stream. You can use a simple helper method to do this (code file `DynamicSamples/DynamicFileReader/DynamicFileHelper.cs`):

```csharp
private StreamReader OpenFile(string fileName)
{
    if(File.Exists(fileName))
    {
        return new StreamReader(fileName);
    }
    return null;
}
```

This just opens the file and creates a new `StreamReader` to read the file contents.

Now you want to get the field names, which you can do easily by reading in the first line from the file and using the `Split` function to create a string array of field names:

```csharp
string[] headerLine =
fileStream.ReadLine().Split(',').Trim().ToArray();
```

Next is the interesting part. You read in the next line from the file, create a string array just like you did with the field names, and start creating your dynamic objects. Here’s what the code looks like (code file `DynamicSamples/DynamicFileReader/DynamicFileHelper.cs`):

```csharp
public IEnumerable<dynamic> ParseFile(string fileName)
{
    var retList = new List<dynamic>();
    while (fileStream.Peek() > 0)
    {
        string[] dataLine =
            fileStream.ReadLine().Split(',').Trim().ToArray();
        dynamic dynamicEntity = new ExpandoObject();
        for(int i=0;i<headerLine.Length;i++)
        {
            ((IDictionary<string,object>)dynamicEntity).Add(headerLine[i],
            dataLine[i]);
        }
        retList.Add(dynamicEntity);
    }
    return retList;
}
```

After you have the string array of field names and data elements, you create a new `ExpandoObject` and add the data to it. Notice that you cast the `ExpandoObject` to a `Dictionary` object. You use the field name as the key and the data as the value. Then you can add the new object to the `retList` object you created and return it to the code that called the method.

What makes this nice is you have a section of code that can handle any data you give it. The only requirements in this case are ensuring that the field names are the first line and that everything is comma-separated. This concept could be expanded to other file types or even to a `DataReader`.

Using this CSV file content that is available with the sample code download

```text
FirstName, LastName, City, State
Niki, Lauda, Vienna, Austria
Carlos, Reutemann, Santa Fe, Argentine
Sebastian, Vettel, Thurgovia, Switzerland
```

and this Main method to read the sample file `EmployeeList.txt` (code file `DynamicSamples/DynamicFileReader/Program.cs`):

```csharp
static void Main()
{
    var helper = new DynamicFileHelper();
    var employeeList = helper.ParseFile("EmployeeList.txt");
    foreach (var employee in employeeList)
    {
        WriteLine($"{employee.FirstName} {employee.LastName} lives in" +
            $"{employee.City}, {employee.State}.");
    }
    ReadLine();
}
```

results in this output to the console:

尼基·劳达居住在奥地利维也纳。

卡洛斯·鲁埃特曼居住在阿根廷圣菲。

塞巴斯蒂安·维特尔居住在瑞士图尔高。

### 摘要

本章介绍了`Type`和`Assembly`类的使用，它们是通过反射访问所提供广泛功能的主要入口点。

此外，本章演示了反射的一个特定方面，即自定义属性的检查，你很可能会比其他任何方面更频繁地使用它。你学习了如何定义和应用自己的自定义属性，以及如何在运行时检索有关自定义属性的信息。

本章的第二个重点是使用动态类型。使用`ExpandoObject`代替多个对象可以显著减少代码行数。此外，使用 DLR 并添加 Python 或 Ruby 等脚本语言可以帮助你构建一个更具多态性的应用程序，该应用程序可以在不重新编译的情况下轻松更改。

下一章详细介绍了 Visual Studio 2015 可用的许多功能。

### 17 Visual Studio 2015

#### 本章内容？

- 使用 Visual Studio 2015
- 创建和处理项目
- 调试
- 使用 Visual Studio 重构
- 处理各种技术：WPF、WCF 等
- 架构工具
- 分析应用程序

#### 本章 Wrox.com 代码下载

本章没有代码下载。

#### 使用 Visual Studio 2015

到目前为止，你应该熟悉 C# 语言，并且几乎准备好进入本书的应用部分，这些部分涵盖了如何使用 C# 编程各种应用程序。在此之前，了解如何使用 Visual Studio 以及 .NET 环境提供的一些功能来充分发挥程序的作用非常重要。

本章解释了在 .NET 环境中编程在实践中意味着什么。它涵盖了 Visual Studio，即你编写、编译、调试和优化 C# 程序的主要开发环境，并提供了编写良好应用程序的指导。Visual Studio 是用于众多目的的主要 IDE，包括编写 ASP.NET 应用程序、Windows Presentation Foundation (WPF) 应用程序以及通用 Windows 平台 (UWP) 应用，以及访问由 ASP.NET Web API 创建的服务，或使用 ASP.NET MVC 的 Web 应用程序。

本章还探讨了构建以 .NET Core 1.0 和 .NET Framework 4.6 为目标的应用程序所需的条件。

Visual Studio 2015 是一个完全集成的开发环境。它旨在使编写代码、调试它并将其编译为要发布的程序集的过程尽可能简单。这意味着 Visual Studio 为你提供了一个非常复杂的多个文档界面应用程序，你可以在其中完成与开发代码相关的几乎所有事情。它提供以下功能：

- 文本编辑器—使用此编辑器，你可以编写 C#（以及 Visual Basic、C++、F#、JavaScript、XAML、JSON 和 SQL）代码。此文本编辑器相当复杂。例如，随着你的输入，它会自动通过缩进行、匹配代码块的开始和结束括号以及为关键字着色来布局你的代码。它还在你输入时执行一些语法检查，并对导致编译错误的`<|message|>`进行下划线，这也称为设计时调试。此外，它还具有 IntelliSense 功能，会在你开始输入时自动显示类、字段或方法的名称。随着你开始为方法输入参数，它还会显示可用重载的参数列表。图 17.1 显示了 IntelliSense 功能在 UWP 应用中的实际效果。

![](img/3d365b72b289213a91ade7eb366b8f35_596_0.png)

> 注意 通过按 Ctrl+Space，你可以在需要时或出于任何原因不可见时重新调出 IntelliSense 列表框。如果想在 IntelliSense 框下方查看一些代码，只需一直按住 Ctrl 键即可。

- 设计视图编辑器—此编辑器使你能够在项目中放置用户界面和数据访问控件；Visual Studio 会自动向你的源文件添加必要的 C# 代码，以在项目中实例化这些控件。（这是可能的，因为所有 .NET 控件都是特定基类的实例。）

- 支持窗口—这些窗口使你能够查看和修改项目的各个方面，例如源代码中的类，以及 Windows Forms 和 Web Forms 类的可用属性（及其启动值）。你还可以使用这些窗口指定编译选项，例如构建中包含哪些程序集。

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;
/// <summary>
/// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=234238
/// </summary>
public sealed partial class MainPage : Page
{
    public MainPage()
    {
        this.InitializeComponent();
    }
}
```
