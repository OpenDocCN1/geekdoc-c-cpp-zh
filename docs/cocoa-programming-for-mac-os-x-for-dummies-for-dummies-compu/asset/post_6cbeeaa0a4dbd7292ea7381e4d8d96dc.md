
### Chapter 17: Document-Based Applications

5. Press ⌘+R to build and run the project.

When the project launches, you see a single document window, as shown in Figure 17-3.

![](img/ea40cad434a338535474e82c1a6ace20_340_0.png)

6. Choose File>New to create a new document.

The application creates a new document and adds it to the Window menu. You can continue creating new windows as long as you want.

Note that the application has many other features, such as a full suite of menus and an About Panel, which you had to add manually to your project in Chapter 5. At this point, however, you can’t save or open a document because you haven’t implemented that functionality yet.

#### Building the Interface for a Document-Based Project

You need to make a decision about what kind of document-based application you want to create. It could be a word processor, a graphics application, or a checkbook program. In this chapter, you create a simple text editor.

Follow these steps:

1. Return to Xcode and double-click the MyDocument.nib file to open it in Interface Builder. A generic document opens (refer to Figure 17-3).

2. Design the interface for this project:
   - Delete the text label that stands at the center of your document window.
   - Add an NSTextView control from the Library window to the document window in MyDocument.nib.
   - Resize the NSTextView to your liking.

Figure 17-4 shows the new interface.

![](img/ea40cad434a338535474e82c1a6ace20_341_0.png)

Figure 17-4: The text editor interface.

3. Add an outlet to the `MyDocument` class.
   a. Select File's Owner in the project window and press ⌘+6 to open the Identity Inspector, labeled My Document Identity.
   b. Add a new outlet to the Identity Inspector and name it `myTextView`, as shown in Figure 17-5.

You use this outlet to get and set text in the `NSTextView` of the document.

![](img/ea40cad434a338535474e82c1a6ace20_342_0.png)

4. Connect the `myTextView` outlet to the `NSTextView` in the interface by Control+dragging from the File's Owner icon to the `NSTextView` in your document window.

![](img/ea40cad434a338535474e82c1a6ace20_342_1.png)

Make sure that you connect to the `NSTextView` and not its Scroll View parent. The `NSTextView` control is embedded within an `NSScrollView` control (which handles the scrolling, as you might have guessed). You may have to drag toward the top of the text view for it to become highlighted.

Figure 17-6 shows the outlet connection.

![](img/ea40cad434a338535474e82c1a6ace20_343_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_343_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_343_2.png)

5. Choose File>Save to save the NIB file and then return to Xcode. The outlet is added to the MyDocument.h file.

6. Expand the **Target** group in the Groups & Files list and select the default application.

7. Click the Info button in the window's toolbar to open the **Target Info** window.

8. Click the **Properties** tab to display the list of document types in this application and click the + button at the bottom of the Info window.

9. Add rich text as a new document type that the application can use, as shown in **Figure 17-7**:
   a. In the *Extensions* box, type *rtf* (without quotation marks).
   b. Enter *text/rtf* in the *MIME Types* field.
   c. In the *OS Types* box, type “RTF” (this time use a double-tick mark, followed by *RTF*, a space, and another closing double-tick mark) in the *OS Types* field.
   d. Enter *MyDocument* in the *Class* field and choose *Binary* as the *Store Type*.

If you add an icon file (with the `.icns` extension) to your project and define it in the icon column, your application uses the custom icon when saving this file type. Chapter 5 details how to assign an icon to your application.

![](img/ea40cad434a338535474e82c1a6ace20_344_0.png)

Feel free to remove the default DocumentType entry by selecting it and pressing the Delete key.

![](img/ea40cad434a338535474e82c1a6ace20_344_1.png)

#### Adding the Code

Now that you’ve set up the interface and classes in Interface Builder and added the RTF document type in Xcode, you can add some code to your project. The MyDocument.h and MyDocument.m files were added to the document by default when you created the project. You need to add code to these two files to make the application work.

