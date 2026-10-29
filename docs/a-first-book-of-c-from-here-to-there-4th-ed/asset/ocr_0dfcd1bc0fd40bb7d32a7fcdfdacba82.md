# 7.4 Two-Dimensional Arrays

A two-dimensional array, sometimes referred to as a table, consists of both rows and columns of elements. For example, the following array of numbers is called a two-dimensional array of integers:

8 16 9 52
3 15 27 6
14 25 2 10

This array consists of three rows and four columns and is called a 3-by-4 array. To reserve storage for this array, both the number of rows and the number of columns must be included in the array's declaration. Calling the array val, the following is the correct specification for this two-dimensional array:

```
int val[3][4];
```

Similarly, the declarations

```
double prices[10][5];
char code[6][26];
```

specify that the prices array consists of 10 rows and 5 columns of double-precision numbers, and the code array consists of 6 rows and 26 columns, with each element capable of holding one character.

To locate each element in a two-dimensional array, you use its position in the array. As shown in Figure 7.7, the term val[1][3] uniquely identifies the element in row 1, column 3. As with one-dimensional array variables, two-dimensional array variables can be used anywhere that scalar variables are valid, as shown in these examples using elements of the val array:

```
price = val[2][3];
val[0][0] = 62;
newnum = 4 * (val[1][0] - 5);
sumRow = val[0][0] + val[0][1] + val[0][2] + val[0][3];
```

The last statement causes the values of the four elements in row 0 to be added and the sum to be stored in the scalar variable sumRow.

![](bbox=[0.12, 0.00135, 0.92, 0.00185])

Figure 7.7 Each array element is identified by its row and column position