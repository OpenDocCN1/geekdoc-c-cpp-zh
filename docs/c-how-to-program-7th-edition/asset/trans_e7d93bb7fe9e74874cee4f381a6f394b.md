
对向量的前半部分调用函数 `sortSubVector`，第 47 行则在向量的后半部分上递归调用函数 `sortSubVector`。当这两个函数调用返回时，向量的每一半都已排序。第 50 行对向量的两半调用函数 `merge`（第 55–99 行），将两个已排序的向量合并成一个更大的已排序向量。

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

**图 19.5** | MergeSort 类的定义。

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
   for ( int i = 0; i < size; i++ )
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
      cout << endl << "          ";
      displaySubVector( low, middle1 );
      cout << endl << "          ";
      displaySubVector( middle2, high );
      cout << endl << endl;

      // split vector in half; sort each half (recursive calls)
      sortSubVector( low, middle1 ); // first half of vector
      sortSubVector( middle2, high ); // second half of vector

      // merge two sorted vectors after split calls return
      merge( low, middle1, middle2, high );
   } // end if
} // end function sortSubVector

// merge two sorted subvectors into one sorted subvector
void MergeSort::merge( int left, int middle1, int middle2, int right )
{
   int leftIndex = left; // index into left subvector
   int rightIndex = middle2; // index into right subvector
   int combinedIndex = left; // index into temporary working vector
   vector< int > combined( size ); // working vector

   // output two subvectors before merging
   cout << "merge:   ";
   displaySubVector( left, middle1 );
   cout << endl << "          ";
   displaySubVector( middle2, right );
   cout << endl;

   // merge vectors until reaching end of either
   while ( leftIndex <= middle1 && rightIndex <= right )
   {
      // place smaller of two current elements into result
      // and move to next space in vector
      if ( data[ leftIndex ] <= data[ rightIndex ] )
         combined[ combinedIndex++ ] = data[ leftIndex++ ];
```

**图 19.6** | MergeSort 类成员函数的定义。（第 1 部分，共 3 部分）

右向量的末尾。如果左向量尚未到达末尾，那么右向量必然已经到达末尾，第 87–88 行将左向量的元素填入组合向量。最后，第 92–93 行将组合向量复制回原向量。图 19.7 创建并使用 `MergeSort` 对象。该程序的输出显示了归并排序所执行的分割和合并，展示了算法在每一步的排序进展。

## 归并排序的效率

归并排序是一种远比插入排序或选择排序高效的算法（尽管看到图 19.7 中相当杂乱的输出时，这可能难以令人相信）。考虑对函数 `sortSubVector` 的第一次（非递归）调用（第 24 行）。这会导致两次对函数 `sortSubVector` 的递归调用，每个子向量的大小约为原向量的一半，以及一次对函数 `merge` 的调用。对函数 `merge` 的此次调用在最坏情况下需要 *n* − 1 次比较来填充原向量，即 O(*n*)。（回想一下，每个向量元素都是通过比较两个子向量中各一个元素来选择的。）对函数 `sortSubVector` 的两次调用又会引发对函数 `sortSubVector` 的另外四次递归调用——每个子向量的大小约为原向量的四分之一——以及两次对函数 `merge` 的调用。对函数 `merge` 的这两次调用在最坏情况下各自需要 *n*/2 − 1 次比较，因此比较的总数为 O(*n*)。这个过程持续进行，每次调用 `sortSubVector` 都会产生两次额外的对 `sortSubVector` 的调用和一次对 `merge` 的调用，直到算法将向量分割成单元素子向量。在每一层上，合并子向量都需要 O(*n*) 次比较。每一层都将向量的大小减半，因此向量大小加倍需要增加一层，扩大为四倍需要增加两层。这种模式是对数式的，会产生 log₂ *n* 层。因此总效率为 O(*n* log *n*)。

```cpp
// Fig. 19.7: Fig19_07.cpp
// MergeSort test program.
#include <iostream>
#include "MergeSort.h" // class MergeSort definition
using namespace std;

int main()
{
   // create object to perform merge sort
   MergeSort sortVector( 10 );

   cout << "Unsorted vector:" << endl;
   sortVector.displayElements(); // print unsorted vector
   cout << endl;

   sortVector.sort(); // sort vector

   cout << "Sorted vector:" << endl;
   sortVector.displayElements(); // print sorted vector
   cout << endl;
} // end main
```

**图 19.7** | MergeSort 测试程序。（第 1 部分，共 3 部分）

```
Unsorted vector:
   30 47 22 67 79 18 60 78 26 54

split:       30 47 22 67 79 18 60 78 26 54
             30 47 22 67 79
                         18 60 78 26 54

split:       30 47 22 67 79
             30 47 22
                      67 79

split:       30 47 22
             30 47
                22

split:       30 47
             30
                47

merge:       30
             47
             30 47

merge:       30 47
                22
             22 30 47

split:                67 79
                      67
                         79

merge:                67
                      79
                      67 79

merge:       22 30 47
                      67 79
             22 30 47 67 79

split:                      18 60 78 26 54
                            18 60 78
                                     26 54

split:                      18 60 78
                            18 60
                               78

split:                      18 60
                            18
                               60

merge:                      18
                            60
                            18 60

merge:                      18 60
                                  78
                            18 60 78
```

**图 19.7** | MergeSort 测试程序。（第 2 部分，共 3 部分）
