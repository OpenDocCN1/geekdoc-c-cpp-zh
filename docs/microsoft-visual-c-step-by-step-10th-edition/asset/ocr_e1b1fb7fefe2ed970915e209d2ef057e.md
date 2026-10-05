To implement an interface, you declare a class or structure that inherits from the interface and implements all the methods specified by the interface. This is not really inheritance as such, although the syntax is the same and some of the semantics that you will see later in this chapter bear many of the hallmarks of inheritance.

> > #### Note
>> Unlike with class inheritance, a structure can implement an interface.

For example, suppose you're defining the `Mammal` hierarchy described in `Chapter 12`, you will need to specify that land-bound mammals provide a method named `NumberOfLegs` that returns as an `int` number of legs that a mammal has. (Sea-bound mammals do not implement this interface.) You could define an `ILandBound` interface that contains this method as follows:

```
interface ILandBound
{
    int NumberOfLegs();
}
```

You could implement this interface in the `Horse` class. You inherit from the interface and provide an implementation of every method defined by the interface (in this case, there's just the one method, `NumberOfLegs`).

[Click here to view code image](#)

```
class Horse : ILandBound
{
    ...
    public int NumberOfLegs()
    {
        return 4;
    }
}
```

When you implement an interface, you must ensure that each method matches its corresponding interface method exactly, according to the following rules:

+   - The method names and return types match exactly.