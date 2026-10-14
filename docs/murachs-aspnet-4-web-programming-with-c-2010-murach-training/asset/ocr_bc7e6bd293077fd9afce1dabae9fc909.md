# A list application that uses a GridView control

Now that you’ve learned the basics of working with a GridView control, the following topics present the design and code for an application that uses a GridView control to list the rows of a data source. As you’ll see, this application provides for sorting and paging and doesn’t require a single line of C# code.

# The Product List application

Figure 14-7 presents the Product List application. Here, the data from the Products table of the Halloweene database is displayed in a GridView control. The data is displayed 8 rows at a time, and numeric page buttons are displayed at the bottom of the GridView control so the user can navigate from page to page. In addition, the user can sort the data by clicking the column headings for the ID, Name, and Category columns.