
现在假设你有一个算法，用于测试向量中是否有任何元素在向量的其他地方重复出现。第一个元素必须与向量中的其他每个元素进行比较。第二个元素必须与除第一个元素之外的每个其他元素进行比较（它已经与第一个元素比较过了）。第三个元素必须与除前两个元素之外的每个其他元素进行比较。最终，这个算法将进行 (n − 1) + (n − 2) + ... + 2 + 1 次比较，即 n²/2 − n/2 次比较。随着 n 增大，n² 项占主导地位，而 n 项变得无关紧要。同样，大 O 表示法突出 n² 项，留下 n²/2。然而，我们很快会看到，在大 O 表示法中常数因子会被省略。

大 O 关注的是算法的运行时间相对于所处理项目数量的增长方式。假设一个算法需要 n² 次比较。对于四个元素，该算法将需要 16 次比较；对于八个元素，需要 64 次比较。对于这个算法，元素数量翻倍会使比较次数变为四倍。考虑一个类似的算法，它需要 n²/2 次比较。对于四个元素，该算法将需要八次比较；对于八个元素，需要 32 次比较。同样，元素数量翻倍会使比较次数变为四倍。这两个算法都按 n 的平方增长，因此大 O 忽略常数，并且这两个算法都被认为是 O(n²)，这被称为二次运行时间，读作“按 n 的平方量级”或更简单地说“n 平方阶”。

当 n 很小时，O(n²) 算法（在当今每秒执行十亿次运算的个人计算机上运行）不会明显影响性能。但随着 n 增大，你就会开始注意到性能下降。一个在百万元素向量上运行的 O(n²) 算法将需要一万亿次“操作”（其中每次操作实际上可能需要执行若干条机器指令）。这可能需要几个小时才能执行完。而一个十亿元素向量将需要一百亿亿次操作，这个数字如此之大，以至于该算法可能需要几十年！不幸的是，O(n²) 算法往往很容易编写。在本章中，你将看到具有更有利大 O 度量的算法。这些高效算法通常需要多一点聪明才智和努力来创建，但它们的卓越性能可能值得付出额外的努力，尤其是当 n 变大以及算法被组合到更大的程序中时。

线性查找算法以 O(n) 时间运行。该算法的最坏情况是必须检查每个元素，以确定查找关键字是否存在于向量中。如果向量的大小翻倍，算法必须执行的比较次数也会翻倍。如果与查找关键字匹配的元素恰好位于向量前部或靠近前部，线性查找可以提供出色的性能。但我们寻求的是在所有查找中平均表现良好的算法，包括与查找关键字匹配的元素位于向量末尾附近的情况。

线性查找是最容易实现的查找算法，但与其他查找算法相比，它可能较慢。如果程序需要在大型向量上执行许多次查找，那么实现另一种更高效的算法可能更好，例如我们将在下一节介绍的二分查找。

## 性能提示 19.1

*有时最简单的算法性能很差。它们的优点在于易于编程、测试和调试。有时需要更复杂的算法才能实现最高性能。*

![](img/023f159fdd47d944d48e08843cea732d_823_0.png)

```cpp
1  // Fig. 19.2: BinarySearch.h
2  // Class that contains a vector of random integers and a function
3  // that uses binary search to find an integer.
4  #include <vector>
5  using namespace std;
6
7  class BinarySearch
8  {
9  public:
10     BinarySearch( int ); // constructor initializes vector
11     int binarySearch( int ) const; // perform a binary search on vector
12     void displayElements() const; // display vector elements
13  private:
14     int size; // vector size
15     vector< int > data; // vector of ints
16     void displaySubElements( int, int ) const; // display range of values
17  }; // end class BinarySearch
```

图 19.2 | BinarySearch 类定义。

```cpp
1  // Fig. 19.3: BinarySearch.cpp
2  // BinarySearch class member-function definition.
3  #include <iostream>
4  #include <cstdlib> // prototypes for functions srand and rand
5  #include <ctime> // prototype for function time
6  #include <algorithm> // prototype for sort function
7  #include "BinarySearch.h" // class BinarySearch definition
8  using namespace std;
9
10 // constructor initializes vector with random ints and sorts the vector
11 BinarySearch::BinarySearch( int vectorSize )
12 {
13     size = ( vectorSize > 0 ? vectorSize : 10 ); // validate vectorSize
14     srand( time( 0 ) ); // seed using current time
15
16     // fill vector with random ints in range 10-99
17     for ( int i = 0; i < size; i++ )
18         data.push_back( 10 + rand() % 90 ); // 10-99
19
20     std::sort( data.begin(), data.end() ); // sort the data
21 } // end BinarySearch constructor
22
23 // perform a binary search on the data
24 int BinarySearch::binarySearch( int searchElement ) const
25 {
26     int low = 0; // low end of the search area
27     int high = size - 1; // high end of the search area
28     int middle = ( low + high + 1 ) / 2; // middle element
29     int location = -1; // return value; -1 if not found
30
31     do // loop to search for element
32     {
```

图 19.3 | BinarySearch 类成员函数定义。（第 1 部分，共 2 部分。）

调用者。循环的每次迭代测试一个值（第 43 行），并排除向量中剩余值的一半（第 46 行或第 48 行）。

图 19.4 的第 22–38 行循环，直到用户输入值 -1。对于用户输入的每个其他数字，程序都会对数据执行二分查找，以确定它是否与向量中的某个元素匹配。该程序输出的第一行是按递增顺序排列的整数向量。当用户指示程序查找 38 时，程序首先测试中间元素，即 67（由 * 指示）。查找关键字小于 67，因此程序排除向量的后半部分，并测试向量前半部分的中间元素。查找关键字等于 38，因此程序返回索引 3。

```cpp
1  // Fig. 19.4: Fig19_04.cpp
2  // BinarySearch test program.
3  #include <iostream>
4  #include "BinarySearch.h" // class BinarySearch definition
5  using namespace std;
6
7  int main()
8  {
9     int searchInt; // search key
10    int position; // location of search key in vector
11
12    // create vector and output it
13    BinarySearch searchVector( 15 );
14    searchVector.displayElements();
15
16    // get input from user
17    cout << "\nPlease enter an integer value (-1 to quit): ";
18    cin >> searchInt; // read an int from user
19    cout << endl;
20
21    // repeatedly input an integer; -1 terminates the program
22    while ( searchInt != -1 )
23    {
24       // use binary search to try to find integer
25       position = searchVector.binarySearch( searchInt );
26
27       // return value of -1 indicates integer was not found
28       if ( position == -1 )
29          cout << "The integer " << searchInt << " was not found.\n";
30       else
31          cout << "The integer " << searchInt
32               << " was found in position " << position << ".\n";
33
34       // get input from user
35       cout << "\n\nPlease enter an integer value (-1 to quit): ";
36       cin >> searchInt; // read an int from user
37       cout << endl;
38    } // end while
39 } // end main
```

图 19.4 | BinarySearch 测试程序。（第 1 部分，共 2 部分。）
