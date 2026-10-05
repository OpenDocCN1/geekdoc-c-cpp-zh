
## CHAPTER 5 Arrays

Display 5.10 The Two-Dimensional array grade

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_253_0.png)

| | grade [0] [0] | grade [0] [1] | grade [0] [2] |
|---|---|---|---|
| student 1 | | | | |
| student 2 | grade [1] [0] | grade [1] [1] | grade [1] [2] |
| student 3 | grade [2] [0] | grade [2] [1] | grade [2] [2] |
| student 4 | grade [3] [0] | grade [3] [1] | grade [3] [2] |

grade [3] [0] is the grade that student 4 received on quiz 1. grade [3] [1] is the grade that student 4 received on quiz 2. grade [3] [2] is the grade that student 4 received on quiz 3.

Display 5.11 The Two-Dimensional array grade

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_253_1.png)

| | 10 | 10 | 10 | | |
|---|---|---|---|---|
| student 1 | | | | stAve [0] |
| student 2 | 2 | 0 | 1 | 1.0 stAve [1] |
| student 3 | 8 | 6 | 9 | 7.7 stAve [2] |
| student 4 | 8 | 4 | 10 | 7.3 stAve [3] |

quizAve 7.0 5.0 7.5

## Self-Test Exercises

20. What is the output produced by the following code?

```
int myArray[4], index1, index2;
for (index1 = 0; index1 < 4; index1++)
  for (index2 = 0; index2 < 4; index2++)
    myArray[index1][index2] = index2;
for (index1 = 0; index1 < 4; index1++)
  for (index2 = 0; index2 < 4; index2++)
    cout << myArray[index1][index2] << " ";
  cout << endl;
```

21. Write code that will fill an array (a declared next) with numbers typed at the keyboard. The numbers will be input five per line, on four lines (although your solution need not depend on how the input numbers are divided into lines).

```
int a[4][5];
```

22. Write a function definition for a void function called echo such that the following call will echo the input described in Self-Test Exercise 21, and will echo it in the same format as we specified for the input (that is, four lines of five numbers per line):

```
echo(a, 4);
```

## Chapter Summary

- An array can be used to store and manipulate a collection of data that is all of the same type.
- The indexed variables of an array can be used just like any other variables of the base type of the array.
- A for loop is a good way to step through the elements of an array and perform some action on each indexed variable.
- The most common programming error made when using arrays is attempting to access a nonexistent array index. Always check the first and last iterations of a loop that manipulates an array to make sure it does not use an index that is illegally small or illegally large.
- An array formal parameter is neither a call-by-value parameter nor a call-by-reference parameter, but a new kind of parameter. An array parameter is similar to a call-by-reference parameter in any change that is made to the formal parameter in the body of the function will be made to the array argument when the function is called.

- The indexed variables for an array are stored next to each other in the computer’s memory so the array occupies a contiguous portion of memory. When the array is passed as an argument to a function, only the address of the first indexed variable (the one numbered :) is given to the calling function. Therefore, a function with an array parameter usually needs another formal parameter of type int to give the size of the array.
- When using a partially filled array, your program needs an additional variable of type int to keep track of how much of the array is used.
- To tell the compiler that an array should not be changed by your function, you can insert the modifier const before the array parameter for argument position. An array parameter that is modified with a const is called a constant array parameter.
- If you need an array with more than one index, you can use a multidimensional array.

## Answers to Self-Test Exercises

1. The statement int a[5]; is a declaration, in which 5 is the number of array elements. The expression a[4] is an access into the array defined by the previous statement. The access is to the element having index 4, which is the fifth (and last) element.

2. a. score
   b. double
   c. 5
   d. 0 through 4

- e. Any of score[0], score[2], score[3], score[4]

3. a. One many initializers
   b. Correct. The array size is 4.
   c. Correct. The array size is 4.

4. abc
   5. 1.1 2.2 3.3
   1.1 3.3 3.3

(Remember that the indexes start with 0, not 1.)

6. 0 2 4 6 8 10 12 14 16 18
   0 4 8 12 16

7. The indexed variables of sampleArray are sampleArray[0] through sampleArray[9], but this piece of code tries to fill sampleArray[1] through sampleArray[10]. The index 10 in sampleArray[10] is out of range.

8. There is an index out of range. When index is equal to 9, index + 1 is equal to 10, so a[index + 1], which is the same as a[10], has an error. To correct the code, change the first line of the loop to:
```
for (int index = 0; index < 9; index++)
```
9. int a[4][5];
   cout << "Enter numbers:\n"
   for (int i = 0; i < 4; i++)
     for (int j = 0; j < 5; j++)
       cin >> a[i][j];
10. The function with an array parameter usually needs another formal parameter of type int to give the size of the array.
11. The following calls are correct:
```
void echo(int a[], int size);
```
The second argument is missing in the call.
12. The correct version is:
```cpp
void echo(int a[], int size) {
  for (int i = 0; i < size; i++) {
    for (int j = 0; j < 5; j++) {
      cout << a[i][j] << " ";
    }
    cout << endl;
  }
}
```
13.
```cpp
void output(int a[], int size);
```
The array parameter is modified with a const is called a constant array parameter.
14. The first of the correct code is:
```cpp
void output(int a[], int size) {
  for (int i = 0; i < size; i++) {
    for (int j = 0; j < 5; j++) {
      cout << a[i][j] << " ";
    }
    cout << endl;
  }
}
```
15.
```cpp
void output(const int a[], int size);
```
16.
```cpp
int outOfOrder(double array[], int size) {
  for (int i = 0; i < size - 1; i++) {
    if (array[i] > array[i+1])
      return 1;
  }
  return -1;
}
```
17.
```cpp
void drop(int a[], int size);
```
18. The array parameter is neither a call-by-value parameter nor a call-by-reference parameter, but a new kind of parameter. An array parameter is similar to a call-by-reference parameter in any change that is made to the formal parameter in the body of the function will be made to the array argument when the function is called.
