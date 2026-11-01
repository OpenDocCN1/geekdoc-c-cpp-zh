Alternatively, you can access the Roles class that contains a number of static methods that you can access directly. The following code is functionally equivalent to the previous example:

```
VB.NET
If Roles.IsUserInRole("Managers") Then
    ' This code runs for Managers only
End If
```

```
C#
if (Roles.IsUserInRole("Managers"))
{
    // This code runs for Managers only
}
```

In addition to the IsUserInRole method, the Roles class contains a lot of other methods that enable you to work with roles programmatically. For example, you can create and delete roles, assign users to and remove users from roles, and you can get a list of users that are assigned to a certain role. For more information about the Roles API, check out the MSDN documentation at http://tinyurl.com/RolesAPI4-5 or pick up a copy of Professional ASP.NET 3.5 Security, Membership, and Role Management with C# and VB by Bilal Haidar (Wrox, ISBN: 978-0-470-37930-1). Although the book targets ASP.NET 3.5, you'll find that most topics discussed in that book still apply to ASP.NET 4.5.

In the following exercise, you learn how to modify the photo albums page so users logged in as Managers are able to delete pictures from a photo album. Other users won't be able to delete a picture because the Delete button will be hidden for them.

# TRY IT OUT  Checking Roles with IsUserInRole at Run Time

This Try It Out uses a programmatic check for the user's role to hide or show the Delete button. Although you could recreate this example by using a LoginView with different templates and RoleGroups, this exercise serves as an example of programmatic role checking.

+   1. Open Default.aspx from the PhotoAlbums folder in Markup View and right after the closing tag of the ListView control, enter two HTML breaks (you can use the br snippet) followed by a HyperLink control (you can use the hyperlink snippet). Set its ID property to EditLink and its Text property to Edit Photo Album. You assign the NavigateUrl programmatically in the next step.
+   
+      <br /> <br />
+      <asp:HyperLink ID="EditLink" runat="server" Text="Edit Photo Album" />
+   
+   2. Switch to Design View, select the ListView control, open up its Properties Grid, and switch to the Events tab. Double-click DataBound to set up a handler for that event. Inside the handler that VS created, add the following code:
+   
+      VB.NET
+      Protected Sub ListView1_DataBound(sender As Object,
+          e As EventArgs) Handles ListView1.DataBound