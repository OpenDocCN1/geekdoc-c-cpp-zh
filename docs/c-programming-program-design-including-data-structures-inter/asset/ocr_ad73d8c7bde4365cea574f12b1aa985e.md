```
```cpp
cout << "Line 1: listA elements: ";                    //Line 1

    //Output the elements of listA using
    //the function printArray
printArray(listA, ARRAY_SIZE);                          //Line 2
cout << endl;                                           //Line 3

    //Initialize listB using the function
    //initializeArray
initializeArray(listB, ARRAY_SIZE);                     //Line 4

cout << "Line 5: listB elements: ";                     //Line 5

    //Output the elements of listB
printArray(listB, ARRAY_SIZE);                          //Line 6
cout << endl << endl;                                   //Line 7

cout << "Line 8: Enter " << ARRAY_SIZE
     << " integers: ";                                  //Line 8

    //Input data into listA using the
    //function fillArray
fillArray(listA, ARRAY_SIZE);                           //Line 9
cout << endl;                                           //Line 10

cout << "Line 11: After filling listA, "
     << "the elements are:" << endl;                    //Line 11

    //Output the elements of listA
printArray(listA, ARRAY_SIZE);                          //Line 12
cout << endl << endl;                                   //Line 13

    //Find and output the sum of the elements
    //of listA
cout << "Line 14: The sum of the elements of "
     << "listA is: "
     << sumArray(listA, ARRAY_SIZE) << endl             //Line 14
     << endl;

    //Find and output the position of the largest
    //element in listA
cout << "Line 15: The position of the largest "
     << "element in listA is: "
     << indexLargestElement(listA, ARRAY_SIZE)
     << endl;                                           //Line 15

    //Find and output the largest element
    //in listA
cout << "Line 16: The largest element in "
     << "listA is: "
     << listA[indexLargestElement(listA, ARRAY_SIZE)]
     << endl << endl;                                   //Line 16
```
```