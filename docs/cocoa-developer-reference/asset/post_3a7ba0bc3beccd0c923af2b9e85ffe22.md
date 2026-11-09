
Potentially, you can create a single method to handle every possible event from an interface. This solution won't be simple or elegant, but it is possible to do this. More typically, you can use class checking in a switch to select handler code for a small number of different sender types.

### Using (id) sender to identify objects

In Case 4, you can use the value of sender directly, in a direct comparison to identify the object that triggered an event. For example, your application might have three objects in its UI:

```objc
@property (assign) IBOutlet NSButtonCell *firstButton;
@property (assign) IBOutlet NSButtonCell *secondButton;
@property (assign) IBOutlet NSTextField *firstTextField;
```

You can link all of these objects to a single handler method, and use a pointer comparison to discover which object triggered the event.

```objc
-(void) eventHandler: (id) sender {
    if (sender == firstButton) {
        //First button was clicked
    }
    if (sender == secondButton) {
        //Second button was clicked
    }

    if (sender == firstTextField) {
        //The text field did something
    }

    //Etc...
}
```

This code is inherently loosely typed, and it is valid for all objects. It's particularly useful for UIs with multiple text fields.

### Placing outlets and actions

A standard problem in UI design is deciding which object to link to. The simple example in this chapter is built around a single subclassed object — the app delegate. This minimal design is perfect for applications with a single view. You can implement menu and other event handlers in the delegate without creating further objects. This is somewhat nonstandard, but it's a simple solution and works.

In a more complex application, there may be many nib files, each with many objects. When designing multi-view UIs, you must do the following:

- 1. Define how objects send messages to each other.
- 2. Create links for those messages.

A key limitation of the nib editing system is that you cannot drag links between nib files. IB’s interface doesn’t support this. But the First Responder object is designed to offer a workaround for action linking.

![](img/2b293e29fc15b0797f113b85dd429b6e_224_0.png)

**NOTE**

There’s no way to link outlets across multiple nib files because the requirement doesn’t make sense. Outlets are associated with a single object, which is in turn associated with a single nib file. Typically, all outlets in a nib are linked to File’s Owner or, occasionally, to a delegate object.

When you create an action method in any object in the application, it’s added to the responder chain. When you click First Responder, you’ll see a list of receive action methods. This list includes all the action methods in the application, collected from every object. You can link to these actions in the usual way—and this solves the cross-linking problem.

Figure 8.21 illustrates this with an example from an iPhone application. The `showZetta` and `showInfo:` methods are in different objects, but both appear as linking destinations inside First Responder. When an application has multiple nibs, the same list of First Responder methods appears in all of them.

**Figure 8.21** Using First Responder to view all of the action methods in an application. You can use this feature to send messages to objects that aren’t in the current nib.

![](img/2b293e29fc15b0797f113b85dd429b6e_224_1.png)

**CAUTION** First Responder doesn't indicate if a method is already linked directly as a selector. You can easily create multiple links to the same methods. This may not be a problem in your application, but it can be useful to double-check whether or not a method is already linked within an object before trying to link it again in First Responder.

### Placing NSResponder events in OS X

First Responder also supports a very long list of standard methods that can be used in every application and which are supported by many objects. These are defined in the documentation for NSResponder, which was introduced in Chapter 6.

To implement these methods, follow this two-step process:

- 1. Link a suitable object to them, so that they're triggered by a user action. The menu items in the default menu are prelinked to some of the methods for convenience.
- 2. Implement a handler method in a suitable object in the application. For example, to implement undo events, create a method called undo:. You can place the method in any object that is a subclass of NSResponder.

### Using standard event messages on the iPhone

The iPhone supports a simplified version of NSResponder, with a smaller selection of standard messages. It also supports a modified selector system, which generates yet another list of messages. Instead of a single blank selector slot triggered by a click, iPhone objects respond to different user actions with different event messages. Figure 8.22 shows the standard event list. This list is available for most objects, but is implemented differently in different objects. For example, a button doesn't send the Value Changed message, but a slider does; a text field doesn't send Touch Down, but it does send Editing Did Begin; and so on.

This is a refinement of the selector system; you can define different handlers for different event types and for objects within them, but in practice it works in a similar way. Link each event to the method in your code that it handles. To ignore an event type, leave it unlinked.

**Figure 8.22** Events on the iPhone. This list is standardized and available in many UI objects, but most objects can only send a subset of these messages.

![](img/2b293e29fc15b0797f113b85dd429b6e_226_0.png)

### Summary

This chapter has covered a lot of ground. You may need to work through it a couple of times to take it all in, but it’s worth the time because it explains some of Cocoa’s key practical concepts.

At the start of the chapter, you were introduced to a typical Interface Builder workflow. Next, you found out how to add objects to a nib, how to center and align them, and how to modify their default properties.

In the next section, you were introduced to outlets and actions, and how to define them in code. You also learned about the Interface Builder linking process and how to link objects in code to objects in a nib file. You then explored a simple application that used selectors to swap handler methods dynamically, creating a UI that reconfigured itself.

Finally, you were introduced to some more advanced techniques used in event handlers, including `id` sender idioms and First Responder events.

## Using Cocoa Design Patterns and Advanced Messaging

> It’s traditional in a Cocoa book to mention design patterns and features such as Model-View-Controller (MVC), target-action, Key-Value Coding (KVC), and Key-Value Observing (KVO).

Apple’s documentation mystifies these design patterns and makes them seem more difficult and complex than they really are. They’re an essential part of Cocoa, and you can use them to implement impressively efficient code. But the practice can be much simpler than the theory.

### Understanding Model-View-Controller

Model-View-Controller, often shortened to MVC, was introduced in Chapter 2. The outline of MVC is shown in Figure 9.1. An application is split into three elements — a store of data called a model, an interface called a view, and a controller object that passes data between them.

MVC implies, but doesn’t enforce, the suggestion that model data should be kept in separate objects and perhaps in separate custom classes.

In a simple application, this seems unnecessarily complex, because it is. If your data is in a single array or dictionary, there’s nothing to be gained by taking a data object out of the App Delegate and putting it into a separate wrapper object. It can be useful in a larger application to keep data in a separate data-handling class. But generally, the key feature of MVC isn’t how the data is stored but how it’s processed and prepared for display by the controller.

- **In This Chapter**
  - Understanding Model-View-Controller in Cocoa
  - Understanding and using target-action
  - Using Key-Value Coding
  - Using Key-Value Observing
  - Working with notifications and errors
