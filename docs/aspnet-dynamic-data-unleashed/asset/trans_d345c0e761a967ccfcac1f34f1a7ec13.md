

> **注意**
>
> 尽管字段模板查找算法看似复杂且需要大量的文件存在性检查，但实际上，Dynamic Data 只在某个列首次需要字段模板时才执行该查找。查找结果会存储在哈希表中，之后对该列的所有查找都基于内存完成，速度非常快。

## 内置字段模板

Visual Studio 2010 中的 Dynamic Data Web 项目模板包含大量可直接使用的字段模板。

### Boolean（布尔）

Boolean.ascx 字段模板用于只读模式下的 Boolean 列。它包含一个禁用的 CheckBox 控件，当字段值为 true 时呈选中状态。

![](img/11b373b78859e17d318fd76939a0df9d_129_0.png)

### Boolean_Edit（编辑布尔）

Boolean_Edit.ascx 字段模板用于编辑和插入模式下的 Boolean 列。它包含一个 CheckBox 控件，用户可用它来将字段值设置为 true 或 false。该字段模板不支持 null 值，并且与其他行为良好的字段模板不同，它不执行验证。

![](img/11b373b78859e17d318fd76939a0df9d_129_1.png)

### Children（子项）

Children.ascx 字段模板用于只读和编辑模式下的导航属性，这些属性表示实体之间一对多关系的“多”端。例如，Northwind 示例数据模型中的 Customer 实体有一个名为 Orders 的子导航属性，它返回给定客户所下所有订单的集合。在只读和编辑模式下，Children.ascx 实体模板会显示一个指向动态 List.aspx 页面的超链接，该页面显示父实体的所有子行。

![](img/11b373b78859e17d318fd76939a0df9d_129_2.png)

### Children_Insert（插入子项）

Children_Insert.ascx 字段模板是空的。由于动态 List.aspx 页面无法显示尚未提交到数据库的父实体的子行，因此该模板可防止 Children.ascx 字段模板在插入模式下被使用。

### DateTime（日期时间）

![](img/11b373b78859e17d318fd76939a0df9d_130_0.png)

DateTime.ascx 字段模板用于只读模式下显示 DateTime 字段值。该字段模板包含一个 Literal 控件，它将字段值直接注入网页，不添加任何修饰性的 HTML 元素。此模板与后续章节中介绍的 Text.ascx 模板几乎完全相同，因此可以移除，让 Text.ascx 也负责在只读模式下显示 DateTime 字段值。

### DateTime_Edit（编辑日期时间）

![](img/11b373b78859e17d318fd76939a0df9d_130_1.png)

DateTime_Edit.ascx 字段模板用于编辑和插入模式下的 DateTime 列。它包含一个 TextBox 控件，并配有一个 CustomValidator，用于确保在 TextBox 中输入的值是有效的 DateTime。它还包含一个 RequiredFieldValidator，用于强制为标记了 RequiredAttribute 的列提供值；一个 RegularExpressionValidator，用于强制为标记了 RegularExpressionAttribute 的列匹配正则表达式模式；以及一个 DynamicValidator，用于强制执行应用于该列的所有其他验证特性。

### Decimal_Edit（编辑十进制）

![](img/11b373b78859e17d318fd76939a0df9d_130_2.png)

Decimal_Edit.ascx 字段模板用于编辑和插入模式下的 Decimal、Float 和 Double 列。它包含一个 TextBox 控件，并配有一个 CompareValidator，用于确保在 TextBox 中输入的值是有效数字。它还包含一个 RequiredFieldValidator，用于强制为标记了 RequiredAttribute 的列提供值；一个 RangeValidator，用于强制为标记了 RangeAttribute 的列提供值的范围；一个 RegularExpressionValidator，用于强制为标记了 RegularExpressionAttribute 的列匹配正则表达式模式；以及一个 DynamicValidator，用于强制执行应用于该列的所有其他验证特性。

### EmailAddress（电子邮件地址）

![](img/11b373b78859e17d318fd76939a0df9d_130_3.png)

EmailAddress.ascx 字段模板是一个只读模板，用于标记了 DataType(DataType.EmailAddress) 特性的 String 列。它包含一个 HyperLink 控件，以 URL 方案“mailto:”的链接形式显示字段值。当用户单击此链接时，大多数 Web 浏览器会启动计算机上安装的默认电子邮件客户端，并创建一封新邮件，同时在“收件人”列表中自动填入该字段值。

### Enumeration（枚举）

![](img/11b373b78859e17d318fd76939a0df9d_130_4.png)

Enumeration.ascx 字段模板用于只读模式下的枚举列。它包含一个 Literal 控件，显示将基础整型字段值转换为其对应的枚举值、然后再转换为字符串的结果。

