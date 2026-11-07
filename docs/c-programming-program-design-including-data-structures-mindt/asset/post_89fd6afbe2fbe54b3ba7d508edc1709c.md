
This statement declares `board` to be an array of four pointers wherein each pointer is of type `int`. Because `board[0]`, `board[1]`, `board[2]`, and `board[3]` are pointers, you can now use these pointers to create the rows of `board`. Suppose that each row of `board` has six columns. Then, the following `for` loop creates the rows of `board`.

```cpp
for (int row = 0; row < 4; row++)
    board[row] = new int[6];
```

Note that the expression `new int[6]` creates an array of six components of type `int` and returns the base address of the array. The assignment statement then stores the returned address into `board[row]`. It follows that after the execution of the previous `for` loop, `board` is a two-dimensional array of four rows and six columns.

In the previous `for` loop, if you replace the number 6 with the number 10, then the loop will create a two-dimensional array of four rows and 10 columns. In other words, the number of columns of `board` can be specified during execution. However, the way `board` is declared, the number of rows is fixed. So in reality, `board` is not a true dynamic two-dimensional array.

Next, consider the following statement:

```cpp
int **board;
```

This statement declares `board` to be a pointer to a pointer. In other words, `board` and `*board` are pointers. Now `board` can store the address of a pointer or an array of pointers of type `int`, and `*board` can store the address of an `int` memory space or an array of `int` values.

Suppose that you want `board` to be an array of 10 rows and 15 columns. To accomplish this, first we create an array of 10 pointers of type `int` and assign the address of that array to `board`. The following statement accomplishes this:

```cpp
board = new int* [10];  // create an array of 10 int pointers
```

Because the elements of `board` are `int` pointers, each of them can point to an array of `int` values.

Next, we create the columns of `board`. The following `for` loop accomplishes this:

```cpp
for (int row = 0; row < 10; row++)
    board[row] = new int[15];
```

To access the components of `board`, you can use the array subscripting notation discussed in Chapter 8.

Note that the number of rows and the number of columns of `board` can be specified during program execution. The following program further explains how to create two-dimensional arrays.

![](img/b217c421655b51e7494cf3b89bb5432d_892_0.png)

### EXAMPLE 12-7

```cpp
#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

void fill(int **p, int rowsSize, int columnSize);       //Line 4
void print(int **p, int rowsSize, int columnSize);       //Line 5

int main()                                               //Line 6
{
    int **board;                                         //Line 8

    int rows;                                            //Line 9
    int columns;                                         //Line 10

    cout << "Line 11: Enter the number of rows "
         << "and columns: ";                            //Line 11
    cin >> rows >> columns;                              //Line 12
    cout << endl;                                        //Line 13

            //Create the rows of board
    board = new int* [rows];                              //Line 14

            //Create the columns of board
    for (int row = 0; row < rows; row++)                 //Line 15
        board[row] = new int[columns];                   //Line 16

            //Insert elements into board
    fill(board, rows, columns);                          //Line 17

    cout << "Line 18: Board:" << endl;                   //Line 18

            //Output the elements of board
    print(board, rows, columns);                         //Line 19

    return 0;                                             //Line 20
}                                                        //Line 21

void fill(int **p, int rowsSize, int columnSize)
{
    for (int row = 0; row < rowsSize; row++)
    {
        cout << "Enter " << columnSize << " number(s)"
             << " for row number " << row << ": ";
        for (int col = 0; col < columnSize; col++)
            cin >> p[row][col];
        cout << endl;
    }
}

void print(int **p, int rowSize, int columnSize)
{
    for (int row = 0; row < rowSize; row++)
    {
        for (int col = 0; col < columnSize; col++)
            cout << setw(5) << p[row][col];
        cout << endl;
    }
}
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 11: Enter the number of rows and columns: 3 4

Enter 4 number(s) for row number 0: 1 2 3 4

Enter 4 number(s) for row number 1: 5 6 7 8

Enter 4 number(s) for row number 2: 9 10 11 12

Line 18: Board:
    1    2    3    4
    5    6    7    8
    9   10   11   12
```

