
```
class bag
{
public:
  ...
private:
  value_type *data; // Pointer to dynamic array
  size_type used;   // How much of array is being used
  size_type capacity; // Current capacity of the bag
};
```

With much of the class definition in hand, we can now state the invariant of the dynamic bag class:

## Invariant for the Revised Bag Class

- 1. The number of items in the bag is in the member variable used.
- 2. The actual items of the bag are stored in a partially filled array. The array is a dynamic array, pointed to by the member variable data.
- 3. The total size of the dynamic array is in the member variable capacity.

## Member Functions Allocate Dynamic Memory As Needed

When a class uses dynamic memory, the class's member functions allocate dynamic memory as needed. For example, the constructor of the dynamic bag allocates the dynamic array that the member variable data points to. But how big should this array be? Our plan is to have the constructor allocate a dynamic array whose initial size is determined by a parameter to the constructor. As a bag is used in a program, the size of its dynamic array may, in effect, increase to whatever capacity is needed.

In other words, the parameter to the constructor determines the initial capacity of the bag, but even after this initial capacity is reached, more items can be inserted. Whenever items are inserted into a bag—through the insert member function or the += operator—the bag's current capacity is examined. If the current capacity is too small, then the member function allocates a new, larger dynamic array. The user of a bag does not need to do anything special to obtain the increased capacity. The insert and += functions increase the capacity as needed.

You might wonder why programmer needs to be concerned about the initial capacity of a bag. Can't a programmer just start with a small initial capacity and insert items one after another? The insert function will take care of increasing the capacity as needed. Yes, this approach will always work correctly.

the importance of the initial capacity

But if there are many items, then many of the activations of insert would need to increase the capacity. This could be inefficient. Each time the capacity is increased, new memory is allocated, the items are copied into the new memory, and the old memory is released. To avoid this repeated allocation of memory, a programmer can request a large initial capacity. With this in mind, here is the documentation for the new bag constructor:

```
bag(size_type initial_capacity = DEFAULT_CAPACITY);
// Postcondition: The bag is empty with a capacity given by the parameter.
// The insert function will work efficiently (without allocating new
// memory) until this capacity is reached.
```

For example, suppose that a programmer is going to place 1000 items into a bag named kilosack. When the bag is declared, the programmer can specify a capacity of 1000, as shown here:

```
bag kilosack(1000); // 1000 items can be efficiently added to kilosack.
```

After the initial capacity is reached, the insert function continues to work correctly, but it might be slowed down by memory allocations.

the constructor serves as a default constructor

Notice that the parameter of the constructor has a default argument, DEFAULT_CAPACITY, which will be a constant in our class definition. Because of the default argument, the single constructor actually serves two purposes: It can be used with an argument to construct a bag with a specific capacity, or it can be used as a default constructor (with no argument list). When the constructor is used with no argument list, DEFAULT_CAPACITY is used for the initial capacity. Here are two examples, using the default constructor and using the constructor with an argument:

```
bag ordinary; <-- The initial capacity is DEFAULT_CAPACITY.
bag super(9000); <-- The initial capacity is 9000.
```

Here is one more example to show how the new constructor works with the other members. The example declares a bag with an initial capacity of 6 and places three items in the bag:

```
bag sixpack(6); <-- The constructor creates a bag
with an initial capacity of 6.
sixpack.insert(10);
sixpack.insert(20);
sixpack.insert(30);
```

After these declarations, the bag's private member variables look like this:

The private member variables of the bag include a pointer to a dynamically allocated array of six elements. The first three elements are now being used.

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_206_0.png)

Later, the program could insert more items into this bag, maybe even more than six. If there are more than six items, then the bag's member functions will increase the bag's capacity as needed.

After a bag has been declared and is already in use, a programmer can make an explicit adjustment to the bag's capacity via a new member function called reserve. Here is the specification of the member function:

```
void reserve(size_type new_capacity);
// Postcondition: The bag's current capacity is changed to the
// new_capacity (but not less than the number of items already in the bag).
// The insert function will work efficiently (without allocating new memory) until
// the new capacity is reached.
```

To some extent, the reserve function is a luxury. Programmers can avoid reserve altogether, allowing the other member functions to adjust the size of a bag as needed. But by using the reserve member function, the bag's efficiency is improved.

Using the name reserve for this function may seem like a strange choice. We choose the name to match the Standard Library container classes that have a reserve member function to change the container's capacity.

use names from the Standard Library container classes when possible

All told, five of the member functions that we have seen so far can allocate new dynamic memory: the constructor, reserve, insert, and the two operators (+= and +). As with any function that allocates dynamic memory, these functions are subject to possible failure—the heap might run out of room. In this case, the function calls the new operator, and the new operator will fail, throwing the bad_alloc exception. This prints an error message and halts the program. For our programs, the error-message-and-halt will suffice. But part of our class documentation will indicate which member functions allocate dynamic memory so that more experienced programmers can deal with the exception in their own way. You can see this documentation at the bottom of Figure 4.8, which provides the complete documentation for the header file (bag2.h) of our new bag class.

## Documentation for a Header File

```
// TYPEDEFS AND MEMBER CONSTANTS for the bag class:
// typedef ___ value_type
// bag::value_type is the data type of the items in the bag. It may be any of the C++
// built-in types (int, char, etc.), or a class with a default constructor, an assignment
// operator, and operators to test for equality (x == y) and non-equality (x != y).
// typedef ___ size_type
// bag::size_type is the data type of any variable that keeps track of how many items
// are in a bag.
// static const size_type DEFAULT_CAPACITY = _____
// bag::DEFAULT_CAPACITY is the initial capacity of a bag that is created by the default
// constructor.
// CONSTRUCTOR for the bag class:
// bag(size_type initial_capacity = DEFAULT_CAPACITY)
// Postcondition: The bag is empty with an initial capacity given by the parameter. The
// insert function will work efficiently (without allocating new memory) until this capacity
// is reached.
// MODIFICATION MEMBER FUNCTIONS for the bag class:
// size_type erase(const value_type& target)
// Postcondition: All copies of target have been removed from the bag.
// The return value is the number of copies removed (which could be zero).
// bool erase_one(const value_type& target)
// Postcondition: If target was in the bag, then one copy has been removed;
// otherwise the bag is unchanged. A true return value indicates that one
// copy was removed; false indicates that nothing was removed.
// void insert(const value_type& entry)
// Postcondition: A new copy of entry has been inserted into the bag.
// void reserve(size_type new_capacity)
// Postcondition: The bag's current capacity is changed to the
// new capacity (but not less than the number of items already
// in the bag). The insert function will work efficiently (without allocating
// new memory) until the new capacity is reached.
// void operator +=(const bag& addend)
// Postcondition: Each item in addend has been added to this bag.

The reserve member function provides efficiency.
```
