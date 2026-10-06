# Introduction to Programming and Problem-Solving Using Scala

+   Data Members:
* score - An Int for how many points the player has.
* lives - An Int for how many lives the player has left.

+   Methods:
* main - As we will see later, this is the method that makes the whole game run.

You have noticed that while some of the types above dealt with some aspects of how things are drawn in the game, nothing actually any drawing. There is a reason for this. Drawing is something of a separate responsibility from game logic, scoring, and movement. For that reason, it should be placed in a different type. This separation of responsibilities makes it easier in the future to change just how things are drawn.

+   Renderer:
* render - Everything that we can see the game being played.

That completes the design for our Pac-Man” game. The key thing is that we are putting functionality directly into the classes that have the data to deal with that data so that any mutation/alteration is limited in what it happens. In the next section, we will see how we can implement these designs in Scala.

# 16.2 Implementing OO in Scala

Scala is a CLASS BASED object-oriented programming language. That means that programmers create classes in their programs and those classes define types that are used to make objects. We already saw how the case classes that we defined new types. We did not put anything in them except some data elements.
The case keyword in front of a case class worked for our needs in chapter 10, but it is not required to define a class. We will be writing normal classes now and only using case classes when they are called for. The class tells Scala what goes into the objects of that type and what type of functionality these objects should have. The syntax for a class is as follows.

```
class TypeName(arg:Type1, arg2:Type2, ...) {
  // Methods and Members
```

As you can see, the only things that are different between this and the case classes we have already worked with is the lack of the keyword case and curly braces with stuff in them after the class. These curly braces, like curly braces in Scala, define a new scope. This scope is associated with the class and anything you want to put in the class inside of them.