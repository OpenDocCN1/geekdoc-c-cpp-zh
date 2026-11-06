
![](img/023f159fdd47d944d48e08843cea732d_991_0.png)

> **Performance Tip 22.19**
>
> *Each of the common operations of a queue is implemented as an inline function that calls the appropriate function of the underlying container. This avoids the overhead of a second function call.*

Figure 22.24 demonstrates the queue adapter class. Header file `<queue>` must be included to use a queue.

```cpp
1  // Fig. 22.24: Fig22_24.cpp
2  // Standard Library adapter queue test program.
3  #include <iostream>
4  #include <queue> // queue adapter definition
5  using namespace std;
6
7  int main()
8  {
9      queue< double > values; // queue with doubles
10
11     // push elements onto queue values
12     values.push( 3.2 );
13     values.push( 9.8 );
14     values.push( 5.4 );
15
16     cout << "Popping from values: ";
17
18     // pop elements from queue
19     while ( !values.empty() )
20     {
21         cout << values.front() << ' '; // view front element
22         values.pop(); // remove element
23     } // end while
24
25     cout << endl;
26 } // end main
```

Popping from values: 3.2 9.8 5.4

**Fig. 22.24** | Standard Library queue adapter class templates.

Line 9 instantiates a queue that stores double values. Lines 12–14 use function push to add elements to the queue. The while statement in lines 19–23 uses function empty (available in all containers) to determine whether the queue is empty (line 19). While there are more elements in the queue, line 21 uses queue function front to read (but not remove) the first element in the queue for output. Line 22 removes the first element in the queue with function pop (available in all adapter classes).

### 22.4.3 `priority_queue` Adapter

Class `priority_queue` provides functionality that enables insertions in sorted order into the underlying data structure and deletions from the front of the underlying data structure. A `priority_queue` can be implemented with STL sequence containers vector or deque. By default, a priority_queue is implemented with a vector as the underlying container. When elements are added to a priority_queue, they’re inserted in priority order, such that the highest-priority element (i.e., the largest value) will be the first element removed from the priority_queue. This is usually accomplished by arranging the elements in a binary tree structure called a heap that always maintains the largest value (i.e., highest-priority element) at the front of the data structure. We discuss the STL’s heap algorithms in Section 22.5.12. The comparison of elements is performed with comparator function object less<T> by default, but you can supply a different comparator.

There are several common priority_queue operations. push inserts an element at the appropriate location based on priority order of the priority_queue (implemented by calling function push_back of the underlying container, then reordering the elements using heap sort). pop removes the highest-priority element of the priority_queue (implemented by calling function pop_back of the underlying container after removing the top element of the heap). top gets a reference to the top element of the priority_queue (implemented by calling function front of the underlying container). empty determines whether the priority_queue is empty (implemented by calling function empty of the underlying container). size gets the number of elements in the priority_queue (implemented by calling function size of the underlying container).

> **Performance Tip 22.20**
>
> *Each of the common operations of a priority_queue is implemented as an inline function that calls the appropriate function of the underlying container. This avoids the overhead of a second function call.*

![](img/023f159fdd47d944d48e08843cea732d_992_0.png)

> **Performance Tip 22.21**
>
> *For the best performance, use class vector as the underlying container for a priority_queue.*

![](img/023f159fdd47d944d48e08843cea732d_992_1.png)

Figure 22.25 demonstrates the priority_queue adapter class. Header file `<queue>` must be included to use class priority_queue.

```cpp
// Fig. 22.25: Fig22_25.cpp
// Standard Library adapter priority_queue test program.
#include <iostream>
#include <queue> // priority_queue adapter definition
using namespace std;

int main()
{
   priority_queue< double > priorities; // create priority_queue

   // push elements onto priorities
   priorities.push( 3.2 );
   priorities.push( 9.8 );
   priorities.push( 5.4 );

   cout << "Popping from priorities: ";

   // pop element from priority_queue
   while ( !priorities.empty() )
   {
       cout << priorities.top() << ' '; // view top element
       priorities.pop(); // remove top element
   } // end while

   cout << endl;
} // end main
```

