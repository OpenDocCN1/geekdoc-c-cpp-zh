
你会立即注意到 `GetItemTypes` 方法中的代码变得更加整洁且易理解。请编译该应用程序并再次从 WCF 测试客户端调用 `GetItemTypes` 方法，以验证服务仍在正常工作，如图 10-7 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_236_0.png)

图 10-7

### 编写测试

现在你已经注入一个实现 `IItemType` 接口的类的 Mock 实例，可以为 `InventoryService` WCF 服务编写单元测试了。你首先创建一个 `.cs` 文件来存放你的单元测试。我将此文件放在 `OSIM.UnitTests` 项目的 `OSIM.ExternalServices` 文件夹中，并命名为 `InventoryServiceTests.cs`，如图 10-8 所示。

为了测试 `InventoryService`，你需要在 `OSIM.UnitTests` 项目上引用 `OSIM.ExternalServices` 项目的项目，如图 10-9 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_237_0.png)

图 10-9

现在使用与之前相同的 BDD 命名风格创建你的测试类及其基类：

```csharp
namespace OSIM.UnitTests.OSIM.ExternalServices
{
    public class when_using_the_external_inventory_service : Specification
    {
        public class and_getting_list_of_item_types : when_using_the_external_inventory_service
        {
        }
    }
}
```

InventoryServiceTests.cs

为了使用 NUnit 框架中的属性，你需要添加一个 `using` 语句引入 `NUnit.Framework` 命名空间。你还需要创建 `InventoryService` 类的实例，因此也需要 `OSIM.ExternalServices` 命名空间。因为你将创建一个 `IItemTypeService` 核心领域服务的 Mock 实例，你还需要添加 `Moq` 命名空间以及 `OSIM.Core.Services` 命名空间的 `using` 语句。最后，与之前的单元测试一样，你使用 NBehavior 提供的扩展方法来评估结果，因此你需要包含 `NBehave.Spec.Unit` 命名空间：

```csharp
using Moq;
using NBehavior.Spec.Unit;
using NUnit.Framework;
using OSIM.Core.Services;
using OSIM.ExternalServices;
```

InventoryServiceTests.cs

测试的 `Because_of` 方法执行 `InventoryService` 的 `GetItemTypes` 方法并将字符串数组存储在变量 `results` 中：

```csharp
protected override void Because_of()
{
    _result = _inventoryService.GetItemTypes();
}
```

InventoryServiceTests.cs

当然，这要求你定义 `_result` 和 `_inventoryService` 成员变量：

```csharp
private IInventoryService _inventoryService;
private string _result;
```

InventoryServiceTests.cs

你为此测试类创建实际的测试方法。为了确保 `InventoryService` 运行正确，你需要验证 `_result` 数组中的元素数量是否正确，并且你 Mock 的 `IItemType` 返回的三个项目是否都体现在 `_result` 数组中。我将此方法命名为 `then_a_list_of_item_types_should_be_returned`：

```csharp
[Test]
public void then_a_list_of_item_types_should_be_returned()
{
    _result.Count().ShouldEqual(expectedNumberOfItems);
    _result.OfType<string>().Select(x => x == _itemOneName).FirstDefault().ShouldNotBeNull();
    _result.OfType<string>().Select(x => x == _itemTwoName).FirstDefault().ShouldNotBeNull();
    _result.OfType<string>().Select(x => x == _itemThreeName).FirstDefault().ShouldNotBeNull();
}
```

InventoryServiceTests.cs

此示例使用 `Select` LINQ 语句来验证测试设置中命名的项目是否存在于 `_results` 字符串数组中。你需要为此类添加一个 `using` 语句引入 `Linq` 命名空间：

```csharp
using System.Linq;
```

// InventoryServiceTests.cs

`then_list_of_item_types_should_be_returned` 测试方法使用了多个成员变量来报告此测试的预期值。你需要在测试类中声明它们：

```csharp
// 可从 W3.com 下载
private int _expectedNumberOfItems;
private string _itemOneName;
private string _itemTwoName;
private string _itemThreeName;
```

// InventoryServiceTests.cs

测试通过后，是时候运行它并观察结果了。此时我预计测试将会失败，事实如此（见图 10-10）。

![](img/15cb6759e167a2d15e60bc37de753a62_239_0.png)

图 10-10

### 打桩依赖项

`InventoryServiceTests.cs` 文件的第 41 行是对 `_inventoryService` 成员变量 `GetTypes` 方法的调用。在之前的章节中，我强调过在编写出需要代码的失败测试之前，不要编写任何代码。在编写测试时，同样的规则也适用。因为 `InventoryService` 有现有的应用程序代码，你可能不需要编写任何额外代码。当你编写测试时，你可能需要确保 `_inventoryService` 变量中包含一个 `ITypeService` 的 Mock。你需要通过 `Establish_context` 方法提供 `ITypeService` 的实例：

