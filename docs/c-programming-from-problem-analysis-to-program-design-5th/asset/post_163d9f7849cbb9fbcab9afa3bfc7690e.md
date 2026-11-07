
*program execution.* That is, the value of list is *constant.* Therefore, the increment and decrement operations cannot be applied to list. In fact, any attempt to use the increment or decrement operations on list results in a compile-time error.

Notice that here, we are *only* saying that the value of list cannot be changed. However, the data into the array list can be manipulated as before. For example, the statement `list[0] = 25;` stores 25 into the first array component. Similarly, the statement `list[3] = 78;` stores 78 into the fourth component of list (see Figure 14-7).

![](img/1fbe55537254baeb2b5b7dbaf64956ae_851_0.png)

FIGURE 14-7 Array list after the execution of the statements `list[0] = 25;` and `list[3] = 78;`

If p is a pointer variable of type int, then the statement:

```
p = list;
```

copies the value of list, which is 1000, the base address of the array, into p. We are allowed to perform increment and decrement operations on p.

*An array name is a constant pointer.*

### EXAMPLE 14-5

The following program segment illustrates how to obtain a user's response to get the array size and create a dynamic array during program execution. Consider the following statements:

```
int *intList;                 //Line 1
int arraySize;                //Line 2

cout << "Enter array size: ";  //Line 3
cin >> arraySize;             //Line 4
cout << endl;                 //Line 5

intList = new int[arraySize]; //Line 6
```

The statement in Line 1 declares `intList` to be a pointer of type int, and the statement in Line 2 declares `arraySize` to be an int variable. The statement in Line 3 prompts the user to enter the size of the array, and the statement in Line 4 inputs the array size into the variable `arraySize`. The statement in Line 6 creates an array of the size specified by `arraySize`, and the base address of the array is stored in `intList`. From this point on, you can treat `intList` just like any other array. For example, you can use the array notation to process the elements of `intList` and pass `intList` as a parameter to the function.

## Functions and Pointers

A pointer variable can be passed as a parameter to a function either by value or by reference. To declare a pointer passed as a value parameter in a function heading, you use the same mechanism as you use to declare a variable. To make a formal parameter be a reference parameter, you use & when you declare the formal parameter in the function heading. Therefore, to declare a formal parameter as a reference pointer parameter, between the data type name and the identifier name, you must include * to make the identifier a pointer and & to make it a reference parameter. The obvious question is: In what order should & and * appear between the data type name and the identifier to declare a pointer as a reference parameter? In C++, to make a pointer a reference parameter in a function heading, * appears before the & between the data type name and the identifier. The following example illustrates this concept.

```cpp
void pointerParameters(int* &p, double *q)
{
    .
    .
    .
}
```

In the function `pointerParameters`, both p and q are pointers. The parameter p is a reference parameter; the parameter q is a value parameter. Furthermore, the function `pointerParameters` can change the value of *q, but not the value of q. However, the function `pointerParameters` can change the value of both p and *p.

## Pointers and Function Return Values

In C++, the return type of a function can be a pointer. For example, the return type of the function:

```cpp
int* testExp(...)
{
    .
    .
    .
}
```

is a pointer of type int.

## Dynamic Two-Dimensional Arrays

The beginning of this section discussed how to create dynamic one-dimensional arrays. You can also create dynamic multidimensional arrays. In this section, we discuss how to create dynamic two-dimensional arrays. Dynamic multidimensional arrays are created similarly.

There are various ways you can create dynamic two-dimensional arrays. One way is as follows. Consider the statement:

```
int *board[4];
```

This statement declares board to be an array of four pointers wherein each pointer is of type `int`. Because `board[0]`, `board[1]`, `board[2]`, and `board[3]` are pointers, you can now use these pointers to create the rows of board. Suppose that each row of board has six columns. Then, the following `for` loop creates the rows of board.

```
for (int row = 0; row < 4; row++)
    board[row] = new int[6];
```

Note that the expression `new int[6]` creates an array of six components of type `int` and returns the base address of the array. The assignment statement then stores the returned address into `board[row]`. It follows that after the execution of the previous `for` loop, board is a two-dimensional array of four rows and six columns.

In the previous `for` loop, if you replace the number 6 with the number 10, then the loop will create a two-dimensional array of four rows and 10 columns. In other words, the number of columns of board can be specified during execution. However, the way board is declared, the number of rows is fixed. So in reality, board is not a true dynamic two-dimensional array.

Next, consider the following statement:

```
int **board;
```

This statement declares board to be a pointer to a pointer. In other words, board and *board are pointers. Now board can store the address of a pointer or an array of pointers of type `int`, and *board can store the address of an `int` memory space or an array of `int` values.

Suppose that you want board to be an array of 10 rows and 15 columns. To accomplish this, first we create an array of 10 pointers of type `int` and assign the address of that array to board. The following statement accomplishes this:

```
board = new int*[10];
```

Next, we create the columns of board. The following `for` loop accomplishes this.

```
for (int row = 0; row < 10; row++)
    board[row] = new int[15];
```

To access the components of board, you can use the array subscripting notation discussed in Chapter 9.

Note that the number of rows and the number of columns of board can be specified during program execution. The following program further explains how to create two-dimensional arrays.

### EXAMPLE 14-6

```cpp
// Dynamic two-dimensional arrays
#include <iostream>
#include <iomanip>

using namespace std;

void fill(int **p, int rowSize, int columnSize);
void print(int **p, int rowSize, int columnSize);

int main()
{
    int **board;                              //Line 1

    int rows;                                 //Line 2
    int columns;                              //Line 3

    cout << "Line 4: Enter the number of rows "
         << "and columns: ";                 //Line 4
    cin >> rows >> columns;                   //Line 5
    cout << endl;                             //Line 6

        //Create the rows of board
    board = new int* [rows];                  //Line 7

        //Create the columns of board
    for (int row = 0; row < rows; row++)      //Line 8
        board[row] = new int[columns];       //Line 9

        //Insert elements into board
    fill(board, rows, columns);               //Line 10

    cout << "Line 11: Board:" << endl;       //Line 11

        //Output the elements of board
    print(board, rows, columns);              //Line 12

    return 0;
}
```

## Shallow versus Deep Copy and Pointers

In an earlier section, we discussed pointer arithmetic and explained that if we are not careful, one pointer might access the data of another (completely unrelated) pointer. This event might result in unexpected or erroneous results. Here, we discuss another peculiarity of pointers. To facilitate the discussion, we will use diagrams to show pointers and their related memory.

Consider the following statements:

```
    int *first;
    int *second;

    first = new int[10];
```

The first two statements declare `first` and `second` pointer variables of type `int`. The third statement creates an array of 10 components, and the base address of the array is stored into `first` (see Figure 14-8). (Note that `first` together with the arrow indicates that `first` points to the allocated memory.)

![](img/1fbe55537254baeb2b5b7dbaf64956ae_856_0.png)

FIGURE 14-8 Pointer `first` and the array to which it points

Suppose that some meaningful data is stored in the array pointed to by `first`. To be specific, suppose that this array is as shown in Figure 14-9.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_856_1.png)

FIGURE 14-9 Pointer `first` and its array

Next, consider the following statement:

```
    second = first;          //Line A
```

This statement copies the value of `first` into `second`. After this statement executes, both `first` and `second` point to the same array, as shown in Figure 14-10.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_856_2.png)

FIGURE 14-10 `first` and `second` after the statement `second = first;` executes
