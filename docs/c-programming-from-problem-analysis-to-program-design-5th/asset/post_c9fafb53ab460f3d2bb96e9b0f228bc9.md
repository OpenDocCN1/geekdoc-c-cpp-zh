
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

## INITIALIZE THE LIST

The function initializeList initializes the list to an empty state. Note that the default constructor or the copy constructor has already initialized the list when the list object was declared. This operation, in fact, reinitializes the list to an empty state, so it must delete the nodes (if any) from the list. This task can be accomplished by using the destroyList operation, which also resets the pointers first and last to NULL and sets count to 0.

```cpp
template <class Type>
void linkedListType<Type>::initializeList()
{
    destroyList(); //if the list has any nodes, delete them
}
```

## Print the List

The member function print prints the data contained in each node. To do so, we must traverse the list, starting at the first node. Because the pointer first always points to the first node in the list, we need another pointer to traverse the list. (If we use first to traverse the list, the entire list will be lost.)

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

## Length of a List

The length of a linked list (that is, how many nodes are in the list) is stored in the variable count. Therefore, this function returns the value of this variable:

```cpp
template <class Type>
int linkedListType<Type>::length() const
{
    return count;
}
```

## Retrieve the Data of the First Node

The function front returns the info contained in the first node, and its definition is straightforward:

```cpp
template <class Type>
Type linkedListType<Type>::front() const
{
    assert(first != NULL);

    return first->info; //return the info of the first node
}//end front
```

Notice that if the list is empty, the assert statement terminates the program. Therefore, before calling this function, check to see whether the list is nonempty.

## Retrieve the Data of the Last Node

The function back returns the info contained in the last node, and its definition is straightforward:

```cpp
template <class Type>
Type linkedListType<Type>::back() const
{
    assert(last != NULL);

    return last->info; //return the info of the last node
}//end back
```

Notice that if the list is empty, the assert statement terminates the program. Therefore, before calling this function, check to see whether the list is nonempty.

## Begin and End

The function begin returns an iterator to the first node in the linked list, and the function end returns an iterator to one past the last node in the linked list. Their definitions are:

```cpp
template <class Type>
linkedListIterator<Type> linkedListType<Type>::begin()
{
    linkedListIterator<Type> temp(first);

    return temp;
}
```

```cpp
template <class Type>
linkedListIterator<Type> linkedListType<Type>::end()
{
    linkedListIterator<Type> temp (NULL);

    return temp;
}
```

## Copy the List

The function copyList makes an identical copy of a linked list. Therefore, we traverse the list to be copied, starting at the first node. Corresponding to each node in the original list, we:

- a. Create a node, and call it newNode.
- b. Copy the info of the node (in the original list) into newNode.
- c. Insert newNode at the end of the list being created.

The definition of the function copyList is:

```cpp
template <class Type>
void linkedListType<Type>::copyList
                      (const linkedListType<Type> & otherList)
{
    nodeType<Type> *newNode;  //pointer to create a node
    nodeType<Type> *current;  //pointer to traverse the list

    if (first != NULL)  //if the list is nonempty, make it empty
        destroyList();

    if (otherList.first == NULL)  //otherList is empty
    {
        first = NULL;
        last = NULL;
        count = 0;
    }
    else
    {
        current = otherList.first;  //current points to the
                                     //list to be copied
        count = otherList.count;

        //copy the first node
        first = new nodeType<Type>;  //create the node
        first->info = current->info; //copy the info
        first->link = NULL;          //set the link field of
                                     //the node to NULL
        last = first;                //make last point to the
                                     //first node
        current = current->link;     //make current point to
                                     //the next node

        //copy the remaining list
        while (current != NULL)
        {
            newNode = new nodeType<Type>;  //create a node
            newNode->info = current->info;  //copy the info
            newNode->link = NULL;           //set the link of
                                            //newNode to NULL
            last->link = newNode;           //attach newNode after last
            last = newNode;                 //make last point to
                                            //the actual last node
            current = current->link;        //make current point
                                            //to the next node
        } //end while
    } //end else
} //end copyList
```

## Destructor

The destructor deallocates the memory occupied by the nodes of a list when the class object goes out of scope. Because memory is allocated dynamically, resetting the pointers first and last does not deallocate the memory occupied by the nodes in the list. We must traverse the list, starting at the first node, and delete each node in the list. The list can be destroyed by calling the function destroyList. Therefore, the definition of the destructor is:

```cpp
template <class Type>
linkedListType<Type>::~linkedListType() //destructor
{
    destroyList();
}
```

## Copy Constructor

Because the class linkedListType contains pointer data members, the definition of this class contains the copy constructor. Recall that if a formal parameter is a value parameter, the copy constructor provides the formal parameter with its own copy of the data. The copy constructor also executes when an object is declared and initialized using another object. (For more information, see Chapter 14.)

The copy constructor makes an identical copy of the linked list. This can be done by calling the function copyList. Because the function copyList checks whether the original is empty by checking the value of first, we must first initialize the pointer first to NULL before calling the function copyList.

The definition of the copy constructor is:

```cpp
template <class Type>
linkedListType<Type>::linkedListType
                  (const linkedListType<Type>& otherList)
{
    first = NULL;
    copyList(otherList);
} //end copy constructor
```

## Overloading the Assignment Operator

The definition of the function to overload the assignment operator for the class `linkedListType` is similar to the definition of the copy constructor. We give its definition for the sake of completeness.

```cpp
//overload the assignment operator
template <class Type>
const linkedListType<Type>& linkedListType<Type>::operator=
                         (const linkedListType<Type>& otherList)
{
    if (this != &otherList) //avoid self-copy
    {
        copyList(otherList);
    } //end else

    return *this;
}
```

## Unordered Linked Lists

As described in the preceding section, we derive the class `unorderedLinkedList` from the abstract class `linkedListType` and implement the operations search, insertFirst, insertLast, and deleteNode.

The following class defines an unordered linked list as an ADT.

```cpp
template <class Type>
class unorderedLinkedList: public linkedListType<Type>
{
public:
    bool search(const Type& searchItem) const;
    //Function to determine whether searchItem is in the list.
    //Postcondition: Returns true if searchItem is in the
    //              list; otherwise the value false is
    //              returned.

    void insertFirst(const Type& newItem);
    //Function to insert newItem at the beginning of the list.
    //Postcondition: first points to the new list, newItem is
    //              inserted at the beginning of the list,
    //              last points to the last node in the
    //              list, and count is incremented by 1.

    void insertLast(const Type& newItem);
    //Function to insert newItem at the end of the list.
    //Postcondition: first points to the new list, newItem
    //              is inserted at the end of the list,
    //              last points to the last node in the
    //              list, and count is incremented by 1.

    void deleteNode(const Type& deleteItem);
    //Function to delete deleteItem from the list.
    //Postcondition: If found, the node containing
```
