# **SortedDictionary's Values Property**

If you do not need the keys, class SortedDictionary also provides a read-only Values property that gets an ICollection<T> of all the values stored in the SortedDictionary. You could use this property to iterate through the values stored in the SortedDictionary without regard for their corresponding keys.

# ## 19.5 Generic LinkedList Collection

Section 9.4 introduced the generic List<T> collection, which defines an array-based list implementation. Here, we discuss class LinkedList<T>, which defines a doubly linked list that an app can navigate both forwards and backwards. A LinkedList<T> contains nodes of generic class LinkedListNode<T>. Each node contains property Value and read-only properties Previous and Next. The Value property's type matches LinkedList<T>'s single type parameter because it contains the data stored in the node. Previous gets a reference to the preceding node in the linked list (or null if the node is the first of the list). Similarly, Next gets a reference to the subsequent reference in the linked list (or null if the node is the last of the list). We demonstrate a few linked-list manipulations in Fig. 19.5.

```
```csharp
// Fig. 19.5: LinkedListTest.cs
// Using LinkedLists.
using System;
using System.Collections.Generic;

class LinkedListTest
{
   private static readonly string[] colors =
      { "black", "yellow", "green", "blue", "violet", "silver" };
   private static readonly string[] colors2 =
      { "gold", "white", "brown", "blue", "gray" };

   // set up and manipulate LinkedList objects
   static void Main()
   {
      var list1 = new LinkedList<string>();

      // add elements to first linked list
      foreach (var color in colors)
      {
         list1.AddLast(color);
      }

      // add elements to second linked list via constructor
      var list2 = new LinkedList<string>(colors2);

      Concatenate(list1, list2); // concatenate list2 onto list1
      PrintList(list1); // display list1 elements

      Console.WriteLine("\nConverting strings in list1 to uppercase\n");
      ToUppercaseStrings(list1); // convert to uppercase string
```
```

**Fig. 19.5** | Using LinkedLists. (Part 1 of 3.)