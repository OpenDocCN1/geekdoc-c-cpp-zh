The Cocoa approach has advantages: it is flexible and open-ended; is able to handle output to various devices, from printers to screens to files, automatically; and can create advanced effects with very little code. Looked at positively, setup code can often be reused as boilerplate. Once you have your equivalent to a Flash stage, you can recycle the setup code in other applications with only minor changes. Even so, allow for extra setup and teardown before you start; there may be more than you’re expecting.

# Abstraction and object orientation

Cocoa is highly abstracted and object oriented. Relationships between causes and outcomes are loose and can be customized. For example, an unsophisticated operating system might include a loop that catches keyboard events into a buffer and a minimal framework that can read and process events. Your application might read the events and process them from the buffer.

Cocoa takes a much less direct approach. Keyboard events are abstracted into messages, and your application must include handlers for some or all of the possible messages. For example, Cocoa’s user interface manager object NSResponder sends various messages as a user types on the Mac keyboard, such as:

```
cancelOperation:
capitalizeWord:
deleteBackward:
willPresentError:
yank:
```

This list of edit control messages includes more than 170 items. The full list of messages that NSResponder can send runs into the hundreds and implements mouse control, touchpad control, gesture sensing, graphics tablet control, and other standard features.

Through abstraction, Cocoa implements much of the event processing and some of the application design for you. Although these message names imply text editing, you could also use them in a different application, such as a mathematical equation editor. You can choose which messages your application responds to. If you don’t include a handler method for a message, the message and the user action are ignored; if you do include a handler, you can choose what it does and how it works. Cocoa doesn’t force you to implement features that match the method names, although it’s less confusing for the user if you do.

Abstraction adds flexibility, often in a useful way. It also adds complexity. Whereas a simple OS sets colors with three numerical RGB components, Cocoa encapsulates color in an NSColor object. There’s no option to set colors directly. You must create and initialize an NSColor object, set its properties to the required components, and then use messaging to allow other objects to read the properties — perhaps to draw a line or to set a point. Sample code might look this:

```
NSColor *myTranslucentBlack = [NSColor initWithCalibratedRed: 0
    green: 0 blue: 0 alpha: 0.5];
[receiverObject drawSomethingWithColor: myTranslucentBlack];
```