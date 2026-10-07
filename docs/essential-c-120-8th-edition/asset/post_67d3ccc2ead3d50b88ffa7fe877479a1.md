
![](img/ffe0f34eac7523830420733690014d17_872_0.png)

FIGURE 17.2: List<T> class diagrams

## Primary Collection Classes 839

```cs
list.Sort();
Console.WriteLine(
  "In alphabetical order { list[0] } is the "
 + "first dwarf while { list[1] } is the last.");

list.Remove("Grumpy");
}
```

## OUTPUT 17.1

In alphabetical order Bashful is the first dwarf while Sneezy is the last.

C# is zero-index based; therefore, index 0 in Listing 17.1 corresponds to the first element and index 6 indicates the seventh element. Retrieving elements by index does not involve a search. Rather, it entails a quick and simple "jump" operation to a location in memory.

A List<T> is an ordered collection; the Add() method appends the given item to the end of the list. Before the call to Sort() in Listing 17.1, "Sneezy" is first and "Grumpy" is last; after the call, the list is sorted into alphabetical order rather than the order in which items were added. Some collections automatically sort elements as they are added, but List<T> is not one of them; an explicit call to Sort() is required for the elements to be sorted.

To remove an element, you use the Remove() or RemoveAt() method to either remove a given element or remove whatever element is at a particular index, respectively.

## ADVANCED TOPIC

### Customizing Collection Sorting

You might have wondered how the List<T>.Sort() method in Listing 17.1 knew how to sort the elements of the list into alphabetical order. The string type implements the IComparable<string> interface, which has one method, CompareTo(). It returns an integer indicating whether the element passed is greater, less, than, or equal to the current element. If the element type implements the generic IComparable<T> interface (or the generic IComparable interface), the sorting algorithm will, by default, use it to determine the sorted order.

But if either the element type does not implement IComparable<T> or the default logic for comparing two things does not meet your needs? You can call the overload of List<T>.Sort(), which takes IComparer<T> as an argument.

The difference between IComparable<T> and IComparer<T> is subtle but important. This first interface, “I know how to compare myself to another instance of my type.” The latter means, “I know how to compare two things of a given type.”

The IComparable interface is typically used when there are many different ways to sort a data type and not obviously the best. For example, you might have a collection of Contact objects that you sometimes want to sort by name, by location, by birthday, by geographic region, or by any number of other possibilities. Rather than choosing a sorting strategy and making the Contact class implement IComparable<Contact>, it might be wiser to create several different classes that implement IComparer<Contact>. Listing 17.2 shows a sample implementation of a LastName, FirstName comparison.

## Listing 17.2: Implementing IComparer<T>

```cs
using System;
using System.Collections.Generic;
// ...
public class Contact
{
    public string FirstName { get; private set; }
    public string LastName { get; private set; }

    public Contact(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }
}

public class NameComparison : IComparer<Contact>
{
    public int Compare(Contact? x, Contact? y)
    {
        if (Object.Equals(x, y))
            return 0;
        if (x == null)
            return 1;
        if (y == null)
            return -1;
        int result = StringCompare(x.LastName, y.LastName);
        if (result == 0)
            result = StringCompare(x.FirstName, y.FirstName);
        return result;
    }

    private static int StringCompare(string? x, string? y)
    {
        if (Object.Equals(x, y))
            return 0;
        if (x == null)
            return 1;
        if (y == null)
            return -1;
        return x.CompareTo(y);
    }
}
```

To sort a List<Contact> by last name and then first name, you can call contact.Sort(new NameComparison());

## Total Ordering

You are required to produce a total order when implementing IComparable<T> or IComparer<T>. Your implementation of CompareTo must provide a fully consistent ordering for any pair of items. For example, every element is required to be equal to itself. If an element X is considered equal to element Y, and element Y is considered equal to element Z, then all three X, Y, and Z must be considered equal to another. If an element X is considered greater than Y, Y must be considered less than X. And there must be no “transitivity paradoxes”—that is, you cannot have X greater than Y, Y greater than Z, and Z greater than X. If you fail to provide a total ordering, the action of the sort algorithm is undefined; it may produce a crazy ordering, it may crash, it may go into an infinite loop, and so on.

Notice, for example, how the comparer in Listing 17.2 ensures a total order even if the elements are null. It would not be legal to say, "If element is null, return zero," for example, because two non-null things could be equal but not equal to each other.

> Guidelines: ensure that custom comparison logic produces a consistent “total order.”

## Searching a List<T>

To search List<T> for a particular element, you use the Contains(), IndexOf(), LastIndexOf(), and BinarySearch() methods. The first three methods search through the array, starting at the first element (or the last element for LastIndexOf()), and examine each element until the desired is found. The execution time for these algorithms is proportional to the number of elements searched. (Be aware that the collection classes do not require all the elements within the collection are unique. If two or more elements in the collection are the same, IndexOf() returns the first index and LastIndexOf() returns the last index.)

BinarySearch() uses a much faster search algorithm that requires the elements be sorted. A useful feature of the BinarySearch() method is that if the element is not found, a negative index is returned. The bitwise complement (~) of this value is the index of the next element larger than the sought, or the total element count if there is no greater value. This provides a convenient means to insert new values into the list at the specific location to maintain sorting. Listing 17.3 provides an example.

Beware that if the list is not sorted, this code will not necessarily find an element, even if it is in the list. The results of Listing 17.3 appear in Output 17.2.

## Listing 17.3: Using the Bitwise Complement of the BinarySearch() Result

```cs
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<string> list = new();
        int search;

        list.Add("public");
        list.Add("protected");
        list.Add("private");

        list.Sort();

        search = list.BinarySearch("protected internal");
        if (search < 0)
        {
            list.Insert(~search, "protected internal");
        }

        foreach (string accessModifier in list)
        {
            Console.WriteLine(accessModifier);
        }
    }
}
```

## OUTPUT 17.2

```
private
protected
protected internal
public
```

## ADVANCED TOPIC

### Finding Multiple Items with FindAll()

Sometimes you must find multiple items within a list, and your search criteria are more complex than merely looking for specific values. To support this scenario, System.Collections.Generic.List<T> includes a FindAll() method.
FindAll takes a parameter of type Predicate<T>, which is a delegate (a reference to a method). Listing 17.4 demonstrates how to use the FindAll() method.

## Listing 17.4: Demonstrating FindAll() and its Predicate Parameter

```cs
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        List<int> list = new();
        list.Add(1);
        list.Add(2);
        list.Add(3);
        list.Add(2);

        List<int> results = list.FindAll(Even);

        foreach (int number in results)
        {
            Console.WriteLine(number);
        }
    }
    public static bool Even(int value) =>
        (value % 2) == 0;
}
```
