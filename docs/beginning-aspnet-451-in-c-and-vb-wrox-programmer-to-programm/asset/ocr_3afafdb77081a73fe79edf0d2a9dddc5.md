# CHAPTER 14 LINQ AND THE AD.NET ENTITY FRAMEWORK

```
If ModelState.IsValid Then
using myEntities As New PlanetWroxEntities()
p.PhotoAlbumId = photoAlbumId
myEntities.Pictures.Add(picture)
myEntities.SaveChanges()
End Using
End If
```

# C#

```
public void ListViewInsertItem([QueryString("PhotoAlbumId")] int photoAlbumId
{
    Picture picture = new Picture();
    TryUpdateModel(picture);
    if (ModelState.IsValid)
    using (var myEntities = new PlanetWroxEntities())
    {
        picture.PhotoAlbumId = photoAlbumId;
        myEntities.Pictures.Add(picture);
        myEntities.SaveChanges();
    }
}
```

This is very similar to the code you saw earlier to create a new photo album. The difference here is the photoAlbumId parameter, which is assigned the ID of the current photo album through the QueryString attribute. This ID is assigned to the PhotoAlbumId property of the picture, which eventually links the picture with the photo album in the database.

+   8. To display images by side by side instead of stacked below each other, add the following CSS code to Monochrome.css in the Monochrome theme's folder and save the file:
```css
.ItemContainer {
    width: 600px;
    list-style-type: none;
    clear: both;
}

.ItemContainer li {
    height: 300px;
    width: 200px;
    float: left;
}

.ItemContainer li img {
    width: 180px;
    margin: 10px 20px 10px 0;
n}
```

+   9. Add the same code to DarkGrey.css in the DarkGrey theme's folder, but this set the width of the ItemContainer class to 400px like this: