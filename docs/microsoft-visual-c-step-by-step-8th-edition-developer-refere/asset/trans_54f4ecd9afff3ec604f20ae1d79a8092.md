

如果打开多个文件，每个源文件都有自己的标签，标签上标有源文件的名称。您可以单击标签，将命名的源文件带到代码和文本编辑器窗口的前台。

Solution Explorer 窗格出现在 IDE 的右侧，与代码和文本编辑器窗口相邻：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_35_0.png)

Solution Explorer 显示与项目关联的文件名称，以及其他项目。您也可以在 Solution Explorer 中双击文件名，将该源文件带到代码和文本编辑器窗口的前台。

在编写任何代码之前，请检查 Solution Explorer 中列出的文件，这些文件是 Visual Studio 2015 作为项目的一部分创建的：

- **Solution ‘TestHello’** 这是顶层的解决方案文件。每个应用程序包含一个解决方案文件。一个解决方案可以包含一个或多个项目，而 Visual Studio 2015 创建解决方案文件是为了帮助组织这些项目。如果您使用文件资源管理器查看 Documents\Microsoft Press\VCSBS\Chapter 1\TestHello 文件夹，您会看到此文件的实际名称是 TestHello.sln。
- **TestHello** 这是 C# 项目文件。每个项目文件引用一个或多个包含项目源代码和其他工件的文件，例如图形图像。您必须在同一个项目中用同一种编程语言编写所有的源代码。在文件资源管理器中，此文件实际称为 TestHello.csproj，它存储在您的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 1\TestHello\TestHello 文件夹中。
- **Properties** 这是 TestHello 项目中的一个文件夹。如果您展开它（单击 Properties 旁边的箭头），您会看到其中包含一个名为 AssemblyInfo.cs 的文件。AssemblyInfo.cs 是一个特殊文件，您可以使用它为程序添加属性，例如作者姓名、程序编写日期等。您可以指定其他属性来修改程序的运行方式。解释如何使用这些属性超出了本书的范围。
- **References** 此文件夹包含对已编译代码库的引用，您的应用程序可以使用这些库。当您的 C# 代码被编译时，它会被转换为一个库并被赋予一个唯一名称。在 Microsoft .NET Framework 中，这些库称为 *assemblies*。开发人员使用程序集打包他们编写的有用功能，以便将其分发给可能希望在自己的应用程序中使用这些功能的其他开发人员。如果您展开 References 文件夹，您将看到 Visual Studio 2015 默认添加到项目的引用集。这些程序集提供了对 .NET Framework 中许多常用功能的访问，并且由 Microsoft 与 Visual Studio 2015 一起提供。随着您在本<|message|> 书中练习的进行，您将了解其中许多程序集。
- **App.config** 这是应用程序配置文件。它是可选的，可能并不总是存在。您可以指定应用程序在运行时使用的设置，以修改其行为，例如用于运行应用程序的 .NET Framework 版本。您将在本书后面的章节中了解有关此文件的更多信息。
- **Program.cs** 这是一个 C# 源文件，当项目首次创建时，它会显示在代码和文本编辑器窗口中。您将在此文件中为控制台应用程序编写代码。它还包含 Visual Studio 2015 自动提供的一些代码，您将很快检查这些代码。

## 编写您的第一个程序

Program.cs 文件定义了一个名为 *Program* 的类，其中包含一个名为 *Main* 的方法。在 C# 中，所有可执行代码必须在方法内定义，并且所有方法都必须属于类或结构体。您将在第 7 章“创建和管理类与对象”中了解更多关于类的信息，并在第 9 章“使用枚举和结构创建值类型”中了解结构体。

*Main* 方法指定程序的入口点。此方法应以 *Program* 类中指定的方式定义为静态方法；否则，.NET Framework 可能无法将其识别为应用程序运行时 的起点。（您将在第 3 章“编写方法并应用作用域”中详细了解方法，第 7 章提供了有关静态方法的更多信息。）

### Important

C# 是一种区分大小写的语言。您必须将 Main 的 M 写成大写。

在下面的练习中，您编写代码以将消息“Hello World!”显示到控制台窗口，构建并运行您的 Hello World 控制台应用程序，并学习命名空间如何用于划分代码元素。

## 使用 Microsoft IntelliSense 编写代码

- 1. 在显示 Program.cs 文件的代码和文本编辑器窗口中，将光标放在 Main 方法中，紧跟在左大括号（ { ）之后，然后按 Enter 创建新行。
- 2. 在新行上，键入单词 Console；这是由您的应用程序引用的程序集提供的另一个类。它提供了在控制台窗口中显示消息和从键盘读取输入的方法。

当您键入单词 Console 开头的字母 C 时，会出现一个 IntelliSense 列表。

此列表包含在此上下文中有效的所有 C# 关键字和数据类型。您可以继续键入或滚动列表并用鼠标双击 Console 项。或者，在您键入 Cons 之后，IntelliSense 列表会自动聚焦到 Console 项，您可以按 Tab 或 Enter 键来选择它。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_37_0.png)

Main 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console
}
```

### Note

*Console* 是一个内置类。

3. 在 *Console* 后立即键入一个句点。
另一个 IntelliSense 列表出现，显示 *Console* 类的方法、属性和字段。

4. 滚动列表，选择 *WriteLine*，然后按 Enter。
或者，您可以继续键入字符 **W**、**r**、**i**、**t**、**e**、**L**，直到 *WriteLine* 被选中，然后按 Enter。
IntelliSense 列表关闭，单词 *WriteLine* 被添加到源文件中。*Main* 现在应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine
}
```

5. 键入一个左括号，( 。另一个 IntelliSense 提示出现。
此提示显示 *WriteLine* 方法可以接受的参数。事实上，*WriteLine* 是一个 *重载方法*，意味着 *Console* 类包含多个名为 *WriteLine* 的方法——它实际上提供了 19 个不同版本的方法。您可以使用 *WriteLine* 方法的每个版本输出不同类型的数据。（*第 3 章* 更详细地描述了重载方法。）*Main* 现在应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine(
}
```

### Tip

您可以通过在提示中单击上、下箭头来滚动浏览 *WriteLine* 的不同重载。

6. 键入一个右括号，)，然后跟一个分号，;。

Main 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine();
}
```

- 7. 移动光标并在 WriteLine 方法后的左、右括号之间键入字符串“Hello World!”，包括引号。

Main 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine("Hello World!");
}
```

![](img/16f6e3fe08f01ddadb2741a92c392b0e_39_0.png)

### Tip

养成键入匹配字符对的习惯，例如括号——( 和 )——和大括号——{ 和 }——然后再填写其内容。在您输入内容后再添加结束字符很容易忘记。

