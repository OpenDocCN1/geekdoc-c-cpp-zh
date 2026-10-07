# CHAPTER 11: Storing Information

# 257

Change the text of each of the two columns in the Table View. Double click on the column header and type Title in the first column and Price in the second column. Your window should now now look something like Figure 11–14.

![](bbox=[0.137, 0.143, 0.663, 0.403])

Figure 11–14. The window layout.

We now have a nice looking window, but none of the controls can do anything yet. In order to make the objects have a purpose, we will need to bind them to something.

> NOTE: Cocoa Bindings is a way to keep your views synchronized with your controller. They help to reduce the amount of code required for you to write.

To connect an object to a controller, you simple have to control click on an item and then drag it to the item you will connect it to. Once you drag it to the item, you will be given a menu of the possible outlets available.

+   1. To start, control-click on your Array Controller and drag it to the table view. A little pop over window will appear with only one outlet selected. Select content. You are telling the table view that it will display the contents of the array controller. See Figure 11–15.