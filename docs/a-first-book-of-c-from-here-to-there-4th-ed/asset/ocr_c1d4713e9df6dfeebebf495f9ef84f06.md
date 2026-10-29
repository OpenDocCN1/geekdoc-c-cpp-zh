to it, but simply removes the storage the address references. Following is a sample run of Program 8.8:

```
Enter the number of grades to be processed: 4
Enter a grade: 85
Enter a grade: 96
Enter a grade: 77
Enter a grade: 92

An array was created for 4 integers
The values stored in the array are:
85
96
77
92
```

# EXERCISES 8.2

+   1. (Practice) Replace each of the following references to a subscripted variable with a pointer reference:
+   a. prices[5]    b. grades[2]    c. yield[10]
+   d. dist[9]      e. mile[0]      f. temp[20]
+   g. celsius[16]  h. num[50]      i. time[12]

+   2. (Practice) Replace each of the following pointer references with a subscript reference:
+   a. *(message + 6)    b. *amount    c. *(yrs + 10)
+   d. *(stocks + 2)     e. *(rates + 15)    f. *(codes + 19)

+   3. (Practice) a. List three things the declaration statement double prices[5]; causes the compiler to do.
+   b. If each double-precision number uses 8 bytes of storage, how much storage is set aside for the prices array?
+   c. Draw a diagram similar to Figure 8.16 for the prices array.
+   d. Determine the byte offset in relation to the start of the prices array, corresponding to the offset in the expression *(prices + 3).

+   4. (Practice) a. Write a declaration to store the string "This is a sample" in an array named samtest. Include the declaration in a program that displays the values in samtest by using a for loop that uses a pointer access to each element in the array.
+   b. Modify the program written in Exercise 4a to display only array elements 10 through 15 (the letters s, a, m, p, l, and e).