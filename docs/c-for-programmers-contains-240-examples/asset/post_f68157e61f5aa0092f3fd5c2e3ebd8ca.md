
a stack of integers that uses a vector of integers as its underlying data structure. Line 26 specifies a stack of integers that uses a list of integers as its underlying data structure.

Function pushElements (lines 49–56) pushes the elements onto each stack. Line 53 uses function push (available in each adapter class) to place an integer on top of the stack. Line 54 uses stack function top to retrieve the top element of the stack for output. Function top does not remove the top element.

Function popElements (lines 59–66) pops the elements off each stack. Line 63 uses stack function top to retrieve the top element of the stack for output. Line 64 uses function pop (available in each adapter class) to remove the top element of the stack. Function pop does not return a value.

```
// Fig. 20.23: fig20_23.cpp
// Standard Library adapter stack test program.
#include <iostream>
using std::cout;
using std::endl;

#include <stack> // stack adapter definition
#include <vector> // vector class-template definition
#include <list> // list class-template definition

// pushElements function-template prototype
template< typename T > void pushElements( T &stackRef );

// popElements function-template prototype
template< typename T > void popElements( T &stackRef );

int main()
{
    // stack with default underlying deque
    std::stack< int > intDequeStack;

    // stack with underlying vector
    std::stack< int, std::vector< int > > intVectorStack;

    // stack with underlying list
    std::stack< int, std::list< int > > intListStack;

    // push the values 0-9 onto each stack
    cout << "Pushing onto intDequeStack: ";
    pushElements( intDequeStack );
    cout << "\nPushing onto intVectorStack: ";
    pushElements( intVectorStack );
    cout << "\nPushing onto intListStack: ";
    pushElements( intListStack );
    cout << endl << endl;

    // display and remove elements from each stack
    cout << "Popping from intDequeStack: ";
    popElements( intDequeStack );
```
```
40  cout << "\nPopping from intVectorStack: ";
41  popElements( intVectorStack );
42  cout << "\nPopping from intListStack: ";
43  popElements( intListStack );
44  cout << endl;
45  return 0;
46 } // end main

// push elements onto stack object to which stackRef refers
template< typename T > void pushElements( T &stackRef )
{
  for ( int i = 0; i < 10; i++ )
  {
    stackRef.push( i ); // push element onto stack
    cout << stackRef.top() << ' '; // view (and display) top element
  } // end for
} // end function pushElements

// pop elements from stack object to which stackRef refers
template< typename T > void popElements( T &stackRef )
{
  while ( !stackRef.empty() )
  {
    cout << stackRef.top() << ' '; // view (and display) top element
    stackRef.pop(); // remove top element
  } // end while
} // end function popElements
```

Pushing onto intDequeStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intVectorStack: 0 1 2 3 4 5 6 7 8 9
Pushing onto intListStack: 0 1 2 3 4 5 6 7 8 9

Popping from intDequeStack: 9 8 7 6 5 4 3 2 1 0
Popping from intVectorStack: 9 8 7 6 5 4 3 2 1 0
Popping from intListStack: 9 8 7 6 5 4 3 2 1 0

Fig. 20.23 | Standard Library stack adapter class. (Part 2 of 2.)

## 20.4.2 queue Adapter

Class queue enables insertions at the back of the underlying data structure and deletions from the front (commonly referred to as a first-in, first-out data structure). A queue can be implemented with STL data structure list or deque. By default, a queue is implemented with a deque. The common queue operations are push to insert an element at the back of the queue (implemented by calling function push_back of the underlying container), pop to remove the element at the front of the queue (implemented by calling function pop_front of the underlying container), front to get a reference to the first element in the queue (implemented by calling function front of the underlying container), back to get a reference to the last element in the queue (implemented by calling function back of the underlying container), empty to determine whether the queue is empty (implemented by calling function empty of the underlying container) and size to get the number of elements in the queue (implemented by calling function size of the underlying container).

## Performance Tip 20.18

Each of the common operations of a queue is implemented as an inline function that calls the appropriate function of the underlying container. This avoids the overhead of a second function call.

## Performance Tip 20.19

For the best performance, use class deque as the underlying container for a queue.

Figure 20.24 demonstrates the queue adapter class. Header file <queue> must be included to use a queue.

Line 11 instantiates a queue that stores double values. Lines 14–16 use function push to add elements to the queue. The while statement in lines 21–25 uses function empty (available in all containers) to determine whether the queue is empty (line 21). While there are more elements in the queue, line 23 uses queue function front to read (but not remove) the first element in the queue for output. Line 24 removes the first element in the queue with function pop (available in all adapter classes).

```
// Fig. 20.24: fig20_24.cpp
// Standard Library adapter queue test program.
#include <iostream>
using std::cout;
using std::endl;

#include <queue> // queue adapter definition

int main()
{
    std::queue< double > values; // queue with doubles

    // push elements onto queue values
    values.push( 3.2 );
    values.push( 9.8 );
    values.push( 5.4 );

    cout << "Popping from values: ";

    // pop elements from queue
    while ( !values.empty() )
    {
        cout << values.front() << ' '; // view front element
        values.pop(); // remove element
    } // end while

    cout << endl;
    return 0;
} // end main
```

Popping from values: 3.2 9.8 5.4

Fig. 20.24 | Standard Library queue adapter class templates.

## 20.4.3 priority_queue Adapter

Class priority_queue provides functionality that enables insertions in sorted order into the underlying data structure and deletions from the front of the underlying data structure. A priority_queue can be implemented with STL sequence containers vector or deque. By default, a priority_queue is implemented with a vector as the underlying container. When elements are added to a priority_queue, they are inserted in priority order, such that the highest-priority element (i.e., the largest value) will be the first element removed from the priority_queue. This is usually accomplished via a sorting technique called heapsort that always maintains the largest value (i.e., highest-priority element) at the front of the data structure—such a data structure is called a heap. The comparison of elements is performed with comparator function object less<T> by default, but you can supply a different comparator.

There are several common priority_queue operations. push inserts an element at the appropriate location based on priority order of the priority_queue (implemented by calling function push_back of the underlying container, then reordering the elements using heapsort). pop removes the highest-priority element of the priority_queue (implemented by calling function pop_back of the underlying container after removing the top element of the heap). top gets a reference to the top element of the priority_queue (implemented by calling function front of the underlying container). empty determines whether the priority_queue is empty (implemented by calling function empty of the underlying container). size gets the number of elements in the priority_queue (implemented by calling function size of the underlying container).

## Performance Tip 20.20

Each of the common operations of a priority_queue is implemented as an inline function that calls the appropriate function of the underlying container. This avoids the overhead of a second function call.

## Performance Tip 20.21

For the best performance, use class vector as the underlying container for a priority_queue.

Figure 20.25 demonstrates the priority_queue adapter class. Header file <queue> must be included to use class priority_queue.

```
// Fig. 20.25: fig20_25.cpp
// Standard Library adapter priority_queue test program.
#include <iostream>
using std::cout;
using std::endl;

#include <queue> // priority_queue adapter definition

int main()
{
    std::priority_queue< double > priorities; // create priority_queue
```
