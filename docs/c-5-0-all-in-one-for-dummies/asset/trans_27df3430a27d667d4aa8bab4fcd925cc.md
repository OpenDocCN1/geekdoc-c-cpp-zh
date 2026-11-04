
## 依赖注入 (DI)

本示例中的 ViewModel *依赖*于获取客户和销售区域数据。但在实际项目中，硬编码假存储库并不是个好主意。我不止一次发布过代码中仍留有测试值的软件！“发布前我会把它改回去”这种想法在两步发布流程中往往会被遗忘。

依赖注入是一种将所需依赖*注入*到需要它们的类中的技术。这有助于防止上述情况发生。WPF 中常用的 DI 工具是 Unity，但还有其他几种高质量的开源工具，例如 Ninject。而且在大多数情况下，用代码自行实现 DI 并不难（见网站 http://csharp102.info）。尽管远超本书范围，DI 仍是软件开发中极其有价值的模式。

### 清单 4-25：视图的代码隐藏文件

```
public partial class CustomerMaintenance : Window
{
    public CustomerMaintenance()
    {
        InitializeComponent();
        DataContext = new CustomerMaintenanceViewModel();
    }
}
```

等等！我们不是说过要从代码隐藏文件中移除所有代码吗？不，不是*所有*代码。*几乎*所有代码。塞满业务逻辑的事件处理程序，当然要移除。但构造函数中必须有两行：*InitializeComponent()*，它呈现所有 XAML；以及 DataContext 赋值。你可能会有一些情况需要在代码隐藏文件中放置额外代码，而这些情况可能完全合理。在开始把代码添加到无法测试或无法复用的地方之前，请先进行批判性思考。

使用 ViewModel 模式后，命令绑定表达式会变得非常不同。实际上，如清单 4-26 所示，它们会变得简单不少。由于基类将 *Command* 挂接到 *CommandManager* 中，因此不再需要 *Windows.CommandBindings* 部分。

### 清单 4-26：添加客户按钮的 XAML

```
<Button HorizontalAlignment="Right" Margin="3,0,3,0"
Command="{Binding Path=AddCustomerCmd}"
CommandParameter="{Binding Path=Customers}"
Content="{Binding RelativeSource={RelativeSource Mode=Self},Path=Command.Text}"
/>
```

Content 与前面的示例相比没有变化，但 Command 和 CommandParameter 的赋值变了。所有控件的 DataContext 都会沿元素树向上查找第一个 DataContext。由于唯一的 DataContext 是在 Window 级别（在构造函数中）设置的，因此所有元素的 DataContext 都是 ViewModel。因此，绑定简化为将 Path 设置为 ViewModel 的属性（在本例中，Command 使用 AddCustomerCmd，CommandParameter 使用 Customers 属性）。

同样，ComboBox 将其 ItemsSource 属性绑定到 ViewModel 中的 IList<T> 属性。清单 4-27 显示了 Window 上两个 ComboBox 的 XAML。

### 清单 4-27：使用 ViewModel 的 ComboBox XAML

```
<ComboBox ItemsSource="{Binding Path=Customers}"
    DisplayMemberPath="Name"/>
<ComboBox ItemsSource="{Binding Path=Regions}"
    DisplayMemberPath="Name"
    SelectedItem="{Binding ElementName=CustomerList,Path=SelectedItem.
    SalesRegion}"
/>
```

第二个 ComboBox 展示了 WPF 数据绑定的强大之处。SelectedItem 应设置为 Customer 的 SalesRegion 属性的值。要通过绑定实现这一点，需将该属性项设置为 CustomerList 的 SelectedItem。这会返回一个 Customer 对象，从而允许在 Path 中选择该 Customer 上的任何属性（在本例中为 SalesRegion 属性）。

## 总结

最近有人问我，使用 ViewModel 模式是否值得，因为它“看起来像是很多额外工作”。这是目前 WPF 开发者中的一个常见话题，考虑到该模式尚属新鲜、当前实际项目中存在各种变体，以及围绕该主题的相互冲突的观点，这并不令人意外。

简而言之，它*确实*绝对值得。ViewModel 带来的最大好处是真正的关注点分离，并附带可测试性。任何时候，只要你能减少对人工用户测试的依赖并增加自动化测试覆盖率，那就是一种胜利。更高的代码隔离性、更强的代码复用能力以及更低的复杂性都随之而来。而且并没有开发出“更多”代码——只是把代码移出了 Window 的代码隐藏文件。

