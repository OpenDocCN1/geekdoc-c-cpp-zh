

## 访问其他列的初始字段值

下一个也是最大的挑战是弄清楚如何在 Region_Edit 字段模板内获取 Country 属性的当前值。最可靠的方法是从为 Country 属性实例化的实际字段模板中获取它。

> **注意**
> 
> 乍一看，FieldTemplateUserControl 的 Row 属性（自定义字段模板的基类）似乎可以用来访问其他属性值。逻辑上，人们会期望该属性返回正在被字段模板编辑的实体实例。这在使用 LINQ to SQL 时确实是如此。Entity Framework，或者更具体地说是 EntityDataSource 控件，会将实际的实体实例包装在 EntityDataSourceWrapper 对象中。下面的代码示例演示了如何在自定义字段模板中实现一个强类型属性，该属性返回 Customer 实例：

```csharp
private Customer Customer
{
    get
    {
        Customer customer = this.Row as Customer;
        if (customer == null)
        {
            var typeDescriptor = (ICustomTypeDescriptor)this.Row;
            if (typeDescriptor != null)
                customer = (Customer)typeDescriptor.GetPropertyOwner(null);
        }
        return customer;
    }
}
```

这段代码同时适用于 LINQ to SQL 和 Entity Framework，但不幸的是，这种方法仍然存在两个问题。FieldTemplateUserControl 类的 Row 属性仅在 ASP.NET 页面生命周期的数据绑定阶段可用。在回发期间（正是你想要检查 Country 属性值是否被修改的时候），访问此属性会抛出 InvalidOperationException。此外，当字段模板在插入模式下实例化时，此属性返回 null，因此无法确定 Country 属性的默认值。

FieldTemplateUserControl 基类提供了一个名为 FindOtherFieldTemplate 的方法，该方法以实体属性的名称作为参数，并返回为该属性实例化的字段模板。在字段模板的生命周期中，可以调用此方法的最早阶段是 Load 阶段。虽然从技术上讲可以在 Init 阶段调用它，但结果将取决于字段模板的创建顺序，并且如果其他字段模板尚未创建，该方法将返回 null。此示例演示了如何通过重写字段模板的 OnLoad 来实现这一点：

```csharp
private FieldTemplateUserControl countryFieldTemplate;
protected override void OnLoad(EventArgs e)
{
    base.OnLoad(e);
    this.countryFieldTemplate = this.FindOtherFieldTemplate("Country");
}
```

找到 Country 属性的字段模板实例后，可以使用它来访问属性值，并将国家名称存储在 AutoCompleteExtender 的 ContextKey 中，该键会将其传递给 RegionCompletionService 的 GetCompletionList。这需要在字段模板生命周期的数据绑定阶段完成，此时 Customer 实体实例已在 Load 阶段从数据库中检索到。下一个代码示例演示了如何在重写的 OnDataBinding 方法中实现这一点：

```csharp
protected override void OnDataBinding(EventArgs e)
{
    base.OnDataBinding(e);
    string country = this.countryFieldTemplate.FieldValueEditString;
    this.autoCompleteExtender.ContextKey = country;
}
```

## 访问其他列修改后的字段值

此时，当网页首次为现有的 Customer 实体实例呈现时，Region 字段模板可以显示与当前国家/地区相匹配的区域列表。但是，当字段模板在插入模式下使用且客户实体不存在时，国家名称尚未输入，区域列表将为空。当用户将 Country 值从其初始值更改时，该列表也不会更新。因此，最后一个挑战是弄清楚如何在 Country 属性值更改时重新加载区域列表。

就像在传统的 ASP.NET 应用程序中一样，您可以使用回发和事件处理程序来实现响应用户输入的代码。自定义 Region 字段模板需要响应用户在 Country 字段模板中所做的更改，这需要访问 Country 字段模板所实例化的 TextBox 控件。下一个示例显示了完成此任务的 Region_Edit 字段模板的摘录：

```csharp
protected override void OnLoad(EventArgs e)
{
    base.OnLoad(e);
    var countryFieldTemplate = this.FindOtherFieldTemplate("Country");
    var countryTextBox = (TextBox)countryFieldTemplate.DataControl;
    countryTextBox.AutoPostBack = true;
    countryTextBox.TextChanged += CountryTextBox_TextChanged;
}

private void CountryTextBox_TextChanged(object sender, EventArgs e)
{
    var countryTextBox = (TextBox)sender;
    this.autoCompleteExtender.ContextKey = countryTextBox.Text;
}
```

