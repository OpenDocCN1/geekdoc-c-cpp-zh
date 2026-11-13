![](bbox=[0.13, 0.08, 0.82, 0.27])

Figure 5.10 (a-e): Node deletion at any position in a linked list

# Searching a singly linked list

This algorithm finds the location of a node in a linked list whose value is ITEM. Temp is a pointer which points to the starting node of the linked list. 'Temp' is a temporary pointer to traverse the list. 'LOC' is the variable to store the location of the search item.

# Algorithm to search Linked List by given value

```
Algorithm: SEARCH(HEAD, ITEM, LOC)
1. Set Temp = HEAD, LOC=NULL
2. If Temp = NULL then
   i) "The linked list is empty"
   ii) Return
3. Repeat step 4 while Temp != NULL
4. If Temp->DATA = ITEM then
   i) Print: "Element found"
   ii) Set LOC = Temp
   iii) Return
   Else
   Temp = Temp->LINK
   [End of If]
   [End of Loop]
5. Print: "Element not found"
6. Return
```

At first Temp is assigned to the address of HEAD

![](bbox=[0.1, 0.805, 0.85, 0.865])

(a)

After that Temp->DATA is compared with ITEM=1 and Temp moves accordingly