## 第六部分

## 使用 ASP.NET 进行 Web 开发

![](img/80ff26f06fc9ab951e1cd4257b867366_674_0.png)

测试，测试

## 内容速览

- 第 1 章：了解 ASP.NET 如何与 C# 协同工作.................651
- 第 2 章：构建 Web 应用程序.......................663
- 第 3 章：掌控你的开发体验 ...........677
- 第 4 章：利用 .NET Framework .....................705
- 第 5 章：深入 Web 构建 .....................723

## 分解 Web 应用程序

Web 应用程序是一种计算机程序，它使用非常轻量的客户端界面，通过 Internet 以无状态方式与服务器通信。*无状态*意味着浏览网站的计算机和提供网站的服务器之间不保持连接。你可以在图 1-1 中从高层视角看到这一过程。

![](img/80ff26f06fc9ab951e1cd4257b867366_677_0.png)

**图 1-1：** Web 应用程序流程。

客户端向服务器请求文档，服务器在方便时发送该文档。该文档通常由超文本标记语言 (HTML)、层叠样式表 (CSS) 和 JavaScript 组合而成，包含构成应用程序界面的标准化元素。

为什么你完全需要 Web 应用程序？如果服务器上只有一组文档，而客户端只是一个接一个地请求它们，那又有什么意义呢？当然，获取文档是件好事，但“应用程序”这一部分又体现在哪里呢？

答案就在 Web 应用程序之中。Web 应用程序之所以强大，是因为服务器可以在收到请求时即时构造文档。正是这个服务器端过程让 Web 应用程序得以运作（见图 1-2）。

别误会，轻量客户端界面——称为 Web 浏览器或简称浏览器——提供了一些重要功能。它负责处理用户界面，并且可以独立于服务器执行一些操作。

不过，服务器在很大程度上才是关键所在。因为服务器可以时刻记住事情，而且假定客户端在页面与页面之间会忘记一切，所以长时间运行的通信都驻留在服务器端。

![](img/80ff26f06fc9ab951e1cd4257b867366_678_0.png)

图 1-2：ASP.NET 解构。

ASP.NET 是一个控件和处理逻辑库，使构建服务器端的事情变得容易得多。你构建“服务器页面”，但它们最终会转换为客户端用来向你显示用户界面的文档。ASP.NET 被归类为 Web 应用程序框架，而不是编程语言。

就你的目的而言，编程语言是 C#。不过，你可以用任何 .NET 语言为 ASP.NET 编写代码——它只是框架中的又一组工具。

C# 是你用来告诉服务器如何组织 ASP.NET 各个部件并将它们发送给客户端的语言。客户端永远不会看到任何 C# 代码；它们甚至不会知道你是用 C# 编写的。

![](img/80ff26f06fc9ab951e1cd4257b867366_679_0.png)

这涉及我在本书中多次讨论过的同一个话题：库与语言之间的区别。ASP.NET 是一个工具库，而该库与语言无关。你使用语言来编排库中各个部件的功能。

然而，Web 开发有几个小注意事项。客户端——它并不关心你是否用 C# 编写代码——需要一些照料和供给。Web 应用程序中没有状态，因此你需要换一种方式思考。在 Web 开发中，客户端会自动为你完成许多事情。服务器则有一些安全性方面的顾虑。

在我深入探讨将 C# 与 ASP.NET 结合使用的细节之前，我想先带你浏览 Web 开发的细节，并指出一些你需要牢记的事情。

## 审视客户端

当你编写 Windows Form、WPF 或控制台应用程序时，客户端平台是 Windows 计算机。当你编写 Web 应用程序时，你完全不知道客户端平台是什么。它可能是 Mac、12 种 Windows 操作系统中的任意一种，或者 Linux。它可能是手机、平板电脑或上网本。它可能是电视、游戏设备，甚至是一台冰箱（真的：见图 1-3）。

![](img/80ff26f06fc9ab951e1cd4257b867366_679_1.png)

**图 1-3：** 没错，一台冰箱。

关键在于，你不知道自己是在为什么平台编写，因此针对 Web 浏览器的开发体验与针对 Windows 客户端的开发体验非常不同。你不知道屏幕尺寸是多少，你不知道
