
We need to fix our plan of attack:

- Find the minimum value.
- Find its position.
- Remove that position from the array.
- Calculate the sum.

Will it work? Let’s continue with our example.

We found a minimum value of 4. Linear search tells us that the value 4 occurs at position 5.

| [0] | [1] | [2] | [3] | [4] | [5] | [6] |
|---|---|---|---|---|---|---|
| 8 | 7 | 8.5 | 9.5 | 7 | **4** | 10 |

We remove it:

| [0] | [1] | [2] | [3] | [4] | [5] |
|---|---|---|---|---|---|
| 8 | 7 | 8.5 | 9.5 | 7 | 10 |

Finally, we compute the sum: 8 + 7 + 8.5 + 9.5 + 7 + 10 = 50.

This walkthrough demonstrates that our strategy works.

Can we do better? It seems a bit inefficient to find the minimum and then make another pass through the array to obtain its position.

We can adapt the algorithm for finding the minimum to yield the position of the minimum. Here is the original algorithm:

```
double smallest = values[0];
for (int i = 1; i < size of values; i++)
{
    if (values[i] < smallest)
    {
        smallest = values[i];
    }
}
```

When we find the smallest value, we also want to update the position:

```
if (values[i] < smallest)
{
    smallest = values[i];
    smallest_position = i;
}
```

In fact, then there is no reason to keep track of the smallest value any longer. It is simply values[smallest_position]. With this insight, we can adapt the algorithm as follows:

```
int smallest_position = 0;
for (int i = 1; i < size of values; i++)
{
    if (values[i] < values[smallest_position])
    {
        smallest_position = i;
    }
}
```

With this adaptation, our problem is solved with the following strategy:

- Find the position of the minimum.
- Remove it from the array.
- Calculate the sum.

In How To 6.1 on page 271, we develop a C++ program from this strategy.

You should be familiar with the implementation of fundamental algorithms so that you can adapt them.

We discussed the algorithm for `min_position` in the preceding section:

```cpp
/**
   Gets the position of the minimum value from an array.
   @param values a partially filled array
   @param size the number of elements in values
   @return the position of the smallest element in values
*/
int min_position(double values[], int size)
{
   int smallest_position = 0;
   for (int i = 1; i < size; i++)
   {
      if (values[i] < values[smallest_position])
      {
         smallest_position = i;
      }
   }
   return smallest_position;
}
```

The remaining helper functions use the algorithms from Section 6.2. You will find the implementations in the book's companion code.

## Step 4 Consider boundary conditions for the functions that you are implementing

Most functions that operate on arrays are a bit intricate, and you have to be careful that you handle both normal and exceptional situations. What happens with an empty array? An array that contains a single element? When no match is found? When there are multiple matches? Consider these boundary conditions and make sure that your functions work correctly.

Here is one example of such a consideration. How do we know that the `min_position` function will be called with an array of size at least 1? (Recall that you must have at least one element in order to find the minimum.) That function is called from the `final_score` function. However, the `final_score` function could conceivably be called with an empty array. We need to either include a test or add a restriction to the function comment. We will opt for the latter and change the comment for the `values` parameter variable of the `min_position` function to

```cpp
@param values a partially filled array of size >= 1
```

Consider another potential problem. What if there are multiple matches? That means that a student had more than one test with a low score. The `final_score` function removes only one of the occurrences of that low score, and that is the desired behavior.

## Step 5 Assemble and test the complete program.

Now we are ready to combine the individual functions into a complete program. Before doing this, consider some test cases and their expected output:

| Test Case | Expected Output | Comment |
| :--- | :---: | :--- |
| 8 7 8.5 9.5 7 5 10 | 50 | See Step 1. |
| 8 7 7 9 | 24 | Only one instance of the low score should be removed. |
| 8 | 0 | After removing the low score, no score remains. |
| (no inputs) | **Error** | That is not a legal input. |

## 6.6 Two-Dimensional Arrays

It often happens that you want to store collections of values that have a two-dimensional layout. Such data sets commonly occur in financial and scientific applications. An arrangement consisting of rows and columns of values is called a *two-dimensional array*, or a *matrix*.

Let’s explore how to store the example data shown in Figure 11: the medal counts of the figure skating competitions at the 2010 Winter Olympics.

![](img/23fb3582e93ebc95909e1de029c3d388_305_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_305_1.png)

| Country | Gold | Silver | Bronze |
|---|---:|---:|---:|
| Canada | 1 | 0 | 1 |
| China | 1 | 1 | 0 |
| Germany | 0 | 0 | 1 |
| Korea | 1 | 0 | 0 |
| Japan | 0 | 1 | 1 |
| Russia | 0 | 1 | 1 |
| United States | 1 | 1 | 0 |

**Figure 11** Figure Skating Medal Counts

### 6.6.1 Defining Two-Dimensional Arrays

C++ uses an array with two subscripts to store a two-dimensional array. For example, here is the definition of an array with 7 rows and 3 columns, suitable for storing our medal count data:

```cpp
const int COUNTRIES = 7;
const int MEDALS = 3;
int counts[COUNTRIES][MEDALS];
```

You can initialize the array by grouping each row, as follows:

```cpp
int counts[COUNTRIES][MEDALS] =
{
    { 1, 0, 1 },
    { 1, 1, 0 },
    { 0, 0, 1 },
    { 1, 0, 0 },
    { 0, 1, 1 },
    { 0, 1, 1 },
    { 1, 1, 0 }
};
```

Just as with one-dimensional arrays, you cannot change the size of a two-dimensional array once it has been defined.

### 6.6.3 Computing Row and Column Totals

A common task is to compute row or column totals. In our example, the row totals give us the total number of medals won by a particular country.

Finding the right index values is a bit tricky, and it is a good idea to make a quick sketch. To compute the total of row i, we need to visit the following elements:

![](img/23fb3582e93ebc95909e1de029c3d388_307_0.png)

As you can see, we need to compute the sum of counts[i][j], where j ranges from 0 to MEDALS - 1. The following loop computes the total:

```cpp
int total = 0;
for (int j = 0; j < MEDALS; j++)
{
    total = total + counts[i][j];
}
```

Computing column totals is similar. Form the sum of counts[i][j], where i ranges from 0 to COUNTRIES - 1.

![](img/23fb3582e93ebc95909e1de029c3d388_307_1.png)

```cpp
int total = 0;
for (int i = 0; i < COUNTRIES; i++)
{
    total = total + counts[i][j];
}
```

The row_total function did not need to know the number of rows of the array. If the number of rows is required, pass it as a variable, as in this example:

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

### ch06/medals.cpp

```cpp
#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

const int COLUMNS = 3;

/**
   Computes the total of a row in a table.
   @param table a table with 3 columns
   @param row the row that needs to be totaled
   @return the sum of all elements in the given row
*/
double row_total(int table[][COLUMNS], int row)
{
   int total = 0;
   for (int j = 0; j < COLUMNS; j++)
   {
      total = total + table[row][j];
   }
   return total;
}

int main()
{
   const int COUNTRIES = 7;
   const int MEDALS = 3;

   string countries[] =
   {
      "Canada",
      "China",
      "Germany",
      "Korea",
      "Japan",
      "Russia",
      "United States"
   };

   int counts[COUNTRIES][MEDALS] =
   {
```
