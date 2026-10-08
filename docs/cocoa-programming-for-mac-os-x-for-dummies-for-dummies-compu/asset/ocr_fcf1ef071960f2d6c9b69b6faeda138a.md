+   c. Connect the three new actions to the buttons in MenuWindow by Control-dragging from each button to the MyWindowController instance and then click Connect in the Inspector window to connect each action.

d. Connect the two window-related outlets to their corresponding windows: Control-drag from the MyWindowController instance to each window in the MainMenu.xib file window and then click Connect in the Inspector window to connect to the appropriate outlet.

e. Connect the theShowButton outlet to the top button in the MenuWindow.

6. Double-click the MyWindowController instance, choose Classes': Create Files for MyWindowController, and add the header and implementation files for the instance.

7. Return to Xcode and add this code to the MyWindowController.m file to implement the functionality of the three buttons:

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
```