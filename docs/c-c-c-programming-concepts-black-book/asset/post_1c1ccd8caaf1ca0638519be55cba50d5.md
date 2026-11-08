
C# implements enumeration with the help of the Enum class and the enum keyword. The Enum class provides the methods to manipulate the instances of the class. Enumeration technique provides an efficient way to define a set of integral constants that may be assigned to a variable using the enum type. Each element in enum is associated with an underlying type which is by default integer. In this section, we discuss about the implementation of enumerator in .NET using the enum type.

### Listing 18.38: Showing an Example of Enumerator

```csharp
using System;
class Enumeration
{
    // Defining enum
    public enum SortingOrder
    {
        Ascending,
        Descending,
        NotDefined
    }
    public static void Main()
    {
        // Type casting the enum variable
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

In the preceding code, the keyword enum is used to define a SortingOrder enumerator whose members are Ascending, Descending, and NotDefined. As there is no underlying type defined for the members in the enum, the compiler automatically assigns 0, 1, and 2 to the enum members. In other words, it assigns 0 to Ascending, 1 to Descending, and 2 to NotDefined. In addition, we have defined an enum variable named sortingOrder by using the enum variable sortingOrder that holds the underlying value of the enum member Descending, in the Main() method.

The output of the preceding program is given as follows:

```text
Please sort in Descending order
```

Next, let’s consider another example that shows the importance of type casting in enums, as shown in Listing 18.39:

### Listing 18.39: Implementing Type Casting of Enumerators

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
    {
        High = 100,
        Low = 10
    }
    public static void Main()
    {
        // Type casting to avoid conflict
        Type flammable = typeof(Flammable);
        Type speedLimit = typeof(SpeedLimit);
        // Printing the Enums
        foreach (string flammableEnum in Enum.GetNames(flammable))
        {
            Console.WriteLine("The flammable enums are:" + flammableEnum);
        }
        foreach (string speedLimitEnum in Enum.GetNames(speedLimit))
        {
            Console.WriteLine("The speed limit enums are:" + speedLimitEnum);
        }
    }
}
```

In the preceding program, the members of the two enums as well as their underlying types are same, but the values are different. The maximum speed limit is 100 (km/hr) and the minimum speed limit is 10 (km/hr); whereas, the underlying value of High and Low for a flammable object is 0 and 1, respectively. The output of the preceding program is given as follows:

```text
The flammable enums are:High
The flammable enums are:Low
The speed limit enums are:Low
The speed limit enums are:High
```

Now, if we simply write the preceding program where we use the member High without applying type casting, then this will give an error, as there exists two values for this member, as shown in Listing 18.40:

### Listing 18.40: Showing an Ambiguous Implementation of Enumeration

```csharp
using System;
class EnumOperation
{
    public enum Flammable
    {
        High,
        Low
    }
    public enum SpeedLimit
    {
        High = 100,
        Low = 10
    }
    public static void Main()
    {
        Console.WriteLine("The highest member value of SpeedLimit enum is" + High);
    }
}
```

Therefore, we should always type cast the members of the enum to avoid the error.

As shown in Listing 18.39, we have used the class Enum to get the list of names of the member variables. The Enum class belongs to Base Class Library (BCL).

### Table 18.2: Noteworthy Member Methods of the Enum Class

| Member Method | Description |
|---|---|
| Equals (object obj1, object obj2) | Determines whether the passed two object instances are similar. If they are similar, then it returns true, else it returns false. |
| Format(Type enumType, Object obj, string format) | Converts the obj of enumType to the specific format passed as an argument and then returns the string type of the object that has been converted. |
| GetName(Type enumType, Object obj) | Returns the name of object of enumType specified in the argument list. |
| GetNames(Type enumType) | Returns an array of string containing the names of the specific enumType specified in the argument. |
| GetUnderlyingType(Type enumType) | Returns an instance of Type, which contains the underlying type of the enumType specified in the argument. |
| GetValues(Type enumType) | Returns an object of Array class that contains the list of constant values associated with the enumType specified in the argument. |
| IsDefined(Type enumType, Object obj) | Returns true if the constant value has been defined for the specific Object type of the enumType specified in the argument. |
| Parse(Type enumType, Object obj) | Converts the name or the constant of the enumType to an equivalent enumerated object and returns that object at the end.<br>Overloads:<br>• Parse (Type enumType, Object obj, bool ignoreCase)➔Ignores the case if ignoreCase is set to true. |
| ReferenceEquals (object obj1, object obj2) | Returns true if all the instances of the objects are of same object; otherwise, returns false. |
| ToObject (Type enumType, ulong value) | Returns an object of the enumeration type set to the specified 64-bit unsigned integer value.<br>Overloads:<br>• ToObject (Type enumType, byte value)➔Returns an instance of enumeration type set to the specified 8-bit unsigned integer value.<br>• ToObject (Type enumType, int value)➔Returns an instance of enumeration type set to the specified 32-bit signed integer value.<br>• ToObject (Type enumType, long value)➔Returns an instance of enumeration type set to the specified 64-bit signed integer value.<br>• ToObject (Type enumType, object value)➔Returns an instance of enumeration type set to object type value.<br>• ToObject (Type enumType, sbyte value)➔Returns an instance of enumeration type set to the specified 8-bit signed integer value.<br>• ToObject (Type enumType, short value)➔Returns an instance of enumeration type set to the specified 16-bit signed integer value.<br>• ToObject (Type enumType, uint value)➔Returns an instance of enumeration type set to the specified 32-bit unsigned integer value.<br>• ToObject (Type enumType, ushort value)➔Returns an instance of enumeration type set to the specified 16-bit unsigned integer value. |

Let’s now learn about generics in C#.

## Generics

In the previous chapter, we have already learned about array and ArrayList as well as how they work in the .NET platform. Therefore, ArrayList is an object-based data structure. However, the main problem with this sort of data structure is that we need to box it to Object type before inserting the value-type element and then unbox it to retrieve the exact type of element. This reduces the performance of the program as boxing and unboxing incur a significant performance penalty, as it creates more pressure on the managed heap; thereby, resulting in more garbage collection. Therefore, we can say that ArrayList is not type safe. On the other hand, Array is type safe, but the array size is restricted; whereas, there is no size limit in ArrayList. Therefore, both Array and ArrayList have their own advantages and disadvantages. In C#, Generics combine the advantages of both array and ArrayList that provide a type safe collection to a user.

In this section, we will cover the generic collection of Dictionary. To access the collection, we need to add the following assembly reference in a program:

```csharp
using System.Collections.Generic;
```

Using this reference, we can implement the collections, such as `List<T>` and `Dictionary<Key, Value>`. A List can be declared as follows, where T represents type:

```csharp
List<T> list = new List<T>();
```

If we want to create a List that contains a string, then we can declare it as follows:

```csharp
List<string> list = new List<string>();
```

On the other hand, the Dictionary collection represents a key-value list that has a key for all the text defined. We can declare the Dictionary collection as follows:

```csharp
Dictionary<key, value> list = new Dictionary<key, value>();
```

### Listing 18.41: Showing an Example of Dictionary Collection

```csharp
using System;
using System.Collections.Generic;
class Program
{
    public static void Main()
    {
        // Declaring the generic Dictionary
        Dictionary<int, Customer> customerList = new Dictionary<int, Customer>();
        CustomerIndexer customers = new CustomerIndexer();
        customers[0] = new Customer(10, "Customer_1");
        customers[1] = new Customer(20, "Customer_2");
        customers[2] = new Customer(30, "Customer_3");
        // Adding the customer information to Dictionary object
        for (int i = 0; i < 3; i++)
        {
            customerList.Add(i + 1, customers[i]);
        }
        Console.WriteLine("The customers are:");
        // Printing the Dictionary content
        foreach (KeyValuePair<int, Customer> custKeyVal in customerList)
        {
            Console.WriteLine("Customer ID: {0}, Name: {1}",
                custKeyVal.Key,
                custKeyVal.Value.custName);
        }
    }
    class Customer
```
