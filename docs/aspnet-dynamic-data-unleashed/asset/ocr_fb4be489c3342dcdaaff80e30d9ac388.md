# Extending DynamicControl

Up until now, you had to specify the Init event handler for every instance of DynamicControl in each multimode entity template. For custom templates, especially the more complex ones, this is not only tedious and error prone, it also increases the size of template markup, making it less readable.

To make implementation of custom multimode templates even easier, the UnleashedControl (in the sample Unleashed.DynamicData project) extends the built-in DynamicControl to set its own Mode property based on the mode of the parent entity template. Instead of the following markup

```
<asp:DynamicControl runat="server" DataField="ContactName" OnInit="DynamicControl_Init"/>
```

you would simply write

```
<unl:UnleashedControl runat="server" DataField="ContactName"/>
```

and not have to worry about specifying the Init event handler. Listing 10.9 includes the complete source code of the UnleashedControl.

# LISTING 10.9 UnleashedControl Implementation

```
using System;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace Unleashed.DynamicData
{
    public class UnleashedControl : DynamicControl
    {
        protected override void OnInit(EventArgs e)
        {
            if (this.Mode == DataBoundControlMode.ReadOnly)
            {
                var entityTemplate = this.TemplateControl as EntityTemplateUserControl;
                if (entityTemplate != null)
                {
                    this.Mode = entityTemplate.Mode;
                }
            }
            base.OnInit(e);
        }
    }
}
```