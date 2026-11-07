# Length of a List

The length of a linked list (that is, how many nodes are in the list) is stored in the variable count. Therefore, this function returns the value of this variable:

```
```cpp
template <class Type>
int linkedListType<Type>::length() const
{
    return count;
} //end length
```
```

# Retrieve the Data of the First Node

The function front returns the info contained in the first node, and its definition is straightforward:

```
```cpp
template <class Type>
Type linkedListType<Type>::front() const
{
    assert(first != nullptr);

    return first->info; //return the info of the first node
} //end front
```
```

Notice that if the list is empty, the assert statement terminates the program. Therefore, before calling this function, check to see whether the list is nonempty.

# Retrieve the Data of the Last Node

The function back returns the info contained in the last node, and its definition is straightforward:

```
```cpp
template <class Type>
Type linkedListType<Type>::back() const
{
    assert(last != nullptr);

    return last->info; //return the info of the last node
} //end back
```
```

Notice that if the list is empty, the assert statement terminates the program. Therefore, before calling this function, check to see whether the list is nonempty.

# Begin and End

The function begin returns an iterator to the first node in the linked list, and the function end returns an iterator to one past the last node in the linked list. Their definitions are as follows:

```
```cpp
template <class Type>
linkedListIterator<Type> linkedListType<Type>::begin()
{
    linkedListIterator<Type> temp(first);
```
```