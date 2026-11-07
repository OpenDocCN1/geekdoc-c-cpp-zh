
### Program 19.4 Using a ragged vector to create a Pascal triangle (Continued)

```cpp
{
    cout << setw(4) << pascal[i][j] << " ";
}
cout << endl;
}
return 0;
}
```

Run:
```text
Coefficients of (x + y)^0 ======>    1
Coefficients of (x + y)^1 ======>    1    1
Coefficients of (x + y)^2 ======>    1    2    1
Coefficients of (x + y)^3 ======>    1    3    3    1
Coefficients of (x + y)^4 ======>    1    4    6    4    1
Coefficients of (x + y)^5 ======>    1    5    10   10   5    1
```

Note that in the constructor, we define the number of rows (power + 1), but the size of the columns is set to zero. The column in each row grows as we insert new elements using the *push_back()* operation. The values are set to 0 during insertion (line 19), but they change in the inner *for* loop (lines 25 to 35).

## 19.3.3 The deque Class

The *deque* class, defined in the `<deque>` header file, is a sequence container similar to a *vector* but with two open ends. The name deque (pronounced deck) is short for *double-ended queue*. This means that we can insert and erase at both ends of a deque. Figure 19.8 shows a deque of *n* elements.

The operations for inserting and erasing elements from both ends are fast. However, the extra capability to insert at the beginning makes a deque less efficient than a vector because doing so requires that the system allocate extra memory to extend the deque at either end. This means if we need a structure that does not need insertion and erasure in the front, it is more efficient to use a vector than a deque. Insertion and erasure in the middle of a deque have the same inefficiencies as in the case of a vector.

### Operations

The syntax of member functions for the *deque* class can be obtained from the general public interface (Table 19.2). Its functions are very similar to the ones for the vector class with some minor differences. We list only the differences.

**Operations Added for deque** The *deque* class uses the same set of operations as the vector but uses two additional operations.

![](img/d68f6199646ca63591a6d8419e0ed4ba_884_0.png)

**Figure 19.8**   A deque as a sequence container

```cpp
deq.push_front(value);              // Insert value at the front
deq.pop_front();                    // Delete value at the front
```

**Operations missing in deque** As the public interface (Table 19.2) shows, the *capacity()* and *reserve()* member functions are missing in the *deque* class. The reason is the implementation. Since a *deque* can grow or shrink from both ends, the standard normally implements the *deque* as a set of blocks in heap memory.

### Application

The *deque* class was designed to be the foundation for the *queue adapter* class that we discuss later. However, it can be used in any application that needs insertion and deletion at both ends. One application that normally uses a *deque* is *rotation*, in which we have a list of data items we want to rotate *n* times. Clockwise rotation requires that we remove an element from the back and insert it at the front; counterclockwise rotation requires that we remove an element from the front and insert it at the back.

### Program 19.5 Using deque to rotate a list to the left and right

```cpp
/*********************************************************
 * A program to demonstrate rotation                    *
 *********************************************************/
#include <deque>
#include <string>
#include <iostream>
#include <iomanip>
using namespace std;

// Global print function
void print(deque<string> deq)
{
   for (int i = 0; i < deq.size(); i++)
   {
      cout << deq.at(i) << " ";
   }
   cout << endl;
}

int main()
{
   // Create a deque of five strings and print it
   deque<string> deq(5);
   string arr[5] = {"John", "Mary", "Rich", "Mark", "Tara"};
   for (int i = 0; i < 5; i++)
   {
27     deq[i] = arr[i];
28 }
29 print(deq);
30 // Rotate the deque clockwise one element
31 deq.push_back(deq.front());
32 deq.pop_front();
33 print(deq);
34 // Rotate the deque counter-clockwise one element
35 deq.push_front(deq.back());
36 deq.pop_back();
37 print(deq);
38 return 0;
39 }
```

Run:
```text
John  Mary  Rich  Mark  Tara
Mary  Rich  Mark  Tara  John
John  Mary  Rich  Mark  Tara
```

