

Table 和 Value 属性存储其主键列的逗号分隔列表。此代码依赖于 `FieldTemplateUserControl` 基类提供的名为 `PopulateListControl` 的便捷方法，该方法完成了查询被引用表、创建 `ListItem` 对象并将其添加到 `DropDownList` 所需的全部繁重工作。

### 清单 3.10 ForeignKey_Edit 字段模板（代码隐藏）

```csharp
using System;
using System.Collections.Specialized;
using System.Web.DynamicData;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class ForeignKey_EditField : FieldTemplateUserControl
    {
        public override Control DataControl
        {
            get { return this.dropDownList; }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            if (this.dropDownList.Items.Count == 0)
            {
                if (this.Mode == DataBoundControlMode.Insert || !this.Column.IsRequired)
                    this.dropDownList.Items.Add(new ListItem("[Not Set]", string.Empty));
                this.PopulateListControl(this.dropDownList);
            }

            this.SetUpValidator(this.requiredFieldValidator);
            this.SetUpValidator(this.dynamicValidator);
        }

        protected override void OnDataBinding(EventArgs e)
        {
            base.OnDataBinding(e);
            string selectedValueString = this.GetSelectedValueString();
            if (this.dropDownList.Items.FindByValue(selectedValueString) != null)
                this.dropDownList.SelectedValue = selectedValueString;
        }
    }
}
```

### 清单 3.11 PhoneNumber_Edit 字段模板（标记）

```aspx
<%@ Control Language="C#" CodeBehind="PhoneNumber_Edit.ascx.cs"
    Inherits="WebApplication.DynamicData.FieldTemplates.PhoneNumberEditField" %>

<asp:TextBox ID="textBox" runat="server" Text='<%# FieldValueEditString %>'/>

<ajax:FilteredTextBoxExtender TargetControlID="textBox" runat="server"
    FilterType="Custom" ValidChars="()+-1234567890" />

<asp:RequiredFieldValidator runat="server" ID="requiredFieldValidator"
    ControlToValidate="textBox" Enabled="false" />
<asp:RegularExpressionValidator runat="server" ID="regularExpressionValidator"
    ControlToValidate="textBox" />
<asp:DynamicValidator runat="server" ID="dynamicValidator"
    ControlToValidate="textBox" />
```

如你所见，PhoneNumber_Edit 字段模板与之前讨论的 DateTime 模板类似。它包含一个用于输入电话号码的 TextBox 控件、一个 FilteredTextBoxExtender（另一个 AJAX 控件，用于防止用户输入电话号码中无效的符号），以及若干验证控件。

尽管使用单个 DynamicValidator 控件就足以强制执行数据模型中应用于该列的所有验证属性，但该控件仅在服务器端执行验证，因此需要回发（post-back）后才能报告错误。其他 ASP.NET 验证控件（如 RequiredFieldValidator）是可选的，但由于它们还提供客户端验证逻辑，因此最好将其包含在字段模板中，以便向用户提供即时反馈，并改善数据输入体验。

清单 3.12 展示了 PhoneNumber_Edit 字段模板的代码隐藏。

### 清单 3.12 PhoneNumber_Edit 字段模板（代码隐藏）

```csharp
using System;
using System.Collections.Specialized;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Web;
using System.Web.DynamicData;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class PhoneNumberEditField : FieldTemplateUserControl
    {
        public override Control DataControl
        {
            get { return this.textBox; }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            this.textBox.ToolTip = this.Column.Description;

            this.SetUpValidator(this.requiredFieldValidator);
            this.SetUpValidator(this.dynamicValidator);
            this.SetUpRegexValidator(this.regularExpressionValidator);
        }

        protected override void ExtractValues(IOrderedDictionary dictionary)
        {
            dictionary[this.Column.Name] = this.ConvertEditedValue(this.textBox.Text);
        }

        private void SetUpRegexValidator(RegularExpressionValidator validator)
        {
            RegularExpressionAttribute attribute = this.Column.Attributes
                .OfType<RegularExpressionAttribute>().FirstOrDefault();
            if (attribute == null)
            {
                attribute = new RegularExpressionAttribute(@"^\(\d{3}\) \d{3}-\d{4}");
                attribute.ErrorMessage = "The field {0} must be a valid phone number.";
            }

            validator.Enabled = true;
            validator.Text = "*";
            validator.ValidationExpression = attribute.Pattern;
            validator.ErrorMessage = HttpUtility.HtmlEncode(
                attribute.FormatErrorMessage(this.Column.DisplayName));
            validator.ToolTip = validator.ErrorMessage;

            this.IgnoreModelValidationAttribute(attribute.GetType());
        }
```

