# The aspx file for the Product List application

To show you how everything you’ve learned works together, figure 13-16 presents the aspx code for the Product List application of figure 13-1. To make it easier for you to follow this code, I’ve shaded parts of the data source controls and the controls they’re bound to. Because this application relies entirely on the data binding declared in this aspx file, it doesn’t require any C# code.

The first control is the drop-down list that’s bound to the first SqlDataSource control, SqlDataSource1. Here, the AutoPostBack attribute for the drop-down list is set to True so the page is automatically posted back to the server when the user selects a category.

The second control is the first SqlDataSource control, which uses this Select statement to get the required data:

```
SELECT [CategoryID], [LongName] FROM [Categories]
    ORDER BY [LongName]
```

As a result, this data source gets the CategoryID and LongName columns for each row in the Categories table and sorts the result based on the LongName column. Then, these columns are used by the drop-down list that’s bound to this data source.

The third control is a DataList control that’s bound to the second SqlDataSource control, SqlDataSource2. The Header template for this control provides for a row of headings that are defined within a row of a table. Then, the Item template defines the table rows that display the data in the rows that are retrieved by the data source. As you can see, each column in the table contains a label whose Text attribute is bound to a column in the data source. Also notice that the columns in the Item template use the same style classes as the columns in the Header template. Although you can’t see these style classes here, they specify the widths of the columns. Because of that, the columns in the two templates are aligned. In addition, the last two columns in each template are right aligned since they contain numeric data.

The last two elements for the DataList control define the styles for alternating items and for the header. You saw the Header style earlier in this chapter. It indicates that the header text should be displayed in a white, boldface font on a black background. The AlternatingItem style indicates that every other row in the data list should be displayed on a light gray background. Since no Item style is included, the other rows will be displayed on a white background.

The fourth control, SqlDataSource2, uses this Select statement:

```
SELECT [ProductID], [Name], [UnitPrice], [OnHand]
    FROM [Products]
    WHERE ([CategoryID] = @CategoryID)
    ORDER BY [ProductID]
```

Here, the Where clause specifies that only those rows whose CategoryID column equals the value of the CategoryID parameter should be retrieved. To make this work, the ControlParameter element specifies that the value of the CategoryID parameter is obtained from the SelectedValue property of the ddlCategory control.