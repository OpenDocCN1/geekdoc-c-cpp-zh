```
```text
Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the vectors contain:
integers1:
   1       2       3       4
   5       6       7
integers2:
   8       9      10      11
  12      13      14      15
  16      17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of vector integers3 is 7
vector after initialization:
   1       2       3       4
   5       6       7

Assigning integers2 to integers1:
integers1:
   8       9      10      11
  12      13      14      15
  16      17
integers2:
   8       9      10      11
  12      13      14      15
  16      17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
   8       9      10      11
  12    1000      14      15
  16      17

Attempt to display integers1.at( 15 )
An exception occurred: invalid vector<T> subscript
```
```

Fig. 15.14 | Demonstrating C++ Standard Library class template vector. (Part 4 of 4.)

# ### Creating vector Objects

Lines 13–14 create two vector objects that store values of type int—integers1 contains seven elements, and integers2 has 10 elements. By default, all the elements of each vector object are set to 0. Note that vectors can be defined to store any data type, by replacing int in vector<int> with the appropriate data type. This notation, which specifies the type stored in the vector, is similar to the template notation that Section 15.13 introduced with function templates.

# ### vector Member Function size; Function outputVector

Line 17 uses vector member function size to obtain the size (i.e., the number of elements) of integers1. To invoke a member function, you access it with the dot (.) operator, just as