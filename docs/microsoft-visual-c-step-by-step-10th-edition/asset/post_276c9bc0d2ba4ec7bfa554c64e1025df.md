
the element, although you can't use array notation to add new elements. However, in general, the List<T> class provides more flexibility than arrays do and is designed to overcome the following restrictions exhibited by arrays:

- If you want to resize an array, you must create a new array, copy the elements (leaving out some if the array is smaller), and then update references to the original array so that they refer to the new array.
- If you want to remove an element from an array, you must move all the trailing elements up by one place. Even this doesn't work because you end up with two copies of the last element.
- If you want to insert an element into an array, you must move elements down by one place to make a free slot. However, you lose the last element of the array!

The following features of the List<T> collection address these limitations:

- You don't need to specify the capacity of a List<T> collection you create; it can grow and shrink as you add elements. There's an overhead associated with this dynamic behavior, and if necessary, you can specify an initial size. However, if you exceed this size, the List<T> collection simply grows as necessary.
- You can remove a specified element from a List<T> collection by using the Remove method. The List<T> collection automatically reorders its elements and closes the gap. You can also remove an item at a specified position in a List<T> collection using the RemoveAt method.
- You can add an element to the end of a List<T> collection by using its Add method. You supply the element to be added. The List<T> collection resizes itself automatically.
- You can insert an element into the middle of a List<T> collection by using the Insert method. Again, the List<T> collection resizes itself.
- You can easily sort the data in a List<T> object by calling the Sort method.

> Note
As arrays, if you use foreach to iterate through a List<T> collection, you cannot use the iteration variable to modify the contents of collection. Additionally, you cannot call the Remove, Add, or Insert method in a foreach loop that iterates through a List<T> collection; any attempt to do so results in an InvalidOperationException exception.

Here’s an example of how you can create, manipulate, and iterate through the contents of a List<int> collection:

Click here to view code image

```
using System;
using System.Collections.Generic;
...
List<int> numbers = new List<int>();
// Fill the List<int> by using the Add method
foreach (int number in new int[12]{10, 9, 8, 7, 6, 5, 10, 4, 3, 2, 1})
{
    numbers.Add(number);
}

// Insert an element in the penultimate position in the list, and move
// last item up
// The first parameter is the position; the second parameter is the
// value being inserted
numbers.Insert(numbers.Count-1, 99);

// Remove the first element whose value is 7 (the 4th element, index)
numbers.Remove(7);

// Remove the element that’s now the 7th element
numbers.RemoveAt(6);

// Iterate the remaining 11 elements using a for statement
Console.WriteLine("Iterating using a for statement:");
for (int i = 0; i < numbers.Count; i++)
{
    int number = numbers[i]; // Note the use of array syntax
    Console.WriteLine(number);
}

// Iterate the same 11 elements using a foreach statement
Console.WriteLine("\nIterating using a foreach statement:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

Here’s the output of this code:

Click here to view image

Iterating using a for statement:
10
9
8
7
6
5
4
3
2
99
1

Iterating using a foreach statement:
10
9
8
7
6
5
4
3
2
99
1

> Note
The way you determine the number of elements for a List<T> collection is different from querying the number of items in an array. When using a List<T> collection, you examine the Count property; when using an array, you examine the Length property.

# The LinkedList<T> collection class

The LinkedList<T> collection class implements a doubly linked list. Each item in the list holds the value for that item together with a reference to the next item in the list (the Next property) and the previous item (the Previous property). The item at the start of the list has the Previous property set to null, and the item at the end of the list has the Next property set to null.

Unlike the List<T> class, LinkedList<T> doesn't support array notation for inserting or exchanging elements. You can use the AddFirst method to insert an element at the start of the list, moving the first item up and setting its Previous property to refer to the new item. Similarly, you can use the AddLast method to insert an element at the end of the list, setting the Next property of the previously last item to refer to the new item. You can also use the AddBefore and AddAfter methods to insert an element before or after a specified item in the list. (You must retrieve the first item.)

You can find the first item in a LinkedList<T> collection by querying the First property, and querying the Last returns a reference to the final item in the list. To iterate through a linked list, you can start at one end and step through the Next or Previous references until you find an item with a null value for this property. Additionally, you can use a foreach statement, which iterates through a LinkedList<T> by using the Remove, RemoveFirst, and RemoveLast methods.

The following example shows how LinkedList<T> collection in action. Notice how the code iterates through the list by using a for statement through the Next (or Previous) references, stopping only when it reaches a null reference, which is the end of the list:

Click here to view code image

```
using System;
using System.Collections.Generic;
LinkedList<int> numbers = new LinkedList<int>();
// Fill the List<int> by using the AddFirst method
foreach (int number in new int[] { 10, 8, 6, 4, 2 })
{
    numbers.AddFirst(number);
}
// Iterate using a for statement
```
Console.WriteLine("Iterating using a for statement:");
for (LinkedList<int> node = numbers.First; node != null; node = node.Next)
{
    Console.WriteLine(node.Value);
}

// Iterate using a foreach statement
Console.WriteLine("\nIterating using a foreach statement:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}

// Iterate backward
Console.WriteLine("\nIterating backward:");
for (LinkedList<int> node = numbers.Last; node != null; node = node.Previous)
{
    Console.WriteLine(node.Value);
}
```

