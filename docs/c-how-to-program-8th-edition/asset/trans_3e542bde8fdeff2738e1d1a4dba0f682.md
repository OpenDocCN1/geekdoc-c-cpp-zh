
（读作“Big Oh”）表示法，用于描述每种方案完成任务必须付出多大代价。

## 插入排序

图 7.19 中的程序将包含 10 个元素的数组 data 的值按升序排序。我们使用的技术称为插入排序——一种简单但效率不高的排序算法。该算法的第一次迭代取出第二个元素，如果它小于第一个元素，就将其与第一个元素交换（即程序将第二个元素插入到第一个元素之前）。第二次迭代查看第三个元素，并将其插入到相对于前两个元素的正确位置，因此这三个元素都有序。在该算法的第 i 次迭代时，原数组中的前 i 个元素将是有序的。

图 7.19 的第 10 行声明并初始化数组 data，其值如下：

|  |  |  |  |  |  |  |  |  |  |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 34 | 56 | 4 | 10 | 77 | 51 | 93 | 30 | 5 | 52 |

程序首先查看 data[0] 和 data[1]，它们的值分别为 34 和 56。这两个元素已经有序，因此程序继续执行——如果它们无序，程序就会交换它们。

```cpp
// Fig. 7.19: fig07_19.cpp
// This program sorts an array's values into ascending order.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    const int arraySize = 10; // size of array a
    int data[ arraySize ] = { 34, 56, 4, 10, 77, 51, 93, 30, 5, 52 };
    int insert; // temporary variable to hold element

    cout << "Unsorted array:\n";

    // output original array
    for ( int i = 0; i < arraySize; ++i )
        cout << setw( 4 ) << data[ i ];

    // insertion sort
    // loop over the elements of the array
    for ( int next = 1; next < arraySize; ++next )
    {
        insert = data[ next ]; // store the value in the current element

        int moveItem = next; // initialize location to place element

        // search for the location in which to put the current element
        while ( ( moveItem > 0 ) && ( data[ moveItem - 1 ] > insert ) )
        {
            // shift element one slot to the right
            data[ moveItem ] = data[ moveItem - 1 ];
            moveItem--;
        } // end while

        data[ moveItem ] = insert; // place inserted element into the array
    } // end for

    cout << "\nSorted array:\n";

    // output sorted array
    for ( int i = 0; i < arraySize; ++i )
        cout << setw( 4 ) << data[ i ];

    cout << endl;
} // end main
```

```text
Unsorted array:
   34  56   4  10  77  51  93  30   5  52
Sorted array:
    4   5  10  30  34  51  52  56  77  93
```

**图 7.19** | 使用插入排序对数组排序。

第二次迭代中，程序查看 data[2] 的值，即 4。该值小于 56，因此程序将 4 存入临时变量，并将 56 向右移动一个元素。程序随后检查并确定 4 小于 34，因此将 34 向右移动一个元素。此时程序已到达数组开头，因此将 4 放入 data[0]。数组现在为

```text
  4   34   56   10   77   51   93   30   5   52
```

第三次迭代中，程序将 data[3] 的值 10 存入临时变量。然后程序将 10 与 56 比较，因为 56 大于 10，所以将 56 向右移动一个元素。程序接着将 10 与 34 比较，将 34 向右移动一个元素。当程序将 10 与 4 比较时，发现 10 大于 4，于是将 10 放入 data[1]。数组现在为

```text
  4   10   34   56   77   51   93   30   5   52
```

使用该算法时，在第 iᵗʰ 次迭代，原数组的前 i 个元素是有序的。不过，它们可能不在最终位置上，因为更小的值可能位于数组后面的位置。

排序由第 21–36 行的 for 语句执行，该语句遍历数组的元素。在每次迭代中，第 23 行将要插入数组已排序部分的元素值临时存入变量 insert（在第 11 行声明）。第 25 行声明并初始化变量 moveItem，它跟踪元素应插入的位置。第 28–33 行循环查找元素应插入的正确位置。当程序到达数组前端，或到达一个小于待插入值的元素时，循环终止。第 31 行将一个元素向右移动，第 32 行递减下一个元素的插入位置。while 循环结束后，第 35 行将元素插入到位。当第 21–36 行的 for 语句终止时，数组元素已排序。

