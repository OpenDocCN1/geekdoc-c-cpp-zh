
## Table 13.4 Summary of deque Class Methods and Operations

| Methods and Operations | Type | Description |
|---|---|---|
| `deque<DataType> name` | constructor | Creates an empty deque named `name` with a compiler-dependent initial size |
| `deque<DataType> name(source)` | constructor | Creates a copy of the source deque |
| `deque<DataType> name(n)` | constructor | Creates a deque of size n |
| `deque<DataType> name(n, object)` | constructor | Creates a deque of size n with each object initialized as `object` |
| `deque<DataType> name(src.beg, src.end)` | constructor | Creates a deque initialized with objects from a source container beginning at `src.beg` and ending at `src.end` |
| `~deque<DataType>()` | destructor | Destroys the deque and all objects it contains |
| `name.at(index)` | accessor | Returns the object at `index` and throws an exception if the index is out of bounds |
| `name.front()` | accessor | Returns the first object at the front of the deque with no check for the existence of a first object |
| `name.pop_front()` | mutator | Removes but does not return the first object at the front of the deque |
| `name.push_front(object)` | mutator | Inserts `object` at the front of the deque |
| `name.back()` | accessor | Returns the object at the back of the deque with no check for the existence of a last object |
| `name.pop_back()` | mutator | Removes but does not return the last object at the back of the deque |
| `name.push_back(object)` | mutator | Inserts `object` at the back of the deque |
| `name.insert(itr, object)` | mutator | Inserts `object` at iterator position `itr` |
| `name.insert(itr, src.beg, src.end)` | mutator | Inserts objects from a source container between `src.beg` and `src.end` at iterator position `itr` |
| `name.insert(itr, n, object)` | mutator | Inserts *n* copies of `object` at iterator position `itr` |
| `name2.assign(n, object)` | mutator | Assigns *n* copies of `object` |
| `name2.assign(src.begin, src.end)` | mutator | Assigns objects of the `src` container (need not be a deque) between the range `src.begin` and `src.end` to `name2` |
| `name.erase(pos)` | mutator | Removes the object at the specified position `pos` |
| `name.erase(begin, end)` | mutator | Removes objects within the specified range |
| `name.resize(value)` | mutator | Resizes the deque larger with new objects instantiated by using the default constructor |
| `name.resize(value, object)` | mutator | Resizes the deque larger with new objects instantiated as `object` |
| `name.clear()` | mutator | Removes all objects from the deque |
| `name.swap(nameB)` | mutator | Swaps objects of `name` and `nameB` deques; can be performed by using the `swap()` algorithm |
| `name.begin()` | accessor | Returns an iterator to the first object in the deque |
| `name.end()` | accessor | Returns an iterator to the position after the last object in the deque |
| `name.rbegin()` | accessor | Returns a reverse iterator to the first object in the deque |
| `name.rend()` | accessor | Returns a reverse iterator to the position after the last object in the deque |
| `nameA == nameB` | relational | Returns a Boolean true if all `nameA` objects equal `nameB` objects; otherwise, returns false |

## Point of Information

### Stacking the Deque

Stacks and queues are two special forms of a more general data object called a **deque** (stands for "double-ended queue" and is pronounced "deck"). In a deque object, data can be handled in one of four ways:

1. Insert at the beginning and remove from the beginning, which is a last-in, first-out (LIFO) stack.
2. Insert at the beginning and remove from the end, which is a first-in, first-out (FIFO) queue.
3. Insert at the end and remove from the end, which represents an inverted LIFO technique.
4. Insert at the end and remove from the beginning, which represents an inverted FIFO queue.

Implementation 1 (a stack object) is discussed in this section, and implementation 2 (a queue object) is covered in the next section. Implementations 3 and 4 are sometimes used for keeping track of memory addresses, as when programming is done in machine language or when objects are handled in a file. When a high-level language, such as C++, manages the data area automatically, users might not be aware of where data is being stored or which type of deque is being applied.

![](img/202cface8244f523c2641baa2e00d7dd_615_0.png)

### Program 13.3

