The following are the algorithms for Push and Pop operations using linked list.

# Algorithms 6.3: PUSH -LSTACK(TOP, ITEM)

Insert item ITEM into the linked stack LSTACK with pointer TOP

+   1. Insert ITEM into STACK
+      NODE=calloc GETNODE (N) //node for item
+   2. Set DATA of NODE to ITEM //insert node NODE into stack
+   3. Set LINK of NODE to Top //update top pointer
+   4. Top=NODE
+   5. END.

# Algorithm 6.4: POP-LSTACK (TOP, ITEM)

Delete the top element from LSTACK and assign to the ITEM.

+   1. Check stack is empty
+      if (Top=0) then write "stack is empty"
+   2. Exit
+   3. Else
+   4. Temp=Top
+   5. Set ITEM to Top of DATA
+   6. Set Top to Top of LINK
+   7. End

Program 6.2 is the program for linked representation of stack.

# Program 6.2

```
#include<iostream.h>
#include<conio.h>
#include<stdio.h>
#include<alloc.h>
template<class t>
class llist
{
struct node
{
t data;
node*link;
};
*top,*head,*temp,*temp1;
public:
llist();
void push();
void pop();
void display();
};
template<class t>
llist<t>::llist()
{
top=NULL;
```