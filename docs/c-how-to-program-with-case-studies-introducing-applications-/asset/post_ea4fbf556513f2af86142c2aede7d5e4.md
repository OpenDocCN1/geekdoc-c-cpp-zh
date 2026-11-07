
## Section 6.7 Passing Arrays to Functions
- To pass an array argument to a function, specify the array name without any brackets.
- Unlike char arrays that contain strings, other array types do not have a special terminator. For this reason, the array’s size is passed to a function, so the function can process the proper number of elements.
- C automatically passes arrays to functions by reference—the called functions can modify the element values in the caller’s original arrays. An array name evaluates to the address of the array’s first element. Because the starting address of the array is passed, the called function knows precisely where the array is stored and can modify the original array in the caller.
- Although entire arrays are passed by reference, individual array elements are passed by value exactly as simple variables are.
- Single pieces of data (such as individual ints, floats and chars) are called scalars (p. 261).
- To pass an array element to a function, use the subscripted name of the array element.
- For a function to receive an array through a function call, the function’s parameter list must specify that an array will be received. The array’s size is not required between the array brackets. If it’s included, the compiler checks that it’s greater than zero, then ignores it.
- If an array parameter is preceded by the const qualifier (p. 263), any attempt to modify an element in the function body results in a compilation error.

## Section 6.8 Sorting Arrays
- Sorting data—that is, placing the data into ascending or descending order—is one of the most important computing applications.
- One sorting technique is called the bubble sort (p. 265) or the sinking sort, because the smaller values gradually “bubble” their way upward to the top of the array like air bubbles rising in water, while the larger values sink to the bottom of the array. The technique is to make several passes through the array. On each pass, successive pairs of elements are compared. If a pair is in increasing order (or the values are identical), we leave the values as they are. If a pair is in decreasing order, their values are swapped in the array.
- Bubble sort may move a large value down the array many positions on a single pass but may move a small value up only one position.
- The chief virtue of the bubble sort is that it’s easy to program. However, it runs slowly. This becomes apparent when sorting large arrays.

## Section 6.9 Intro to Data Science Case Study: Survey Data Analysis
- The mean is the arithmetic average of a set of values.
- The median is the “middle value” in a sorted set of values.
- The mode is the value that occurs most frequently in a set of values.

## Section 6.10 Searching Arrays
- The process of finding a particular array element is called searching (p. 272).
- The linear search compares each array element with a search key (p. 272). The array is not in any particular order, so it’s just as likely that the value will be found in the first element as in the last. On average, therefore, the search key will be compared with half the array’s elements.
- The linear search algorithm (p. 272) works well for small or unsorted arrays. For sorted arrays, the high-speed binary search algorithm can be used.
- The binary search algorithm (p. 272) eliminates from consideration one-half of a sorted array's elements after each comparison. The algorithm locates the middle array element and compares it to the search key. If they're equal, the search key is found, and that element's subscript is returned. If they're not equal, the problem is reduced to searching one-half of the array. If the search key is less than the middle array element, the array's first half is searched; otherwise, the second half is searched. If the search key is not found in the specified subarray, the algorithm is repeated on one-quarter of the original array. The search continues until the search key is equal to a subarray's middle element, or until the subarray consists of one element that's not equal to the search key (i.e., the search key is not found).
- When using a binary search, the maximum number of comparisons required for any array can be determined by finding the first power of 2 greater than the number of array elements.

## Section 6.11 Multidimensional Arrays
- A common use of multidimensional arrays (p. 278) is to represent tables of values consisting of rows and columns. To identify a particular table element, we specify two subscripts. By convention, the first identifies the element's row, and the second identifies its column.
- Arrays that require two subscripts to identify an element are called two-dimensional arrays (p. 278). Multidimensional arrays can have more than two subscripts.
- A multidimensional array can be initialized when it's defined. The values in a two-dimensional array's initializer list are grouped by row in braces. If there are not enough initializers for a given row, its remaining elements are initialized to 0.
- The first subscript of a multidimensional array parameter declaration is not required, but all subsequent subscripts are. The compiler uses these sizes to determine the locations in memory of elements in multidimensional arrays. All array elements are stored consecutively in memory, regardless of the number of subscripts. In a two-dimensional array, the first row is stored in memory, followed by the second row, and so on.
- Providing the subscript values in a parameter declaration enables the compiler to tell the function how to locate an array element. In a two-dimensional array, each row is basically a one-dimensional array. To locate an element in a particular row, the compiler must know how many elements are in each row, so it can skip the proper number of memory locations when accessing elements of a given row.

## Section 6.12 Variable-Length Arrays
- A variable-length array (p. 286) is an array for which the size is defined by an expression evaluated at execution time.
- When applied to a variable-length array, sizeof operates at runtime.
- Variable-length arrays are optional in C—they may not be supported by your compiler.

## Self-Review Exercises
### 6.1 Answer each of the following:
- a) Lists and tables of values are stored in ______.
- b) The number used to refer to a particular array element is called its ______.
- c) A(n) ______ should be used to specify the size of an array because it makes the program more modifiable.
- d) Placing the elements of an array in order is called ______ the array.
- e) Determining whether an array contains a key value is called ______ the array.
- f) An array that uses two subscripts is referred to as a(n) ______ array.

### 6.2 State whether the following are true or false. If the answer is false, explain why.
- a) An array can store many different types of values.
- b) An array subscript can be of data type double.
- c) If there are fewer initializers in an initializer list than there are array elements, the remaining elements are initialized with the initializer list's last value.
- d) It's an error if an initializer list contains more initializers than there are array elements.
- e) An individual array element that's passed to a function as an argument of the form a[i] and modified in the called function will contain the modified value in the calling function.

### 6.3 Follow the instructions below regarding an array called fractions.
- a) Define a symbolic constant SIZE with the replacement text 10.
- b) Define a double array with SIZE elements and initialize the elements to 0.
- c) Refer to array element 4.
- d) Assign the value 1.667 to array element nine.
- e) Assign the value 3.333 to the seventh element of the array.
- f) Print array elements 6 and 9 with two digits of precision to the right of the decimal point, and show the output that's displayed on the screen.
- g) Print all the elements of an array using a for iteration statement. Use the variable x as the loop's control variable. Show the output.

### 6.4 Write statements to accomplish the following:
- a) Define table to be an integer array and to have 3 rows and 3 columns. Assume the symbolic constant SIZE has been defined to be 3.
- b) How many elements does the array table contain? Print the total number of elements.
- c) Use a for iteration statement to initialize each element of table to the sum of its subscripts. Use variables x and y as control variables.
- d) Print the values of each element of array table. Assume the array was initialized with the definition:
```
int table[SIZE][SIZE] = {{1, 8}, {2, 4, 6}, {5}};
```

### 6.5 Find the error in each of the following program segments and correct the error.
```
#define SIZE 100;
SIZE = 10;
int b[10] = {0};
int i;
for (size_t i = 0; i <= 10; ++i) {
    b[i] = 1;
}
#include <stdio.h>;
int a[2][2] = {{1, 2}, {3, 4}};
a[1, 1] = 5;
#define VALUE = 120
```
