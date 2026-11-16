# DEPENDENCY PROPERTIES

Dependency properties “extend the functionality of CLR properties”. Fine. What does that mean, exactly? Do they do things that you can’t do with a CLR property? No, not really. It’s just that dependency properties encapsulate a bunch of useful functionality that can be tedious to implement using CLR properties, and because they’re part of the WPF infrastructure, other components of WPF know how to work with them. So, for example, you can bind a dependency property value to another object (we’ll see how to do that in Chapter 22) or animate its value using a WPF Storyboard. (We’ll take a quick look at animation in Chapter 20.)

CLR PROPERTY

DEPENDENCY PROPERTY

VALUE CALCULATION

SPARSE STORAGE

CHANGE TRACKING AND NOTIFICATION

This is arguably the most important capability of dependency properties from a programming perspective. It lets you inherit values, animate them, and ensure that they’re always valid.

This means that a dependency property only takes up space if it’s being used. It’s particularly important for attached properties (which are a form of dependency property), but it’s true of all dependency properties. And WPF handles it automatically; you don’t have to do a thing.

A lot of applications need to react when the value of a property changes. That can be bothersome with CLR properties, because they don’t automatically generate change events, but support for change notification is built into the WPF dependency property system.