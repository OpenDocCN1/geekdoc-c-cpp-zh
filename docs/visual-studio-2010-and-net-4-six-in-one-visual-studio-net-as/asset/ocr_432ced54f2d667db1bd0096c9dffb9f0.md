```
TempData["book"] = book;
return View(book);
}
```

```
[HttpPost]
public ActionResult Delete(int id, FormCollection collection)
{
    try
    {
        var context = TempData["context"] as AcmeLibraryDataEntities;
        var book = TempData["book"] as Book;
        if (context != null && book != null)
        {
            context.DeleteObject(book);
            context.SaveChanges();
        }
        context.Dispose();

        return RedirectToAction("Index");
    }
    catch
    {
        return View();
    }
}
```

The first Delete action is used when the book information is to be shown in a view where the user can confirm the delete operation. The second Delete action is invoked when the operation is confirmed. Now, you can most likely figure out how these methods work without any further explanation.

Use the Add View command from one of the Delete methods and use both for the view name and the View selection. The structure of the generated Delete.aspx file you do not need to display all book attributes in the confirmation page. Keep only the Author, Title, and ISBN fields. Remove the HTML tags associated with other fields. Your Delete view should look like the code in Listing 18.

# LISTING 18: Book/Delete.aspx

```
<@ Page Title="" Language="C#" MasterPageFile="~/Views/Shared/Site.Master" Inherits="System.Web.Mvc.ViewPage<AcmeLibrary.Models.Book> %>
<asp:Content ID="Content1" ContentHolderID="TitleContent" runat="server">
Delete
</asp:Content>
<asp:Content ID="Content2" ContentHolderID="MainContent" runat="server">
Delete
<h2></h2>
<h3>
<p>Are you sure you want to delete this book?</p>
</h3>
<fieldset>
    <legend>Fields</legend>
    <div class="display-label">Author</div></div>
```