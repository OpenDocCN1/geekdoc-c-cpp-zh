
```cpp
//Note that this is an abstract function.
//Postcondition: If removeItem is found in the list,
//              it is removed from the list and
//              length is decremented by one.
//
arrayListType(int size = 100);
//Constructor
//Creates an array of the size specified by the
//parameter size. The default array size is 100.
//Postcondition: The list points to the array,
//              length = 0, and maxSize = size;

arrayListType (const arrayListType& otherList);
//Copy constructor

virtual ~arrayListType();
//Destructor
//Deallocate the memory occupied by the array.

protected:
    int *list;     //array to hold the list elements
    int length;    //variable to store the length of the list
    int maxSize;   //variable to store the maximum
                   //size of the list
};
```

Figure 12-22 shows the UML class diagram of the class `arrayListType`. Note that in the UML class diagram, the name of the abstract class and abstract function are shown in italics.

![](img/b217c421655b51e7494cf3b89bb5432d_926_0.png)

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

The definition of the function `isItemAtEqual` is straightforward. If the element at the position location is the same as item, it returns `true`. If either location is out of range or item is not in the list, it returns `false`. The definition of this function is:

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

The function `removeAt` removes an item from a specific location in the list. The location of the item to be removed is passed as a parameter to this function. After removing the item from the list, the length of the list is reduced by 1. If the item to be removed is somewhere in the middle of the list, after removing the item we must move certain elements up one array slot because we cannot leave holes in the portion of the array containing the list. Figure 12-23 illustrates this concept.

![](img/b217c421655b51e7494cf3b89bb5432d_928_0.png)

**FIGURE 12-23**  Array list

The number of elements currently in the list is 6, so `length` is 6. Thus, after removing an element, the length of the list is 5. Suppose that the item to be removed is at, say, location 3. Clearly, we must move `list[4]` into `list[3]` and `list[5]` into `list[4]`, in this order.

The definition of the function `removeAt` is:

```cpp
void arrayListType::removeAt(int location)
{
    if (location < 0 || location >= length)
        cout << "The location of the item to be removed "
             << "is out of range." << endl;
    else
    {
        for (int i = location; i < length - 1; i++)
            list[i] = list[i + 1];

        length--;
    }
} //end removeAt
```

The definition of the function `retrieveAt` is straightforward. The index of the item to be retrieved, and the location where to retrieve the item, are passed as parameters to this function. The definition of this function is as follows:

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

The function `clearList` removes the elements from the list, leaving it empty. Because the member variable `length` indicates the number of elements in the list, the elements are removed by simply setting `length` to 0. Therefore, the definition of this function is

```cpp
void arrayListType::clearList()
{
    length = 0;
} //end clearList
```

We now discuss the definition of the constructor and destructor. The constructor creates an array of the size specified by the user, and initializes the `length` of the list to 0 and the `maxSize` to the size of the array specified by the user. The size of the array is passed as a parameter to the constructor. The default array size is 100. The destructor deallocates the memory occupied by the array holding the list elements. The definitions of the constructor and the destructor are as follows:

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

arrayListType::~arrayListType()
{
    delete [] list;
} //end destructor
```

Next we describe the copy constructor. Recall that the copy constructor is called when an object is passed as a (value) parameter to a function, and when an object is declared and initialized using the value of another object of the same type. It copies the values of the member variables of the actual object into the corresponding member variables of the formal parameter and the object being created. Its definition is as follows:

```cpp
arrayListType::arrayListType(const arrayListType& otherList)
{
    maxSize = otherList.maxSize;
    length = otherList.length;

    list = new int[maxSize];  //create the array
    for (int j = 0; j < length; j++) //copy otherList
        list[j] = otherList.list[j];
} //end copy constructor
```

## Unordered Lists

As described in the preceding section, we derive the class `unorderedArrayListType` from the abstract class `arrayListType` and implement the operations `insertAt`, `insertEnd`, `replaceAt`, `seqSearch`, `insert`, and `remove`.

The definition of the class `unorderedArrayListType` is as follows: (To save space, we list the member functions without documentation. The descriptions of these functions are the same as the descriptions of the functions of the class `arrayListType`.)

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
    //Constructor
};
```

We leave the UML class diagram and its inheritance hierarchy of the class `unorderedArrayListType` as an exercise for you.

The function `insertAt` inserts an item at a specific location in the list. The item to be inserted and the insert location in the array are passed as parameters to this function. In order to insert the item somewhere in the middle of the list, we must first make room for the new item. That is, we need to move certain elements down one array slot. Consider the list in Figure 12-24.

![](img/b217c421655b51e7494cf3b89bb5432d_931_0.png)

**FIGURE 12-24**  Array list

The number of elements currently in the list is 6, so length is 6. Thus, after inserting a new element, the length of the list is 7. If the item is to be inserted at, say, location 6, we can easily accomplish this by copying the item in `list[6]`. On the other hand, if the item is to be inserted at, say, location 3, we first need to move `list[3]`, `list[4]`, and `list[5]` one array slot left to make room for the new item. Thus, we must first copy `list[5]` into `list[6]`, `list[4]` into `list[5]`, and `list[3]` into `list[4]`, in this order. Then we can copy the new item into `list[3]`.

Of course, special cases such as trying to insert in a full list must be handled separately. Some of these cases can be accomplished by other member functions.

The definition of the function `insertAt` is as follows:

```cpp
void unorderedArrayListType::insertAt(int location,
                                      int insertItem)
{
    if (location < 0 || location >= maxSize)
        cout << "The position of the item to be inserted "
             << "is out of range." << endl;
    else if (length >= maxSize) //list is full
        cout << "Cannot insert in a full list." << endl;
    else
    {
        for (int i = length; i > location; i--)
            list[i] = list[i - 1]; //move the elements down

        list[location] = insertItem; //insert the item at
                                     //the specified position

        length++; //increment the length
    }
} //end insertAt
```

The function `insertEnd` can be implemented by using the function `insertAt`. However, the function `insertEnd` does not require the shifting of elements. Therefore, we give its definition directly.
