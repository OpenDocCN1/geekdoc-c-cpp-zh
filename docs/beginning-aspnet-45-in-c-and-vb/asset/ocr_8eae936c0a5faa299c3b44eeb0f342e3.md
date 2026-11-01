the PlanetWroxModel namespace, and then add the following bold code. Don't forget the _id variable outside Page_Load but inside the class definition.

# VB.NET

```
```vbnet
Imports PlanetWroxModel

Partial Class Management_AddEditReviewHandCoded
    Inherits System.Web.UI.Page

    Dim _id As Integer = -1
    Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
        If Not String.IsNullOrEmpty(Request.QueryString.Get("Id")) Then
            _id = Convert.ToInt32(Request.QueryString.Get("Id"))
        End If
        If Not Page.IsPostBack And _id > -1 Then
            Using myEntities As New PlanetWroxEntities()
                Dim review = (From r In myEntities.Reviews
                              Where r.Id = _id
                              Select r).SingleOrDefault()

                If review IsNot Nothing Then
                    TitleText.Text = review.Title
                    SummaryText.Text = review.Summary
                    BodyText.Text = review.Body
                    GenreList.DataBind()
                    Dim myItem As ListItem =
                        GenreList.Items.FindByValue(review.GenreId.ToString())
                    If myItem IsNot Nothing Then
                        myItem.Selected = True
                    End If
                    Authorized.Checked = review.Authorized
                End If
            End Using
        End If
    End Sub
End Class
```
```

# C#

```
```csharp
using PlanetWroxModel;

public partial class Management_AddEditReviewHandCoded : System.Web.UI.Page
{
    int _id = -1;
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!String.IsNullOrEmpty(Request.QueryString.Get("Id")))
        {
            _id = Convert.ToInt32(Request.QueryString.Get("Id"));
        }
        if (!Page.IsPostBack && _id > -1)
        {
            using (PlanetWroxEntities myEntities = new PlanetWroxEntities())
```
```