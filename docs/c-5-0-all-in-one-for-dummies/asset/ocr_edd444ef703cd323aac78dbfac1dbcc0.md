# Knowing What an Interface Is

An interface in C# resembles a class with no data members and nothing but abstract methods, almost like an abstract class — almost:

```
interface IRecordable
{
    void TakeANote(string note);
}
```

The interface begins with the interface keyword. It contains nothing but abstract methods. It has no data members and no implemented methods.

Interfaces can contain a few other features, including properties (covered in Chapter 5 of this minibook), events (covered in Chapter 9 of this minibook), and indexers (covered in Chapter 7 of Book I).

![](bbox=[0.12, 0.48, 0.2, 0.6])

Among the elements that a C# interface cannot exhibit are

+   - Access specifiers, such as public or private (see Chapter 5 of this minibook)
+   - Keywords such as virtual, override, or abstract (see Chapter 7 of this minibook)
+   - Data members (see Chapter 2 of this minibook)
+   - Implemented methods — nonabstract methods with bodies

All members of a C# interface are public (you can't even mention access specifiers in defining interface methods), and a C# interface isn't involved in normal inheritance; hence, it has none of those keywords. (An interface itself can be public, protected, internal, or private.)

Unlike an abstract class, a C# interface isn't a class. It can't be subclassed, and none of the methods it contains can have bodies.

# How to implement an interface

To put a C# interface to use, you implement it with one or more classes. The class heading looks like this:

```
class Pen : IRecordable // Looks like inheritance, but isn't
```

![](bbox=[0.12, 0.9, 0.2, 1.0])

A C# interface specifies that classes which implement the interface must provide specific implementations. They must. For example, any class that implements the IRecordable interface must provide an implementation for