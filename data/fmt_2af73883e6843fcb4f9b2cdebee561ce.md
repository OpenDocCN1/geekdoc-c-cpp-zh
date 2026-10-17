
一旦通过 `K2 Service Object Designer` 创建并将服务对象发布到 K2 服务器，它就可以用于任何 K2 SmartObject。在本示例中，使用了上一个示例创建的 `EmployeeServiceObject` 来创建一个新的 `EmployeeSmartObject`。

1. 打开上一个示例中创建的 `EmployeeServiceObject` 项目。
2. 右键点击项目名称并选择 `Add New Item`（新建项），向项目添加一个 SmartObject。
3. 在打开的对话框中，选择 `K2 SmartObject`。将新的 SmartObject 命名为 `Employee`。该 SmartObject 将基于添加到 `EmployeeServiceObject` 中的 SAP 信息，因此需要删除为此 SmartObject 创建的默认方法。
4. 在 `K2 SmartObject Designer` 中点击 `Advanced Mode`（高级模式）。
5. 在设计器的 SmartObject Methods 部分，点击 `Remove All`（全部删除）以删除默认方法。
6. 若要添加方法，在 SmartObject Methods 部分点击 `Add`（添加）。打开 SmartObject Method 向导。
7. 为了设置参数，SmartObject Method 向导将打开。
8. 在 `Method Details`（方法详情）屏幕上，为方法命名为 `GetList`。属性看起来应该像图 23-15 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_854_0.png)

图 23-15

## 第 23 章：介绍 K2 connect

在 `Method Parameters`（方法参数）屏幕上，包含了以下参数：

| 参数名称 | 类型 |
| :--- | :--- |
| `p_InputDate` | Date |
| `p_FirstName` | Text |
| `p_LastName` | Text |

添加参数后，`Method Parameters` 屏幕应该像图 23-16。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_855_0.png)

图 23-16

现在服务对象需要关联方法。在这种情况下，`GetList` 方法将使用 `Employee`。在浏览器窗口中，进入 `ServiceObject -> [MachineName] -> EmployeeServiceObject` 并选择 `GetList` 方法。见图 23-17。

### 第五部分：高级 K2 blackpearl 概念与平台扩展

![](img/20dd98d522a8a8d52ab6ce563d548ca5_856_0.png)

图 23-17

服务对象的所有输入参数和属性已更新到接口和 SmartObject。

12. 首先通过点击每个参数的 `Assign`（分配）按钮并遵循下表来分配输入参数：

| 服务方法参数 | 映射到 | SmartObject 属性名称 |
| :--- | :--- | :--- |
| `p_InputDate` | Date | `InputDate` |
| `p_FirstName` | Text | `FirstName` |
| `p_LastName` | Text | `LastName` |

13. 对于剩余属性，将创建相应的 SmartObject 属性。
14. 点击返回部分的 `EmployeeInfo_EmployeeID` 并选择 `Assign`。
15. 点击按钮。在 `SmartObject Property Name` 字段中输入 `Employee ID`。点击 `OK`，然后再次点击 `OK`。

对于每个额外的返回属性，按照相同的步骤配置每个 SmartObject 属性，使用下表提供的信息：

| 服务方法属性 | SmartObject 属性名称 |
| :--- | :--- |
| `EmployeeInfo_EmploymentStartDate` | `Employment Start Date` |
| `EmployeeInfo_LastName` | `Last Name` |
| `EmployeeInfo_FirstName` | `First Name` |
| `EmployeeInfo_Birthplace` | `Birthplace` |
| `EmployeeInfo_BirthYear` | `Birth Year` |

16. 当所有属性都映射完成后，点击 `OK` 关闭窗口。`ServiceObject Methods` 屏幕应该像图 23-18 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_857_0.png)

图 23-18

17. 点击 `Next`（下一步）和 `Finish`（完成）完成向导。

# 第五部分：高级 K2 blackpearl 概念与平台扩展

部署状态显示在 Visual Studio 环境的左下角。当显示 `"Deploy succeeded"` 时，表示部署成功。

`Employee SmartObject` 可用于任何应用程序中显示 SAP 数据。这些数据可以在 InPath 或 ASP.NET 表单中、使用 `K2 Report Designer` 构建的报告中、作为 K2 工作流过程的一部分、包含任何其他基于 .NET 的应用程序（如 SharePoint Server）中，或通过 `.NET Data Provider for K2 SmartObjects` 直接查询。有关在这些不同应用程序中使用 K2 SmartObjects 的更多信息，请参阅第 7 章。

