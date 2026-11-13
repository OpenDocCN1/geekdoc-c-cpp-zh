# FIGURE 7.6 Header File for the Array Version of the Stack Template Class

# A Header File

```
// FILE: stack1.h (part of the namespace main_savitch_7A)
// TEMPLATE CLASS PROVIDED: stack<Item>
//
// TEMPLATE PARAMETER, TYPEDEFS, and MEMBER CONSTANTS for the stack<Item> class:
//   The template parameter, Item, is the data type of the items in the stack, also defined
//   as stack<Item>::value_type. It may be any of the C++ built-in types (int, char, etc.), or
//   a class with a default constructor, a copy constructor, and an assignment operator.
//   The definition stack<Item>::size_type is the data type of any variable that keeps track
//   of how many items are in a stack. For this implementation, stack<Item>::CAPACITY
//   is the maximum capacity of any stack (once CAPACITY is reached, further pushes
//   are forbidden).
//
// CONSTRUCTOR for the stack<Item> template class:
//   stack( )
//     Postcondition: The stack has been initialized as an empty stack.
//
// MODIFICATION MEMBER FUNCTIONS for the stack<Item> template class:
//   void push(const Item& entry)
//     Precondition: size( ) < CAPACITY.
//     Postcondition: A new copy of entry has been pushed onto the stack.
//
//   void pop( )
//     Precondition: size( ) > 0.
//     Postcondition: The top item of the stack has been removed.
//
// CONSTANT MEMBER FUNCTIONS for the stack<Item> template class:
//   Item top( ) const
//     Precondition: size( ) > 0.
//     Postcondition: The return value is the top item of the stack, but the stack is
//     unchanged. This differs slightly from the STL stack (where the top function returns a
//     reference to the item on top of the stack).
//
//   size_type size( ) const
//     Postcondition: The return value is the total number of items in the stack.
//
//   bool empty( ) const
//     Postcondition: The return value is true if the stack is empty, and false otherwise.
//
// VALUE SEMANTICS for the stack<Item> template class:
//   Assignments and the copy constructor may be used with stack<Item> objects.
//
```