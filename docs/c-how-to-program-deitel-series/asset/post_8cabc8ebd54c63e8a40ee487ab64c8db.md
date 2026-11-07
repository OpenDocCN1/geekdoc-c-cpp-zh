
```cpp
// insert elements of ints into otherValues
otherValues.insert( otherValues.begin(), ints.begin(), ints.end() );
otherValues.sort(); // sort the list
cout << "\nAfter insert and sort, otherValues contains: ";
printList( otherValues );

// remove otherValues elements and insert into values in sorted order
values.merge( otherValues );
cout << "\nAfter merge, values contains: ";
printList( values );
cout << "\n\totherValues contains: ";
printList( otherValues );

values.pop_front(); // remove element from front
values.pop_back(); // remove element from back
cout << "\nAfter pop_front and pop_back:\n\t values contains: ";
printList( values );

values.unique(); // remove duplicate elements
cout << "\nAfter unique, values contains: ";
printList( values );

// swap elements of values and otherValues
values.swap( otherValues );
cout << "\nAfter swap:\n\t values contains: ";
printList( values );
cout << "\n\t otherValues contains: ";
printList( otherValues );

// replace contents of values with elements of otherValues
values.assign( otherValues.begin(), otherValues.end() );
cout << "\nAfter assign, values contains: ";
printList( values );

// remove otherValues elements and insert into values in sorted order
values.merge( otherValues );
cout << "\nAfter merge, values contains: ";
printList( values );

values.remove( 4 ); // remove all 4s
cout << "\nAfter remove( 4 ), values contains: ";
printList( values );
cout << endl;
} // end main

// printList function template definition; uses
// ostream_iterator and copy algorithm to output list elements
template < typename T > void printList( const list< T > &listRef )
{
    if ( !listRef.empty() ) // list is empty
        cout << "List is empty";
    else
    {
        ostream_iterator<T> output(cout, " ");
        copy( listRef.cbegin(), listRef.cend(), output );
    } // end else
} // function printList
```

Fig. 15.13 | Standard Library list class template. (Part 2 of 3.)

```text
values contains: 2 1 4 3
values after sorting contains: 1 2 3 4
After insert, otherValues contains: 2 2 6 4 8
After splice, values contains: 1 2 3 4 2 6 4 8
After sort, values contains: 1 2 2 3 4 4 6 8
After insert and sort, otherValues contains: 2 2 4 4 6 8
After merge:
    values contains: 1 2 2 2 3 4 4 4 6 6 8 8
    otherValues contains: List is empty
After pop_front and pop_back:
    values contains: 2 2 2 3 4 4 6 6 8
After unique, values contains: 2 3 4 6 8
After swap:
    values contains: List is empty
    otherValues contains: 2 3 4 6 8
After assign, values contains: 2 3 4 6 8
After merge, values contains: 2 2 3 3 4 4 6 6 8 8
After remove(4), values contains: 2 2 3 3 6 6 8 8
```

Fig. 15.13 | Standard library list class template (Part 3 of 3.)

### Creating list Objects

Lines 17–18 instantiate two list objects capable of storing ints. Lines 21–22 use function push_front to insert integers at the beginning of values. Function push_front is specific to classes forward_list, list and deque. Lines 23–24 use function push_back to insert integers at the end of values. Function push_back is common to all sequence containers, except array and forward_list.

### List Member Function sort

Line 29 uses list member function sort to arrange the elements in the list in ascending order. [Note: This is different from the sort in the Standard Library algorithms.] A second version of function sort allows you to supply a binary predicate function that takes two arguments (values in the list), performs a comparison and returns a bool value indicating whether the first argument should come before the second in the sorted contents. This function determines the order in which the elements of the list are sorted. This version could be particularly useful for a list that stores pointers rather than values. [Note: We demonstrate a unary predicate function in Fig. 16.3. A unary predicate function takes a single argument, performs a comparison using that argument and returns a bool value indicating the result.]

### List Member Function splice

Line 39 uses list function splice to remove the elements in otherValues and insert them into values before the iterator position specified as the first argument. There are two other versions of this function. Function splice with three arguments allows one element to be removed from the container specified as the second argument from the location specified by the iterator in the third argument. Function splice with four arguments uses the

```cpp
// use subscript operator to modify element at location 1
values[ 1 ] = 5.4;
cout << "\nAfter values[ 1 ] = 5.4, values contains: ";
copy( values.cbegin(), values.cend(), output );
cout << endl;
} // end main
```

