
```cpp
else
{
    for (int i = location; i < length - 1; i++)
        list[i] = list[i+1];
    length--;
} //end removeAt
```

The definition of the function retrieveAt is straightforward. The index of the item to be retrieved, and the location where to retrieve the item, are passed as parameters to this function. The definition of this function is:

```cpp
void arrayListType::retrieveAt(int location, int& retItem) const
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be retrieved is "
             << "out of range" << endl;
    else
        retItem = list[location];
} //end retrieveAt
```

The function clearList removes the elements from the list, leaving it empty. Because the member variable length indicates the number of elements in the list, the elements are removed by simply setting length to 0. Therefore, the definition of this function is

```cpp
void arrayListType::clearList()
{
    length = 0;
} //end clearList
```

We now discuss the definition of the constructors and destructor. The constructor creates an array of the size specified by the user, and initializes the length of the list to 0, and the maxSize to the size of the array specified by the user. The size of the array is passed as a parameter to the constructor. The default array size is 100. The destructor deallocates the memory occupied by the array holding the list elements. The definitions of the constructor and the destructor are as follows:

```cpp
arrayListType::arrayListType(int size)
{
    if (size <= 0)
    {
        cout << "The array size must be positive. Creating "
             << "an array of the size 100." << endl;

        maxSize = 100;
    }
    else
        maxSize = size;

    length = 0;

    list = new int[maxSize];
} //end constructor
```

```cpp
arrayListType::~arrayListType()
{
    delete [] list;
} //end destructor
```

Next we describe the copy constructor. Recall that the copy constructor is called when an object is passed as a (value) parameter to a function, and when an object is declared and initialized using the value of another object of the same type. It copies the values of the member variables of the actual object into the corresponding member variables of the formal parameter and the object being created. Its definition is

```cpp
arrayListType::arrayListType(const arrayListType& otherList)
{
    maxSize = otherList.maxSize;
    length = otherList.length;

    list = new int[maxSize]; //create the array

    for (int j = 0; j < length; j++)  //copy otherList
        list[j] = otherList.list[j];
} //end copy constructor
```

### Unordered Lists

As described in the preceding section, we derive the class unorderedArrayListType from the abstract class arrayListType and implement the operations insertAt, insertEnd, replaceAt, seqSearch, insert, and remove.

The definition of the class unorderedArrayListType is: (To save space, we list the member functions without documentation. The descriptions of these functions are the same as the descriptions of the functions of the class arrayListType.)

```cpp
class unorderedArrayListType: public arrayListType
{
public:
    void insertAt(int location, int insertItem);
    void insertEnd(int insertItem);
    void replaceAt(int location, int repItem);
    int seqSearch(int searchItem) const;
    void remove(int removeItem);

    unorderedArrayListType(int size = 100);
      //Constructor.
};
```

We leave the UML class diagram and its inheritance hierarchy of the class unorderedArrayListType as an exercise for you.

The function insertAt inserts an item at a specific location in the list. The item to be inserted and the insert location in the array are passed as parameters to this function. In order to insert the item somewhere in the middle of the list, we must first make room for the new item. That is, we need to move certain elements down one array slot. Consider the list in Figure 12-24.

![](img/d0be7fc6d804b63484835c6c8bc67a07_926_0.png)

The number of elements currently in the list is 6, so length is 6. Thus, after inserting a new element, the length of the list is 7. If the item is to be inserted at, say location 6, we can easily accomplish this by copying the item in list[6]. On the other hand, if the item is to be inserted at, say location 3, we first need to move elements list[3], list[4], and list[5] one array slot right to make room for the new item. Thus, we must first copy list[5] into list[6], list[4] into list[5], and list[3] into list[4], in this order. Then we can copy the new item into list[3].

Of course, special cases such as trying to insert in a full list must be handled separately. Some of these cases can be accomplished by other member functions.

The definition of the function insertAt is as follows:

```cpp
    void unorderedArrayListType::insertAt(int location,
                                          int insertItem)
    {
        if (location < 0 || location >= maxSize)
            cout << "The position of the item to be inserted "
                 << "is out of range." << endl;
        else if (length >= maxSize)  //list is full
            cout << "Cannot insert in a full list" << endl;
        else
        {
            for (int i = length; i > location; i--)
                list[i] = list[i - 1];  //move the elements down

            list[location] = insertItem;  //insert the item at
                                          //the specified position

            length++;  //increment the length
        }
    } //end insertAt
```

The function insertEnd can be implemented by using the function insertAt. However, the function insertEnd does not require the shifting of elements. Therefore, we give its definition directly.

```cpp
    void unorderedArrayListType::insertEnd(int insertItem)
    {
        if (length >= maxSize)  //the list is full
            cout << "Cannot insert in a full list." << endl;
        else
        {
            list[length] = insertItem; //insert the item at the end
            length++; //increment the length
        }
    } //end insertEnd
```

Chapter 8 describes a **sequential or linear** search. For easy reference and the sake of completeness, next we give the sequential search algorithm for array-based lists:

```cpp
int unorderedArrayListType::seqSearch(int searchItem) const
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < length && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;
} //end seqSearch
```

The function remove deletes an item from the list. The item to be deleted is passed as a parameter to this function. In order to delete the item, the function calls the member function seqSearch to determine whether or not the item to be deleted is in the list. If the item to be deleted is found in the list, the item is removed from the list and the length of the list is decremented by 1. If the item to be removed is found in the list, the function seqSearch returns the index of the item in the list to be deleted. We can now use the index returned by the function seqSearch, and use the function removeAt to remove the item from the list. Therefore, the definition of the function remove is:

```cpp
void unorderedArrayListType::remove(int removeItem)
{
    int loc;

    if (length == 0)
        cout << "Cannot delete from an empty list." << endl;
    else
    {
        loc = seqSearch(removeItem);

        if (loc != -1)
            removeAt(loc);
        else
            cout << "The item to be deleted is not in the list."
                 << endl;
    }
} //end remove
```

The definition of the function replaceAt is:

```cpp
void unorderedArrayListType::replaceAt(int location, int repItem)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be "
             << "replaced is out of range." << endl;
```
