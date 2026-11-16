
As mentioned in Section 10.5, given the same basic algorithm implemented recursively or iteratively, the iterative version will be more efficient. This is because each recursive call requires additional space on the stack to store fresh local variables (if any) and parameters. Not only does a recursive method or function require more memory, it takes more time to complete because the executing program must perform extra work to set up the new space needed by a recursive invocation and restore the context when a recursive invocation returns. If we build a very large linked list, a call to our recursive length or clear method could consume considerable space on the stack and impose a significant performance overhead. For future versions of our linked list code we will use the iterative version of the clear method.

To optimize the length method, we will choose a different route. If you have an application that manages rather large lists and makes frequent calls to the length method, even iteration can take considerable time. We can add an integer instance variable to the IntList1 class that keeps track of the number of elements in the list. This new instance variable affects the rest of the class members as follows:

- The constructor would initialize this variable to zero.
- The insert method would increment this variable by one each time the client adds an element to the list.
- The clear method would reset this variable to zero.
- The length method would avoid the loop completely and simply return the value of this variable.

The time spent looping over all the elements in a list counting them can be considerable for large lists, so the additional space required by a single extra integer is a good trade off for speeding up the length method.

The IntList1 class code as defined in Listing 18.3 (intlist.h) and Listing 18.4 (intlist.cpp) is useful for introducing the concepts of implementing linked data structures. Our IntList1 class is, however, fundamentally different from all the earlier custom classes we examined in Section 16. With the optimizations to length and clear mentioned above, it may appear to be ready for clients to use as an alternative to std::vector, but it has some severe limitations and pitfalls that make it practically useless for most applications. Section 18.4 exposes its weaknesses and introduces the modifications required to make it a viable, high-quality class worthy for use in any applications requiring a dynamic linked list data structure.

## 18.4 Resource Management

Section 18.3 provided our first attempt at a dynamic linked list class, IntList1, defined in Listing 18.3 (intlist.h) and Listing 18.4 (intlist.cpp). The IntList1::insert method dynamically allocates memory for list elements from the heap. It is essential that the programmer intentionally call clear when finished with a linked list object. Consider the following function definition:

```
void f() {
    IntList1 my_list; // Constructor called here
    // Add some numbers to the list
    my_list.insert(22);
    my_list.insert(5);
    my_list.insert(-44);
    // Print the list
    my_list.print();
} // Oops! Forgot to call my_list.clear!
```

The variable my_list is local to function f. When function f finishes executing the variable my_list goes out of scope. At this point the space on the stack allocated for the local IntList1 variable named my_list is reclaimed; however, the space for the list's heap-allocated elements remains. The only access the program could have to that memory is via my_list.head (or my_list.tail to the last element in the list), but my_list no longer exists. This presents a classic memory leak.

Observe that none of the classes we have designed thus far except for IntList1 have this potential problem.

Fortunately C++ provides a way for class designers to specify actions that must occur at the end of an object's lifetime. Analogous to a constructor that executes code at the beginning of an object's existence, a destructor is a special method that executes immediately before an object ceases to exist. A destructor has the same name as its class, with a tilde ~ prefix. A destructor accepts no arguments. Listing 18.6 (intlist2.h) adds a destructor to Listing 18.3 (intlist.h) and also adds the previously suggested optimizations of the length and clear methods.

### Listing 18.6: intlist2.h

```
// intlist2.h

class IntList2 {
  // The nested private Node class from before
  struct Node {
    int data; // A data element of the list
    Node* next; // The node that follows this one in the list
    Node(int d); // Constructor
  };

  Node* head; // Points to the first item in the list
  Node* tail; // Points to the last item in the list

  int len; // The number of elements in the list

public:
  // The constructor makes an initially empty list
  IntList2();

  // The destructor that reclaims the list's memory
  ~IntList2();

  // Inserts n onto the back of the list.
  void insert(int n);

  // Prints the contents of the linked list of integers.
  void print() const;

  // Returns the length of the linked list.
  int length() const;

  // Removes all the elements in the linked list.
  void clear();
};
```

Listing 18.7 (intlist2.cpp) provides the implementation of the IntList2 class.

### Listing 18.7: intlist2.cpp

```
// intlist2.cpp

#include "intlist2.h"
#include <iostream>

// Private IntList2 operations

// Node constructor
IntList2::Node::Node(int n): data(n), next(nullptr) {}

// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
// The list's length initially is zero.
IntList2::IntList2(): head(nullptr), tail(nullptr), len(0) {}

// The destructor deallocates the memory held by the list
IntList2::~IntList2() {
    clear();
}

// Inserts n onto the back of the list.
// n is the element to insert.
void IntList2::insert(int n)
{
    // Make a node for the new element n
    IntList2::Node *new_node = new Node(n);
    if (tail) { // Is tail non-null?
        tail->next = new_node; // Link the new node onto the back
        tail = new_node; // The new node is the new tail of the list
    }
    else // List is empty, so make head and tail point to new node
        head = tail = new_node;
    len++; // List now has one more element
}

// Prints the contents of the linked list of integers.
void IntList2::print() const
{
    for (auto cursor = head; cursor; cursor = cursor->next)
        std::cout << cursor->data << ' ';
    std::cout << '\n';
}

// Returns the length of the linked list.
int IntList2::length() const {
    return len;
}

// Removes all the elements in the linked list.
void IntList2::clear() {
    auto cursor = head;
    while (cursor) {
        auto temp = cursor;
        cursor = cursor->next;
        delete temp;
    }
    head = tail = nullptr; // Null head signifies list is empty
    len = 0;
}
```

The destructor implementation:

```
IntList2::~IntList2() {
    clear(); // Free up the space held by the nodes in the list
}
```

simply invokes the services of the clear method to deallocate the space held by the list.

When do constructors and destructors execute? A local or global object definition calls the class constructor to properly initialize the object; for example,

```
IntList2 seq;
```

defines the object seq. This definition invokes the IntList2 constructor to set both seq.head and seq.tail to nullptr. If seq is a local variable, its destructor executes at the end of the function's execution. If seq is global, its destructor executes when the program finishes.

A pointer is not an object; it points to an object. This means the definition

```
IntList2 *p;
```

does not invoke IntList2's constructor. Given this definition of p, the statement

```
p = new IntList2;
```

actually creates an IntList2 object and therefore calls the IntList2 constructor for the newly created object. The object to which p points is not destroyed until the programmer uses delete, as in

```
delete p;
```

It is at this point IntList2's destructor executes for p's object.

The addition of the destructor to IntList2 removes the memory leak from the f function we saw earlier. Listing 18.8 (test.cpp) is a complete program that uses IntList2 in function f.

### Listing 18.8: test.cpp

```
#include <iostream>
#include "intlist2.h"

void f() {
    IntList2 my_list; // Constructor called here
    // Add some numbers to the list
    my_list.insert(22);
    my_list.insert(5);
    my_list.insert(-44);
    // Print the list
    my_list.print();
} // my_list goes out of scope; destructor automatically frees its memory

int main() {
```
