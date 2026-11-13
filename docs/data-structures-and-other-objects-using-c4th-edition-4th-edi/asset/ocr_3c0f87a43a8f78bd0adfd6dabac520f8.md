all, we could simply use the formula "(1+1) % CAPACITY" directly instead of calling next_index. The reason for declaring next_index is to make the other implementations easier to read. The name next_index suggests the purpose it serves, which is to "move to the next index." On the other hand, the formula on its own requires some thought as to its purpose.

# PROGRAMMING TIP

# USE SMALL HELPER FUNCTIONS TO IMPROVE CLARITY

When a class requires some small operation that is implemented as a formula, consider implementing the formula with a helper function (that is, a private member function). This will improve the clarity of your other code.

# FIGURE 8.9 Header File for the Array Version of the Queue Template Class

# A Header File

```
// FILE: queue1.h (part of the namespace main_savitch_8B)
// TEMPLATE CLASS PROVIDED: queue<item> (a queue of items)
// TEMPLATE PARAMETER, TYPEDEFS, and MEMBER CONSTANTS for the queue<item> class:
//   The template parameter, item, is the data type of the items in the queue, also defined
//   as queue<item>::value_type. It may be any of the C++ built-in types (int, char, etc.), or a
//   class with a default constructor, a copy constructor, and an assignment operator. The
//   definition queue<item>::size_type is the data type of any variable that keeps track of how
//   many items are in a queue. The static const CAPACITY is the maximum capacity of a
//   queue for this first queue implementation.
// CONSTRUCTOR for the queue<item> template class:
//   queue( )
//     Postcondition: The queue has been initialized as an empty queue.
// MODIFICATION MEMBER FUNCTIONS for the queue<item> template class:
//   void pop( )
//     Precondition: size( ) > 0.
//     Postcondition: The top item of the queue has been removed.
//   void push(const Item& entry)
//     Postcondition: A new copy of entry has been inserted at the rear of the queue.
// CONSTANT MEMBER FUNCTIONS for the queue<item> template class:
//   bool empty( ) const
//     Postcondition: The return value is true if the queue is empty.
(continued)
```