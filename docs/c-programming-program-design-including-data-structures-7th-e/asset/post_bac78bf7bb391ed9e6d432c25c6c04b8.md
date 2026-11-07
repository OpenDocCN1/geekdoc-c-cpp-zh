
```cpp
virtual void insertAt(int location, int insertItem) = 0;
    //Function to insert insertItem in the list at the
    //position specified by location.
    //Note that this is an abstract function.
    //Postcondition: Starting at location, the elements of
    //              the list are shifted down,
    //              list[location] = insertItem; length++;
    //              If the list is full or location is out of
    //              range, an appropriate message is displayed.

virtual void insertEnd(int insertItem) = 0;
    //Function to insert insertItem at the end of
    //the list. Note that this is an abstract function.
    //Postcondition: list[length] = insertItem; and length++;
    //              If the list is full, an appropriate
    //              message is displayed.

void removeAt(int location);
    //Function to remove the item from the list at the
    //position specified by location.
    //Postcondition: The list element at list[location] is
    //              removed and length is decremented by 1.
    //              If location is out of range, an
    //              appropriate message is displayed.

void retrieveAt(int location, int& retItem) const;
    //Function to retrieve the element from the list at the
    //position specified by location.
    //Postcondition: retItem = list[location]
    //              If location is out of range, an
    //              appropriate message is displayed.

virtual void replaceAt(int location, int repItem) = 0;
    //Function to replace repItem the element in the list
    //at the position specified by location.
    //Note that this is an abstract function.
    //Postcondition: list[location] = repItem
    //              If location is out of range, an
    //              appropriate message is displayed.

void clearList();
    //Function to remove all the elements from the list
    //After this operation, the size of the list is zero.
    //Postcondition: length = 0;

virtual int seqSearch(int searchItem) const = 0;
    //Function to search the list for searchItem.
    //Note that this is an abstract function.
    //Postcondition: If the item is found, returns the
    //              location in the array where the item is
    //              found; otherwise, returns -1.

virtual void remove(int removeItem) = 0;
    //Function to remove removeItem from the list.
    //Note that this is an abstract function.
    //Postcondition: If removeItem is found in the list,
    //              it is removed from the list and length
    //              is decremented by one.

arrayListType(int size = 100);
    //Constructor
    //Creates an array of the size specified by the
    //parameter size. The default array size is 100.
    //Postcondition: The list points to the array, length = 0,
    //               and maxSize = size.

arrayListType(const arrayListType &otherList);
    //Copy constructor

virtual ~arrayListType();
    //Destructor
    //Deallocate the memory occupied by the array.

protected:
    int *list;       //array to hold the list elements
    int length;      //variable to store the length of the list
    int maxSize;     //size of the list

};
```

Figure 12-22 shows the UML class diagram of the class `arrayListType`. Note that in the UML class diagram, the name of an abstract class and abstract function is shown in italics.

![](img/d0be7fc6d804b63484835c6c8bc67a07_921_0.png)

**FIGURE 12-22** UML diagram of the class `arrayListType`

Notice that the member variables of the class `arrayListType` are declared as `protected`. Moreover notice that the functions `insertAt`, `insertEnd`, `replaceAt`, `seqSearch`, `insert`, and `remove` are declared as abstract. This is because, as noted earlier, typically we deal with two types of lists—lists whose elements are arranged according to some criteria, such as sorted list, and lists whose elements are in no particular order, unsorted lists. The algorithms to implement the operations search, insert, and remove slightly differ for sorted and unsorted lists. Therefore, by using the principle of inheritance, from the class `arrayListType`, we will, in fact, derive two classes: `orderedArrayListType` and `unorderedArrayListType`.

Objects of the class `unorderedArrayListType` would arrange list elements in no particular order, that is, these lists are unsorted. On the other hand, objects of the class `orderedArrayListType` would arrange elements according to some comparison criteria, usually greater than or equal to. That is, these lists will be in ascending order. Moreover, after inserting an element into or removing an element from an ordered list, the resulting list will be ordered. We will, therefore, separately describe the algorithm to implement the operations search, insert, and remove for unsorted and sorted lists. Because each of the classes `orderedArrayListType` and `unorderedArrayListType` will provide separate definitions of the functions `insertAt`, `insertEnd`, `replaceAt`, `seqSearch`, `insert`, and `remove`, and because these functions would access the instance variable, to provide direct access to the instance variables, the instance variables are declared as protected.

Next, we write the definitions of the nonabstract functions.

The list is empty if length is 0; it is full if length is equal to `maxSize`. Therefore, the definitions of the functions `isEmpty` and `isFull` are

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

The member variable `length` of the class `arrayListType` stores the number of elements currently in the list. Similarly, because the size of the array holding the list elements is stored in the member variable `maxSize`, `maxSize` specifies the maximum size of the list. Therefore, the definitions of the functions `listSize` and `maxListSize` are

```cpp
int arrayListType::listSize() const
{
    return length;
} //end listSize
```

```cpp
int arrayListType::maxListSize() const
{
    return maxSize;
} //end maxListSize
```

The member function `print` outputs the elements of the list. We assume that the output is sent to the standard output device:

```cpp
void arrayListType::print() const
{
    for (int i = 0; i < length; i++)
        cout << list[i] << " ";
    cout << endl;
} //end print
```

The definition of the function `isItemAtEqual` is straightforward. If element at the position location is the same as item, it returns `true`. If either location is out of range or item is not in the list, it returns `false`. The definition of this function is:

```cpp
bool arrayListType::isItemAtEqual(int location, int item) const
{
    if (location < 0 || location >= length)
    {
        cout << "The location of the item to be removed "
             << "is out of range." << endl;

        return false;
    }
    else
        return (list[location] == item);
} //end isItemAtEqual
```

The function `removeAt` removes an item from a specific location in the list. The location of the item to be removed is passed as a parameter to this function. After removing the item from the list, the length of the list is reduced by 1. If the item to be removed is somewhere in the middle of the list, after removing the item we must move certain elements up one array slot because we cannot leave holes in the portion of the array containing the list. Figure 12–23 illustrates this concept.

![](img/d0be7fc6d804b63484835c6c8bc67a07_923_0.png)

**FIGURE 12-23** Array list

The number of elements currently in the list is 6, so length is 6. Thus, after removing an element, the length of the list is 5. Suppose that the item to be removed is, say, location 3. Clearly, we must move list[4] into list[3] and list[5] into list[4], in this order.

The definition of the function `removeAt` is

```cpp
void arrayListType::removeAt(int location)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be removed "
             << "is out of range." << endl;
```