> 在上一个示例中，`K2 connect for SAP` 用于一个简单的场景来从 SAP 显示员工信息。然而，可以遵循相同的基本步骤，根据组织的需要提供更复杂的功能。使用 `K2 connect for SAP` 中的 `K2 SmartObject Designer`，可以从单个 Service Object 调用 API 方法、在 SAP 环境中创建对象以及过滤 API 结果。所有这些任务都可以在不编写单行代码的情况下完成。这些高级场景的特定示例可以在 `K2 connect for SAP` 产品文档附带的指南中找到。

### 总结

在本章中，您将介绍了 `K2 connect for SAP`，它是 `K2 blackpearl` 的一个组件，提供了一个接口，用于针对 SAP 业务实体建模而无需编写代码。我们讨论了 `K2 connect` 的架构以及它如何融入 `K2 blackpearl` 平台。

在深入研究如何使用 `K2 connect for SAP` 构建简单的 Service Object 的示例之前，我们概述了 `K2 Service Object Designer` 和设计画布（Design canvas），并介绍了如何在 K2 SmartObject 中使用该 Service Object 以集成到任何应用程序中（例如表单、报告、K2 工作流过程或其他基于 .NET 的应用程序）。

最后，我们简要提到了 `K2 connect` 中的高级主题，以让您了解 `K2 connect for SAP` 开启的许多可能性。

通过减少访问 SAP 所需的代码量并提供易用工具，`K2 connect for SAP` 减少了开发时间，并允许业务用户以重用且简单的方式访问相关的 SAP 信息。

## K2 blackpearl 技巧与

当我们开始写这本书时，我们希望确保每个读者读完后都能带一些有用的信息，不仅来自每章包含的信息，还来自每个作者提供的见解。这在很大程度上解释了为什么选择这些作者参与。他们来自不同的领域，并帮助您利用 K2 平台。为了进一步这一理念，我们从更广泛的受众中收集了各种技巧和“如何做”信息，包括来自全球的 K2 员工以及发现省时间技术的社区代表。其中一些内容您可能已经在各种 K2 博客上见过，另一些将是全新的。我们希望您发现其中有很多用。

### 从 XML 字段元素检索值

作者：Joseph Dunagan，K2 顾问

有时您需要从 K2 XML 文件的元素中获取值。这通常发生在服务器事件内部。在下面的示例中，我需要从 K2 生成的 XML 字段中检索 URL。如果您不预期 `Items` 节点中有重复值，此特定示例应该可以工作。对于选择了重复值的场景，您需要更改 XPath。

```csharp
// 从 K2 XML 字段中获取 XML
string strXML = K2.ProcessInstance.XmlFields["SPEEventsField"].Value;
// 将 XPath 设置为所需的路径
string strXPath = "/Items/Item/URL";
// 使用辅助类检索此元素的值
// （如在 XPath 中设置的那样）针对此 XML
string strValue = SourceCode.Workflow.Common.XmlHelper.GetXPathValue(strXML, strXPath);
```

# 附录 A：K2 blackpearl 技巧与

### InfoPath 中带历史记录的超简单备注字段

作者：Joseph Dunagan，K2 顾问

基于 InfoPath 的过程通常需要一个备注字段，允许用户添加而不是编辑备注历史。这是一个包含几个规则和一个隐藏文本字段的快照。

1. 在 InfoPath 表单上，创建三个文本框和一个按钮。所有文本框都应该是多行的。在我的情况下，我将它们命名为：
   - `NewNote`
   - `NotesHistory`
   - `CarriageReturn`
   - `SaveNewNote`（按钮）
2. `NotesHistory` 文本框应该是最大的（可能是 8 或 10 行；表单的完整宽度），因为它将显示所有之前的备注。此文本框在控件属性中应设置为只读。
3. 我通常让 `NewNote` 文本框足够容两行文本（表单的完整宽度）。
4. `SaveNewNote` 按钮应该放在 `NewNote` 文本框和 `NotesHistory` 文本框之后，并附带类似“点击此按钮将保存新注释”的说明。
5. `CarriageReturn` 文本框应该是隐藏的，并在函数生成器中设置其默认值：
   - 输入一个左引号（"）。
6. 最后为 `SaveNewNote` 字段创建一个规则：`NotesHistory` ⋄ Value（函数体）：`concat(today(), ":", NewNote, CarriageReturn, NotesHistory)`。注意，`NewNote`、`CarriageReturn` 和 `NotesHistory` 是使用“插入字段或组”按钮插入的。
   - 设置字段的值 ⋄ 字段：`NewNote` ⋄ Value（留空值）。

此按钮将成功地用新注释更新到 `NotesHistory` 中，新注释位于顶部并以当前日期开头。

### 检索进程实例数据

作者：Bob Maggio，K2 架构师

通常，您需要从某些应用程序中访问 K2 内置报告的数据。标准的 K2 报告是基于 SmartObjects 构建的，并且您可以使用这些 SmartObjects 来访问数据。第一件事是了解哪些内置 SmartObjects 是可用的，您可以在图 A-1 中看到 SmartObjects 的列表。

