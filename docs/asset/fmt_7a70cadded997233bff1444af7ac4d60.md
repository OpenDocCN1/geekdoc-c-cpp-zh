
Height="200" Width="325">

```xml
<Grid>
    <DockPanel LastChildFill="True">
        <StackPanel Orientation="Horizontal" DockPanel="Top">
            <TextBox Text="Criteria" Margin="0,0,5" />
            <TextBox x:Name="Search" Width="100" Margin="0,0,5" />
            <Button x:Name="Search" Content="Search" Margin="5,0,5" />
            <Button x:Name="Clear" Content="Clear" Margin="5,0,5" />
        </StackPanel>
        <ListBox x:Name="Results" DisplayMemberPath="Name" />
    </DockPanel>
</Grid>
</UserControl>
```

```xml
SearchView.xaml
```

项目现在看起来像图11-3。

为了利用 Caliburn.Micro，你需要在 WPF 项目中进行设置。第一步是修改 `App.xaml` 以移除 `Startup` 标签。`App.xaml` 应该精简为如下：

```csharp
public partial class App : Application
{
    public App()
    {
```

![](img/15cb6759e167a2d1560bc37de753a62_262_0.png)

下一步是项目中项目的“bootstrapper”。在 WinClient 项目根目录下，你创建一个名为 `WinClientBootstrapper` 的类，其内容如下：

```csharp
public class WinClientBootstrapper : Bootstrapper<SearchViewModel> { }
```

这就是你需要的全部。记住，编写尽可能简单的 bootstrapper 来让项目运行。Caliburn.Micro 网站（http://caliburnmicro.codplex.com/）包含了大量精彩内容，描述了你可以使用 bootstrapper 进行的所有事情，所以请务必查看。现在我们在 `app.xaml` 中添加一些 XAML：

```xml
<Application x:Class="OSIM.WinClient.App"
     xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
     xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
     xmlns:local="clr-namespace:OSIM.WinClient">
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <local:WinClientBootstrapper x:Key="bootstrapper"/>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Application.Resources>
</Application>
```

# 总结 | 263

如果你正在编写 Silverlight 应用，App.xaml 看起来会略有不同：

```xml
<Application x:Class="OSIM.WinClient.App"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:OSIM.WinClient">
    <Application.Resources>
        <local:WinClientBootrapper x:Key="bootstrapper"/>
    </Application.Resources>
</Application>
```

![](img/15cb6759e167a2d15e60bc37de753a62_263_0.png)

这就是你在 Caliburn.Micro 中需要做的所有工作。基于所使用的约定，以及对 App.xaml 和 `WinClientBootrapper` 类的修改，当你运行 WinClient 应用时，会出现基础搜索界面。注意，“搜索（Search）”和“清除（Clear）”按钮处于禁用的状态，直到你在“条件（Criteria）”文本框中输入内容并点击“清除”按钮，内容被清空后，“搜索”和“清除”按钮再次禁用。输入某些条件并点击“搜索”按钮将显示项目类型（ItemTypes）列表。图 1-4 显示了最基础的搜索界面。

![](img/15cb6759e167a2d15e60bc37de753a62_263_1.png)

图 1-4

该项目是从先查看 ViewModel 然后编写测试来支持所需功能的角度切入的。你可以轻松地从视图开始，但无论哪种，你都创建了一个经过彻底单元测试的应用，并满足了章节开头所述的用户故事的要求。

#### 总结

WPF 和 Silverlight 是使用 XAML 创建丰富应用程序的强大框架。对这些框架的应用进行单元测试可能是困难的，但并不是你应该避免的。与 WCF 和 ASP.NET 一样，为你的各种客户端制定测试策略是关重要的。

与其为了规避代码后置（`code-behind`）范式的局限性并尝试实例化紧耦合的类，MVVM 模式促进了用户界面与其受控代码之间的真正分离。

MVVM 不仅允许你对应用进行单元测试，还能让应用更具可维护性。它还允许设计师仅在 XAML 中工作，而不必担心代码，从而帮助了开发者/设计师之间的关系。许多优秀的 MVVM 框架减轻了实现这种模式的负担，让你能够专注于编写优秀软件的过程。

# 第四部分

# 需求与工具

- 第 12 章：处理缺陷和新需求
- 第 13 章：关于工具大争论
- 第 14 章：结论

