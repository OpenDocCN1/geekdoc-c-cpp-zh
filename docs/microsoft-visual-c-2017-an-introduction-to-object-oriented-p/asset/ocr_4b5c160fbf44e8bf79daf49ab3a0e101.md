The delegate used to create mouse event handlers is MouseEventHandler. Depending on the event, the type of the second parameter is EventArgs or MouseEventArgs. Keyboard events, also known as key events, when a user presses and releases keyboard keys. Depending on the event, the type of the second parameter is KeyEventArgs or KeyPressEventArgs.

+   - When you encounter multiple GUI Controls on a Form, usually one Control has focus. That is, if the user presses Enter, the Control will raise an event. When a Form contains multiple Controls, you can create a special event for each Control, or you associate the same event with multiple Controls.

+   - When you encounter a new control in the IDE, you probably can use it without understanding all the code generated in the background. However, when you learn about the background code, your knowledge of C# is more complete.

# Key Terms

An event is a reaction to an occurrence in a program.

At runtime describes actions that occur during a program's execution.

Event-driven programs contain code that causes an event such as a button click to drive the program to a task.

A button raises an event, fires an event, or triggers an event.

An event handler is a method that performs a task in response to an event.

An event sender is the object that generates an event.

An event receiver is another name for an event handler.

A click event is an action fired when a user clicks a button in a GUI environment.

Event wiring is the act of connecting an event to its resulting actions.

A delegate is an object that contains a reference to a method.

A composed delegate calls the delegates from which it is built.

Invoking the event occurs when the user calls an event method.

Key events are keyboard events that occur when a user presses and releases keyboard keys.

Focus is the property of a Control that causes an event to be raised when the user presses Enter.