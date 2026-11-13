+   • Circular Linked List can also be used to create Circular Queue. In a Queue we have to keep two pointers, FRONT and REAR in memory all the time, where as in Circular Linked List, only one pointer is required.

# Josephus Problem

The Josephus problem consists of a group of soldiers surrounded by an overwhelming enemy force. There is only a single horse available for escape. To determine which soldier is to escape, they form a circle & a number n is picked from a hat. A name is also picked from the hat. They begin to count clockwise around the circle, beginning with the soldier, whose name is picked. One soldier is removed from the circle on which count reaches n & the count starts again with next soldier, removing another soldier each time the count reaches n & the last remaining soldier is the one to take the horse.

Our problem is to find the order in which soldier will escape; The input to our program is the number and a list of names. The names are according to the clockwise; ordering of circle beginning with the soldier from whom the count is to start. The program prints the names in the order in which they are eliminated & the name of the soldier who escapes. The data structure used is, a circular linked list in which each node represents one soldier as it is possible to reach any node from any other node by moving around the circle.

The structure of the node in the circular linked list consist of name and link part

```
struct node
{
 char name[30];
 struct node *link;
 }
```

# Algorithm to solve Josephus problem

```
ALGORITHM: JOSEPHUS (HEAD)
1. Read N and Name
2. Set count= number of soldiers
   Set Temp=HEAD
3. Repeat until Name=Temp->name
   Temp=Temp->LINK
   [End of loop]
4. Repeat until Count=1
   a) Set C=1
   b) Repeat until C=N
      i) Set Prev=Temp
     ii) Set Temp=Temp->LINK
    iii) Set C=C+1
      [End of loop]
   c) Prev->LINK=Temp->LINK
      Print Temp->DATA "soldier remove"
   d) Set Count=Count-1
   [End of loop]
5. Print Prev->name "soldier escape"
6. Return
```