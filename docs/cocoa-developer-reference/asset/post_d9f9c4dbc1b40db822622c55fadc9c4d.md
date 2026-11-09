
SEL is the associated data type. You can define a SEL variable and use it in place of a literal selector.

```
SEL theSelector;
if (aCondition)
    theSelector = @selector(methodOne:);
else
    theSelector = @selector(methodTwo:);
anObject.action = theSelector;
```

![](img/2b293e29fc15b0797f113b85dd429b6e_237_0.png)

## CAUTION

**SEL doesn’t define a pointer. Don’t put an asterisk in front of a SEL variable.**

## Using selectors in code

Target-action is often, but not exclusively, used with subclasses of NSControl. This includes most UI objects such as buttons, menus, and sliders. This code is valid for all of its subclasses:

```
[aControl setTarget: anObject];
[aControl setAction: @selector(aMethod:)];
```

Where aControl is @synthesized, dot syntax is also valid.

```
aControl.target = anObject;
aControl.action = @selector(aMethod:);
```

You can read an action and compare it with a selector directly with ==:

```
if (aControl.action == @selector(aMethod:)) {...}
```

You can use this to test whether you need to modify the selector or to process an event according to the current selector state.

A property called continuous is an optional feature implemented in NSControl. When continuous is TRUE, a control fires its selector while the user holds the mouse down. Otherwise, it generates one single message for each click. Use this feature to implement auto-increment and auto-decrement.

## Understanding the limitations of selectors

The action system has an obvious limitation: you can’t use it to pass parameters to the target method. Some variants of target-action support an extended syntax with an extra parameter that can pass an object to the selector:

```
[anObject setAction:
    @selector(withObject:) withObject:anObjectUsedAsAParameter];
```

This is only available in limited circumstances. If you need to pass parameters to your selector method, pass them externally through some associated properties or other data objects.

The other limitation is that a selector *isn’t* a pointer. It doesn’t point to a specific entry point in memory. Instead, it triggers a runtime lookup of a method name, which returns a pointer. This can be an ambiguous process, because more than one object may implement the same method name.

Generally, selectors are local. If there’s no explicit `target` object, the lookup assumes that you’re trying to find a matching method in `self`. This is intuitive behavior, and rarely a problem. But keep in mind that selectors don’t usually range over the whole of your application, except when there’s a supporting target property.

This short summary is almost all you need to know about target-action. It’s an unusual feature that isn’t available in most other languages, but in practice it’s very unmysterious.

## Defining selectors in Interface Builder

When you create an `IBAction` link in Interface Builder (IB), you’re really setting an object’s target and the action properties. This is why setting an action is a two-step process. Assume you have a nib file with a button and you’re going to link the button to an action. The first step selects the target object graphically, as shown in Figure 9.6.

**Figure 9.6**

When creating a link, the first step sets the target object for the link.

![](img/2b293e29fc15b0797f113b85dd429b6e_238_0.png)

In this example, this step defines the button’s target object as the App Delegate. The second step sets the action method, as shown in Figure 9.7.

**Figure 9.7**

Setting the action method by selecting from a pop-up list

![](img/2b293e29fc15b0797f113b85dd429b6e_239_0.png)

In code, you can select any public method as a valid action. In IB, only methods that are defined as an IBAction appear in the pop-up menu. It would be convenient if IB listed every compatible method in the target object — but it doesn’t. You can work around this by defining the actions in code when the application loads. Use this to choose any valid selector in any object, including objects that your code creates dynamically.

## CROSS-REF

For an example of dynamically created buttons with an assigned action, see the random button example in Chapter 16.

## Creating an example application

Figure 9.8 shows a simple application that illustrates target-action. It’s a slightly extended and simplified variation on the counter application from the previous example. Two buttons create a counter that counts up and down. The timer is replaced by the continuous property. When this is enabled, trigger events are generated while the mouse button is held down.

**Figure 9.8**

