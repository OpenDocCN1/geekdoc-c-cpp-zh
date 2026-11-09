Now, let’s put this instant bookshelf aside; we’ll start again from the data model and add the controller and view by hand. This will help you understand the various layers involved in a Core Data application.

# 22.3 The Managed Object Context

Go back to a fresh copy of the project, and let’s pick it up after you have created the data model with a single entity named PragBook that contains the two required string attributes named title and author. Open your nib file.

Add an array controller to the nib’s Document window. Use the Identity inspector to set the name of the array controller to BookController. Note that we are changing the name but not the class. We need to make only two small changes to set up the array controller.

First, open the Attributes inspector for the BookController. This time set the mode to Entity, and type in *PragBook* for the entity name.

![](bbox=[0.279, 0.44, 0.635, 0.649])

Next, open the Bindings inspector for the array controller. Way down at the bottom under the “Parameters” heading, open the disclosure triangle for the Managed Object Context. I’ll tell you what to set, and then I’ll explain what you’ve done.

Select the “Bind to” checkbox, and select CDBookshelf_AppDelegate from the drop-down list. You’ll leave the Controller Key and Value Transformer entries blank. Set Model Key Path to managedObjectContext.