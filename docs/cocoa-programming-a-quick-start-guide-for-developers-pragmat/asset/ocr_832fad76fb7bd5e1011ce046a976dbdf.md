# ## 22.8 Managing Dependencies

To let your users add chapters to a book, start by following the same steps we followed for the Book Controller. Drag an array controller from the Library to your Document window. In the Identity inspector, change its name to Chapter Controller. In the Attributes inspector, change the mode to Entity and Entity Name to Chapter. This time leave Prepares Content unselected. In the Bindings inspector, bind Managed Object Context to the CDBookshelf_AppDelegate with the Model Key Path setting of managedObjectContext.

Now we’ll do something dramatically different. Each book has its own set of chapters. The Chapter Controller will manage the chapters for whatever book is currently selected. As you’ll soon see, if you switch books, the chapters should switch as well. In the Bindings inspector, you’ll need to bind Content Set for the Chapter Controller to the appropriate keypath in the Book Controller. To do this, Controller Key should be selection, and Model Key Path should be chapters.

![](bbox=[0.295, 0.438, 0.607, 0.557])

All that remains is to wire up the view. If you created the chapter table and buttons by duplicating the book table, the elements are probably connected to the BookController. Let’s move everything to the Chapter-Controller.

Select the + button in the Chapter section. In the Connections inspector, connect the selector to the Chapter Controller. When you get a pop-up of available connections, choose add:. Similarly, connect the - button’s selector to the Chapter Controller’s remove: method.

We also need to set the bindings on the buttons. Select the + button again, and use the Bindings inspector to bind Enabled to the Chapter Controller with Controller Key canAdd. Similarly, bind Enabled for the - button with the Controller Key canRemove.