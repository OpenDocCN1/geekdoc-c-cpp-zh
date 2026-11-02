
The `row_total` function did not need to know the number of rows of the array. If the number of rows is required, pass it as a variable, as in this example:

```c
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

**sec06/medals.cpp**

```cpp
#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

const int COLUMNS = 3;

/**
 * Computes the total of a row in a table.
 * @param table a table with 3 columns
 * @param row the row that needs to be totaled
 * @return the sum of all elements in the given row
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
    const int COUNTRIES = 8;
    const int MEDALS = 3;

    string countries[] =
    {
        "Canada",
        "Italy",
        "Germany",
        "Japan",
        "Kazakhstan",
        "Russia",
        "South Korea",
        "United States"
    };

    int counts[COUNTRIES][MEDALS] =
    {
        { 0, 3, 0 },
        { 0, 0, 1 },
        { 0, 0, 1 },
        { 1, 0, 0 },
        { 0, 0, 1 },
        { 3, 1, 1 },
        { 0, 1, 0 },
        { 1, 0, 1 }
    };

    cout << "    Country   Gold  Silver  Bronze  Total" << endl;

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

### Program Run

| Country | Gold | Silver | Bronze | Total |
|---|---|---|---|---|
| Canada | 0 | 3 | 0 | 3 |
| Italy | 0 | 0 | 1 | 1 |
| Germany | 0 | 0 | 1 | 1 |
| Japan | 1 | 0 | 0 | 1 |
| Kazakhstan | 0 | 0 | 1 | 1 |
| Russia | 3 | 1 | 1 | 5 |
| South Korea | 0 | 1 | 0 | 1 |
| United States | 1 | 0 | 1 | 2 |

![](img/d61019b035dd82beb581604273c0ee6b_341_0.png)

### Common Error 6.2

Omitting the Column Size of a Two-Dimensional Array Parameter

When passing a one-dimensional array to a function, you specify the size of the array as a separate parameter variable:

```cpp
void print(double values[], int size)
```

This function can print arrays of any size. However, for two-dimensional arrays you cannot simply pass the numbers of rows and columns as parameter variables:

```cpp
void print(double table[][], int rows, int cols) // NO!
```

The function must know at compile time how many columns the two-dimensional array has. You must specify the number of columns with the array parameter variable. This number must be a constant.

```cpp
const int COLUMNS = 3;
void print(const double table[][COLUMNS], int rows) // OK
```

This function can print tables with any number of rows, but the column size is fixed.

![](img/d61019b035dd82beb581604273c0ee6b_342_0.png)

### Worked Example 6.2

**A World Population Table**

Learn how to print world population data in a table with row and column headers, and with totals for each of the data columns. See your E-Text or visit wiley.com/go/bcl63.

## 6.7 Vectors

A vector stores a sequence of values whose size can change.

When you write a program that collects values from user input, you don't always know how many values you will have. Unfortunately, the size of the array has to be known when the program is compiled.

In Section 6.1.3, you saw how you can address this problem with partially filled arrays. The vector construct, which we discuss in the following sections, offers a more convenient solution. A vector collects a sequence of values, just like an array does, but its size can change.

![](img/d61019b035dd82beb581604273c0ee6b_342_1.png)

A vector expands to hold as many elements as needed.

### Syntax 6.3 Defining a Vector

```cpp
vector<double> values(10); // Element type   Name   Initial size

vector<double> values = { 32, 54, 67.5, 29, 34.5 };

values[1] = 0; // Use brackets to access an element.
```

If you omit the size and the parentheses, the vector has initial size 0.

If you specify initial values, you don't provide the size.

The index must be >= 0 and < values.size().

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

With C++ 11 and above, you can specify initial values for a vector, using the same notation as for arrays:

```cpp
vector<double> values = { 32, 54, 67.5, 29, 34.5 };
```

In order to use vectors in your program, you need to include the `<vector>` header.

You access the vector elements as `values[i]`, just as you do with arrays.

The `size` member function returns the current size of a vector. In a loop that visits all vector elements, use the `size` member function like this:

```cpp
for (int i = 0; i < values.size(); i++)
{
    cout << values[i] << endl;
}
```

Use the `size` member function to obtain the current size of a vector.

### Table 2 Defining Vectors

| Code | Description |
|------|-------------|
| `vector<int> numbers(10);` | A vector of ten integers. |
| `vector<string> names(3);` | A vector of three strings. |
| `vector<double> values;` | A vector of size 0. |
| `vector<double> values();` | Error: Does not define a vector; it declares a function returning a vector. |
| `vector<int> numbers; for (int i = 1; i <= 10; i++) { numbers.push_back(i); }` | A vector of ten integers, filled with 1, 2, 3, ..., 10. |
| `vector<int> numbers(10); for (int i = 0; i < numbers.size(); i++) { numbers[i] = i + 1; }` | Another way of defining a vector of ten integers and filling it with 1, 2, 3, ..., 10. |
| `vector<int> numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };` | This syntax is supported with C++ 11 and above. |

### 6.7.2 Growing and Shrinking Vectors

Use the `push_back` member function to add more elements to a vector. Use `pop_back` to reduce the size.

If you need additional elements, you use the `push_back` function to add an element to the end of the vector, thereby increasing its size by 1. The `push_back` function is a member function that you must call with the dot notation, like this:

```cpp
values.push_back(37.5);
```

Suppose the vector `values` had size 2 and elements 32 and 54 before the call to `push_back` (see Figure 14). After the call, the vector has size 3, and `values[2]` contains the value 37.5.

![](img/d61019b035dd82beb581604273c0ee6b_344_0.png)

Figure 14 Adding an Element with push_back

A common use for the `push_back` member function is to fill a vector with input values.

```cpp
vector<double> values; // Initially empty

double input;
while (cin >> input)
{
    values.push_back(input);
}
```

Note how this input loop is much simpler than the one in Section 6.2.11.

Another member function, `pop_back`, removes the last element of a vector, shrinking its size by one (see Figure 15):

```cpp
values.pop_back();
```

![](img/d61019b035dd82beb581604273c0ee6b_344_1.png)

Figure 15 Removing an Element with pop_back

### 6.7.3 Vectors and Functions

Vectors can occur as function arguments and return values.

You can use vectors as function arguments in exactly the same way as any other values. For example, the following function computes the sum of a vector of floating-point numbers:

```cpp
double sum(vector<double> values)
{
    double total = 0;
    for (int i = 0; i < values.size(); i++)
    {
        total = total + values[i];
    }
    return total;
}
```

Use a reference parameter to modify the contents of a vector.

This function visits the vector elements, but it does not modify them. If your function modifies the elements, use a reference parameter. The following function multiplies all values of a vector with a given factor.

```cpp
void multiply(vector<double>& values, double factor) // Note the &
{
    for (int i = 0; i < values.size(); i++)
    {
        values[i] = values[i] * factor;
    }
}
```

It is a good idea to use a constant reference (see Special Topic 5.2) for vector parameters that are not modified, for example:

```cpp
double sum(const vector<double>& values) // const & added for efficiency
```

A function can return a vector.

Again, vectors are no different from any other values in this regard. Simply build up the result in the function and return it. In this example, the `squares` function returns a vector of squares from 0² up to (n−1)²:

```cpp
vector<int> squares(int n)
{
    vector<int> result;
    for (int i = 0; i < n; i++)
    {
        result.push_back(i * i);
    }
    return result;
}
```

As you can see, it is easy to use vectors with functions—there are no special rules to keep in mind.

**EXAMPLE CODE** See sec07_03 of your companion code for a program that demonstrates vectors and functions.

### 6.7.4 Vector Algorithms

Most of the algorithms in Section 6.2 apply without change to vectors—simply replace `size of values` with `values.size()`. In this section, we discuss which of the algorithms are different for vectors.
