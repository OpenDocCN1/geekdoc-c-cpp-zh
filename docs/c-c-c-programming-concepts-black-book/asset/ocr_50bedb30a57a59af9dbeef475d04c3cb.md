C# implements enumeration with the help of the Enum class and the enum keyword. The Enum class provides the methods to manipulate the instances of the class. Enumeration technique provides an efficient way to define a set of integral constants that may be assigned to a variable using the enum type. Each element in enum is associated with an underlying type which is by default integer. In this section, we discuss about the implementation of enumerator in .NET using the enum type.

Listing 18.38 shows an example of enumerator:

# Listing 18.38: Showing an Example of Enumerator

```
```csharp
using System;
class Enumeration
{
    //Defining enum
    public enum SortingOrder
    {
        Ascending,
        Descending,
        NotDefined
    }
    public static void Main()
    {
        //Type casting the enum variable
        SortingOrder sortingorder = SortingOrder.Descending;
        switch (sortingorder)
        {
            case SortingOrder.Ascending:
                Console.WriteLine("Please sort in Ascending order");
                break;
            case SortingOrder.Descending:
                Console.WriteLine("Please sort in Descending order");
                break;
            case SortingOrder.NotDefined:
                Console.WriteLine("Please provide the sorting order");
                break;
        }
    }
}
```
```

In the preceding code, the keyword enum is used to define a SortingOrder enumerator whose members are Ascending, Descending, and NotDefined. As there is no underlying type defined for the members in the enum, the compiler automatically assigns 0, 1, and 2 to the enum members. In other words, it assigns 0 to Ascending, 1 to Descending, and 2 to NotDefined. In addition, we have defined an enum variable named sortingOrder by using the enum variable sortingOrder that holds the underlying value of the enum member Descending, in the Main() method.

The output of the preceding program is given as follows:

```
```text
Please sort in Descending order
```
```

Next, let’s consider another example that shows the importance of type casting in enums, as shown in Listing 18.39:

# Listing 18.39: Implementing Type Casting of Enumerators

```
```csharp
using System;
class Enumeration
{
    public enum Flammable
    {
        High,
        Low
    }
    public enum SpeedLimit
```
```