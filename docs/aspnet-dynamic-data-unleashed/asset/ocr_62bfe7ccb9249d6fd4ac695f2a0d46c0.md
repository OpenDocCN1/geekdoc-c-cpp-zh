```
countryTextBox.TextChanged += CountryTextBox_TextChanged;
}

private void CountryTextBox_TextChanged(object sender, EventArgs e)
{
    var countryTextBox = (TextBox)sender;
    this.autoCompleteExtender.ContextKey = countryTextBox.Text;
}
```

The overridden OnLoad method retrieves the TextBox control created by the countryFieldTemplate through its DataControl1 property. It then assigns the CountryTextBox_TextChanged method as an event handler to its TextChanged event. This event handler is where you can access the current Country value from the text box and store it in the ContextKey of the AutoCompleteExtender. Note that by default, changing a value in a TextBox control does not trigger a post-back. For the list of regions to be updated immediately, as the user modifies the Country field value, the OnLoad method explicitly sets the AutoPostBack property of the country TextBox control to true. This triggers a post-back when the user tabs out or clicks away from the text box after changing the Country value.

# Initial Implementation of the Region_Edit Field Template

Figure 10.5 shows a web page generated after the Customer entity template was modified to use the Region field template.

![](bbox=[0.12, 0.72, 0.62, 0.86])

FIGURE 10.5 Web page with custom Region field template.

The complete code-behind file of the Region_Edit field template is shown in Listing 10.15.

# LISTING 10.15 Initial Implementation of the Region_Edit Field Template (Code-Behind)

```
using System;
using System.Collections.Specialized;
using System.Web.DynamicData;
using System.Web.UI;

namespace WebApplication.DynamicData.FieldTemplates
{
```