重写的 OnLoad 方法通过 countryFieldTemplate 的 DataControl 属性检索该字段模板创建的 TextBox 控件。然后，它将 CountryTextBox_TextChanged 方法指定为其 TextChanged 事件的事件处理程序。在此事件处理程序中，您可以访问文本框中的当前 Country 值，并将其存储在 AutoCompleteExtender 的 ContextKey 中。请注意，默认情况下，更改 TextBox 控件中的值不会触发回发。为了在用户修改 Country 字段值时立即更新区域列表，OnLoad 方法显式将 country TextBox 控件的 AutoPostBack 属性设置为 true。这样，当用户更改 Country 值后切换焦点或单击离开文本框时，就会触发回发。

## Region_Edit 字段模板的初始实现

图 10.5 显示了在将 Customer 实体模板修改为使用 Region 字段模板后生成的网页。

![](img/11b373b78859e17d318fd76939a0df9d_350_0.png)

图 10.5 使用自定义 Region 字段模板的网页。

Region_Edit 字段模板的完整代码隐藏文件如清单 10.15 所示。

### 清单 10.15 Region_Edit 字段模板的初始实现（代码隐藏）

```csharp
using System;
using System.Collections.Specialized;
using System.Web.DynamicData;
using System.Web.UI;

namespace WebApplication.DynamicData.FieldTemplates
{
    public partial class RegionEditField : FieldTemplateUserControl
    {
        private FieldTemplateUserControl countryFieldTemplate;

        public override Control DataControl
        {
            get { return this.textBox; }
        }

        protected override void OnInit(EventArgs e)
        {
            base.OnInit(e);
            this.textBox.ToolTip = this.Column.Description;
            this.SetupValidator(this.requiredFieldValidator);
            this.SetupValidator(this.dynamicValidator);
        }

        protected override void OnLoad(EventArgs e)
        {
            base.OnLoad(e);
            this.countryFieldTemplate = this.FindOtherFieldTemplate("Country");
            var countryTextBox = (TextBox)this.countryFieldTemplate.DataControl;
            countryTextBox.AutoPostBack = true;
            countryTextBox.TextChanged += CountryTextBox_TextChanged;
        }

        protected override void OnDataBinding(EventArgs e)
        {
            base.OnDataBinding(e);
            string country = this.countryFieldTemplate.FieldValueEditString;
            this.autoCompleteExtender.ContextKey = country;
        }

        protected override void ExtractValues(IOrderedDictionary dictionary)
        {
            dictionary[this.Column.Name] = this.ConvertEditedValue(this.textBox.Text);
        }

        private void CountryTextBox_TextChanged(object sender, EventArgs args)
        {
            var countryTextBox = (TextBox)sender;
            this.autoCompleteExtender.ContextKey = countryTextBox.Text;
        }
    }
}
```

## 改进字段模板的封装

虽然 Region 字段模板的当前实现满足了您的直接需求，但它也存在一个严重的问题。通过直接访问 Country 字段模板的 DataControl 并将其转换为 TextBox 类型，Region 字段模板假设 Country 字段模板将始终使用 TextBox 作为其数据控件。虽然这一假设目前是正确的，但一旦您决定更改 Country 属性在网页上呈现的实际内部实现，它很容易被破坏。您可能决定创建一个使用 DropDownList 的自定义字段模板，以便用户可以选择国家而不是输入国家名称。您也可能决定更改 Text_Edit 字段模板，使用第三方控件而不是内置的 TextBox。任何这样的更改都会破坏 Region_Edit 字段模板。

随着动态和自定义字段模板数量的增加，改进封装有助于保持其维护的简单性。访问当前字段值并检测其变化的需求是一个常见问题。您可以通过为字段模板引入一个扩展基类来解决此问题，该基类提供了一种通用的方式来访问此信息，而无需依赖于特定模板的具体实现细节。在本书随附的示例解决方案中，这个新基类名为 UnleashedFieldTemplate；您可以在清单 10.16 中查看其完整源代码。

### 清单 10.16 UnleashedFieldTemplate 基类

```csharp
using System;
using System.Collections.Specialized;
using System.ComponentModel;
using System.Web.DynamicData;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace Unleashed.DynamicData
{
    public class UnleashedFieldTemplate : FieldTemplateUserControl
    {
        private static readonly object FieldValueChangedEvent = new object();

        public virtual bool AutoPostBack { get; set; }

        public override object FieldValue
        {
            get { return base.FieldValue; }
            set
            {
                if (base.FieldValue != value)
                {
                    base.FieldValue = value;
                    this.OnFieldValueChanged(EventArgs.Empty);
                }
            }
        }
```

