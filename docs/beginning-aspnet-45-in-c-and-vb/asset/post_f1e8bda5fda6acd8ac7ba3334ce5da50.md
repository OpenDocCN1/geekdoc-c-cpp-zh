
For example, to return the ID and the title of a review together with the name of the genre it belongs to, you use this SQL statement:

```
SELECT
  Review.Id, Review.Title, Genre.Name
FROM
  Review
INNER JOIN Genre ON Review.GenreId = Genre.Id
```

Note that in the SELECT statement each column is prefixed with the table name. This makes it clear what table you are referring to and avoids conflicts when multiple tables have similar column names (like the Id column that exists in both tables).

In addition to an INNER JOIN that returns only matching rows, you can also use an OUTER JOIN. The OUTER JOIN enables you to retrieve rows from one table regardless of whether they have a matching row in another table. The following example returns a list with all the genres in the system together with the reviews in each genre:

```
SELECT
  Genre.Id, Genre.Name, Review.Title
FROM
  Genre
LEFT OUTER JOIN Review ON Genre.Id = Review.GenreId
```

For each review assigned to a genre, a unique row is returned that contains the review's title. However, even if a genre has no reviews assigned, the row is still returned as shown in Figure 12-14.

![](img/eadab2ccd79b253c01a3fdff2321202d_480_0.png)

FIGURE 12-14

The genre Indie Rock is repeated multiple times, once for each review in the Review table that has been assigned to that genre. The Punk genre has only one review attached to it, so it's listed only once. Finally, the Rock and Grunge genres have no reviews associated with them. However, because the SQL statement uses a LEFT OUTER JOIN, those two genres (listed on the left side of the JOIN) are still returned. Instead of the Title of a review, that column now contains a NULL value to indicate there is no associated review.

Besides the LEFT OUTER JOIN, there is also a RIGHT OUTER JOIN that returns all the rows from the table listed at the right side of the JOIN.

In addition, you can use other joins including cross joins and self joins. For a detailed description of these types of joins, pick up a copy of the book Beginning Microsoft SQL Server 2012 Programming by Paul Atkinson and Robert Vieira, Wrox, 2012 (ISBN: 978-1-1181-0228-2). You see how to use a very common type of join, the INNER JOIN, in the next Try It Out.

## TRY IT OUT Joining Data

To join data from two tables, you need to write a JOIN statement in your code. To help you write the code, SSMS adds a JOIN for you whenever you add related tables to the Diagram pane. However, sometimes this JOIN is not correct, so you'll need to check the code to see if it's okay.

- 1. Still in your test database in SSMS, right-click the Review table and choose Edit Top 200 Rows. You'll see all the reviews in the table appear. Next, enable the Diagram, Criteria, and SQL panes by clicking their respective buttons on the Query Designer toolbar.
- 2. Right-click an open spot of the Diagram pane next to the Review table and choose Add Table. Alternatively, choose Query Designer > Add Table from the main menu.
- 3. In the dialog box that opens, click the Genre table and then click the Add button. Finally, click Close.
- 4. The SQL statement that SSMS generated looks like this:
- 5. To see how you can create JOINs yourself without writing code directly, you'll manually re-create the JOIN. First, right-click the line that is drawn between the two tables in the Diagram pane and choose Remove. The SQL statement now contains a CROSS JOIN.
- 6. Next, click the GenreId column of the Review table in the Diagram pane once and drag it onto the Id column of the Genre table. As soon as you release the mouse, SSMS creates a new INNER JOIN in the SQL pane for you with the exact same code as you saw earlier. SQL Server understands the primary and foreign keys that have been set up in the database tables and correctly joins the primary key of the Genre table (Id) to the foreign key of the Reviews table (GenreId).
- 7. Modify the SQL statement so it selects only the Id and the Title columns from the Review table and the Name column from the Genre table. You can do this by altering the SQL statement manually or by unchecking the columns in the Diagram pane. Your SQL statement should now look like this:

```
SELECT TOP (200) Review.Id, Review.Title, Review.Summary, Review.Body,
Review.GenreId, Review.Authorized, Review.CreateDateTime, Review.UpdateDateTime
FROM Review
INNER JOIN Genre ON Review.GenreId = Genre.Id
```

SSMS correctly detected the relationship defined in the database between the GenreId column of the Review table and the Id column of the Genre table, and applied the correct JOIN for you.

```
SELECT TOP (200) Review.Id, Review.Title, Genre.Name
FROM Review INNER JOIN Genre ON Review.GenreId = Genre.Id
```

## Updating Data

