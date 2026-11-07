
```cpp
// return copy of data in node
template< typename NODETYPE >
NODETYPE ListNode< NODETYPE >::getData() const
{
   return data;
} // end function getData

#endif
```

### Fig. 20.3 | ListNode class-template definition.

Lines 23–24 of the List class template (Fig. 20.4) declare private data members `firstPtr` (a pointer to the first ListNode in a List) and `lastPtr` (a pointer to the last ListNode in a List). The default constructor (lines 31–36) initializes both pointers to 0 (null). The destructor (lines 39–59) ensures that all ListNode objects in a List object are destroyed when that List object is destroyed. The primary List functions are insertAtFront (lines 62–74), insertAtBack (lines 77–89), removeFromFront (lines 92–110) and removeFromBack (lines 113–140).

Function isEmpty (lines 143–147) is called a *predicate function*—it does not alter the List; rather, it determines whether the List is empty (i.e., the pointer to the first node of the List is null). If the List is empty, true is returned; otherwise, false is returned. Function print (lines 158–178) displays the List’s contents. Utility function getNewNode (lines 150–155) returns a dynamically allocated ListNode object. This function is called from functions insertAtFront and insertAtBack.

![](img/bfd978e7e9b192bab46ec2a89e481263_785_0.png)

> **Error-Prevention Tip 20.1**
>
> *Assign null (0) to the link member of a new node. Pointers must be initialized before they’re used.*

