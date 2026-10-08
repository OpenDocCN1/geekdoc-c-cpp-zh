
# LISTING 18-11 (continued)

```html
<tr>
    <td><%%: item.ISBN %></td>
    <td><@%: String.Format("0:g", item.Published) %></td>
    <td><@%: item.Publisher %></td>
</tr>
<% %>
</table>
<p>
    <@%: Html.ActionLink("Create New", "Create") %>
</p>
</@asp:Content>
```

Code line [Book/Index.aspx] available for download at Wrox.com

As you can see, the code is very simple. The list is represented by an HTML <table>, where the first column contains links for the available actions Edit, Details, and Delete.

Select the AcmeLibrary project in Solution Explorer. Build and run the project by Ctrl+F5. When the application starts, Insert file file. Go to the home page. The Book/Index request path to the current URL in your browser's address line to navigate to the list of books. Figure 18-16 shows the page with an empty list of books.

![](img/b5597c749e848b27b0d305153ae16106_819_0.png)

FIGURE 18-16: The empty list of books

The page is currently not available from the home page of the application, but you can easily put a link by modifying the Site.Master file. Insert the following line between the two existing links in the <ul id="menu"> tag:

```html
<li><%% Html.ActionLink("Book", "Index", "Book")%></></li>
```

Using the Server Explorer, open the Book table with the Show Table Data context menu command, and add a few records to the table. Build and run your application and click the Book link. Your browser navigates to the Book/Index pages and lists the books you've recently added directly to the Book table, as shown in Figure 18-17.

![](img/b5597c749e848b27b0d305153ae16106_820_0.png)

**FIGURE 18-17:** The list of books can be accessed through a link

When you try to click on any of the Edit, Delete, or Create New links, you will receive a server error because the views of actions represented by these links have not yet been implemented.

## Adding Book Actions

Creating the controller actions and views for manifesting books is really simple and straightforward—thanks to the great tools and architecture behind MVC 2. First, let's create the Details action.

## Adding the Details View

The Details action displays the attributes of the model instance, and does not provide controls to edit them. Change the body of the Details method in the BookController class to the following code:

```csharp
public ActionResult Details(int id)
{
    var context = new AcmeLibraryDataEntities();
    var book = context.Books.First(b => b.Id == id);
    return View(book);
}
```

This code created an AcmeLibraryEntities context and used it to query the Book instance having the identifier by the Details method. This identifier comes from the third parameter of the ActionLink representing the action in the Index.aspx file:

```razor
<%% Html.ActionLink("Details","Details",new {itemId=id})%>
```

The action retrieves a view encapsulating the Book instance with the specified identifier. Right-click the body of the Details method in the code editor, and start the Add View menu command. Configure the Add View dialog as shown in Figure 18-18.

The content of the dialog is very similar to the one used for the Index view (see Figure 18-15), but this time the name of the view is set to Details, and the "View content" is set to the Details type. Click Add, and the Details.aspx page is generated in the Views/Book folder. The source code of this new view is simple, as shown in Listing 18-12.

![](img/b5597c749e848b27b0d305153ae16106_821_0.png)

# LISTING 18-12: Book/Details.aspx

```razor
<%@ Page Title="" Language="C#" MasterFile="~/Views/Shared/Site.Master"
Inherits="System.Web.Mvc.ViewPageBase:AcmeLibrary.Models.Book" %>

<asp:Content ID="Content1" ContentHolderID="TitleContent" runat="server">
    Details
</asp:Content>
<asp:Content ID="Content2" ContentHolderID="MainContent" runat="server">
    <h2>Details</h2>
    <fieldset>
        <legend>
            <div class="display-label">Id</div>
        </legend>
        <div class="display-field"><%= Model.Id %></div>
        <div class="display-label">Author</div>
        <div class="display-field"><%= Model.Author %></div>
        <div class="display-label">Title</div>
        <div class="display-field"><%= Model.Title %></div>
        <div class="display-label">ISBN</div>
        <div class="display-field"><%= Model.ISBN %></div>
        <div class="display-label">Published</div>
        <div class="display-field"><%= Model.Published %></div>
    </fieldset>
</asp:Content>
```

(Note: The provided OCR text for pages 822-824 contained significant corruption and repetitive fragments. Based on the context of MVC 2 and the preceding pages, the logical flow for the Edit action implementation is reconstructed below.)
