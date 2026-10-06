STL Containers 673

Operations that remove entries from a collection throw exception when they fail.

To use the STL classes, you must include the appropriate header file, which has the same name as the STL class. To use the class stack, for example, your code must have the following statement:

```
#include <stack>
```

To instantiate an stack, you must supply the type of item it will hold, just as you instantiated our ADTs. For example, the following statement creates a vector that can hold 10 items:

```
vector<string> cities(10); // Create a vector to hold 10 strings
```

All STL containers are part of the std:: namespace. Therefore, if you do not use the statement

```
using namespace std;
```

in your code, you must precede any reference to the container with std:: as shown here:

```
std::vector<string> cities(10); // Create a vector to hold 10 strings
```

In our ADTs, we use ItemType to represent the type of item stored in the collection. The STL header files use value_type or simply T to represent the item in a collection. If the collection is similar to our ADT dictionary, with key and item types, the STL uses key_type and mapped_type respectively.

# C.7.1 STL Container Adapters

The STL container adapters are stack, queue and priority_queue. These correspond to the ADTs stack, queue, and priority queue and optimized so that the operations listed below perform at O(1). These containers grow to accommodate new entries as they are added. When entries are removed, the size of the container decreases. Thus, each of these containers has a size exactly equal to the number of entries in it currently.

| OPERATION | DESCRIPTION |
| --- | --- |
| value_type& top() | Returns a reference to the top entry on the stack. |
| void push(value_type& item) | Pushes item onto the top of the stack. |
| void pop() | Removes the top entry from the stack. |

| OPERATION | DESCRIPTION |
| --- | --- |
| value_type& front() | Returns a reference to the front entry in the queue. |
| value_type& back() | Returns a reference to the last (back) entry in the queue. |
| void push(value_type& item) | Adds item onto the back of the queue. |
| void pop() | Removes the front entry from the queue. |