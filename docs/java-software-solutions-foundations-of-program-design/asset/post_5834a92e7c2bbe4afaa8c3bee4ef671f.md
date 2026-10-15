
![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_647_0.png)

# FIGURE 13.1 A linked list

> KEY CONCEPT
> A dynamically linked list is managed by storing and updating references to objects.

object’s next reference can refer to a third Node object, and so on, creating a linked list. The first node in the list could be referenced using a separate variable. The last node in the list would have a next reference that is null, indicating the end of the list. Figure 13.1 depicts this situation.

In this example, the information stored in each Node class is a simple integer, but keep in mind that we could define a class to contain any amount of information of any type.

## A Dynamically Linked List

The program in Listing 13.1 sets up a list of Magazine objects and then prints the list. The list of magazines is encapsulated inside the MagazineList class shown in Listing 13.2 and is maintained as a dynamically linked list.

The MagazineList class represents the list of magazines. From outside of the class (an external view), we do not focus on how the list is implemented. We don’t know, for instance, whether the list of magazines is stored in an array or in a linked list. The MagazineList class provides a set of methods that allows the user to maintain the list of magazines. That set of methods, specifically add and toString, defines the operations to the MagazineList ADT.

The MagazineList class uses an inner class called MagazineNode to represent a node in the linked list. Each node contains a reference to one magazine and a reference to the next node in the list. Because MagazineNode is an inner class, it is reasonable to allow the data values in the class to be public. Therefore, the code in the MagazineList class refers to those data values directly.

The Magazine class shown in Listing 13.3 is well encapsulated, with all data declared as private and methods provided to accomplish any updates necessary. Note that because we use a separate class to represent a node in the list, the Magazine class itself does not need to contain a link to the next Magazine in the list. That allows the Magazine class to be free of any issues regarding its containment in a list.

> VideoNote
> Example using a linked list.

### 13.2 Dynamic Representations

#### LISTING 13.1

```
//**********************************
// MagazineRack.java Author: Lewis/Loftus
// Driver to exercise the MagazineList collection.
//**********************************

public class MagazineRack
{
	//----------------------------------
	// Creates a MagazineList object, adds several magazines to the
	// list, then prints it.
	//----------------------------------
	public static void main (String[] args)
	{
		MagazineList rack = new MagazineList();

		rack.add (new Magazine("Time"));
	rack.add (new Magazine("Woodworking Today"));
	rack.add (new Magazine("Communications of the ACM"));
	rack.add (new Magazine("House and Garden"));
	rack.add (new Magazine("GQ"));

		System.out.println (rack);
	}
	
}
```

#### OUTPUT

- Time
- Woodworking Today
- Communications of the ACM
- House and Garden
- GQ

Other methods could be included in the MagazineList ADT. For example, in addition to the add method provided, which always adds a new magazine to the end of the list, another method called insert could be defined to add a node anywhere in the list (to keep it sorted, for instance). A parameter to insert could indicate the value of the node after which the new node should be inserted. Figure 13.2 shows how the references would be updated to insert a new node.

> Insert and delete operations can be implemented by carefully manipulating object references.

#### LISTING 13.2

```
//********************** MagazineList.java Author: Lewis/Loftus
// Represents a collection of magazines.
//**********************

public class MagazineList
{
private MagazineNode list;

// Sets up an initially empty list of magazines.
//--------------------
public MagazineList()
{
list = null;
}

// Creates a new MagazineNode object and adds it to the end of the linked list.
//--------------------
public void add (Magazine mag)
{
MagazineNode node = new MagazineNode (mag);
MagazineNode current;

if (list == null)
list = node;
else
{
current = list;
while (current.next != null)
current = current.next;
current.next = node;
}
}

// Returns this list of magazines as a string.
//--------------------
public String toString ()
{
// code would go here
}
```

```
{
    String result = "";
    MagazineNode current = list;
    while (current != null)
    {
        result += current.magazine + "\n";
        current = current.next;
    }
    return result;
}

// An inner class that represents a node in the magazine list.
// The public variables are accessed by the MagazineList class.
private class MagazineNode
{
    public Magazine magazine;
    public MagazineNode next;

    // Sets up the node
    public MagazineNode (Magazine mag)
    {
        magazine = mag;
        next = null;
    }
}
```

```
//******************************************************
//  Magazine.java        Author: Lewis/Loftus
//
//  Represents a single magazine.
*******************************************************/

public class Magazine
{
    private String title;

    //--------------------------------------------------
    //  Sets up the new magazine with its title.
    //--------------------------------------------------
    public Magazine (String newTitle)
    {
        title = newTitle;
    }

    //--------------------------------------------------
    //  Returns this magazine as a string.
    //--------------------------------------------------
    public String toString ()
    {
        return title;
    }
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_651_0.png)

**FIGURE 13.2** Inserting a node into the middle of a list

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_652_0.png)

# FIGURE 13.3 Deleting a node from a list

Another operation that would be helpful in the list ADT would be a delete method to remove a particular node. Recall from our discussion in Chapter 3 that by removing all references to an object, it becomes a candidate for garbage collection. Figure 13.3 shows how references would be updated to delete a node from a list. Care must be taken to accomplish the modifications to the references in the proper order to ensure that other nodes are not lost and that references continue to refer to valid, appropriate nodes in the list.

## Other Dynamic List Representations

You can use different list implementations, depending on the specific needs of the program you are designing. For example, in some situations it may make processing easier to implement a doubly linked list in which each node has not only a reference to the next node in the list but another reference to the previous node in the list. Our generic Node class might be declared as follows:

KEY CONCEPT
Many variations on the implementation of dynamically linked lists can be defined.

```
class Node
{
    int info;
    Node next, prev;
}
```

Figure 13.4 shows a doubly linked list. Note that, like a single linked list, the next reference of the last node is null. Similarly, the previous node of the first node is null since there is no node that comes before the first one. This type of structure makes it easy to move back and forth between nodes in the list but requires more effort to set up and modify.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_652_1.png)

# FIGURE 13.4 A doubly linked list

# FIGURE 13.5 A list with front and rear references

Another implementation of a linked list could include a header node for the list that has a reference to the front of the list and another reference to the rear of the list. A rear reference makes it easier to add new nodes to the end of the list. The header node could contain other information, such as a count of the number of nodes currently in the list. The declaration of the header node would be similar to the following:

```
class ListHeader
{
    int count;
    Node front, rear;
}
```

Note that the header node is not of the same class as the Node class to which it refers. Figure 13.5 depicts a linked list that is implemented using a header node.

Still other linked list implementations can be created. For instance, the use of a header can be combined with a doubly linked list, or the list can be maintained in sorted order. The implementation should cater to the type of processing that is required. Some extra effort to maintain a more complex data structure may be worthwhile if it makes common operations on the structure more efficient.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 13.4 What is a dynamic data structure?
- SR 13.5 Describe the steps depicted in Figure 13.2 to insert a node into a list. What special cases exist?
- SR 13.6 Describe the steps depicted in Figure 13.3 to delete a node from a list. What special cases exist?

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_653_0.png)
