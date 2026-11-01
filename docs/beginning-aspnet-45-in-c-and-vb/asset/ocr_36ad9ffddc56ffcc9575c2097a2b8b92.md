10. Double-click the Save Profile button and in the Click event handler that VS added for you, write the following bolded code:

```
VB.NET
Protected Sub SaveButton_Click(sender As Object,
    e As EventArgs) Handles SaveButton.Click
    If Page.IsValid Then
        Profile.FirstName = FirstName.Text
        Profile.LastName = LastName.Text
        Profile.DateOfBirth = DateTime.Parse(DateOfBirth.Text)
        Profile.Bio = Bio.Text
    End If
End Sub
```

```
C#
protected void SaveButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        Profile.FirstName = FirstName.Text;
        Profile.LastName = LastName.Text;
        Profile.DateOfBirth = DateTime.Parse(DateOfBirth.Text);
        Profile.Bio = Bio.Text;
    }
}
```

11. In the Page_Load event handler of the same page, add the following code, which fills in the text box controls with the data from the profile when the page loads:

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    If Not Page.IsPostBack Then
        FirstName.Text = Profile.FirstName
        LastName.Text = Profile.LastName
        DateOfBirth.Text = Profile.DateOfBirth.ToShortDateString()
        Bio.Text = Profile.Bio
    End If
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
    {
        FirstName.Text = Profile.FirstName;
        LastName.Text = Profile.LastName;
        DateOfBirth.Text = Profile.DateOfBirth.ToShortDateString();
        Bio.Text = Profile.Bio;
    }
}
```

12. Save all changes and request the page in the browser. If you're required to log in first, enter your details and click the Login button. You should see the My Profile page reappear with the data you