

```csharp
}
}
}

protected override object GetColumnValue(MetaColumn column)
{
    try
    {
        return base.GetColumnValue(column);
    }
    catch (InvalidOperationException)
    {
        return this.ExtractFieldValue();
    }
}

public event EventHandler FieldValueChanged
{
    add { this.Events.AddHandler(FieldValueChangedEvent, value); }
    remove { this.Events.RemoveHandler(FieldValueChangedEvent, value); }
}

protected new UnleashedFieldTemplate FindOtherFieldTemplate(string columnName)
{
    return (UnleashedFieldTemplate)base.FindOtherFieldTemplate(columnName);
}

protected virtual void OnFieldValueChanged(EventArgs e)
{
    var eventHandler = (EventHandler)this.Events[FieldValueChangedEvent];
    if (eventHandler != null)
        eventHandler(this, e);
}

private object ExtractFieldValue()
{
    var dictionary = new OrderedDictionary();
    this.ExtractValues(dictionary);
    if (this.Column is MetaForeignKeyColumn)
    {
        var values = new object[dictionary.Count];
        dictionary.Values.CopyTo(values, 0);
        return string.Join(",", values);
    }
}

TypeConverter converter =
```

## FieldValueChanged 事件

OnFieldValueChanged 方法负责在 FieldValue 属性更改时调用 FieldValueChanged 事件处理程序（如果已分配）。遵循标准的 .NET 事件实现模式，该方法被声明为 virtual。这允许后代通过重写该方法来处理事件，这比分配事件处理程序更高效。

> **注意**
> 
> FieldValueChanged 事件显式定义了 add 和 remove 块，以利用从 ASP.NET Control 类继承的 Events 集合。该集合针对存储不经常分配的事件处理程序进行了优化，并允许您将事件处理程序存储在哈希表中，而不是为每个控件实例中的每个事件留出空间。FieldValueChangedEvent 对象被用作哈希键，用来存储和检索 FieldValueChanged 事件处理程序（如果有）。

## AutoPostBack 属性

字段模板的 AutoPostBack 属性封装了数据输入控件的 AutoPostBack 属性。使用者（如自定义的 Region 字段模板）通常需要在收到字段值更改的即时通知时设置它。不幸的是，ASP.NET 控件没有允许通用地设置其 AutoPostBack 属性的公共基类。各个字段模板负责根据该属性初始化其数据控件。

## 扩展现有字段模板

要利用新的 UnleashedFieldTemplate 基类提供的更好封装，您需要在每个现有字段模板中实现以下更改：

- 将字段模板改为继承自 `UnleashedFieldTemplate` 类。
- 使用字段模板的 `AutoPostBack` 属性的值设置数据控件的 `AutoPostBack` 属性值。
- 当数据控件的值更改时，引发 `FieldValueChanged` 事件。
- 当 `FieldValue` 更改时，更新数据控件的值。

除最后一项外，这些任务正是原始版本的 Region_Edit 字段模板所硬编码的。通过实现这些更改，您将此逻辑封装在每个通用字段模板内部，并允许自定义字段模板访问信息，而无需依赖其他模板的内部实现细节。清单 10.17 和 10.18 显示了已扩展的 Text_Edit 字段模板的标记和代码隐藏。本节的其余部分将讨论这些更改（以粗体表示）。

## 清单 10.17 扩展的 Text_Edit 字段模板（标记）

```
<%@ Control Language="C#" CodeBehind="Text_Edit.ascx.cs"
Inherits="WebApplication.DynamicData.FieldTemplates.TextEditField" %>

<asp:TextBox ID="textBox" runat="server" Text='<%# FieldValueEditString %>'
AutoPostBack='<%# AutoPostBack %>' Columns='<%# Columns %>'
OnTextChanged="TextBox_TextChanged"/>

<asp:RequiredFieldValidator runat="server" ID="requiredFieldValidator"
ControlToValidate="textBox" Enabled="false" />
<asp:RegularExpressionValidator runat="server" ID="regularExpressionValidator"
ControlToValidate="textBox" Enabled="false" />
<asp:DynamicValidator runat="server" ID="dynamicValidator"
ControlToValidate="textBox" />
```

### 更改字段模板的基类

由于字段模板的基类是在其代码隐藏文件（清单 10.18）中指定的，因此您需要将其从内置的 FieldTemplateUserControl 更改为新的 UnleashedFieldTemplate。

### 设置数据控件的 AutoPostBack 属性

