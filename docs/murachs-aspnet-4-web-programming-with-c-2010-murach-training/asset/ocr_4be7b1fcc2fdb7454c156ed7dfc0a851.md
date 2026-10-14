# The aspx file

Figure 17-5 shows the main division of the Default.aspx page for the Product List application. If you compare this listing with the listing shown in figure 13-16, you’ll discover that the only difference is that the SqlDataSource elements have been replaced by ObjectDataSource elements. In other words, the code for the drop-down list and DataList controls is identical whether the application uses a SQL data source or an object data source.

In the first ObjectDataSource control, the TypeName attribute specifies ProductDB, and the SelectMethod attribute specifies GetAllCategories. As a result, the GetAllCategories method in the ProductDB data access class will be called to retrieve the category data when the drop-down list is bound.

In the second ObjectDataSource control, a ControlParameter element within the SelectParameters element is used to declare the CategoryID parameter. This parameter is bound to the SelectedValue property of the drop-down list.

Because the data binding for this application is defined entirely in the aspx file, there is no code-behind file for this page. As a result, the only C# code for this application is in the ProductDB class, which is presented in the next figure.