### ForeignKey（外键）

![](img/11b373b78859e17d318fd76939a0df9d_132_0.png)

ForeignKey.ascx 字段模板用于只读模式下的外键列。它包含一个 HyperLink 控件，显示父表“显示”列的字段值。你可以通过将 DisplayColumnAttribute 应用于父实体类来显式指定显示列，也可以根据 Dynamic Data 的启发式规则自动选择。用户可以单击该控件生成的链接，导航到父表的 List.aspx 页面。

### ForeignKey_Edit（编辑外键）

![](img/11b373b78859e17d318fd76939a0df9d_132_1.png)

ForeignKey_Edit.ascx 字段模板用于编辑和插入模式下的外键列。它包含一个 DropDownList 控件，显示父表中的所有行。父表的显示列决定每个 ListItem 的 Text，其主键列决定其 Value。

### Integer_Edit（编辑整数）

![](img/11b373b78859e17d318fd76939a0df9d_132_2.png)

Integer_Edit.ascx 字段模板用于编辑和插入模式下的 Byte、Int16、Int32 和 Int64 列。它包含一个 TextBox 控件，并配有一个 CompareValidator，用于确保在 TextBox 中输入的值是有效数字。它还包含一个 RequiredFieldValidator，用于强制为标记了 RequiredAttribute 的列提供值；一个 RangeValidator，用于强制为标记了 RangeAttribute 的列提供值的范围；一个 RegularExpressionValidator，用于强制为标记了 RegularExpressionAttribute 的列匹配正则表达式模式；以及一个 DynamicValidator，用于强制执行应用于该列的所有其他验证特性。

### ManyToMany（多对多）

![](img/11b373b78859e17d318fd76939a0df9d_132_3.png)

ManyToMany.ascx 字段模板用于多对多关系中的子列，例如 Northwind 示例数据库中的 Territory 实体的 Employees 列。此模板包含一个 Repeater 控件，为每个子实体生成一个 DynamicHyperLink。在实际页面上，这看起来像是一个超链接列表，用户可单击这些链接导航到特定子实体的 Details.aspx 页面。

> **注意**
>
> 多对多关系在 Entity Framework 中受到原生支持，但在 LINQ to SQL 中不受支持。因此，只有 Visual Studio 中 Dynamic Data 项目模板的 Entity Framework 版本包含 ManyToMany 字段模板。与同样适用于两种数据访问框架的其他字段模板不同，ManyToMany 字段模板直接使用 Entity Framework API。

LINQ to SQL 原生仅支持一对多关系，并且要求你在模型中有一个显式的多对多实体。不过，按照 Eric Smith 和 Shannon Davidson 在 Code Project 上发布的文章中描述的方法，实现一个简单的编码模式就可以模拟多对多关系。该文章可在以下网址在线找到：

http://www.codeproject.com/KB/linq/linq-to-sql-many-to-many.aspx

基于这种方法，可以为 LINQ to SQL 创建 Dynamic Data 多对多字段模板。不过，这项实践超出了本章的范围。

### ManyToMany_Edit（编辑多对多）

![](img/11b373b78859e17d318fd76939a0df9d_133_0.png)

ManyToMany_Edit.ascx 字段模板用于编辑和插入模式下的多对多子列。此模板包含一个 CheckBoxList 控件，为每个实体生成一个复选框，用户可通过勾选复选框将该实体添加到子项列表中。

### MultilineText_Edit（编辑多行文本）

![](img/11b373b78859e17d318fd76939a0df9d_133_1.png)

MultilineText_Edit.ascx 字段模板用于编辑和插入模式下的长字符串列。它包含一个 TextBox 控件，其 TextMode 属性设置为 MultiLine。它还包含一个 RequiredFieldValidator，用于强制为标记了 RequiredAttribute 的列提供值；一个 RegularExpressionValidator，用于强制为标记了 RegularExpressionAttribute 的列匹配正则表达式模式；以及一个 DynamicValidator，用于强制执行应用于该列的所有其他验证特性。

当字符串列在数据模型中没有指定最大长度时，即被视为长字符串列，例如 Northwind 示例中 Employee 实体的 Notes 列，其类型为 NTEXT。你也可以通过将 DataType(DataType.MultilineText) 特性应用于数据模型中相应列的属性，强制 Dynamic Data 对具有最大长度的列使用 MultilineText_Edit 字段模板。

### Text（文本）

![](img/11b373b78859e17d318fd76939a0df9d_133_2.png)

由于模板查找过程中使用的数据类型回退机制，Text.ascx 字段模板可用于只读模式下所有基元类型的列，但 Boolean 和 DateTime 列除外，Dynamic Data 为这些列提供了专门的模板。该字段模板包含一个 Literal 控件，显示转换为字符串后的字段值。

