+   5. **Set the button's Caption property to Hello World!**. This is the text that appears on the face of the button.

+   6. **Click the drop-down list in the button's On Click event property, and select mcrHelloWorld from the list (shown in Figure 22.5).**

# FIGURE 22.5

Set any object's event property to the macro to trigger that macro when that event occurs.

![](bbox=[0.22, 0.35, 0.62, 0.6])

# Tip

You aren't limited to the button's Click event. If you want a macro to run every time a form loads, set the On Load event property of the form to the macro's name. Select the Event tab on any object's Property Sheet to see the available events.

That's all there is to creating and running a macro. Just select the action, set the action arguments, and assign the macro to an event property.

# NOTE

Historically, there has been quite a bit of confusion about the names of events and their associated event properties. An event is always an action, such as Click, while its event property is OnClick or On Click. Conceptually, they're almost the same thing, but in technical terms, an event (like Click or Open) is an action supported by an Access object (like a form or command button), and an event procedure (OnClick or OnOpen) is how the event is attached or bound to the object.

# Understanding Macro Security

The Hello World! macro we built in the last section is as harmless as they come. But not all macros are harmless. You can do almost anything in a macro that you can do in the Access user interface. Some of those things, like running a delete query, can cause data loss. Access has built-in a security environment that helps you prevent unwanted, harmful macros from being run.