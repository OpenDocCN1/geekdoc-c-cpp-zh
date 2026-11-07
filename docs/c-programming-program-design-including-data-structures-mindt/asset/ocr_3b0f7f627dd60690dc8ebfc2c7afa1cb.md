The function `insertAt` inserts an item at a specific location in the list. The item to be inserted and the insert location in the array are passed as parameters to this function. In order to insert the item somewhere in the middle of the list, we must first make room for the new item. That is, we need to move certain elements down one array slot. Consider the list in Figure 12-24.

![](bbox=[0.182, 0.201, 0.909, 0.278])

**FIGURE 12-24**  Array list

The number of elements currently in the list is 6, so length is 6. Thus, after inserting a new element, the length of the list is 7. If the item is to be inserted at, say, location 6, we can easily accomplish this by copying the item in `list[6]`. On the other hand, if the item is to be inserted at, say, location 3, we first need to move `list[3]`, `list[4]`, and `list[5]` one array slot left to make room for the new item. Thus, we must first copy `list[5]` into `list[6]`, `list[4]` into `list[5]`, and `list[3]` into `list[4]`, in this order. Then we can copy the new item into `list[3]`.

Of course, special cases such as trying to insert in a full list must be handled separately. Some of these cases can be accomplished by other member functions.

The definition of the function `insertAt` is as follows:

```
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