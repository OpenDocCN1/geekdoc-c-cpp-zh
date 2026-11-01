

## 手动部署

你可以使用命令行工具 .NET 服务安装工具 `regsvcs.exe` 手动部署程序集。运行命令

```
regsvcs SimpleServer.dll
```

会将程序集 `SimpleServer` 注册为 COM+ 应用程序，并根据其特性配置所包含的组件；同时还会创建一个类型库，供访问 .NET 组件的 COM 客户端使用。

配置完程序集后，可以通过选择“管理工具 › 组件服务”启动组件服务资源管理器。在该应用程序的左侧树状视图中，你可以选择“组件服务 › 计算机 › 我的电脑 › COM+ 应用程序”来验证应用程序是否已配置成功。

![](img/d7d2ffa0a76feaab821930e95daace93_1641_0.png)

## 创建安装程序包

借助组件服务资源管理器，你可以为服务器或客户端系统创建 Windows 安装程序包。用于服务器的安装程序包包含程序集和配置设置，以便在其他服务器上安装该应用程序。如果从运行在不同系统上的应用程序调用服务组件，则必须在客户端系统上安装代理。用于客户端的安装程序包包含代理的程序集和配置。

要创建安装程序包，你可以启动组件服务资源管理器，选择 COM+ 应用程序，然后选择菜单选项“操作 › 导出”，并在第一个对话框中单击“下一步”按钮。此时会打开如图 51-4 所示的对话框。在该对话框中，你可以导出“服务器应用程序”或“应用程序代理”。选择“服务器应用程序”选项时，你还可以配置“导出包含角色在内的用户标识”。仅当目标系统与创建程序包的系统位于同一域中时，才应选择此选项，因为配置的用户标识会被放入安装程序包中。选择“应用程序代理”时，则会为客户端系统创建安装程序包。

![](img/d7d2ffa0a76feaab821930e95daace93_1641_1.png)

![](img/d7d2ffa0a76feaab821930e95daace93_1641_2.png)

要安装代理，你必须从安装程序包中启动 `setup.exe`。请注意，应用程序代理不能安装在已安装该应用程序的同一系统上。安装应用程序代理后，你可以在组件服务资源管理器中看到一个表示该应用程序代理的条目。对于应用程序代理，唯一可以配置的选项是“激活”选项卡中的服务器名称，这将在下一节中讨论。

此功能仅在开发期间有用。自动部署还需要管理员权限。如果你从 Visual Studio 中启动应用程序，则应以管理员权限启动 Visual Studio。

应用程序运行期间，你可以使用组件服务资源管理器监视服务组件。通过在树状视图中选择“组件”并选择“视图 → 详细信息”，如果设置了 [EventTrackingEnabled] 特性，则可以查看已实例化对象的数量。

如你所见，创建服务组件只需从基类 ServicedComponent 派生类，并设置一些特性来配置应用程序即可。接下来，你将了解如何将事务与服务组件一起使用。

## 事务

自动事务是企业服务中最常用的功能。使用企业服务，你可以将组件标记为需要事务，然后由 COM+ 运行时创建事务。组件内所有感知事务的对象（如 ADO.NET 连接）都在该事务内运行。

![](img/d7d2ffa0a76feaab821930e95daace93_1644_0.png)

### 事务特性

服务组件可以用 [Transaction] 特性进行标记，以定义组件是否需要事务以及需要何种事务。

图 51-7 显示了多个具有不同事务配置的组件。客户端调用组件 A。由于组件 A 配置为“要求事务”，且之前不存在事务，因此创建了新事务 1。组件 A 调用组件 B，组件 B 又调用组件 C。因为组件 B 配置为“支持事务”，而组件 C 的配置设置为“要求事务”，所以这三个组件（A、B 和 C）使用同一个事务上下文。如果组件 B 配置为“不支持事务”设置，组件 C 将获得一个新事务。组件 D 配置为“新建事务要求”设置，因此当它被组件 A 调用时会创建一个新事务。

![](img/d7d2ffa0a76feaab821930e95daace93_1644_1.png)

