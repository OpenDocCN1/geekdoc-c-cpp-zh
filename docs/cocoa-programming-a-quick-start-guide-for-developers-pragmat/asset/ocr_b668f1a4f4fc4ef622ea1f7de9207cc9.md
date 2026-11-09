Open your data model in Xcode. Select the Chapter entity, and add a new attribute named chapterNumber of type Integer 16. Save your work, and head to your nib.

In Interface Builder, add a second column to the table in the Chapters area. Rearrange the two columns so that the new column is on the left and is fairly narrow, with only # as the column’s title. Bind the column’s value to the Chapter Controller with the Controller Key setting of arrangedObjects and the Model Key Path setting of chapterNumber.

We have a small adjustment to make. The column expects to get input as an NSNumber, but when you type into the available field, it will be read as an NSString. To fix this, grab a number formatter from the Library, and drop it on the table cell. Use the Attributes inspector to set the number formatter to support a Decimal style with a maximum of 0 fraction digits. Your formatter should be set to support Mac OS X 10.4+ Custom. You’ll know that you have this set up if you see “123” where you used to see “Text Cell.”

![](bbox=[0.301, 0.437, 0.613, 0.499])

Now we’ll set both columns to sort on the chapter number. Select the first column, and open the Attributes inspector. Set Sort Key to chapterNumber, and set Selector to compare:. Do the same in the second column—make sure that you are still sorting on chapterNumber.

Click Build & Run. Enter the chapter numbers and titles for a book. If the chapters get out of order, you can reorder the table by clicking the title bar of either column. I’m still not happy with this behavior. I’d like to be able to start up the application and have the Chapters table sorted by default. Unfortunately, we’re going to need just a little bit of code to make that work so it will have to wait.

Before we move on, I want you to pause and take a look back at how far we’ve come in this chapter without printing any code. We have an application that can persist its data on disk and allow the user to create and modify information on books, authors, and chapters.^11^ Up next we’ll let the user filter which books are displayed.

11. Compare your version with CDBookshelf4 in the code download.