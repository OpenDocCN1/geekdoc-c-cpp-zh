
本示例中归并排序的实现是*递归的*。*基本情况*是只含一个元素的向量。当然，单元素向量已经有序，因此当以单元素向量调用归并排序时，它会立即返回。*递归步骤*将包含两个或更多元素的向量拆分为两个大小相等的子向量，递归地对每个子向量排序，然后将它们合并为一个更大的有序向量。（同样，如果元素个数为奇数，则一个子向量会比另一个多一个元素。）

假设该算法已经合并了较小的向量，从而创建了有序向量 A：

| 4 | 10 | 34 | 56 | 77 |
|---:|---:|---:|---:|---:|

和 B：

| 5 | 30 | 51 | 52 | 93 |
|---:|---:|---:|---:|---:|

归并排序将这两个向量合并为一个更大的有序向量。A 中的最小值是 4（位于 A 的第 0 个元素）。B 中的最小值是 5（位于 B 的第 0 个元素）。为了确定更大向量中的最小元素，算法比较 4 和 5。来自 A 的值较小，因此 4 成为合并后向量的第一个元素的值。算法继续比较 10（A 中第二个元素的值）与 5（B 中第一个元素的值）。来自 B 的值较小，因此 5 成为更大向量的第二个元素的值。算法继续比较 10 与 30，10 成为该向量的第三个元素的值，依此类推。

图 19.5 定义了类 MergeSort，图 19.6 的第 22–25 行定义了 sort 函数。第 24 行以 0 和 size − 1 为参数调用函数 sortSubVector。这些参数对应于待排序向量的起始索引和结束索引，使 sortSubVector 作用于整个向量。函数 sortSubVector 定义在第 28–52 行。第 31 行测试基本情况。如果向量的大小为 1，则向量已经有序，因此函数会立即返回。如果向量的大小大于 1，则函数将向量一分为二，递归调用函数 sortSubVector 对两个子向量排序，然后将它们合并。第 46 行递归调用函数 sortSubVector 处理向量的前半部分，第 47 行递归调用函数 sortSubVector 处理向量的后半部分。当这两个函数调用返回时，向量的每一半都已排序。第 50 行对向量的两半调用函数 merge（第 55–99 行），将两个有序向量合并为一个更大的有序向量。

```cpp
// Fig. 19.5: MergeSort.h
// Class that creates a vector filled with random integers.
// Provides a function to sort the vector with merge sort.
#include <vector>
using namespace std;

// MergeSort class definition
class MergeSort
{
public:
    MergeSort( int ); // constructor initializes vector
    void sort(); // sort vector using merge sort
    void displayElements() const; // display vector elements
private:
    int size; // vector size
    vector< int > data; // vector of ints
    void sortSubVector( int, int ); // sort subvector
    void merge( int, int, int, int ); // merge two sorted vectors
    void displaySubVector( int, int ) const; // display subvector
}; // end class MergeSort
```

**图 19.5** | *MergeSort 类定义。*

```cpp
// Fig. 19.6: MergeSort.cpp
// Class MergeSort member-function definition.
#include <iostream>
#include <vector>
#include <cstdlib> // prototypes for functions srand and rand
#include <ctime> // prototype for function time
#include "MergeSort.h" // class MergeSort definition
using namespace std;

// constructor fill vector with random integers
MergeSort::MergeSort( int vectorSize )
{
    size = ( vectorSize > 0 ? vectorSize : 10 ); // validate vectorSize
    srand( time( 0 ) ); // seed random number generator using current time

    // fill vector with random ints in range 10-99
    for ( int i = 0; i < size; ++i )
        data.push_back( 10 + rand() % 90 );
} // end MergeSort constructor

// split vector, sort subvectors and merge subvectors into sorted vector
void MergeSort::sort()
{
    sortSubVector( 0, size - 1 ); // recursively sort entire vector
} // end function sort

// recursive function to sort subvectors
void MergeSort::sortSubVector( int low, int high )
{
    // test base case; size of vector equals 1
    if ( ( high - low ) >= 1 ) // if not base case
    {
        int middle1 = ( low + high ) / 2; // calculate middle of vector
        int middle2 = middle1 + 1; // calculate next element over

        // output split step
        cout << "split:   ";
        displaySubVector( low, high );
        cout << endl << "       ";
        displaySubVector( low, middle1 );
        cout << endl << "       ";
```

