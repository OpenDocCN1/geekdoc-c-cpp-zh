# NOTE

This is where name of the EntityTemplate control becomes confusing because it collides with the concept of entity templates represented by the EntityTemplateUserControl base class. The EntityTemplate control defines a markup template used to create a DynamicControl and a Label for a single entity property, whereas the EntityTemplateUserControl defines markup for all properties of the entire entity class. Perhaps ColumnTemplate would have been a better name for the EntityTemplate control.

# LISTING 11.14 TwoColumn Entity Template (Code-Behind)

```
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace WebApplication
{
    public partial class TwoColumnEntityTemplate : EntityTemplateUserControl
    {
        private MetaColumn currentColumn;

        protected override void OnLoad(EventArgs e)
        {
            IEnumerable<MetaColumn> scaffoldColumns =
                this.Table.GetScaffoldColumns(this.Meta, this.ContainerType);
            foreach (MetaColumn column in scaffoldColumns)
            {
                this.currentColumn = column;
                var container = new NamingContainer();
                this.entityTemplate.ItemTemplate.InstantiateIn(container);
                PlaceHolder placeHolder = this.FindGroupPlaceHolder(column);
                placeHolder.Controls.Add(container);
            }
        }

        protected void Label_Init(object sender, EventArgs e)
        {
            ((UnleashedLabel)sender).DataField = this.currentColumn.Name;
        }
    }
```