
In this example, it's possible to create a new Student object without specifying a college parameter (if that were desirable). Either way, we ultimately have to initialize the base class's inherited state by calling a base class constructor.

## OUTSMARTING THE COMPILER... OR NOT?

If you have a hacker's mind like I do, you'll find it challenging to try to work around restrictions imposed by the compiler, like the one shown in Figure 14.3. In fact, you can, with very limited success. If you create a cycle in constructor chains using the this keyword, the compiler won't notice you've never called a base constructor. However, all you've done is create a set of mutually recursive constructors that will result in a stack overflow exception at runtime.

## Single Inheritance for Classes

The CLR, the C# programming language, as well as other Common Language Infrastructure (CLI) languages support only single inheritance for classes. In other words, only a single base class can be used for any given class. When omitted, that base class is System.Object. In the example shown in Figure 14.6, we try to declare a class Tomato, which is both a Fruit and a Vegetable.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_690_0.png)

FIGURE 14.6 No multiple-class inheritance allowed.

## THE DIAMOND PROBLEM

One of the main reasons for not supporting multiple-class inheritance in the CLR comes from the well-known problems and complexities that arise from multiple inheritance, as seen in languages like C++. One such problem is known as the diamond problem.

Named after the shape of a type hierarchy where a class D derives from both B and C, both of which derive from A, the diamond problem pinpoints complexities that arise in this setting. Suppose A has a member called Bar and both B and C override it. Which of the two overrides should be called when code in D calls the equivalent of base.Bar() in C#? This introduces the need for virtual base classes, which complicate programming quite a bit.

Less-invasive forms of multiple inheritance have been suggested here and there, the most notable of which include traits and mixins. In fact, they aren't really forms of multiple inheritance but allow certain sets of functionality to be adopted by classes, thus reducing the need for duplication of code. Approaches such as those have their problems, too.

As you will see, the CLR supports multiple inheritance for interfaces, which doesn't suffer from those problems but is of limited use to overcome some of the scenarios where multiple inheritance proves handy. However, extension methods can be used to mimic “interfaces with default implementations” to some extent.

Because of single inheritance for classes, the base class of any class is defined in an unambiguous manner. Therefore, to refer to a base class's members explicitly, you can use the single keyword called base. Where this refers to the current instance (of the containing type), base refers to the immediate base class. In most cases, the use of the base keyword is optional:

```csharp
class Student : Person
{
    // Constructors shown earlier.

    public string College { get; private set; }

    public override string ToString()
    {
        return base.Name + " is " + base.Age
            + " and studies at " + this.College;
    }
}
```

Later you'll see one case where the use of the base keyword is required to disambiguate between a subclass's member and a base class's member with the same name. We discuss this scenario when talking about hiding members in the section, “Sealing and Hiding: Take Two.”

## INHERITANCE OR CONTAINMENT?

Here's another story for you. A long while ago, in the .NET 1.0 days, I was explaining OOP and inheritance. It turned out my explanation was unnecessary for a reason I'll explain here.

Some of my friends were working on a user interface application that had to display a Windows Forms tree view control to visualize an organization chart. If the user clicked a node in the tree, details for the selected node should have been displayed in another pane to the right (much like Windows Explorer). The obvious question was how to associate the rich business object representing an entry in the organization hierarchical structure with the TreeNode object used in the UI.

Knowing the art of OOP, my choice was quite obvious: Let's derive a subclass from TreeNode, add a property to it to contain the business object, and that's it. Windows Forms will still work fine with our custom TreeNode object (polymorphism), and we have a spot to put the business object.

However, explaining this object-oriented technique turned out to be challenging because my friends didn't have such a background. Exploring the API surface of TreeNode a bit more, I soon discovered a Tag property on the Windows Forms Control type, allowing an arbitrary object to be associated with a control. Instead of inheritance, this uses the technique of containment. The only drawback is the weakly typed nature of it, having to cast back from Tag's object type to the business object type. Ultimately, we settled for this approach.

Yet another option is to have an external collection that associates the (regular) TreeNode objects with the business objects (for example, using some kind of dictionary collection type). This, however, leads to memory-management concerns: Upon removal of a tree node, you should clean the auxiliary data structure, too.

## Multiple Inheritance for Interfaces

Each class (or struct) can implement multiple interfaces. Interfaces are covered at the end of this chapter, but you can roughly regard them as contracts that do not have an implementation of their own. When implementing an interface, you basically promise to obey the contract specified by the interface. One example is IDisposable, which we talked about in Chapter 12, “Constructors and Finalizers.”

```
public interface IDisposable
{
    void Dispose();
}
```

Implementing an interface is allowed to coexist with derivation from a base class or implementation of zero or more interfaces. In the class base specification, which is the part of the class declaration after the colon, the base class (if any is specified) has to come before the list of interfaces implemented by the class. All of those are comma-separated:

```
class Stream : MarshalByRefObject, IDisposable
{
    ...
    public void Dispose()
    {
        // I promised to implement IDisposable. Here it is.
    }
}
```

The Base Class Library (BCL) is full of types that implement multiple interfaces. Some notable ones are all the numeric primitive types that derive from System.ValueType and implement a bunch of interfaces allowing for comparison, equality checks, formatting, and so on. This is illustrated in Figure 14.7 by means of inspection through .NET Reflector.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_693_0.png)

FIGURE 14.7 Multiple inheritance for interfaces.

## INHERITANCE FOR STRUCTS: WHY (NOT)?

In the example shown in Figure 14.7, you might notice how Byte derives from the System.ValueType class, even though the Byte type itself is a struct. This is one of the implementation details of the CLR unified type system, facilitating things such as boxing.

Beyond inheriting from System.ValueType, there's no subtyping possible for value types, other than the implementation of interfaces. By implication, there's also no means to do polymorphism with structs. The reason this is the case is a rather fundamental one. Recall that value types get allocated on the stack by default. If we were to allow subtyping for structs, you could have a Point2D variable on the stack and assign it a subtype of type Point3D:

```
static double Distance(Point2D first, Point2D second)
{
    ...
}

static void Main()
{
    var point1 = new Point3D(1, 2, 3);
    var point2 = new Point3D(4, 5, 6);
    Console.WriteLine(Distance(point1, point2));
}
```

Assume in the preceding example that both Point2D and Point3D are structs and the latter is a subtype of the former (hypothetically). Implementation of the Distance method using stack allocation for the parameters has just become incredibly hard because the size of the parameters is no longer fixed. Where a Point2D may have two fields of type Int32 (hence causing a total of 8 bytes to allocate the object), any subtype may add an arbitrary amount of data to it.