To update data in a table, you use the UPDATE statement:

```
UPDATE TableName SET Column1 = NewValue1 [, Column2 = NewValue2] WHERE
Column3 = Value3
```

With the UPDATE statement, you can use Column = Value constructs to indicate the new value of the specified column. You can have as many of these constructs as you want, with a maximum of one per column in the table. To limit the number of items that get updated, you use the WHERE clause, just as with selecting data as you saw earlier. Without a WHERE clause, all rows will be affected which is usually not what you want.

The following example updates the row that was inserted with the INSERT statement you saw earlier. It sets the Name to Trance and updates the SortOrder to 5 to move the item up a little in sorted lists. It also uses the unique Id of the new row (13 in this example) in the WHERE clause to limit the number of rows that get affected with the UPDATE statement.

```
UPDATE Genre SET Name = 'Trance', SortOrder = 5 WHERE Id = 13
```

Obviously, you may also need to delete existing rows. It should come as no surprise that the SQL language uses the DELETE statement for this.

## Deleting Data

Just as with the SELECT and UPDATE statements, you can use the WHERE clause in a DELETE statement to limit the number of rows that get deleted. This WHERE clause is often very important, because you will otherwise wipe out the entire table instead of just deleting a few rows. Beware!

When you write a DELETE statement, you don't need to specify any column names. All you need to do is indicate the table that you want to delete rows from and an (optional) WHERE clause to limit the number of rows that get deleted. The following example deletes the row that was inserted and updated in the previous two examples:

```
DELETE FROM Genre WHERE Id = 13
```

If you leave out the WHERE clause, all rows will be deleted from the table.

You see these SQL statements at work in the next exercise.

## TRY IT OUT Working with Data in the Sample Database

In this exercise, you put everything you learned so far into practice. In a series of steps, you see how to create a new row in the Genre table, select it again to find its new ID, update it using the UPDATE statement, and finally, delete the genre from the database. Although the examples themselves may seem pretty trivial, they are at the core of how SQL works. If you understand the examples from this section, you'll be able to work with the remaining SQL statements in this and coming chapters.

- 1. Still in SSMS, right-click the Genre table and choose Edit Top 200 Rows. If the table was already open with an old query, you need to close it first by pressing Ctrl+F4. This gets rid of the existing SQL statement.
- 2. Click the first three buttons on the Query Designer toolbar (Diagram, Criteria, and SQL pane) to open up their respective panes.
- 3. In the SQL pane, remove TOP (200) from the SQL statement and then in the Diagram pane, uncheck the Id column and leave Name and SortOrder checked, as shown in Figure 12-16.

Because the Id column gets an auto-generated value from the database, you cannot supply an explicit value for it in an INSERT statement.

![](img/eadab2ccd79b253c01a3fdff2321202d_484_0.png)

FIGURE 12-16

- 4. On the Query Designer toolbar click the Change Type button and choose the third option: Insert Values. The query in the SQL pane is updated and now contains a template for the INSERT statement:

```
INSERT INTO Genre (Name, SortOrder) VALUES (,)
```

- 5. Between the parentheses for the VALUES, enter a name (between single quotes) and a sort order for your genre separated by a comma:

```
INSERT INTO Genre (Name, SortOrder) VALUES ('Folk', 15)
```

- 6. Press Ctrl+R to execute the query. You should get a dialog box that tells you that your action caused one row to be affected, as shown in Figure 12-17.

![](img/eadab2ccd79b253c01a3fdff2321202d_484_1.png)

FIGURE 12-17

- 7. Click OK to dismiss the dialog box.
- 8. Clear out the entire SQL statement from the SQL pane (you can use Ctrl+A to select the entire SQL statement and then press the Delete key to delete it) and replace it with this code, which selects all the genres and sorts them in descending order:

```
SELECT Id, Name FROM Genre ORDER BY Id DESC
```

- 9. Press Ctrl+R to execute this SELECT statement. The Results pane shows a list of genres with the one you just inserted at the top of the list. Note the ID of the newly inserted row. It should be 13 if you haven't inserted any rows before, although it's okay if you have a different ID.
- 10. Click the Change Type button on the toolbar again, this time choosing Update. Complete the SQL statement that SSMS created for you so it looks like this:

```
UPDATE Genre
SET
    Name = 'British Folk',
    SortOrder = 5
WHERE
    Id = 13
```

Don't forget to replace the number 13 in the SQL statement with the ID you determined in step 9.
- 11. Press Ctrl+R again to execute the query and you'll get a dialog box informing you that one row has been modified.
