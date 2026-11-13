
This may look peculiar, with the last index of 0 being before the first index of 2. But keep in mind the circular view of the array. With this view, the queue's entries start at data[first] and continue forward. If you reach the end of the array, you come back to data[0] and keep going until you find the rear. It may help to actually view the array as bent into a circle, with the final array element attached back to the beginning, as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_442_0.png)

An array used in this way is called a **circular array**. We now turn to a detailed implementation of our queue using the idea of a circular array. The header file for our queue is given in Figure 8.9. The queue's entries are held in the array, data, which is a private member variable. The private member variables first and last hold the indexes for the front and the rear of the queue, as we have discussed. Whenever the queue is non-empty, the entries begin at the location data[first], continuing forward in the array. If the entries reach the end of the array, then they continue at the first location, data[0]. In any case, data[last] is the last entry in the queue. One other private member variable, count, records the number of items that are in the queue. We will use count to check whether the queue is empty or full, and also to produce the value returned by the size member function.

The queue class definition also has a new feature: a private member function called next_index. This is a function that we think will be useful for the implementation, but it is not part of the public interface. We don't want other programmers to use this function; it is just for our own use in implementing a specific kind of queue. A private function such as this is called a **helper function**.

The next_index helper function allows us to step easily through the array, one index after another, with wraparound at the end. The function call next_index(i) usually returns i+1, with one exception. When i is equal to the last index of the array, next_index(i) returns the first index of the array (0). By the way, you may be wondering, why bother defining next_index at all? After all, we could simply use the formula "(1+1) % CAPACITY" directly instead of calling next_index. The reason for declaring next_index is to make the other implementations easier to read. The name next_index suggests the purpose it serves, which is to "move to the next index." On the other hand, the formula on its own requires some thought as to its purpose.

## PROGRAMMING TIP

### USE SMALL HELPER FUNCTIONS TO IMPROVE CLARITY

When a class requires some small operation that is implemented as a formula, consider implementing the formula with a helper function (that is, a private member function). This will improve the clarity of your other code.

## FIGURE 8.9 Header File for the Array Version of the Queue Template Class

### A Header File

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

### (FIGURE 8.9 continued)

// Item front( ) const
// Precondition: size( ) > 0.
// Postcondition: The return value is the front item of the queue (but this item is not
// removed from the queue).
//
// size_type size( ) const
// Postcondition: The return value is the total number of items in the queue.
//
#ifndef MAIN_SAVITCH_QUEUE1_H
#define MAIN_SAVITCH_QUEUE1_H
#include <cstddef> // Provides size_t
namespace main_savitch_8B
{
template <class Item>
class queue
{
public:
// TYPEDEFS and MEMBER CONSTANTS -- See Appendix E if this fails to compile.
typedef std::size_t size_type;
typedef Item value_type;
static const size_type CAPACITY = 30;
// CONSTRUCTOR
queue( );
// MODIFICATION MEMBER FUNCTIONS
void pop( );
void push(const Item& entry);
// CONSTANT MEMBER FUNCTIONS
bool empty( ) const { return (count == 0); }
Item front( ) const;
size_type size( ) const { return count; }
private:
Item data[CAPACITY]; // Circular array
size_type first; // Index of item at the front of the queue
size_type last; // Index of item at the rear of the queue
size_type count; // Total number of items in the queue
// HELPER MEMBER FUNCTION
size_type next_index(size_type i) const { return (i+1) % CAPACITY; }
};
}
#include "queue1.template" // Include the implementation.
#endif
```

## Discussion of the Circular Array Implementation of a Queue

Figure 8.10 shows the implementation file for the queue class. Once you understand the next_index function, it is easy to see that the push and pop implementations add and remove items in the usual way for a circular array.

One point that may seem counterintuitive is the implementation of the queue's constructor. It initializes last to the final index of the array (that is, CAPACITY - 1). This may seem peculiar, but the reason relates to a requirement in the invariant:

- **Invariant of the Queue Class (Array Version)**
- 1. The number of items in the queue is in count.
- 2. For a non-empty queue, the items are stored in a circular array beginning at data[first] and continuing through data[last]. The total capacity of the array is CAPACITY.
- 3. For an empty queue, last is some valid index, and first is always equal to next_index(last).

Part of the invariant states: For an empty queue, last is some valid index, and first is always equal to next_index(last). The queue constructor ensures that this requirement is met by setting last to the final index of the array and setting first to the first index of the array.

Of course, you may also wonder why we imposed this requirement on an empty queue. The answer involves how the insert function works on an empty array. When the first item is inserted into the queue for an empty array, the insert function moves the last value to the next available index with the assignment statement last = next_index(last). After this assignment, the new item is placed at data[last]. Therefore, by requiring an empty queue to have first equal to next_index(last), we have ensured that the first item placed in the queue will reside at data[first].

## FIGURE 8.10 Implementation File for the Array Version of the Queue Template Class

```
An Implementation File

// FILE: queue1.template
// TEMPLATE CLASS IMPLEMENTED: queue<Item> (see queue1.h for documentation)
// This file is included in the header file and not compiled separately.
// INVARIANT for the queue class:
// 1. The number of items in the queue is in the member variable count.
// 2. For a non-empty queue, the items are stored in a circular array beginning at data[first] and continuing through data[last]. The total capacity of the array is CAPACITY.
// 3. For an empty queue, last is some valid index, and first is always equal to next_index(last).
(continued)
```