In Xcode, add an outlet and an NSData pointer to your MyDocument.h interface file by entering this code:

```objectivec
#import <Cocoa/Cocoa.h>

@interface MyDocument : NSDocument
{
    IBOutlet id myTextView;
    NSData *fileContents;
}
@end
```

The NSData object holds the contents of your rich text file. The IBOutlet is the outlet that you already added to File’s Owner in Interface Builder.

2. **Navigate to your MyDocument.m implementation file and change its code to read as follows:**

```objectivec
#import "MyDocument.h"

@implementation MyDocument
- (id)init
{
    self = [super init];
    if (self) {
        // Add your subclass-specific initialization here.
        // If an error occurs here, send a [self release] message and return nil.
    }
    return self;
}

- (NSString *)windowNibName
{
    return @"MyDocument";
}

- (void)windowControllerDidLoadNib:(NSWindowController *)aController
{
    [super windowControllerDidLoadNib:aController];
    [myTextView replaceCharactersInRange:NSMakeRange(0,[[myTextView string] length])
        withRTF:fileContents];
}

- (NSData *)dataOfType:(NSString *)typeName
  error:(NSError **)outError
{
    [fileContents release];
    fileContents = [[myTextView RTFFromRange:NSMakeRange(0,[[myTextView string] length])] retain];
    return fileContents;
}

- (BOOL)readFromData:(NSData *)data ofType:(NSString *)typeName error:(NSError **)outError
{
    fileContents = [data retain];
    return YES;
}

- (void)dealloc {
    [fileContents release];
    [super dealloc];
}

@end
```

The big changes in this file are in **dataOfType**, **readFromData**, and **windowControllerDidLoadNib**:

- The **dataOfType** method takes care of saving the file. The **dataOfType** method doesn't really have anything to do with files. Instead, it returns the data that the application should save to the file. The application actually takes care of the rest!
- The **readFromData** and **windowControllerDidLoadNib** methods handle the task of opening a rich text file. The **readFromData** method receives the incoming data from the file and lets the application know whether it's successful. Then the **windowControllerDidLoadNib** method takes care of displaying the text in the NSData instance named fileContents.

3. **Press ⌘+R to test your work.** You can open and save rich text files just like those created with TextEdit or Microsoft Word. When you open a file, your application displays its contents in a new window. Notice that the application's other menus work, too. You can close a window by pressing ⌘+W or even use the spell-check on a document.

The beauty of using a Cocoa document project is that Cocoa takes care of a lot of the work for you. You don't have to do much work to implement a large assortment of features. Besides making it easy on you, Cocoa makes it easier on your users. By using the default behaviors that Cocoa document-based apps provide you, your users will be familiar with their operation.

# Chapter 18: Cocoa Bindings

**In This Chapter**

- Understanding bindings
- Working on a project with bindings
- Using KVC and KVO to make your bindings work
- Adding bindings to an existing project

Whenever you create a Cocoa application the traditional way, you implement a Model class that manages data, an interface that users interact with, and a Controller class that ties the two together. This is all well and good, but Objective-C saves you from a substantial bit of coding and hassle by permitting you to bypass the Controller class altogether.

Bindings let you bridge items in your interface directly to data in your Model classes. This is handy because Objective-C handles the tasks of keeping your interface updated and, more importantly, you don’t have to. That means less coding work for you and less chance of creating bugs.

This chapter explains what bindings are and why you use them. Then, it describes some of the technology behind bindings (namely KVC and KVO). KVC and KVO are two complementary technologies that you can use to generically get and set the values of instance variables. Finally, you create a project that uses bindings instead of code to control an interface in your application.

![](img/ea40cad434a338535474e82c1a6ace20_348_0.png)

Bindings is an advanced topic that is also voluminous, and as such, you have to do some exploration on your own to master the wild and wooly world of bindings. This chapter only scratches the surface of what you can do with bindings. You can bind all sorts of elements in your interface to many different keys in your classes to affect how the application behaves when it runs.
