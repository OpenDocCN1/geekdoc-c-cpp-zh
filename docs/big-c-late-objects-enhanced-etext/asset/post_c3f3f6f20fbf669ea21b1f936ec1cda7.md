
### E14.22
Add a member function first_to_last to the implementation of a queue in Section 14.5.3. The member function moves the element at the head of the queue to the tail of the queue. The element that was second in line will now be at the head.

### E14.23
Add a member function last_to_first to the implementation of a queue in Section 14.5.3. The member function moves the element at the tail of the queue to the head.

### E14.24
Add a member function first_to_last, as described in Exercise E14.22, to the circular array implementation of a queue in Section 14.5.4.

### E14.25
Add a member function last_to_first, as described in Exercise E14.23, to the circular array implementation of a queue in Section 14.5.4.

### E14.26
Write a function that removes all strings of a given length from a linked list and returns them in another linked list.

### E14.27
Implement the following operator function that prints the contents of a list of strings, separated by commas and enclosed in braces.

```cpp
ostream& operator<<(ostream& out, const list<string>& lst)
```

### E14.28
Implement an operator>> function that can read a list<string> that was produced by the output operator of Exercise E14.27.

### E14.29
Implement the operators of Exercise E14.27 and Exercise E14.28 so that they can be applied to a list<T>.

### E14.30
Change the increment and decrement operators of the iterator in Worked Example 14.1 so that they return the appropriate value (that is, the iterator before the move or a reference to the iterator after the move).

### E14.31
The * operator of the iterator in Worked Example 14.1 is not as useful as the one in the standard list class. You cannot use it to modify a list, by calling

```cpp
*iter = . . . ;
```

Rectify this by providing two iterators: a ConstIterator whose * operator returns a const T&, and an Iterator whose * operator returns a T&. You now need two begin member functions:

```cpp
List<T>::Iterator List<T>::begin()
List<T>::ConstIterator List<T>::begin() const
```

When calling begin() on a const List<T> (or more likely, a const List<T>&), the second member function is called. Provide a program that demonstrates that fact. Also provide two versions for the end member function.

## PROGRAMMING PROJECTS

### P14.1
Turn the linked list implementation into a circular list: Have the previous pointer of the first node point to the last node, and the next pointer of the last node point to the first node. Then remove the last pointer in the List class because the value can now be obtained as first->previous. Reimplement the member functions so that they have the same effect as before.

### P14.2
Turn the linked list implementation into a singly-linked list: Drop the previous pointer of the nodes and the previous member function of the iterator. Reimplement the other member functions so that they have the same effect as before. Hint: In order to remove an element in constant time, iterators should store the predecessor of the current node.

### ■■ P14.3
Modify the linked list implementation to use a dummy node for the past-the-end position whose data member is unused. A past-the-end iterator should point to the dummy node. Remove the container pointer in the iterator class. Reimplement the member functions so that they have the same effect as before.

### ■■ P14.4
Improve the linked list implementation in Section 14.2 by printing an error message whenever any of the member functions of the List or Iterator classes is invoked with an invalid argument, or when the list or iterator is in an invalid state for the given operation. For example, you should detect a call to get or next when an iterator is at the end of the list, or a call to erase with an iterator that points to a different list.

### ■■ P14.5
Write a class Polynomial that stores a polynomial such as
$p(x)=5x^{10}+9x^{7}-x-10$
as a linked list of terms. A term contains the coefficient and the power of x. For example, you would store $p(x)$ as
$(5,10),(9,7),(-1,1),(-10,0)$
Supply member functions to add, multiply, and print polynomials. Supply a constructor that makes a polynomial from a single term. For example, the polynomial p can be constructed as

```
Polynomial p(Term(-10, 0));
p.add(Polynomial(Term(-1, 1)));
p.add(Polynomial(Term(9, 7)));
p.add(Polynomial(Term(5, 10)));
```

Then compute $p(x) \times p(x)$.

```
Polynomial q = p.multiply(p);
q.print();
```

### ■■ P14.6
Using a queue of vectors, implement a non-recursive variant of the merge sort algorithm as follows. Start by inserting vectors of length 1 for each element into the queue. Keep removing pairs of vectors from the queue, merging them into a single vector, and adding the result back into the queue. Stop when the queue has size 1.

![](img/d61019b035dd82beb581604273c0ee6b_768_0.png)

### ■■■ P14.7
In a paint program, a “flood fill” fills all empty pixels of a drawing with a given color, stopping when it reaches occupied pixels. In this exercise, you will implement a simple variation of this algorithm, flood-filling a 10 × 10 array of integers that are initially 0.
Prompt for the starting row and column.
Push the (row, column) pair on a stack.
You will need to provide a simple Pair class.
Repeat the following operations until the stack is empty:
Pop off the (row, column) pair from the top of the stack.
If it has not yet been filled, fill the corresponding array location with numbers 1, 2, 3, and so on (to show the order in which the square is filled.)
Push the coordinates of any unfilled neighbors in the north, east, south, or west direction on the stack.
When you are done, print the entire array.

the free store, and someone needs to deallocate them. Programmers expect that this happens in the destructor. As you have seen in Section 13.2, you also need to provide a copy constructor and operator= once you have a destructor.

In most cases, the operator= destroys the left-hand side and then copies the right-hand side into the left hand side. However, we cannot call destructors explicitly, and we cannot invoke constructors on existing objects. Instead, let us put the destruction and copy construction activities into two helper functions free and copy. Then we call them in the “big 3” memory management functions as follows:

```
List::List(const List& other)
{
    copy(other);
}
```

```
List::~List()
{
    free();
}
```

```
List& List::operator=(const List& other)
{
    if (this != &other)
    {
        free();
        copy(other);
    }
}
```

Now we just have two functions to implement.

The free function deallocates all nodes. It is straightforward to traverse all nodes and to delete them. You just have to be careful about one issue. As soon as a node is passed to delete, you can no longer use its data members. (Some free store implementations overwrite part of the deleted memory with data for internal use.) Therefore, you need to save the pointer to the next node before deleting a node:

```
void List::free()
{
    Node* to_delete = first;
    while (to_delete != nullptr)
    {
        Node* next_to_delete = to_delete->next;
        delete to_delete;
        to_delete = next_to_delete;
    }
}
```

The copy member function traverses the list that is to be copied, makes a copy of each node, and links the nodes together. The member function must also update the first and last pointers.

```
void List::copy(const List& other)
{
    Node* just_copied = nullptr;
    Node* next_to_copy = other.first;
    first = nullptr;
    last = nullptr;
    while (next_to_copy != nullptr)
    {
        Node* copy = new Node(next_to_copy->data);
        copy->previous = just_copied;
        if (just_copied == nullptr)
        {
```
