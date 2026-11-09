at the lower left of the Entity area. Type *PragBook* in the Name field.¹ The bottom of the window holds a graphical representation of your data model. You should see *PragBook* with no attributes or relationships.

Now let’s add attributes for the book’s title and author’s name. With *PragBook* selected in the entity view, click the + button at the bottom of the properties view. A pop-up list appears with the options Add Attribute, Add Fetched Property, Add Relationship, and Add Fetch Request.

Choose Add Attribute, or use the menu item Design > Data Model > Add Attribute or the keyboard shortcut ^ ⌘ A. Name the attribute `title`, and configure it so it is not optional and so that it is of type `String`. Because this attribute is not optional, you should add a default value like “Book’s title.” Add another attribute named `author`, and also set it to not be optional and to be of type `String`. Your data model should look like this:

![](bbox=[0.386, 0.379, 0.548, 0.471])

We’re done with the data model for now. We’ll do the rest of our work in the nib file.

# ## 22.2 Using the Core Data Widget

Make a copy of your project because we’re going to finish the application in two different ways. First we’ll use the widget that Apple has provided that will create both the controller and the view at the same time.

Double-click `MainMenu.xib` to open the nib in IB. Drag a `Core Data Entity` from the Library onto your `Window` object. A wizard will allow you to select the *PragBook* entity. To do so, you first select the current Xcode project, and then you select the data model contained in the project. Projects can contain more than one data model. In our case, there is only one. Within the data model there are usually multiple entities.

1. You need to tab out of the Name field for *PragBook* to appear in the entity view as well.