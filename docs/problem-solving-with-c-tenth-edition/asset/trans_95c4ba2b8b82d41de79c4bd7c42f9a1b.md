

## DISPLAY 14.5 二分搜索的伪代码

```
int a[Some_Size_Value];
```

搜索 a[first] 到 a[last] 的算法

```
1    //Precondition:
2    //a[first]<= a[first + 1] <= a[first + 2] <= ... <= a[last]
```

定位值 key：

```
1    if (first > last) //A stopping case
2        found = false;
3    else
4    {
5        mid = approximate midpoint between first and last;
6        if (key == a[mid]) //A stopping case
7        {
8            found = true;
9            location = mid;
10       }
11       else if key < a[mid] //A case with recursion
12           search a[first] through a[mid - 1];
13       else if key > a[mid] //A case with recursion
14           search a[mid + 1] through a[last];
15   }
```

## DISPLAY 14.6 二分搜索的递归函数（第 1 部分，共 2 部分）

```
1    //Program to demonstrate the recursive function for binary search.
2    #include <iostream>
3    using namespace std;
4    const int ARRAY_SIZE = 10;
5
6
7    void search(const int a[], int first, int last,
8        int key, bool& found, int& location);
9    //Precondition: a[first] through a[last] are sorted in increasing order.
10   //Postcondition: if key is not one of the values a[first] through a[last],
11   //then found == false; otherwise, a[location] == key and found == true.
12
13
14   int main()
15   {
16       int a[ARRAY_SIZE];
17       const int finalIndex = ARRAY_SIZE - 1;
```

(continued)

## DISPLAY 14.6 二分搜索的递归函数（第 2 部分，共 2 部分）

< This portion of the program contains some code to fill and sort the array a. The exact details are irrelevant to this example. >

```
19    int key, location;
20    bool found;
21    cout << "Enter number to be located: ";
22    cin >> key;
23    search(a, 0, finalIndex, key, found, location);
24
25    if (found)
26        cout << key << " is in index location "
27           << location << endl;
28    else
29        cout << key << " is not in the array." << endl;
30
31    return 0;
32 }
33 void search(const int a[], int first, int last,
34                int key, bool& found, int& location)
35 {
36    int mid;
37    if (first > last)
38    {
39        found = false;
40    }
41    else
42    {
43        mid = (first + last)/2;
44
45        if (key == a[mid])
46        {
47            found = true;
48            location = mid;
49        }
50        else if (key < a[mid])
51        {
52            search(a, first, mid -1, key, found, location);
53        }
54        else if (key > a[mid])
55        {
56            search(a, mid + 1, last, key, found, location);
57        }
58    }
59 }
```

## DISPLAY 14.7 函数 search 的执行

key is 63

a[0] 15
 a[1] 20
 a[2] 35
 a[3] 41
 a[4] 57
 a[5] 63
 a[6] 75
 a[7] 80
 a[8] 85
 a[9] 90
 first == 0
 mid = (0 + 9)/2
 last == 9
 Next

a[0] 15
 a[1] 20
 a[2] 35 Not in this half
 a[3] 41
 a[4] 57
 a[5] 63 first == 5
 a[6] 75
 a[7] 80 mid = (5 + 9)/2
 a[8] 85
 a[9] 90 last == 9

a[0] 15
 a[1] 20
 a[2] 35
 a[3] 41
 a[4] 57
 a[5] 63 first == 5
 a[6] 75 last == 6
 a[7] 80
 a[8] 85
 a[9] 90
 Not here
 Next

mid = (5 + 6)/2 which is 5
 a[mid] is a[5] == 63
 found = true;
 location = mid;

## 求解更一般的问题

请注意，函数 search 解决的问题比原始任务更一般。我们的目标是设计一个函数来搜索整个数组。然而该函数允许我们通过指定索引边界 first 和 last 来搜索数组的任意区间。这在设计递归函数时很常见。经常有必要求解一个更一般的问题，以便能够表达递归算法。在本例中，我们只希望在 first 和 last 分别设为 0 和 finalIndex 的情况下得到答案。然而递归调用会将它们设为 0 和 finalIndex 以外的其他值。