A simple target-action application. Selecting the Flip button swaps the selectors in the Up and Down buttons.

![](img/2b293e29fc15b0797f113b85dd429b6e_240_0.png)

The buttons are linked to `addOne:` and `subtractOne:` methods that change the value of a timer variable. The value is displayed in a text field. Figure 9.9 shows the elements and links in the nib file.

`upButton`, `downButton`, and the `theText` outlets link to the properties of the two main buttons and the text field. The `addOne:` and `subtractOne:` methods control a counter. The `flipButton` action triggers the button flip method.

The header file for the project defines the objects, outlets, and actions that are used.

```objc
#import <Cocoa/Cocoa.h>
@interface TargetAction_AppDelegate : NSObject
{
    NSWindow *window;
    NSTextField *theText;
    NSButton *upButton;
    NSButton *downButton;
}
@property (nonatomic, retain) IBOutlet NSWindow *window;
@property (nonatomic, retain) IBOutlet NSTextField *theText;
@property (nonatomic, retain) IBOutlet NSButton *upButton;
@property (nonatomic, retain) IBOutlet NSButton *downButton;
- (IBAction) addOne: (id) sender;
- (IBAction) subtractOne: (id) sender;
- (IBAction) flipButtons: (id) sender;
@end
```

**Figure 9.9**

The project nib file: it’s straightforward and has no unusual features.

![](img/2b293e29fc15b0797f113b85dd429b6e_241_0.png)

The implementation file implements the button action methods. The code for the addOne: and subtractOne: methods updates the counter and writes its new value to the text field.

The flipButtons: method swaps the title and action of both buttons, and it also toggles their continuous property. When the buttons are flipped, single clicks trigger a single update of the counter. Otherwise, the count changes while the mouse button is held down. The code also includes a selector comparison that checks the current flip state.

```objc
#import "TargetAction_AppDelegate.h"
@implementation TargetAction_AppDelegate
@synthesize window, theText, upButton, downButton;
int theCount;
- (IBAction) addOne: (id) sender{
    theCount +=1;
    theText.stringValue =
    [NSString stringWithFormat:@"%i", theCount];
}
- (IBAction) subtractOne: (id) sender{
    theCount -=1;
    theText.stringValue =
    [NSString stringWithFormat:@"%i", theCount];
}
- (IBAction) flipButtons: (id) sender {
    if (upButton.action == @selector(addOne:)) {
        upButton.action = @selector(subtractOne:);
        [upButton setContinuous: NO];
        upButton.title = @"Down";
        downButton.action = @selector(addOne:);
        [downButton setContinuous: NO];
        downButton.title = @"Up";
    } else {
        upButton.action = @selector(addOne:);
        [upButton setContinuous: YES];
        upButton.title = @"Up";
        downButton.action = @selector(subtractOne:);
        [downButton setContinuous: YES];
        downButton.title = @"Down";
    }
}
@end
```

## Other applications of selectors

Table 9.1 lists some other ways that selectors and target-action are used in Cocoa.

**Table 9.1** Selected Advanced applications of target-action and selectors

| Application | Description |
|---|---|
| NSTimer | Supports both target and action. Selects a method that is called on each timer tick or after a delay. |
| performSelector: | A method built into NSObject and supported by most classes. Supports both target and action. Selects a method that can be run immediately or after a delay. Supports explicit multithreading. |
| performSelectorInBackground: | A very simple way to run a method in a separate background thread. |
| Data collection objects: NSArray and so on | Include a makeObjectsPerformSelector: method that automatically enumerates through every object in the collection and runs the selected method on it. |
| Core Animation | Certain Core Animation classes can trigger a selector when an animation completes. Use this for composite multiple animations or to control user input while the animation runs. |
| NSInvocation | Wraps a selector and a target into a combined object with parameters to create a powerful composite. Sometimes used to manage Cocoa's undo system. |
| canPerformSelector: | A method that can be run on any object to check whether it implements a selector. Use it to avoid crashes and error messages. |
