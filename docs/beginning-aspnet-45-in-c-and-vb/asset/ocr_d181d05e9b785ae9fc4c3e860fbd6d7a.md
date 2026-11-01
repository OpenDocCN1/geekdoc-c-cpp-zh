```
font-style: italic;
display: block;
}
```

9. Save all changes and then request All.aspx from the Reviews folder in your browser. Click the title of a review and you're taken to ViewDetails.aspx with the ID of the requested review in the query string.

> **COMMON MISTAKES** If you see an error message about an invalid page title, make sure you removed Title="" from the Page directive in ViewDetails.aspx. With the attribute set to an empty string, the title you set in Code Behind won't stick, and then your BasePage will raise an exception because the title is missing.

You should now see the details of the review displayed on the page. Press Ctrl+F5 or Ctrl+R to refresh the contents of the page. Although you don't see the difference, the review now comes from the cache. If you want to confirm this is really the case, you can add a Label control to the ViewDetails.aspx page and then update it with a text saying whether or not the item was in the cache:

# VB.NET

```
Label1.Text = "In the cache"
If myReview Is Nothing Then
    Label1.Text = "NOT in the cache"
Using myEntities As New PlanetWroxEntities()
```

# C#

```
Label1.Text = "In the cache";
if (myReview == null)
{
    Label1.Text = "NOT in the cache";
    using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
```

This code initially sets the Label's Text to "In the cache". However, if the item isn't found, the Label is updated to reflect that observation.

> **COMMON MISTAKES** If you get the error "Page title cannot be 'Untitled Page' or an empty string", make sure you're passing a valid Review ID in the ReviewId query string parameter to the ViewDetails.aspx page. You usually get this error when you browse to the details page directly from within VS using Ctrl+F5 rather than through All.aspx. To work around this situation, you could add code to redirect the user back to All.aspx when there's not valid value in the ReviewId query string parameter, which you could check using String.IsNullOrEmpty(Request.QueryString.Get("ReviewId")). For other unforeseen situations you need to add error-handling code to your page. This is the topic of Chapter 18.