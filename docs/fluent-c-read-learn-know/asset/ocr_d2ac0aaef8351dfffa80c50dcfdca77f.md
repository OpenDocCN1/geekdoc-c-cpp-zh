# # DISSECTING CLASSES

FIELDS are simple variables.
You usually won't let these
be accessed outside the class
itself. Instead, you'll wrap
the field in a property so
that you can control what
happens to it.

FIELDS and PROPERTIES represent the state of the
class: the thing it knows about like the name of an
elephant or the color of a fish.

![](bbox=[0.372, 0.22, 0.853, 0.583])

PROPERTIES contain
information, like fields, but
you can control how that
information is changed.
Properties are often, but not
always, made available outside
the class.

METHODs are routines that accept
parameters and may or may not return
a value. MessageBox.Show() and
Int32.Parse() are examples of
methods that we've already used.

EVENTs are things that happen while
an application is running, like a user clicking a Button
or a property being changed. The class PUBLISHES
the event. Other classes can SUBSCRIBE to the
event by writing code to handle (respond to) it.

METHODs and EVENTs
represent the behavior of a
class: the things it can do and
respond to.

So far, all the code we've written was in the
event handler for the Button.Click event.