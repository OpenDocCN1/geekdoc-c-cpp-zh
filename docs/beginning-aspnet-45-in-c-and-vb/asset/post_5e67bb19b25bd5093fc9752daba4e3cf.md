
5. At the top of the Code Behind, add the following namespace to bring the SqlException class into scope:

# VB.NET

```
Imports System.Data.SqlClient
```

# C#

```
using System.Data.SqlClient;
```

6. Inside the event handler that VS added for you in step 4, write the following code:

# VB.NET

```
Protected Sub SqlDataSource1_Deleted(sender As Object, e As SqlDataSourceStatusEventArgs) Handles SqlDataSource1.Deleted
    If e.Exception IsNot Nothing AndAlso TypeOf (e.Exception) Is SqlException Then
        Dim myException As SqlException = CType(e.Exception, SqlException)
        If myException.Number = 547 Then
            ErrorMessage.Text = "Sorry, you can't delete this genre because " &
            "it has associated reviews that you need to delete first."
            e.ExceptionHandled = True
        End If
    End If
End Sub
```

# C#

```
protected void SqlDataSource1_Deleted(object sender,
    SqlDataSourceStatusEventArgs e)
{
    if (e.Exception != null && e.Exception is SqlException)
    {
        SqlException myException = (SqlException)e.Exception;
        if (myException.Number == 547)
        {
            ErrorMessage.Text = @"Sorry, you can't delete this genre because
it has associated reviews that you need to delete first.";
            e.ExceptionHandled = true;
        }
    }
}
```

7. Comment out the code that you added in the previous Try It Out to stop the Delete link from being disabled. For this exercise it's enough to just comment out the line that disables the link:

# VB.NET

```
' deleteLink.Enabled = False
```

# C#

```
// deleteLink.Enabled = false;
```

If you wanted to remove this functionality completely, you could remove the entire event handler. In that case, don't forget to remove the handler from the GridView's markup in C# as well.

8. Save all your changes and then press Ctrl+F5 to open Genres.aspx in your browser. Try deleting a genre that you know has associated reviews, such as Rap and Hip-Hop. Instead of deleting the genre, the ASPX page now presents you with the error that is displayed above the GridView in Figure 15-11.

![](img/eadab2ccd79b253c01a3fdff2321202d_622_0.png)

FIGURE 15-11

If the error message doesn't appear in red, press Ctrl+F5 to force a fresh copy of the Management theme's style sheet.

9. Click the Manage Reviews menu item in the Management menu and then select the Rap and Hip-Hop genre from the drop-down list. Delete the reviews in the genre, or edit them and reassign them to a different genre.

10. Go back to Genres.aspx and try deleting the Rap and Hip-Hop genre again. This time the genre is successfully deleted from the database.

11. To see the error you would get without this error handling, comment out the line in the Code Behind that sets ExceptionHandled to True. Save your changes, open the page again in your browser, and try to delete a genre with reviews. You'll get a detailed ASP.NET error instead, shown in Figure 15-12.

![](img/eadab2ccd79b253c01a3fdff2321202d_622_1.png)

FIGURE 15-12

nasty error page, but a nice and friendly error message at the top of the GridView instead. Note that for all other types of exceptions, the user still gets the default ASP.NET error message screen, also called the Yellow Screen of Death. Chapter 18 teaches you some techniques to log the error in a central location and present the user with a friendly, human-readable error page instead.

The number 547 seems to be arbitrarily chosen, but it's the number that SQL Server returns for a foreign key constraint exception. In Chapter 18, which deals with debugging, you learn a few tricks that enable you to look into the exceptions that are thrown so you can diagnose the Number property for different kinds of exceptions.

In the past few chapters you have seen many examples of accessing a database using one of the built-in data controls like SqlDataSource and EntityDataSource. Useful and quick to use as they are, they are not suitable for every situation. In cases where they don't fit, you can always hand-code your pages, as you see how to do next.

## HAND-CODING DATA ACCESS CODE

The biggest issue I often have with the data controls is the amount of markup that they require. Although, for example, the ListView generates most of the code for you, you still end up with a lot of code in the page. This makes it cumbersome and time-consuming to make a lot of modifications to this control. Another issue with these controls is that often you find yourself defining almost identical markup twice: once for an Insert template and once for an Edit template. The final issue I often encounter when working with the data controls is that I do not have complete control over the markup they create. This can make it difficult sometimes to create fancy and complex pages with multiple levels of bound drop-down controls, AJAX UpdatePanel controls, image uploads, and more. To overcome these issues, you can hand-code your pages, which gives you full control over the markup in the page and the code in the Code Behind.

Hand-coding isn't as difficult as it seems and you do get a lot of flexibility in return for the extra effort. Though the actual process differs from page to page, here's a general description of the steps you need to carry out to hand-code an Add/Edit page that enables you to enter a new or update an existing item in the database with the same markup:

- Create the user interface by adding a number of controls, such as TextBox and DropDownList, to a page that enables users to enter new and update existing data.
- Add validation controls to the page so users are forced to enter valid data.
- In the Code Behind, figure out whether you're creating a new or editing an existing item. You can make the distinction by looking at the query string, for example. When you're editing an existing item, you get it from the data source and prepopulate the form controls.
- Handle the Save button to insert or update the item. When you're updating an existing item, you should get the item from the database first and then overwrite the existing values with the new ones from the form. Finally, save the items back to the data store.

In the next Try It Out you build a page that implements this process.

> NOTE In the next exercise, you hand-code the user interface and use the ADO.NET Entity Framework to handle all data access for you. It's also common to hand-code the interaction with the database using ADO.NET classes, such as classes that inherit from DbConnection, DbCommand, and DbDataReader. Although hand-coding the interaction with the database requires a lot more code, it also gives you greater control and more flexibility. Get yourself a copy of Wrox's Professional ASP.NET 4.5 in C# and VB (ISBN: 978-1-118-31182-0) for a deeper dive into ADO.NET.

### TRY IT OUT Hand-Coding Data Access Pages

In this exercise you create a new version of the AddEditReview.aspx page to replace the existing one that currently uses a DetailsView to handle the insert and update process. In the new page you add form controls to enter the review's title, summary, body, and genre and whether or not it's authorized. In the Code Behind of the page you work with the PlanetWroxEntities class to handle all data access code. To keep the exercise short you won't be adding any validation controls. However, with the knowledge you gained from Chapter 9, you know what to do to make this page accept valid data only.

+   1. Start by adding a standard Web Form (don't use your custom template) using Code Behind to the Management folder of your site and call it AddEditReviewHandCoded.aspx. Base the page on the Management master page and give it a meaningful title.
+   2. Switch to Design View, choose Table ⇨ Insert Table, and insert a table of six rows and two columns. Add controls to the cells of the HTML table and set their properties according to this table:

| ROW | COLUMN 1 | COLUMN 2 |
|---|---|---|
| 1 | Add a Label control
Text: Title | Add a TextBox control
ID: TitleText
Width: 450px |
| 2 | Add a Label control
Text: Summary | Add a TextBox control
ID: SummaryText
Width: 450px
TextMode: MultiLine |
| 3 | Add a Label control
Text: Body | Add a TextBox control
ID: BodyText
Width: 450px
TextMode: MultiLine |
| 4 | Add a Label control
Text: Genre | Add a DropDownList control
ID: GenreList |
