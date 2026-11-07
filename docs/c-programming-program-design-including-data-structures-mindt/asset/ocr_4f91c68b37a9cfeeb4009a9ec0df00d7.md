```
```cpp
cin >> number;                                      //Line 19
cout << endl;                                        //Line 20

intList.remove(number);                              //Line 21

cout << "Line 22: After removing" << number          //Line 22
     << " in intList: ";                             //Line 23
intList.print();                                      //Line 24
cout << endl;

cout << "Line 25: Enter the search item: ";          //Line 25
cin >> number;                                        //Line 26
cout << endl;                                         //Line 27

if (intList.seqSearch(number) != -1)                  //Line 28
    cout << "Line 29: " << number                    //Line 29
         << " found in intList." << endl;
else                                                  //Line 30
    cout << "Line 31: " << number                    //Line 31
         << " is not in intList." << endl;

return 0;                                             //Line 32
}                                                     //Line 33
```
```

**Sample Run:** In this sample run, the user input is shaded.

Line 8: Enter 8 integers: **35 62 18 26 45 72 55 60**

Line 15: intList: 35 62 18 26 45 72 55 60

Line 18: Enter the number to be deleted: **62**

Line 22: After removing 62 intList: 35 18 26 45 72 55 60

Line 25: Enter the search item: **72**

Line 29: 72 found in intList.

The preceding program is self-explanatory. We leave the details as an exercise.

> **NOTE**  The website accompanying this book contains the program `testProgUnorderedList_II.cpp`, which illustrates how the copy constructor on an `unorderedArrayListType` object works.

> **NOTE**  **(Unordered Set)** Recall that a list is a collection of elements of the same type. However, in a list an element may repeat. That is, the elements of the list need not be distinct. On the other hand, a set is also a collection of elements of the same type. However, the elements of a set are distinct. It follows that a set is a list with distinct elements. In this section we describe the class `unorderedArrayListType` to process unordered lists. Note that the functions `insertAt` and `insertEnd` do not check whether the item to be inserted is already in the list. Similarly, the function `replaceAt` does not check if the item to be replaced is already in the list. Just as you can design a class to manipulate lists, you can also design a class to manipulate sets. Programming Exercise 12, at the end of this chapter, asks you to design the class `unorderedSetType`, derived from the class `unorderedArrayListType`, to manipulate sets.