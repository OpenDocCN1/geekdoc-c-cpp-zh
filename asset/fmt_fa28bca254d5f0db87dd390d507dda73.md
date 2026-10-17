
### Convention over configuration

按配置注册涉及 painstakingly 将接口映射到实现。除了耗时之外，它还很冗长。相反，你可以使用约定来减少编写的代码量。

约定是向容器发出的指令，告诉它如何自动将接口映射到实现。这些指令构成了容器的输入，代替了注册。理想情况下，容器接收此输入并处理它，输出与你原本手动完成的确切注册相同。

> Note
>
> 这里的“over”可以读作“instead of”。因此，本主题是关于约定而不是配置。

Listing 9-30 显示了延续的示例如何使用约定优于配置进行注册。

#### LISTING 9-30 通过使用约定，注册阶段可以大大简化。

Click here to view code image

```
private void OnApplicationStartup(object sender, StartupEventArgs e)
{
    CreateMappings();

    container = new UnityContainer();
    container.RegisterTypes(
        AllClasses.FromAssembliesInBasePath(),
        WithMappings.FromMatchingInterface,
        WithName.Default
    );

    MainWindow = container.Resolve<TaskListView>();
    MainWindow.Show();

    ((TaskListController)MainWindow.DataContext).OnLoad();
}
```

注册已被 `RegisterTypes` 的调用所取代，该方法用于向容器提供如何查找类并将它们映射到接口的指令。此示例中提供的指令告诉容器：

- 注册 `bin` 文件夹（即基本路径）中程序集中的所有类。
- 将这些类映射到与类名匹配的接口。这里的约定是 `Service` 实现类将针对 `IService` 接口进行注册。
- 在注册每个映射时使用默认名称。此默认值为空，表示映射未命名。

因此，容器将遍历 `bin` 文件夹中每个程序集中的每个公共类，找到其实现的接口，并将其映射到与类名匹配的那个（以 `I`，即 Interface 为前缀），并且不为映射提供名称。很容易想象，结果注册会相当贪婪，可能将比你手动注册时更多的类注册到接口。然而，更重要的关注点是它是否正确地将你想要的类注册到正确的接口。这是约定引入的新问题。

注册无疑比之前的版本更简单，但仅在于它更短：代码更少。通过按配置注册，很容易理解每个接口使用了哪个实现——并且它们肯定已正确注册。

`RegisterTypes` 的第一个参数是要注册的类型集合。`AllClasses` 静态类提供了一些帮助方法，用于使用各种常见策略检索此类集合。第二个参数需要一个函数，它接受从第一个参数集合中传入的 `Type`——实现类型——并返回将映射到的 `Type` 实例集合——接口类型。`WithMappings` 静态帮助程序提供了一些匹配此签名的方法，并使用各种策略为每个类型找到合适的接口进行映射。第三个参数是另一个函数，这次要求你为每个类型。`WithName` 静态辅助类提供了两种替代方案：`Default` 始终返回 `null`（因此映射是未命名的），而 `TypeName` 则使用类型名称作为映射名称。这使你可以调用 `Resolve<IService>("MyServiceImplementation")` 来按名称检索映射的类型。

当然，由于该方法的参数非常通用，你可以自由提供任何匹配该签名的方法，以便根据自己的需要定制约定。如清单 9-31 所示，按约定注册的关键在于用于查找类型、映射类型和命名类型的约定。

#### 清单 9-31 约定可以根据你的规格进行定制。

单击此处查看代码图像

```csharp
public partial class App : Application
{
    private void OnApplicationStartup(object sender, StartupEventArgs e)
    {
        CreateMappings();

        container = new UnityContainer();
        container.RegisterTypes(
            AllClasses.FromAssembliesInBasePath().Where(type =>
            type.Assembly.FullName.StartsWith(MatchingAssemblyPrefix)),
            UserDefinedInterfaces,
            WithName.Default
        );

        MainWindow = container.Resolve<TaskListView>();
        MainWindow.Show();

        ((TaskListController)MainWindow.DataContext).OnLoad();
    }

    private IEnumerable<Type> UserDefinedInterfaces(Type implementingType)
    {
        return WithMappings.FromAllInterfaces(implementingType)
            .Where(iface => iface.Assembly.FullName.StartsWith(MatchingAssemblyPrefix));
    }
}
```

