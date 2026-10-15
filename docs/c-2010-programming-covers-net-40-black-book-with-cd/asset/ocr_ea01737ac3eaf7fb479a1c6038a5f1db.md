```
System.Web.UI.WebControls.BaseDataBoundControl
System.Web.UI.WebControls.DataBoundControl
System.Web.UI.DataVisualization.Charting.Chart
```

Noteworthy properties of the Chart class are listed in Table 26.25:

# Table 26.25: Noteworthy Properties of the Chart Class

| Property | Description |
|---|---|
| AlternateText | Displays the alternate text when the chart image is not shown |
| AccessKey | Stores the Keyboard shortcut(Inherited from the control) |
| BackImage | Gets or sets the background image path |
| BackImageAlignment | Gets or sets the alignment of the background image |
| ClientIDMode | Generates ClientID property for the control(Inherited from the control) |
| Compression | Stores the compression value |
| DataSourceID | Stores the ID of the data source control |
| ViewStateContent | Saves the chart content in the ViewState |
| ViewStateMode | Determines whether the view state is enabled for the chart control or not(Inherited from the control) |
| Visible | Decides whether the control should be visible or not |

Noteworthy methods of the Chart class are listed in Table 26.26:

# Table 26.26: Noteworthy Methods of the Chart Class

| Method | Description |
|---|---|
| CopyBaseAttributes() | Allows you to copy only those properties that are not encapsulated by the Style object from the defined Web server control to the Web server control that called this method. |
| MergeStyle() | Allows you to copy non-blank elements of the defined style to the Web control and does not overwrite any existing elements of the control. |
| Paint() | Allows you to draw the chart image in graphics. |
| RenderBeginTag() | Writes the opening tag of the specified markup element to the output stream. |
| RenderEndTag() | Writes the end tag of a markup element to the output stream (Inherited from the control). |

Noteworthy events of the Chart class are listed in Table 26.27:

# Table 26.27: Noteworthy Events of the Chart Class

| Event | Description |
|---|---|
| Click | Invokes when the control is clicked |
| Customize | Invokes before the chart image is drawn |
| DataBound | Invokes when the control is DataBound(Inherited from the control) |
| Disposed | Invokes when the control is disposed |
| PostPaint | Invokes when the chart element is painted |

# The QueryExtender Control

The QueryExtender control is a data source control that helps in retrieving only those records from the database which meet the specific criteria or in other words,to filter the records.Filtering of records helps in displaying the