

## Exercise 13-1 Create an Invoice Line Item List application

在本练习中，你将创建一个按发票列出明细项目的应用程序。为此，你将使用两个 SqlDataSource 控件和两个绑定控件。完成后，应用程序应如下所示：

![](img/c024ccf88e28c30c07dd410d4342288f_460_0.png)

## Create a drop-down list and the data source it’s bound to

- 1. Open the Ch13InvoiceLineItems application in the C:\aspnet4_cs directory. This application contains the starting page and the image and style sheet used by the page.
- 2. Enter the text shown above into the main division of the page, followed by a space. Add a drop-down list following the text. When the smart tag menu is displayed, select the Choose Data Source command and then select New Data Source from the first drop-down list in the Data Source Configuration Wizard dialog box that’s displayed.
- 3. Continue configuring the data source as shown in figures 13-2 through 13-6. The data source should include the InvoiceNumber column from the Invoices table for all invoices whose Total column is greater than 300. To create the Where clause for the Select statement, select None from the Source drop-down list.
- 4. When the Data Source Configuration Wizard is displayed again, accept the defaults so the InvoiceNumber column is displayed in the drop-down list and stored as the value of the drop-down list.
- 5. Change the name of the drop-down list to ddlInvoice and set its AutoPostBack property to True. Then, review the aspx code that was generated. In particular, review the Select statement and the select parameter that were generated for the SqlDataSource control.

## Create another data source and bind it to a data list

- 6. Add a second SqlDataSource control to the page. Configure this data source so it uses the connection string that’s stored in the web.config file, so it selects the ProductID, UnitPrice, Quantity, and Extension columns from the LineItems table, and so it selects only the line items for the invoice that’s selected from the drop-down list.
- 7. Add a DataList control to the form, and set its data source to the SqlDataSource control you just created.
- 8. Run the application to see how the data is displayed by default. Then, close the browser window.

## Modify the templates for the data list

- 9. Display the smart tag menu for the DataList control, and select the Edit Templates command to display the Item template.
- 10. Delete the literal text for each column. Then, add a table at the bottom of the template that consists of one row and four columns and that has a width of 400 pixels.
- 11. Set the width of each column to 100 pixels, and right-align the second, third, and fourth columns. (You can do that by creating styles that use the width and text-align properties or by setting the Width and Align properties of the table cells.)
- 12. Move the labels for the four columns into the four cells of the table, and then delete the space above the table.
- 13. Select the label for the UnitPrice column, display its smart tag menu, and select Edit DataBindings. Then, use the DataBindings dialog box to apply the Currency format to that column. Do the same for the Extension column.
- 14. Use the drop-down list in the smart tag menu for the data list to display the header template for the control.
- 15. Add a table like the one you used for the Item template, but enter the values shown in the heading above. When you’re done, exit from template-editing mode.

## Format the data list

- 16. Display the smart tag menu for the data list, select the Auto Format command, and highlight one or more of the predefined schemes to see how they look.
- 17. Apply the Simple scheme. Then, review the aspx code for the DataList control to see the style properties and elements that were generated.
- 18. Run the application to make sure it’s formatted properly. Select a different invoice from the drop-down list to make sure this works. Then, close the browser window.

## How to use
the GridView control

在本章中，你将学习如何使用 GridView 控件。此控件可让你以表格的行和列形式显示数据源的数据。它包含许多高级功能，例如自动分页和排序。它可让你使用最少的 C# 代码更新和删除数据。其外观完全可定制。

- **How to customize the GridView control** ................................ 444
- How the GridView control works ...................................................... 444
- How to define the fields in a GridView control .................................... 446
- Elements used to create and format fields .......................................... 448
- How to enable sorting .................................................................... 450
- How to enable paging ...................................................................... 452
- How to customize paging .................................................................. 454

- **A list application that uses a GridView control** .................... 456
- The Product List application .............................................................. 456
- The aspx file ................................................................................... 458

- **How to update GridView data** ................................................ 460
- How to work with command fields ....................................................... 460
- How to use events raised by the GridView control ................................. 462
- How to insert a row in a GridView control ............................................ 464

- **A maintenance application
that uses a GridView control** .................................................. 466
- The Category Maintenance application ............................................... 466
- The aspx file ................................................................................... 468
- The code-behind file ......................................................................... 472

- **How to work with template fields** ........................................... 474
- How to create template fields ............................................................ 474
- The template version of the Category Maintenance application .............. 476
- The aspx code for the template version ............................................... 476

- **Perspective** ............................................................................... 480

## How to customize the GridView control

GridView 控件是 ASP.NET 4 中最强大的用户界面控件之一。它提供了许多选项，可让你自定义其外观和行为。在以下主题中，你将学习如何定义字段、自定义这些字段的内容和外观、启用排序以及提供自定义分页。

## How the GridView control works

如图 14-1 所示，GridView 控件以行列格式显示数据源提供的数据。事实上，GridView 控件将其数据渲染为 HTML 表格，其中数据源中的每一行对应一个 Tr 元素，数据源中的每一列对应一个 Td 元素。

图上方显示的 GridView 控件显示的是万圣节数据库的 Categories 表中的数据。这里，控件的前三列显示的是该表的三列数据。

该控件的另外两列显示用户可以单击以编辑或删除行的按钮。在此示例中，用户已单击 masks 行的 Edit 按钮，将该行置于编辑模式。在此模式下，短名称和长名称列的标签被文本框取代，Edit 按钮被 Update 和 Cancel 按钮取代，Delete 按钮被移除。

本图中的表格列出了 GridView 控件的一些基本属性，本图中的 aspx 代码即为创建上方 GridView 控件的代码。默认情况下，此控件包含数据源中每一列的一个列。这些列由 BoundField 元素定义，该元素在 Columns 元素内编码。例如，本图中的 GridView 控件包含一个包含三个 BoundField 元素的 Columns 元素。请注意，三个 BoundField 元素都包含定义列宽度的 ItemStyle 元素。Columns 元素还包含两个定义按钮列的 CommandField 元素。

GridView 控件的大部分 aspx 代码都是由 Visual Studio 在你将控件从工具箱拖到表单上以及使用配置向导配置数据源时自动创建的。但是，你通常会修改此代码以自定义此控件的外观和行为。

