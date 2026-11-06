The row_total function did not need to know the number of rows of the array. If the number of rows is required, pass it as a variable, in this example:

```
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
```

Working with two-dimensional arrays is illustrated in the following program. The program prints out the medal counts and the row totals.

# ### ch06/medals.cpp

```
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
```
```