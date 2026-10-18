When here is NULL, it is not pointing to any node, so there is no member named data nor any member named link. Hence, we make a special case of the empty list. The complete function definition is given in Display 13.7.

# DISPLAY 13.7 Function to Locate a Node in a Linked List

# Function Declaration

```
1   struct Node
2   {
3       int data;
4       Node *link;
5   };
6
7   typedef Node* NodePtr;
8
9   NodePtr search(NodePtr head, int target);
10  //Precondition: The pointer head points to the head of
11  //a linked list. The pointer variable in the last node
12  //is NULL. If the list is empty, then head is NULL.
13  //Returns a pointer that points to the first node that
14  //contains the target. If no node contains the target,
15  //the function returns NULL.
```

# Function Definition

```
1   //Uses cstddef:
2   NodePtr search(NodePtr head, int target)
3   {
4       NodePtr here = head;
5
6       if (here == NULL)
7       {
8           return NULL;
9       }
10      else
11      {
12          while (here->data != target &&
13                  here->link != NULL)
14              here = here->link;
15
16          if (here->data == target)
17              return here;
18          else
19              return NULL;
20      }
21  }
```

Empty list case