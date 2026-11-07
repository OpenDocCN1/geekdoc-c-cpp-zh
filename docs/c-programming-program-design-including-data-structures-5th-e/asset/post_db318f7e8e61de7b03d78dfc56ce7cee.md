
## Arrays of Strings

Suppose that you need to perform an operation, such as alphabetizing a list of names. Because every name is a string, a convenient way to store the list of names is to use an array. Strings in C++ can be manipulated using either the data type `string` or character arrays (C-strings). Also, on some compilers, the data type `string` may not be available in Standard C++ (that is, non-ANSI/ISO Standard C++). This section illustrates both ways to manipulate a list of strings.

### Arrays of Strings and the `string` Type

Processing a list of strings using the data type `string` is straightforward. Suppose that the list consists of a maximum of 100 names. You can declare an array of 100 components of type `string` as follows:

```cpp
string list[100];
```

Basic operations, such as assignment, comparison, and input/output, can be performed on values of the string type. Therefore, the data in `list` can be processed just like any one-dimensional array discussed in the first part of this chapter.

### Arrays of Strings and C-Strings (Character Arrays)

Suppose that the largest string (for example, name) in your list is 15 characters long and your list has 100 strings. You can declare a two-dimensional array of characters of 100 rows and 16 columns as follows (see Figure 9-16):

```cpp
char list[100][16];
```

![](img/f97f778697507bb6fdd80c5991210cba_571_0.png)

**FIGURE 9-16**  Array list of strings

If you know the size of the tables with which the program will be working, then you can use `typedef` to first define a two-dimensional array data type and then declare variables of that type.

For example, consider the following:

```cpp
const int NUMBER_OF_ROWS = 20;
const int NUMBER_OF_COLUMNS = 10;

typedef int tableType[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];
```

The previous statement defines a two-dimensional array data type `tableType`. Now we can declare variables of this type. So:

```cpp
tableType matrix;
```

declares a two-dimensional array `matrix` of 20 rows and 10 columns.

You can also use this data type when declaring formal parameters, as shown in the following code:

```cpp
void initialize(tableType table)
{
    int row;
    int col;

    for (row = 0; row < NUMBER_OF_ROWS; row++)
        for (col = 0; col < NUMBER_OF_COLUMNS; col++)
            table[row][col] = 0;
}
```

This function takes as an argument any variable of type `tableType`, which is a two-dimensional array, and initializes the array to 0.

By first defining a data type, you do not need to keep checking the exact number of columns when you declare a two-dimensional array as a variable or formal parameter, or when you pass an array as a parameter during a function call.

## Multidimensional Arrays

In this chapter, we defined an array as a collection of a fixed number of elements (called components) of the same type. A one-dimensional array is an array in which the elements are arranged in a list form; in a two-dimensional array, the elements are arranged in a table form. We can also define three-dimensional or larger arrays. In C++, there is no limit on the dimension of arrays. Following is the general definition of an array.

*n*-dimensional array: A collection of a fixed number of elements (called components) arranged in *n* dimensions (*n* ≥ 1).

The general syntax for declaring an n-dimensional array is:

```cpp
dataType arrayName[intExp1][intExp2] ... [intExpn];
```

where intExp1, intExp2, . . . , and intExpn are constant expressions yielding positive integer values.

The syntax to access a component of an n-dimensional array is:

```cpp
arrayName[indexExp1][indexExp2] ... [indexExpn]
```

where indexExp1, indexExp2, . . . , and indexExpn are expressions yielding nonnegative integer values. indexExp_i gives the position of the array component in the i-th dimension.

For example, the statement:

```cpp
double carDealers[10][5][7];
```

declares carDealers to be a three-dimensional array. The size of the first dimension is 10, the size of the second dimension is 5, and the size of the third dimension is 7. The first dimension ranges from 0 to 9, the second dimension ranges from 0 to 4, and the third dimension ranges from 0 to 6. The base address of the array carDealers is the address of the first array component—that is, the address of carDealers[0][0][0]. The total number of components in the array carDealers is 10 * 5 * 7 = 350.

The statement:

```cpp
carDealers[5][3][2] = 15564.75;
```

sets the value of the component carDealers[5][3][2] to 15564.75.

