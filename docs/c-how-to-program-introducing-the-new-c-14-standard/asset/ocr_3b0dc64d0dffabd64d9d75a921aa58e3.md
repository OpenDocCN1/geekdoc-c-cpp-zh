```
```cpp
// modify and output contents of array1
for (size_t j{0}; j < array1.size(); ++j) {
   cout << "array1[" << j << "] = " << (array1[j] += 5) << " ";
}
}

// function to demonstrate an automatic local array
void automaticArrayInit(void) {
   // initializes elements each time function is called
   array<int, arraySize> array2{1, 2, 3}; // automatic local array

   cout << "\n\nValues on entering automaticArrayInit:\n";

   // output contents of array2
   for (size_t i{0}; i < array2.size(); ++i) {
      cout << "array2[" << i << "] = " << array2[i] << " ";
   }

   cout << "\n\nValues on exiting automaticArrayInit:\n";

   // modify and output contents of array2
   for (size_t j{0}; j < array2.size(); ++j) {
      cout << "array2[" << j << "] = " << (array2[j] += 5) << " ";
   }
}
```
```

```
```
First call to each function:

Values on entering staticArrayInit:
array1[0] = 0  array1[1] = 0  array1[2] = 0
Values on exiting staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8

Second call to each function:

Values on entering staticArrayInit:
array1[0] = 5  array1[1] = 5  array1[2] = 5
Values on exiting staticArrayInit:
array1[0] = 10  array1[1] = 10  array1[2] = 10

Values on entering automaticArrayInit:
array2[0] = 1  array2[1] = 2  array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6  array2[1] = 7  array2[2] = 8
```
```

Fig. 7.10 *static array* initialization and automatic *array*