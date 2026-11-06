
## 6.6.3 Computing Row and Column Totals

A common task is to compute row or column totals. In our example, the row totals give us the total number of medals won by a particular country.

Finding the right index values is a bit tricky, and it is a good idea to make a quick sketch. To compute the total of row *i*, we need to visit the following elements:

![](img/5e58fb4c840712efd6ed6fa82bb97f57_307_0.png)

As you can see, we need to compute the sum of `counts[i][j]`, where *j* ranges from 0 to `MEDALS - 1`. The following loop computes the total:

```c
int total = 0;
for (int j = 0; j < MEDALS; j++)
{
   total = total + counts[i][j];
}
```

Computing column totals is similar. Form the sum of `counts[i][j]`, where *i* ranges from 0 to `COUNTRIES - 1`.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_307_1.png)

```c
int total = 0;
for (int i = 0; i < COUNTRIES; i++)
{
   total = total + counts[i][j];
}
```

## 6.6.4 Two-Dimensional Array Parameters

> A two-dimensional array parameter must have a fixed number of columns.

When passing a two-dimensional array to a function, you must specify the number of columns *as a constant* with the parameter type. For example, this function computes the total of a given row:

```cpp
const int COLUMNS = 3;

int row_total(int table[][COLUMNS], int row)
{
    int total = 0;
    for (int j = 0; j < COLUMNS; j++)
    {
        total = total + table[row][j];
    }
    return total;
}
```

This function can compute row totals of a two-dimensional array with an arbitrary number of rows, but the array must have 3 columns. You have to write a different function if you want to compute row totals of a two-dimensional array with 4 columns.

To understand this limitation, you need to know how the array elements are stored in memory. Although the array appears to be two-dimensional, the elements are still stored as a linear sequence. Figure 13 shows how the `counts` array is stored, row by row.

For example, to reach

`counts[3][1]`

the program must first skip past rows 0, 1, and 2 and then locate offset 1 in row 3. The offset from the start of the array is

3 × *number of columns* + 1

Now consider the `row_total` function. The compiler generates code to find the element

`table[i][j]`

by computing the offset

`i * COLUMNS + j`

The compiler uses the value that you supplied in the second pair of brackets when declaring the parameter:

```cpp
int row_total(int table[][COLUMNS], int row)
```

Note that the first pair of brackets should be empty, just as with one-dimensional arrays.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_308_0.png)

**Figure 13** A Two-Dimensional Array is Stored as a Sequence of Rows

The `row_total` function did not need to know the number of rows of the array. If the number of rows is required, pass it as a variable, as in this example:

```cpp
int column_total(int table[][COLUMNS], int rows, int column)
{
    int total = 0;
    for (int i = 0; i < rows; i++)
    {
        total = total + table[i][column];
    }
    return total;
}
```

Working with two-dimensional arrays is illustrated in the following program. The program prints out the medal counts and the row totals.

## ch06/medals.cpp

```cpp
1 #include <iostream>
2 #include <iomanip>
3 #include <string>
4
5 using namespace std;
6
7 const int COLUMNS = 3;
8
9 /**
10    Computes the total of a row in a table.
11    @param table a table with 3 columns
12    @param row the row that needs to be totaled
13    @return the sum of all elements in the given row
14 */
15 double row_total(int table[][COLUMNS], int row)
16 {
17    int total = 0;
18    for (int j = 0; j < COLUMNS; j++)
19    {
20        total = total + table[row][j];
21    }
22    return total;
23 }
24
25 int main()
26 {
27    const int COUNTRIES = 7;
28    const int MEDALS = 3;
29
30    string countries[] =
31    {
32        "Canada",
33        "China",
34        "Germany",
35        "Korea",
36        "Japan",
37        "Russia",
38        "United States"
39    };
40
41    int counts[COUNTRIES][MEDALS] =
42    {
{ 1, 0, 1 },
{ 1, 1, 0 },
{ 0, 0, 1 },
{ 1, 0, 0 },
{ 0, 1, 1 },
{ 0, 1, 1 },
{ 1, 1, 0 }
};

cout << "        Country    Gold   Silver  Bronze   Total" << endl;

// Print countries, counts, and row totals
for (int i = 0; i < COUNTRIES; i++)
{
    cout << setw(15) << countries[i];
    // Process the ith row
    for (int j = 0; j < MEDALS; j++)
    {
        cout << setw(8) << counts[i][j];
    }
    int total = row_total(counts, i);
    cout << setw(8) << total << endl;
}

return 0;
}
```

## Program Run

| Country | Gold | Silver | Bronze | Total |
|---|---:|---:|---:|---:|
| Canada | 1 | 0 | 1 | 2 |
| China | 1 | 1 | 0 | 2 |
| Germany | 0 | 0 | 1 | 1 |
| Korea | 1 | 0 | 0 | 1 |
| Japan | 0 | 1 | 1 | 2 |
| Russia | 0 | 1 | 1 | 2 |
| United States | 1 | 1 | 0 | 2 |

## SELF CHECK

![](img/5e58fb4c840712efd6ed6fa82bb97f57_310_0.png)

- 30. What results do you get if you total the columns in our sample data?
- 31. Consider an 8 × 8 array for a board game:

  `int board[8][8];`

  Using two nested loops, initialize the board so that zeroes and ones alternate, as on a checkerboard:

  ```text
  0 1 0 1 0 1 0 1
  1 0 1 0 1 0 1 0
  0 1 0 1 0 1 0 1
  ...
  1 0 1 0 1 0 1 0
  ```

  *Hint:* Check whether `i + j` is even.

- 32. Define a two-dimensional array for representing a tic-tac-toe board. The board has three rows and columns and contains strings `"x"`, `"o"`, and `" "`.

- 33. Write an assignment statement to place an `"x"` in the upper-right corner of the tic-tac-toe board.

**34.** Which elements are on the diagonal joining the upper-left and the lower-right corners of the tic-tac-toe board?

**Practice It** Now you can try these exercises at the end of the chapter: R6.23, P6.19, P6.20.

## Common Error 6.2 — Omitting the Column Size of a Two-Dimensional Array Parameter

When passing a one-dimensional array to a function, you specify the size of the array as a separate parameter variable:

```cpp
void print(double values[], int size)
```

This function can print arrays of any size. However, for two-dimensional arrays you cannot simply pass the numbers of rows and columns as parameter variables:

```cpp
void print(double table[][], int rows, int cols) // NO!
```

The function must know at compile time how many columns the two-dimensional array has. You must specify the number of columns with the array parameter variable. This number must be a constant:

```cpp
const int COLUMNS = 3;
void print(const double table[][COLUMNS], int rows) // OK
```

This function can print tables with any number of rows, but the column size is fixed.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_311_0.png)

## WORKED EXAMPLE 6.2 — A World Population Table

This Worked Example shows how to print world population data in a table with row and column headers, and with the footnotes for each of the data columns.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_311_1.png)

## 6.7 Vectors

A vector stores a sequence of values whose size can change.

When you write a program that collects values from user input, you don’t always know how many values you will have. Unfortunately, the size of the array has to be known *when the program is compiled*. In Section 6.1.3, you saw how you can address this problem with partially filled arrays. The vector construct, which we discuss in the following sections, offers a more convenient solution. A vector collects a sequence of values, just like an array does, but its size can change.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_311_2.png)

*A vector expands to hold as many elements as needed.*

⊕ Available online at www.wiley.com/college/horstmann.

## Syntax 6.3 — Defining a Vector

![](img/5e58fb4c840712efd6ed6fa82bb97f57_312_0.png)

### 6.7.1 Defining Vectors

When you define a vector, you specify the type of the elements in angle brackets, like this:

```cpp
vector<double> values;
```

You can optionally specify the initial size. For example, here is a definition of a vector whose initial size is 10:

```cpp
vector<double> values(10);
```

If you define a vector without an initial size, it has size 0. While there would be no point in defining an array of size zero, it is often useful to have vectors with initial size zero, and then grow them as needed.

In order to use vectors in your program, you need to include the `<vector>` header.

**Table 2 Defining Vectors**

| Definition | Description |
|---|---|
| `vector<int> numbers(10);` | A vector of ten integers. |
| `vector<string> names(3);` | A vector of three strings. |
| `vector<double> values;` | A vector of size 0. |
| `vector<double> values();` | **Error:** Does not define a vector. |
| `vector<int> numbers;`<br>`for (int i = 1; i <= 10; i++)`<br>`{`<br>&nbsp;&nbsp;&nbsp;&nbsp;`numbers.push_back(i);`<br>`}` | A vector of ten integers, filled with 1, 2, 3, ..., 10. |
| `vector<int> numbers(10);`<br>`for (int i = 0; i < numbers.size(); i++)`<br>`{`<br>&nbsp;&nbsp;&nbsp;&nbsp;`numbers[i] = i + 1;`<br>`}` | Another way of defining a vector of ten integers and filling it with 1, 2, 3, ..., 10. |