```cpp
// Fig. 20.4: List.h
// Template List class definition.
#ifndef LIST_H
#define LIST_H

#include <iostream>
#include "ListNode.h" // ListNode class definition
using namespace std;

template< typename NODETYPE >
class List
{
public:
   List(); // constructor
   ~List(); // destructor
   void insertAtFront( const NODETYPE & );
   void insertAtBack( const NODETYPE & );
   bool removeFromFront( NODETYPE & );
   bool removeFromBack( NODETYPE & );
   bool isEmpty() const;
   void print() const;
private:
    ListNode< NODETYPE > *firstPtr; // pointer to first node
    ListNode< NODETYPE > *lastPtr;  // pointer to last node

    // utility function to allocate new node
    ListNode< NODETYPE > *getNewNode( const NODETYPE & );

}; // end class List

// default constructor
template< typename NODETYPE >
List< NODETYPE >::List()
    : firstPtr( 0 ), lastPtr( 0 )
{
    // empty body
} // end List constructor

// destructor
template< typename NODETYPE >
List< NODETYPE >::~List()
{
    if ( !isEmpty() ) // List is not empty
    {
        cout << "Destroying nodes\n";

        ListNode< NODETYPE > *currentPtr = firstPtr;
        ListNode< NODETYPE > *tempPtr;

        while ( currentPtr != 0 ) // delete remaining nodes
        {
            tempPtr = currentPtr;
            cout << tempPtr->data << "\n";
            currentPtr = currentPtr->nextPtr;
            delete tempPtr;
        } // end while
    } // end if

    cout << "All nodes destroyed\n\n";
} // end List destructor

// insert node at front of list
template< typename NODETYPE >
void List< NODETYPE >::insertAtFront( const NODETYPE &value )
{
    ListNode< NODETYPE > *newPtr = getNewNode( value ); // new node

    if ( isEmpty() ) // List is empty
        firstPtr = lastPtr = newPtr; // new list has only one node
    else // List is not empty
    {
        newPtr->nextPtr = firstPtr; // point new node to previous 1st node
        firstPtr = newPtr; // aim firstPtr at new node
    } // end else
} // end function insertAtFront

// insert node at back of list
template < typename NODETYPE >
void List< NODETYPE >::insertAtBack( const NODETYPE &value )
{
    ListNode< NODETYPE > * newPtr = getNewNode( value ); // new node

    if ( isEmpty() ) // List is empty
        firstPtr = lastPtr = newPtr; // new list has only one node
    else // List is not empty
    {
        lastPtr->nextPtr = newPtr; // update previous last node
        lastPtr = newPtr; // new last node
    } // end else
} // end function insertAtBack

// delete node from front of list
template< typename NODETYPE >
bool List< NODETYPE >::removeFromFront( NODETYPE &value )
{
    if ( isEmpty() ) // List is empty
        return false; // delete unsuccessful
    else
    {
        ListNode< NODETYPE > *tempPtr = firstPtr; // hold tempPtr to delete

        if ( firstPtr == lastPtr ) // List has one element
            firstPtr = lastPtr = 0; // no nodes remain after removal
        else
            firstPtr = firstPtr->nextPtr; // point to previous 2nd node

        value = tempPtr->data; // return data being removed
        delete tempPtr; // reclaim previous front node
        return true; // delete successful
    } // end else
} // end function removeFromFront

// delete node from back of list
template< typename NODETYPE >
bool List< NODETYPE >::removeFromBack( NODETYPE &value )
{
    if ( isEmpty() ) // List is empty
        return false; // delete unsuccessful
    else
    {
        ListNode< NODETYPE > *tempPtr = lastPtr; // hold tempPtr to delete

        if ( firstPtr == lastPtr ) // List has one element
            firstPtr = lastPtr = 0; // no nodes remain after removal
        else
        {
            ListNode< NODETYPE > *currentPtr = firstPtr;

            // locate second-to-last element
            while ( currentPtr->nextPtr != lastPtr )
                currentPtr = currentPtr->nextPtr; // move to next node

            lastPtr = currentPtr; // remove last node
            currentPtr->nextPtr = 0; // this is now the last node
        } // end else

        value = tempPtr->data; // return value from old last node
        delete tempPtr; // reclaim former last node
        return true; // delete successful
    } // end else
} // end function removeFromBack

// is List empty?
template< typename NODETYPE >
bool List< NODETYPE >::isEmpty() const
{
    return firstPtr == 0;
} // end function isEmpty

// return pointer to newly allocated node
template< typename NODETYPE >
ListNode< NODETYPE > *List< NODETYPE >::getNewNode(
    const NODETYPE &value )
{
    return new ListNode< NODETYPE >( value );
} // end function getNewNode

// display contents of List
template< typename NODETYPE >
void List< NODETYPE >::print() const
{
    if ( isEmpty() ) // List is empty
    {
        cout << "The list is empty\n\n";
        return;
    } // end if

    ListNode< NODETYPE > *currentPtr = firstPtr;

    cout << "The list is: ";

    while ( currentPtr != 0 ) // get element data
    {
        cout << currentPtr->data << ' ';
        currentPtr = currentPtr->nextPtr;
    } // end while

    cout << "\n\n";
} // end function print

#endif
```

### Fig. 20.4 | List class-template definition.

In Fig. 20.5, Lines 69 and 73 create List objects for types int and double, respectively. Lines 70 and 74 invoke the testList function template to manipulate objects.

```cpp
// Fig. 20.5: Fig20_05.cpp
// List class test program.
#include <iostream>
#include <string>
#include "List.h" // List class definition
using namespace std;

// display program instructions to user
void instructions()
{
   cout << "Enter one of the following:\n"
        << "  1 to insert at beginning of list\n"
        << "  2 to insert at end of list\n"
        << "  3 to delete from beginning of list\n"
        << "  4 to delete from end of list\n"
        << "  5 to end list processing\n";
} // end function instructions

// function to test a List
template< typename T >
void testList( List< T > &listObject, const string &typeName )
{
   cout << "Testing a List of " << typeName << " values\n";
   instructions(); // display instructions

   int choice; // store user choice
   T value; // store input value

   do // perform user-selected actions
   {
      cout << "? ";
      cin >> choice;

      switch ( choice )
      {
         case 1: // insert at beginning
            cout << "Enter " << typeName << ": ";
            cin >> value;
            listObject.insertAtFront( value );
            listObject.print();
            break;
```

### Fig. 20.5 | Manipulating a linked list.
