
144 Chap. 4. Lists, Stacks, and Queues

```cpp
// Dictionary implemented with a sorted array-based list
template <typename Key, typename E>
class SALdict : public Dictionary<Key, E> {
private:
    SAList<Key, E*> list;
public:
    SALdict(int size=defaultSize) // Constructor
    { list = new SAList<Key, E>(size); }
    ~SALdict() { delete list; } // Destructor
    void clear() { list->clear(); } // Reinitialize
}
```

```cpp
// Insert an element: Keep elements sorted
void insert(const Key& k, const E& e) {
    KVpair<Key, E> temp(k, e);
    list->insert(temp);
}
```

```cpp
// Use sequential search to find the element to remove
E remove(const Key& k) {
    E* temp = find(k);
    if (temp != NULL) list->remove();
    return temp;
}
```

```cpp
removeAny() { // Remove the last element
    Assert(size() != 0, "Dictionary is empty");
    list->moveToToEnd(pos1);
    list->prev(pos1);
    KVpair<Key, E> e = list->remove();
    return e.value();
}
```

```cpp
// Find using binary search
E find(const Key& k) const {
    int l = 1;
    int r = list->length();
    while (l+1 <= r) { // Stop when l and r meet
        int i = (l+r)/2; // Check middle of remaining subarray
        list->moveToPos(i);
        KVpair<Key, E> temp = list->getValue();
        if (k < temp.key()) r = i; // In left
        if (k == temp.key()) return temp.value(); // Found it
        if (k > temp.key()) l = i; // In right
    }
    return NULL; // "k" does not appear in dictionary
}
```

Figure 4.34 Dictionary implementation using a sorted array-based list.

Sec. 4.5 Further Reading

```cpp
int size() { // Return list size
{ return list->length(); }
};
```

Figure 4.34 (continued)

for the comparator class to extract the key from the record type, as an alternative to
storing key-value pairs here is an example of the required class for comparing integers.

```cpp
class intCompare { // Comparator class for integer keys
public:
    static bool lt(int x, int y) { return x < y; }
    static bool eq(int x, int y) { return x == y; }
    static bool gt(int x, int y) { return x > y; }
};
```

intCompare provides methods for determining if int variables
are equal (eq), or if the first is less than the second (lt), or greater than the second
(gt).
Here is a class for comparing C-style character strings. It makes use of the
standard library function strcmp // Compare two character strings

```cpp
class CCmpare {
public:
    static bool lt(char* x, char* y) {
        return strcmp(x, y) < 0; }
    static bool eq(char* x, char* y) {
        return strcmp(x, y) == 0; }
    static bool gt(char* x, char* y) {
        return strcmp(x, y) > 0; }
};
```

We use a comparator in Section 5.5 to implement comparison in heaps, and
in Chapter 7 to implement comparison in sorting algorithms.

# 4.5 Further Reading

For more discussion on choice functions used to define the List ADT, see the
work of the Reuse Software Research Group from Ohio State. Their definition
for the List ADT can be found in [SWH93]. More information about designing
classes can be found in [SWH94].

# 4.6 Exercises

4.1 Assume a list has the following configuration:

| 2, 23, 15, 5, 9 |

146 Chap. 4 Lists, Stacks, and Queues

Write a series of C++ statements using the List ADT of Figure 4.1 to delete the element with value 15.

4.2 Show the list configuration resulting from each series of list operations using the List ADT of Figure 4.1. Assume that lists L1 and L2 are empty at the beginning of each series. Show where the current position is in the list.

```
a) L1.append(10);
L1.append(20);
L1.append(15);
```

```
b) L2.append(10);
L2.append(20);
L2.append(15);
L2.moveToStart();
L2.insert(39);
L2.next();
L2.insert(12);
```

4.3 Write a series of C++ statements that uses the List ADT of Figure 4.1 to create a list of holding twenty elements and which actually stores the list with the following configuration:

> { 2, 23 | 15, 5, 9 }

4.4 Using the List ADT of Figure 4.1, write a function to interchange the current element and the one following it.

4.5 In the linked list implementation presented in Section 4.1.2, the current position is implemented using a pointer to the element ahead of the logical node. The more “natural” approach might seem to be curr point directly to the node containing the current element. However, if this was done, the pointer of the node preceding the current one cannot be updated properly because there is no access to this node from curr. An alternative is to add a new node after the current element, copy the value of the current element to this new node, and then insert the new value into the current node.

