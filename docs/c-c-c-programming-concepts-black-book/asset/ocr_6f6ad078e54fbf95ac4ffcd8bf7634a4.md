Listing 18.37: Showing an Example of Explicit Interface

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        GUIClass gui = new GUIClass();
        //Explicitly cast the IWin interface
        ((IWin)gui).GetMenu();
        //Explicitly cast the IOther interface
        ((IOther)gui).GetMenu();
    }
}
interface IWin
{
    void GetMenu();
}
interface IOther
{
    void GetMenu();
}
class GUIClass: IWin, IOther
{
    //Explicit definition of the methods of two interfaces
    void IWin.GetMenu()
    {
        Console.WriteLine("Windows menu is called");
    }
    void IOther.GetMenu()
    {
        Console.WriteLine("Other menu is called");
    }
}
```
```

In Listing 18.37, we have defined the two interfaces, IWin and IOther, where both the interfaces declare the same method called GetMenu(). Next, we have declared a class named GUIClass where we have explicitly defined the methods of the two interfaces. The Main() method declared inside the Program class calls the interface methods by casting the interface to the class instance; thereby, allowing type safety. It is a good practice to use the explicit interface when a program deals with more than one interface definitions. The output of the preceding program is given as follows:

```
```
windows menu is called
Other menu is called
```
```

Let's now learn about enumerators in C#.

# Enumerators

Enumeration is a strongly typed constant whose underlying type is integral. Enumerators are used to group some constants to define definite properties of an object whose underlying type will be defined by a user. While handling the enumerators, we need to know the following important points:

+   - Underlying type of an enumerator can be any integral type except char.
+   - Enumerator of one type cannot be implicitly assigned to the enumerator of another type even though the underlying members are same. That's why it is called strongly typed.
+   - Enumerators cannot be inherited as it is a value type and contain their own specific values.
+   - If underlying types are not defined explicitly, then integers starting from 0 are assigned to the members of the enumerator type automatically.