# 第 12 章

# 处理缺陷和新需求

本章内容包括：

- 理解为什么在现代业务计算环境中，应用需要具有灵活性
- 使用 TDD 处理应用程序的变更
- 通过 TDD 构建更具灵活性的应用程序
- 在应用引入新功能或发现缺陷的情况下练习 TDD

应用程序的开发工作并非在真空中进行。敏捷项目方法论的日益普及正证明了这一事实。在敏捷环境中，从记录第一个需求到应用部署到生产环境，开发工作跨度可能越越数月甚至几年。这为需求的变化留下了大量时间。

变更在应用上线生产后并没有结束。无论开发团队和 QA 部门表现得多么出色，大多数应用程序都有某些缺陷，直到应用到达生产环境后才被发现。即使应用进入了生产且没有发现缺陷，来自各种外部力量（客户、政府、市场力量）的作用和影响也可以表明应用需要变更。

在 TDD 中，缺陷和新需求代表了创建新测试的机会。通过以测试优先的哲学来处理缺陷和新需求，你可以更容易地交付高质量的应用，而不会破坏现有功能。阅读此本书帮助你获取了处理这些情况所需的技能和知识。现在，只需将这些技能和知识以略有不同的方式应用即可。

## 处理变更

变更是不可避免的。从历史上看，大多数业务应用程序并没有很好地处理变更。这是因为尽管开发者和架构师主意良好，但大多数应用程序会变得脆弱且易碎。如果没有单元测试和集成测试套件的安全保障，大多数应用程序会退化为高积木式的代码。不久，应用程序就会变得不稳定，至于大多数开发者都不敢碰它，导致整个结构崩塌。

这些应用程序缺乏单元测试和集成测试。如果没有一种方法对进行修改过的应用程序进行自动回归测试，没有人能保证应用程序在变更后仍正常运行。在练习 TDD 的同时开发应用程序提供了一套此类测试，以确保在进行变更时，应用程序保持稳定。

TDD 的实践还有另一个副作用，使应用程序在面对变更时更具灵活性。练习 TDD 的开发者（无论是出于设计还是作为为了可测试性而编写代码的副作用）似乎比不练习 TDD 的开发者更遵循 SOLID 原则。遵循 SOLID 原则使得软件更容易维护和扩展。在在一个不可避免变更的环境中，这显然是一个优势。

## 变更总会发生

由于多种原因，应用程序在部署到生产环境后可能需要变更。也许公司采取了新的业务策略，或确定了一个新的进入市场。金融和医学等许多业务领域受到州联邦政府的严格监管。新法律法规不断通过。使用应用程序的客户可能希望添加新功能或对现有功能进行更改。没有任何应用程序是对缺陷免疫的。

无论应用程序变更的来源或原因，作为开发者你必须处理新需求和缺陷。在从开始就实践 TDD 的应用中，处理方法可能是显而易见的。即使在未使用 TDD 开发的应用中，在添加新功能和修复缺陷时仍然可以采用这种实践。测试确保了你应用程序的某种质量，这种对质量的承诺应该贯穿部署后的开发工作。

## 添加新功能

新功能可以任何时候引入应用程序。在用敏捷方法论的正常开发周期内引入的新功能并不值得注意。它们被添加到项目待办列表中，并像其他任何功能一样被计划。在应用部署到生产环境后（此时开发团队的大部分可能已经转移到另一个项目）引入的功能有些不同。

重要的一点是，在应用程序主要开发周期结束后引入的功能，应该被视为在该应用开发期间已知并构建的功能。

# 270 | 第 12 章 处理缺陷与新需求

在开发缺陷修复方案时，其方法与功能开发的开发方法相同。第一步是与业务部门讨论缺陷，以确保应用程序应该如何运行，以及这种行为与应用程序目前的运行方式有何不同。在重新验证了业务规则后，你开始编写一个测试。对于新功能，这个测试应该是失败的。一个未失败的测试可能表明你正在测试正确的内容。测试应该暴露缺陷。这样，你就可以确保不仅修复了缺陷，而且它不会再次出现。

#### 从测试开始

在第 11 章中，在开发 InventoryService WCF 服务期间发现了一个潜在的缺陷，如图 12-1 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_268_0.png)

图 12-1

这里是测试生成的代码：

