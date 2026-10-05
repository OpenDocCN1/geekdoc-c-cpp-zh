# Object-Oriented Programming with C++

This function erases all elements in a list.

```
list<int> ilist;
lilist.push_back(1);
list.push_back(2);
list.push_back(3);
cout<<ilist.size()<<endl; //outputs 3
//removes all elements of the
//list
ilist.clear();

cout<<ilist.size()<<endl; //outputs 0
```

# The list<>::empty() Function

This function is used to test whether a list is empty or not.

```
if(ilist.empty())
    //do something
else
    //do something else
```

Insertion into and deletion from an intermediate position in a list is because for such operations only the pointers of the affected element need to be reassigned.
 the other hand, random access to a particular element is inefficient. For traversing to the element that has our desired value, value of the pointer in each of the preceding elements has to be read starting from the first element since the elements are not in contiguous blocks of memory.

# 10.4.2 vector Class

The vector class is used to create sequential containers. Elements of the list are single objects.
The names of member functions of the vector class are the same as those of the list class. Global functions, like the find() function that works on objects of the list class, have been overloaded to work upon objects of the vector class.

However, the layout of elements in a vector is completely different from in a list. In a vector, unlike a list, elements are stored in contiguous blocks (like an array).
For using the vector template class, the header file needs to be included in the source code.

```
#include<vector>
```

A vector does not actually grow itself with each individual insertion. The amount of memory a vector captures is larger than the number of elements it actually stores. When this storage becomes full, it again grows itself by a certain amount to accommodate the latest insertion. The amount by which a vector grows differs from compiler to compiler.
This brings us two important concepts about vectors, namely capacity and size.
Capacity is the total size of the block currently captured by a vector. Obviously, it is directly proportional to the total number of elements that can be inserted into the vector before it needs to regrow.

Size, on the other hand, is the number of elements actually stored in the memory block that has been captured by the vector. Obviously, size of a vector is always less than or equal to its capacity.