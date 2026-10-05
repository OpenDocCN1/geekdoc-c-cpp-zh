# CHAPTER 19 Standard Template Library

Display 19.11 The set Template Class

# set TEMPLATE CLASS DETAILS

Type name: <set> or <set, Ordering> for a set of elements of type T. The Ordering is used to sort elements for storage. If no Ordering is given, the ordering used is the binary operator, <. Library header: <set>, which places the definition in the std namespace.
Defined types includes value_type, size_type.
Iterators iterator, const_iterator, reverse_iterator, and const_reverse_iterator. All iterators are bidirectional and not including const_ are mutable. begin(), end(), rbegin(), and rend() have the expected behavior. Adding or deleting elements does not affect iterators, except for an iterator located at the element removed.

# SAMPLE MEMBER FUNCTIONS

| MEMBER FUNCTION (IS A SET OBJECT) | MEANING |
| --- | --- |
| s.insert(Element) | Inserts a copy of Element in the set. If Element is already in the set, this has no effect. |
| s.erase(Element) | Removes Element from the set. If Element is not in the set, this has no effect. |
| s.find(Element) | Returns an iterator located at copy of Element in the set. If Element is not in the set, s.end() is returned. Whether the iterator is mutable or not is implementation dependent. |
| s.erase(Iterator) | Erases the element at the location of the Iterator. |
| s.size() | Returns the number of elements in the set. |
| s.empty() | Returns true if the set is empty; otherwise, returns false. |
| s1 == s2 | Returns true if the sets contain the same elements; otherwise, returns false. |

The set template class also has a default constructor, a copy constructor, and other specialized constructors not mentioned here. It has a destructor as well that returns all storage for recycling, and a well-behaved assignment operator.

Display 19.12 Using the set Template Class (part 1 of 2)

```
//Program to demonstrate use of the set template class.
#include <iostream>
#include <set>
using std::cout;
using std::endl;
using std::set;
```