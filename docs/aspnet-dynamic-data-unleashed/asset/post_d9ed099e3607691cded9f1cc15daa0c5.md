
Table and Value property storing a comma-separated list of its primary key columns. This code relies on the convenience method, called PopulateListControl, provided by the FieldTemplateUserControl base class, which does all the heavy lifting required to query the referenced table, create the ListItem objects, and add them to the DropDownList.

### LISTING 3.10 ForeignKey_Edit Field Template (Code-Behind)

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

### LISTING 3.11 PhoneNumber_Edit Field Template (Markup)

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

As you can see, the PhoneNumber_Edit field template is similar to the DateTime template discussed earlier. It has a TextBox control used to enter the phone number, a FilteredTextBoxExtender, another AJAX control used to prevent users from entering symbols that would not be valid in a phone number, as well as several validator controls.

Although having a single DynamicValidator control is sufficient to enforce all validation attributes applied to the column in the data model, this control performs validation only on the server side, which requires a post-back before the error can be reported. Other ASP.NET validation controls, such as the RequiredFieldValidator, are optional, but because they also offer client-side validation logic, it’s best to include them in field templates to provide immediate feedback to the user, and improve the data entry experience.

Listing 3.12 shows the code-behind of the PhoneNumber_Edit field template.

### LISTING 3.12 PhoneNumber_Edit Field Template (Code-Behind)

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

Most of the phone number validation in the new field template is performed by the standard ASP.NET control, RegularExpressionValidator, which ensures that the value entered by the user matches the regular expression pattern that defines a valid phone number. In addition to the server-side validation based on the .NET implementation of regular expressions in the System.Text.RegularExpressions namespace, it also works on the client side taking advantage of the regular expression functionality in JavaScript.

```csharp
public object HomePhone;
}
}
```

DataTypeAttribute, applied to the HomePhone column, specifies this string column's actual data type is PhoneNumber. Dynamic Data uses this information as a hint when looking for a matching field template for this column and chooses the new PhoneNumber_Edit template instead of the default Text_Edit. In this example, RegularExpressionAttribute is also applied to the HomePhone column to provide a pattern that matches not only U.S. phone numbers, which have three-digit area codes, but also UK numbers, which might have two-digit area codes.

Figure 3.3 shows the Employee Edit page after the implementation of the PhoneNumber_Edit field template has been completed. Although you cannot tell from this screenshot, thanks to the FilteredTextBoxExtender, you cannot type any alphabetical symbols in the phone number text box. The pattern validation is performed on the client side as soon as you tab out of the text box, such as in this case, where one digit was removed from an otherwise valid UK phone number.

![](img/11b373b78859e17d318fd76939a0df9d_121_0.png)

FIGURE 3.3 Employee Edit page with the New PhoneNumber_Edit field template.

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

### Control Mode

Control mode defines the context where the field template will be used. It can be one of the members of the ASP.NET `DataBoundControlMode` enumeration:

- `ReadOnly` templates are used by the `Details.aspx` page template or custom pages to display field values in Read-only mode.
- `Edit` templates are used by the `Edit.aspx` page template or custom pages to change field values of an existing row.
- `Insert` templates are used by the `Insert.aspx` page template or custom pages to collect field values for a new row.

When looking for a `ReadOnly` field template for the ShippedDate column of the Order table, which has DateTime data type and no additional metadata attributes in the sample data model, Dynamic Data finds the `DateTime.ascx` template. Edit mode is considered more specific because it requires the field template to not only display the current field value, but also allow changing it. Therefore, when looking for an Edit field template for the ShippedDate column, Dynamic Data chooses the template called `DateTime_Edit.ascx` if it exists. Note that Dynamic Data uses the "_Edit" suffix for Edit templates and no suffix for the ReadOnly templates. The Insert mode is even more specific because it might require special logic to deal with rows that have not been submitted to the database, and Dynamic Data chooses the template called `DateTime_Insert.ascx` if it exists.

### Mode Fallback

If there is no matching field template for a particular control mode, Dynamic Data uses fallback logic to find another template for a more generic mode. In this ongoing example, when looking for an Insert template for the ShippedDate column, Dynamic Data will first try to find the template called `DateTime_Insert.ascx`. Because there is no field template with this name, it falls back from the Insert to the Edit mode and ends up using the template called `DateTime_Edit.ascx`, assuming it can handle both Edit and Insert modes. Similarly, if an Edit mode template cannot be found, Dynamic Data falls back to Read-only mode.

However, before Dynamic Data falls back to the next mode, it performs the type fallback. Consider `Int16` column from the Products table. When looking for an Edit template for this field, it tries using `System.Int16_Edit.ascx` and `Int16_Edit.ascx` templates first, but because they do not exist, it falls back to type `Int32` and checks for `System.Int32_Edit.ascx` and `Int32_Edit.ascx` and eventually finds `Integer_Edit.ascx`. If Dynamic Data performed the mode fallback first, it would skip this template and try to look for a ReadOnly template called `System.Int16.ascx` instead.
