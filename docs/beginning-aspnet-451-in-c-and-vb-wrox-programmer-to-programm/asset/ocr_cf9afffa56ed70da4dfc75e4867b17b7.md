# EXERCISES

+   1. Imagine you have a page in the Reviews folder MostRecent.aspx. This page should show the 10 most recently added reviews. What would your LINQ query look like if you only wanted to show the review's Title property and the genre of it belongs to? You should use the Take method to limit the result to 10. If you're having trouble writing the code to get the last reviews, look at the section titled "First, FirstOrDefault, Last, and LastOrDefault," which shows you how to get the last review in the database.

+   2. What is the major benefit of the ListView control over other data controls like GridView and Repeater?

+   3. Currently the Default.aspx page from the PhotoAlbums folder just shows the thumbnails of the pictures. What would you need to do to display the full-size picture on its own page using a LINQ query?

+   4. When you delete a picture from the ListView on the Photo Album page, only the database row is deleted, but the image on disk is left untouched. Make use of the static SystemIO.File.Delete method to delete the item from disk when the picture gets deleted.

+   5. Currently, the AllByGenre.aspx page displays the title of the genre, regardless of whether it has any reviews attached to it. How can you hide genres that don't have reviews? Make use of the Count method on the Reviews collection to solve this question.

You can find answers to these exercises in Appendix A.