well, but with some problems it seems like the natural solution.

The idea behind the delegation pattern is similar to that behind inheritance and prototypes: You allow one object to define some subset of the behavior of another object.

You won't see this in the Foundation framework much, but it's very common in AppKit or UIKit code. Each user interface object uses delegation to allow you to define what happens in response to user interface events.

Several patterns are related to delegation, and they are all related to the general rule that you should favor object composition over inheritance. This is important for loose coupling, because it makes it much easier to reuse the code.

If you have a C++ class with three superclasses providing some aspects of its behavior, then it is a lot harder to modify than an Objective-C class delegating aspects of its functionality to three other classes.