```text
values contains: 3.5 2.2 1.1
After pop_front, values contains: 2.2 1.1
After values[ 1 ] = 5.4, values contains: 2.2 5.4
```

**Fig. 15.14** Standard Library deque class template. (Part 2 of 2.)

Line 11 instantiates a deque that can store double values. Lines 15–17 use functions `push_front` and `push_back` to insert elements at the beginning and end of the deque.

The `for` statement in lines 22–23 uses the subscript operator to retrieve the value in each element of the deque for output. The condition uses function `size` to ensure that we do not attempt to access an element outside the bounds of the deque.

Line 25 uses function `pop_front` to demonstrate removing the first element of the deque. Line 30 uses the subscript operator to obtain an *lvalue*. This enables values to be assigned directly to any element of the deque.

## 15.6 Associative Containers

The *associative containers* provide direct access to store and retrieve elements via **keys** (often called **search keys**). The four *ordered associative containers* are multiset, set, multimap and map. Each of these maintains its keys in *sorted order*. There are also four corresponding *unordered associative containers*—unordered_multiset, unordered_set, unordered_multimap and unordered_map—that offer most of the same capabilities as their ordered counterparts. The primary difference between the ordered and unordered associative containers is that the unordered ones do not maintain their keys in *sorted order*. In this section, we focus on the *ordered associative containers*.

![](img/b42ba5cd262b1358d16610173f975e4d_699_0.png)

**Performance Tip 15.10**

> *The unordered associative containers might offer better performance for cases in which it’s not necessary to maintain keys in sorted order.*

Iterating through an *ordered associative container* traverses it in the sort order for that container. Classes **multiset** and **set** provide operations for manipulating sets of values where the values are the keys—there is *not* a separate value associated with each key. The primary difference between a multiset and a set is that a multiset allows duplicate keys and a set does not. Classes **multimap** and **map** provide operations for manipulating values associated with keys (these values are sometimes referred to as *mapped values*). The primary difference between a multimap and a map is that a multimap allows duplicate keys with associated values to be stored and a map allows only *unique keys* with associated values. In addition to the common container member functions, *ordered associative containers* also support several other member functions that are specific to associative containers. Examples of each of the *ordered associative containers* and their common member functions are presented in the next several subsections.

### 15.6.6 multiset Associative Container

The multiset *ordered associative container* (from header `<set>`) provides fast storage and retrieval of keys and allows duplicate keys. The elements’ ordering is determined by a so-called **comparator function object**. For example, in an integer multiset, elements can be sorted in *ascending order* by ordering the keys with **comparator function object less\<int\>**. We discuss function objects in detail in Section 16.4. For this chapter, we’ll simply show how to use `less<int>` when declaring ordered associative containers. The data type of the keys in all *ordered associative containers* must support comparison based on the comparator function object—keys sorted with `less<int>` must support comparison with operator\<. If the keys used in the *ordered associative containers* are of user-defined data types, those types must supply the appropriate comparison operators. A multiset supports *bidirectional iterators* (but not *random-access iterators*). If the order of the keys is not important, you can use unordered_multiset (header `<unordered_set>`) instead.

Figure 15.15 demonstrates the multiset *ordered associative container* for a multiset of ints with keys that are sorted in *ascending order*. Containers multiset and set (Section 15.6.2) provide the same basic functionality.

```cpp
// Fig. 15.15: fig15_15.cpp
// Standard Library multiset class template
#include <array>
#include <iostream>
#include <set> // multiset class-template definition
#include <algorithm> // copy algorithm
#include <iterator> // ostream_iterator
using namespace std;

int main()
{
   const size_t SIZE = 10;
   array<int, SIZE> a = { 1, 22, 9, 1, 18, 30, 100, 22, 85, 13 };
   multiset<int, less<int> > intMultiset; // multiset of ints
   ostream_iterator<int> output(cout, " ");

   cout << "There are currently " << intMultiset.count(15)
      << " values of 15 in the multiset\n";

   intMultiset.insert(15); // insert 15 in intMultiset
   intMultiset.insert(15); // insert 15 in intMultiset
   cout << "After inserts, there are " << intMultiset.count(15)
      << " values of 15 in the multiset\n";

   // find 15 in intMultiset; find returns iterator
   auto result = intMultiset.find(15);

   if (result != intMultiset.end()) // if iterator not at end
      cout << "Found value 15\n"; // found search value 15
```

**Fig. 15.15** | Standard Library multiset class template. (Part 1 of 2.)
