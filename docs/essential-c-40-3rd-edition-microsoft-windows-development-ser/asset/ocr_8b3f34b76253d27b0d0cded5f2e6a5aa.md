# Listing 5.29: Calling an Object Initializer

```
class Program
{
    static void Main()
    {
        List<Employee> employees = new List<Employee>()
        {
            new Employee("Inigo", "Montoya"),
            new Employee("Chuck", "McAtee")
        };
        // ...
    }
}
```

After the assignment of a new collection instance, the compiler-generated code instantiates each object in sequence and adds them to the collection via the Add() method.

# ADVANCED TOPIC

# Finalizers

Constructors define what happens during the instantiation process of a class. To define what happens when an object is destroyed, C# provides the finalizer construct. Unlike destructors in C++, finalizers do not run immediately after an object goes out of scope. Rather, the finalizer executes after an object is last active and before the program shuts down. Specifically, the garbage collector identifies objects with finalizers during a garbage collection cycle, and instead of immediately deallocating those objects, it adds them to a finalization queue. A separate thread runs through each object in the finalization queue and calls the object’s finalizer before removing it from the queue and making it available for the garbage collector again. Chapter 9 discusses this process, along with resource cleanup, in depth.

# Overloading Constructors

Constructors can be overloaded—you can have more than one constructor as long as the number or types of the parameters vary. For example, as