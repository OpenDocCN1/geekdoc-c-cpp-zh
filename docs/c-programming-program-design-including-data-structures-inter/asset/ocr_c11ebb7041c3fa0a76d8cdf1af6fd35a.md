Notice that the member variables of the class `arrayListType` are declared as protected. Moreover notice that the functions `insertAt`, `insertEnd`, `replaceAt`, `seqSearch`, `insert`, and `remove` are declared as abstract. This is because, as noted earlier, typically we deal with two types of lists—lists whose elements are arranged according to some criteria, such as sorted list, and lists whose elements are in no particular order, unsorted lists. The algorithms to implement the operations search, insert, and remove slightly differs for sorted and unsorted lists. Therefore, by using the principle of inheritance, from the class `arrayListType`, we in fact, will derive two classes: `orderedArrayListType` and `unorderedArrayListType`.

Objects of the class `unorderedArrayListType` would arrange list elements in no particular order, that is, the lists are unsorted. On the other hand, objects of the class `orderedArrayListType` would arrange elements according to some comparison criteria, usually, greater than or equal to. That is, these lists will be in ascending order. Moreover, after inserting an element into or removing an element from an ordered list, the resulting list will be ordered. We will, therefore, separately describe the algorithm to implement the operations search, insert, and remove for unsorted and sorted lists. Because each of the classes `orderedArrayListType` and `unorderedArrayListType` will provide separate definitions of the functions `insertAt`, `insertEnd`, `replaceAt`, `seqSearch`, `insert`, and `remove`, and because these functions would access the instance variable, to provide direct access to the instance variables, the instance variables are declared as protected.

Next, we write the definitions of the nonabstract functions.

The list is empty if length is 0; it is full if length is equal to maxSize. Therefore, the definitions of the functions isEmpty and isFull are

```
```cpp
bool arrayListType::isEmpty() const
{
    return (length == 0);
} //end isEmpty

bool arrayListType::isFull() const
{
    return (length == maxSize);
} //end isFull
```
```

The member variable length of the class arrayListType stores the number of elements currently in the list. Similarly, because the size of the array holding the list elements is stored in the member variable maxSize, maxSize specifies the maximum size of the list. Therefore, the definitions of the functions listSize and maxListSize are

```
```cpp
int arrayListType::listSize() const
{
    return length;
} //end listSize

int arrayListType::maxListSize() const
{
    return maxSize;
} //end maxListSize
```
```