```csharp
protected void Establish_context()
{
    _itemTypeService = new Mock<ITypeService>();
    _inventoryService = new InventoryService(_itemTypeService.Object);
}
```

此时，你需要为 `itemTypeService` 声明：

```csharp
private Mock<ITypeService> _itemTypeService;
```

测试通过后，是时候再次运行它并查看是否通过了测试，如图 10-11 所示。

![](img/15cb6759e167a2d15e60bc37de753a62_240_0.png)

图 10-11

### 测试 WCF 服务

此错误指向了一个有趣的地方：`InventoryService.cs` 第 19 行抛出了 `ArgumentNullException`：

```csharp
var itemTypeList = _itemTypeService.GetItemTypes()
    .Select(x => x.Name)
    .ToArray();
```

![](img/15cb6759e167a2d15e60bc37de753a62_241_0.png)

InventoryService.cs

只要 `TypeService` 的 `GetTypes` 方法不返回 `null`，此行代码就可以工作。发生的情况是我正尝试编写一个可以验证看似正常的测试，结果发现了 `InventoryService` 类中 `GetTypes` 方法的一个潜在漏洞。如果没有彻底的单元测试，这个漏洞可能会一直穿整个流程直到生产环境才被发现。这应该是一个教训：不要低估简单的代码；缺陷可能存在任何地方。

第 12 章将涵盖测试和修复此缺陷。目前，此测试的解决方案是提供一个返回 `ItemType` 数组的 `ITypeService` Mock 给 `InventoryService`：

```csharp
_itemOneName = "USB drives"
_itemTwoName = "Nerf darts"
_itemThreeName = "Flying Monkeys"
var itemTypeOne = new ItemType(Id = 1, Name = _itemOneName);
var itemTypeTwo = new ItemType(Id = 2, Name = _itemTwoName);
var itemTypeThree = new ItemType(Id = 3, Name = _itemThreeName);
var itemTypeList = new List<ItemType>
{
    itemTypeOne,
    itemTypeTwo,
    itemTypeThree
};
_expectedNumberOfItems = itemTypeList.Count;
_itemTypeService.Setup(x => x.GetItemTypes()).Returns(itemTypeList);
```

InventoryServiceTests.cs

`ItemType` 位于 `OSIM.Core.Entities` 命名空间，因此你需要将该命名空间引入此测试类。同样，使用 `System.Collections.Generic` 命名空间中的 `List` 类，这需要如下的 `using` 语句：

```csharp
using System.Collections.Generic;
using OSIM.Core.Entities;
```

InventoryServiceTests.cs 文件中测试的完整实现现在应该是：

```csharp
using System.Collections.Generic;
using OSIM.Core.Entities;
using System.Linq;
using Moq;
using NBehave.Spec.NUnit;
using NUnit.Framework;
using OSIM.Core.Services;
using OSIM.ExternalServices;

namespace OSIM.UnitTests.OSIM.ExternalServices
{
    public class when_using_the_external_inventory_service : Specification
    {
    }

    public class class_and_getting_a_list_of_item_types : when_using_the_external_inventory_service
    {
        private IInventoryService _inventoryService;
        private string[] _result;
        private Mock<IItemTypeService> _itemTypes;
        private int _expectedNumberOfItems;
        private string _itemOneName;
        private string _itemTwoName;
        private string _itemThreeName;

        protected override void Establish_context()
        {
            base.Establish_context();
            _itemTypeService = new Mock<IItemTypeService>();
            _inventoryService = new InventoryService(_itemTypeService.Object);
            _itemOneName = "USB drives";
            _itemTwoName = "Nerf deats";
            _itemThreeName = "Flying Monkeys";
            var itemTypeOne = new ItemType(Id = 1, Name = _itemOneName);
            var itemTypeTwo = new ItemType(Id = 2, Name = _itemTwoName);
            var itemTypeThree = new ItemType(Id = 3, Name = _itemThreeName);
            var itemTypeList = new List<ItemType>
            {
                itemTypeOne,
                itemTypeTwo,
                itemTypeThree
            };
            _expectedNumberOfItems = itemTypeList.Count;
            _itemTypeService.Setup(x => x.GetItemTypes()).Returns(itemTypeList);
        }
    }

    protected override void Because_of()
    {
        _result = _inventoryService.GetItemTypes();
    }

    [Test]
    public void then_a_list_of_item_types_should_be_returned()
    {
        _result.Count().Should().Equal(expectedNumberOfItems);
        _result.OfType<string>().Select(x => x == _itemOneName).FirstDefault().ShouldNotBeNull();
        _result.OfType<string>().Select(x => x == _itemTwoName).FirstDefault().ShouldNotBeNull();
        _result.OfType<string>().Select(x => x == _itemThreeName).FirstDefault().ShouldNotBeNull();
    }
}
```
