```
Enter data value to delete:
16
List Values:
5
10
15
16
20
25
Enter 0 to delete node, 1 to add node, 2 to quit.
0
Enter data value to delete:
10
List Values:
5
15
16
20
25
```

# Additional Dynamic Data Structures

We will present five additional linked data structures that are very powerful. Although each of these data structures could be the topic of a separate section, we will introduce them in this section to illustrate some of the special structures that can be developed with linked lists.

Circularly linked list

Circularly Linked List. A circularly linked list is generated when the last node in a linked list points to the first node in the list as shown in Figure 7.9. Note that the NULL constant is not used with the circularly linked list because there really is not an end to the list. However, in an empty circularly linked list, the pointer first will contain the NULL constant.

Inserting and deleting in a circularly linked list is very similar to inserting and deleting in a regular linked list. We do need to be careful that we properly handle the pointer first, because it points to the beginning of the list and also determines when we have followed the links back around to the beginning.

![](bbox=[0.27, 0.735, 0.87, 0.885])

Figure 7.9 Circularly linked list.