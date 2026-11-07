
```cpp
namesMultiSet.insert("Goofy");                         //Line 49
namesMultiSet.insert("Donny");                         //Line 50

cout << "Line 51: namesMultiSet: ";                    //Line 51
copy(namesMultiSet.begin(), namesMultiSet.end(),
     screen);                                          //Line 52
cout << endl;                                          //Line 53

}
return 0;
```

**Sample Run:**

```text
Line 9: intSet: 3 8 16 20
Line 19: intSetA: 238 156 84 59 39 36 30
Line 23: After removing 59, intSetA: 238 156 84 39 36 30
Line 31: After removing the fourth element,
        intSetA: 238 156 84 36 30
Line 35: intSetB: 238 156 84 36 30
Line 39: After removing all the elements,
        intSetB:
Line 51: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

The statement in Line 1 declares `intSet` to be a set container. The statement in Line 2 declares `intSetA` to be a set container whose elements are to be arranged in descending order. The statement in Line 3 declares `intGtIt` to be a set iterator. The iterator `intGtIt` can process the elements of any set container whose elements are of type `int` and are arranged in descending order. The statement in Line 4 declares `screen` to be an ostream iterator that outputs the elements of any container whose elements are of type `int`.

The statements in Lines 5 through 8 insert 16, 8, 20, and 3 into `intSet`, and the statement in Line 10 outputs the elements of `intSet`. In the output, see the line marked Line 9; it contains the output of the statements in Lines 9 through 11.

The statements in Lines 12 through 18 insert 36, 84, 30, 39, 59, 238, and 156 into `intSetA`, and the statement in Line 20 outputs the elements of `intSetA`. In the output, see the line marked Line 19. It contains the output of the statements in Lines 19 through 21. Notice that the elements of `intSetA` appear in descending order.

The statement in Line 22 removes 59 from `intSetA`. After the statement in Line 26 executes, `intGtIt` points to the first element of `intSetA`. The statement in Line 27 advances `intGtIt` to the next element of `intSetA`. After the statement in Line 29 executes, `intGtIt` points to the fourth element of `intSetA`. The statement in Line 30 removes the element of `intSetA` pointed to by `intGtIt`. The meanings of the statements in Lines 34 through 41 are similar.

The statement in Line 42 declares `namesMultiSet` to be a container of type `multiset`. The elements in `namesMultiSet` are of type `string` and are arranged in descending order. The statement in Line 43 declares `iter` to be a `multiset` iterator.

The statements in Lines 45 through 50 insert Donny, Zippy, Goofy, Hungry, Goofy, and Donny into `namesMultiSet`. The statement in Line 52 outputs the elements of `namesMultiSet`.

## Container Adapters

The previous sections discussed several types of containers. In addition to the containers that work in a general framework, the STL provides containers to accommodate special situations. These containers, called **container adapters**, are adapted standard STL containers to work in a specific environment. The three container adapters are:

- Stacks
- Queues
- Priority queues

Container adapters do not support any type of iterator. That is, iterators cannot be used with these types of containers. The next two sections describe two types of container adapters: stack and queue.

### Stack

Chapter 18 discussed the data structure stack in detail. Because a stack is an important data structure, the STL provides a class to implement a stack in a program. The name of the class defining a stack is `stack`; the name of the header file containing the definition of the class `stack` is `stack`. Table 22-19 defines the various operations supported by the `stack` container class.

**Table 22-19** Various Operations on a `stack` Object

| Operation | Description |
|---|---|
| `size` | Returns the actual number of elements in the stack. |
| `empty` | Returns `true` if the stack is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of item onto the stack. |
| `top` | Returns the top element of the stack but does not remove the element from the stack. This operation is implemented as a value-returning function. |
| `pop` | Removes the top element of the stack. |

In addition to the operations `size`, `empty`, `push`, `top`, and `pop`, the `stack` container class provides relational operators to compare two stacks. For example, the relational operator `==` can be used to determine whether two stacks are identical.

The program in Example 22-9 illustrates how to use the `stack` container class.

**Example 22-9**

```cpp
#include <iostream>
#include <stack>

using namespace std;

int main()
{
    stack<int> intStack;                          //Line 1

    intStack.push(16);                            //Line 2
    intStack.push(8);                             //Line 3
    intStack.push(20);                            //Line 4
    intStack.push(3);                             //Line 5

    cout << "Line 6: The top element of intStack: "
         << intStack.top() << endl;               //Line 6

    intStack.pop();                               //Line 7

    cout << "Line 8: After the pop operation, "
         << "the top element of intStack: "
         << intStack.top() << endl;               //Line 8

    cout << "Line 9: intStack elements: ";        //Line 9

    while (!intStack.empty())                     //Line 10
    {
        cout << intStack.top() << " ";            //Line 11
        intStack.pop();                            //Line 12
    }

    cout << endl;                                  //Line 13

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

Chapter 18 discussed the data structure queue in detail. Because a queue is an important data structure, the STL provides a class to implement queues in a program. The name of the class defining the queue is `queue`, and the name of the header file containing the definition of the class `queue` is `queue`. Table 22-20 defines the various operations supported by the `queue` container class.

**Table 22-20** Various Operations on a `queue` Object

| Operation | Description |
|---|---|
| `size` | Returns the actual number of elements in the queue. |
| `empty` | Returns `true` if the queue is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of item into the queue. |
| `front` | Returns the next—that is, first—element in the queue, but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `back` | Returns the last element in the queue but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `pop` | Removes the next element in the queue. |

In addition to the operations `size`, `empty`, `push`, `front`, `back`, and `pop`, the `queue` container class provides relational operators to compare two queues. For example, the relational operator `==` can be used to determine whether two queues are identical.

The program in Example 22-10 illustrates how to use the `queue` container class.

**Example 22-10**

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main()
{
    queue<int> intQueue;                         //Line 1

    intQueue.push(26);                           //Line 2
    intQueue.push(18);                           //Line 3
    intQueue.push(50);                                      //Line 4
    intQueue.push(33);                                      //Line 5

    cout << "Line 6: The front element of intQueue: "
         << intQueue.front() << endl;                       //Line 6

    cout << "Line 7: The last element of intQueue: "
         << intQueue.back() << endl;                        //Line 7

    intQueue.pop();                                         //Line 8

    cout << "Line 9: After the pop operation, "
         << "the front element of intQueue: "
         << intQueue.front() << endl;                       //Line 9

    cout << "Line 10: intQueue elements: ";                //Line 10

    while (!intQueue.empty())                               //Line 11
    {
        cout << intQueue.front() << " ";                   //Line 12
        intQueue.pop();                                     //Line 13
    }

    cout << endl;                                           //Line 14

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

The previous sections discussed various types of containers. Recall that every container is a class. The definition of the class implementing a specific container is contained in the header file. Table 22-21 describes the container, its associated header file, and the type of iterator supported by the container.
