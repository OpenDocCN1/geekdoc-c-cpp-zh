Except for the highlighted line of code and the variable name, this LINQ query is identical to the one used in AllByGenre.aspx. What makes this example special is the where clause that limits the number of reviews to those that the user is really interested in. Note how the Contains method of the generic List class is used here. Although at first it may seem that all genres and reviews are retrieved from the database into the ASPX page and then compared with the values in the profile property called FavoriteGenres, the reverse is actually the case. The Entity Framework is smart enough to collect all the IDs from the FavoriteGenres property first and then include them in the SQL statement that is sent to the database to fetch the requested genres and reviews. This means that filtering of the requested genres takes place at the database level, and not in the ASPX page. This in turn means that fewer rows are transferred from the database to the ASPX page (only those that are really needed), which results in better performance.

The profile property FavoriteGenres returns an empty list, rather than throwing an exception for anonymous users. So, even users with no profile can safely view this page. Instead of seeing any reviews, they get a message stating they haven’t set their genre preferences yet, or that they need to log in first.

In the end of the Page_Load handler, some code determines whether to show or hide the Repeater and the NoRecords controls:

# VB.NET

```
GenreRepeater.Visible = GenreRepeater.Items.Count > 0
NoRecords.Visible = Not GenreRepeater.Visible
```

# C#

```
GenreRepeater.Visible = GenreRepeater.Items.Count > 0;
NoRecords.Visible = !GenreRepeater.Visible;
```

If after data binding the outer Repeater, its Items collection is still empty, it means no genres were found for the current user. If that’s the case, the entire Repeater is hidden and the PlaceHolder is shown. However, if the Count property of the Items collection is larger than zero, the Repeater is made visible and the PlaceHolder is hidden.

In Chapter 14, you created a page called NewPhotoAlbum.aspx that lets users insert new Gig Pics albums. The current implementation of this page has a few shortcomings. First of all, anyone can insert a new album. There’s no way to block anonymous users from creating a new album and uploading pictures.

Secondly, only Managers can remove pictures from an existing photo album. It would be nice if the owner of an album could also remove her own pictures. Now that you know more about security and personalizing web pages, this is pretty easy to implement, as you see in the following exercise.

# TRY IT OUT  Letting Users Manage Their Own Photo Albums

In this Try It Out you see how to block the NewPhotoAlbum.aspx and ManagePhotoAlbum.aspx pages from unauthenticated users. Additionally, you see how to record the name of the user who created the photo album and use that name later on to enable users to alter their own photo albums.