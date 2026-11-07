```
```cpp
first = newNode;        //of the list
cin >> num;             //update the head pointer of
                        //the list, that is, first
}                       //read the next number

return first;
} //end buildListBackward
```
```

# Linked List as an ADT

The previous sections taught you the basic properties of linked lists and how to construct and manipulate them. Because a linked list is a very important data structure, rather than discuss specific lists such as a list of integers or a list of strings, this section discusses linked lists as an abstract data type (ADT). Using templates, this section gives a generic definition of linked lists, which is then used in the next section and later in this book. The programming example at the end of this chapter also uses this generic definition of linked lists.

The basic operations on linked lists are:

+   1. Initialize the list.
+   2. Determine whether the list is empty.
+   3. Print the list.
+   4. Find the length of the list.
+   5. Destroy the list.
+   6. Retrieve the info contained in the first node.
+   7. Retrieve the info contained in the last node.
+   8. Search the list for a given item.
+   9. Insert an item in the list.
+   10. Delete an item from the list.
+   11. Make a copy of the linked list.

In general, there are two types of linked lists—sorted lists, whose elements are arranged according to some criteria, and unsorted lists, whose elements are in no particular order. The algorithms to implement the operations search, insert, and remove slightly differ for sorted and unsorted lists. Therefore, we will define the `class linkedListType` to implement the basic operations on a linked list as an `abstract class`. Using the principle of inheritance, we, in fact, will derive two `classes`—`unorderedLinkedList` and `orderedLinkedList`—from the `class linkedListType`.

Objects of the `class unorderedLinkedList` would arrange list elements in no particular order, that is, these lists may not be sorted. On the other hand, objects of the `class orderedLinkedList` would arrange elements according to some comparison criteria, usually less than or equal to. That is, these lists will be in ascending order. Moreover, after