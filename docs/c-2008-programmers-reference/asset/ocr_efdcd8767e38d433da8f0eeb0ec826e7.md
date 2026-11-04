The next example shows how to use the LinkedList<T> class available in the .NET Framework to store a list of random numbers. As each random number is generated, it is inserted into the linked list in numeric sorted order (from small to big). The end result is a list of sorted random numbers. Specifically, the example uses the LinkedList<T> class members shown in the following table.

| Member | Description |
| --- | --- |
| AddAfter() | Adds a new node after an existing node |
| AddBefore() | Adds a new node before an existing node |
| First | Gets the first node |
| Last | Gets the last node |

Each node in the LinkedList<T> class is an object of type LinkedListNode<T>. The following table shows the properties in the LinkedListNode<T> that are used in this example.

| Property | Description |
| --- | --- |
| Next | Gets the next node |
| Previous | Gets the previous node |
| Value | Gets the value contained in the node |

Now for the example, first create an instance of the LinkedList<T> class using the int type:

```
```csharp
LinkedList<int> Numbers = new LinkedList<int>();
```
```

Define the InsertNumber() function, which accepts an int parameter:

```
```csharp
private void InsertNumber(int number)
{
    //--start from first node---
    LinkedListNode<int> currNode = Numbers.First;
    LinkedListNode<int> newNode = new LinkedListNode<int>(number);

    if (currNode == null)
    {
        Numbers.AddFirst(newNode);
        return;
    }
    while (currNode != null)
    {
        if (currNode.Value > number)
        {
            if (currNode.Previous != null)
                //--Case 1 - add the node to the previous node---
                Numbers.AddAfter(currNode.Previous, newNode);
```
```