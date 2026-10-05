# 16.4. LINKED LISTS

435

![](bbox=[0.275, 0.173, 0.766, 0.313])

Figure 16.1: A null-terminated linked list

# Listing 16.6: intlist.h

```
class IntList {
  * An object that holds an element in a linked list.
  * This type is local to the IntList class and inaccessible
  * to outside this class.
  *
  struct Node {
    int data;        // A data element of the list
    Node *next;      // The node that follows this one in the list
    Node(int d);     // Constructor
  };

  Node *head;      // Points to the first item in the list

  // Private helper methods

  /*
  * insert(p, n)
  * Inserts n onto the back of the
  * list pointed to by p.
  * p points to a node in a linked list
  * n is the element to insert.
  * Returns a pointer to the list that
  * contains n.
  */
  Node *insert(Node *p, int n);

  /*
  * print(p)
  * Prints the contents of a linked list of integers.
  * p points to a linked list of nodes.
  */
```

©2024 Richard L. Haerman

Draft date: January 26, 2024