```
```cpp
while (first != NULL)    //while there are nodes in the list
{
    temp = first;        //set temp to the current node
    first = first->link; //advance first to the next node
    delete temp;         //deallocate the memory occupied by temp
}

last = NULL;             //initialize last to NULL; first has already
                         //been set to NULL by the while loop
count = 0;
}
```
```

# INITIALIZE THE LIST

The function initializeList initializes the list to an empty state. Note that the default constructor or the copy constructor has already initialized the list when the list object was declared. This operation, in fact, reinitializes the list to an empty state, so it must delete the nodes (if any) from the list. This task can be accomplished by using the destroyList operation, which also resets the pointers first and last to NULL and sets count to 0.

```
```cpp
template <class Type>
void linkedListType<Type>::initializeList()
{
    destroyList(); //if the list has any nodes, delete them
}
```
```

# Print the List

The member function print prints the data contained in each node. To do so, we must traverse the list, starting at the first node. Because the pointer first always points to the first node in the list, we need another pointer to traverse the list. (If we use first to traverse the list, the entire list will be lost.)

```
```cpp
template <class Type>
void linkedListType<Type>::print() const
{
    nodeType<Type> * current; //pointer to traverse the list

    current = first;           //set current so that it points to
                               //the first node
    while (current != NULL)    //while more data to print
    {
        cout << current->info << " ";
        current = current->link;
    }
}//end print
```
```

# Length of a List

The length of a linked list (that is, how many nodes are in the list) is stored in the variable count. Therefore, this function returns the value of this variable: