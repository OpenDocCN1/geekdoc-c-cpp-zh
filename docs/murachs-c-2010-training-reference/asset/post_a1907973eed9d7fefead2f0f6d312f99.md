
Part 2 of figure 15-7 shows some code that uses the CustomList<> class defined in part 1. To start, the first test creates a CustomList<> class that can store int types, adds two int values to the list, and prints these values to the console. Then, the second test creates a CustomList<> class that can store Product types, adds two Product objects to the list, and prints these objects to the console.

This example shows that the CustomList<> class can store value types (such as int types) or reference types (such as Product types). More importantly, it shows that the CustomList<> class works like the other generic classes defined by the .NET Framework, although it doesn't yet provide as much functionality as any of those classes. Note that the output for this example assumes that the Product class contains a ToString method that returns a string that includes the product's code, description, and price separated by tabs.

# Chapter 15 How to work with interfaces and generics

## Code that uses the CustomList<>

```
// Test 1
Console.WriteLine("List 1 - ints");
CustomList<int> list1 = new CustomList<int>();
int i1 = 11;
int i2 = 7;
list1.Add(i1);
list1.Add(i2);
Console.WriteLine(list1.ToString());

// Test 2
Console.WriteLine("List 2 - Products");
CustomList<Product> list2 = new CustomList<Product>();
Product p1 = new Product("VB10", "Murach's Visual Basic 2010, 54.50m");
Product p2 = new Product("CS10", "Murach's C# 2010, 54.50m");
list2.Add(p1);
list2.Add(p2);
Console.Write(list2.ToString());
```

## Result output

List 1 - ints
11
7

List 2 - Products
VB10 Murach's Visual Basic 2010 $54.50
CS10 Murach's C# 2010 $54.50

## Description

- The generic CustomList<> class works like the generic collection classes of the .NET Framework described in chapter 8.
- The resulting output shown above assumes that the Product class includes a ToString method that displays the product code, description, and price separated by tabs.

![](img/3148667e42d4db35b3d08576aaa1fa01_494_0.png)

## Some of the generic interfaces defined by the .NET Framework

The generic collections of the .NET Framework work with the generic interfaces described in figure 15-8. If you compare these with the interfaces presented in figure 15-2, you'll see that most of these generic interfaces have corresponding regular interfaces. However, the generic interfaces use angle brackets to specify the data type for the interface, just as generic classes use angle brackets to specify the data type for the class. In addition, the generic interfaces are stored in the System.Collections.Generic namespace and were designed to work with the generic collections stored in that namespace.

If you decide to define your own generic collection, such as the CustomList<> class shown in the previous figure, you may want to implement some of these interfaces. For example, if you want to use a foreach loop to iterate through your generic collection, you'll need to implement the IEnumerable<> interface. You'll learn how to do that in figure 15-11. But first, you'll learn how to implement the IComparable<> interface in the next figure.

## A commonly used generic .NET interface

| Interface | Member | Description |
| --- | --- | --- |
| IComparable<T> | int CompareTo(T) | Compares objects of type T |

## Commonly used .NET interfaces for generic collections

| Interface | Members | Description |
| --- | --- | --- |
| IEnumerable<T> | Enumerator<T> GetEnumerator() | Gets an enumerator of type T for the collection. |
| IList<T> | int Count bool IsReadOnly Add(T) SyncRoot void Clear() bool Contains(T) void CopyTo(array, int) bool Remove(T) | Provides basic properties for an enumerable collection. This interface inherits IEnumerable<T>. |
| IList<T> | [int] int IndexOf(T) void Insert(int) void RemoveAt(int) | Manages a basic list of objects. This interface inherits IList<T> and IEnumerable<T>. |
| IDictionary<K, V> | [int] ICollection<K> Keys ICollection<V> Values void Add(K, V) bool ContainsKey(K) bool Remove(K) bool TryGetValue(K, V) | Manages a collection of key/value pairs. This interface inherits ICollection<T> and IEnumerable<T>. |

## Description

- The .NET Framework defines many generic interfaces. These interfaces are particularly useful for working with classes that define generic collections, and they correspond to most of the regular interfaces defined in figure 15-2.
- The IList<T> inherits the IEnumerable<T> interface, which means that any class that implements IList<T> must also implement IEnumerable<T>. Similarly, the IList<T> and IDictionary<K, V> inherit IList<T> and IEnumerable<T>.
- The interfaces for working with generic collections are stored in the System.Collections.Generic namespace.
- This table lists only the most important members of each interface. For a complete description of these interfaces and a list of their members, see the online documentation.

![](img/3148667e42d4db35b3d08576aaa1fa01_496_0.png)

## How to implement the IComparable<> interface

Figure 15-9 shows a Product class that implements the IComparable interface. To start, the declaration for this class indicates that it implements the IComparable interface for the Product type. You would typically want to compare one Product object to another Product object, this makes sense.

Then, this class implements the IComparable interface's only member, the CompareTo method. Since the class specifies an IComparable interface for a Product type, this method compares a parameter of the Product type against the current Product object and returns an int value. For this method properly, this int value should be greater than zero if the current product is greater than the compared product, less than zero if the current product is less than the compared product, and zero if the two products are equal.

To accomplish this task, this method uses the CompareTo method of the String class to compare the Code field for the two Product objects. The CompareTo method of the String class compares the two strings alphabetically the compared string. Conversely, this method typically returns -1 when the current string comes earlier in the alphabet than the compared element. And it returns a 0 when the two strings are the same. As a result, the CompareTo method of the Product class allows you to define a generic collection of Product objects that are sorted alphabetically by their Code fields. You'll see an example of this in the next figure.

The second example shows some code that uses the CompareTo method of the Product class. To start, this code creates two Product objects. The first has a Code field of "VB10", and the second has a Code field of "CS10". Then, this example uses the CompareTo method to compare these two objects. Since the Code field for the first object comes later in the alphabet, the CompareTo method returns an int value of 1. As a result, the if statements in this example print a message to the console that indicates that the first Product object is greater than the second one.

## A class that implements the IComparable<> interface

```
public class Product : IComparable<Product>
{
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }
}
```

// other members

```
#region IComparable<Product>
public int CompareTo(Product other)
{
    return this.Code.CompareTo(other.Code);
}
#endregion
```

## Code that uses the class

```
Product p1 = new Product("VB10", "Murach's Visual Basic 2010", 54.50m);
Product p2 = new Product("CS10", "Murach's C# 2010", 54.50m);
int compareValue = p1.CompareTo(p2);
if (compareValue < 0)
    Console.WriteLine("p1 is greater than p2");
else if (compareValue > 0)
    Console.WriteLine("p1 is less than p2");
else if (compareValue == 0)
    Console.WriteLine("p1 is equal to p2");
```

## Values that can be returned by the CompareTo method

| Value | Meaning |
| --- | --- |
| -1 | The current element is less than the compare element. |
| 0 | The current element is equal to the compare element. |
| 1 | The current element is greater than the compare element. |

## Description

- Since the IComparable<> interface is a generic interface, you can use angle brackets after the IComparable<> interface to identify the type of the objects that are being compared.
- To implement the IComparable<> interface, you must implement the CompareTo method. This method returns an int value that determines if the current element is less than, equal to, or greater than the element that is passed as a parameter of the method.
