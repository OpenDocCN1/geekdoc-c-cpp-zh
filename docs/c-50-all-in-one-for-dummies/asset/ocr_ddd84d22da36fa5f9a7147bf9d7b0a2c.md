# Figure 8-1:
A tale of two class hierarchies and one interface.

![](bbox=[0.22, 0.13, 0.79, 0.31])

I’ve shown you two concrete classes that inherit from Animal and two that inherit from Robot. However, you can see that neither class Cobra nor class Robozilla implements IPet — probably for good reasons. I have no plans to watch TV with my pet cobra beside me on the couch, and a robozilla sounds nasty too. Some of the classes in both hierarchies exhibit what you might call “petness” and some don’t.

The InterfacesBridgingHierarchies example on this book’s website puts these items through their paces.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robocat and Robodog can carry out the AskForStrokes() and DoTricks() actions and have the NumberOfLegs property, as can Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don’t implement IPet.

You can add support for an interface to any class — but only if you’re free to modify the source code.

![](bbox=[0.11, 0.42, 0.21, 0.52])

![](bbox=[0.105, 0.6, 0.205, 0.7])

# Hiding Behind an Interface

Often in this book, I discuss code that (a) you write but (b) someone else (a client) uses in her programs (you may be the client yourself, of course). Sometimes, you have a complex or tricky class for which you would truly rather not expose the whole public interface to clients. For various reasons, it includes some dangerous operations that nonetheless have to be public. Ideally, you would expose a safe subset of your class’s public methods and properties and hide the dangerous ones. C# interfaces can do that, too.

Here’s a different Robozilla class, with several methods and properties that amateurs can use safely and enjoyably. But Robozilla also has some advanced features that can be, well, scary: