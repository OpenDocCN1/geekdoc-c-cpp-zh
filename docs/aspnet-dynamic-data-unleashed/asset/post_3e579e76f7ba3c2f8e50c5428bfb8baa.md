
## Accessing Initial Field Values of Other Columns

The next and biggest challenge is to figure out how to get the current value of the Country property inside of the Region_Edit field template. The most reliable way to do this is by getting it from the actual field template instantiated for the Country property.

> **NOTE**
> 
> At first thought, the Row property of the FieldTemplateUserControl (the base class of the custom field template) looks as if it could be used to access other property values. Logically one would expect this property to return the entity instance, which is being edited by the field template. This is indeed the case with LINQ to SQL. Entity Framework, or more specifically the EntityDataSource control, wraps the actual entity instance inside of an EntityDataSourceWrapper object. The code example that follows shows how to implement a strongly-typed property that returns the Customer instance inside of the custom field template:

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

This code works with both LINQ to SQL and Entity Framework, but unfortunately, there are still two problems with this approach. The Row property of the FieldTemplateUserControl class is only available during the data binding stage of the ASP.NET page lifecycle. During post-backs, which is when you would want to check for a modified Country property value, accessing this property throws an InvalidOperationException. Moreover, this property returns null when the field template is instantiated in Insert mode, making it impossible to determine the default value of the Country property.

The FieldTemplateUserControl base class provides a method called FindOtherFieldTemplate that takes the name of the entity property as a parameter and returns the field template that was instantiated for it. The earliest stage in the field template's lifecycle when it can call this method is the Load. Although it is technically possible to call it during the Init stage, the result would depend on the order in which the field templates are created, and the method returns null if the other field template has not been created yet. This example shows how this can be implemented by overriding the OnLoad of the field template:

```csharp
private FieldTemplateUserControl countryFieldTemplate;
protected override void OnLoad(EventArgs e)
{
    base.OnLoad(e);
    this.countryFieldTemplate = this.FindOtherFieldTemplate("Country");
}
```

Having located the field template instance of the Country property, you can use it to access the property value and store the country name in the ContextKey of the AutoCompleteExtender, which will pass it to the GetCompletionList of the RegionCompletionService. This needs to be done during the Data Binding stage of the field template lifecycle when the Customer entity instance has already been retrieved from the database during the Load stage. The next code example shows how this can be implemented in the overridden OnDataBinding method:

```csharp
protected override void OnDataBinding(EventArgs e)
{
    base.OnDataBinding(e);
    string country = this.countryFieldTemplate.FieldValueEditString;
    this.autoCompleteExtender.ContextKey = country;
}
```

## Accessing Modified Field Values of Other Columns

At this point, the Region field template can display the list of regions appropriate for the current country when the web page is first rendered for an existing Customer entity instance. However, when the field template is used in Insert mode and the customer entity does not exist, the country name has not been entered yet, and the list of regions will be empty. The list will also not be updated when user changes the Country value from its initial value. So the last challenge is to figure out how to reload the list of regions as the Country property value changes.

Just like in a traditional ASP.NET application, you can use post-backs and event handlers to implement code that reacts to user input. The custom Region field template needs to respond to the change made by the user in the Country field template, which requires accessing the TextBox control it instantiates. The next example shows an extract from the Region_Edit field template that accomplishes this task:

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

The overridden OnLoad method retrieves the TextBox control created by the countryFieldTemplate through its DataControl property. It then assigns the CountryTextBox_TextChanged method as an event handler to its TextChanged event. This event handler is where you can access the current Country value from the text box and store it in the ContextKey of the AutoCompleteExtender. Note that by default, changing a value in a TextBox control does not trigger a post-back. For the list of regions to be updated immediately, as the user modifies the Country field value, the OnLoad method explicitly sets the AutoPostBack property of the country TextBox control to true. This triggers a post-back when the user tabs out or clicks away from the text box after changing the Country value.

## Initial Implementation of the Region_Edit Field Template

Figure 10.5 shows a web page generated after the Customer entity template was modified to use the Region field template.

![](img/11b373b78859e17d318fd76939a0df9d_350_0.png)

FIGURE 10.5 Web page with custom Region field template.

The complete code-behind file of the Region_Edit field template is shown in Listing 10.15.

### LISTING 10.15 Initial Implementation of the Region_Edit Field Template (Code-Behind)

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

## Improving Encapsulation of Field Templates

Although the current implementation of the Region field template satisfies your immediate requirements, it also suffers from a serious problem. By accessing the DataControl of the Country field template directly and casting it down to the TextBox type, the Region field template assumes that the Country field template will always use a TextBox as its data control. Although this assumption is correct today, it easily breaks as soon as you decide to change what is really an internal implementation of how the Country property is presented on the web page. You could decide to create a custom field template with a DropDownList so that users can pick a country instead of typing its name. You could also decide to change the Text_Edit field template to use a third-party control instead of the built-in TextBox. Any number of changes like this breaks the Region_Edit field template.

As the number of dynamic and custom field templates increases, improving encapsulation helps to keep their maintenance simple. The need to access the current field value and detect its changes is a common problem. You can solve it by introducing an extended base class for field templates that provides a common way to access this information without having to take a dependency on the specific implementation details of a particular template. In the sample solution accompanying this book, this new base class is called UnleashedFieldTemplate; you can see its complete source code in Listing 10.16.

### LISTING 10.16 UnleashedFieldTemplate Base Class

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
