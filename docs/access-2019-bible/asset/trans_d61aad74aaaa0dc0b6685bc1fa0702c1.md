

在将汇总数据放入主窗体之前，其值必须先在子窗体中找到。为此，在子窗体中任意位置放置一个文本框，并将其 Visible 属性设置为 No（False），使其隐藏。将汇总表达式，例如 = Count ([ProductID])，放入隐藏控件的 Control Source 属性中。

在主窗体中，插入一个新的文本框，并将 Control Source 设置为以下值：
= [Subform1].Form![Name-of-Aggregate-Control]

其中 Subform1 是主窗体上包含嵌入式子窗体的控件的名称，而 Name-of-Aggregate-Control 是子窗体上包含汇总数据的控件的名称。控件的名称，例如本例中的 Subform1，并不一定是该控件所包含的 Form 对象的名称。当你在控件名称后加上 .Form 时，你引用的是底层的窗体，而无需知道其对象名称。

主窗体上的控件在子窗体中更改其值时每次都会更新。

## Form Design Tips

以下是一些窗体设计技巧合集，你可能会觉得很实用。我们希望它们能激发你自己想出更多技巧！

## Using the Tab Stop property

有时，你可能会在窗体上放置一个控件，其目的是触发相当激进的结果，例如删除记录或打印长报表。如果你想降低用户可能意外激活该控件的风险，你可能希望使用 Tab Stop 属性，该属性指定是否可以使用 Tab 键将焦点移动到该控件。

例如，假设你在一个窗体上放置了一个名为 cmdDelete 的命令按钮，用于删除当前记录。你不希望用户不小心点击此按钮。将 cmdDelete 的 Tab Stop 属性修改为 No，以将其从窗体的制表符顺序中移除（默认值为 Yes）。用户必须显式点击按钮才能激活它，并且用户在输入数据时不会意外选择它。

## Tallying check boxes

如果您需要计算复选框控件中 True 值的数量，请考虑使用以下表达式：

```
Sum(Abs([CheckBoxControl]))
```

Abs 将每个 -1 转换为 1，而 Sum 函数将它们相加。要计算 False 值，请使用以下表达式：

```
Sum([CheckBoxControl] + 1)
```

每个 True 值（-1）被转换为 0，每个 False 值（0）被转换为 1，然后再求和。

## Setting up combo boxes and list boxes

组合框和列表框是您窗体构建工具箱中的强大工具，但设置起来可能很复杂。在构建组合框和列表框时，重要的是要记住 Control Source（控件保存和加载数据的表或查询字段）和 Row Source（列表中显示的数据的来源）之间的区别。因为组合框和列表框支持多列，所以它们允许您轻松地关联来自另一个表的数据，而无需基于联接表的查询来设计窗体。这种技术涉及一个绑定组合框或列表框控件，该控件存储 ID 号码但在列表中显示名称，在 Chapter19.accdb 中名为 frmContacts_Northwind 的窗体中的 Organization 组合框中使用了该技术。

例如，假设您正在创建一个窗体来显示有关您的客户和顾客（您的“联系人”）的信息，并且您希望标识这些联系人所属的组织。在设计良好的数据库中，您只需为每个联系人记录存储一个组织 ID 号码，而将组织的名称和其他信息存储在单独的表中。您希望窗体包含一个组合框，在列表中显示组织名称和地址，但将组织 ID 号码存储在字段中。（有关此技术的示例，请参阅 Chapter19.accdb 中的 frmContacts_Northwind。）

要实现您的设计目标，请创建一个多列组合框。将 Control Source 设置为 OrgID 字段（Contacts 表中包含每个联系人的组织 ID 号码的字段）。将组合框的 Row Source Type 属性设置为 Table/Query。您可以基于表来构建列表，但您希望名称列表按排序顺序排列；因此，将 Row Source 属性设置为查询，该查询在第一个字段中包含 OrgID 号码，并在第二个字段中按升序包含组织名称。执行此操作的最佳方法是使用 Row Source 属性的查询生成器创建 SQL 语句；或者，您可以创建并保存一个查询来提供列表。在 frmContacts_Northwind 示例（Organization 组合框）中，Row Source 查询如下：