新字段模板中的大部分电话号码验证由标准 ASP.NET 控件 RegularExpressionValidator 执行，该控件确保用户输入的值与定义有效电话号码的正则表达式模式匹配。除了基于 System.Text.RegularExpressions 命名空间中 .NET 正则表达式实现的服务器端验证外，它还可以利用 JavaScript 中的正则表达式功能在客户端工作。

```csharp
public object HomePhone;
}
}
```

应用于 HomePhone 列的 DataTypeAttribute 指定该字符串列的实际数据类型为 PhoneNumber。Dynamic Data 在为此列查找匹配的字段模板时，会利用此信息作为提示，并选择新的 PhoneNumber_Edit 模板，而不是默认的 Text_Edit。在本示例中，RegularExpressionAttribute 也应用于 HomePhone 列，以提供一个模式，该模式不仅匹配具有三位区号的美国电话号码，还匹配可能具有两位区号的英国号码。

图 3.3 展示了完成 PhoneNumber_Edit 字段模板实现后的 Employee 编辑页。虽然从该屏幕截图中无法看出，但得益于 FilteredTextBoxExtender，你无法在电话号码文本框中输入任何字母符号。一旦你跳出文本框，模式验证就会在客户端执行，例如在本例中，从原本有效的英国电话号码中删除了一位数字。

![](img/11b373b78859e17d318fd76939a0df9d_121_0.png)

图 3.3 使用新的 PhoneNumber_Edit 字段模板的 Employee 编辑页

## 基本法律常识

### 法律的基本知识

- 法律的概念
- 法律的特征
- 法律的本质
- 法律的作用

### 宪法

- 宪法的概念与地位
- 宪法的基本原则
- 宪法规定的公民权利义务

### 刑法

- 刑法的概念与任务
- 犯罪的概念与构成
- 刑罚的种类

### 民法

- 民法的概念与调整对象
- 民事主体
- 民事权利与民事责任

### 控件模式

控件模式定义了使用字段模板的上下文。它可以是 ASP.NET `DataBoundControlMode` 枚举的成员之一：

- `ReadOnly` 模板由 `Details.aspx` 页面模板或自定义页面使用，以只读模式显示字段值。
- `Edit` 模板由 `Edit.aspx` 页面模板或自定义页面使用，以更改现有行的字段值。
- `Insert` 模板由 `Insert.aspx` 页面模板或自定义页面使用，以收集新行的字段值。

当为 Order 表的 ShippedDate 列查找 `ReadOnly` 字段模板时（该列具有 DateTime 数据类型，且在示例数据模型中没有额外的元数据属性），Dynamic Data 会找到 `DateTime.ascx` 模板。Edit 模式被认为更具体，因为它要求字段模板不仅要显示当前字段值，还要允许更改它。因此，在为 ShippedDate 列查找 Edit 字段模板时，如果存在名为 `DateTime_Edit.ascx` 的模板，Dynamic Data 会选择它。请注意，Dynamic Data 对 Edit 模板使用“_Edit”后缀，而 ReadOnly 模板没有后缀。Insert 模式甚至更具体，因为它可能需要特殊逻辑来处理尚未提交到数据库的行，如果存在名为 `DateTime_Insert.ascx` 的模板，Dynamic Data 会选择它。

### 模式回退

如果特定控件模式没有匹配的字段模板，Dynamic Data 会使用回退逻辑查找另一个用于更通用模式的模板。在正在进行的示例中，当为 ShippedDate 列查找 Insert 模板时，Dynamic Data 将首先尝试查找名为 `DateTime_Insert.ascx` 的模板。由于没有此名称的字段模板，它会从 Insert 模式回退到 Edit 模式，并最终使用名为 `DateTime_Edit.ascx` 的模板，前提是它能够同时处理 Edit 和 Insert 模式。同样，如果找不到 Edit 模式模板，Dynamic Data 会回退到只读模式。

然而，在 Dynamic Data 回退到下一个模式之前，它会执行类型回退。以 Products 表中的 `Int16` 列为例。在为该字段查找 Edit 模板时，它首先尝试使用 `System.Int16_Edit.ascx` 和 `Int16_Edit.ascx` 模板，但由于它们不存在，它回退到类型 `Int32`，检查 `System.Int32_Edit.ascx` 和 `Int32_Edit.ascx`，最终找到 `Integer_Edit.ascx`。如果 Dynamic Data 首先执行模式回退，它将跳过此模板，并改为尝试查找名为 `System.Int16.ascx` 的只读模板。

