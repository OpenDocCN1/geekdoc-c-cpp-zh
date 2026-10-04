9. After the word InsertMethod, type an equals sign (=). Visual Studio inserts the equals sign and two double quotes and pops up a list that you create a new method, as shown in Figure 14-10.

```
<Content Content="runat=Server">\<View DefaultMethod="Insert" runat="Server" SelectMethod="" />
```

FIGURE 14-10

10. Select the <Create New Method> item with the keyboard and press Enter or double-click the item. Visual Studio completes the DetailsView as follows:

```
InsertMethod="DetailsView1_InsertItem"
```

Besides the change in Markup View, Visual Studio also added the following method definition to the Code Behind:

# VB.NET

```
Public Sub DetailsView1_InsertItem()
```

```
End Sub
```

# C#

```
public void DetailsView1_InsertItem()
{
}
```

11. Switch to Code Behind and complete that method as follows:

# VB.NET

```
Public Sub DetailsView1_InsertItem()
Dim photoAlbum As New PhotoAlbum()
TryUpdateModel(photoAlbum)
If ModelState.IsValid Then
    Using myEntities As New PlanetWrixEntities()
    myEntities.PhotoAlbums.Add(photoAlbum)
    myEntities.SaveChanges()
End Using
Response.Redirect(String.Format("*ManagePhotoAlbum?PhotoId={0}", photoAlbum.Id.ToString()))
End If
End Sub
```

# C#

```
public void DetailsView1_InsertItem()
{
    PhotoAlbum photoAlbum = new PhotoAlbum();
    TryUpdateModel(photoAlbum);
    if (ModelState.IsValid)
    {
        using (var myEntities = new PlanetWrixEntities())
        {
```