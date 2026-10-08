+   7. Create the files for the FileInfoController class:
	a. In the XIB project window, click the FileInfoController class.
	b. Choose File→Write Class Files to create the files for FileInfoController and to add them to the Xcode project.
8. In Xcode, assign an NSObject superclass to the FileInfoController.h file.

Change this line:

```
@interface FileInfoController :/* Specify a superclass (eg: NSObject or NSView) */{
```

to this:

```
@interface FileInfoController : NSObject {
```

# Open sesame . . . er, panel

When you have the interface built, you can add some code in Xcode to make the interface functional. Don’t forget about the goal of this project — to select a file and report information about it. To display information about a specific file or folder, you use Cocoa’s OpenPanel class. With the OpenPanel class, you can display an Open dialog that allows a user to select a file or folder.

When you use an OpenPanel, you typically follow four basic steps:

+   1. Create an instance of OpenPanel.
2. Set the attributes of the OpenPanel instance.
3. Display the OpenPanel for the user and wait for the user to do something with it: Select a file and click OK or cancel the operation.
4. Perform a function with the file that the user selected.

To see how OpenPanel works in Cocoa, perform these four steps.

+   1. Create an OpenPanel instance.
You do so in the same way that you create other objects in Cocoa:
NSOpenPanel *openPanel = [NSOpenPanel openPanel];
2. Alter the attributes of OpenPanel by calling one or more of its methods.
For example, to change the title of OpenPanel, use the setTitle method.
[openPanel setTitle:@"Choose a File or Folder"];