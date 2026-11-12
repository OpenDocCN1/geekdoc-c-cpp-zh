The method clear. To clear all of the entries from a list, our final method simply sets itemCount to zero:

```
template<class ItemType>
void ArrayList<ItemType>::clear()
{
   itemCount = 0;
} // end clear
```

The entire implementation file for the class ArrayList is available online from the book's website.

Question 4 Although the method remove cannot remove an entry from an empty list, it does not explicitly check for one. How does this method avoid an attempted deletion from an empty list?

# 9.2 A Link-Based Implementation of the ADT List

We now consider how we can use C++ pointers instead of an array to implement the ADT list. Unlike the array-based implementation, a link-based implementation does not shift items during insertion and deletion operations. It also does not impose a fixed maximum length on the list—except, of course, as imposed by the storage limits of the system.

Once again, we need to represent the items in the list and its length. Figure 9-4 indicates one possible way to represent this data by using pointers. Here headPtr points to the linked nodes containing the items in the list, where the first node contains the entry at position 1 in the list, and so on. The integer itemCount is the current number of entries in the list. Both headPtr and itemCount will be private data members of our class.

# 9.2.1 The Header File

Let's name our class of lists LinkedList and write its header file as shown in Listing 9-2. This file has similarities to the header file for ArrayList, as given in Listing 9-1, but let's point out the differences. Here we include the header files for the classes Node and PrecondViolatedExcep, as defined in Listing 4-1 of Chapter 4 and Listing 7-5 of Chapter 7, respectively.

The private section declares the two data members—headPtr and itemCount—as well as a private method getNodeAt that we will use to locate any node within the chain of linked nodes, given its position in the chain. Unlike an array, which provides direct access to a specified element, the chain of linked nodes requires the get, insertion, and removal operations to traverse it until the specified node is reached. While you could write the necessary loop in the method getEntry, you would soon discover that the methods insert and remove will need the same loop. At that time, you should realize

![](bbox=[0.22, 0.81, 0.93, 0.91])