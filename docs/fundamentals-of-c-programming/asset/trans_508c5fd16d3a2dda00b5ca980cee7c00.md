

**图 11.10 有缺陷的数组复制**

![](img/e84ad11adb18201d71595b31ce6c9eff_338_0.png)

必须为动态数组分配独立空间，然后将原始数组中的每个元素复制到新数组中。图 11.11 展示了此过程的工作原理。

需要注意的是，由于上述代码使用 new 动态分配了 b，程序中其他位置的代码在不再使用 b 时最终应使用 delete 释放 b 的空间。未能正确释放 b 会构成内存泄漏。

请考虑以下场景：

```
int *a = new int[10],
     *b = new int[10];
// Do somethings with arrays a and b, and then
b = a;
```

赋值前，动态数组 b 已经被使用。这种简单的赋值不仅会创建别名，还会造成内存泄漏。如果重新赋值的数组最初指向为其分配的一块内存，且没有其他指针引用该内存块，那么该内存块对执行程序来说已不可达。

清单 11.18 (flexiblearrayaverage.cpp) 要求用户预先输入要平均的值的数量。这很不方便，而且人们臭名昭著地不擅长计数。一个解决方案是先分配一个最小大小的数组，然后在数组填满时根据需要调整其大小。清单 11.19 (resizearray.cpp) 采用了这种方法。

**清单 11.19: resizearray.cpp**

```
#include <iostream>
int main() {
    double sum = 0.0, // Sum of the elements in the list
           *numbers,  // Dynamic array of numbers
           input;      // Current user entry
```

**图 11.11 正确的数组复制**

```
int a[] = { 2, 4, 6, 8 }, b;

b = new int[4];

for ( int i = 0; i < 4; i++ )
    b[i] = a[i];
```

```
// Initial size of array and amount to expand full array
const int CHUNK = 3;
int size = 0, // Current number of entries
    capacity = CHUNK; // Initial size of array

// Allocate a modest-sized array to begin with
numbers = new double[capacity];

std::cout << "Please enter any number of nonnegative values "
          << "(negative value ends the list) : ";
std::cin >> input;

while (input >= 0) { // Continue until negative number entered
    if (size >= capacity) { // Room left to add an element?
        capacity += CHUNK; // Expand array
        double *temp = new double[capacity]; // Allocate space
        for (int i = 0; i < size; i++)
            temp[i] = numbers[i]; // Copy existing values
        delete [] numbers; // Free up old space
        numbers = temp; // Update numbers to new location
        std::cout << "Expanding by " << CHUNK << "\n";
    }
    numbers[size] = input; // Add number to array at last position
    size++; // Update last position
    sum += input; // Add to running sum
    std::cin >> input; // Get next number
}

if (size > 0) { // Can't average less than one number
    for (int i = 0; i < size - 1; i++)
        std::cout << numbers[i] << ", ";
    // No comma following last element
    std::cout << numbers[size - 1] << " is "
              << sum/size << '\n';
}
else
    std::cout << "No numbers to average\n";
delete [] numbers; // Free up the space held by numbers
}
```

请注意，清单 11.19 (resizearray.cpp) 的程序员花费了大量精力来实现 std::vector 提供的功能。与向量不同，数组的大小是固定的。除非修改源代码并重新编译，否则无法更改静态数组的大小。为了在运行时更改动态数组的大小，你必须

- 1. 分配所需大小的不同内存块，
- 2. 将所有现有元素复制到新内存中，
- 3. 使用 `delete` 释放之前的内存块以避免内存泄漏，以及
- 4. 将原始动态数组指针重新赋值以指向新内存块。

**图 11.12 一个 2 x 3 的二维数组**

![](img/e84ad11adb18201d71595b31ce6c9eff_341_0.png)

清单 11.19 (resizearray.cpp) 包含执行此数组调整大小的代码。向量对象管理动态数组，其 push_back 方法为我们处理这些细节。

## 11.2.5 多维数组

正如 C++ 支持高维向量一样，它也支持多维数组。以下语句：

```
int a[2][3];
```

声明 a 为整数的二维（2D）数组。在此情况下，该声明指定数组 a 包含两行三列。图 11.12 显示了以下代码序列创建的数组的逻辑结构：

