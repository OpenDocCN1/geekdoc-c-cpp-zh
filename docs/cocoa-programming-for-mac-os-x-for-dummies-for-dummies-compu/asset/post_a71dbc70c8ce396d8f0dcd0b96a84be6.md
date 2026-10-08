
In addition to the new look, the **textured** property also changes the behavior of windows that have the property set. Whereas a non-textured window permits dragging from its title bar, you can drag textured windows by clicking and dragging anywhere in the window that isn't within the bounds of a control.

The first time you see the cool metallic look of the textured window, you'll be tempted to make the windows in every application with this style. After all, Apple does with many of its applications (such as iTunes and iPhoto).

![](img/ea40cad434a338535474e82c1a6ace20_176_0.png)

Before you start giving every window in sight a textured look, keep in mind that the Apple guidelines recommend that you use a textured window only when hardware is involved. This explains why you see it in many Apple applications, such as iMovie and iPhoto, which use hardware in one way or another. Although textured windows look tempting, try to use them only when necessary. Your users will thank you.

## Sizing up your windows

When you want to know the size of a window in code, use the frame method in the same way that you did earlier in this chapter. It gives you access to the window's position and size. To alter the size of a window in code, use the setFrame method. You can use the following code to resize a window to half its current width:

```c
- (IBAction)halfAsWide: (id) sender
{
    CGRect theFrame = [theWindow frame];
    theFrame.size.width = theFrame.size.width/2;
    [theWindow setFrame:theFrame display:YES];
}
```

If you want to zoom a window without forcing the user to click the zoom button on that window, all you have to do is call the window's zoom method.

```c
[theWindow zoom];
```

## Setting a window's title

Sometimes you'll want to change the title that appears in the title bar of a window. This is an easy task to perform with the setTitle method:

```c
[theWindow setTitle:@"My New Window Title"];
```

![](img/ea40cad434a338535474e82c1a6ace20_176_1.png)

Of course, you can also set the title of the window in the Inspector window of Interface Builder.

If the window title is the name of a document, use the `setTitleWithRepresentedFilename` method instead of `setTitle`. This method converts from a file path to a window title suitable for viewing:

```c
[theWindow setTitleWithRepresentedFilename:theFileName];
```

## Windows that you can see through

Cocoa windows have an alpha setting that enables you to set the translucency of a window. To see this magic in action, use the `setAlpha` method of `NSWindow`, passing it a value between 0.0 and 1.0. A value of 1.0 means that a window is fully visible; a value of 0.0 displays a window that’s completely transparent. This line of code makes a window 50-percent transparent:

```c
[theWindow setAlphaValue:0.5];
```

Figure 8-4 shows the difference between a window with `setAlpha` values of 0.5 and 1.0.

![](img/ea40cad434a338535474e82c1a6ace20_177_0.png)

## Beneath the Sheets

Besides the run-of-the-mill windows that you've used so far, Cocoa offers a special animated window — a sheet. A sheet is sort of a parasitic window, in that it needs a host, or a parent, from which to spring. Because its functionality is directly connected to another window, it appears from out of the blue at the top of its parent window, as shown in Figure 8-5. You're probably already familiar with sheets because many common applications use them — often when working with files.

Besides looking neat when they open, sheets also serve a useful purpose. Because they're attached to a parent window, they indicate a specific scope for a task: that of the parent window. In other words, if a sheet appears, you can be certain that any actions you perform in that sheet are pertinent to the parent window when the sheet closes. This is a subtle, but important, distinction.

![](img/ea40cad434a338535474e82c1a6ace20_178_0.png)

A sheet behaves in a particular manner — modally: it takes over a window and doesn't let the user perform any other action in the parent window until you dismiss it. Usually the user has to make some kind of decision before the sheet can be dismissed.

Implementing sheets takes some special preparation. To see how they work, launch Xcode and create a new Cocoa application. In the project window, double-click MainMenu.xib to open the interface in Interface Builder and then perform the following steps to add a sheet to your project:

- 1. Drag a panel from the Library (as shown in Figure 8-6) to your MainMenu.xib file window.
- 2. Change the panel settings. Open the Inspector window by choosing Tools->Inspector and deselect all the Style and Controls settings for the new panel, as shown in Figure 8-7. Also change the new Panel’s title to Sheet.
- 3. Open the default window in the project (named Window) and add a push button to the window; then, open the new panel from Step 1 and add a push button to it too.

At runtime, the button in the default window causes the panel to open as a sheet. The button in the sheet causes the sheet to close. Figure 8-8 shows the buttons as they appear in their respective windows.

![](img/ea40cad434a338535474e82c1a6ace20_179_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_180_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_180_1.png)

- 4. **Add a new object to the project.**  
  Drag an object class from the Library to the XIB window (as shown in Figure 8-9) and name it MySheetController. If you have problems locating the object class in the Library, search for it via the search field at the bottom of the Library window.
- 5. **Add outlets and actions to the object.**  
  Press ⌘+6 to open the Identity Inspector and add two outlets to the `MySheetController` class in the Class Outlets section of the Identity Inspector. To follow along with the example, name the two outlets `theWindow` and `theSheet`, respectively. Likewise, add two actions to the `MySheetController` class and rename the actions as `openSheet` and `closeSheet`. Figure 8-10 demonstrates what the Inspector window looks like.
- 6. **Connect the outlets and actions:**
  - a. *Control-drag from the MySheetController instance to the main window and connect it to the theWindow outlet.*
  - b. *Control-drag from the MySheetController instance to the panel in MainMenu.xib and connect it to the theSheet outlet.*
  - c. *Control-drag from the button in the main window to the MySheet Controller instance and connect it to the openSheet action.*
  - d. *Control-drag from the button in the Sheet panel to the MySheet Controller instance and connect it to the closeSheet action.*

![](img/ea40cad434a338535474e82c1a6ace20_181_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_182_0.png)

**Figure 8-10:**
Add outlets and actions to the controller.

- 7. **Create the class files.**
  - a. *Click MySheetController in the project window, choose Classes->Write Files, and save as MySheetController.*
  - b. *Make sure that the Create .h file check box is selected, as shown in Figure 8-11.*
  - c. *Click the Save button.*

![](img/ea40cad434a338535474e82c1a6ace20_182_1.png)

**Figure 8-11:**
Writing class files.

- 8. **Add the new files to the Xcode project.**  
  When you write the files for MySheetController, Interface Builder asks whether you want to add the files to the current Xcode project (see Figure 8-12). Toggle the check box for the desired project and click the Add button.
- 9. **Exit Interface Builder and return to Xcode where you find the new files.**

![](img/ea40cad434a338535474e82c1a6ace20_183_0.png)

**Figure 8-12:** Add the new class files to the Xcode project.

- 10. **Tweak the header.**  
  Change the interface definition by adding **NSObject** in the MySheetController.h file like this (the changed line is shown in boldface):

```c
#import <Cocoa/Cocoa.h>

@interface MySheetController : NSObject {
IBOutlet id theSheet;
IBOutlet id theWindow;
}
- (IBAction)closeSheet: (id) sender;
- (IBAction)openSheet: (id) sender;
@end
```

- 11. **Change the MySheetController.m file.**  
  The file looks like this (changed lines are shown in boldface):

```c
#import "MySheetController.h"

@implementation MySheetController

- (IBAction)closeSheet: (id) sender
{
[theSheet orderOut:nil];
[NSApp endSheet:theSheet];
}

- (IBAction)openSheet: (id) sender
```
