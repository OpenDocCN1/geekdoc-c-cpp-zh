# How to configure the Select statement

Figure 13-5 shows how to configure the Select statement for a data source as you proceed through the steps of the wizard. The easiest way to do that is to choose the columns for the query from a single table or view. You can also specify a custom SQL statement or stored procedure as shown later in this chapter.

To select columns from a table, use the Name drop-down list to select the table. Then, check each of the columns you want to retrieve in the Columns list box. In this figure, I chose the Products table and selected four columns: ProductID, Name, UnitPrice, and OnHand.

As you check the columns in the list box, the wizard creates a Select statement that’s shown in the text box at the bottom of the dialog box. In this case, the Select statement indicates that the data source will retrieve the ProductID, Name, UnitPrice, and OnHand columns from the Products table.

The buttons to the right of the Columns list box let you specify additional options for selecting data. If, for example, you want to sort the data that’s retrieved, you can click on the ORDER BY button to display a dialog box that lets you select up to three sort columns. If you want to select rows that satisfy certain criteria, you can click on the WHERE button to display the dialog box that’s described in the next figure. And if you want to use an advanced feature, you can click on the Advanced button to display the dialog box that’s described in figure 13-16.

When you finish specifying the data you want the data source to retrieve, click Next. This takes you to a dialog box that includes a Test Query button. If you click this button, the wizard immediately retrieves the data that you specified. You can then look over this data to make sure the query retrieves the data you expected. If it doesn’t, you can click the Back button and adjust the query as needed.