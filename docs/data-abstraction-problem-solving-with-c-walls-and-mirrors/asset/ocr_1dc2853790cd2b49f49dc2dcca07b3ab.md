The method clear. To clear of all the entries from a list, our final method simply sets itemCount to zero.

```
template<class ItemType>
void ArrayList<ItemType>::clear()
{
    itemCount = 0;
} // end clear
```

The entire implementation file for the class ArrayList is available online from the book's website.

> Question 4 Although the method cannot remove an entry from an empty list, it does not explicitly check for one. How does this method avoid deletion from an empty list?

# 9.2 A Link-Based Implementation of the ADT List

We now consider how to use C++ pointers instead of an array to implement the ADT list. Unlike the array-based implementation, a link-based implementation does not shift items during insertion and deletion operations. It also does not fix a maximum length on the list—except, of course, as imposed by the storage limits of the system.\ Once again, we need to represent the entries in the list and in the list. Listing 9-4 indicates one possible way to represent this data using pointers. Here headPtr points to the linked nodes containing the items in the list, where the first node contains the entry at position 1 in the list, and so on. The itemCount is the current number of entries in the list. Both headPtr and itemCount be private data members of our class.

# 9.2.1 The Header File

Let's name our class LinkedList and write its header file as shown in Listing 9-2. This file has similarities to the header file for ArrayList, as given in Listing 9-1, but let's point out the differences. Here we include the header files for the class Node and PrevalidatedException, as defined in Listing 4-1 of Chapter 4 and Listing 7-5 of Chapter 7, respectively.
The private section declares the two data members—headPtr and itemCount—as a private method getAt that we will use to locate any node within the chain of linked nodes, given its position in the chain. Unlike an array, which provides direct access to a specified element, the chain of linked nodes requires the insertion, and removal operations to traverse it until the specified node is reached. While you could write the necessary loop in the method getEntry, you would soon discover that the methods insert and remove will need the same loop. At that time, you should

FIGURE 9-4 A link-based implementation of the ADT list

![](bbox=[0.276, 0.843, 0.853, 0.903])