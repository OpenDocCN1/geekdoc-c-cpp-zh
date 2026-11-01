16. Save all your changes and then request `Default.aspx` from the `PhotoAlbums` folder in your browser. Choose a photo album from the drop-down list and the page reloads, showing you the relevant pictures in the photo album.

> **COMMON MISTAKES** If nothing happens when you choose a new item from the drop-down list, go back to VS and ensure you set `autoPostBack` on the `DropDownList` control to True.
> 
> If you don't have any pictures in a photo album, or not enough to fill an entire page, choose New Album from the Gig Pics menu, create a new photo album, and add at least four images to it. Then click the Gig Pics menu item and choose your new photo album from the drop-down list. Note that there is now a paging user interface, enabling you to move forward and backward through the list of pictures in the photo album using the First, Previous, Next, and Last buttons visible at the bottom of the screen in Figure 14-22. Because of the AJAX panel you added, the selection and paging operations now occur completely flicker-free.

> **NOTE** Your first few albums will end up broken. That's because you didn't supply images when you created them. You can delete the albums (and their associated picture rows) from the database if you want to clean up a bit. In Chapter 16 you develop functionality to delete images from the `Default.aspx` page in the `PhotoAlbums` folder.

![](bbox=[0.13, 0.75, 0.77, 0.88])

FIGURE 14-22