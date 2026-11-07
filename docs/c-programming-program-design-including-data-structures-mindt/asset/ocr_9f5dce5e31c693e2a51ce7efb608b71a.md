+   3. A variable, **maxSize**, to store the size of the array (that is, the maximum number of elements that can be stored on an array).

Now that you know the operations to be performed on a list and ways to store the list into computer memory, we can define the class implementing the list as an ADT (abstract data type). For illustration purposes, we assume that the elements of the list are of type `int`. We will remove this restriction when we discuss class templates in Chapter 13; there, we will develop a generic class that can be used to process a variety of lists.

The following class defines an array-based list ints as an ADT;

Now that you know the operations to be performed on a list and how to store the list into the computer’s memory, next we define the abstract class `arrayListType` implementing the list as an ADT (abstract data type).

```
class arrayListType
{
public:
    bool isEmpty() const;
        //Function to determine whether the list is empty
        //Postcondition: Returns true if the list is empty;
        //               otherwise, returns false.
        //

    bool isFull() const;
        //Function to determine whether the list is full
        //Postcondition: Returns true if the list is full;
        //               otherwise, returns false.
        //

    int listSize() const;
        //Function to determine the number of elements in
        //the list.
        //Postcondition: Returns the value of length.

    int maxListSize() const;
        //Function to determine the maximum size of the list
        //Postcondition: Returns the value of maxSize.

    void print() const;
        //Function to output the elements of the list
        //Postcondition: Elements of the list are output on the
        //               standard output device.

    bool isItemAtEqual(int location, int item) const;
        //Function to determine whether item is the same as
        //the item in the list at the position specified
        //by location.
        //Postcondition: Returns true if list[location]
        //               is the same as item; otherwise,
        //               returns false.
        //
        //               If location is out of range, an
        //               appropriate message is displayed.
```