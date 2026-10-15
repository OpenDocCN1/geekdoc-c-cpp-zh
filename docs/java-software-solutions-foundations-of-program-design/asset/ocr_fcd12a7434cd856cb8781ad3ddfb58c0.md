# 4.7 Graphical User Interfaces

In Chapters 2 and 3 we introduced a few key components that are helpful in the design of graphics-based programs. What we need now is true user interaction, which is the heart of a graphical user interface (GUI). This section introduces the concepts needed to create interactive GUI-based programs. It lays the groundwork for all GUI discussions throughout the book.

At least three kinds of objects are needed to create a graphical user interface in Java:

+   - components
+   - events
+   - listeners

As we mentioned in Chapter 3, a GUI component is an object that defines a screen element to display information or allow the user to interact with a program in a certain way. Examples of GUI components include push buttons, text fields, labels, scroll bars, and menus. A container is a special type of component that is used to hold and organize other components. We’ve already used containers such as frames and panels and explored the use of labels as well.

An event is an object that represents some occurrence in which we may be interested. Often, events correspond to user actions, such as pressing a mouse button or typing a key on the keyboard. Most GUI components generate events to indicate a user action related to that component. For example, a button component will generate an event to indicate that the button has been pushed. A program that is oriented around a GUI, responding to events from the user, is called event-driven.

A listener is an object that “waits” for an event to occur and responds in some way when it does. We must carefully establish the relationships among the listener, the event it listens for, and the component that will generate the event.

> KEY CONCEPT
> A GUI is made up of components, events that represent user actions, and listeners that respond to those events.

For the most part, we will use components and events that are predefined by classes in the Java class library. We will tailor the behavior of the components, but their basic roles have been established. We will, however, write listener classes to perform whatever actions we desire when events occur.

Specifically, to create a Java program that uses a GUI, we must:

+   - instantiate and set up the necessary components,
+   - implement listener classes that define what happens when particular events occur, and
+   - establish the relationship between the listeners and the components that generate the events of interest.

VideoNote
Overview of GUI development.