In lines 23 to 29, we create a deque of five strings. In lines 31 to 33, we copy the front element and push it at the back and then delete it. In lines 35 to 37, we copy the back element and push it at the front and then delete it.

## 19.3.4 The list Class

The `list` class, defined in the `<list>` header file, is a sequence container with fast insertion and deletion at any point. This means that we can insert or delete easily at any point in a `list`. On the other hand, a `list` does not support random access for retrieving or changing the value of an element using the index operator or the `at()` member function because the `list` is implemented as a doubly linked list, not an array in the heap. If we want to access the list randomly, we must use an iterator that moves to the desired element and then accesses it. Figure 19.9 shows a list made of five elements. The figure shows that each node has a data section and two pointers, one pointing to the previous node and the other pointing to the next node.

![](img/d68f6199646ca63591a6d8419e0ed4ba_886_0.png)

### Operations

The syntax of member functions for the `list` class can be obtained from the general public interface (Table 19.2). These member functions are similar to the ones for the `vector` class and `deque` class with some differences. We discuss only the differences.

**Iterators** The `list` class supports only bidirectional iterators (not random-access iterators). This means that the list elements cannot be accessed using the index operator or the `at()` member function because it requires the operators `+` and `−` defined for random-access iterators.

**Capacity and Reserve** The `capacity()` and `reserve()` member functions do not exist in the `list` class because the system adds an element at the front, at the back, and in the middle using pointers in the doubly linked list.

**Accessing Elements** The operator `[]` and the `at()` function are not supported for the `list` class because the `list` class does not support the random-access operator (only bidirectional). We must explicitly use an iterator to access elements.

**Erasure** The `list` class provides three new operations to erase an element or elements from the list as the public interface shows. The following shows how we call these operations.

```cpp
remove(value);              // Erases all occurrences of value
remove_if(predicate);       // Erases all occurrences for which parameter is true
unique(predicate);          // Erases adjacent duplicates if parameter is true
```

**Splice, Merge, and Sort** The `list` class defines three other operations: `splice()`, `merge()`, and `sort()` as defined in the public interface.

```cpp
splice(pos, first, last);   // Inserts elements [first, last) from another list before pos
merge(other);               // Merges two sorted lists to a new sorted list
sort();                     // Sorts the list
```

Figure 19.10 shows the idea behind splicing. The iterator *firstIter* defines the insertion position in the first list; the iterators *secondIter1* and *secondIter2* define the range to be moved in the second list.

![](img/d68f6199646ca63591a6d8419e0ed4ba_887_0.png)

### Application

Since the *list* class can easily grow or shrink from both ends, it has many applications. We give some examples next.

As a simple example, we create a list of five integers input by the user. We then print the list in the forward and reverse directions. Program 19.6 shows the code.

### Program 19.6 Printing list elements

```cpp
/********************************************************************
 * The program that creates a list of five integers and prints     *
 * in both forward and reverse direction                           *
 ********************************************************************/
#include <list>
#include <iostream>
using namespace std;

int main()
{
    // Instantiation of a list object and declaration of a variable
    list<int> lst;
    int value;
    // Inputting five integers and store them in the list
    for (int i = 0; i < 5; i++)
    {
        cout << "Enter an integer: ";
        cin >> value;
        lst.push_back(value);
    }
    // Printing the list in forward direction
    cout << "Print the list in forward direction." << endl;
    list<int>::iterator iter1;
    for (iter1 = lst.begin(); iter1 != lst.end(); iter1++)
    {
        cout << *iter1 << " ";
    }
    cout << endl;
    // Printing the list in backward direction
    cout << "Print the list in reverse direction." << endl;
    list<int>::reverse_iterator iter2;
    for (iter2 = lst.rbegin(); iter2 != lst.rend(); iter2++)
    {
        cout << *iter2 << " ";
    }
    return 0;
}
```
