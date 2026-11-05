
template option and naming the file, you create the **class** in the same way you have created other files that produce an `.exe` extension when compiled.

默认情况下，Visual Studio 将 **命名空间** 名称分配为与项目名称相同（Person）。你应该更改 **命名空间** 名称；否则，当你开始添加对已创建 DLL 的引用时，可能会变得相当混乱。

本示例中为 Person **类** 选择的 **命名空间** 名称是 PersonNamespace。要更改名称，只需用鼠标突出显示旧的 **命名空间** 名称并输入新名称即可。与 **命名空间** 相关的其他更改无需进行。

## 构建项目而不是运行项目

在键入完 **类** 后，你不会运行应用程序。Person **类** 没有 `Main()` 方法。如果按下 F5 或 Ctrl+F5，将生成类似图 11-7 所示的错误消息。

![](img/e33ae760e23d89eac66541252ad65de8_698_0.png)

**图 11-7** 尝试运行类库文件

要编译并创建 DLL，请在 Build 菜单栏下使用其中一个 **生成解决方案** 选项。你可以选中 **生成, 生成解决方案**，或选中 **生成** 后跟项目名称。保存工作后，关闭项目。应为 **Student 类** 创建一个全新的项目。你将使用 Visual Studio 开始页上的 Class Library 模板为 **Student 类** 创建一个 **类库**，就像为 Person **类** 所做的那样。

你在第 1 章学到 .NET 支持应用程序包含来自多个 .NET 语言的代码。这是因为所有 .NET 支持的和 .NET 管理的语言都使用相同的公共语言运行时 (CLR) 和相同的 Framework 类库 (FCL)。Person **类** 可以用 C# 编写。Student **类** 可以用 C++ 编写。实例化从 Person **类** 派生的 Student **类** 的图形用户界面展示 **类** 可以用 Visual Basic .NET 编写。

![](img/e33ae760e23d89eac66541252ad65de8_699_0.png)

使用多种语言的应用程序的唯一要求是，在项目内部源代码必须只使用一种语言。因此，如果你有一个包含三个项目的解决方案文件，每个项目都可以用不同的语言编写。

## 添加对基类的引用

由于你是从 Person 基类派生，因此首先应该做的事情之一是添加对 Person.dll 的引用。这样做首先可以让你在新创建的 Student 类内部访问 Person 类的成员。这在 Visual Studio 中可以通过几种方式完成。一个选项是使用 Solution Explorer 窗口。选中项目名称后，右键单击它并选择 **添加引用**，如图 11-8 所示。

![](img/e33ae760e23d89eac66541252ad65de8_699_1.png)

**图 11-8** 添加对 DLL 的引用

会显示一个类似图 11-9 所示的窗口，使你能够选择其中一个 .NET 预定义组件，或使用 **浏览** 选项卡定位 Person.dll。

![](img/e33ae760e23d89eac66541252ad65de8_700_0.png)

**图 11-9** 添加引用对话框

选中 **浏览** 选项卡后，导航到项目所在的位置。DLL 存储在你创建项目位置的 bin 文件夹下的 Debug 目录中。对于本示例，Person 项目是在 `C:\CSharpProjects\LibraryFiles` 文件夹中创建的。因此，有必要导航到该目录以定位 Person.dll，如图 11-10 所示。

![](img/e33ae760e23d89eac66541252ad65de8_700_1.png)

**图 11-10** 定位 Person.dll 组件

建立引用后，你可以从组件中定义的 `class` 派生新类。

## 添加 using 语句

现在你回到 Student 类，如果你只是键入：

```csharp
public class Student : Person
```

你会收到错误消息，如图 11-11 所示。

![](img/e33ae760e23d89eac66541252ad65de8_701_0.png)

仅仅添加引用是不够的——你需要完成最后一步。你必须通过添加 `namespace` 和在 `class` 名称前加一个点来限定 `Person`，如示例 11-11 所示。

### 示例 11-11

```csharp
public class Student : PersonNamespace.Person
```

更好的选择是在源代码文件顶部简单地添加一个 `using` 指令。`using` 语句应指示 `Person class` 的 `namespace` 标识符。在 `Person class` 中，本示例输入的名称为 `PersonNamespace`；因此，通过添加 `using` 语句，你可以避免对 `Person class` 的所有引用都需要限定。示例 11-12 包含 PersonNamespace 的 `using` 指令。

### 示例 11-12

```csharp
using PersonNamespace;    // Use whatever name you typed for the
                          // namespace for Person.
```

添加 `using` 语句后，你的 `class` 声明现在可以写为：

```csharp
public class Student : Person    // No need to fully qualify now.
```

在键入程序语句后，从 **生成** 菜单栏下的 **生成** 选项构建 DLL。保存工作并关闭项目。

## 创建客户端应用程序以使用 DLL

你现在有两个组件可以与许多不同的应用程序重复使用。所需要做的就是在程序中添加对组件的引用并包含带有适当命名空间的 using 语句。为了说明客户端程序如何使用 Student 组件，开发了一个 Windows 应用程序来实例化 Student 类的对象。

使用 Visual Studio，创建一个新项目并选择 Windows Forms Application 模板作为项目类型。类名为 PresentationGUI。

### 添加对 DLL 的引用

必须为 Person 和 Student 类添加引用。如果需要帮助添加引用，请查看图 11-8 至 11-10。两者都应在 PresentationGUI 项目中引用，如图 11-12 所示。

![](img/e33ae760e23d89eac66541252ad65de8_702_0.png)

**图 11-12** PresentationGUI 类中引用的 DLL

### 为命名空间添加 using 语句

为了避免键入完全限定的名称，请为 Student 命名空间添加 using 指令。在前面的示例中，Student 项目使用的命名空间为 StudentNamespace。因此，示例 11-13 显示了如何为 StudentNamespace 添加 using 指令。

### 示例 11-13

```csharp
using StudentNamespace;
```

由于 Student 类已包含 PersonNamespace 的 using 语句，并且没有实例化 Person 对象，因此在 PresentationGUI 类中添加 PersonNamespace 的 using 语句不是必需的。然而，如果也添加 using PersonNamespace; 也不会生成语法错误。

### 声明组件类型的对象

你必须声明一个 `Student object`。这是在 `PresentationGUI` 类内部作为 `private` 数据成员完成的，如示例 11-14 所示。

### 示例 11-14

```csharp
public class PresentationGUI : System.Windows.Forms.Form
{
    Student aStudent;
```

示例 11-14 中的语句声明了一个 `Student object`。当然，你也可以使用数组定义 `Student objects` 的集合。

### 实例化对象

要创建或实例化 `Student class` 的实际 `object`，必须使用其中一个 `Student constructors`。请记住为 `Student class` 定义了两个构造函数。因此，实例化 `class` 的一种方法是写：

```csharp
aStudent = new Student("123456789", "Maria", "Woo", "CS", 1111);
```

此实例化放置在处理窗体加载事件的方法中。它也可以放置在 `InitializeComponent( )` 方法中，该方法放置了 Windows Forms Designer 生成的代码。

### 使用派生类和基类的成员

向窗体添加了多个控件对象。`TextBox` 对象被拖到窗体上用于显示姓名、年龄、学生 ID、学生的睡眠量以及他人的睡眠量。添加了一个 `Button` 对象用于填充 `TextBox` 对象。示例 11-15 显示了 `PresentationGUI` 的程序语句。由于篇幅限制，Windows Forms Designer 生成的代码未包含在列表中。

### 示例 11-15

```csharp
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
```
