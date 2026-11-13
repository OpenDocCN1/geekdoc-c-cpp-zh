3.14 Looking ahead in an STL iterator requires an application of operator++, which in turn advances the iterator. In some cases looking at the next item in the list, without advancing to it, may be preferable. Write the member function with the declaration `const_iterator operator+( int k ) const;` to facilitate this in a general case. The binary operator+ returns an iterator that corresponds to k positions ahead of current.

3.15 Add the splice operation to the List class. The method declaration `void splice( iterator position, List<T>& lst );` removes all the items from lst, placing them prior to position in List *this. lst and *this must be different lists. Your routine must run in constant time.

3.16 Add reverse iterators to the STL List class implementation. Define reverse_iterator and const_reverse_iterator. Add the methods rbegin and rend to return appropriate reverse iterators representing the position prior to the endmarker and the position that is the header node. Reverse iterators internally reverse the meaning of the ++ and -- operators. You should be able to print a List L in reverse by using the code

```
List<Object>::reverse_iterator itr = L.rbegin( );
while ( itr != L.rend( ) )
    cout << *itr++ << endl;
```

3.17 Modify the List class to provide stringent iterator checking by using the ideas suggested at the end of Section 3.5.

3.18 When an erase method is applied to a list, it invalidates any iterator that is referencing the removed node. Such an iterator is called stale. Describe an efficient algorithm that guarantees that any operation on a stale iterator acts as though the iterator's current is nullptr. Note that there may be many stale iterators. You must explain which classes need to be rewritten in order to implement your algorithm.

3.19 Rewrite the List class without using header and tail nodes and describe the differences between the class and the class provided in Section 3.5.

3.20 An alternative to the deletion strategy we have given is to use lazy deletion. To delete an element, we merely mark it deleted (using an extra bit field). The number of deleted and nondeleted elements in the list is kept as part of the data structure. If there are as many deleted elements as nondeleted elements, we traverse the entire list, performing the standard deletion algorithm on all marked nodes.
a. List the advantages and disadvantages of lazy deletion.
b. Write routines to implement the standard linked list operations using lazy deletion.

3.21 Write a program to check for balancing symbols in the following languages:
a. Pascal (begin, end, {, ], (, )).
b. C++ (/* */, /, [, ], {, } ).
* c. Explain how to print out an error message that is likely to reflect the probable cause.