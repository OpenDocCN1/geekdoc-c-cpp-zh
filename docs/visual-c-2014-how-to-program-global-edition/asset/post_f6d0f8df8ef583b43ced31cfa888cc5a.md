
# Chapter 12 OOP: Polymorphism and Interfaces

The IPayable interface reference payable, even though ToString is declared in interface IPayable—all references (including those of interface types) refer to objects of classes that extend object and have a ToString method. Line 27 invokes IPayable method GetPaymentAmount to obtain the payment amount for each object in payableObjects, regardless of the actual type of the object. The output reveals that the method calls in lines 25 and 27 invoke the class's implementation of ToString and GetPaymentAmount.

# Software Engineering Observation 12.9

All methods of object class can be called using a reference of an interface type—the reference to it, and all objects inherit the methods of class object.

```csharp
// Fig. 12.14: PayableInterfaceTest.cs
// Tests IPayable with disparate classes.
using System;
using System.Collections.Generic;

class PayableInterfaceTest
{
    static void Main()
{
        // Create a List<IPayable> and initialize it with four
        // objects of classes that implement interface IPayable
        var payableObjects = new List<IPayable>() {
            new Invoice("01234", "seat", 2, 375.00),
            new Invoice("06789", "tire", 4, 79.95),
            new SalaryEmployee("John", "Smith", "111-1111", 800.00),
            new SalaryEmployee("Lisa", "Barnes", "888-8888", 120.00));
        };

        Console.WriteLine("Invoices and Employees processed polymorphically:\n");

        // generally process each element in payableObjects
        foreach (var payable in payableObjects)
        {
            // output payable and its appropriate payment amount
            Console.WriteLine($"{payable}");
            Console.WriteLine($"{payment due: {payable.GetPaymentAmount()}:C\n}");
        }
    }
}
```

Fig. 12.14 | Tests interface IPayable with disparate classes (Part I of 2).

# 12.7 Case Study: Creating and Using Interfaces

invoice:
- part number: 56789 (tire)
- quantity: 4
- price per item: $79.95
- payment due: $319.00

salaried employee: John Smith
- social security number: 111-11-1111
- weekly salary: $800.00
- payment due: $800.00

salaried employee: Lisa Barnes
- social security number: 888-88-8888
- weekly salary: $1,200.00
- payment due: $1,200.00

Fig. 12.14 | Tests interface IPayable with disparate classes (Part 2 of 2)

# 12.7.6 Common Interfaces of the .NET Framework Class Library

In this section, we overview several common interfaces defined in the .NET Framework Class Library. These interfaces are implemented and used in the same manner as those you create (e.g., IPayable in Section 12.7.2). Implementing interfaces enables you to incorporate objects of your own types into many important aspects of the Framework Class Library. Figure 12.15 overviews commonly used Framework Class Library interfaces and why you might implement them in your own types.

| Interface | Description |
|---|---|
| IComparable | C# contains several comparison operators (e.g., <, <=, >, >=, !=) that allow you to compare simple-type values. Section 10.13 shows that you could overload these operators for your own types. Interface IComparable is used to allow objects of a class that implements the interface to be compared to one another. The interface contains one method, CompareTo, which compares the object that calls the method to the object passed as an argument. Classes must implement CompareTo to return a value indicating whether the object is less (negative return value), equal to (0 return value) or greater (positive return value) the object passed as an argument, using any criteria. For example, if Employee implements IComparable, its CompareTo method could compare employee objects by their earnings amounts. IComparable is commonly used for ordering objects in a collection such as an array. We see IComparable in Chapter 20, Generics, and Chapter 21, Generic Collections; Functional Programming with LINQ/PLINQ. |
| IComponent | Implemented by any class that represents a component, including Graphical User Interface (GUI) controls (such as buttons or labels). Interface IComponent defines the behaviors that components must implement. We discuss IComponent and many GUI controls that implement this interface in Chapter 14, Graphical User Interfaces with Windows Forms: Part 1, and Chapter 15, Graphical User Interfaces with Windows Forms: Part 2 |

Fig. 12.15 | Common interfaces of the .NET Framework Class Library. (Part 1 of 2)

![](img/57baed2319be0bb1b5f98674846f2711_542_0.png)

# Chapter 12 OOP: Polymorphism and Interfaces

| Interface | Description |
|---|---|
| IDisposable | Implemented by classes that must provide an explicit mechanism for releasing resources. Some resources can be used by only one program at a time. In addition, some resources, such as files on disk, are unmanaged resources that, unlike memory, cannot be released by the garbage collector. Classes that implement interface IDisposable provide a Dispose method that can be explicitly called to release resources that are explicitly associated with an object. We discuss this properly in Chapter 13, Exception Handling: A Deeper Look. You can learn more about this interface at http://msdn.microsoft.com/library/system.idisposable. The MSDN Implementing a Dispose Method at http://microsoft.com/library/fs2kftw discusses the proper implementation of this interface in your classes. |
| Enumerator | Used for iterating through the elements of a collection (such as an array or a List) one at a time—the statement uses an IEnumerator to iterate through them. Interface IEnumerator contains method MoveNext, Reset to move to the position before the first element and property Current to return the object at the current location. We use IEnumerator in Chapter 21. All IEnumerable objects have a GetEnumerator method that returns an IEnumerator object. |

# 12.8 Wrap-Up

This chapter introduced polymorphism—the ability to process objects that share the same base class in a class hierarchy as if they were all objects of the base class. We discussed how polymorphism makes systems extensible and maintainable, then demonstrated how to use overridden methods to achieve polymorphic behavior. We introduced the notion of an abstract class, which allows you to define a base class for subclasses. We also learned that interfaces provide a way to define behavior without specifying implementation. This chapter showed how polymorphism allows us to treat different objects through a common interface or base class reference.
