You will see that the file starts out including the Core Data framework. This allows Core Data to manage your information. Further down, you will see the three attributes you created.

# Managed Object Context

We have created a managed object called Book. The nice thing with Xcode is that it will generate the necessary code to manage these new data objects. In Core Data, every managed object should exist within a managed object context. The context is responsible for tracking changes to objects, carrying out undo operations, and writing the data to the database. In this example, we will not have to write code to create or manage the object context, but as you explore using Core Data in your projects, you will need to be aware of it. For now, the base functionality of what is provided for the generated classes will work fine.

# Setting Up the Interface

The following steps will assist you in setting up your interface:

+   1. In the Resources folder in your project, you should have a MainMenu.xib. Double-click on this file and Interface Builder should open in a new window. On the left-hand side of this window, you should have a list of current objects. If you do not have this window, click on the little arrow at the bottom left-hand side of the window. Click on the Window object. Your window will be shown on the right-hand side of the screen. See Figure 11–10.