

用下划线标记它，类似于 Microsoft Word 拼写或语法错误下划线。当你点击带下划线的文本时，编译器会告诉你项目中需要引用哪些其他程序集才能使用该类。

## 常用命名空间

在新建的 Namespace_Sampler 项目的解决方案资源管理器中显示的引用列表包含了 Windows 窗体应用程序项目的大部分，但并非全部命名空间。例如，一个未显示为引用的命名空间是 Microsoft.VisualBasic，以及随附的 Microsoft.VisualBasic.dll。每个 Visual Basic 2010 项目都包含 Microsoft.VisualBasic 命名空间。该命名空间是 Visual Basic 2010 的 Visual Studio 项目模板的一部分，简而言之，它使 Visual Basic 2010 与 C# 或其他任何 .NET 语言不同。隐式包含此命名空间的原因是你可以直接调用 IsDBNull 以及 Visual Basic 2010 的其他方法。Visual Basic 2010 和 C# Windows 窗体应用程序项目默认包含的命名空间唯一区别在于，前者使用 Microsoft.VisualBasic，而后者使用 Microsoft.CSharp。

要查看所有自动导入的命名空间，例如 Microsoft.VisualBasic 命名空间，请在解决方案资源管理器中右键单击项目名称并从上下文菜单中选择属性。这将在 Visual Studio 中打开项目的属性窗口。从左侧窗格选择引用选项卡，你将在列表顶部看到 Microsoft.VisualBasic 引用（见图 4-11）。

![](img/d99870e80390742f93963da7be0b2e61_255_0.png)

图 4-11

当查看页面底部文本区域中的项目全局导入列表时，你可以看到除了 Microsoft.VisualBasic 命名空间之外，System.Collections 和 System.Diagnostics 命名空间也被导入到项目中。这由命名空间旁边的复选标记表示。与列表中其他命名空间不同，这些命名空间并未在上方的文本区域中列为引用。那是因为 System.Collections 和 System.Diagnostics 命名空间的实现是引用 System.dll 的一部分。与 Microsoft.VisualBasic 类似，导入这些命名空间允许引用相关类，而无需

完全限定路径。因为这些命名空间包含常用类，因此在项目级别始终包含它们是值得的。

以下列表简要总结了 Visual Basic 2010 项目中常用的一些命名空间：

- **System.Collections** — 包含支持各种功能丰富的对象集合的类。自动包含其中，包含数组、列表、字典、队列、哈希表等的类。
- **System.Collections.Generic** — 自 .NET 2.0 以来，此命名空间已启用使用框架的泛型功能——一种构建类型安全集合以及提供泛型方法和类的方式。
- **System.Data** — 此命名空间包含支持 ADO.NET 核心功能所需的类。
- **System.Diagnostics** — 包含在所有 Visual Basic 2010 项目中，此命名空间包含调试类。Trace 和 Debug 类提供了主要功能，但该命名空间包含数十个类来支持调试。
- **System.Drawing** — 此命名空间包含用于支持 Windows 应用程序项目的简单绘图类。
- **System.EnterpriseServices** — 未自动包含，必须引用 System.EnterpriseServices 实现才能使其可用。此命名空间包含将 .NET 程序集与 COM+ 接口的类。
- **System.IO** — 此命名空间包含重要的类，使你能够读取和写入文件以及数据流。
- **System.Linq** — 此命名空间包含一个对象接口，用于以新的简便方式处理不同的数据源。
- **System.Text** — 此常用命名空间使你能够以多种不同的方式处理文本，通常与字符串操作有关。此命名空间提供的更受欢迎的对象之一是 StringBuilder 对象。
- **System.Threading** — 此命名空间包含用于在应用程序中工作和操作线程所需的对象。
- **System.Web** — 这是处理 .NET Framework 中更令人兴奋的功能之一的命名空间：ASP.NET。此命名空间提供处理浏览器-服务器通信的对象。两个主要对象包括 HttpRequest，它处理从客户端到服务器的请求，以及 HttpResponse，它处理从服务器到客户端的响应。
- **System.Web.Services** — 这是你在创建 Web 服务时使用的主要命名空间，这是 .NET Framework 提供的更强大的功能之一。此命名空间提供处理 SOAP 消息和操作这些消息的类。
- **System.Windows.Forms** — 此命名空间提供在 Windows 窗体应用程序项目中创建 Windows 窗体的类。它包含窗体元素。

当然，要真正利用此列表中的类和其他对象，你需要更详细的信息。除了 Visual Studio 2010 的帮助文件等资源外，最好的信息来源是对象浏览器，可直接在 Visual Studio 2010 IDE 中使用。你可以通过选择 查看 ▸ 对象浏览器 来找到它，如果你使用的是 Visual Studio 2010、2005 或 2003，或选择 查看 ▸ 其他窗口 ▸ 对象浏览器 如果你使用的是 Visual Studio 2002。Visual Studio 2010 对象浏览器如图 4-12 所示。

对象浏览器显示每个引用的程序集，并使你能够深入到各种命名空间。图 4-12 说明了 System.dll 如何实现多个命名空间，包括 System 命名空间的一部分。通过深入命名空间，你可以看到一些可用的类。通过进一步选择一个类，浏览器不仅显示所选类关联的方法和属性，还显示该类的作用的简要概述。

![](img/d99870e80390742f93963da7be0b2e61_257_0.png)

# 图 4-12

使用对象浏览器是了解项目中包含的不同程序集可用的类和接口以及它们的工作方式的绝佳方法。显然，能够实际看到哪些类可用并知道如何使用它们是能够高效工作的基础。在 .NET CLR 环境中有效工作需要找到适合任务的正确类。

## 导入和别名命名空间

并非所有命名空间都应在全局级别导入。虽然你已经查看了在此级别包含的命名空间，但最好仅在模块中使用它们时才导入命名空间。与项目中使用的变量一样，可以在模块级别定义命名空间。其优点类似于使用局部变量，有助于防止不同命名空间相互干扰。正如本节所示，两个不同的命名空间可能包含具有相同名称的类甚至子命名空间。

### 导入命名空间

开发环境和编译器需要一种方法来确定在引用类时应检查命名空间的优先级。始终可以通过声明其完整命名空间路径来明确指定一个类。这称为完全限定你的声明。以下示例完全限定了一个 StringBuilder 对象：

```
Dim sb As New System.Text.StringBuilder
```

然而，如果对每个类的每个引用都需要其完整的命名空间声明，那么 Visual Basic 2010 以及其他所有 .NET 语言将很难编程。毕竟，谁想每次想要 ArrayList 类的实例时都输入 System.Collections.ArrayList？如果你查看全局引用，你会看到 System.Collections 命名空间。因此，你只需在需要该类的实例时输入 ArrayList，因为对更大的 System.Collections 命名空间的引用已经由应用程序完成。

理论上，引用 StringBuilder 类的另一种方法是使用 Text.StringBuilder，但由于所有命名空间都全局导入，这会带来一个问题，由所谓的命名空间拥挤引起。

