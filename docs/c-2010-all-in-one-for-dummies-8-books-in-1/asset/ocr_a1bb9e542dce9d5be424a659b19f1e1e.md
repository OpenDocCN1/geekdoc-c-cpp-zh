# As the base type of an array or collection

Suppose that you have two classes, Animal and Robot, and that both are abstract. You want to set up an array to hold both thisCat (an Animal) and thatRobot (a cute droid). The only way is to fall back on type Object, the ultimate base class in C#, and the only base class that's common to both Animal and Robot as well as their subclasses:

```
object[] things = new object[] { thisCat, thatRobot };
```

That's poor design for lots of reasons. But suppose you're focused on the objects' movements. You can have each class implement IMovable:

```
interface IMovable
{
  void Move(int direction, int speed, int distance);
}
```

and then set up an array of IMovables to manipulate your otherwise incompatible objects:

```
IMovable[] movables = { thisCat, thatRobot };
```

The interface gives you a commonality that you can exploit in collections.

# As a more general type of object reference

The following variable declaration refers to a specific, physical, concrete object (see the later section “Abstract or concrete: When to use an abstract class and when to use an interface"):

```
Cat thisCat = new Cat();
```

One alternative is to use a C# interface for the reference:

```
IMovable thisMoveCat = (IMovable)new Cat(); // Note the required cast.
```

You can put any object into the variable that implements IMovable. This practice has wide, powerful uses in object-oriented programming, and you can see it in this chapter.

# Using the C# Predefined Interface Types

Because interfaces are extremely useful, you find more interfaces in the .NET class library than gun racks at an NRA convention. I counted dozens in Help before getting tired and stressed. Among the dozen or more interfaces in the System namespace alone are IComparable, IComparable<T>, IDisposable, and IFormatable. The System.Collections.Generics

![](bbox=[0.895, 0.328, 0.973, 0.483])