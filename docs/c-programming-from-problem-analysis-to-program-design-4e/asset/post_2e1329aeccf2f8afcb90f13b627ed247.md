
- 16. The `Queue` class represents a First In First Out (FIFO) collection of objects. The `Enqueue()` method adds an object to the end of the queue. `Dequeue()` removes and returns the object at the beginning of the queue.

- 17. The `Stack` class represents a simple last-in-first-out (LIFO) collection of objects. The `Push()` method adds an object to the end of the stack. `Pop()` removes and returns the object at the beginning of the stack.

## EXERCISES

- 1. When three values are contained within the square brackets, the last number represents the number of:

  a. classes
  b. rows
  c. planes
  d. columns
  e. none of the above

- 2. Which of the following array declarations would enable you to store the high and low temperatures for each day of one full week?

  a. `int temp1Lo, temp2Lo, temp3Lo, temp4Lo, temp5Lo, temp6Lo, temp7Lo, temp1Hi, temp2Hi, temp3Hi, temp4Hi, temp5Hi, temp6Hi, temp7Hi;`
  b. `int temp [ 7, 2] = new int [ 7, 2] ;`
  c. `int [ , ] temp = new int [ 7, 2] ;`
  d. `int [ , ] temp = new int [ 7, 2] ;`
  e. `int [ , ] temp = new int [ 8, 3] ;`

- 3. Assume a two-dimensional array called `num` is declared to hold four rows and seven columns. Which of the following statements correctly assigns the value 100 to the third physical column of each row?

  a. `for (x = 0; x < 3; ++x) num[ x, 2] = 100;`
  b. `for (x = 0; x < 4; ++x) num[ x, 2] = 100;`
  c. `for (x = 1; x < 4; ++x) num[ x, 2] = 100;`
  d. `for (x = 1; x < 5; ++x) num[ x, 2] = 100;`
  e. none of the above

- 4. Choose the statement that does not apply to the following declaration:

```
double [ , ] totalCostOfItems = {{109.95, 169.95, 1.50, 89.95},{27.9, 18.6, 26.8, 98.5}};
```

  a. declares a two-dimensional array of floating-point values
  b. establishes the maximum number of rows as 4
  c. sets the array element totalCostOfItems[0, 1] to 169.95
  d. declares an area in memory where data of double type can be stored
  e. all are correct

- 5. What value is returned by the method named result?

```
int result(int [ , ] anArray)
{
    int j = 0;
    int i = 0;
    for (int r = 0; r < anArray.GetLength(0); r++)
        for (int c = 0; c < anArray.GetLength(1); c++)
            if (anArray[r, c] < anArray[i, j])
            {
                i = r;
                j = c;
            }
    return i;
}
```

  a. the row index of the largest element of array anArray
  b. the value of the largest element of array anArray
  c. the row index of the smallest element of array anArray
  d. the column index of the smallest element of array anArray
  e. the index of the last element greater than its predecessor

- 6. What is the largest dimension an array can be declared to store values?

  a. 10
  b. 100
  c. 3
  d. 5
  e. there is no limit

- 7. Using the following declaration:

```
char [ , ] n = {{'a', 'b', 'c', 'd', 'e'},
              {'f', 'g', 'h', 'i', 'j'}};
```

What does n[1, 1] refer to?

  a. a
  b. f
  c. b
  d. g
  e. none of the above

- 8. A two-dimensional array is a list of data items that __________.

  a. all have the same type
  b. all have different names
  c. all are integers
  d. all are originally set to null ('\0')
  e. none of the above

- 9. Using the following declaration:

```
int [ , ] x = {{12, 13, 14, 15}, {16, 17, 18, 19}};
```

What does x[2, 4] refer to?

  a. 19
  b. 18
  c. '\0'
  d. 0
  e. none of the above

- 10. Which of the following adds 95 to the array element that is currently storing 14?

```
int [ , ] x = {{12, 13}, {14, 15}, {16, 17}, {18, 19}};
```

  a. x[2] += 95;
  b. x[1, 0] += 95;
  c. x[1, 0 += 95];
  d. x = 14 + 95;
  e. none of the above

- 11. How many components are allocated by the following statement?

```
double [ , ] values = new double [ 3, 2 ] ;
```

  a. 32
  b. 3
  c. 5
  d. 6
  e. none of the above

- 12. Given the declaration for values in number 11 above, how would you store 0 in the last physical location?

  a. values = 0;
  b. values[6] = 0;
  c. values[3, 2] = 0;
  d. values[2, 1] = 0;
  e. none of the above

