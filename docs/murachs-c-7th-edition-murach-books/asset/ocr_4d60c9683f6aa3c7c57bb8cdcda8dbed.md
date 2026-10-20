# How to display data
in a DataGridView control

In the topics that follow, you’ll learn the skills for displaying data in a DataGridView control and for formatting the grid. First, though, you’ll learn the basics of how the control works, including how to set its basic functionality.

# An introduction to the DataGridView control

The DataGridView control displays the data in a row and column format. To illustrate, figure 22-1 shows a DataGridView control that displays the data from the Products table of the MMABooks database. As you can see, the grid starts with a header row that identifies the columns in the table. Then, each of the remaining rows displays the data for one product. Here, the intersection of a column and row is a cell that displays the data for a single column in a single row of the table. In addition, each row starts with a header column, and the current row is identified by an arrowhead. To select a row, you can click on its header column.

The grid in this figure has also been formatted so the data is easy to read. For example, the width of each column has been set so you can view all of the data in the column for each row. The foreground and background colors and the font for the column headers have been changed. And the background color of every other row has been changed.

Although the grid in this figure only displays data, you can also use a DataGridView control to add, update, and delete data. However, most production programs are designed so this functionality isn’t provided directly from the grid. Instead, it can be provided using buttons like the ones shown in this figure. You’ll see how that works later in this chapter.

This figure also lists some of the properties and a method of the DataGridView class. You use the Rows and Columns properties to get a collection of the rows and columns in the grid, and you use the DataSource property to determine what data is displayed in the grid. To size the columns of a grid, you can use the AutoResizeColumns() method. Then, the width of each column is set so the contents of each row in that column, including the header row, fits in the column. In most cases, though, you’ll want to set the width of each column explicitly so it’s the same width each time the grid is displayed.

Before going on, you should notice the vertical scrollbar that’s displayed at the right side of the grid. This scrollbar is displayed automatically if the grid contains more rows than can be displayed at one time. Similarly, if a grid contains more columns than can be displayed at one time, a horizontal scrollbar is displayed. If that’s not what you want, you can adjust the height and width of the DataGridView control.