插入排序的主要优点在于易于编程；然而，它运行缓慢。在对大型数组排序时，这一点会变得明显。在练习中，我们将研究一些用于数组排序的替代算法。我们将在第 19 章更深入地研究排序和搜索。

## 7.9 多维数组

二维（即两个下标）数组通常表示由按行和列排列的信息组成的值表。要标识某个特定表元素，必须指定两个下标。按照惯例，第一个下标标识元素所在的行，第二个下标标识元素所在的列。需要两个下标来标识特定元素的数组称为二维数组或 2-D 数组。具有两个或更多维度的数组称为多维数组，并且可以具有两个以上维度。图 7.20 展示了一个二维数组。该数组包含三行四列，因此称为 3×4 数组。一般来说，具有 m 行 n 列的数组称为 m×n 数组。

![](img/bfd978e7e9b192bab46ec2a89e481263_330_0.png)

**图 7.20** | 具有三行四列的二维数组。

图 7.20 中，数组 a 的每个元素都通过形如 a[i][j] 的元素名来标识，其中 a 是数组名，i 和 j 是唯一标识 a 中每个元素的下标。注意，第 0 行中元素名的第一个下标均为 0；第 3 列中元素名的第二个下标均为 3。

> **常见编程错误 7.7**
> 
> 将二维数组元素 `a[x][y]` 错误地引用为 `a[x, y]` 是一种错误。实际上，`a[x, y]` 会被当作 `a[x]`，因为 C++ 会把表达式 `x, y`（包含逗号运算符）简单地求值为 `y`（逗号分隔表达式中的最后一个）。

多维数组可以像一维数组一样在声明中初始化。例如，一个二维数组 b，其第 0 行元素为 1 和 2，第 1 行元素为 3 和 4，可以这样声明并初始化：

```cpp
int b[ 2 ][ 2 ] = { { 1, 2 }, { 3, 4 } };
```

这些值在花括号中按行分组。因此，1 和 2 分别初始化 `b[0][0]` 和 `b[0][1]`，3 和 4 分别初始化 `b[1][0]` 和 `b[1][1]`。如果给定行的初始化值不够，该行剩余元素初始化为 0。因此，声明

```cpp
int b[2][2] = { { 1 }, { 3, 4 } };
```

会将 `b[0][0]` 初始化为 1，`b[0][1]` 初始化为 0，`b[1][0]` 初始化为 3，`b[1][1]` 初始化为 4。图 7.21 演示了在声明中初始化二维数组。第 12–14 行声明了三个数组，每个数组都有两行三列。`array1` 的声明（第 12 行）在两个子列表中提供了六个初始化值。第一个子列表将数组的第 0 行初始化为值 1、2 和 3；第二个子列表将数组的第 1 行初始化为

```cpp
// Fig. 7.21: fig07_21.cpp
// Initializing multidimensional arrays.
#include <iostream>
using namespace std;

void printArray( const int a[][ 3 ] ); // prototype
const int rows = 2;
const int columns = 3;

int main()
{
   int array1[ rows ][ columns ] = { { 1, 2, 3 }, { 4, 5, 6 } };
   int array2[ rows ][ columns ] = { { 1, 2, 3, 4, 5 } };
   int array3[ rows ][ columns ] = { { 1, 2 }, { 4 } };

   cout << "Values in array1 by row are:" << endl;
   printArray( array1 );

   cout << "\nValues in array2 by row are:" << endl;
   printArray( array2 );

   cout << "\nValues in array3 by row are:" << endl;
   printArray( array3 );
} // end main

// output array with two rows and three columns
void printArray( const int a[][ columns ] )
{
   // loop through array's rows
   for ( int i = 0; i < rows; ++i )
   {
      // loop through columns of current row
      for ( int j = 0; j < columns; ++j )
         cout << a[ i ][ j ] << ' ';

      cout << endl; // start new line of output
   } // end for
} // end function printArray
```

**图 7.21** | 初始化多维数组。（第 1 部分，共 2 部分。）
