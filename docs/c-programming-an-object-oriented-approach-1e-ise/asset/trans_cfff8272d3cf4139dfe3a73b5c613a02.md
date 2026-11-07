
![](img/d68f6199646ca63591a6d8419e0ed4ba_878_0.png)

**注释：**

`begin()` 函数返回一个指向第一个元素的普通迭代器。

`end()` 函数返回一个指向最后一个元素之后的不存在元素的普通迭代器。

`rbegin()` 函数返回一个指向最后一个元素的反向迭代器。

`rend()` 函数返回一个指向第一个元素之前的不存在元素的反向迭代器。

这两种迭代器都是随机访问迭代器，可以向前和向后跳跃。

**图 19.6** 向量中的迭代器和反向迭代器

```cpp
iter = vec.begin();                 // iter starts when the vec.begin() points to
riter = vec.rbegin();               // riter starts when the vec.rbegin() points to
```

我们创建一个大小为 10 的向量，并使用普通迭代器和反向迭代器访问元素（程序 19.1）。

## 程序 19.1 测试向量中的迭代器

```cpp
/**************************************************************
 * A simple program to test regular and reverse navigation      *
 **************************************************************/
#include <vector>
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    // Constructing a vector of 10 elements and two iterators
    vector<int> vec(10);
    vector<int>::iterator iter;
    vector<int>::reverse_iterator rIter;
    // Changing the value of elements
    for (int i = 0; i < 10; i++)
    {
        vec.at(i) = i * i;
    }
    // Printing the elements using the forward iterator
    cout << "Regular navigation: ";
    for (iter = vec.begin(); iter != vec.end(); ++iter)
    {
        cout << setw(4) << *iter;
    }
```

*（续）*

## 程序 19.2 展示迭代器的随机访问特性（续）

```cpp
vector <int>::iterator iter1;
vector <int>::reverse_iterator iter2;
// Filling the vector with 10 elements
for (int i = 0; i < 10; i++)
{
    vec.push_back(i * 10);
}
// Using the regular iterator to print 40 followed by 20
cout << "Printing 40 followed by 20" << endl;
iter1 = vec.begin();
iter1 += 4;
cout << *iter1 << " ";
iter1 -= 2;
cout << *iter1 << endl;
// Using the reverse iterator to print 70 followed by 50
cout << "Printing 50 followed by 70" << endl;
iter2 = vec.rbegin();
iter2 += 4;
cout << *iter2 << " ";
iter2 -= 2;
cout << *iter2 << endl;
return 0;
}
```

```text
Run:
Printing 40 followed by 20
40  20
Printing 50 followed by 70
50  70
```

图 19.7 展示了普通迭代器和反向迭代器如何在向量中随机地向前和向后移动。

![](img/d68f6199646ca63591a6d8419e0ed4ba_880_0.png)

**图 19.7** 普通迭代器和反向迭代器在向量中的移动

### 插入

vector 类定义了几个成员函数，用于向容器中插入一个或多个元素。在尾部插入非常高效，并且不需要重新定位向量中的元素。在中间和前端插入则需要在内存中重新分配元素。下面展示如何使用成员函数向向量中插入新元素。注意，最后一个示例将元素从第一个复制到倒数第二个元素。

```cpp
vec.push_back(value);                  // Insert value at the back
vec.insert(pos, value);                 // Insert value before pos
vec.insert(pos, n, value);              // Insert n copies of value before pos
vec.insert(pos, first, last);           // Insert elements [first, last) before pos
```

*pos* 参数是已定义迭代器所指向的位置。*first* 和 *last* 参数是定义范围 [first, last) 的输入迭代器。它们可用于复制宿主向量或另一个容器中的元素。

### 删除

vector 类定义了几个成员函数，用于删除容器中的一个或多个元素。在尾部删除非常高效，并且不需要重新分配任何元素。从中间或前端删除需要重新分配内存，应尽量避免。下面展示可用于从向量中删除元素的成员函数。

```cpp
vec.pop_back();                       // Erase the back (last) element
vec.erase(pos);                         // Erase the element before pos
vec.erase(first, second);               // Erase all the elements in the range [first, last)
vec.clear();                             // Erase all elements
```