- What happens if curr is at the end of the list already? Is there still a way to make this work? The resulting code simpler or more complex the implementation of Section 4.1.2?

- Will deletion always work in constant time if curr points directly to the current node? In particular, can you make several deletions in a row?

4.6 Add to the LList class implementation a member function to reverse the order of the elements on the list. Your algorithm should run in Θ(n) time for a list of n elements.

4.7 Write a function to merge two linked lists. The input lists have their elements in sorted order, from lowest to highest. The output list should also be sorted from lowest to highest. Your algorithm should run in linear time on the length of the output list.

4.8 A circular linked list is one in which the next field for the last link node of the list points to the first link node of the list. This can be useful when you wish to have relative positioning for elements, but no concept of an absolute first or last.

- (a) Modify the code of Figure 4.8 to implement circular singly linked lists.
- (b) Modify the code of Figure 4.14 to implement circular doubly linked lists.

4.9 Section 4.1.3 states "the space required by the array-based list implementation is Ω(n), but can be greater." Explain why this is

4.10 Section 4.1.3 presents an equation for determining the break-even point for the space requirements of two implementations of lists. The variables are D, E, P, and n. What are the dimensional units for each variable? Show that both sides of the equation balance in terms of their dimensional units.

4.11 Use the space equation of Section 4.1 to determine the break-even point for an array-based and linked list implementation for lists when the sizes for the data field, a pointer, and the array-based list's array are specified. State when the linked list needs less space than the array.

- (a) The data field is eight bytes, a pointer is four bytes, and the array holds twenty elements.
- (b) The data field is two bytes, a pointer is four bytes, and the array holds thirty elements.
- (c) The data field is one byte, a pointer is four bytes, and the array holds thirty elements.
- (d) The data field is 32 bytes, a pointer is four bytes, and the array holds forty elements.

4.12 Determine the size of an int variable, a double variable, and a pointer on your computer. The C++ operator sizeof might be useful if you do not already know the answer.

- (a) Calculate the break-even point, as a function of n, beyond which the array-based list is more efficient than the linked list for lists whose elements are of int.
- (b) Calculate the break-even point, as a function of n, beyond which the array-based list is more efficient than the linked list for lists whose elements are of double.

166

4.13 Modify the code of Figure 4.18 to implement two stacks sharing the same array, as shown in Figure 4.20.

4.14 Modify the array-based queue definition of Figure 4.26 to use a separate Boolean variable to keep track of whether the queue is empty, rather than require that one array position remain empty.

4.15 A palindrome is a string that reads same forwards as backwards. Using only a fixed number of stacks and queues, the stack and queue ADT functions, and a fixed number of int and char variables, write an algorithm to determine if a string is a palindrome. Assume that the string is read from standard input one character at a time. The algorithm should output true or false as appropriate.

4.16 Re-implement fibr from Exercise 2.11, using a stack to replace the recursive call as described in Section 4.2.4.

4.17 Write a recursive algorithm to compute the value of the recurrence relation

```
T(n) = T[n/2] + T[n/2] + n;  T(1) = 1.
```

Then, write your algorithm to simulate the recursive calls with a stack.

4.18 Let Q be a non-empty queue, and let S be an empty stack. Using only the stack and queue ADT functions a element variable X, write an algorithm to reverse the order of elements in Q.

4.19 A common problem for compilers and text editors is to determine if the parentheses (or other brackets) are balanced and properly nested. For example, the string "((())" contains properly nested pairs of parentheses, but the string "()()" does not, and the string "()" does not.

- (a) Give an algorithm that returns true if a string contains properly nested and balanced parentheses, and false otherwise. Use a stack to keep track of the number of left parentheses seen so far. Hint: At time while scanning a legal string from left to right you will have more right parentheses than left.
- (b) Give an algorithm that returns the position in the string of the first offending parenthesis if the string is not properly nested and balanced. If there is an excess right parenthesis found, return its position; if there are too many left parentheses, return the position of the first excess left parenthesis. Return -1 if the string is properly balanced and nested. Use a stack to keep track of the number and positions of left parentheses seen so far.

4.20 Imagine that you are designing an application where you need to perform the operations Insert, Delete Maximum, and Delete Minimum. For this application, the cost of inserting is not important, because it can be done