你再次从 `bin` 文件夹中的程序集中检索所有类型。但这一次，你只返回完整名称以特定前缀字符串开头的程序集，从而限制可接受的程序集。通常使用点号表示法来命名程序集，使其与所包含的顶级命名空间匹配。因此，`Microsoft.Practices.Unity` 是该命名空间所在的 DLL 名称。如果该程序集存在于你的 `bin` 文件夹中——如果你使用 Unity，它必然存在——你可能希望将其排除在要映射类型的扫描之外。一个简单的做法是只检索与你自己的应用程序前缀匹配的类型。你会使用类似 `MyBusiness` 或 `OurProject` 这样的前缀，而不是 `Microsoft`。

第二个参数已被替换为对你自己的本地方法的引用，该方法匹配所需的签名。给定一个 `Type`（即实现类型），你需要返回一个集合，其中包含要映射到的接口类型。你无需编写特别复杂的内容，只需特化 `WithMappings.FromAllInterfaces`，它会返回该类型实现的所有接口。这个列表完全可能包含你并不想映射到的接口——例如 `INotifyPropertyChanged` 或 `IDataErrorInfo`。因此，你再次只返回位于与你的程序集前缀匹配的程序集中的接口。这确保你只将自己的类型映射到自己的接口。

### 优点与缺点

与手工依赖注入（Poor Man's Dependency Injection）以及使用控制反转容器进行普通注册一样，使用约定也需要权衡取舍。你需要编写的代码更少，但这些代码比声明式替代方案更具算法性。

约定在最初设置起来更难。如果你编写的是真正符合 SOLID 原则的代码，并非所有内容都能与接口形成完美的一一映射。事实上，如果一个接口只有一个实现，这本身就是一种代码坏味道——用于单元测试的模拟对象不计入该总数。无论它们是适配器、装饰器还是不同策略，每个接口拥有多个实现应该是常见情况，这使得按约定注册更加困难。随着将复杂对象图注入类的做法越来越普遍，设计一个通用的规则来让类和接口相互映射就变得更加困难。在这种情况下，约定只能覆盖所需注册代码的一小部分，而不是成为通用做法。

Mark Seemann 是优秀著作《Dependency Injection in .NET》（Manning Publications, 2011）的作者，他探讨了可用于 DI 的三种选项，并得出了图 9-5 所总结的结论。简而言之，权衡发生在两个标准之间：价值和复杂性。价值是对选项功利性价值的衡量，范围从毫无价值到颇有价值。复杂性衡量选项的相对难度，范围从简单到复杂。如图所示，这三种选项位于钟形曲线的不同位置。手工 DI 简单而有价值，而约定优于配置则复杂而有价值。因此，它们之间的主要区别在于，使用约定比手动构造类并基于这些类形成对象图更复杂。

### 结论

依赖注入是本书其他所有内容得以紧密结合的粘合剂。如果没有依赖注入，就不可能如此专注地将依赖从类中剥离出来，并将它们的实现隐藏在通用接口之后。这些扩展点是开发自适应代码的关键，也是应用程序在规模和复杂性增长过程中稳步前进的关键。

DI 的实现有多种选项，每种选项都有其适用场景。无论你使用手工 DI 还是约定（辅以最少的手动映射），拥有 DI 本身比如何实现它更重要。

一些常见的 DI 用法实际上属于*滥用*，更适合归入代码坏味道或反模式的范畴。服务定位器（Service Locator）和非法注入（Illegitimate Injection）是两种滥用方式，它们会抵消正确实现的 DI 的部分积极效果。

每种应用程序类型都有一个组合根和一个解析根，识别这些根有助于你理解如何组织类以促进 DI。组合根始终非常接近应用程序的入口点，前提是将注册视为初始化关注点。解析根是唯一应该被解析的对象类型。在某些应用程序中，解析根只有一个实例，而在另一些应用程序中，会解析一组不同的子类。

尽管依赖注入具有深远的影响，它实际上是一个看似简单却功能强大且常被误解的模式。

## 第三部分：自适应示例

- 第 10 章 自适应示例：简介
- 第 11 章 自适应示例：冲刺 1
- 第 12 章 自适应示例：冲刺 2

本书的这一部分将带你经历开发软件产品的初始阶段。后续章节使用一个虚构的团队和项目，描述团队成员之间的对话以及他们在此过程中必须做出的决策。

代码示例反映了第一部分和第二部分中介绍的部分模式和实践。并非涵盖所有内容，但解答了一些更常见的实现问题。

