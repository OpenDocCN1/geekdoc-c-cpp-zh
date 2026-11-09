
```objc
Download Persistence/HelloApplication4D/PreferencesController.h
#import <Cocoa/Cocoa.h>

@interface PreferencesController : NSWindowController {
    NSButton *loadSavedRemovedAppsCheckbox;
}
@property IBOutlet NSButton *loadSavedRemovedAppsCheckbox;
-(IBAction) toggleLoadSavedRemovedApps: (id)sender;

@end
```

The PreferencesController doesn't need to do very much. When the preference window appears, we want to set the checkbox to the state that is stored in the user preferences:

```objc
Download Persistence/HelloApplication4D/PreferencesController.m
-(void) awakeFromNib {
    [self.loadSavedRemovedAppsCheckbox
        setState:[[NSUserDefaults standardUserDefaults]
            boolForKey:@"LoadSavedRemovedApps"]];
}
```

And when the user selects or unselects the checkbox, we need to store the new value in the user preferences:

```objc
Download Persistence/HelloApplication4D/PreferencesController.m
-(IBAction) toggleLoadSavedRemovedApps: (id) sender {
    [[NSUserDefaults standardUserDefaults]
        setBool:[self.loadSavedRemovedAppsCheckbox state]
            forKey:@"LoadSavedRemovedApps"];
}
```

Let's connect the PreferencesController to the nib it manages. Double-click Preferences.xib. Set the File's Owner class to be PreferencesController. Connect its window outlet to the Window. Connect its loadSavedRemovedAppsCheckbox outlet and toggleLoadSavedRemovedApps action to the Checkbox. Select the Window, and connect its delegate to the File's Owner.

Save your work. We've created the preference window and its controller. We've implemented the controller and wired up everything in our new nib. Meanwhile, we also have set the ActivityController to use these preferences. All that remains is to pop open the Preferences window when the user selects HelloApplication > Preferences.

Use the Connections inspector to connect the HelloApplicationDelegate's openPreference: action to the Preferences... menu item.

So, we now initialize the PreferencesController and load the Preferences nib file when the user selects Preferences.... We also need to clean up these resources when the user dismisses the preference window. There's no need for the window to exist when it isn't visible, so we'll destroy it and create a new one if the user decides to modify the preferences later.

The PreferencesController is the delegate for its window, so we can implement this delegate method:

```objc
// Persistence/HelloApplication4D/PreferencesController.m
- (void)windowWillClose:(NSNotification *)notification {
    [self autorelease];
}
```

This is yet another advantage of using many small focused nibs. We can load resources when we need them and clean them up afterward.

At this point, if you click Build & Run, you can bring up the Preferences window either using the menu item or using the ⌘, keyboard shortcut. Everything is positioned for you to set and retrieve settings. Play around with changing the preferences and quitting and restarting.

You can even open your preference file (the plist not the window) and look at the value you've set.

| Key | Type | Value |
| --- | --- | --- |
| Root | Dictionary | (1 item) |
| LoadSavedRemovedApps | Boolean | ☑ |

In this chapter, you've learned techniques for saving small amounts of data. You've seen how to create plists from basic types like NSArrays and how to archive more complex data. You've also seen how to work with user preferences. When we need to store either a greater amount or a more complex arrangement of data, we'll turn to Core Data. In the next chapter, we'll swap different views, and then we'll begin the journey to understanding Core Data.

## Chapter 18

## Changing Views

Back in Chapter 16, *Displaying Data in a Table*, on page 256, we made it easy to swap which view controller and view were used by the window controller. The good news is that you can switch back and forth by changing the name of the view controller class and the nib name and recompiling. The bad news is that your user can’t make that same change at runtime.

In this chapter, we’ll create a new preference that the user can set to specify which view should be visible when the application launches. We’ll then use that preference to display the view that the user chose at launch time. We’ll then extend the example to allow the user to switch back and forth as often as they’d like while the application is running.

We wrapped up the first act of our story by re-creating our simple web browser for the iPhone. That wasn’t a lot of new material, but the point was to take another quick pass through what you’ve learned so far in a new context.

As the curtain falls on our second act, let’s look back on some of the techniques you’ve learned while working with this example. Although you’ll learn new things here and there, the main goal is for you to see the advantages of working with multiple nibs and small well-defined classes and methods.

### 18.1 Working with Radio Buttons

Let’s add a group of radio buttons to the preference panel. Double-click Preferences.xib, and search in the Library for *Radio*.

You should find this widget:

![](img/9355405953264484a02198b0e3d25b7e_285_0.png)

Drag it onto the preference window. Resize your widget and window, and add text to the right of the two radio buttons so it looks something like this:

![](img/9355405953264484a02198b0e3d25b7e_285_1.png)

Take a look at the hierarchy of GUI elements in the Preferences.xib Document window:

![](img/9355405953264484a02198b0e3d25b7e_285_2.png)

We could connect to and interact with each NSButtonCell object in the radio button group individually. Instead, we’re going to work with the group as a whole by using the NSMatrix object.

To set which radio button is selected from the PreferencesController object, add a property named group of type NSMatrix to the PreferencesController class. You also need to add an action to PreferencesController that is called whenever a radio button is selected. Name your action chooseView:, and save PreferencesController.h. In IB, use the Connections inspector to wire this outlet and action to the NSMatrix.

If we’re going to connect the controller to the NSMatrix and not the individual buttons, we need a way to tell the two buttons apart so that we can figure out which one is selected. When we worked with tables, we used the column’s identifier. NSButtonCells don’t have identifiers, but they do have tags.

In Interface Builder, select the button you've labeled Display Icon view at startup. Look at the bottom of the Attributes inspector, and you should see the attribute Tag with the value 1. Similarly, the Tag attribute for the other button cell has the value 0.¹

### 18.2 Adding Preferences for View at Launch

We need to do four things to get the preferences working:

- 1. Choose a name for the preference and a format for it.
- 2. Create a default value that will be used before the user sets their own preferences.
- 3. Read from the preference when our PreferencesController awakes from nib.
- 4. Write to the preference when the user selects a radio button.

We could store our preference as a boolean like we did for the checkbox. This would work fine for now because either we are using the Icon view or we're not. We've done that already. Let's do something different.

Let's store the tag of the currently selected button as the value of the preference. The tag is an int. We need to convert it to and from an NSNumber when writing to or reading from preferences. We create an NSNumber from an int with the class method numberWithInt:. Going the other way, we extract the int from the NSNumber with the method intValue.

Now that we have a format for our preference, we can name it to communicate what it is. Let's call it TagForView. We can register the default value in HelloApplicationAppDelegate.m just below where we registered the default value for LoadSavedRemovedApps.

```objective-c
+(void)initialize {
    NSDictionary *defaults =
        [NSDictionary dictionaryWithObjectsAndKeys:
            @"NO", @"LoadSavedRemovedApps",
            [NSNumber numberWithInt:1], @"TagForView",
            nil];
    [[NSUserDefaults standardUserDefaults] registerDefaults:defaults];
}
```

¹ If the values of these tags are different, please change them to 1 and 0.
