

## 第23章：使用 Access 数据宏

### 图 23.1

每个 Access 表都包含五个可在使用 Datasheet 视图时选择的面向数据的事件。

![](img/1e45673ab6eca9d20e67635ff5b9b318_786_0.png)

### “Before” 事件

“Before” 事件（BeforeChange 和 BeforeDelete）非常简单，仅支持少数宏操作。它们支持程序流程结构（Comment、Group 和 If）以及仅 LookupRecord 数据块。它们提供的唯一宏数据操作是 ClearMacroError、OnError、RaiseError、SetLocalVar、SetField 和 StopMacro。

BeforeChange 事件类似于附加到窗体、报表和控件的 BeforeUpdate 事件。顾名思义，BeforeChange 在用户、查询或 VBA 代码更改表中的数据之前触发。

BeforeChange 让你有机会查看当前记录中的新值并在需要时进行更改。默认情况下，在 BeforeChange 或 BeforeDelete 数据宏中对字段的引用自动引用当前记录。

BeforeChange 是在将值提交到表之前验证用户输入的绝佳机会。图 23.2 中显示了一个简单示例。在这种情况下，tblProducts_BeforeChange 中 Description 字段的默认值被设置为 Description。如果用户在向表中添加新记录时未能更改 Description 字段，BeforeChange 事件会将该字段更新为“Please provide description。”

### 图 23.2

使用 BeforeChange 更新字段。

![](img/1e45673ab6eca9d20e67635ff5b9b318_786_1.png)

BeforeChange 事件无法通过消息框中断用户或阻止记录在底层表中更新。BeforeChange 能做的全部就是在记录添加到表或在表中更新之前设置字段的值或设置本地宏变量的值。

BeforeChange 会在对现有记录的更新和向表插入新记录时触发。Access 提供了 IsInsert 属性，该属性告诉宏当前更改是由于插入新记录的结果还是由于记录正在被更新。

图 23.3 说明了如何在使用 If 块中使用 IsInsert，以确保 BeforeChange 因向表中插入新记录而触发。

### 图 23.3

使用 IsInsert 确定 BeforeChange 是否因添加新记录而触发。

![](img/1e45673ab6eca9d20e67635ff5b9b318_787_0.png)

图 23.3 还说明了程序流程块（如 If）可以嵌套。外部 If 块检查 IsInsert 的值，而内部 If 有条件地设置 Description 字段值。

BeforeDelete 事件在几乎所有方面都与 BeforeChange 平行，因此此处不提供示例。使用 BeforeDelete 验证删除的条件是否合适。与 BeforeChange 一样，BeforeDelete 事件无法阻止记录的删除，但它可以根据情况设置本地变量或引发错误。

### “After” 事件

“After” 事件（AfterUpdate、AfterInsert 和 AfterDelete）比其“Before”对应事件更强大。这些事件中的每一个都支持整个数据宏操作族（DeleteRecord、SetField、SendEmail 等），因此你很可能会经常使用这些事件作为数据宏的基础。

图 23.4 显示了 AfterInsert 事件的典型用法。AfterInsert 事件在向表添加新记录时触发。新记录已经提交到表中，并且 AfterInsert 用于更新名为 tblProductActivityLog 的表。

### 图 23.4

使用 AfterInsert 向 tblProductActivityLog 添加记录。

![](img/1e45673ab6eca9d20e67635ff5b9b318_788_0.png)

在图 23.4 中，注意 tblProductActivityLog 中的三个字段（ProductActivity、ProductID 和 ProductDescription）正在作为 CreateRecord 数据块的一部分进行更新。ProductID 是 tblProducts_AfterInsert 中的 AutoNumber 字段。CreateRecord 块已经将记录添加到表中，因此新记录的 ProductID 值可供此数据宏使用。因此，当 SetField 宏操作更新 tblProductActivityLog 中的 ProductID 字段时，新产品记录的 ID 会成功添加到日志表中。

AfterInsert 数据宏在向表添加记录时运行。类似的数据宏可以添加到表的 AfterUpdate 和 AfterDelete 中以记录对表的其他更改。

“After” 事件最有用的方面是它们可以使用 ForEachRecord 宏块来遍历由表或查询提供的记录集。此功能使这些事件非常适合扫描表以检查一致性、向日志表添加记录或执行其他计算密集型更新。

### 使用宏生成器创建数据宏

数据宏使用与创建嵌入式和用户界面宏相同的宏生成器。一旦掌握宏生成器，你将用于所有宏开发和宏管理。主要区别在于 Action Catalog（在下一节中描述）包含的操作取决于上下文。

向表添加数据宏非常容易。事实上，Access 表甚至不必处于设计视图中——如果你愿意，可以向以数据表形式显示的表添加数据宏。你为表构建的数据宏会立即生效，因此你可以轻松地处理宏并观察宏的工作效果，而无需编译或在设计视图和数据表视图之间切换。

在 Chapter23.accdb 数据库中，首先以数据表视图打开 tblProducts。在功能区中，你将选择 Table 选项卡以显示表的数据事件（见图 23.1）。单击 After Update 命令以打开宏生成器（如图 23.5 所示）。最初，至少，看起来没什么可看的。

### 图 23.5

表的 AfterUpdate 事件的宏生成器。

![](img/1e45673ab6eca9d20e67635ff5b9b318_789_0.png)

左侧的大空白区域是宏设计区域。在此放置宏操作。右侧是 Action Catalog，是当前所有可用宏操作的层次列表。正在编程哪个表事件的唯一指示是在主 Access 窗口标题中以及宏设计区域上方的选项卡中。

在宏设计区域打开宏时，功能区包含你在处理宏时使用的多个工具。请注意，你可以折叠或展开宏部分、保存正在构建的宏并关闭宏生成器。

你会注意到图 23.6 中看到的功能区与处理嵌入式或标准宏时看到的功能区完全相同。然而，一些选项对你不可用。例如，Tools 组中的所有项目都是灰色的。这是因为数据宏不提供单步执行宏操作或转换为 VBA 代码的选项。数据宏旨在相对简单、简短、直截了当，而不是庞大而复杂。

顺便说一下，如果你的表处于设计视图中，你可以通过从 Design 选项卡中选择 Create Data Macros 命令来访问数据宏生成器（见图 23.6）。

### 图 23.6

表处于设计视图时选择表事件。

![](img/1e45673ab6eca9d20e67635ff5b9b318_790_0.png)

无论哪种情况，宏生成器都会如图所示打开 23.5。当使用 Access 选项卡式界面时，表的名称和所选事件会出现在宏生成器的选项卡中。如果选择了重叠窗口界面，此信息会出现在 Access 主窗口的标题中。

在图 23.6 中，注意 Create Named Macro 选项。命名宏就像附加到表事件的数据宏一样。唯一的区别是命名宏是自由浮动的，并且不专门绑定到特定事件。命名宏旨在从事件宏调用，通常实现对表的字段通用的逻辑。考虑前面描述的业务规则。如果表中的多个数据宏可能会更改产品的批发成本，你可能会创建一个命名宏来处理更新 RetailPrice 字段。命名宏然后可以被表的任何其他数据宏调用，以便表中的每个宏都以相同的方式处理更新。

### 了解 Action Catalog

宏生成器右侧的 Action Catalog 用作你添加到数据宏中的宏操作的存储库。Action Catalog 的内容完全取决于所选的表事件，因此你在处理 Access 宏时它的外观会大不相同。