- 13. If you declare an array as int [ , ] anArray = new int [ 5, 3 ] ; you can double the value stored in anArray[2, 1] with the statement:

  a. anArray[2, 1] = anArray[5, 1] * 2;
  b. anArray = anArray * 2;
  c. anArray[2, 1] *= anArray[2, 1] * 2;
  d. anArray[2, 1] *= 2;
  e. none of the above

- 14. With the following declaration:

```
int [ , ] points = {{300, 100, 200, 400, 600}, {550, 700, 900, 800, 100}};
```

The statement points[1, 3] = points[1, 3] + 10; will

  a. replace the 300 amount with 310 and 900 with 910
  b. replace the 500 amount with 510
  c. replace the 900 amount with 910
  d. replace the 800 amount with 810
  e. none of the above

- 15. With the following declaration:

```csharp
int[,] points = {{300, 100, 200, 400, 600},
                 {550, 700, 900, 200, 100}};
```

The statement `points[0, 4] = points[0, 4-2];` will

  a. replace the 400 amount with 2
  b. replace the 300 and 600 with 2
  c. replace the 600 with 200
  d. result in an error
  e. none of the above

- 16. With the following declaration:

```csharp
int[,] points = {{300, 100, 200, 400, 600},
                 {550, 700, 900, 200, 100}};
```

The statement `Console.Write(points[1, 2] + points[0, 3]);` will

  a. display 900400
  b. display 1300
  c. display "points[1, 2] + points[0, 3]"
  d. result in an error
  e. none of the above

- 17. When you pass an element from an `ArrayList` to a method, the method receives:

  a. a copy of the `ArrayList`
  b. the address of the `ArrayList`
  c. a copy of the value in the element of the `ArrayList`
  d. the address of the element in the `ArrayList`
  e. none of the above

- 18. When you pass the entire `ArrayList` to a method, the method receives:

  a. a copy of the `ArrayList`
  b. the address of the `ArrayList`
  c. a copy of the first value in the `ArrayList`
  d. the address of each of the elements in the `ArrayList`
  e. none of the above

- 19. To convert all the uppercase letters in a `string` to their lowercase counterpart, you can use the ______ method of the `string` class.

  a. `IsLower()`
  b. `ConvertLower()`
  c. `Lower()`
  d. `ToLower()`
  e. none of the above

- 20. Which method in the `ArrayList` class can be used to place a value onto the end of the `ArrayList`?

  a. `AddLast()`
  b. `AddLastIndex()`
  c. `Add()`
  d. `Insert()`
  e. none of the above

- 21. Which method in the `ArrayList` class can be used to get or set the number of elements that an `ArrayList` can contain?

  a. `Length()`
  b. `Size()`
  c. `Dimension()`
  d. `Rank()`
  e. `Capacity()`

- 22. Which class includes methods to create a dynamic one-dimensional structure?

  a. `Array`
  b. `string`
  c. `array`
  d. `ArrayList`
  e. all of the above

- 23. A correct method call to a method that has the following heading would be:

`int result(int[ ] anArray, int num)`

  a. `Console.Write(result(anArray, 3));`
  b. `result(anArray, 30);`
  c. `Console.Write(result(anArray[ ], 3));`
  d. `result(anArray[ ], 30);`
  e. none of the above

- 24. With two-dimensional arrays a limitation on the `foreach` statement is that it can:

  a. only be used for read-only access
  b. only be used with integral type arrays
  c. not be used with multidimensional arrays
  d. only be used with arrays smaller than 1000 elements
  e. not be used with dynamic arrays

- 25. In order to retrieve a value stored in an object of the `Queue` class, you would use which method?

  a. Pop( );
  b. Push( );
  c. Dequeue( );
  d. Enqueue( );
  e. none of the above

- 26. Use the following string to answer questions a through c.

```
string sValue = "Today is the first day of "
               + "the rest of your life.";
```

  a. Create a new string that has all lowercase characters except the word
  day. Day should be all uppercase.
  b. Create a new string array that contains the eight elements. Each word
  from the sValue string should be in a separate array cell.
  c. Remove the period from the last array element created in Step b. Display
  the contents of the new array verifying its removal.
  d. Surround the sValue string with three asterisks on each end.
  e. Replace the word first with the word best in the sValue string.

- 27. Using the following declaration:

```
int [ , ] anArray = {{34, 55, 67, 89, 99}, {22, 68, 11, 19, 45}};
```

What would be the result of each of the following output statements?

  a. Console.WriteLine(anArray.Length);
  b. Console.WriteLine(anArray[1, 2]);
  c. Console.WriteLine(anArray[0, anArray.GetLength(0) - 2]);
  d. Console.WriteLine(anArray[0, 2 + 1] * anArray[0, 0]);
  e. Console.WriteLine(anArray.Rank);
