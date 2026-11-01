
6. The diagram window should now show a line between the two tables. At the side of the Genre table, you should see a yellow key to indicate this table contains the primary key for the relationship. At the other end, you should see the infinity symbol (the number 8 turned 90 degrees) to indicate that the Review table can have many rows that use the same GenreId. You see the diagram in Figure 12-24.

![](img/eadab2ccd79b253c01a3fdff2321202d_493_0.png)

FIGURE 12-24

Note that in your diagram the line heads between the two tables don't necessarily point to the correct columns; they just point to the entire table. This can be confusing sometimes because you may think that other columns are actually related. To confirm the columns participating in the relationship, right-click the line between the two tables and choose Properties. The Table and Columns Specification item shows which columns and tables participate in the relationship, shown in Figure 12-25.

You can drag the line heads up and down to point to the correct column. This doesn't affect the tables, but it makes your intent clearer to others viewing the diagram.

![](img/eadab2ccd79b253c01a3fdff2321202d_493_1.png)

FIGURE 12-25

7. Press Ctrl+S to save the changes to the diagram. You can leave the name set to its default or you can enter a more descriptive name such as Reviews and Genres and click OK. You'll get another warning that states that you are about to make changes to the Review and Genre tables. Click Yes to apply the changes.

8. Go back to the Object Explorer, expand the Tables node, right-click the Genre table, and choose Edit Top 200 Rows. Enter a few different genres by typing a Name and a SortOrder. When you press Tab in the SortOrder field to tab away from the current row, the row is inserted in the database, and the Id column is filled with a unique, sequential number. You should end up with a list similar to the one shown in Figure 12-26.

9. Open the Review table from the Database Explorer using the Edit Top 200 Rows command and enter a few review rows. For the GenreId, supply some of the new IDs you got when you inserted rows in the Genre table. You can just make up the Title, Summary, and Body fields for now and set Authorized to True. Remember, you don't have to enter a value for the date columns. If you leave them out, the database will insert the default value for you. Notice that you can't insert a value in the Id column yourself. Because this column is an Identity field, the database supplies values for you automatically. If you get an error about missing values for the date columns, ensure that you entered a proper default value in the previous exercise. When you're done entering a row, click outside the row (on the new, empty row below it, for example) to insert the row in the table. Your list of rows should look similar to Figure 12-27, although your content for the columns, of course, may be different.

![](img/eadab2ccd79b253c01a3fdff2321202d_494_0.png)

![](img/eadab2ccd79b253c01a3fdff2321202d_494_1.png)

10. Right-click the Genre table again and choose Edit Top 200 Rows. Click the SQL pane button on the Query Designer toolbar and then use the Change Type button on the same toolbar to create a DELETE query. Modify the query so it deletes one of the genre IDs you used in step 9 to link the reviews to, like this:

```
DELETE FROM Genre WHERE Id = 5
```

This code will attempt to delete the Indie Rock genre. However, because reviews are connected to it, the delete action should fail. Press Ctrl+R to execute the query. Instead of deleting the row from the Genre table, SSMS now shows you the dialog box you see in Figure 12-28.

![](img/eadab2ccd79b253c01a3fdff2321202d_494_2.png)

## How It Works

When you create a relationship between two tables, the database will enforce this relationship when you try to insert, update, or delete data. In this example, rows in the `Review` table have a genre that exists in the `Genre` table. When you try to delete a row from the `Genre` table, the database sees that the genre is used by a row in the `Review` table and cancels the delete operation. In Chapter 15 you learn how to handle this situation in your website and present your user with a friendly error message.

Now that you've seen the underlying concepts in dealing with databases, you're ready for the next chapter, which shows you how to work with your database using the many available ASP.NET data controls.

## PRACTICAL DATABASE TIPS

The following list provides some practical tips on working with databases:

- Because the database is often at the heart of a website, you need to carefully consider its design. It's especially important to think of a good design up front, before you start building your site on top of it. When you have a number of pages that access your database, it will become harder to make changes—such as removing tables or renaming columns—to the data model.
- Always consider the primary key for your table. I prefer to give each table a column called Id. The underlying data type is then an `int` and an identity, which gives each row a unique ID automatically. Instead of an `int`, you can also consider the `uniqueidentifier` data type, which ensures uniqueness even across database or application boundaries. However, a `uniqueidentifier` is much slower than the `int` data type (especially during inserts) so use this only when you need the benefits of the `uniqueidentifier` data type.
- Give your database objects such as tables and columns logical names. Avoid characters such as spaces, underscores, and dashes. A name like `GenreId` is much easier to read than `colGen_ID_3`.
- Don't use `SELECT *` to get all columns from a database. By using `SELECT *` you may be selecting more columns than you actually need. By defining the columns you want to retrieve explicitly, you make your intentions to others clearer and increase the performance of your queries at the same time.
- Always create relationships between tables when appropriate. Although querying for the reviews and genres you saw in this chapter without a relationship between the two tables works just fine, relationships help you enforce the quality of your data. With proper relationships, you minimize the chance of ending up with orphaned or incorrect data.

## SUMMARY

The ability to work with databases is a good addition to your set of web development skills. Most of today's dynamic websites use databases, so it's important to understand how to work with them.

To access and manipulate data in a relational database, you use a language called Structured Query Language, or SQL for short. Among other elements, this language defines four important keywords that enable you to perform CRUD—Create, Read, Update, Delete—operations against a database.

The SELECT statement enables you to retrieve data from one or more tables. To access more than one table, you can use one of the available JOIN types to define a relationship between the tables. To limit the number of rows returned by a query, you can use a WHERE clause. To order the items in the result set returned by your query, you use the ORDER BY clause. To create new rows in your database you use the INSERT statement, and you need an UPDATE statement to change existing rows. Finally, to delete rows that you no longer need, you use the DELETE statement. Just like the SELECT and UPDATE statements, DELETE takes an optional WHERE clause that enables you to limit the number of rows that get deleted.

The second part of this chapter showed you how to use the built-in database tools to create tables with relationships between them. In addition, you saw how a relationship between two tables enables you to protect your data from becoming corrupt or orphaned.

Although this chapter had a strong focus on the SQL that you need to write to access a database, you see in the next chapter that in many cases Visual Studio makes accessing databases pretty easy as well by generating most of the code for you. However, a solid knowledge of SQL helps you in understanding and tweaking the code that is being written for you.

## EXERCISES

- 1. If you try to delete a row from the Genre table that has matching rows in the Review table, the DELETE statement fails. How is this possible?
- 2. If you try to delete a row from the Review table that has its GenreId set to the Id of an existing genre in the Genre table, the DELETE statement succeeds. Why?
- 3. Imagine you want to clean up your database and decide to delete all rows from the Review table that have an Id of 100 or less. Write a SQL statement that deletes these rows.
- 4. Imagine you want to delete the genre with an ID of 4. But before you delete the genre, you want to reassign reviews assigned to this genre to another genre with an ID of 11. What SQL statements do you need to accomplish this?
- 5. Write a SQL statement that updates the Rock genre to read Punk Rock instead. You have at least two ways to write the WHERE clause for this statement.

You can find answers to these exercises in Appendix A.
