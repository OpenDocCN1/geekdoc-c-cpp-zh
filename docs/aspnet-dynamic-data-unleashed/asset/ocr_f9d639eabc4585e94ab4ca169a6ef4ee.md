required to filter child entities based on the parent property value. In the following two sections, Initializing Nested Filter Control and Implementing Query Logic, you get a close look at the internals of this filter control. Based on this example, some of the more challenging aspects of advanced filter template design are discussed. However, you can also skip them and continue reading the section Using the Parent Filter Template later in the chapter.

# Initializing Nested Filter Control

The filter control needs an IQueryableDataSource object (an EntityDataSource or a LinqDataSource), a MetaTable describing the target entity, and a name of the target entity property. Listing 12.8 shows the part of ParentFilter implementation responsible for the initialization.

# LISTING 12.8 Parent Filter Template (Initialization Logic)

```
```csharp
using System;
using System.Linq;
using System.Linq.Expressions;
using System.Web.DynamicData;
using System.Web.UI.WebControls;

namespace WebApplication.DynamicData.Filters
{
public partial class ParentFilter : UnleashedFilterTemplate
{
private object dataSourceContext;

public string DisplayField { get; set; }

protected void Filter_Init(object sender, EventArgs args)
{
this.filter.DataSource = this.DataSource;
this.filter.Table = this.ForeignKeyColumn.ParentTable;
this.filter.DisplayField = this.DisplayField;
((EntityDataSource)this.DataSource).ContextCreated +=
this.DataSourceContextCreated;
((EntityDataSource)this.DataSource).Selecting += this.DataSourceSelecting;
}

private void DataSourceContextCreated(object sender,
EntityDataSourceContextCreatedEventArgs e)
{
this.dataSourceContext = e.Context;
}

private void DataSourceSelecting(object sender,
```
```