```
int a[2][3]; // a is a 2D array
a[0][0] = 5;
a[0][1] = 19;
a[0][2] = 3;
a[1][0] = 22;
a[1][1] = -8;
a[1][2] = 10;
```

二维数组 a 被称为 2 x 3 数组，意味着它有两行三列（如图 11.12 所示）。行水平排列，列中的值垂直排列。在上面的每个赋值语句中，例如

```
a[1][0] = 22;
```

第一个索引（这里是 1）表示行，第二个索引（这里是 0）表示数组中元素的列。

使用类似于 2D 向量的语法，我们可以像下面这样声明和创建上述 2D 数组：

```
int a[2][3] = { { 5, 19, 3 },
{ 22, -8, 10 } };
```

你可以省略第一个索引，如下所示：

```
int a[][3] = { { 5, 19, 3 },
{ 22, -8, 10 } };
```

以这种方式初始化的 2D 数组中，第一个下标是可选的，但第二个下标（即每列的大小）是必需的。

要访问 2D 数组的元素，请使用两个下标：

```
a[r][c] = 4; // Assign element at row r, column c
std::cout << a[m][n] << '\n'; // Display element at row m, column n
```

以下函数打印 ROWS × COLUMNS 二维 double 数组的内容，其中 ROWS 和 COLUMNS 均为常量：

```
void print(const double m[ROWS][COLUMNS]) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++)
            std::cout << std::setw(5) << m[row][col];
        std::cout << '\n';
    }
}
```

我们可以在参数声明中省略 ROW 大小，但第二组方括号必须是常量积分表达式。参数 m 的声明相当复杂，和我们对 2D 向量所做的一样，可以通过使用 C++ 类型别名语句来简化语法。

```
using Matrix = double[ROWS][COLUMNS];
```

定义一个名为 Matrix 的新类型。

给定定义新类型名 Matrix 的类型别名 using 语句，我们可以更简单地表示 print 函数的参数：

```
void print(const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++)
            std::cout << std::setw(5) << m[row][col];
        std::cout << '\n';
    }
}
```

清单 11.20 (twodimarray.cpp) 尝试使用 2D 数组，并利用类型别名语句简化代码。

**清单 11.20: twodimarray.cpp**

```
#include <iostream>
#include <iomanip>
const int ROWS = 3,
          COLUMNS = 5;

// The name Matrix represents a new type
// that means a ROWS x COLUMNS
// two-dimensional array of double-precision
// floating-point numbers.
using Matrix = double[ROWS][COLUMNS];

// Allow the user to enter the elements of a matrix
void populate_matrix(Matrix m) {
    std::cout << "Enter the " << ROWS << " rows of the matrix.\n";
    for (int row = 0; row < ROWS; row++) {
        std::cout << "Row #" << row << " (enter " << COLUMNS << " values):";
        for (int col = 0; col < COLUMNS; col++)
            std::cin >> m[row][col];
    }
}

// We declare m constant because printing a matrix should not
// change it.
void print_matrix(const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++)
            std::cout << std::setw(5) << m[row][col];
        std::cout << "\n";
    }
}

int main() {
    // Declare the 2D array
    Matrix mat;
    // Populate the array
    populate_matrix(mat);
    // Print the array
    print_matrix(mat);
}
```

仅使用一个索引与 2D 数组一起使用的表达式表示 2D 数组中的单行。该行本身是一个 1D 数组。因此，如果 a 是 2D 数组且 i 是整数，则表达式

```
a[1]
```

是一个表示行 i 的 1D 数组。

与向量一样，C++ 允许维度高于二的数组。3D 数组的每个“切片”只是一个 2D 数组，4D 数组是 3D 数组的数组，等等。例如，语句

```
matrix[x][y][z][t] = 1.0034;
```

将 1.0034 赋给 double 4D 数组中的一个元素。在实践中，超过两个维度的数组很少见，但高级科学和工程应用有时需要高维数组。

## 11.2.6 C 字符串

字符串是字符序列。C 和 C++ 将字符串实现为 char 数组。C++ 语言还支持字符串对象（参见第 13.1 节）。在 C 语言中，唯一的选择是 char 数组。