You can use loops to process multidimensional arrays. For example, the nested for loops:

```cpp
for (i = 0; i < 10; i++)
    for (j = 0; j < 5; j++)
        for (k = 0; k < 7; k++)
            carDealers[i][j][k] = 0.0;
```

initialize the entire array to 0.0.

When declaring a multidimensional array as a formal parameter in a function, you can omit the size of the first dimension but not the other dimensions. As parameters, multidimensional arrays are passed by reference only, and a function cannot return a value of the array type. There is no check to determine whether the array indices are within bounds.

## PROGRAMMING EXAMPLE: Code Detection

When a message is transmitted in secret code over a transmission channel, it is usually sent as a sequence of bits, that is, 0s and 1s. Due to noise in the transmission channel, the transmitted message may become corrupted. That is, the message received at the destination is not the same as the message transmitted; some of the bits may have been changed. There are several techniques to check the validity of the transmitted message at the destination. One technique is to transmit the same message twice. At the destination, both copies of the message are compared bit by bit. If the corresponding bits are the same, the message received is error-free.

Let’s write a program to check whether the message received at the destination is error-free. For simplicity, assume that the secret code representing the message is a sequence of digits (0 to 9) and the maximum length of the message is 250 digits. Also, the first number in the message is the length of the message. For example, if the secret code is:

```cpp
7 9 2 7 8 3 5 6
```

then the actual message is 7 digits long, and it is transmitted twice.

The above message is transmitted as:

```cpp
7 9 2 7 8 3 5 6 7 9 2 7 8 3 5 6
```

**Input**  A file containing the secret code and its copy

**Output**  The secret code, its copy, and a message—if the received code is error-free—in the following form:

| Code | Digit | Code | Digit Copy |
|:---|---:|:---|---:|
|  | 9 |  | 9 |
|  | 2 |  | 2 |
|  | 7 |  | 7 |
|  | 8 |  | 8 |
|  | 3 |  | 3 |
|  | 5 |  | 5 |
|  | 6 |  | 6 |

Message transmitted OK.

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

Because we have to compare the corresponding digits of the secret code and its copy, we first read the secret code and store it in an array. Then we read the first digit of the copy and compare it with the first digit of the secret code, and so on. If any of the corresponding digits are not the same, we indicate this fact by printing a message next to the digits. Because the maximum length of the message is 250, we use an array of 250 components. The first number in the secret code, and in the copy of the secret code, indicates the length of the code. This discussion translates into the following algorithm:

- 1. Open the input and output files.
- 2. If the input file does not exist, exit the program.
- 3. Read the length of the secret code.
- 4. If the length of the secret code is greater than 250, terminate the program because the maximum length of the code in this program is 250.
- 5. Read and store the secret code into an array.
- 6. Read the length of the copy.
- 7. If the length of the secret code and its copy are the same, compare the codes. Otherwise, print an error message.

To simplify the function `main`, let us write a function, `readCode`, to read the secret code and another function, `compareCode`, to compare the codes.

**`readCode`**

This function first reads the length of the secret code. If the length of the secret code is greater than 250, a `bool` variable `lenCodeOk`, which is a reference parameter, is set to `false` and the function terminates. The value of `lenCodeOk` is passed to the calling function to indicate whether the secret code was read successfully. If the length of the code is less than 250, the `readCode` function reads and stores the secret code into an array. Because the input is stored into a file and the file was opened in the function `main`, the input stream variable corresponding to the input file must be passed as a parameter to this function. Furthermore, after reading the length of the secret code and the code itself, the `readCode` function must pass these values to the function `main`. Therefore, this function has four parameters: an input file stream variable, an array to store the secret code, the length of the code, and the `bool` parameter `lenCodeOk`. The definition of the function `readCode` is as follows:

```cpp
void readCode(ifstream& infile, int list[], int& length,
              bool& lenCodeOk)
{
    int count;

    lenCodeOk = true;

    infile >> length;  //get the length of the secret code

    if (length > MAX_CODE_SIZE)
    {
        lenCodeOk = false;
        return;
    }

    //Get the secret code.
    for (count = 0; count < length; count++)
        infile >> list[count];
}
```
