# 3. Next, set up the SelectMethod for the DropList control and call the method GenreList_GetData. Your control should look like this:

```
<asp:DropDownList ID="GenreList" runat="server" DataTextField="Name"
    DataValueField="Id" SelectMethod="GenreList_GetData">
</asp:DropDownList>
```

Then switch to the Code Behind and implement the GetData method as follows:

```
Public Function GenreList(GetData()) As Enumerable(Of Genre)
    Using MyEntities As PlanetWroxEntities()
        Return (from genre in myEntities.Genres
               Order By genre.SortOrder
               Select genre).ToList()
    Using
End Function
```

# C#

```
public IEnumerable<Genre> GenreList_GetData()
{
    using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
    {
        return (from genre in myEntities.Genres
                orderby genre.SortOrder
                select genre).ToList();
    }
}
```

# 4. The next step is to write code that gets an Review from the database if the user is editing an item. The page assumes you are editing an item when the query string contains the item's ID. If it doesn't, it assumes you are creating a new review.

To set up the code, double-click the gray and read-only area of the page in Design View to set up a handler for the Page's Load event, and add the following code. Don't forget the _id variable outside the class definition.

# VB.NET

```
Partial Class Management_AddEditReviewHandCoded
    Inherits System.Web.UI.Page

    Dim _id As Integer = -1
    GenreList_GetData
```

```
Protected Sub Page_Load(Sender As Object, As EventArgs) Handles Me.Load
    If Not String.IsNullOrEmpty(Request.QueryString("*id*")) Then
        _id = Convert.ToInt32(Request.QueryString("*id*"))
    End If
    If Not Page.IsPostBack And _id = -1 Then
        Using MyEntities As New PlanetWroxEntities()
            Dim review = (from R In MyEntities.Reviews
                          Where R.Id = _id
                          Select R).SingleOrDefault()
```