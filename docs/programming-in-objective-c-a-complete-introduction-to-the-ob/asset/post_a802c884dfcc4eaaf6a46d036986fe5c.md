
# Arrays 249

sequences through the first 100 elements of the array grades (elements 0-99) adds the value of each grade into sum. When the loop is finished, the variable sum contains the total of the first 100 values of the grades array (assuming that sum was set to 0 before the loop was entered).

As with other types of variables, you must declare arrays before you can use them. Declaring an array involves declaring the type of element that will be contained in the array, such as int, float, or an object, as well as the maximum number of elements that will be stored inside the array.

The definition

```
fracts [100];
```

defines fracts to be an array containing 100 fractions. You can make valid references to this array by using subscripts 0-99.

The expression

```
fracts[2] = fracts[0] add: fracts[1];
```

invokes Fraction's method: to add the first two fractions from the fract array and stores the result in the third location of array.

Program 13.1 generates a table of the first 15 Fibonacci numbers. Try to predict its output. What relationship exists between each number in the table?

# Program 13.1

```
// Program to generate the first 15 Fibonacci numbers
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc] init];
    Fibonacci[0] = 0; /* by definition */
    Fibonacci[1] = 1; /* dito */

    for (int i = 2; i < 15; ++i) {
        Fibonacci[i] = Fibonacci[i-2] + Fibonacci[i-1];
    }

    NSLog("@%d", Fibonacci[i]);
    [pool drain];
    return 0;
}
```

# Program 13.1 Output