**图 19.6** | *MergeSort 类成员函数定义。（第 1 部分，共 3 部分。）*

```cpp
// create object to perform merge sort
MergeSort sortVector(10);

cout << "Unsorted vector:" << endl;
sortVector.displayElements(); // print unsorted vector
cout << endl;

sortVector.sort(); // sort vector

cout << "Sorted vector:" << endl;
sortVector.displayElements(); // print sorted vector
cout << endl;
} // end of main
```

```
Unsorted vector:
30 47 22 67 79 18 60 78 26 54

split:   30 47 22 67 79 18 60 78 26 54
                    30 47 22 67 79
                                18 60 78 26 54

split:   30 47 22 67 79
          30 47 22
                    67 79

split:   30 47 22
          30 47
                22

split:   30 47
          30
             47

merge:   30
             47
          30 47

merge:   30 47
                22
          22 30 47

split:                67 79
                      67
                         79

merge:                67
                         79
                      67 79

merge:    22 30 47
                         67 79
          22 30 47 67 79

split:                18 60 78 26 54
                      18 60 78
                                   26 54
```

**图 19.7** | MergeSort 测试程序。（第 2 部分，共 3 部分。）

- 插入排序的第一次迭代取第二个元素的值，如果它小于第一个元素，则将其与第一个元素交换。第二次迭代查看第三个元素的值，并相对于前两个元素的值将其插入正确位置。插入排序的第 *j* 次迭代后，原始向量中的前 *j* 个元素值已排序。只需进行 *n* − 1 次迭代。
- 插入排序算法的运行时间为 *O(n²)*。

## 第 19.3.3 节 归并排序（递归实现）

- 归并排序（第 733 页）比选择排序和插入排序更快，但实现更复杂。
- 归并排序算法通过将向量拆分为两个大小相等的子向量、对每个子向量排序，并将这些子向量合并为一个更大的向量来对向量排序。
- 归并排序的基本情况是只含一个元素的向量。单元素向量已经有序，因此当以单元素向量调用归并排序时，它会立即返回。归并排序的合并部分取两个有序向量（这些可以是一元素向量），并将它们合并为一个更大的有序向量。
- 归并排序通过查看每个向量中的第一个元素（它也是该向量中最小的元素）来执行合并。归并排序取这些元素中最小的一个，并将其放入更大的有序向量的第一个元素中。如果子向量中仍有元素，归并排序查看该子向量中的第二个元素（现在它是剩余的最小元素），并将其与另一个子向量中的第一个元素进行比较。归并排序继续此过程，直到更大向量被填满。
- 在最坏情况下，第一次调用归并排序必须进行 *O(n)* 次比较，以填充最终向量中的 *n* 个槽位。
- 归并排序算法的合并部分在两个子向量上执行，每个子向量的大小约为 *n/2*。创建这些子向量中的每一个都需要对每个子向量进行 *n/2 − 1* 次比较，或总共 *O(n)* 次比较。这种模式继续下去，因为每一层处理的向量数量是上一层的两倍，但每个向量的大小是上一层的一半。
- 与二分查找类似，这种减半导致 log *n* 层，每层需要 *O(n)* 次比较，总效率为 *O(n log n)*（第 740 页）。

## 自测练习

1. **19.1** 填写下列各句中的空白：
   a) 选择排序应用程序在 128 个元素的向量上运行所需的时间大约是在 32 个元素的向量上运行所需时间的 __________ 倍。
   b) 归并排序的效率是 __________。
2. **19.2** 二分查找和归并排序的哪个关键方面解释了它们各自大 O 表示法中的对数部分？
3. **19.3** 插入排序在什么意义上优于归并排序？归并排序在什么意义上优于插入排序？
4. **19.4** 文中说，归并排序将向量拆分为两个子向量后，会对这两个子向量排序并合并它们。为什么有人可能会对我们“然后对这两个子向量排序”的说法感到困惑？

## 自测练习答案

**19.1** a) 16，因为 *O(n²)* 算法排序四倍信息量所需的时间是 16 倍。b) *O(n log n)*。