Popping from priorities: 9.8 5.4 3.2

**Fig. 22.25** | Standard Library `priority_queue` adapter class.

Line 9 instantiates a priority_queue that stores double values and uses a vector as the underlying data structure. Lines 12–14 use function push to add elements to the priority_queue. The while statement in lines 19–23 uses function empty (available in all containers) to determine whether the priority_queue is empty (line 19). While there are more elements, line 21 uses priority_queue function top to retrieve the highest-priority element in the priority_queue for output. Line 22 removes the highest-priority element in the priority_queue with function pop (available in all adapter classes).

## 22.5 Algorithms

Until the STL, class libraries of containers and algorithms were essentially incompatible among vendors. Early container libraries generally used inheritance and polymorphism, with the associated overhead of virtual function calls. Early libraries built the algorithms into the container classes as class behaviors. The STL separates the algorithms from the containers. This makes it much easier to add new algorithms. With the STL, the elements of containers are accessed through iterators. The next several subsections demonstrate many of the STL algorithms.

> **Performance Tip 22.22**
>
> *The STL is implemented for efficiency. It avoids the overhead of virtual function calls.*

> **Software Engineering Observation 22.8**
>
> *STL algorithms do not depend on the implementation details of the containers on which they operate. As long as the container’s (or array’s) iterators satisfy the requirements of the algorithm, STL algorithms can work on C-style, pointer-based arrays, on STL containers and on user-defined data structures.*

> **Software Engineering Observation 22.9**
>
> *Algorithms can be added easily to the STL without modifying the container classes.*

```cpp
int main()
{
    const int SIZE = 10;
    int a1[ SIZE ] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int a2[ SIZE ] = { 1, 2, 3, 4, 1000, 6, 7, 8, 9, 10 };
    vector< int > v1( a1, a1 + SIZE ); // copy of a1
    vector< int > v2( a1, a1 + SIZE ); // copy of a1
    vector< int > v3( a2, a2 + SIZE ); // copy of a2
    ostream_iterator< int > output( cout, " " );

    cout << "Vector v1 contains: ";
    copy( v1.begin(), v1.end(), output );
    cout << "\nVector v2 contains: ";
    copy( v2.begin(), v2.end(), output );
    cout << "\nVector v3 contains: ";
    copy( v3.begin(), v3.end(), output );

    // compare vectors v1 and v2 for equality
    bool result = equal( v1.begin(), v1.end(), v2.begin() );
    cout << "\n\nVector v1 " << ( result ? "is" : "is not" )
         << " equal to vector v2.\n";

    // compare vectors v1 and v3 for equality
    result = equal( v1.begin(), v1.end(), v3.begin() );
    cout << "Vector v1 " << ( result ? "is" : "is not" )
         << " equal to vector v3.\n";

    // location represents pair of vector iterators
    pair< vector< int >::iterator, vector< int >::iterator > location;

    // check for mismatch between v1 and v3
    location = mismatch( v1.begin(), v1.end(), v3.begin() );
    cout << "\nThere is a mismatch between v1 and v3 at location "
         << ( location.first - v1.begin() ) << "\nwhere v1 contains "
         << *location.first << " and v3 contains " << *location.second
         << "\n";

    char c1[ SIZE ] = "HELLO";
    char c2[ SIZE ] = "BYE BYE";

    // perform lexicographical comparison of c1 and c2
    result = lexicographical_compare( c1, c1 + SIZE, c2, c2 + SIZE );
    cout << c1 << ( result ? " is less than " :
         " is greater than or equal to " ) << c2 << endl;
} // end main
```

```text
Vector v1 contains: 1 2 3 4 5 6 7 8 9 10
Vector v2 contains: 1 2 3 4 5 6 7 8 9 10
Vector v3 contains: 1 2 3 4 1000 6 7 8 9 10

Vector v1 is equal to vector v2.
Vector v1 is not equal to vector v3.
```

**Fig. 22.27** | Algorithms equal, mismatch and lexicographical_compare. (Part 2 of 3.)