```
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

The two Fibonacci numbers, which we call $F0$ and $F1$, are defined to be 0 and 1, respectively. Thereafter, each successive Fibonacci number $Fi$ is defined to be the sum of the preceding Fibonacci numbers $Fi-2$ and $Fi-1$. So $F2$ is calculated by adding the values of $F0$ and $F1$. In the preceding program, this corresponds directly to calculating Fibonacci $[2]$ and Fibonacci $[1]$. This calculation is performed inside the *for* loop, which calculates the values of $F2-F14$ (or, equivalently, Fibonacci $[2]$ through Fibonacci $[14]$).# Initializing Array Elements

Just as you can assign initial values to variables when they are declared, you can assign initial values to the elements of an *array*. This is done by simply listing the initial values of the array, starting from the first element. Values in the list are separated by commas, and the entire list is enclosed in a pair of brackets.

The statement

```
int integers[5] = { 0, 1, 2, 3, 4 };
```

sets the value of *integers[0]* to 0, *integers[1]* to 1, *integers[2]* to 2, and so on.
Arrays of characters are initialized in a similar manner; thus the statement

```
char letters[5] = { 'a', 'b', 'c', 'd', 'e' };
```

defines the array and initializes the five elements to the characters 'a', 'b', 'c', 'd', and 'e', respectively.
You don't have to completely initialize an entire array. If fewer initial values are specified, only an equal number of elements are initialized; the remaining values in the array are set to zero. Thus the declaration

```
float sample_data[5] = { 100.0, 300.0, 500.5 };
```

initializes the first three values of *sample_data* to 100.0, 300.0, and 500.5 and sets the remaining 7 elements to 0.

By enclosing an element number in pair of brackets, you can initialize specific array elements in any order. For example:

```
int x = 1233;
int a[] = { [9] = x + 1, [2] = 3, [1] = 2, [0] = 1 };
```

defines a 10-element array called a (based on the highest index in the array) and initializes the element to the value of x + 1 (1234). In addition, it initializes the first three elements to 1, 2, and 3, respectively.# Character Arrays

Program 13.2 illustrates how you can use a character array. However, one point is worthy of discussion. Can you spot it?

Program 13.2

```
#import <Foundation/Foundation.h>
int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc] init];
    char word[] = { 'H', 'e', 'l', 'l', 'o', '!' };
    int i;

    for ( i = 0; i < 6; ++i ) {
        NSLog("@%c", word[i]);
    }
    [pool drain];
    return 0;
}
```

Program 13.2 Output
```
H
e
l
l
o
!
```

In this case, the size of the array is determined automatically based on the number of elements. Because Program 13.2 has six values listed for the array, Objective-C language implicitly dimensions the array to six elements. This approach works fine as long as you initialize every element in the array. If this is not to the case, you must explicitly dimension the array. If you put a terminating null ('\0') at the end of character array, you create what is often called character string. If you substitute the initialization of word in Program 13.2 with

```
char word[] = { 'H', 'e', 'l', 'l', 'o', '!', '\0' };
```

you could have displayed the string with a single NSLog call, like this:

```
NSLog("@%s", word);
```

This works because NSLog tells to keep displaying characters until a terminating null character you put at the end of your array.# Multidimensional Arrays

The types of arrays you've seen thus far are all linear arrays—that is, they all deal with a single dimension. The language enables you to define arrays of any dimension. This section takes a look at two-dimensional arrays. One of the most natural applications for two-dimensional array arises in the case of a matrix. Consider 4 × 5 matrix shown here:

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | 10 | 5 | -3 | 17 | 82 |
| 1 | 9 | 0 | 0 | 8 | -7 |
| 2 | 32 | 20 | 1 | 0 | 14 |
| 3 | 0 | 0 | 8 | 7 | 6 |

In mathematics, an element of a matrix commonly referred to by using a double subscript. If the preceding matrix were M, the notation $M_{ij}$ would refer to the element in the $i$-th row, $j$-th column, where $i$ ranges from 1 through 4 and $j$ ranges from 1 through 5. The notation $M_{1,2}$ would refer to the value 20, which is found in the third row, second column of the matrix. In a similar fashion, $M_{4,5}$ would refer to the element contained in the fourth row, fifth column (the value 6). In Objective-C, an analogous notation is used when referring to elements of a two-dimensional array. However, because Objective-C likes to start numbering at 0, the first row of the matrix is actually 0 and the first column of the matrix is 0. The preceding matrix would then have row and column designations as shown in the following:

| Row (i) \ Column (j) | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | 10 | 5 | -3 | 17 | 82 |
| 1 | 9 | 0 | 0 | 8 | -7 |
| 2 | 32 | 20 | 1 | 0 | 14 |
| 3 | 0 | 0 | 8 | 7 | 6 |

Whereas in mathematics the notation $M_{i,j}$ is used, Objective-C the equivalent notation is as follows:

M[i][j]

Remember, the first index number refers to the row number, whereas the second index number references the column. Therefore, the statement

```
sum = M[0][2] + M[2][4];
```

adds the value contained in row 0, column 2 (which is -3) to the value contained in row 2, column 4 (which is 14) and assigns the result of 11 to the variable sum. Two-dimensional arrays are declared the same way that one-dimensional arrays; thus,

```
int M[4][5];
```

declares array M to be a two-dimensional array consisting of 4 rows and 5 columns, for a total of 20 elements. Two-dimensional arrays are initialized in a manner analogous to their one-dimensional counterparts. When listing elements for initialization, the values are listed by row. Brace pairs are used to separate the list of initializers for one row from the next. Thus, to define and initialize the array M to the elements in the preceding table, you can use a statement such as the following:

```
int M[4][5] = {
{ 10, 5, -3, 17, 82 },
{ 9, 0, 0, 8, -7 },
{ 32, 20, 1, 0, 14 },
{ 0, 0, 8, 7, 6 };
};
```

Pay particular attention to the syntax of the previous statement. Note that commas are required after each brace closes a row, except in the case of the last row. The use of the inner pairs of braces is actually optional. If they aren't supplied, initialization proceeds by row. Therefore, the previous statement could have been written as follows:

```
int M[4][5] = { 10, 5, -3, 17, 82, 9, 0, 0, 8, -7, 32,
20, 1, 0, 14, 0, 8, 7, 6 };
```

With one-dimensional arrays, the entire array may need to be initialized. A statement such as the following initializes only the first three elements of each row of the matrix to the indicated values:

```
int M[4][5] = {
{ 10, 5, -3 },
{ 9, 0, 0 },
{ 32, 20, 1 },
{ 0, 0, 8 };
};
```
