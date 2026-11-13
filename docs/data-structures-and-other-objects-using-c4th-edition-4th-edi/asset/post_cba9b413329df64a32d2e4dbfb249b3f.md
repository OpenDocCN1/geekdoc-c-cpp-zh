
## (FIGURE 5.11 continued)

```cpp
// NONMEMBER FUNCTIONS for the bag class:
// bag operator +(const bag& b1, const bag& b2)
// Postcondition: The bag returned is the union of b1 and b2.
// VALUE SEMANTICS for the bag class:
// Assignments and the copy constructor may be used with bag objects.
// DYNAMIC MEMORY USAGE by the bag:
// If there is insufficient dynamic memory, then the following functions throw bad_alloc:
// The constructors, insert, operator +=, operator +, and the assignment operator.
#ifndef MAIN_SAVITCH_BAG3_H
#define MAIN_SAVITCH_BAG3_H
#include <cstddef> // Provides size_t and NULL
#include "node1.h" // Provides node class
namespace main_savitch_5
{
class bag
{
public:
    // TYPEDEFS
    typedef std::size_t size_type;
    typedef node::value_type value_type;
    // CONSTRUCTORS and DESTRUCTOR
    bag( );
    bag(const bag& source);
    ~bag( );
    // MODIFICATION MEMBER FUNCTIONS
    size_type erase(const value_type& target);
    bool erase_one(const value_type& target);
    void insert(const value_type& entry);
    void operator +=(const bag& addend);
    void operator =(const bag& source);
    // CONSTANT MEMBER FUNCTIONS
    size_type size( ) const { return many_nodes; }
    size_type count(const value_type& target) const;
    value_type grab( ) const;
private:
    node *head_ptr; // List head pointer
    size_type many_nodes; // Number of nodes on the list
};
// NONMEMBER FUNCTIONS for the bag class:
bag operator +(const bag& b1, const bag& b2);
}
#endif
```

- Prototype for the copy constructor
- Prototype for the destructor
- Prototype for the overloaded operator =

If we need a different type of item, we can change node::value_type to the required new type and recompile. The bag::value_type will then match the new node::value_type. For example, suppose we want a bag of strings using the Standard Library string class (from <string>). In order to obtain the bag of strings, the start of our node definition will be:

```cpp
#include <string>
class node
{
public:
  typedef std::string value_type;
  ...
```

In this case, the node::value_type is defined as the string class, so that bag::value_type will also be a string. By the way, when we get to the implementation details, we will use examples where the items are strings, keep in mind, however, that the underlying item type could easily be changed.

## Following the Rules for Dynamic Memory Usage in a Class

Our new bag is a class that uses dynamic memory, therefore it must follow the four rules that we outlined in "Prescription for a Dynamic Class" on page 195. Let's review these rules:

- 1. Some of the member variables of the class are pointers. In particular, our new bag has a member variable, head_ptr, that is a head pointer of a linked list.
- 2. Member functions allocate and release dynamic memory as needed. We will see this when the bag's member functions are implemented. For example, the bag's insert function will allocate a new node.
- 3. The automatic value semantics of the class is overridden. In other words, the class must implement a copy constructor and an assignment operator that correctly copy one bag to another. You can see that the bag's class definition in Figure 5.11 on page 262 accounts for this by including the prototypes for the copy constructor and the assignment operator.
- 4. The class has a destructor. Again, the bag's class definition in Figure 5.11 provides for this with the destructor's prototype.

Also notice that the bag's documentation does not list a destructor, since the programmer who uses the bag's class does not normally make explicit calls to the destructor. But our planned implementation uses dynamic memory, so a destructor will be part of the class.

## The Third Bag Class—Implementation

With our design in mind, we can implement each of the member functions, starting with the constructors. The key to simple implementations is to use the linked-list functions whenever possible.

Constructors. The default constructor sets head_ptr to be the null pointer (indicating the empty list) and sets many_nodes to zero. The copy constructor uses list_copy to make a separate copy of the source list, and many_nodes is then copied from the source to the newly constructed bag. Only a few statements are needed for the copy constructor, as shown here:

```cpp
bag::bag(const bag& source)
// Library facilities used: node1.h
{
    node *tail_ptr; // Needed for argument to list_copy
    list_copy(source.head_ptr, head_ptr, tail_ptr);
    many_nodes = source.many_nodes;
}
```

Overloading the assignment operator. The overloaded assignment operator needs to change an existing bag so that it is the same as some other bag. The main difference between this and the copy constructor is that we must remember that when the assignment operator begins, the bag already has a linked list, and this linked list must be returned to the heap. With this in mind, you might write the implementation shown here, with the highlighted statement returning the existing linked list to the heap:

```cpp
void bag::operator =(const bag& source)
// Library facilities used: node1.h
{
    node *tail_ptr; // Needed for argument to list_copy
    list_clear(head_ptr);
    many_nodes = 0;
    list_copy(source.head_ptr, head_ptr, tail_ptr);
    many_nodes = source.many_nodes;
}
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_291_0.png)

In fact, we actually did write this implementation for our first attempt on the assignment operator. Then we remembered the programming tip from Chapter 4: “How to Check for Self-Assignment” on page 188. For a bag, it is possible for a programmer to write b = b. Perhaps you think this is a pointless assignment statement, but nevertheless the operator should work correctly, assigning b to be equal to its current value—that is, leave the bag unchanged. But instead, when the buggy assignment operator is activated with b = b, the first thing that happens is that the bag b (which activated the operator) is cleared. Once that list is cleared, there is no hope of leaving the bag unchanged.

The solution is to check for this special “self-assignment” at the start of the operator. If we find that an assignment such as b = b is occurring, then we will return immediately. We can check for this condition with the test this == &source, described on page 188. This is done in the highlighted statement in this correct implementation:

```cpp
void bag::operator= (const bag& source)
// Library facilities used: node1.h
{
    node *tail_ptr; // Needed for argument to list_copy
    if (this == &source)
        return;
    list_clear(head_ptr);
    many_nodes = 0;
    list_copy(source.head_ptr, head_ptr, tail_ptr);
    many_nodes = source.many_nodes;
}
```

One other point about the implementation: After we clear the linked list, we also set many_nodes to zero. The reason for this is that we want the bag to be valid before calling list_copy. In general, we will ensure that the bag is valid before calling any function that allocates dynamic memory; otherwise debugging is difficult (see “How to Allocate Memory in a Member Function” on page 191).

## The Assignment Operator Causes Trouble with Linked Lists

When a class uses a linked list, you must take care with the assignment operator. Part of the care is checking for the special situation of “self-assignment” such as b = b. The easiest way to handle self-assignment is to check for it at the start of the assignment operator and simply return with no work if self-assignment is discovered.

Care is also needed before allocating dynamic memory. Before calling a function that allocates dynamic memory, make sure that the invariant of your class is valid.

The destructor. Our documentation, which is meant for other programmers, never mentioned a destructor, but a destructor is needed because our particular implementation uses dynamic memory. The destructor is responsible for returning all dynamic memory to the heap. The job is accomplished by list_clear, shown next.
