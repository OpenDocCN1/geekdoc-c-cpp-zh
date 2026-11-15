A memory snapshot of s and t is given below:

```
double s   0.5  0.0  -0.1  0.2  0.15  0.2  <-- data values
               [0]  [1]  [2]  [3]  [4]  [5]  <-- offsets
int t      0   1   2   3   <-- data values
               [0][1][2][3]   <-- offsets
```

The size of an array must be specified in the declaration statement, using either a constant within brackets or by an initialization list.

![](bbox=[0.145, 0.225, 0.205, 0.265])

# Statement Box 7.1

Array Declaration Statements: The declaration of a one-dimensional array allocates a consecutive block of memory addresses, and the name of the array holds the first address in the block. The array name and an offset are used to access individual values, thus the data type of each value must be the same.

```
Syntax:
data type identifier[size] [= initialization list];
```

```
Example:
int data[5]; //allocates consecutive memory for 5 integer values
Memory diagram: data [?][?][?][?][?]
Offsets: 0 1 2 3 4

char vowels[5] = {'a', 'e', 'i', 'o', 'u'}; //allocates and
initializes
Memory diagram: vowels ['a'|'e'|'i'|'o'|'u']
Offsets: 0 1 2 3 4

double t[100] = (0.0); //allocates and initialized all values to 0.0
Memory diagram: t [0|0|0|0|...|0]
Offsets: 0 1 2 ... 99
```

```
Valid References:
cout << vowels[0];
cout << t[2];
```

```
Invalid References:
cout << vowel[5]; //invalid offset.
cout << t[-1]; //invalid offset
```

Arrays can also be assigned values after they have been declared. For example, suppose that we want to fill a double array g with the values 0.0, 0.5, 1.0, 1.5, ..., 10.0. Because there are 21 different values, listing the values in an initialization list would be tedious, but assigning the values to the array within a for loop is very easy, as illustrated in program chapter7_1.