```cpp
#include <iostream>
#include <deque>
#include <string>
#include <cctype>
using namespace std;

int main()
{
    string name;
    deque<string> stack;

    cout << "Enter as many names as you want, one per line" << endl;
    cout << "To stop enter a single x" << endl;
    while(true)
    {
        cout << "Enter a name (or x to stop): ";
        getline(cin, name);
        if (tolower(name.at(0)) == 'x') break;
        stack.push_front(name);
    }

    cout << "\nThe names in the stack are:\n";

    // pop names from the stack
    while(!stack.empty())
    {
        name = stack.front();  // retrieve the name
        stack.pop_front();     // pop name from the stack
        cout << name << endl;
    }
    return 0;
}
```

Following is a sample run of Program 13.3:

```text
Enter as many names as you want, one per line
    To stop enter a single x
Enter a name (or x to stop): Jane Jones
Enter a name (or x to stop): Bill Smith
Enter a name (or x to stop): Jim Robinson
Enter a name (or x to stop): x

The names in the stack are:
Jim Robinson
Bill Smith
Jane Jones
```

## EXERCISES 13.3

1. **(Review)** State whether a stack is appropriate for each of the following tasks, and indicate why or why not:
   a. A word-processing program must remember a line of up to 80 characters. Pressing the Backspace key deletes the previous character, and pressing Ctrl+Backspace deletes the entire line. Users must be able to undo deletion operations.
   b. Customers must wait one to three months for delivery of their new cars. The dealer creates a list to determine the "fair" order in which customers should get their cars; the list is prepared in the order in which customers placed their requests for a new car.
   c. You're required to search downward in a pile of magazines to locate the issue for last January. Each magazine was placed on the pile as soon as it was received.
   d. A programming team accepts jobs and prioritizes them on the basis of urgency.
   e. A line forms at a bus stop.

2. **(Practice)** Enter and run Program 13.3.

3. **(Modify)** Modify Program 13.3 to implement a stack of integers rather than a stack of strings.

4. **(Modify)** Modify Program 13.3 to instantiate three stacks of digits named `digits1`, `digits2`, and `digits3`. Initialize `digits1` to contain the digits 9, 8, 5, and 2, which is the number 2589 in reverse order. Similarly, the `digits2` stack should be initialized to contain the digits 3, 1, 5, and 7, which is the number 7513 in reverse order. Calculate and place the sum of these two numbers in the `digits3` stack. This sum should be obtained by popping objects from `digits1` and `digits2` and adding them together with a variable named `carry`, which is initialized to 0. If the sum of the two popped objects and `carry` doesn't exceed 10, the sum should be pushed onto `digits3` and `carry` should be set to 0; otherwise, `carry` should be set to 1, and the units digit of the sum should be pushed onto the `digits3` stack.

5. **(Program)** Write a C++ program that allows a user to enter a maximum of 100 integers in a stack object. Then have the program do the following:
   a. Reverse the stack's contents into a second stack of integers.
   b. Using two additional stacks, reverse the contents in the original stack. For example, if the original stack contains the integers 1, 2, 3, and 4, it should contain the integers 4, 3, 2, and 1 at the end of the program.

6. **(Program)** Write a C++ program that allows a user to enter a maximum of 50 characters in a stack object. Then have the program sort the stack contents in increasing order. For example, if the stack's contents are initially D, E, A, and B, its final contents are A, B, D, and E.

## 13.4 Queues

A queue (pronounced "cue") is a list in which items are added to one end of the list, called the top, and removed from the other end of the list, called the bottom. This arrangement ensures that items are removed from the list in the exact order in which they were entered. This means the first item placed on the list is the first item to be removed, the second item placed on the list is the second item to be removed, and so on. Therefore, a queue is a first-in, first-out (FIFO) list—a list in which the first item added to the list is the first item that can be removed.

As an example of a queue, think of a list of people waiting to purchase season tickets to a professional football team. The first person on the list should be called when the first set of tickets becomes available, the second person should be called for the second available set, and so on. Figure 13.8 shows the names of people currently on the list.

![](img/202cface8244f523c2641baa2e00d7dd_617_0.png)

Figure 13.8 A queue with its pointers

The names have been added to the list in the same fashion as on a stack: As new names are added to the list, they're stacked on top of existing names. The difference in a queue relates to how the names are popped off the list. Clearly, the people on this list expect to be serviced in the order they were placed on the list—that is, first in, first out. Therefore, unlike a stack, the name added to the list most recently is not the first name removed. Rather, the oldest name still on the list is always the first name removed.
