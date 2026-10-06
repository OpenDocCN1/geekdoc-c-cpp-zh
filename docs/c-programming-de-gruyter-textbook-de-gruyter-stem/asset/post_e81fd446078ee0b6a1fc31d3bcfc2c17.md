
# 10.2 Containers in STL - 417

```cpp
cout << "Popping fromDequeStack: ";
popElements( intDequeStack ); //pop the element in stack
cout << endl;
}
```

```cpp
template< class T>
void popElements( T &s ) //define a template function
{
    while ( s.empty() ) {
        cout << s.top() << ' '; //get the top element of stack and
        //print
        s.pop(); //use pop to remove the top element
    }
}
```

Results:

| Popping from intDequeStack: 9 8 7 6 5 4 3 2 1 0 |

# 2. Queues

Queue adapters provide interfaces for First In Out (FIFO) services, i.e., adding an element to the tail of the container (enqueuing) and removing the first element of the container (dequeuing). Queues are implemented based on an underlying storage, typically a list or deque. The default underlying implementation of storage is the deque. Here is an example of a declaration of a queue, using the deque as the underlying storage implementation:

```cpp
queue<int, deque<int>> myQueue;
```

The method push() adds an element to the tail of the queue, the method pop() removes the first element of the queue, and the methods front() and back() return the reference of the head and the tail of the queue respectively. The method empty() checks whether the queue is empty, and the method size() returns the number of elements in the queue. Please refer to related documents like MSDN for detailed information. Here is a simple example using a queue.

# Example 10.5: Initialize a queue with integers.

```cpp
//10_5.cpp
#include <iostream>
#include <queue> //include queue adapter header file
using namespace std;
```

```cpp
template< class T>
void popElements( T &s );
```

# 418 10 Generic Programming and the Standard Template Library

```cpp
int main()
{
    queue<int> intDequeQueue; //use queue as the default container
    for (int i = 0; i < 10; ++i ) {
        intDequeQueue.push( i ); //push the integer in deque as the
                                //top of the queue
    }

    cout << "Popping from intDequeQueue: ";
    popElements(intDequeQueue); //pop the top element of the queue
                                //and print

    cout << endl;
}
```

```cpp
template< class T>
void popElements(T &s ) //define a template function
{
    while (!s.empty()) {
        cout << s.front() << ' '; //use front to get top element of
                                //Queue and print
        s.pop(); //use pop to remove the top element
    }
}
```

Results:

| Popping from intDequeQueue: 0 1 2 3 4 5 6 7 8 9 |

Similar to stacks and queues, a priority queue is another adapter for implementing an advanced data structure. Priority queues are designed as ordered queues, which are able to extract the highest priority element from a queue.

# 10.3 Iterators

Iterators are an object-oriented version of a pointer. They provide a uniform mechanism with which to traverse through a container. Pointers point to a memory location, so that program is able to access the object at the memory location through the pointer. You can see iterator as a type-safe pointer – it points to an object of a specific type.

the iterator is a common design pattern for bridging algorithms and containers. Real algorithms need to traverse a linear collection, traversing a linked list through a pointer or traversing an array subscripts. It is good to use an algorithm that works for linear collections, so that you do not have to implement an algorithm many times for every type of linear collections. Therefore, the algorithm needs an abstraction layer to handle things “get me the next element”, or “is it the end?”. In theory, pointers can handle this issue, but make the implementation of algorithms and containers more complicated. For an object-oriented pointer, an iterator is included in STL to enable writing abstract algorithms that works on all containers.

# 10.3.1 Types of Iterators

There are five basic types of iterators: the input iterator, output iterator, forward iterator, bidirectional iterator, and random access iterator. There are two iterator adapters: the reverse iterator adapter and insert iterator adapter.

# 1. Categories

An input iterator can read data from a collection and an output iterator can write data to a collection.

A forward iterator is both an input iterator and output iterator, and it can traverse through the collection in a certain direction. A bidirectional iterator can traverse the collection in both directions. A random access iterator can access any position in a collection.

# 2. Iterator Adapters

An iterator adapter is an adapter that extends or adjusts the functions of an iterator. There are two types of iterator adapters: 

- The reverse iterator adapter reverses the functionalities of the increment order and decrement operator, so that the algorithm processes the elements in a reversed order. All standard containers can be used with reverse iterators.
- The insert iterator overloads the assignment operator and turns it into inserters, so algorithms running on its elements into the collections rather than overwriting the value of the elements. There are three types of insert adapters: back inserters, front inserters, and general inserters. Back inserters append an element to the end of a collection, and front inserters add an element at the head of a collection. General inserters decide the insertion.

Here is an example of an iterator adapter.

# Example 10.6: Example of iterator adapter.

```cpp
//10_6.cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int A[] = {1, 2, 3, 4, 5};
    const int N = sizeof(A)/sizeof(int);
    vector<int> col1(A,N);

    cout << "List1 contains: ";
    copy(col1.begin(), col1.end(), output);

    vector<int>::iterator pos=col1.begin();
    cout<<"\nThe fist element is: "<<pos;

    vector<int>::reverse_iterator rpos=col1.rbegin();
    cout<<"\nThe last element is: "<<rpos<<endl;

    back_insert_iterator<vector<int>> > iter(col1);
    *iter=66;
    back_inserter(col1)=88;
    copy(col1.begin(), col1.end(), output);

    cout <<endl;
}
```

Results:

| List1 contains: 1 2 3 4 5 |
| The fist element is: 1 |
| The last element is: 5 |
| 1 2 3 4 5 66 88 |

# 10.3.2 Auxiliary Functions in Iterators

There are three auxiliary functions in iterators: advance(), distance(), and iter_swap(). advance() and distance() emulate the power of random access iterators such as advancing and going back for several positions and calculating the distances of two iterates, through basic iterator primitives. Iter_swap() allows programmers to swap the values that two iterators are pointing to.

- 1. advance() move the position of an iterator forward or backward by n position. Here is the prototype: 

```cpp
void advance(InputIterator & pos, Dist n);
```

In bidirectional or random access iterators, n can be negative so that the iterator goes back for n elements.

- 2. distance() calculates the distances between two iterators: 

```cpp
Dist distance(InputIterator pos1, InputIterator pos2);
```

pos1 and pos2 should point to the same container. If the iterators are not random access iterates, then pos1 must be able to reach pos2 via advance.

- 3. iter_swap() swaps the values that two iterators are pointing to: 

```cpp
void iter_swap(ForwardIterator1 pos1, ForwardIterator2 pos2);
```

pos1 and pos2 may point to different containers, but the elements they are pointing to must be able to assign to each other.

Here is an example:

Example 10.7: Example of auxiliary function adapters.

```cpp
#include <iostream>
#include <list>
#include <algorithm>
using namespace std;

int main() {
    int A[] = {1, 2, 3, 4, 5};
    const int N = sizeof(A)/sizeof(int);
    list<int> col1(A,N);

    advance(col1.begin(), 2);
    cout << "Element after advance 2: " << *col1.begin() << endl;

    cout << "Distance: " << distance(col1.begin(), col1.end()) << endl;

    list<int> l1 = {10, 20};
    list<int> l2 = {30, 40};
    iter_swap(l1.begin(), l2.begin());
    cout << "l1: " << *l1.begin() << ", l2: " << *l2.begin() << endl;
}
```