## 检查递归

在标题为“递归设计技术”的小节中，我们给出了三个准则，用于确保递归 void 函数定义是正确的。让我们对 DISPLAY 14.6 中给出的函数 search 检查这三件事。

- 1. 没有无限递归：在每次递归调用中，first 的值会增加或 last 的值会减小。如果递归调用链没有以其他方式结束，那么最终函数将被调用时 first 大于 last，而这是一个停止情况。

- 2. 每个停止情况都执行该情况的正确操作：有两个停止情况：当 first > last 时以及当 key==a[mid] 时。让我们分别考虑每种情况。
  
  如果 first > last，则 a[first] 和 a[last] 之间没有数组元素，因此 key 不在该数组段中。 （该数组段中没有任何内容！）因此，如果 first > last，函数 search 正确地将 found 设为 false。
  
  如果 key==a[mid]，算法正确地将 found 设为 true 并将 location 设为 mid。因此，两个停止情况都是正确的。

- 3. 对于涉及递归的每种情况，如果所有递归调用都正确执行其操作，则整个情况执行正确：有两种涉及递归调用的情况：当 key < a[mid] 时以及当 key > a[mid] 时。我们需要检查这两种情况。

首先假设 key < a[mid]。在这种情况下，由于数组已排序，我们知道如果 key 在数组中的话，则 key 是 a[first] 到 a[mid-1] 之一的元素。因此，函数只需搜索这些元素，这正是递归调用

```
search(a, first, mid - 1, key, found, location);
```

所做的。因此如果递归调用是正确的，则整个操作是正确的。

接下来，假设 key > a[mid]。在这种情况下，由于数组已排序，我们知道如果 key 在数组中的话，则 key 是 a[mid+1] 到 a[last] 之一的元素。因此，函数只需搜索这些元素，这正是递归调用

```
search(a, mid + 1, last, key, found, location);
```

所做的。因此如果递归调用是正确的，则整个操作是正确的。因此，在这两种情况下，函数都执行正确的操作（假设递归调用执行正确的操作）。

函数 search 通过了我们所有的三个测试，因此它是一个良好的递归函数定义。

## 效率

与简单地按顺序尝试所有数组元素的算法相比，二分搜索算法极快。在二分搜索中，你在开始时就将大约一半的数组从考虑中排除。然后你排除四分之一，然后是八分之一，等等。这些节省累积起来形成了一个非常快的算法。对于包含 100 个元素的数组，二分搜索永远不需要将超过 7 个数组元素与 key 进行比较。简单的串行搜索可能需要将多达 100 个数组元素与 key 进行比较，平均而言会比较约 50 个数组元素与 key。此外，数组越大，节省就越显著。在包含 1000 个元素的数组上，二分搜索只需要比较大约 10 个数组元素与 key 值，而简单的串行搜索算法平均为 500。

函数 search 的迭代版本在 DISPLAY 14.8 中给出。在某些系统上，迭代版本比递归版本运行更高效。迭代版本的算法是通过镜像递归版本得出的。在迭代版本中，局部变量 first 和 last 镜像了递归版本中参数的作用，这些参数也命名为 first 和 last。正如本例所示，即使你期望稍后将其转换为迭代算法，设计递归算法也通常是有意义的。

迭代版本

## DISPLAY 14.8 二分搜索的迭代版本（第 1 部分，共 2 部分）

### 函数声明

```
1   void search(const int a[], int lowEnd, int highEnd,
2   int key, bool& found, int& location);
3   //Precondition: a[lowEnd] through a[highEnd] are sorted in increasing
4   //order.
5   //Postcondition: If key is not one of the values a[lowEnd] through
6   //a[highEnd], then found == false; otherwise, a[location] == key and
7   //found == true.
```

### 函数定义

```
1   void search(const int a[], int lowEnd, int highEnd,
2     int key, bool& found, int& location)
3   {
4     int first = lowEnd;
5     int last = highEnd;
```

(continued)

