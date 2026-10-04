# Making flexible dependencies through interfaces

There must be a way to implement Move() that doesn't require you to open a can of worms every time a client wants wriggling instead. You can use interfaces, of course!

Look at the following code that uses HAS_A, a now-familiar relationship between two classes in which one class contains the other:

```
public class Robot
{
    // This object is used to implement motion.
    protected Motor _motor = new Motor(); // Refers to Motor by name
    // ...
}
internal class Motor { ... }
```

The point about this example is that the contained object is of type Motor, where Motor is a concrete object. (That is, it represents a real item, not an abstraction.) HAS_A sets up a dependency between classes Robot and Motor: Robot depends on the concrete class Motor. A class with concrete dependencies is tightly coupled to them: When you need to replace Motor with something else, code that depends directly on Motor like this has to change, too. Instead, insulate your code by relying only on the public interface of dependencies, which you can do with interfaces. You can depend on dependent objects in a, er, less dependent way.

Depend on abstractions, not on concrete classes. I show you how.

![](bbox=[0.13, 0.53, 0.2, 0.65])

# Abstract or concrete: When to use an abstract class and when to use an interface

In Chapter 7 of this minibook, in my little discourse about birds, I say, “Every bird out there is a subtype of Bird.” In other words, a duck is an instance of a subclass Duck. You never see an instance of Bird itself — Bird is an abstraction. Instead, you always see concrete, physical ducks, sparrows, or hummingbirds. Abstractions are concepts. As living creatures, ducks are real, concrete objects. And, concrete objects are instances of concrete classes. (A concrete class is a class that you can instantiate. It lacks the abstract keyword, and it implements all methods.)

![](bbox=[0.13, 0.8, 0.2, 0.92])

You can represent abstractions in two ways in C#: with abstract classes or with C# interfaces. The two have differences that can affect your choice of which one to use:

+   Use an abstract class when you can profitably share an implementation with subclasses — the abstract base class can contribute real code that its subclasses can use by inheritance. For instance, maybe class Robot can handle part of the robot’s tasks, just not movement.