如果您想像图 A-2 所示获取进程实例数据，可以使用 K2 Service Object 进行程序化处理。以下代码示例创建了一个接受方法名称和进程 ID 方法，为了简单起见，我直接返回 Response。

```csharp
private void GetData(string strObjectName, int procInst)
{
    SourceCode.SmartObjects.Client.ConnectionString connectionString =
        new SourceCode.SmartObjects.Client.ConnectionString();
    // 构建连接字符串
    connectionString.Authenticated = true;
    connectionString.Host = "localhost";
    connectionString.Integrated = true;
    connectionString.Port = 5555;
    // 打开连接
    connectionString.Open();
    try
    {
        // 获取
        SourceCode.SmartObjects.Client.SmartObject smartObject =
            connectionString.SmartObject(strObjectName);
        // 指定方法参数
        smartObject.Properties["ProcessID"] = procInst.ToString();
        // 调用方法
        SourceCode.SmartObjects.Client.SmartObject osList =
            smartObject.ExecuteMethod("List");
        // 遍历集合中的 smartobject
        foreach (SourceCode.SmartObjects.Client.SmartObject osMo in osList)
        {
            // 为了这个示例，我只是构建一个字符串
            string strRecord = "";
            foreach (SourceCode.SmartObjects.Client.SmartProperty oProp in osMo.Properties)
            {
                strRecord += oProp.Name + " : " + oProp.Value.ToString() + ",";
            }
            Response.Write(strRecord + "<br/>");
        }
    }
    catch (Exception)
    {
        // 关闭连接
        connectionString.Close();
    }
}
```

当我在以下参数调用此方法时：

```
GetData("Activity_", 4782);
```

我看到了（见图 3），这指向了数据。

## 附录 A：K2 blackpearl 提示与技巧

显然这只是一个展示如何与这些 SmartObjects（智能对象）交互的简单示例。还能用它们做其他事情吗？例如，如果你不想编写任何代码，可以使用 K2 SmartObjects 的 `.NET Data Provider` 将结果绑定到控件上。你还可以将这些对象作为表集成到 InfoPath 中。

此外，一种与这些 SmartObjects（以及任何 SmartObjects）交互的非常实用的方法是使用 `Amazing SmartObject Tool`，该工具在 K2 黑市（http://k2underground.com/k2/ProjectHome.aspx?ProjectID=47）上免费提供，并包含在 `K2 blackpearl (0807)` 中。我强烈建议任何开发或处理 SmartObjects 工作的人员使用此工具。（注意：你必须在该网站上创建一个成员账户才能查看该工具。）

# 根据重复的 XML 元素设置活动目标用户

作者：Bob Maggio，K2 架构师

`K2 blackpearl` 扩展规则功能的已知特性之一是能够非常容易地根据包含用户 ID 的重复 XML 节点来设置目标用户。在 K2 2003 中，这需要在每个想要执行此类操作的活动目标规则（Destination Rule）中编写一些代码。而在 `K2 blackpearl` 中，这现在是流程设计画布上的一个拖放体验。这在模式驱动的流程开发工作中这可能是一个非常实用的功能。

在例示例中，我将展示如何利用 InfoPath 表单捕获用户列表，然后该列表将作为下一步“目标规则”的依据。

1. 照常方式创建一个 InfoPath 表单和集成了 InfoPath 的 K2 流程。
2. 照常方式设计表单。
3. 在主数据源中添加一个新的重复文本（string）元素，如图 A-4 所示（在本示例中，我们将该字段命名为“`Reviewers` 评审人员]”）。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_864_0.png)

图 A-4

4. 然后我将重复文本字段拖到所需的 InfoPath 视图中，如图 A-5 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_865_0.png)

图 A-5

5. 在此示例中，我执行了以下操作：
   - 在提示时选择了“重复表”（Repeating Table）。
   - 将文本框更改为下拉列表（List）。
   - 向下拉列表中添加了内容，允许用户从易于阅读的下拉列表中选择评审人员（实际的 `Domain\userID` 作为隐藏值），如图 A-6 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_865_1.png)

图 A-6

6. 保存并关闭 InfoPath 表单。
7. 你现在应该回到了流程设计画布，并看到如图 A-7 所示的消息。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_866_0.png)

8. 点击“确定”，然后点击“完成”。
9. 在此示例中，我们随后想要通过点击如图 A-8 所示的目标规则图标来更改所需活动的目标规则。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_866_1.png)

10. 在目标规则窗口打开的情况下，导航到“目标用户”窗口，如图 A-9 所示。

![](img/20dd98d522a8a8d52ab6ce563d548ca5_867_0.png)

图 A-9
