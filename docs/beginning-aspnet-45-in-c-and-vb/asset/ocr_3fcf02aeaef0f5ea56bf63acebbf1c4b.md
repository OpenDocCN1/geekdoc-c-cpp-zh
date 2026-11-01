Although it may take you some time to fully understand the principles behind these LINQ queries and the Entity Framework, I am sure you are beginning to appreciate their power and accessibility. With just a few lines of code and a few controls, you can create powerful data presentation pages.

However, it's possible to create LINQ queries that execute against EF and use them with the ASP.NET Server Controls with even fewer lines of code. You see how this works in the next section, which deals with the EntityDataSource, the ListView, and the DataPager controls.

# USING SERVER CONTROLS WITH LINQ QUERIES

So far you have seen one way to bind the results of a LINQ query against EF to a control in your ASPX page: assign the data to the control's DataSource property and then call DataBind. This way of getting data into the controls has a few shortcomings. First of all, this method does not support the editing, updating, and deleting of data directly. Secondly, because you define the data source in the Code Behind, the GridView doesn't know what data you're feeding it until run time, so you get no tool support to set up its columns. These shortcomings are easy to overcome by using the server controls, including the ListView and the EntityDataSource control.

# Using Data Controls with the Entity Framework

In the previous chapter you were introduced to some of the data controls, like the GridView and the SqlDataSource. But ASP.NET 4.5 ships with more controls that let you create data-driven pages with very few lines of code. Two of these controls provide a visual interface in your ASP.NET pages, and the third one works as a bridge between your data-bound controls and your underlying data sources. The following table briefly introduces you to these controls.

| CONTROL | DESCRIPTION |
|---|---|
| EntityDataSource | As with the SqlDataSource that you saw in previous chapters, the EntityDataSource works as a bridge between your data-bound controls and the underlying data source: EF in this case. |
| ListView | The ListView control provides a template-driven visual interface that enables you to display, insert, edit, and delete items in a database, providing full CRUD services. |
| DataPager | The DataPager is used together with the ListView and enables you to paginate the data in the data source, feeding data to users in bite-sized chunks instead of all rows at once. |

The next few sections provide you with more detail about these controls and show you how to use them in a few Try It Out exercises.

# Introducing the EntityDataSource Control

As its name implies, the EntityDataSource is a close relative of the SqlDataSource and other data source controls. The EntityDataSource control is to EF what the SqlDataSource control