Deletion can be performed using the following function:

```
void Array :: Delete(int Location)
{
    int i;
    for(i = Location; i < Size; i++)
    {
        A[i - 1] = A[i];
        // shifting elements to the left by 1 position
    }
    A[Size - 1] = 0;
    // Store 0 at the last location to mark it empty
    Size = Size - 1;
}

void main()
{
    Array A;
    A.Read_Array();
    A.Display(); // Traverse_Forward()
    A.Traverse_Backward();
    A.Insert(3, 66); // insert at position 3
    A.Display();
    cout << endl;
    A.Delete(3); // delete 4th element
    A.Display();
    cout << endl;
    cout << A.Search(66);
    cout << A.Search(3);
}
```

We have studied the basic operations for an array, such as reading an array and traversing it along with some common operations such as inserting an element and deleting an element in an array. Insertion and deletion operations need data shifting within the array.

The array and its operations in Program Code 2.1 are defined. To define an array of floating point data to operate on integer data, we need to change `int A[]` to `float A[]` in declaration of data members of class. This can be done each time the data type of array elements varies by editing the code using text editor and then recompiling it. C++ has a feature called template (also known as parameterized type). A template is a variable that can be instantiated to any data type. This data type could be a built-in or a user-defined type.