图 51-7

下表列出了可以使用 TransactionOption 枚举设置的不同值：

| TRANSACTIONOPTION 值 | 说明 |
|---|---|
| Required | 将 `[Transaction]` 特性设置为 `TransactionOption.Required` 意味着组件在事务内运行。如果已创建事务，组件将在同一事务中运行。如果不存在事务，则创建一个事务。 |
| RequiresNew | `TransactionOption.RequiresNew` 始终导致创建新事务。该组件永远不会与调用方参与同一事务。 |
| Supported | 使用 `TransactionOption.Supported`，组件本身不需要事务。但是，如果调用方和所调用的组件需要事务，则事务会跨越两者。 |
| NotSupported | 选项 `TransactionOption.NotSupported` 意味着组件绝不会在事务中运行，无论调用方是否有事务。 |
| Disabled | `TransactionOption.Disabled` 意味着当前上下文中可能存在的事务会被忽略。 |

### 事务结果

可以通过设置上下文的“一致位”和“完成位”来影响事务。如果一致位设置为 true，则组件对事务的结果满意。如果参与该事务的所有组件都同样成功，则事务可以提交。如果一致位设置为 false，则组件对事务的结果不满意，并且在启动事务的根对象完成时，事务会中止。如果设置了完成位，则在方法调用结束后对象可以被停用。下一次方法调用时会创建新实例。

可以使用 ContextUtil 类的四个方法设置一致位和完成位，结果如下表所示。

| CONTEXTUTIL 方法 | 一致位 | 完成位 |
|---|---|---|
| SetComplete | True | True |
| SetAbort | False | True |
| EnableCommit | True | False |
| DisableCommit | False | False |

使用 .NET，还可以通过将 [AutoComplete] 特性应用于方法而不是调用 ContextUtil 方法来设置一致位和完成位。使用此特性时，如果方法成功，会自动调用 ContextUtil.SetComplete() 方法。如果方法失败并抛出异常，则使用 [AutoComplete] 时会调用 ContextUtil.SetAbort() 方法。

### 示例应用程序

此示例应用程序模拟了一个简化的场景，即向 Northwind 示例数据库写入新订单。如图 51-8 所示，多个组件用于 COM+ 应用程序。客户端应用程序调用 OrderControl 类来创建新订单。OrderControl 使用 OrderData 组件。OrderData 负责在 Northwind 数据库的 Order 表中创建新条目。OrderData 组件使用 OrderLineData 组件将 Order Detail 条目写入数据库。OrderData 和 OrderLineData 都必须参与同一事务。

```
internal void SetOrderId(int orderId)
{
    this.OrderId = orderId;
}

public void AddOrderLine(OrderLine orderLine)
{
    orderLines.Add(orderLine);
}

private readonly List<OrderLine> orderLines = new List<OrderLine>();

public int OrderId { get; private set; }
public string CustomerId { get; private set; }
public DateTime OrderDate { get; private set; }
public string ShipAddress { get; private set; }
public string ShipCity { get; private set; }
public string ShipCountry { get; private set; }

public OrderLine[] OrderLines
{
    get
    {
        OrderLine[] ol = new OrderLine[orderLines.Count];
        orderLines.CopyTo(ol);
        return ol;
    }
}
```

*代码片段 NorthwindComponents/Order.cs*

第二个实体类是 OrderLine。OrderLine 有一个静态的 Create() 方法，与 Order 类的方法类似。除此之外，该类只有一些属性 ProductId、UnitPrice 和 Quantity：

```
using System;

namespace Wrox.ProCSharp.EnterpriseServices
{
    [Serializable]
    public class OrderLine
    {
        public static OrderLine Create(int productId, float unitPrice, int quantity)
        {
            return new OrderLine
            {
                ProductId = productId,
                UnitPrice = unitPrice,
                Quantity = quantity
            };
        }
        public OrderLine()
        {
        }

        public int ProductId { get; set; }
        public float UnitPrice { get; set; }
        public int Quantity { get; set; }
    }
}
```

*代码片段 NorthwindComponents/OrderLine.cs*

