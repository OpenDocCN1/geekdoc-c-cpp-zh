+   1. You request the page in your browser and the page begins its page life cycle.
+   
+   2. The GridView knows it is set up to retrieve and display data because it has a DataSourceID attribute that points to a SqlDataSource control. It contacts this data source control and asks it for its data. The SqlDataSource connects to the database and fires its SelectCommand, the SQL statement that selects the Id, Name, and SortOrder from the Genre table in the database:
+   
+   3. When the SqlDataSource receives the requested rows from the database it hands them over to the GridView, which creates an HTML table out of them using the bound fields that have been set up in the <Columns> element. The GridView keeps track of the unique ID for each row that is displayed in the page by storing it in View State.
+   
+   4. As soon as you click the Edit link, the page posts back. The GridView is able to see what row you clicked on by looking at the associated DataKeyNames and retrieving the row's ID from View State. It then gets the latest results from the database by asking the SqlDataSource again to fire its SelectCommand, and, finally, puts the selected row in edit mode so you can change the relevant details. When you click the Update link, the GridView collects the new values from the TextBox controls and then contacts the SqlDataSource again.
+   
+   5. For each of the parameters in the <UpdateParameters> element of the SqlDataSource, the GridView supplies a value. It retrieves the Id of the genre from the selected row, and then retrieves the new Name and SortOrder values from the TextBox controls in the page.
+   
+   6. Armed with the relevant data for the Id, Name, and SortOrder, the SqlDataSource then executes its UpdateCommand against the database:
+   
+   Each of the parameters prefixed with the at symbol (@) is filled with the values that the GridView supplied. The SQL statement that gets sent to the database ends up looking similar to this:
+   
+   7. Finally, the GridView refreshes the data on the page by once again asking the SqlDataSource to execute its SelectCommand. This way, the GridView now displays the latest data with the update you made.

```
SelectCommand="SELECT [Id], [Name], [SortOrder] FROM [Genre]"
```

```
UpdateCommand="UPDATE [Genre] SET [Name] = @Name, [SortOrder] = @SortOrder WHERE [Id] = @Id"
```

```
UPDATE [Genre] SET [Name] = 'New Name', [SortOrder] = 1 WHERE [Id] = 1
```

The other commands work in a similar way and send their own SQL commands to the database.

At the end of the exercise, you added a new Web.config file to the Management folder to reset the theme that is applied to all pages in the Management section. With the theme removed, it's easier to focus on the functionality of the Management section, rather than be distracted by layout issues. In Chapter 15 you create a third theme specifically for the Management folder and apply that theme in the Web.config file in the Management folder. That way, your management pages will have a look and feel that's different from the pages in the front end.