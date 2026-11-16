# Listing 18.25: intlist6.cpp

```
// intlist6.cpp

#include "intlist6.h"
#include <iostream>
#include <utility>

// Private IntList6 operations

// Node constructor
IntList6::Node::Node(int n): data(n), next(nullptr) {
    std::cout << "Creating node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

IntList6::Node::~Node() {
    std::cout << "Destroying node " << data
              << " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}

// The constructor makes an initially empty list.
// The list is empty when head and tail are null.
IntList6::IntList6(): head(nullptr), tail(nullptr), len(0) {}

// Copy constructor makes a copy of the other object's list
IntList6::IntList6(const IntList6& other): IntList6() {
    // Walk through other's list inserting each of its elements
    // into this list
    for (auto cursor = other.head; cursor; cursor = cursor->next)
        insert(cursor->data);
}

// Move constructor takes possession of the temporary's list
IntList6::IntList6(IntList6&& temp): IntList6() {
    // Swap contents with the temporary
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);
}

// Assignment operator
IntList6& IntList6::operator=(const IntList6& other) {
    // Make a local, temporary copy of other
    IntList6 temp(other);

    // Exchange the head and tail pointers and len from this list
    // with those of the new, temporary list
    std::swap(head, temp.head);
    std::swap(tail, temp.tail);
    std::swap(len, temp.len);

    // The temporary list now points to this list's original contents,
    // and this list now points to the copy of other's list
    // The temporary list will be destroyed since it is a temporary
    return *this;
}
```