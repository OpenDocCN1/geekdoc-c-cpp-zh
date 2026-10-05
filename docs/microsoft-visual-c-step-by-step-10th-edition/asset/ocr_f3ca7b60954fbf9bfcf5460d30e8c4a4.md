The LinkedList<T> collection class implements a doubly linked list. Each item in the list holds the value for that item together with a reference to the next item in the list (the Next property) and the previous item (the Previous property). The item at the start of the list has the Previous property set to null, and the item at the end of the list has the Next property set to null.

Unlike the List<T> class, LinkedList<T> doesn't support array notation for inserting or exchanging elements. You can use the AddFirst method to insert an element at the start of the list, moving the first item up and setting its Previous property to refer to the new item. Similarly, you can use the AddLast method to insert an element at the end of the list, setting the Next property of the previously last item to refer to the new item. You can also use the AddBefore and AddAfter methods to insert an element before or after a specified item in the list. (You must retrieve the first item.)

You can find the first item in a LinkedList<T> collection by querying the First property, and querying the Last returns a reference to the final item in the list. To iterate through a linked list, you can start at one end and step through the Next or Previous references until you find an item with a null value for this property. Additionally, you can use a foreach statement, which iterates through a LinkedList<T> by using the Remove, RemoveFirst, and RemoveLast methods.

The following example shows how LinkedList<T> collection in action. Notice how the code iterates through the list by using a for statement through the Next (or Previous) references, stopping only when it reaches a null reference, which is the end of the list:

Click here to view code image

```
using System;
using System.Collections.Generic;
nLinkedList<int> numbers = new LinkedList<int>();
// Fill the List<int> by using the AddFirst method
foreach (int number in new int[] { 10, 8, 6, 4, 2 })
{
    numbers.AddFirst(number);
}
// Iterate using a for statement
```