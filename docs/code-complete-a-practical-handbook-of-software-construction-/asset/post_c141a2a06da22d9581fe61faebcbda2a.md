
When you choose to implement a new class through inheritance, think through the kind of inheritance you want for each member routine. Beware of inheriting implementation just because you’re inheriting an interface, and beware of inheriting an interface just because you want to inherit an implementation. If you want to use a class’s implementation but not its interface, use containment rather than inheritance.

## Don’t “override” a non-overridable member function

Both C++ and Java allow a programmer to override a non-overridable member routine—kind of. If a function is private in the base class, a derived class can create a function with the same name. To the programmer reading the code in the derived class, such a function can create confusion because it looks like it should be polymorphic, but it isn’t; it just has the same name. Another way to state this guideline is, “Don’t reuse names of non-overridable base-class routines in derived classes.”

## Move common interfaces, data, and behavior as high as possible in the inheritance tree

The higher you move interfaces, data, and behavior, the more easily derived classes can use them. How high is too high? Let abstraction be your guide. If you find that moving a routine higher would break the higher object’s abstraction, don’t do it.

## Be suspicious of classes of which there is only one instance

A single instance might indicate that the design confuses objects with classes. Consider whether you could just create an object instead of a new class. Can the variation of the derived class be represented in data rather than as a distinct class? The Singleton pattern is one notable exception to this guideline.

## Be suspicious of base classes of which there is only one derived class

When I see a base class that has only one derived class, I suspect that some programmer has been “designing ahead”—trying to anticipate future needs, usually without fully understanding what those future needs are. The best way to prepare for future work is not to design extra layers of base classes that “might be needed someday”; it’s to make current work as clear, straightforward, and simple as possible. That means not creating any more inheritance structure than is absolutely necessary.

## Be suspicious of classes that override a routine and do nothing inside the derived routine

This typically indicates an error in the design of the base class. For instance, suppose you have a class Cat and a routine Scratch() and suppose that you eventually find out that some cats are declawed and can’t scratch. You might be tempted to create a class derived from Cat named ScratchlessCat and override the Scratch() routine to do nothing. This approach presents several problems:

- It violates the abstraction (interface contract) presented in the Cat class by changing the semantics of its interface.
- This approach quickly gets out of control when you extend it to other derived classes. What happens when you find a cat without a tail? Or a cat that doesn’t catch mice? Or a cat that doesn’t drink milk? Eventually you’ll end up with derived classes like ScratchlessTaillessMicelessMilklessCat.

Over time, this approach gives rise to code that’s confusing to maintain because the interfaces and behavior of the ancestor classes imply little or nothing about the behavior of their descendants.

The place to fix this problem is not in the base class, but in the original Cat class. Create a Claws class and contain that within the Cats class. The root problem was the assumption that all cats scratch, so fix that problem at the source, rather than just bandaging it at the destination.

## Avoid deep inheritance trees

Object-oriented programming provides a large number of techniques for managing complexity. But every powerful tool has its hazards, and some object-oriented techniques have a tendency to increase complexity rather than reduce it.

In his excellent book Object-Oriented Design Heuristics (1996), Arthur Riel suggests limiting inheritance hierarchies to a maximum of six levels. Riel bases his recommendation on the “magic number 7±2,” but I think that’s grossly optimistic. In my experience most people have trouble juggling more than two or three levels of inheritance in their brains at once. The “magic number 7±2” is probably better applied as a limit to the total number of subclasses of a base class rather than the number of levels in an inheritance tree.

Deep inheritance trees have been found to be significantly associated with increased fault rates (Basili, Briand, and Melo 1996). Anyone who has ever tried to debug a complex inheritance hierarchy knows why. Deep inheritance trees increase complexity, which is exactly the opposite of what inheritance should be used to accomplish. Keep the primary technical mission in mind. Make sure you’re using inheritance to avoid duplicating code and to minimize complexity.

## Prefer polymorphism to extensive type checking

Frequently repeated case statements sometimes suggest that inheritance might be a better design choice, although this is not always true. Here is a classic example of code that cries out for a more object-oriented approach:

```
C++ Example of a Case Statement That Probably Should Be Replaced by Polymorphism
switch ( shape.type ) {
    case Shape_Circle:
        shape.DrawCircle();
        break;
    case Shape_Square:
        shape.DrawSquare();
        break;
    ...
}
```

In this example, the calls to shape.DrawCircle() and shape.DrawSquare() should be replaced by a single routine named shape.Draw(), which can be called regardless of whether the shape is a circle or a square.

On the other hand, sometimes case statements are used to separate truly different kinds of objects or behavior. Here is an example of a case statement that is appropriate in an object-oriented program:

## C++ Example of a Case Statement That Probably Should Not Be Replaced by Polymorphism

```
switch ( ui.Command() ) {
    case Command_OpenFile:
        OpenFile();
        break;
    case Command_Print:
        Print();
        break;
    case Command_Save:
        Save();
        break;
    case Command_Exit:
        ShutDown();
        break;
    ...
}
```

In this case, it would be possible to create a base class with derived classes and a polymorphic DoCommand() routine for each command (as in the Command pattern). But in a simple case like this one, the meaning of DoCommand() would be so diluted as to be meaningless, and the case statement is the more understandable solution.

Make all data private, not protected As Joshua Bloch says, “Inheritance breaks encapsulation” (2001). When you inherit from an object, you obtain privileged access to that object’s protected routines and data. If the derived class really needs access to the base class’s attributes, provide protected accessor functions instead.

## Multiple Inheritance

Inheritance is a power tool. It’s like using a chain saw to cut down a tree instead of a manual crosscut saw. It can be incredibly useful when used with care, but it’s dangerous in the hands of someone who doesn’t observe proper precautions.

> The one indisputable fact about multiple inheritance in C++ is that it opens up a Pandora’s box of complexities that simply do not exist under single inheritance.
> —Scott Meyers

If inheritance is a chain saw, multiple inheritance is a 1950s-era chain saw with no blade guard, no automatic shutoff, and a finicky engine. There are times when such a tool is valuable; mostly, however, you’re better off leaving the tool in the garage where it can’t do any damage.

Although some experts recommend broad use of multiple inheritance (Meyer 1997), in my experience multiple inheritance is useful primarily for defining “mixins,” simple classes that are used to add a set of properties to an object. Mixins are called mixins because they allow properties to be “mixed in” to derived classes. Mixins might be classes like *Displayable*, *Persistent*, *Serializable*, or *Sortable*. Mixins are nearly always abstract and aren’t meant to be instantiated independently of other objects.

Mixins require the use of multiple inheritance, but they aren’t subject to the classic diamond-inheritance problem associated with multiple inheritance as long as all mix-ins are truly independent of each other. They also make the design more comprehensible by “chunking” attributes together. A programmer will have an easier time understanding that an object uses the mixins *Displayable* and *Persistent* than understanding that an object uses the 11 more-specific routines that would otherwise be needed to implement those two properties.

Java and Visual Basic recognize the value of mixins by allowing multiple inheritance of interfaces but only single-class inheritance. C++ supports multiple inheritance of both interface and implementation. Programmers should use multiple inheritance only after carefully considering the alternatives and weighing the impact on system complexity and comprehensibility.

## Why Are There So Many Rules for Inheritance?

![](img/649c8eee28c38ca1e062691e45dc9883_185_0.png)

This section has presented numerous rules for staying out of trouble with inheritance. The underlying message of all these rules is that *inheritance tends to work against the primary technical imperative you have as a programmer, which is to manage complexity*. For the sake of controlling complexity, you should maintain a heavy bias against inheritance. Here’s a summary of when to use inheritance and when to use containment:

**Cross-Reference** For more on complexity, see “Software’s Primary Technical Imperative: Managing Complexity” in Section 5.2.

- If multiple classes share common data but not behavior, create a common object that those classes can contain.
- If multiple classes share common behavior but not data, derive them from a common base class that defines the common routines.
- If multiple classes share common data and behavior, inherit from a common base class that defines the common data and routines.
- Inherit when you want the base class to control your interface; contain when you want to control your interface.
