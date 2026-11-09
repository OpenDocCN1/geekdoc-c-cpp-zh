We have another option for the chapters relationship. When we delete the book, we could delete all of the chapters for that book as well. In other words, we want the delete to cascade down. We are still enforcing the idea that it doesn’t make sense for the chapters to survive if the book doesn’t—we’ve just chosen a different result.

So, set the Delete rule for chapters to Cascade. The inverse relationship book should have the Delete rule Nullify. When we delete a chapter, we don’t delete the book it belongs to, but we make sure the book no longer has a reference to this deleted chapter. Similarly, the rule for authors and books should be Nullify.⁶

# 22.7 Updating the View

By this point, you should be comfortable using Interface Builder without a lot of direction. Open your nib file, select your table view, and reduce the number of columns to one. Select all of the components inside your content view, and choose Layout > Embed Objects In > Box. Change the box’s title to Prag Books. Select that box, paste it twice, and customize the contents to look like this:

![](bbox=[0.136, 0.491, 0.776, 0.829])

The contents of the chapter and authors boxes need to depend on which book is selected. That’s a job for the controller layer.

6. You can compare your work with the data model in CDBookshelf2 in the code download.