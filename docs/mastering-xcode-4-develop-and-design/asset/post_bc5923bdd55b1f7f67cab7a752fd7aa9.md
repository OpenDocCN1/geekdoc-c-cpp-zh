
![](img/d4b18a89aece4a6ccac4cb886bdef5f7_70_0.png)

You’ll need to add some code to make the action do something interesting. Navigate to the `TestAppAppDelegate.m` file (the implementation file for the `TestAppAppDelegate` class), and scroll down to find the `-sayHello:` method. Edit it to look like the following:

```objective-c
- (IBAction)sayHello:(id)sender {
    [[NSAlert alertWithMessageText:@"Important Message"
                     defaultButton:@"Hello Yourself"
                   alternateButton:nil
                       otherButton:nil
         informativeTextWithFormat:@"Hello World"] runModal];
}
```

Click the Run button to build and run the application. Give your Say Hello button a test click to make sure it’s working. You should see something similar to **Figure 5.9**. When you’re satisfied, quit the application and navigate back to the `MainMenu.xib` file.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_71_0.png)

**FIGURE 5.10** TestApp showing its Hello World message in a text field

## ADDING A TEXT FIELD

Perhaps you believe modal dialog boxes are overused, so you’ll want to put that text into a text field in the application’s window. Find the Text Field control in the Object library, and drag it into your window. To communicate with the text field and set its string value to Hello World, you’ll need to create an outlet for it.

To add the outlet, drag a connection from the text field to the source code in the Assistant. This time, place the connection within the curly braces (because outlets are instance variables of a class). Choose the Outlet connection type, name it **textField**, and then press Return to finish adding the outlet.

Now that your code has a reference to the text field, you can change the action to display the message there rather than in a modal dialog box. Navigate back to the `-sayHello:` action in the `TestAppAppDelegate.m` file, and change it to look like the following:

```objective-c
- (IBAction)sayHello:(id)sender {
    [textField setStringValue:@"Hello World"];
}
```

Build and run the application, and verify everything is working. Your application should look something like **Figure 5.10**.

## LAYOUT

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_72_0.png)

**FIGURE 5.11** Improperly behaving layout

You’ve learned the basics of creating and wiring up a simple user interface. There’s one small problem, however. Run TestApp again if it isn’t running already, and try resizing the window. The controls stubbornly stay where they are, refusing to do something smart (**Figure 5.11**).

There are, as of the release of Mac OS X 10.7 Lion, two mechanisms through which you can define the sizing and positioning behavior of views: the original “springs and struts” and the new Autolayout feature.

> **NOTE:** Each of the two layout mechanisms has a well-defined API that allows you to use code to control layout behavior. Because this book focuses on Xcode and not Cocoa development, the coding topic will not be covered.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_0.png)

**FIGURE 5.13** Springs and struts deactivated in the Autosizing control

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_1.png)

**FIGURE 5.14** Overlapping controls

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_2.png)

**FIGURE 5.15** Selecting multiple controls

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_3.png)

**FIGURE 5.16** Centered controls

## CONSTRAINTS

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_0.png)

**FIGURE 5.18** Cut-off controls in a small window

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_1.png)

**FIGURE 5.19** Setting window size constraints

Run TestApp once again and play with the window size. Notice how the text field now grows and shrinks. And notice that if the window gets too small, the button is cut off and the field gets a little too narrow (Figure 5.18). This is a limitation of the springs and struts model: The only way to apply any kind of constraints is by setting a minimum size so things don’t get smooshed together or cut off.

The simplest fix is to set a minimum window size. Select the window, and in the Constraints section of the Size inspector, select the Minimum Size check box and set a reasonable minimum size (such as 200 by 150), as shown in Figure 5.19.

Now when you run TestApp and play with the sizing, the controls should more or less behave themselves. You may need to play with the minimum window size or the sizes of the text field and enclosing custom view to get it right.

## USING AUTOLAYOUT IN LION

As mentioned, Lion (Mac OS X 10.7) introduces a new layout mechanism called Autolayout. Although it certainly has vast improvements over springs and struts (and a nifty layout language all its own for use in code), its use is not compulsory on Lion or above. That is, the springs and struts mechanism will still work as it always has. In fact, you must turn on Autolayout for each Interface Builder document in which you intend to use it, otherwise springs and struts still rule. Correspondingly, Autolayout can only be used with applications that target OS X 10.7 and above.

> **NOTE:** You’ll need to be running Xcode version 4.1 or later to use the Autolayout features of the editor.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_2.png)

**FIGURE 5.20** The Interface Builder document's file settings

**FIGURE 5.21** The Mac OS X 10.7 upgrade prompt

## ACTIVATING AUTOLAYOUT

To activate Autolayout for `MainMenu.xib`, navigate to it and make sure the Utility area is visible with the File Inspector panel selected. Under the Interface Builder Document section (Figure 5.20), select the Use Autolayout check box.

You may be prompted to upgrade your project’s minimum deployment version to Mac OS X 10.7 if it’s set to a lower version, as in Figure 5.21. Click the Continue and Upgrade button to accept the upgrade.

> **NOTE:** Accepting the Autolayout upgrade and setting the minimum deployment version to 10.7 means your application will not run on versions of Mac OS X prior to 10.7. As mentioned, 10.7 is required for Autolayout.

## CONSTRAINTS

You’ll notice something different immediately. Figure 5.22 shows the new Constraints entries in Interface Builder’s Objects dock. Constraints are real objects, just like buttons and windows. They define the sizing and positioning behavior of the controls they constrain. Because they’re real objects, you can select, configure, or remove them in Interface Builder the same as you would a button or a window.

Figure 5.23 shows a vertical space constraint selected. This constraint manages the vertical space between the Say Hello button and the custom view’s top border. With Autolayout, dragging controls into a window or view and snapping them to the guides will automatically create the constraint that the system determined appropriate to maintain the best positioning.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_79_0.png)

**FIGURE 5.22** (top) Constraint objects added to the document

**FIGURE 5.23** (left) A vertical space constraint selected

To fix this (and explore adding constraints), select the custom view and choose Editor > Pin > Leading Space to Superview from the main menu. Select the custom view again and choose Editor > Pin > Trailing Space to Superview. Your window should look something like **Figure 5.25**.

If you run TestApp now, you’ll see that this didn’t quite fix things. Although the button stays the same distance from the field below it, and the custom view seems to be resizing (as evidenced by the text field’s left edge following along), nothing else seems to be behaving itself.

The fix for the text field is easy enough. By snapping the left and right edges to the blue guides inside the custom view (**Figure 5.26**), the appropriate constraints are created for you automatically.

Figure 5.27 shows the constraints that were added as a result of your snapping the text field’s edges to the left and right guides. The constraints indicate that you want to maintain the space between the field’s sides and the sides of the superview’s bounds. Running TestApp once more shows that the Autolayout constraints now work as the original springs and struts did.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_0.png)

**FIGURE 5.25** The custom view’s leading and trailing space constraints

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_1.png)

**FIGURE 5.26** Creating constraints by snapping to guides

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_2.png)

**FIGURE 5.27** Newly added constraints
