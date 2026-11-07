This statement creates an array intArray of nine components. Here, intArray[0] = 5, intArray[1] = 6, and so on.

The statement:

```
```
vector<int> vecList(9);
```
```

creates an empty container of nine components of type vector, and the element type is int.

Recall that the array name, intArray, is, in fact, a pointer and contains the base address of the array. Therefore, intArray points to the first component of the array, intArray + 1 points to the second component of the array, and so on.

Consider the statement:

```
```
copy(intArray, intArray + 9, vecList.begin());
```
```

This statement copies the elements starting at the location intArray—which is the first component of the array intArray, until intArray + 9 - 1 (that is, intArray + 8), which is the last element of the array intArray—into the container vecList. (Note that here first1 is intArray, last is intArray + 9, and first2 is vecList.begin().) After the previous statement executes:

```
```
vecList = {5, 6, 8, 3, 40, 36, 98, 29, 75}
```
```

Now consider the statement:

```
```
copy(intArray + 1, intArray + 9, intArray);
```
```

Here, first1 is intArray + 1; that is, first1 points to the location of the second element of the array intArray, and last is intArray + 9. Also, first2 is intArray, that is, first2 points to the location of the first element of the array intArray. Therefore, the second array element is copied into the first array component, the third array element into the second array component, and so on. After the preceding statement executes:

```
```
intArray[] = {6, 8, 3, 40, 36, 98, 29, 75, 75}
```
```

Clearly, the elements of the array intArray are shifted to the left by one position.

Now consider the statement:

```
```
copy(vecList.rbegin() + 2, vecList.rend(), vecList.rbegin());
```
```

Recall that the function rbegin, reverse begin, returns a pointer to the last element in a container, and this function is used to process the elements of a container in reverse. Therefore, vecList.rbegin() + 2 returns a pointer to the third to the last element in the container vecList. The function rend, reverse end, returns a pointer to the position before the first element in a container. The previous statement shifts the elements of the container vecList to the right by two positions. After the previous statement executes, the container vecList is: