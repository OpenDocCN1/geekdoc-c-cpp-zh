+   4. With some minor coding trickery, it reads the artist key from each album. If the artist name matches the name box, it inserts the album name into the `searchReturnArray`.
+   5. It assigns the array to itself to trigger a KVO update.
+   6. The array controller in the nib notices the updates, and sends them to a column in the Albums table view to display them.
+   7. The list appears.

**Figure 14.16**

Creating an improved interface and adding a table view to display a summary list of albums for each artist, with a new array controller to bind the search results to the table

![](bbox=[0.18, 0.383, 0.79, 0.773])