The preceding program contains the functions `fill` and `print`. The function `fill` prompts the user to enter the elements of a two-dimensional array of type `int`. The function `print` outputs the elements of a two-dimensional array of type `int`.

For the most part, the preceding output should be clear. Let us look at the statements in the function `main`. The statement in Line 8 declares `board` to be a pointer to a pointer of type `int`. The statements in Lines 9 and 10 declare `int` variables `rows` and `columns`. The statement in Line 11 prompts the user to input the number of rows and number of columns. The statement in Line 12 stores the number of rows in the variable `rows` and the number of columns in the variable `columns`. The statement in Line 14 creates the rows of `board`, and the `for` loop in Lines 15 and 16 creates the columns of `board`. The statement in Line 17 uses the function `fill` to fill the array `board`, and the statement in Line 19 uses the function `print` to output the elements of `board`.

## Shallow versus Deep Copy and Pointers

In an earlier section, we discussed pointer arithmetic and explained that if we are not careful, one pointer might access the data of another (completely unrelated) pointer. This event might result in unsuspected or erroneous results. Here, we discuss another peculiarity of pointers. To facilitate the discussion, we will use diagrams to show pointers and their related memory.

Consider the following statements:

```cpp
int *first;
int *second;

first = new int[10];
```

The first two statements declare `first` and `second` pointer variables of type `int`. The third statement creates an array of 10 components, and the base address of the array is stored into `first` (see Figure 12-8). (Note that `first` together with the arrow indicates that `first` points to the allocated memory.)

![](img/b217c421655b51e7494cf3b89bb5432d_895_0.png)

**FIGURE 12-8**  Pointer `first` and the array to which it points

Suppose that some meaningful data is stored in the array pointed to by `first`. To be specific, suppose that this array is as shown in Figure 12-9.

![](img/b217c421655b51e7494cf3b89bb5432d_895_1.png)

**FIGURE 12-9**  Pointer `first` and its array

Next, consider the following statement:

```cpp
second = first;        //Line A
```

This statement copies the memory address held by `first` into `second`. After this statement executes, both `first` and `second` point to the same array, as shown in Figure 12-10.

![](img/b217c421655b51e7494cf3b89bb5432d_895_2.png)

**FIGURE 12-10**  `first` and `second` after the statement `second = first;` executes

Let us next execute the following statement:

```cpp
delete [] second;
```

After this statement executes, the array pointed to by `second` is deleted. This action results in Figure 12-11.

![](img/b217c421655b51e7494cf3b89bb5432d_895_3.png)

**FIGURE 12-11**  `first` and `second` after the statement `delete [] second;` executes

Because **first** and **second** point to the same array, after the statement

```cpp
delete [] second;
```

executes, **first** becomes invalid; that is, **first** (as well as **second**) are now dangling pointers. Therefore, if the program later tries to access the memory pointed to by **first**, either the program will access the wrong memory or it will terminate in an error. This case is an example of a shallow copy. More formally, in a **shallow copy**, two or more pointers of the same type point to the same memory; that is, they point to the same data.

On the other hand, suppose that instead of the earlier statement, **second = first;** (in Line A), we have the following statements:

```cpp
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```

The first statement creates an array of 10 components of type **int**, and the base address of the array is stored in **second**. The second statement copies the array pointed to by **first** into the array pointed to by **second** (see Figure 12-12).

![](img/b217c421655b51e7494cf3b89bb5432d_896_0.png)

**FIGURE 12-12**  *first* and *second* both pointing to their own data

Both **first** and **second** now point to their own data. If **second** deletes its memory, there is no effect on **first**. This case is an example of a deep copy. More formally, in a **deep copy**, two or more pointers of the same type each point to their own copy of the data.

From the preceding discussion, it follows that you must know when to use a shallow copy and when to use a deep copy.

## Classes and Pointers: Some Peculiarities

In a previous section, we discussed how to use the arrow notation to access class members via the pointer if a pointer variable is of a class type. Because a class can have pointer member variables, this section discusses some peculiarities of such classes. To facilitate the discussion, we will use the following class:

```cpp
class ptrMemberVarType
{
```
