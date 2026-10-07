# CHAPTER 10: Creating User Interfaces

```
// ViewController.h
// RandomNumber
//
// Created by Gary Bennett on 10/6/11.
// Copyright (c) 2011 xcelME. All rights reserved.
//
#import <UIKit/UIKit.h>
@interface ViewController : ViewController
{
    @IBOutlet UILabel *randomNumber;
}
@end
```

![](bbox=[0.137, 0.065, 0.365, 0.335])

Figure 10–19. Outlet instance variable code generated and connected to the Label Object.

As a reminder, outlets, outlets (pointers) are declared in our object's interface file and connected to specific instance variables.

There is also a declaration that may be new to you an IOBOutlet, commonly referred to as an outlet. **Outlets** signal your controller that this instance variable is a pointer to another object that is set up in Interface Builder. IOButlet will enable Interface Builder to see the outlet and enable you to connect the variable to the object in Interface Builder.

Using the analogy of an electrical wall outlet, these instance variable outlets are connected to objects. Using Interface Builder, we can connect these instance variables to the appropriate object.

# Connecting Actions and Objects

User interface object events, also known as Actions, trigger methods.

Now we need to connect the object actions to the buttons.

+   1. Control-Drag from the "Seed Random Number Generator" button to below the last curly bracket and drop. Complete the pop-up as indicated in Figure 10–20 and **press the connect button**. Make sure you change the connection as an Action and not an Outlet.