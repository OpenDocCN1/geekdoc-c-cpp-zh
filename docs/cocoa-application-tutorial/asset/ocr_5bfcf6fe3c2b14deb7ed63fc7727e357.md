# # Defining the View: Building the User Interface

Every application has a user interface. It can be a tedious and infuriating task to design user interfaces without a good program to help you. Interface Builder, an application supplied with Xcode, makes designing user interfaces simple, and so turns a tedious task into something easy.

This chapter teaches you how Interface Builder integrates with Cocoa. It guides you through building the user interface for your application. You learn where to locate the tools you need and how to use the features in Interface Builder to create the perfect user interface for your application.

# ## User Interface Elements and Interface Builder

Interface Builder is an application that helps you design the user interface and connect the different parts of your application. It contains a drag-and-drop interface for UI design, and an inspector that allows you to view and change the properties of the various objects in your design, as well as the connections between them.

# ### What Is a Nib File?

Every Cocoa application with a graphical user interface has at least one nib file. The main nib file is loaded automatically when an application launches. It contains the menu bar and generally at least one window along with various other objects. An application can have other nib files as well. Each nib file contains:

+   - **Archived objects.** Also known as “flattened” or “serialized” objects—meaning that the object has been encoded in such a way that it can be saved to disk and later restored in memory. Archived objects contain information such as their size, location, and position in the object hierarchy. At the top of the hierarchy of archived objects is the File’s Owner object, a proxy object that, at runtime, becomes the actual object that owns the nib file (typically the one that loaded the nib file from disk).
+   - **Images.** Image files that appear somewhere in your application’s interface, such as a button or image view.
+   - **Class references.** Interface Builder can store the details of Cocoa objects and objects that you place into static palettes, but it does not know how to archive instances of your custom classes because it doesn’t have access to their code. For these classes, Interface Builder stores a proxy object to which it attaches your custom class information.
+   - **Connection information.** Information about how objects within the class hierarchies are interconnected. When you save a document, information about the connections between the objects in the nib is archived along with the objects themselves.