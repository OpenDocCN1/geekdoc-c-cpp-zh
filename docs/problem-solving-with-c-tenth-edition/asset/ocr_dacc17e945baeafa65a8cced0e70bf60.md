Create a menu that allows the administrator to simulate the transmission of information by manually typing in the login or logoff data. Whenever someone logs in or out, the display should be updated. Also write a search option so that the administrator can type in a user ID and the system will output what lab and station number that user is logged into, or “None” if the user ID is not logged into any computer station.

You should use a fixed array of length 4 for the labs. Each array entry points to a dynamic array that stores the user login information for each respective computer station.

The structure is shown in the figure below. This structure is sometimes called a ragged array since the columns are of unequal length.

![](bbox=[0.22, 0.38, 0.88, 0.52])

6. One problem with dynamic arrays is that once the array is created using the new operator, the size cannot be changed. For example, you might want to add or delete entries from the array as you can with a vector. This project asks you to create functions that use dynamic arrays to emulate the behavior of a vector.

First, write a program that creates a dynamic array of five strings. Store five names of your choice into the dynamic array. Next, complete the following two functions:

```
string* addEntry(string *dynamicArray, int &size, string newEntry);
```

This function should create a new dynamic array one element larger than dynamicArray, copy all elements from dynamicArray into the new array, add the new entry onto the end of the new array, increment size, delete dynamicArray, and return the new dynamic array.

```
string* deleteEntry(string *dynamicArray, int &size, string entryToDelete);
```

This function should search dynamicArray for entryToDelete. If not found, the request should be ignored and the unmodified dynamicArray