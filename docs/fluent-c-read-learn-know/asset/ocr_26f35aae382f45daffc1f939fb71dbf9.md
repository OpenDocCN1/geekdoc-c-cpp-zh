# THE LOGICAL LEVEL

Routed commands are actually pretty simple to use, but the class diagram of all the objects involved is pretty complex (and frankly, a little scary), so let's begin by looking at how the pieces fit together:

The command source triggers the command. Any given command can have multiple command sources.

The command itself is an independent object.

The command binding links the element that will handle the command events to the command.

# ROUTED COMMAND

# COMMAND SOURCE

# COMMAND TARGET

The command target is operated on by the command (an example is a TextBox that receives pasted text).

# COMMAND BINDING

UIElement defines the CommandBindings collection (to be inherited by FrameworkElement and Control) that allows any descendant to handle multiple commands.

# UIELEMENT

MAKE A NOTE
Routed commands aren't actually routed, but the events they expose are.