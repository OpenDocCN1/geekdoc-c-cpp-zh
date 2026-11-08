
The statements in Lines 45 through 50 insert Donny, Zippy, Goofy, Hungry, Goofy, and Donny into `namesMultiSet`. The statement in Line 52 outputs the elements of `namesMultiSet`.

## Container Adapters

The previous sections discussed several types of containers. In addition to the containers that work in a general framework, the STL provides containers to accommodate special situations. These containers, called **container adapters**, are adapted standard STL containers to work in a specific environment. The three container adapters are:

- Stacks
- Queues
- Priority queues

Container adapters do not support any type of iterator. That is, iterators cannot be used with these types of containers. The next two sections describe two types of container adapters: stack and queue.

### Stack

Chapter 17 discussed the data structure stack in detail. Because a stack is an important data structure, the STL provides a class to implement a stack in a program. The name of the class defining a stack is `stack`; the name of the header file containing the definition of the `class` `stack` is `stack`. Table 21-19 defines the various operations supported by the stack container class.

**TABLE 21-19 — Various Operations on a stack Object**

| Operation | Description |
|---|---|
| `size` | Returns the actual number of elements in the stack. |
| `empty` | Returns `true` if the stack is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of `item` onto the stack. |
| `top` | Returns the top element of the stack, but does not remove the element from the stack. This operation is implemented as a value-returning function. |
| `pop` | Removes the top element of the stack. |

In addition to the operations size, empty, push, top, and pop, the stack container class provides relational operators to compare two stacks. For example, the relational operator == can be used to determine whether two stacks are identical.

The program in Example 21-9 illustrates how to use the stack container class.

### Example 21-9

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main()
{
    stack<int> intStack;                         //Line 1

    intStack.push(16);                           //Line 2
    intStack.push(8);                            //Line 3
    intStack.push(20);                           //Line 4
    intStack.push(3);                            //Line 5

    cout << "Line 6: The top element of intStack: "
         << intStack.top() << endl;              //Line 6

    intStack.pop();                              //Line 7

    cout << "Line 8: After the pop operation, "
         << "the top element of intStack: "
         << intStack.top() << endl;              //Line 8

    cout << "Line 9: intStack elements: ";      //Line 9

    while (!intStack.empty())                    //Line 10
    {
        cout << intStack.top() << " ";           //Line 11
        intStack.pop();                          //Line 12
    }

    cout << endl;                                 //Line 13

    return 0;
}
```

**Sample Run:**

```text
Line 6: The top element of intStack: 3
Line 8: After the pop operation, the top element of intStack: 20
Line 9: intStack elements: 20 8 16
```

The preceding output is self-explanatory. The details are left as an exercise for you.

### Queue

Chapter 17 discussed the data structure queue in detail. Because a queue is an important data structure, the STL provides a class to implement queues in a program. The name of the class defining the queue is queue, and the name of the header file containing the definition of the class queue is queue. Table 21-20 defines the various operations supported by the queue container class.

**TABLE 21-20** Various Operations on a queue Object

| Operation | Description |
|---|---|
| `size` | Returns the actual number of elements in the queue. |
| `empty` | Returns `true` if the queue is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of `item` into the queue. |
| `front` | Returns the next item, the first element in the queue, but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `back` | Returns the last element in the queue, but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `pop` | Removes the next element in the queue. |

In addition to the operations size, empty, push, front, back, and pop, the queue container class provides relational operators to compare two queues. For example, the relational operator == can be used to determine whether two queues are identical.

The program in Example 21-10 illustrates how to use the queue container class.

### Example 21-10

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main()
{
    queue<int> intQueue;                    //Line 1

    intQueue.push(26);                      //Line 2
    intQueue.push(18);                      //Line 3
    intQueue.push(50);                      //Line 4
    intQueue.push(33);                      //Line 5

    cout << "Line 6: The front element of intQueue: "
         << intQueue.front() << endl;       //Line 6

    cout << "Line 7: The last element of intQueue: "
         << intQueue.back() << endl;        //Line 7

    intQueue.pop();                         //Line 8

    cout << "Line 9: After the pop operation, "
         << "the front element of intQueue: "
         << intQueue.front() << endl;       //Line 9

    cout << "Line 10: intQueue elements: "; //Line 10
    while (!intQueue.empty())               //Line 11
    {
        cout << intQueue.front() << " ";    //Line 12
        intQueue.pop();                     //Line 13
    }

    cout << endl;                           //Line 14

    return 0;
}
```

**Sample Run:**

```text
Line 6: The front element of intQueue: 26
Line 7: The last element of intQueue: 33
Line 9: After the pop operation, the front element of intQueue: 18
Line 10: intQueue elements: 18 50 33
```

The preceding output is self-explanatory. The details are left as an exercise for you.

## Containers, Associated Header Files, and Iterator Support

The previous sections discussed various types of containers. Recall that every container is a class. The definition of the class implementing a specific container is contained in the header file. Table 21-21 describes the container, its associated header file, and the type of iterator supported by the container.

**TABLE 21-21** Containers, Their Associated Header Files, and the Type of Iterator Supported by Each Container

| Sequence containers | Associated header file | Type of iterator support |
|---|---|---|
| `vector` | `<vector>` | Random access |
| `deque` | `<deque>` | Random access |
| `list` | `<list>` | Bidirectional |
| **Associative containers** | **Associated header file** | **Type of iterator support** |
| `map` | `<map>` | Bidirectional |
| `multimap` | `<map>` | Bidirectional |
| `set` | `<set>` | Bidirectional |
| `multiset` | `<set>` | Bidirectional |
| **Adapters** | **Associated header file** | **Type of iterator support** |
| `stack` | `<stack>` | No iterator support |
| `queue` | `<queue>` | No iterator support |
| `priority_queue` | `<queue>` | No iterator support |

## Algorithms

Several operations can be defined for a container. Some of the operations are very specific to a container and, therefore, are provided as part of the container definition (that is, as member functions of the class implementing the container). However, several operations—such as find, sort, and merge—are common to all containers. These operations are provided as generic algorithms and can be applied to all containers, as well as the built-in array type. The algorithms are bound to a particular container through an iterator pair.

The generic algorithms are contained in the header file `algorithm`. This section describes several of these algorithms and shows how to use them in a program. Because algorithms are implemented with the help of functions, in this section, the terms *function* and *algorithm* mean the same thing.