Text_Edit 字段模板使用 TextBox 作为其数据控件。初始化其 AutoPostBack 属性的最简单方法是在模板的标记文件中使用 ASP.NET 数据绑定表达式 <%= AutoPostBack %>，如清单 10.15 所示。该表达式在页面首次生成时的数据绑定阶段计算。它将基类 UnleashedFieldTemplate 提供的 AutoPostBack 属性值分配给 TextBox 控件的 AutoPostBack 属性。

### 引发 FieldValueChanged 事件

Text_Edit 字段模板使用的 TextBox 控件提供 TextChanged 事件，您可以使用该事件检测用户何时更改其值。在模板标记中，TextBox_TextChanged 方法被分配为事件处理程序。其实现（如清单 10.18 所示）只是调用从 UnleashedFieldTemplate 继承的 OnFieldValueChanged 方法来引发 FieldValueChanged 事件。

## 清单 10.18 扩展的 Text_Edit 字段模板（代码隐藏）

```
using System;
using System.Collections.Specialized;
using System.Web.UI;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class Text_EditField : UnleashedFieldTemplate
    {
public override Control DataControl
{
    get { return this.textBox; }
}

public int Columns { get; set; }

protected void Page_Load(object sender, EventArgs e)
{
    this.textBox.ToolTip = this.Column.Description;
    if (this.Column.MaxLength < 20)
        this.textBox.Columns = this.Column.MaxLength;

    this.SetupValidator(this.requiredFieldValidator);
    this.SetupValidator(this.regularExpressionValidator);
    this.SetupValidator(this.dynamicValidator);
}

protected override void ExtractValues(IOrderedDictionary dictionary)
{
    dictionary[this.Column.Name] = this.ConvertEditedValue(this.textBox.Text);
}

protected override void OnDataBinding(EventArgs e)
{
    base.OnDataBinding(e);
    if (this.Column.MaxLength > 0)
    {
        this.textBox.MaxLength = Math.Max(
            this.FieldValueEditString.Length, this.Column.MaxLength);
    }
}

protected override void OnFieldValueChanged(EventArgs e)
{
    base.OnFieldValueChanged(e);
    this.textBox.Text = this.FieldValueEditString;
}

protected void TextBox_TextChanged(object sender, EventArgs e)
{
    this.OnFieldValueChanged(e);
}
}
```

## 当 FieldValue 更改时更新数据控件

模板的 FieldValue 属性也可能因字段模板之外的其他原因而更改，也许是另一个自定义字段模板。您可以想象一个自定义 ZipCode 字段模板，当用户输入有效的美国邮编时，它可以查找该邮编所代表的城市名称，并更改通用 Text_Edit 字段模板为 City 字段显示的值。

字段模板（Text_Edit）可以通过重写 OnFieldValueChanged 方法来检测 FieldValue 属性的更改，如清单 10.18 所示。注意，这个重写方法如何使用模板的 FieldValueEditString 属性设置 TextBox 控件的 Text 属性。正如第 3 章“字段模板”中所讨论的，该属性返回为编辑模式适当格式化的 FieldValue。该属性在模板标记中用于在数据绑定时为 Text 属性提供初始值，而重写的 OnFieldValueChanged 方法需要与此逻辑保持一致。

## 利用扩展的字段模板

凭借新版本的通用 Text_Edit 字段模板，您现在可以修改前面清单 10.15 中显示的自定义 Region_Edit 字段模板，使其不再依赖 Country 数据控件为 TextBox。在下一个示例中，其 OnLoad 方法被修改为初始化模板的 AutoPostBack 属性并分配其 FieldValueChanged 事件：

```csharp
private FieldTemplate countryFieldTemplate;

protected override void OnLoad(EventArgs e)
{
    base.OnLoad(e);
    this.countryFieldTemplate = this.FindOtherFieldTemplate("Country");
    this.countryFieldTemplate.AutoPostBack = true;
    this.countryFieldTemplate.FieldValueChanged +=
        CountryFieldTemplate_FieldValueChanged;
}
```

下面显示的 FieldValueChanged 事件处理程序替换了先前版本的 Region_Edit 字段模板中的 TextChanged 事件处理程序，后者必须直接从 TextBox 数据控件中提取当前字段值。既然 Country 字段模板的 FieldValueEditString 属性在回发期间可用，此方法使用它来更新下拉列表中的区域列表。请注意，这与页面首次生成时 OnDataBinding 方法中最初填充下拉列表的方式相同：

```csharp
private void CountryFieldTemplate_FieldValueChanged(
    object sender, EventArgs e)
{
    string country = this.countryFieldTemplate.FieldValueEditString;
    this.PopulateRegionList(country);
}
```

