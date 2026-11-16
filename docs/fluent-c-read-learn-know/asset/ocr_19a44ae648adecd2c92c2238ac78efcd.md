# CLASS PROPERTIES

Like any Visual Studio Designer, the Class Diagram Designer Properties window shows you the properties of the selected objects. Unfortunately, in Visual Studio 2010, not all of these properties can be set in the Designer itself, but changes you make in code will be reflected in the Properties window.

Properties that are grey in the Properties window can only be changed in code. We'll talk about most of these when we look at the code for declaring a class.

![](bbox=[0.32, 0.26, 0.69, 0.71])

We'll talk about Access modifiers in just a minute.

New Member Location define the file where members will be defined. It isn't retroactive—it doesn't change existing member definitions to the file you specify here—but any new definitions will be placed in the file you specify here.

You can change the name of the class here, but it won't change the name of the code file.

Inheritance Modifiers control whether and how new classes can inherit from this class. We'll discuss them in Chapter 12.

The definition of a class can be spread across multiple code files. As we'll see, that's really handy when you're working with Designers, but it's not something you'll do often otherwise.

If you fill in the XML Documentation properties here, Visual Studio will add them to the class file so that they'll be available to Intellisense.