Here’s the output of this code:

Click here to view image

Iterating using a for statement:
10
8
6
4
2

Iterating using a foreach statement:
10
8
6
4
2

Iterating backward:
2
4
6
8
10

# The Queue<T> class

The Queue<T> class implements a first-in, first-out mechanism. An element is inserted into the queue at the back (the Enqueue operation) and is removed from the front (the Dequeue operation).

The following code is an example showing a Queue<int> and its common operations:

Click here to view image

```
using System;
using System.Collections.Generic;

Queue<int> numbers = new Queue<int>();

// fill the queue
Console.WriteLine("Populating the queue:");
foreach (int number in new int[]{9, 3, 7, 2})
{
    numbers.Enqueue(number);
    Console.WriteLine($"{number} has joined the queue");
}

// iterate through the queue
Console.WriteLine("\nThe queue contains the following items:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}

// empty the queue
Console.WriteLine("\nDraining the queue:");
while (numbers.Count > 0)
{
    int number = numbers.Dequeue();
    Console.WriteLine($"{number} has left the queue");
}
```

Here’s the output from this code:

Click here to view image

Populating the queue:
9 has joined the queue
3 has joined the queue
7 has joined the queue
2 has joined the queue
The queue contains the following items:
9
3
7
2

Draining the queue:
9 has left the queue
3 has left the queue
7 has left the queue
2 has left the queue

# The PriorityQueue<TElement, TPriority> collection class

The PriorityQueue<TElement, TPriority> extends the idea of the Queue<T> class to associate a priority with each queued element. The class takes two parameters: the first is the type of the elements that are queued, and the second indicates the type for the priority (commonly an int, but it can be any comparable). Elements are enqueued at the back of the queue but can be dequeued earlier than longer-lived elements if they have a higher priority. All elements with the same priority are enqueued and dequeued in the same order, as for a regular queue.

The following code shows an example, illustrating how elements with different priorities are enqueued and dequeued. Elements with a lower-priority value have a higher priority (elements with priority 1 are dequeued before those with priority 2):

Click here to view code image

```
using System;
using System.Collections.Generic;
// Create the queue
// The data items are strings. The second type parameter (an int)
indicates the priority
PriorityQueue<string, int> messages = new PriorityQueue<string, int>();

// Add messages with different priorities to the queue
messages.Enqueue("Twas", 1);
messages.Enqueue("Brilling", 1);
messages.Enqueue("and", 2);
messages.Enqueue("the", 3);
messages.Enqueue("Slithy", 2);
```
