```
SortedList s = new SortedList();
s.Add(0, "Hi");
s.Add(3, "Sorted List");
s.Add(6, "F");
s.Add(1, "This");
s.Add(5,1.25);
s.Add(4, 1);
s.Add(2, "is");
Console.WriteLine("Printing the elements of a sorted list....");
foreach (DictionaryEntry var in s)
{
    Console.WriteLine(var.Value);
}
```

In the preceding program, we have first instantiated an object of the SortedList class that stores its content in a name-value pair. Therefore, whenever we add an element in SortedList, we need to specify a number that corresponds to the value in the name-value pair and a value against the number that corresponds to the name in the name-value pair. The number specifies the position of the element in the list. If the number is 0, then it will be the first element in the list. In the preceding program, we randomly add different types of elements and at the end, all the elements are printed in a sorted manner. The output of the program is given as follows:

```
Printing the elements of a sorted list....
Hi
This
is
Sorted List
1
1.25
F
```

# Hash Table

Hash table represents a key-value collection where a key maps to its value. This data structure is important in implementing the search functionality to make it easier and faster. C# provides the Hashtable class, which has the functionalities to manipulate the hash table elements easily. Listing 17.30 shows the various functionalities of hash table using the Hashtable class:

# Listing 17.30: Showing the Usage of the Hashtable Class

```
using System;
using System.Collections;
class Program
{
    public static void Main()
    {
        Hashtable direction = new Hashtable();
        direction.Add(1, "North");
        direction.Add(2, "South");
        direction.Add(3, "East");
        direction.Add(4, "West");
        //Displaying the first element of the hash table
        Console.WriteLine("Printing the first element of the hash table....");
        Console.WriteLine(direction[1].ToString());
        //Search for an item in hash table
        if (direction.ContainsValue("South"))
        {
```