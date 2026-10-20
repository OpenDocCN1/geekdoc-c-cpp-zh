
## A DataGridView control that displays a list of products

![](img/844f608d10a44654833ea5efc8a2e7a7_751_0.png)

### Common properties of the DataGridView class

| Property | Description |
| --- | --- |
| Rows | A collection that contains all the rows in the control. |
| Columns | A collection that contains all the columns in the control. |
| DataSource | The data source for the control. |

### Common method of the DataGridView class

| Method | Description |
| --- | --- |
| AutoResizeColumns() | Causes the widths of all columns to be adjusted to fit the contents of their cells, including the header cells. |

### Description

- You can use a *DataGridView control* to display data in a row and column format. The intersection of a row and column is called a *cell*.
- You can also use a DataGridView control to add, update, and delete data.
- If the data source for a DataGridView control contains more rows and columns than can be displayed at one time, scrollbars are displayed.
- You use the Rows and Columns properties to access the collections of rows and columns in a DataGridView control. Then, you can use an index to access a specific column or row.
- The DataSource property determines what data is displayed in the grid. See figure 22-3 for more information on setting this property.
- Instead of using the AutoResizeColumns() method, you can set the width of each column explicitly so it’s the same size each time it’s displayed. See figure 22-4 for more information.

## How to set the functions provided by a DataGridView control

Figure 22-2 shows how to set the main functions that will be provided by a DataGridView control. The easiest way to do that is to use the smart tag menu that’s displayed when you add this control to a form. By default, the adding, editing, and deleting functions of the control are enabled. However, you can disable an option by removing its checkmark from the appropriate box. You can also control whether the user can reorder the columns in the grid.

You can also change the functionality of a grid by writing code that sets the properties listed in this figure. For example, if you don’t want users to be able to use the grid to add rows, you can set the AllowUserToAddRows property to false. Similarly, if you don’t want users to be able to use the grid to delete rows, you can set the AllowUserToDeleteRows property to false. However, to determine whether users can use the grid to edit data, you use the ReadOnly property. For example, if you don’t want users to be able to use the grid to edit its data, you set the ReadOnly property to true.

Note that the smart tag menu contains other options for working with a DataGridView control. For example, it lets you choose the data source for the control, and it lets you edit and add columns. However, you can’t use these options when you use code to specify the data source for the grid like you do when you use Entity Framework and ADO.NET as shown in this book. Instead, you have to perform these functions in code.

### A DataGridView control after it’s added to a form

![](img/844f608d10a44654833ea5efc8a2e7a7_753_0.png)

### Properties that you can set from the smart tag menu

| Property | Description |
| --- | --- |
| AllowUserToAddRows | If set to true, users can add rows directly to the grid. Otherwise, they can’t. The default is true. |
| AllowUserToDeleteRows | If set to true, users can delete rows directly from the grid. Otherwise, they can’t. The default is true. |
| AllowUserToOrderColumns | If set to true, users can manually reposition columns. Otherwise, they can’t. The default is false. |
| ReadOnly | If set to true, users can’t edit data directly in the grid. Otherwise, they can. The default is false. |

### Description

- When you first add a DataGridView control to a form, its smart tag menu is displayed. You can use the options in this menu to determine if users can add, edit, and delete data directly in the control and if they can reorder columns.
- You can also determine the functions provided by the DataGridView control by using code to set the properties shown above.
- When you set the data source for a DataGridView control in code as shown in this chapter, you can’t choose the data source from the smart tag menu. In addition, you can’t edit or add columns using the commands available from this menu.

Figure 22-2    How to set the functions provided by a DataGridView control

## How to bind to a data source

To display data in a DataGridView control, you have to bind it to a data source such as a list that implements the IList interface. If you haven’t read chapter 15, you should know that an interface consists of a set of declarations for one or more properties, methods, and events. However, it doesn’t include the implementation for those properties, methods, and events. Instead, another class provides the code that implements that interface. For example, the List class implements the IList interface. As a result, a List object can be the data source for a DataGridView control.

Figure 22-3 shows three ways to bind a DataGridView control to a data source. In the first example, the control is bound to an entity collection created by EF. Here, the code uses the ToList() method to convert the collection to a list so it implements the IList interface.

When you bind a DataGridView control to an entity collection, each property of that entity is displayed in a column by default. That includes columns that define relationships with other entities. If that’s not what you want, you can remove those columns from the grid as shown later in this chapter. Another option, though, is to use a LINQ query to retrieve just the columns you need as shown in the second example.

If you’re using ADO.NET instead of EF, you can call a method that gets a collection of objects. Then, you can bind the DataGridView control to that collection as shown by the third example. Here, the code calls a method named GetProducts() that returns a List<Product> object. Then, it binds the grid to this list.

The DataGridView control at the top of this figure shows the default formatting that’s applied when you bind the control. To improve the appearance of the control, you can format it as shown in the next two figures.

### A DataGridView control that’s bound to a data source

![](img/844f608d10a44654833ea5efc8a2e7a7_755_0.png)

### How to bind a DataGridView control to an entity collection

```csharp
MMABooksContext context = new MMABooksContext();
dgvProducts.DataSource = context.Products.ToList();
```

### How to bind a DataGridView control to the results of a query

```csharp
MMABooksContext context = new MMABooksContext();
var products = context.Products.OrderBy(p => p.Description)
    .Select(p => new { p.ProductCode, p.Description, p.UnitPrice, p.OnHandQuantity }).ToList();
dgvProducts.DataSource = products;
```

### How to bind a DataGridView control to a list of objects created in code

```csharp
List<Product> products = GetProducts();
dgvProducts.DataSource = products;
```

### Description

- A DataGridView control can be bound to any class that implements the IList interface, including an array.
- To bind a DataGridView control, you set its DataSource property. Then, the data in the data source is displayed in the grid.
- When you bind the DataGridView to a list of objects, each property of that object becomes a column in the grid.
- If you’re using EF and you bind a DataGridView control to an entity collection whose entities contain one or more properties for related entities, a column will be included for each relationship. If that’s not what you want, you can use a LINQ query to get just the properties you want to include in the data source. Or, you can remove the relationship columns from the grid as shown later in this chapter.
- If you’re using ADO.NET code, you can call a method that gets a collection of objects and then bind the DataGridView control to that collection.
