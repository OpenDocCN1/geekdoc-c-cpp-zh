
```cpp
void insert(const Type& insertItem);
    //Function to insert insertItem in the list.
    //Precondition: If the list is nonempty, it must be in
    //              order
    //Postcondition: insertItem is inserted at the proper place
    //               in the list; first points to the first
    //               node, last points to the last node of the
    //               new list, and count is incremented by 1.

void deleteNode(const Type& deleteItem);
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing deleteItem
    //               is deleted from the list; first points
    //               to the first node of the new list, last
    //               points to the last node of the new list,
    //               and count is decremented by 1; otherwise
    //               an appropriate message is printed.

doublyLinkedList();
    //default constructor
    //Initializes the list to an empty state.
    //Postcondition: first = nullptr; last = nullptr; count = 0;

doublyLinkedList(const doublyLinkedList<Type>& otherList);
    //copy constructor
~doublyLinkedList();
    //destructor
    //Postcondition: The list object is destroyed.

    protected:
        int count;
        nodeType<Type> *first;   //pointer to the first node
        nodeType<Type> *last;    //pointer to the last node

    private:
        void copyList(const doublyLinkedList<Type>& otherList);
            //Function to make a copy of otherList.
            //Postcondition: A copy of otherList is created and
            //               assigned to this list.

};
```

We leave the UML class diagram of the class doublyLinkedList as an exercise for you.

The functions to implement the operations of a doubly linked list are similar to the ones discussed earlier. Here, because every node has two pointers, back and next, some of the operations require the adjustment of two pointers in each node. For the insert and delete operations, because we can traverse the list in either direction, we use only one pointer to traverse the list. Let us call this pointer current. We can set the value of trailCurrent by using both the current pointer and the back pointer of the node pointed to by current. We give the definition of each function here, with four exceptions. Definitions of the functions copyList, the copy constructor, overloading the assignment operator, and the destructor are left as exercises for you. (See Programming Exercise 11 at the end of this chapter.) Moreover, the function copyList is used only to implement the copy constructor and overload the assignment operator.

### Default Constructor

The default constructor initializes the doubly linked list to an empty state. It sets first and last to nullptr and count to 0.

```cpp
template <class Type>
doublyLinkedList<Type>::doublyLinkedList()
{
        first = nullptr;
        last = nullptr;
        count = 0;
}
```

### isEmptyList

This operation returns true if the list is empty; otherwise, it returns false. The list is empty if the pointer first is nullptr.

```cpp
template <class Type>
bool doublyLinkedList<Type>::isEmptyList() const
{
        return (first == nullptr);
}
```

### Destroy the List

This operation deletes all of the nodes in the list, leaving the list in an empty state. We traverse the list starting at the first node and then delete each node. Furthermore, count is set to 0.

```cpp
template <class Type>
void doublyLinkedList<Type>::destroy()
{
        nodeType<Type> *temp; //pointer to delete the node

        while (first != nullptr)
        {
                temp = first;
                first = first->next;
                delete temp;
        }

        last = nullptr;
        count = 0;
}
```

### Initialize the List

This operation reinitializes the doubly linked list to an empty state. This task can be done by using the operation destroy. The definition of the function initializeList is:

```cpp
template <class Type>
void doublyLinkedList<Type>::initializeList()
{
    destroy();
}
```

### Length of the List

The length of a linked list (that is, how many nodes are in the list) is stored in the variable count. Therefore, this function returns the value of this variable.

```cpp
template <class Type>
int doublyLinkedList<Type>::length() const
{
    return count;
}
```

### Print the List

The function print outputs the info contained in each node. We traverse the list, starting from the first node.

```cpp
template <class Type>
void doublyLinkedList<Type>::print() const
{
    nodeType<Type> *current; //pointer to traverse the list
    current = first; //set current to point to the first node

    while (current != nullptr)
    {
        cout << current->info << "  "; //output info
        current = current->next;
    }//end while
}//end print
```

### Reverse Print the List

This function outputs the info contained in each node in reverse order. We traverse the list in reverse order, starting from the last node. Its definition is:

```cpp
template <class Type>
void doublyLinkedList<Type>::reversePrint() const
{
    nodeType<Type> *current; //pointer to traverse
                             //the list
    current = last;    //set current to point to the
                       //last node

    while (current != nullptr)
    {
        cout << current->info << " ";
        current = current->back;
    }//end while
}//end reversePrint
```

### Search the List

The function search returns true if searchItem is found in the list; otherwise, it returns false. The search algorithm is exactly the same as the search algorithm for an ordered linked list.

```cpp
template <class Type>
bool doublyLinkedList<Type>::search(const Type& searchItem) const
{
    bool found = false;
    nodeType<Type> *current;  //pointer to traverse the list

    current = first;

    while (current != nullptr && !found)
        if (current->info >= searchItem)
            found = true;
        else
            current = current->next;

    if (found)
        found = (current->info == searchItem);  //test for
                                                //equality

    return found;
}//end search
```

### First and Last Elements

The function front returns the first element of the list, and the function back returns the last element of the list. If the list is empty, both functions terminate the program. Their definitions are:

```cpp
template <class Type>
Type doublyLinkedList<Type>::front() const
{
    assert(first != nullptr);

    return first->info;
}
```

```cpp
template <class Type>
Type doublyLinkedList<Type>::back() const
{
    assert(last != nullptr);

    return last->info;
}
```

## INSERT A NODE

Because we are inserting an item in a doubly linked list, the insertion of a node in the list requires the adjustment of two pointers in certain cases. As before, we find the place where the new item is supposed to be inserted, create the node, store the new item, and adjust the link fields of the new node and other particular nodes in the list. There are four cases:

- **Case 1:** Insertion in an empty list
- **Case 2:** Insertion at the beginning of a nonempty list
- **Case 3:** Insertion at the end of a nonempty list
- **Case 4:** Insertion somewhere in a nonempty list

Both Cases 1 and 2 require us to change the value of the pointer `first`. Cases 3 and 4 are similar. After inserting an item, `count` is incremented by 1. Next, we show Case 4.

Consider the doubly linked list shown in Figure 16-40.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1176_0.png)

**FIGURE 16-40**  Doubly linked list before inserting 20

Suppose that 20 is to be inserted in the list. After inserting 20, the resulting list is as shown in Figure 16-41.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1177_0.png)

**FIGURE 16-41**  Doubly linked list after inserting 20

From Figure 16-41, it follows that the next pointer of node 15, the back pointer of node 24, and both the next and back pointers of node 20 need to be adjusted.

The definition of the function insert is:

```cpp
template <class Type>
void doublyLinkedList<Type>::insert(const Type& insertItem)
{
    nodeType<Type> *current;       //pointer to traverse the list
    nodeType<Type> *trailCurrent;   //pointer just before current
    nodeType<Type> *newNode;        //pointer to create a node
    bool found;

    newNode = new nodeType<Type>;   //create the node
    newNode->info = insertItem;     //store the new item in the node
    newNode->next = nullptr;
    newNode->back = nullptr;

    if (first == nullptr) //if the list is empty, newNode is
                          //the only node
    {
        first = newNode;
        last = newNode;
        count++;
    }
    else
    {
        found = false;
        current = first;

        while (current != nullptr && !found) //search the list
            if (current->info >= insertItem)
                found = true;
            else
            {
                trailCurrent = current;
                current = current->next;
            }
```
