nasty error page, but a nice and friendly error message at the top of the GridView instead. Note that for all other types of exceptions, the user still gets the default ASP.NET error message screen, also called the Yellow Screen of Death. Chapter 18 teaches you some techniques to log the error in a central location and present the user with a friendly, human-readable error page instead.

The number 547 seems to be arbitrarily chosen, but it's the number that SQL Server returns for a foreign key constraint exception. In Chapter 18, which deals with debugging, you learn a few tricks that enable you to look into the exceptions that are thrown so you can diagnose the Number property for different kinds of exceptions.

In the past few chapters you have seen many examples of accessing a database using one of the built-in data controls like SqlDataSource and EntityDataSource. Useful and quick to use as they are, they are not suitable for every situation. In cases where they don't fit, you can always hand-code your pages, as you see how to do next.

# HAND-CODING DATA ACCESS CODE

The biggest issue I often have with the data controls is the amount of markup that they require. Although, for example, the ListView generates most of the code for you, you still end up with a lot of code in the page. This makes it cumbersome and time-consuming to make a lot of modifications to this control. Another issue with these controls is that often you find yourself defining almost identical markup twice: once for an Insert template and once for an Edit template. The final issue I often encounter when working with the data controls is that I do not have complete control over the markup they create. This can make it difficult sometimes to create fancy and complex pages with multiple levels of bound drop-down controls, AJAX UpdatePanel controls, image uploads, and more. To overcome these issues, you can hand-code your pages, which gives you full control over the markup in the page and the code in the Code Behind.

Hand-coding isn't as difficult as it seems and you do get a lot of flexibility in return for the extra effort. Though the actual process differs from page to page, here's a general description of the steps you need to carry out to hand-code an Add/Edit page that enables you to enter a new or update an existing item in the database with the same markup:

+   - Create the user interface by adding a number of controls, such as TextBox and DropDownList, to a page that enables users to enter new and update existing data.
+   - Add validation controls to the page so users are forced to enter valid data.
+   - In the Code Behind, figure out whether you're creating a new or editing an existing item. You can make the distinction by looking at the query string, for example. When you're editing an existing item, you get it from the data source and prepopulate the form controls.
+   - Handle the Save button to insert or update the item. When you're updating an existing item, you should get the item from the database first and then overwrite the existing values with the new ones from the form. Finally, save the items back to the data store.

In the next Try It Out you build a page that implements this process.