# Using the DetailsView Control

The DetailsView control is a data-bound control that is used to display a single record from the associated data source in a tabular format, where each row of the table represents a field of the record. This control uses the DataSourceID property to support data binding; consequently, it also supports insert, update, and delete operations.

The DetailsView control exists within the System.Web.UI.WebControls namespace.

Table 6.19 lists the noteworthy properties of the DetailsView class:

| Property | Description |
|---|---|
| **Table 6.19: Noteworthy Properties of the DetailsView Class** | |
| AllowPaging | Obtains or specifies a value indicating whether the paging feature is enabled or not. |
| AlternatingRowStyle | Obtains or specifies a reference to the TableItemStyle object that allows you to set the appearance of the alternating data rows in a DetailsView control. |
| AutoGenerateInsertButton | Obtains or specifies a value indicating whether the built-in controls to insert a new record are displayed in a DetailsView control. |
| AutoGenerateRows | Obtains or specifies a value indicating whether the row fields for each field in the data source are automatically generated and displayed in a DetailsView control. |
| BackImageUrl | Obtains or specifies the Uniform Resource Locator (URL) to an image to display in the background of a DetailsView control. |
| BottomPagerRow | Obtains a DetailsViewRow object that represents the bottom pager row in a DetailsView control. |
| Caption | Obtains or specifies the text to render in a Hypertext Markup Language (HTML) caption element in a DetailsView control. This property is provided to make the control more accessible to users of assistive technology devices. |
| CaptionAlign | Obtains or specifies the horizontal or vertical position of the HTML caption element in a DetailsView control. This property is provided to make the control more accessible to users of assistive technology devices. |
| DataItem | Obtains the data item bound to the DetailsView control. |
| DataItemCount | Obtains the number of items in the underlying data source. |
| DataItemIndex | Obtains the index of the item displayed in a DetailsView control from the underlying data source. |
| DataKey | Obtains a DataKey object that represents the primary key of the displayed record. |
| DataKeyNames | Obtains or sets an array that contains the names of the key fields for the data source. |
| DefaultMode | Obtains or sets the default data-entry mode of the DetailsView control. |
| EditRowStyle | Obtains a reference to the TableItemStyle object that allows you to set the appearance of the data rows when a DetailsView control is in edit mode. |
| EmptyDataRowStyle | Obtains a reference that allows you to set the appearance of the empty data row displayed when the data source bound to a DetailsView control does not contain any records. |