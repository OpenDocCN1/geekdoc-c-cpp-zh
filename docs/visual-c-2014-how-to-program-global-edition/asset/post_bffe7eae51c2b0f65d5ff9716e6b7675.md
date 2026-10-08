
The link-reference member stored in the previous node. By convention, the link reference in the last node of a list is set to null to mark the end of the list. Data is stored in a linked list dynamically—that is, each node is created as necessary. A node can contain data of any type, including references to other classes. Stacks and queues are also linear data structures—in fact, they may be viewed as constrained versions of linked lists. Trees are nonlinear data structures.

Lists of data can be stored in arrays, but linked lists provide several advantages. A linked list is preferable when the amount of elements to be represented in the data structure is unpredictable. Unlike a linked list, the size of a conventional C# array cannot be altered, because the array size is fixed at creation time. Conventional arrays can become full, but linked lists become full only when the system has insufficient memory to satisfy dynamic memory allocation.

## Performance Tip 19.1

An array can be declared to contain more elements than the number of items expected, possibly wasting memory. Linked lists provide better memory utilization in these situations, because they grow and shrink at execution time.

Programmers can maintain linked lists in sorted order simply by inserting each new element at the proper point in the list (locating the insertion point does take time). They do not need to move existing elements.

## Performance Tip 19.2

The elements of an array are stored contiguously in memory to allow immediate access to any array element—the address of any element can be calculated directly from its index. Linked lists do not afford such access to their elements—an element can be accessed only by traversing the list.

Normally linked-list nodes are not stored continuously in memory. Rather, the nodes are logically contiguous. Figure 19.3 illustrates a linked list with several nodes. Note that the reference lastNode is not required to implement a linked list—it's an optimization that enables fast access to a linked list's last element.

## Performance Tip 19.3

Using linked data structures and dynamic memory allocation (instead of arrays) for structures that grow and shrink at execution time can save memory. Keep in mind, however, that reference links occupy space, and dynamic memory allocation incurs the overhead of method calls.

![](img/57baed2319be0bb1b5f98674846f2711_816_0.png)

Fig. 19.3 | Linked list graphical representation.

## 19.4 Linked Lists

### Linked-List Implementation

Figures 19.4–15 use an object of our List class to manipulate a list of miscellaneous objects. ClassTest's Main method (Fig. 19.5) creates of objects, inserts objects at the beginning of the list using List method InsertFront, inserts at the end of the list using List method InsertBack, deletes objects from the front of the list using List method RemoveFront. After each insert and delete operation, the program invokes List method Display to output the list contents. If an attempt is made to remove an item from the list, an EmptyListException occurs. A detailed discussion of the program follows.

## Performance Tip 19.4

Insertion and deletion in a sorted array can be consuming—all the elements inserted or deleted element must be shifted appropriately.

The program consists of four classes—Node (Fig. 19.4, lines 8–27), List (lines 30–161), EmptyListException (lines 164–170) and ListTest (Fig. 19.5). The classes in Fig. 19.4 create a linked-list library (in namespace LinkedLibrary) that can be reused throughout this chapter. You should place the code of Fig. 19.4 in its own class project, as we describe in Section 15.13.

```
// Fig. 19.4: LinkedList.cs
// Node, List and EmptyAccessException class declarations.
using System;
namespace LinkedListLibrary
{
    // class to represent one node in a list
    class Node
    {
        // automatic read-only property Data
        public object Data { get; private set; }
        // automatic property Next
        public Node Next { get; set; }
        // constructor to create Node that refers to dataValue
        // and is last node in list
        public Node(object dataValue) : this(dataValue, null) {}
        // constructor to create Node that refers to dataValue
        // and refers to last Node in List
        public Node(object dataValue, Node nextNode)
        {
            Data = dataValue;
            Next = nextNode;
        }
    }
```

> Fig. 19.4 | Node, List and EmptyAccessException class declarations. (Part I of 4).

## Chapter 19 Custom Linked Data Structures

```
// class List declaration
public class List {
    private ListNode firstNode;
    private ListNode lastNode;
    private string name; // string like "list" to display

    // construct empty List with specified name
    public List(string lastName) {
        name = listName;
        firstNode = lastNode = null;
    }

    // construct empty List with "list" as its name
    public List() : this("list") {}

    // Insert object at front of List. If List is empty,
    // firstNode and lastNode will refer to same object.
    // Otherwise, firstNode refers to new node.
    public void InsertAtFront(object insertItem) {
        if (IsEmpty()) {
            firstNode = new ListNode(insertItem);
        } else {
            firstNode = new ListNode(insertItem, firstNode);
        }
    }

    // Insert object at end of List. If List is empty,
    // firstNode and lastNode will refer to same object.
    // Otherwise, lastNode's Next property refers to new node.
    public void InsertAtBack(object insertItem) {
        if (IsEmpty()) {
            firstNode = new ListNode(insertItem);
        } else {
            lastNode = lastNode.Next = new ListNode(insertItem);
        }
    }

    // remove node from List
    public object RemoveFromFront() {
        if (IsEmpty()) {
```

Fig. 19.4 | ListNode, List and EmptyListException class declarations. (Part 2 of 4)

```
81  throw new EmptyListException(name);
82  }
83
84  object removeItem = firstNode.Data; // retrieve data
85
86  // reset firstNode and lastNode references
87  if (firstNode == lastNode)
88  {
89      firstNode = null;
90  }
91  else
92  {
93      firstNode = firstNode.Next;
94  }
95
96  return removeItem; // return removed data
97  }
98
99  // remove last node from List
100 public object RemoveBack() {
101  if (IsEmpty())
102    {
103      throw new EmptyListException(name);
104    }
105
106  object removeItem = lastNode.Data; // retrieve data
107
108  // reset firstNode and lastNode references
109  if (firstNode == lastNode)
110  {
111      firstNode = lastNode = null;
112  }
113  else
114  {
115      ListNode current = firstNode;
116      // loop while current.Next is not lastNode
117      while (current.Next != null)
118      {
119          current = current.Next; // move to next node
120      }
121      
122      // current is new lastNode
123      lastNode = current;
124      current.Next = null;
125  }
126  }
127  
128  return removeItem; // return removed data
129  }
130else
```

Fig. 19.4 | ListNode. List and EmptyListException class declarations. (Part 3 of 4).

```
// return true if List is empty
public bool IsEmpty()
{
    return firstNode == null;
}

// output List contents
public void Display()
{
    if (IsEmpty())
    {
        Console.WriteLine($"Empty {name}");
    }
    else
    {
        Console.Write($"{The {name} is: ");
        ListNode current = firstNode;
        // output current node data not at end of list
        while (current != null)
        {
            Console.Write($"{current.Data}");
            current = current.Next;
        }
        Console.WriteLine("\n");
    }
}
```

```
// class EmptyListException declaration
public class EmptyListException : Exception
{
    // parameterless constructor
    public EmptyListException() : base("The list is empty") { }

    // one-parameter constructor
    public EmptyListException(string name) : base("The {name} is empty") { }

    // two-parameter constructor
    public EmptyListException(string exception, Exception inner) : base(exception, inner) { }
}
```

Fig. 19.4 ListNode, List and EmptyListException class declarations. (Part 4 of 4).

**Class ListNode**
Encapsulated in this is a linked list of ListNode objects. Class ListNode (Fig. 19.4, lines 8–27) contains two properties—Data and Next. Data can refer to any object. [Note: Typically, a data structure will contain data of only one type, or data of any type derived from one base type.] In this example, we use data of various types derived from object to demon-
