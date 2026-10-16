# Class Hierarchies

> *Abstraction is selective ignorance.*  
> — Andrew Koenig

+   - Introduction
+   - Design of Class Hierarchies
+     - Implementation Inheritance; Interface Inheritance; Alternative Implementations; Localizing Object Creation
+   - Multiple Inheritance
+     - Multiple Interfaces; Multiple Implementation Classes; Ambiguity Resolution; Repeated Use of a Base Class; Virtual Base Classes; Replicated vs. Virtual Bases
+   - Advice

# 21.1 Introduction

The primary focus of this chapter is design techniques, rather than language features. The examples are taken from user-interface design, but I avoid the topic of event-driven programming as commonly used for graphical user interface (GUI) systems. A discussion of exactly how an action on the screen is transformed into a call of a member function would add little to the issues of class hierarchy design and has a huge potential for distraction: it is an interesting and important topic in its own right. For an understanding of GUI, have a look at one of the many C++ GUI libraries.

# 21.2 Design of Class Hierarchies

Consider a simple design problem: Provide a way for a program (“an application”) to get an integer value from a user. This can be done in a bewildering number of ways. To insulate our program from this variety, and also to get a chance to explore the possible design choices, let us start by defining our program’s model of this simple input operation.

The idea is to have a class `Ival_box` (“integer value input box”) that knows what range of input values it will accept. A program can ask an `Ival_box` for its value and ask it to prompt the user if necessary. In addition, a program can ask an `Ival_box` if a user changed the value since the program last looked at it:

```
user
(via “system”)
Ival_box:
value application set_value() get_value()
```

Because there are many ways of implementing this basic idea, we must assume that there will be many different kinds of `Ival_box`es, such as sliders, plain boxes in which a user can type a number, dials, and voice interaction.