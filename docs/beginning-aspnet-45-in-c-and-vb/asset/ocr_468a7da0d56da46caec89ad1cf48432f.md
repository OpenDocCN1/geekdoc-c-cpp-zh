15. Save all your changes, close all open files, and then request `NewPhotoAlbum.aspx` in your browser. Make sure you don't accidentally open `ManagePhotoAlbum.aspx`, because it requires a query string that is sent by `NewPhotoAlbum.aspx`. Enter a new name for the photo album and click Insert. You're taken to `ManagePhotoAlbum.aspx` where you can enter new pictures. For now, all you can do is enter the description of the picture, the tooltip, and a fake URL of the image (just enter some text); you see later how to modify this and let a user upload real pictures to the website. Once you click the Insert button, a new item appears in the list, next to the insert controls. Add a few more items and you'll notice that the insert controls move to a row below the others, as shown in Figure 14-16, which shows the page in Firefox.

![](bbox=[0.11, 0.34, 0.86, 0.77])

FIGURE 14-16

16. Click the Delete button for an item and see how the item is removed from the list automatically.

17. If you're currently viewing the site in the Monochrome theme, use the drop-down list to switch to DarkGrey. Notice that this theme shows only two images per row instead of the three displayed by the Monochrome theme shown in Figure 14-16.

# How It Works

You started this exercise by attaching an `EntityDataSource` control to the `ListView` control. The `EntityDataSource` is configured to work with the `Pictures` entity set. As you saw earlier, each picture