## 应用

vector 类的设计使其看起来像一个数组。它具有与数组相同的功能，但也有一些优点。首先，vector 是一个具有内置类型操作的类。其次，它分配在堆中，并可按需调整大小。第三，它具有定义良好的迭代器机制，允许我们访问、插入和删除元素。总之，每当需要数组时，我们都可以使用 vector，并受益于它的优点。

在第 8 章中，我们学习了如何使用二维数组。使用 vector 也可以做到这一点。我们可以创建一个二维向量，即向量的向量。向量的向量相对于二维数组的优势，与 vector 相对于一维数组的优势相同。在程序 19.3 中，我们创建一个二维向量，用来模拟小学教授的乘法表。为了理解实例化，我们逐步展示如何编写二维向量的定义代码。

```cpp
vector <type> table(rows, value);
vector <vector <int> > table(rows, value);
vector <vector <int> > table(rows, vector <int>(cols));
```

在第一行中，我们定义一个名为 *table* 的向量，包含 rows 个元素，每个元素都初始化为 *value*。在第二行中，我们看到 table 的类型是整数向量。在第三行中，我们看到每一行的值都是一个整数类型的向量，并且有 *cols* 个这样的向量。注意，两个符号（> >）之间需要一个空格，以表明该组合不是 >> 运算符。

## 程序 19.3 向量的向量（表）

```cpp
/*******************************************************
 * A program to simulate a table using a vector of vectors *
 *******************************************************/
#include <vector>
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    // Creation of a vector of vectors
    int rows = 10;
    int cols = 10;
    vector < vector <int> > table(rows, vector <int>(cols));
    // Changing values from default
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            table[i][j] = (i + 1) * (j + 1);
        }
    }
    // Retrieving and printing values
    for (int i = 0; i < rows; i++)
    {
        for (int j = 0; j < cols; j++)
        {
            cout << setw(4) << table[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}
```

运行：

|  |  |  |  |  |  |  |  |  |  |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 |
| 3 | 6 | 9 | 12 | 15 | 18 | 21 | 24 | 27 | 30 |
| 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 |
| 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 | 45 | 50 |
| 6 | 12 | 18 | 24 | 30 | 36 | 42 | 48 | 54 | 60 |
| 7 | 14 | 21 | 28 | 35 | 42 | 49 | 56 | 63 | 70 |
| 8 | 16 | 24 | 32 | 40 | 48 | 56 | 64 | 72 | 80 |
| 9 | 18 | 27 | 36 | 45 | 54 | 63 | 72 | 81 | 90 |
| 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 | 90 | 100 |

在第 8 章中，我们使用不规则数组来创建多项式 (x + y)^n 的系数。现在我们使用向量的向量来解决这个问题（程序 19.4）。

## 程序 19.4 使用不规则向量创建帕斯卡三角形

```cpp
1 /************************************************************
2  * A program to print Pascal coefficients                  *
3  ************************************************************/
4 #include <vector>
5 #include <iostream>
6 #include <iomanip>
7 using namespace std;
8
9 int main()
10 {
11     // Declaration
12     int power = 5;
13     vector < vector <int> > pascal(power + 1, vector <int>());
14     // Creation of ragged vector
15     for (int i = 0; i <= power; i++)
16     {
17         for (int j = 0; j < i + 1; j++)
18         {
19             pascal[i].push_back(0);
20         }
21     }
22     // Filling ragged table to create a Pascal triangle
23     for (int i = 0; i <= power; i++)
24     {
25         for (int j = 0; j < i + 1; j++)
26         {
27             if (j == 0 || i == j)
28             {
29                 pascal[i][j] = 1;
30             }
31             else
32             {
33                 pascal[i][j] = pascal[i-1][j-1] + pascal[i-1][j];
34             }
35         }
36     }
37     // Printing the triangle
38     for (int i = 0; i <= power; i++)
39     {
40         cout << "Coefficients of (x + y)^" << i << " ====> ";
41         for (int j = 0; j < i + 1; j++)
```
