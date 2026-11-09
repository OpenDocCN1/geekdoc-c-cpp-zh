# Working around keypath limitations

The model keypath feature suggests you should be able to access subproperties. For example, the app delegate has a property called someThing of a class with an internal property called aString, as shown in Figure 13.6. You might think someThing.aString would be a valid model keypath.

It isn’t. This idiom is valid in some of the various object controllers, but it doesn’t work with simple bindings. If you want to bind to subproperties, you have to use KVO to copy a property value to the top-level object after an update, and bind to the copy.

# Figure 13.6

Working around keypath limitations. This is an ugly hack, but the model keypath can’t usually bind to subproperties directly.

![](bbox=[0.186, 0.389, 0.505, 0.82])