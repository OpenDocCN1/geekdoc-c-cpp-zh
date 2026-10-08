
The `orderOut` method of the `NSWindow` class hides a window from view. The window still exists in memory; it just isn't visible anymore. To find out whether a window is visible, you can check the return value of the `isVisible` method:

```
- (IBAction)hideWindow: (id) sender
{
    if ([theWindow  isVisible])
        [theWindow  orderOut:sender];
}
```

To make the window reappear, use the `orderFront` method, but first check to see if the window is already visible:

```
- (IBAction)showWindow: (id) sender
{
    if (![theWindow  isVisible])
        [theWindow  orderFront:sender];
}
```

If you want a specific window to appear on the screen and act as the main window, thus intercepting keystrokes, use the `makeKeyAndOrderFront` method. You might use this method in the `awakeFromNib` method to force a main window to the foreground:

```
- (void)awakeFromNib {
    [theWindow  makeKeyAndOrderFront:nil];
}
```

## Positioning windows

Positioning windows is another important task that you'll need to perform. Before you go bossing around a window, you first need to find out its current position on the screen. Use the `frame` method of the `NSWindow` class to discover the origin and size of a window. The `frame` method returns an `NSRect` structure, which contains `NSPoint` and `NSSize` elements that describe the window's origin and size, respectively:

```
typedef  struct  _NSRect  {
    NSPoint  origin;
    NSSize  size;
} NSRect;
```

When you know the origin of a window, it's a trivial matter to reposition it. First, define an origin to your liking and then call the `setFrameOrigin` method to apply the new origin. This code moves a window 20 pixels to the right of its current position:

```
- (IBAction)moveRight: (id) sender
{
    NSRect theFrame = [theWindow frame];
    NSPoint theOrigin = theFrame.origin;
    theOrigin.x = theOrigin.x + 20;
    [theWindow setFrameOrigin: theOrigin];
}
```

To position a window in the middle of the screen, use the handy center method. This code centers a window on the screen:

```
- (IBAction)centerWindow: (id) sender
{
    [theWindow center];
}
```

## Keeping track of windows

Most Cocoa applications have a Window menu to help users keep track of open windows. Normally, this menu lists the open document windows. (You probably wouldn't display, say, a toolbar window in the Window menu.) The great thing about the Window menu is that Cocoa takes care of it for you automatically. If your window has the following properties, Cocoa automatically adds it to the Window menu:

- Has a title bar
- Is resizable
- Can become the main window

You can exclude a window from the Window menu by altering any one of these properties.

> If you have a window that obeys each of these rules but you still want it left out of the Window menu, use the `setExcludedFromWindowsMenu:` method. The `awakeFromNib` method is a good place to use this call because the method takes effect when your application launches and the window resources is loaded from the NIB file.

```
- (void)awakeFromNib {
    [theWindow setExcludedFromWindowsMenu:nil];
}
```

# Putting windows to work for you

To see how these window features work, do the following:

1. Launch Xcode and create a new Cocoa application project:
   1. Double-click the Xcode icon in the Finder to launch it.
   2. Choose File→New Project.
   3. In the window that appears, select Cocoa Application and click OK.
2. Create a new window in the MainMenu.xib file.
   1. Double-click the MainMenu.xib file in the Resources Group of your project to open the file in Interface Builder.
   2. In the XIB project window, double-click to open the default window if it’s not open already.
   3. Press ⌘+I to open the Attributes window and name the window MenuWindow.
3. Add three buttons to MenuWindow, as shown in Figure 8-1, and label them Hide Window, Move Left, and Center Window, respectively.

For more information on adding buttons, see Chapter 2.

![](img/ea40cad434a338535474e82c1a6ace20_172_0.png)

4. Add an object to the project:
   1. Drag an Object item from the Library window to the project window.
   2. Name the object MyWindowController.
5. Double-click the new MyWindowController instance and add outlets and actions to the instance in the Inspector window.
   1. Add these outlets: theMenuWindow, theShowButton, and theWindow.
   2. Add these actions: centerWindow, moveRight, and showWindow.

For details on adding outlets and actions, see Chapter 2.

6. Connect the three new actions to the buttons in MenuWindow by Control-dragging from each button to the MyWindowController instance and then click Connect in the Inspector window to connect each action.
7. Connect the two window-related outlets to their corresponding windows: Control-drag from the MyWindowController instance to each window in the MainMenu.xib file window and then click Connect in the Inspector window to connect to the appropriate outlet.
8. Connect the theShowButton outlet to the top button in the MenuWindow.
9. Double-click the MyWindowController instance, choose Classes': Create Files for MyWindowController, and add the header and implementation files for the instance.
10. Return to Xcode and add this code to the MyWindowController.m file to implement the functionality of the three buttons:

```
#import "MyWindowController.h"
@implementation MyWindowController

- (IBAction)centerWindow: (id)sender
{
	[theWindow center];
}

- (IBAction)moveRight: (id)sender
{
	NSRect theFrame = [theWindow frame];
	NSPoint theOrigin = theFrame.origin;
	theOrigin.x = theOrigin.x + 20;
	[theWindow setFrameOrigin:theOrigin];
}

- (IBAction)showWindow: (id)sender
{
	if ([theWindow isVisible])
	{
		[theWindow orderOut:sender];
		[theShowButton setTitle:@"Show Window"];
	}
	else
	{
		[theWindow orderFront:sender];
		[theShowButton setTitle:@"Hide Window"];
	}
}

- (void)awakeFromNib {
	[theWindow makeKeyAndOrderFront:nil];
	[theMenuWindow makeKeyAndOrderFront:nil];
}

@end
```

11. **Choose Build** **⌘B** and Go to test the project.

## Changing the Appearance of Windows

Beauty may be only skin deep, but when it comes to using your application, an attractive interface is mandatory. In this section, you explore some of the possible window settings for nice-looking interfaces. These features also enhance the functionality of your applications, so you have some brawn to go with that beauty.

### Using different windows for different tasks

The standard Mac window style has a gray background, as shown in Figure 8-2. However, this isn’t the only appearance a window can have. Apple has strict guidelines about how windows should look, which are outlined in the famous Human Interface Guidelines document available online at developer.apple.com. The basic gist of the Apple guidelines is that windows should look the same for the same tasks. A document window looks one way. A toolbar window looks a different way. A window in a one-window application should look yet another way. Always follow Apple’s guidelines when designing interface windows because your users expect windows to look and behave identically across applications.

Open the default XIB file from a Cocoa application in Interface Builder. You can change the appearance of a window by following these steps:

1. **Open the default window in Interface Builder.**
   Double-click it in the XIB project window.
2. **Press ⌘+1 to open the Inspector window.**
   In the Attributes section of the Inspector window, you find the Textured check box for the window.

![](img/ea40cad434a338535474e82c1a6ace20_175_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_175_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_175_2.png)

3. Toggle the Textured check box to change the appearance of the window.

If the Inspector doesn't display the textured attribute, click the window's toolbar to display the Inspector appropriate to the window.

The window now has a textured appearance (see Figure 8-3).

![](img/ea40cad434a338535474e82c1a6ace20_175_3.png)

![](img/ea40cad434a338535474e82c1a6ace20_175_4.png)
