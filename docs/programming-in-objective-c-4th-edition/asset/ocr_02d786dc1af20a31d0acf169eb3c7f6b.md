defined as nothing in the UIKit header file UINibDeclarations.h. (That is, it is literally replaced by nothing in the source file by the preprocessor). However, it's needed because Xcode looks for IBOutlets when it reads its header file to determine which of your variables can be used as outlets and can be connected to the appropriate UI elements in the interface.

The click1 method is defined to return a value of type IBAction. (This is defined as void in the UINibDeclarations.h header file). Like IBOut, Xcode uses this identifier when it examines your header file to identify methods that can be used as actions.

Now it's time to modify the corresponding iPhone_1ViewController.m implementation file for your class. Here you synthesize the accessor methods for your display property.

Now edit your implementation file and add the lines as shown in Program 21.1 (note that we're not showing methods that Xcode placed in your implementation file that won't be modifying).

# Program 21.1. iPhone_1ViewController.m

```
@import "iPhone_1ViewController.h"

@implementation iPhone_1ViewController

@synthesize display;

-(IBAction) click1
{
    display.text = @"1";
}

// Other methods inserted by Xcode not shown
```