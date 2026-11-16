program to crash. The scenario is similar to a recursive function that recurses too deeply. On one system the program crashed when attempting to destroy a linked list containing 10,000 nodes.

The version of clear in Listing 18.25 (intlist6.cpp) iterates through the list setting the next pointers of the nodes it most recently visited to nullptr. On the very next iteration the temporary pointer temp destroys the node during its reassignment from cursor. This means it must destroy temp's next smart pointer, but the previous iteration set this to null. This eliminates the chaining problem and allows the previous node to be destroyed with a single function call that returns immediately. This version deallocates the list through a series of separate, isolated function calls that return immediately rather than a chain of function invocations that potentially can overflow the stack.

Listing 18.26 (smartlist.cpp) exercises our IntList6 class, verifying that the smart pointers properly manage the dynamic memory.

# Listing 18.26: smartlist.cpp

```
```cpp
// smartlist.cpp

#include <iostream>
#include "intlist6.h"

void test() {
  IntList6 list;
  for (int i = 0; i < 10; i++)
    list.insert(i);
  list.print();
}

int main() {
  for (int i = 0; i < 10; i++)
    test();
}
```
```

When you run Listing 18.26 (smartlist.cpp) you will see that all Node object creations have corresponding destructions. The std::shared_ptr objects take care of all the heap management.

Our linked list class has an insert method that allows clients to add elements to the list, but it has no method that enables a client to remove a single element. In our most recent non-smart-pointer class, IntList5, we could add the following method:

```
```cpp
// Removes the first occurrence of n from the list.
// Returns true if successful (found n and removed it).
// Returns false if n is not originally present in the list.
bool IntList5::remove(int n) {
  Node *cursor = head, // Start at head of list
       *prev = head;   // Keep track of previous node seen
  // Loop until we run off the end of the list or
  // whichever comes first
  while (cursor && cursor->data != n) {
    prev = cursor;     // Remember previous node
    cursor = cursor->next; // Move to next node
  }
  if (!cursor)         // Did we run off the end of the list?
    return false;      // Indicate we did not find n
```
```