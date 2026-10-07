# Separate User Interface and Code-Behind

One of the biggest goals of WPF was to separate the user interface from the code that lies behind it. Using XAML to define the user interface and C# or Visual Basic to provide the application's functions lets separate the two tasks of interface construction and programming.

In theory, graphic designers using Expression Blend can build the interface without knowing anything about programming. Programmers can use Visual Studio to add the addition code.

In practice, not every company can afford dedicated graphic designers and Expression Blend. In that, the same people may end up building the user interface and the code behind it, with a combination of Expression Blend and Visual Studio, or with Visual Studio alone. In that case, however, separating the user interface from the code behind makes working on the two pieces easier.

| GOOD, OLD IDEA |
| Good developers have been separating UI development and the code behind for years. In Windows Forms applications, one developer can build the user interface, while others code to perform application tasks. Then you can stitch the two together.
Using XAML makes the separation a bit stricter, so it provides additional benefit.
Windows Forms developers often make the code attached to the user interface as thin as possible, making simple event handlers that call routines in other modules to do all of the heavy lifting. That strategy still works for WPF applications.

Another drawback to the "separate designers" theory is that as graphic designers can build the interfaces you need without knowing a lot about programming. Unfortunately

This has led to my non-purist WPF philosophy. Do whatever is reasonable in XAML. If something is easier to handle in code, do so.

# New Controls

WPF comes with several new controls for arranging child controls. For example, StackPanel arranges its children in a single row or column, DockPanel attaches its children to its edges, WrapPanel arranges its children in a row or column and wraps to a new row or column necessary, and Grid arranges its children in rows and columns.