与本书其他部分一样，可工作的代码示例可在 GitHub 上获取。有关使用 Git 进行源代码控制的简要介绍，请参阅附录 A“自适应工具”；有关每章代码清单与 GitHub 上 Adaptive Code 仓库分支名称的对应关系，请参阅附录 B“GitHub 代码示例”，你可以从 Microsoft Press Store 中本书的目录页面下载该附录。

### 第 10 章 自适应示例：简介

#### 在本章中，你将

- 了解将开发自适应示例应用程序的团队。
- 理解自适应示例应用程序的产品功能。
- 在冲刺零中为应用程序创建初始产品待办列表。

本书这一部分的章节通过使用 Scrum 并遵循本书详述的自适应设计原则，逐步构建一个可工作的应用程序。这是迄今所有内容的集大成，呈现出一个连贯的整体图景。与其他章节一样，我建议你在阅读这些章节时研究随附的代码¹。如果没有这些章节的内容，代码本身缺乏上下文。同样，如果没有完整的 Microsoft Visual Studio 解决方案，后续章节中的清单只会让你看到全貌的一小部分。

> 1 有关如何访问示例应用程序代码以及本书其他代码的说明，请参阅附录 A“自适应工具”。

本章的格式旨在反映现实世界中的场景，但出于简洁和清晰的目的做了一些让步。本章其余部分介绍一个虚构的 Scrum 团队，并概述将要开发的产品。

#### Trey Research

示例应用程序将由一家虚构的公司 Trey Research 开发。该公司以编写能够适应变化的自适应代码为傲。

#### 团队

示例应用程序将使用 Scrum 流程开发，因此团队需要成员来履行 Scrum 中的角色。如需回顾这些角色和 Scrum 流程，请参阅第 1 章“Scrum 简介”。

团队包含从应用程序启动到交付所需的所有角色。产品负责人清楚她希望应用程序如何运作、哪些功能优先级最高，以及哪些功能能为业务带来最大收入。Scrum Master 专注于团队正在使用的流程。他关心的是流程是否适合团队、团队工作是否没有障碍，以及产品负责人是否了解用户故事开发过程中出现的任何问题。Trey Research 的开发团队由实现用户故事的开发人员和设计测试用例并验证用户故事达到一定交付标准的测试分析师组成。

#### 产品负责人

产品负责人是 Petra。她是一位最近加入公司的资深业务分析师。她的专长是准确找到客户的需求——这对产品负责人来说是一项宝贵的技能。她坦率地承认自己对敏捷流程还很陌生，但她渴望进一步了解自己的新角色。

在整个开发过程中，Petra 与客户公司保持联络，以确切了解 it is that they want and why they want it. Also, she will calculate the value of various features to the client so that she can better prioritize work for the development team.

#### Scrum master

Steve holds two roles in the company. He is simultaneously a Scrum master and the technical team lead. This is a common scenario that the company is keen to remedy in the near future, freeing Steve up to concentrate on his preferred role as Scrum master. To facilitate this, the company is looking to hire an experienced developer into a dedicated technical team lead role.

In his capacity as Scrum master, Steve ensures that the team follows the Scrum process and that the team members are happy with the current incarnation of the process. He prides himself on working honestly and transparently with any assigned product owner or customer—never altering metrics or over-promising on delivery.

Although Steve rarely has time to write code, he still attends design meetings and tries to steer the development team in the right direction whenever he can.

#### Developers

David and Dianne are the company’s two dedicated developers. David is considered a junior developer because he was brought into the company after graduating from college, whereas Dianne is at more of an intermediate level.

One of the reasons that Steve hired David is his continued self-education on programming practices and techniques. David tries to stay current on the latest trends and is always hungry to learn. However, he does tend to view each new technique or technology as a cure-all and liberally applies it whenever he can. This is excellent practice for David, but often his code is a morass of needless indirection.

Dianne is more advanced than David, but she has a tendency to sound jaded by the tidal wave of new technologies that have emerged over the last few years. She has been burnt by the same issues that David is currently working through. Dianne is vying for the technical team lead role and is determined to prove her credentials to be promoted from within. To this end, she is keen to work closely with David to help him to improve.

#### The Hype Cycle

The Hype Cycle was developed by Gartner, an IT research and advisory firm. It is a useful tool for assessing the progress of new techniques and technologies. It is shown in Figure 10-1.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_359_0.png)