```csharp
public string[] GetItemTypes()
{
    var itemTypeList = _itemTypeService.GetItemTypes()
        .Select(x => x.Name)
        .ToArray();
    return itemTypeList;
}
```

`InventoryService.svc`

当 `ItemTypeService` 的 `GetItemTypes` 方法返回 `null` 时发生错误。对于该方法来说，这是一种异常行为。诚然，`ItemTypeService` 的 `GetItemTypes` 方法永远应该不需要返回 `null`。即使数据存储中没有 `ItemTypes`，Fluent NHibernate 返回它的空实例。`ItemTypeService` 上的 `GetItemTypes` 方法只是将空列表传递给 `InventoryService` 的 `GetItemTypes` 方法。

那么这又如何呢？我们在生产环境中的所有应用程序都有一个要求：用户永远不应该看到意外的异常。除了潜在的安全泄露外，用户不知道如何从这种情况下恢复。大多数用户还会对应用程序崩溃并重启感到不满，因为这可能导致他们丢失工作。用户需要被隔离并免受未处理的 .NET 异常的影响。

我将通过创建一个测试来开始这个缺陷。具体来说，我想查看 `ItemTypeService` 的 `GetItemTypes` 方法上的存根是否返回了 `null`：

```csharp
public class and_get_list_of_item_types_when_the_returned_list_is_null :
    using_the_external_inventory_service
{
    private IInventoryService _inventoryService;
    private string[] _result;
    private Mock<IItemTypeService> _itemTypeService;

    protected override void Establish_context()
    {
        base.Establish_context();
        _itemTypeService = new Mock<IItemTypeService>();
        _inventoryService = new InventoryService(_itemTypeService.Object);
        List<ItemType> itemTypeList = null;
        _itemTypeService.Setup(x => x.GetItemTypes())
            .Returns(itemTypeList);
    }

    protected override void Because_of()
    {
        _result = _inventoryService.GetItemTypes();
    }

    [Test]
    public void then_an_empty_list_of_item_types_should_be_returned()
    {
        _result.ShouldNotBeNull();
        _result.Count().ShouldEqual(0);
    }
}
```

![](img/15cb6759e167a2d15e60bc37de753a62_269_0.png)

这个测试看起来与第 10 章中用于验证 InventoryService WCF 服务功能的测试相似。事实上，它们几乎是完全相同的——有两个例外。要指出的第一个变化是，`ItemService` mock 上的 `GetItemTypes` 存根不是返回 `ItemTypes` 列表，而是返回 `null`。这模拟了 `GetItemService` mock 返回 `null` 的情况。另一个变化是 `then_a_list_of_items_should_returned` 方法没有在 `List` 中查找项目。它仅仅验证了 `_result` 变量不为 `null` 就到此为止。

运行此测试后，你可以从图 12-2 中看到它是失败的，代表了导致 `InventoryService` 出现缺陷的情况。

![](img/15cb6759e167a2d15e60bc37de753a62_270_0.png)

图 12-2

## 修改代码

你现在有一个测试可以暴露 InventoryService WCF 服务中的缺陷。在开始编写代码之前，你应该运行所有测试，并验证该缺陷的测试是目前唯一失败的测试。该测试如图 12-3 所示。

下一步是查看 `InventoryService` 的 `GetItemTypes` 方法的代码，找出缺陷发生的地方。这里显示了整个 `GetItemTypes` 方法：

![](img/15cb6759e167a2d15e60bc37de753a62_271_0.png)

图 12-3

```csharp
public string GetItemTypes()
{
    var itemTypeList = _itemTypes.GetItemTypes()
        .Select(x => x.Name)
        .ToArray();
    return itemTypeList;
}
```

`InventoryService.svc.cs` 的第 17 行是 `InventoryService` 的 `GetTypes` 方法中调用 `_itemType.GetItemTypes` 方法的行。这段代码的修复方法非常简单。我们需要在调用 `Select` 和 `ToArray` 之前，捕获 `GetItemTypes` 方法的输出。如果 `GetItemTypes` 的结果为 `null`，我们需要返回一个空数组：

```csharp
public string GetItemTypes()
{
    var itemTypeList = _itemTypeService.GetItemTypes();
    if (itemTypeList == null)
    {
        return new string[0];
    }
    // ... 后续逻辑
}
```
