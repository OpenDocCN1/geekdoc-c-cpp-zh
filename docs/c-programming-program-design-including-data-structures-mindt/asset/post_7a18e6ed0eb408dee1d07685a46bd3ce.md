
```cpp
namesMultiSet.insert("Goofy");                         //Line 58
namesMultiSet.insert("Donny");                         //Line 59

cout << "Line 60: namesMultiSet: ";                    //Line 60
copy(namesMultiSet.begin(), namesMultiSet.end(),        //Line 61
     pScreen);
cout << endl;                                             //Line 62

return 0;                                                //Line 63
}                                                        //Line 64
```

### Sample Run

```text
Line 18: intSet: 3 8 16 20
Line 28: intSetA: 238 156 84 59 39 36 30
Line 32: After removing 59, intSetA: 238 156 84 39 36 30
Line 40: After removing the fourth element,
         intSetA: 238 156 84 36 30
Line 44: intSetB: 238 156 84 36 30
Line 48: After removing all elements,
         intSetB:
Line 60: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

The statement in Line 10 declares intSet to be a set container. The statement in Line 11 declares intSetA to be a set container whose elements are to be arranged in descending order. The statement in Line 12 declares intGtIt to be a set iterator. The iterator intGtIt can process the elements of any set container whose elements are of type int and are arranged in descending order. The statement in Line 13 declares screen to be an ostream iterator that outputs the elements of any container whose elements are of type int.

The statements in Lines 14 through 17 insert 16, 8, 20, and 3 into intSet, and the statement in Line 19 outputs the elements of intSet. In the output, see the line marked Line 18; it contains the output of the statements in Lines 18 through 20.

The statements in Lines 21 through 27 insert 36, 84, 30, 39, 59, 238, and 156 into intSetA, and the statement in Line 29 outputs the elements of intSetA. In the output, see the line marked Line 28. It contains the output of the statements in Lines 28 through 30. Notice that the elements of intSetA appear in descending order.

The statement in Line 31 removes 59 from intSetA. After the statement in Line 35 executes, intGtIt points to the first element of intSetA. The statement in Line 36 advances intGtIt to the next element of intSetA. After the statement in Line 38 executes, intGtIt points to the fourth element of intSetA. The statement in Line 39 removes the element of intSetA pointed to by intGtIt. The meanings of the statements in Lines 43 through 50 are similar.

The statement in Line 51 declares namesMultiSet to be a container of type multiset. The elements in namesMultiSet are of type string and are arranged in descending order. The statement in Line 52 declares iterator to be a multiset iterator. The statements in Lines 54 through 59 insert Donny, Zippy, Goofy, Hungry, Goofy, and Donny into `namesMultiSet`. The statement in Line 61 outputs the elements of `namesMultiSet`.

You can initialize a set or multiset object during declaration. See modified `STL_Example21-9_setAndMultisetModified.cpp`.

## Container Adapters

The previous sections discussed several types of containers. In addition to the containers that work in a general framework, the STL provides containers to accommodate special situations. These containers, called **container adapters**, are standard STL containers adapted to work in a specific environment. The three container adapters are as follows:

- Stacks
- Queues
- Priority queues

Container adapters do not support any type of iterator. That is, iterators cannot be used with these types of containers. The next two sections describe two types of container adapters: stack and queue.

### Stack

Chapter 17 discussed the data structure stack in detail. Because a stack is an important data structure, the STL provides a class template to implement a stack in a program. The name of the class defining a stack is `stack`; the name of the header file containing the definition of the class `stack` is `stack`. Table 21-19 defines the various operations supported by the stack container class.

**TABLE 21-19** Various Operations on a stack Object

| Operation | Description |
| --- | --- |
| `size` | Returns the actual number of elements in the stack. |
| `empty` | Returns `true` if the stack is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of `item` onto the stack. |
| `top` | Returns the top element of the stack, but does not remove the element from the stack. This operation is implemented as a value-returning function. |
| `pop` | Removes the top element of the stack. |

In addition to the operations **size**, **empty**, **push**, **top**, and **pop**, the stack container class provides relational operators to compare two stacks. For example, the relational operator `==` can be used to determine whether two stacks are identical.

The program in Example 21-10 illustrates how to use the stack container class.

### EXAMPLE 21-10

```cpp
#include <iostream>                              //Line 1
#include <stack>                                  //Line 2

using namespace std;                              //Line 3

int main()                                        //Line 4
{
    stack<int> intStack;                          //Line 6

    intStack.push(16);                            //Line 7
    intStack.push(8);                             //Line 8
    intStack.push(20);                            //Line 9
    intStack.push(3);                             //Line 10

    cout << "Line 11: The top element of intStack: "
         << intStack.top() << endl;              //Line 11

    intStack.pop();                               //Line 12

    cout << "Line 13: After the pop operation, "
         << "the top element of intStack: "
         << intStack.top() << endl;              //Line 13

    cout << "Line 14: intStack elements: ";      //Line 14

    while (!intStack.empty())                     //Line 15
    {
        cout << intStack.top() << " ";            //Line 17
        intStack.pop();                           //Line 18
    }                                             //Line 19

    cout << endl;                                 //Line 20

    return 0;                                     //Line 21
}                                                //Line 22
```

### Sample Run

```text
Line 11: The top element of intStack: 3
Line 13: After the pop operation, the top element of intStack: 20
Line 14: intStack elements: 20 8 16
```

The preceding output is self-explanatory. The details are left as an exercise for you.

### Queue

Chapter 17 discussed the data structure queue in detail. Because a queue is an important data structure, the STL provides a class to implement queues in a program. The name of the class defining the queue is `queue`, and the name of the header file containing the definition of the class `queue` is `queue`. Table 21-20 defines the various operations supported by the queue container class.

**TABLE 21-20** Various Operations on a `queue` Object

| Operation | Description |
| --- | --- |
| `size` | Returns the actual number of elements in the queue. |
| `empty` | Returns `true` if the queue is empty, `false` otherwise. |
| `push(item)` | Inserts a copy of `item` into the queue. |
| `front` | Returns the next—that is, first—element in the queue, but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `back` | Returns the last element in the queue, but does not remove the element from the queue. This operation is implemented as a value-returning function. |
| `pop` | Removes the next element in the queue. |

In addition to the operations `size`, `empty`, `push`, `front`, `back`, and `pop`, the queue container class provides relational operators to compare two queues. For example, the relational operator `==` can be used to determine whether two queues are identical. The program in Example 21-11 illustrates how to use the queue container class.

### EXAMPLE 21-11

```cpp
#include <iostream>               //Line 1
#include <queue>                  //Line 2

using namespace std;              //Line 3

int main()                        //Line 4
{                                 //Line 5
    queue<int> intQueue;          //Line 6

    intQueue.push(26);            //Line 7
    intQueue.push(18);            //Line 8
```