```
SELECT Organizations.OrgID, Organizations.Name,
Organizations.AddressLine1, Organizations.AddressLine2,
Organizations.City, Organizations.State,
Organizations.ZipCode, Organizations.Country
FROM Organizations ORDER BY Organizations.Name
```

由于您有兴趣在组合框中查看所有这些数据列表，请将 Column Count 属性设置为 8（SELECT 语句中的字段数）。您将在一分钟内隐藏 OrgID 列，但您需要在组合框 Row Source 中包含它，因为它包含控件在用户选择一行时保存的数据。此列由组合框的 Bound Column 属性标识（默认设置为 1）。包含 ID 号码的绑定列不必对用户可见。Column Widths 属性包含下拉列表中列的可视列宽的以分号分隔的列表。Access 使用默认算法来确定您未明确选择宽度的任何列的宽度。如果您为任何列选择宽度为 0，则该列在屏幕上对用户隐藏，但不会对您的其他窗体、VBA 代码或宏隐藏。在本例中，您将该属性设置为以下内容：

```
0";1.4";1.2";0.7";0.7";0.3";0.5";0.3"
```

这指示 Access 您希望第一列不可见，并为其他列设置明确的列宽。

第二列——在本例中为组织名称——是用户文本输入进行匹配的列。组合框中第一个可见列始终用于此目的。图 19.5 显示了 resulting 下拉列表。虽然这是一个加载组合框数据的极端示例，但它有效地说明了 Access 组合框控件的强大功能。

## FIGURE 19.5

Organization 组合框的下拉列表。

![](img/1e45673ab6eca9d20e67635ff5b9b318_618_0.png)

在使用组合框时，如果将 Limit To List 属性设置为 Yes，则用户只能从下拉列表中的条目中进行选择。然后，您可以为控件的 NotInList 事件构造一个事件过程，以处理如果用户输入列表中不存在的值时应发生的情况。您可能希望打开一个窗体，用户可以在其中输入新信息；或者，也许您希望显示一个消息框，指示用户应遵循什么程序来添加数据。

## Tackling Advanced Forms Techniques

Access 在其窗体设计和用户界面功能中包含许多强大而令人兴奋的功能。正如您现在所知，应用程序中的窗体是用户界面的主要组成部分。在很大程度上，用户对应用程序易用性和强度的感知是由其用户界面的吸引力和有效性决定的。Microsoft 已为 Access 窗体提供了控制用户界面的重要功能。其中许多功能在 Access 中已经存在很长时间，但尚未被许多开发人员讨论。

## Using the Page Number and Date/Time controls

窗体通常包含当前日期和时间。许多开发人员通过未绑定的文本框以及 Date() 函数将此信息添加到窗体或报表中，以将此信息返回给未绑定的文本框。Access 通过设计选项卡上功能区“页眉/页脚”组中的日期和时间命令简化了此过程（见图 19.6）。

## FIGURE 19.6

这些命令简化了向窗体和报表添加日期的过程。

![](img/1e45673ab6eca9d20e67635ff5b9b318_619_0.png)

图 19.6 显示了窗体处于设计视图时功能区。

当选择日期和时间命令时，日期和时间对话框（如图 19.7 所示）会出现，询问您希望如何格式化日期和时间。在您做出选择并单击确定后，Access 会添加一个包含按您要求格式化的日期和时间的窗体页眉。如果您改变了对日期或时间格式的主意，您始终可以更改此命令添加的文本框的 Format 属性。页眉中显示的日期和时间反映的是打开窗体的时间，而不一定是当前时间。

页眉/页脚组还包括用于向窗体页眉区域添加徽标（几乎任何图像文件）和标题的其他命令。在应用程序中使用页眉/页脚控件可使所有窗体具有一致的外观（见图 19.8，即示例数据库中的 frmDialog）。

