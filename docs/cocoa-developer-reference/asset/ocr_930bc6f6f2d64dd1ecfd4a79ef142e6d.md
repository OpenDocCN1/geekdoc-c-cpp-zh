# Creating a class with NSCoder

I'll show you how to create a simple implementation of NSCoder and NSKeyedArchiver to save and load data in a form. The data is stored in a custom data model class. In a commercial application, multiple instances of the class could be used to store many forms. In this example, you'll concentrate on the code that saves and loads a single instance, using a single file with a fixed name. The code writes data from the form UI before saving the values. When the data is reloaded, the code creates a new data instance with the saved values, and copies them back to the form for display and editing.

> > **TIP**
> >
> > If you want to experiment with saving and loading multiple files, you can combine this project with the sample code for save/open panes in Chapter 10.

The project nib is shown in Figure 12.5. It uses an NSForm object to store three text strings, one of which is interpreted as an integer. An associated NSTextView object provides a free text field for notes. The NSForm and NSTextView are linked to outlets in the App Delegate. Two buttons trigger disk save and load actions.

**Figure 12.5**

The application nib file uses an NSForm, which is simply an array of text fields, accessed by index.

![](bbox=[0.225, 0.55, 0.76, 0.823])