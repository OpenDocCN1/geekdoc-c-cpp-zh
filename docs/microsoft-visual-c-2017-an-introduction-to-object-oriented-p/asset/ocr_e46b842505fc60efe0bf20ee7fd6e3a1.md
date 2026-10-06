(continued)

When you double-click a component on a Form in Design View, you move to the default method code. By clicking the component, however, you remain in Design View, and the correct set of properties appears in the Properties list.

+   6. Click the Save All button, and then execute the program. As you click Buttons, the Form’s background color changes appropriately.
7. Dismiss the form, and exit Visual Studio.

# Chapter Summary

+   GUI programs are event-driven—an event such as a button click “drives” the program to perform a task. Programmers also say a button click raises an event, fires an event, or triggers an event. A method that performs a task in response to an event is an event handler. The C# event is generated when a button is clicked.

+   A delegate is an object that contains a reference to a method. C# delegates provide a way for a program to take alternative courses that are not predetermined; a delegate provides a way to pass to a method as an argument to another method. You can assign one delegate to another using the = operator. You can use the + and += operators to combine delegates into a delegate that calls the delegates from which it is built.

+   To declare your event, use a delegate. A class identifies methods to execute by associating the delegate with the method that should execute when the event occurs. The delegate type for an event should take exactly two parameters: a parameter indicating the source of the event, and an EventArgs parameter encapsulates any additional information about the event. For events that do not use additional information, the .NET Framework already has defined an appropriate type name EventHandler.

+   When using Control components as Buttons and ListBoxes, they contain events with names as Click. A Form can contain any number of Controls that might have events associated with them, and a single control might be able to raise any number of events.

+   Every mouse or keyboard-event handler must have two parameters: an object representing the sender, and an object that holds event information. Mouse events include all the actions the user takes with a mouse, including clicking, pointing, and drawing. Mouse events can be handled by any Control through an object of the class MouseEventArgs.