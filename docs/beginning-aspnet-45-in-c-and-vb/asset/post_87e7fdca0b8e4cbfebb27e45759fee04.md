
```csharp
GridView1.DataBind();
}
```

This code also uses the New keyword (new in C#) to create a new, anonymous type that contains only the review's title and the genre's name.

## Exercise 2 Solution

The biggest benefit of the ListView control is that it combines the strengths of those other data controls. Just like the GridView control, the ListView control makes it easy to display data in a grid format that users can edit from within the grid. Additionally, the ListView control enables you to insert new rows, behavior that is found in controls like DetailsView and FormView but not in GridView.

Finally, the ListView control gives you full control over the markup that gets sent to the browser, an important feature that only the Repeater control gives you out of the box.

## Exercise 3 Solution

First you would need to change the Default.aspx page in the PhotoAlbums folder so it links each thumbnail to a details page and passes the ID of the picture to this new page. In the `<ItemTemplate>` of the ListView control in Default.aspx, add this HyperLink control around the Image control that was already there:

```aspx
<asp:HyperLink ID="HyperLink1" runat="server"
NavigateUrl='<%# "PictureDetails.aspx?id=" + Item.Id.ToString() %>'>
<asp:Image ID="Image1" runat="server" ImageUrl='<%# Item.ImageUrl %>'
ToolTip='<%# Item.ToolTip %>' />
</asp:HyperLink>
```

Note that the NavigateUrl is built up from the static text `PictureDetails.aspx?id=` and the ID of the picture in the database.

Then create a new page called PictureDetails.aspx and add an Image control in the markup:

```aspx
<asp:Content ID="Content2" ContentPlaceHolderID="cpMainContent" runat="server">
<asp:Image ID="Image1" runat="server" />
</asp:Content>
```

Finally, you need to execute the following LINQ query in the Load event of the page in the Code Behind to set the ImageUrl:

### VB.NET

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Dim pictureId As Integer = Convert.ToInt32(Request.QueryString.Get("Id"))
    Using myEntities As New PlanetWroxEntities()
        Dim imageUrl As String = (From picture In myEntities.Pictures
                                  Where picture.Id = pictureId
                                  Select picture).Single().ImageUrl
        Image1.ImageUrl = imageUrl
    End Using
End Sub
```

You need to store the ImageUrl in the DataKeyNames property. This adds it to View State so it roundtrips to the browser and is available in the Deleted event.

## Exercise 5 Solution

To display only genres that have at least one review, all you need to do is filter out empty genres using Where with a Count method like this:

### VB.NET

```vb
Dim genresWithReviews = From genre In myEntities.Genres
    Order By genre.Name
    Where genre.Reviews.Count() > 0
    Select New With {genre.Name, genre.Reviews}
```

### C#

```csharp
var genresWithReviews = from genre in myEntities.Genres
    orderby genre.Name
    where genre.Reviews.Count() > 0
    select new { genre.Name, genre.Reviews };
```

## CHAPTER 15

## Exercise 1 Solution

The Load event of the Page always fires before user-triggered events such as a Button control's Click.

## Exercise 2 Solution

To preselect the correct item in the drop-down list after a user has inserted or edited a review, you need to make two modifications. First, you need to change the Redirect statement in the AddEditReviewHandCoded.aspx page so it includes the ID of the genre:

### VB.NET

```vb
Response.Redirect(String.Format("Reviews.aspx?GenreId={0}",
    GenreList.SelectedValue))
```

### C#

```csharp
Response.Redirect(string.Format("Reviews.aspx?GenreId={0}",
    GenreList.SelectedValue));
```

Using String.Format makes this code a bit easier to read as opposed to plain string concatenation using the ampersand (&) in VB.NET and the plus (+) in C#.

If you now insert or edit a new review, you'll see that the ID of the genre is passed back to the Reviews.aspx page. On that page, you can use that ID to preselect the correct item in the DropDownList control, which you can accomplish with the following code in the Page_Load method:

### VB.NET

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Not Page.IsPostBack Then
        Dim genreId As String = Request.QueryString.Get("GenreId")
        If Not String.IsNullOrEmpty(genreId) Then
            DropDownList1.DataBind()
            Dim myItem As ListItem = DropDownList1.Items.FindByValue(genreId)
            If myItem IsNot Nothing Then
                myItem.Selected = True
            End If
        End If
    End If
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
    {
        string genreId = Request.QueryString.Get("GenreId");
        if (!string.IsNullOrEmpty(genreId))
        {
            DropDownList1.DataBind();
            ListItem myItem = DropDownList1.Items.FindByValue(genreId);
            if (myItem != null)
            {
                myItem.Selected = true;
            }
        }
    }
}
```

Only when the page loads from a new request (and not from a postback) does this code fire. The code then tries to find a GenreId in the query string. If it can find it, it tries to find an item with that requested value in the DropDownList. Because the DropDownList control hasn't been data bound yet, it doesn't contain any items. Therefore, you need to call DataBind() first. This gets the genres from the database using EF and puts them in the DropDownList. Once that's done and the item is found in the Items collection, it's made the active item by setting its Selected property to True/true. The SqlDataSource control watches this DropDownList, so when the data source gets its reviews, it does so for the correct genre.

## Exercise 3 Solution

The various data-bound controls can raise exceptions that you can handle in their event handlers.

Once you have dealt with the exception appropriately, you need to set the ExceptionHandled property of the e argument to True. The following code snippet shows how a Label control is updated.

From a maintainability perspective, it would be a lot better to add John to the Managers or Editors role if possible. However, you may end up giving John more rights than you want (he could then access anything that a Manager or an Editor could access). Generally, it's best to manage users through roles as much as possible, but it's good to know that you can grant individual accounts the necessary rights as well (or explicitly take those rights away using a deny element).

## Exercise 3 Solution

If you want to redirect all users to the same page, all you need to set is the DestinationPageUrl:

```aspx
<asp:Login ID="Login1" runat="server" DestinationPageUrl="~/MyProfile.aspx">
```

When a user is logged in successfully, she's taken to MyProfile.aspx automatically.

## Exercise 4 Solution

The LoginStatus simply displays a simple link that indicates whether or not the user is logged in. By default, the text that is displayed is Login when the user is currently not logged in, and Logout when the user is already logged in. Clicking the link either sends the user to the default Login page or logs the user out.

The LoginView is somewhat similar in that it displays different content depending on whether the user is currently logged in. However, because the control is completely template driven, you can fully control the content that is displayed. To enable you to differentiate between different user roles, you can use the RoleGroups element to set up templates that are shown only to users in specific roles.

## CHAPTER 17

## Exercise 1 Solution

You would implement the favorite theme as a String property and call it FavoriteTheme. To ensure that you always have a valid theme, you could also set a default value. Finally, you should make the property accessible to anonymous users. Your final profile property could end up like this:

```xml
<add name="FavoriteTheme" defaultValue="Monochrome" allowAnonymous="true" />
```

To support anonymous profiles, you need to explicitly enable them by adding an `<anonymousIdentification>` element as a direct child of `<system.web>` in the Web.config file:

```xml
<system.web>
    <anonymousIdentification enabled="true" cookieName="PlanetWroxAnonymous" />
```

## Exercise 2 Solution

Given the syntax you saw in the question, you could now access the new property and use it to change the current theme in the BasePage:

### VB.NET

```vb
Private Sub Page_PreInit(sender As Object, e As EventArgs) _
```