```
//specified by position.
//Postcondition: list[position] = item; length++;
//
//            If position is out of range, the program
//            is aborted.

listType(int listSize = 50);
//Constructor
//Creates an array of the size specified by the
//parameter listSize; the default array size is 50.
//Postcondition: list contains the base address of the
//            array; length = 0; maxsize = listSize;

~listType();
//Destructor
//Deletes all the elements of the list.
//Postcondition: The array list is deleted.

private:
    int maxSize;    //variable to store the maximum size
                    //of the list
    int length;     //variable to store the number of elements
                    //in the list
    elemType *list; //pointer to the array that holds the
                    //list elements
};


template <class elemType>
bool listType<elemType>::isEmpty() const
{
    return (length == 0)
}

template <class elemType>
bool listType<elemType>::isFull() const
{
    return (length == maxSize);
}

template <class elemType>
int listType<elemType>::getLength() const
{
    return length;
}

template <class elemType>
int listType<elemType>::getMaxSize() const
{
    return maxSize;
}

    //Constructor; the default array size is 50
template <class elemType>

```