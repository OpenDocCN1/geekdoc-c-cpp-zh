Figure 12.3 (output shown in Fig. 12.4) manipulates a list of characters. You can insert a character in the list in alphabetical order (function insert) or delete a character from the list (function delete). A detailed discussion of the program follows.

```
```c
1 // Fig. 12.3: fig12_03.c
2 // Inserting and deleting nodes in a list
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 // self-referential structure
7 struct listNode {
8 char data; // each listNode contains a character
9 struct listNode *nextPtr; // pointer to next node
10 };
11
12 typedef struct listNode ListNode; // synonym for struct listNode
13 typedef ListNode *ListNodePtr; // synonym for ListNode*
14
15 // prototypes
16 void insert(ListNodePtr *sPtr, char value);
17 char delete(ListNodePtr *sPtr, char value);
18 int isEmpty(ListNodePtr sPtr);
19 void printList(ListNodePtr currentPtr);
20 void instructions(void);
21
22 int main(void)
23 {
24 ListNodePtr startPtr = NULL; // initially there are no nodes
25 char item; // char entered by user
26
27 instructions(); // display the menu
28 printf("\n");
29 unsigned int choice; // user's choice
30 scanf("%u", &choice);
31
32 // loop while user does not choose 3
33 while (choice != 3) {
34
35 switch (choice) {
36 case 1:
37 printf("\n%s", "Enter a character: ");
38 scanf("\n%c", &item);
39 insert(&startPtr, item); // insert item in list
40 printList(startPtr);
41 break;
42 case 2: // delete an element
43 // if list is not empty
44 if (!isEmpty(startPtr)) {
45 printf("\n%s", "Enter character to be deleted: ");
46 scanf("\n%c", &item);
```
```