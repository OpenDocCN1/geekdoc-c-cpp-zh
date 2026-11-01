# LISTING 10.5 Continued

```
OnInit="DynamicControl_Init" />
</td>
</tr>
</ItemTemplate>
</asp:EntityTemplate>
</table>
```

Notice how this new version is nearly identical to the previous one shown in Listing 10.4. The hardcoded Mode property was removed from the DynamicControl, but the DynamicControl_Init event handler was already in place because the dynamic entity templates already need to initialize another property of the DynamicControl instances programmatically, the DataField property.

Listing 10.6 shows the code-behind of the dynamic multimode entity template. Bold font indicates the only significant difference between this new implementation and the code-behind of the original Default_Edit and Default_Insert entity templates.

# LISTING 10.6 Multimode Dynamic Entity Template (Code-Behind)

```
using System;
using System.Collections.Generic;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.EntityTemplates
{
    public partial class DefaultEntityTemplate : EntityTemplateUserControl
    {
        private MetaColumn currentColumn;

        protected override void OnLoad(EventArgs e)
        {
            IEnumerable<MetaColumn> scaffoldColumns = this.Table.GetScaffoldColumns(
                this.Mode, this.ContainerType);
            foreach (MetaColumn column in scaffoldColumns)
            {
                this.currentColumn = column;
                NamingContainer container = new NamingContainer();
                this.entityTemplate.ItemTemplate.InstantiateIn(container);
                this.entityTemplate.Controls.Add(container);
            }
        }

        protected void Label_Init(object sender, EventArgs e)
        {
```