

# 12 • 数组的搜索与排序 357

```cpp
for(i = 0; i < SIZE; i++)
{
    std::cout << "Enter number: ";
    std::cin >> a[i];
}
bubble_sort(a);

std::cout << "\n***** 后的数组 *****\n";
for(i = 0; i < SIZE; i++)
    std::cout << a[i] << '\n';

return 0;
```

```cpp
void bubble_sort(int arr[])
{
    bool reorder;
    int i, j, temp;
    for(i = 1; i < SIZE; i++)
    {
        reorder = 0;
        for(j = SIZE-1; j >= i; j--)
        {
            if(arr[j] < arr[j-1])
            {
                // 交换值。
                temp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = temp;
                reorder = 1;
            }
        }
        if(reorder == 0)
            return;
    }
}
```

**注释：** `reorder` 变量检查排序是否已完成以避免不必要的迭代。如果交换了两个元素，它被设置为 1。否则，值 0 表示数组已排序完毕，函数终止。为了查看算法如何工作，假设数组元素为：10, 9, 4, 7, 6。

外层 **for**(i = 1) 的第一次迭代：

| 内层 **for**(j = 4) 的第一次迭代: 10 | 9 | 4 | 6 <-> 7 |
| 内层 **for**(j = 3) 的第二次迭代: 10 | 9 | 4 | 6 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 10 | 4 <-> 9 | 6 | 7 |
| 内层 **for**(j = 1) 的第四次迭代: 10 | 6 <-> 10 | 9 | 7 |

因此，数组转换为：4 10 9 6 7

| 外层 **for**(i = 2) 的第二次迭代: 4 | 10 | 9 | 6 | 7 |
| 内层 **for**(j = 3) 的第二次迭代: 4 | 10 | 6 <-> 9 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 4 | 6 <-> 10 | 9 | 7 |

# C++ 简介

因此，数组转换为：4 6 10 9 7

外层 for(i = 3) 的第三次迭代: 4
内层 for(j = 4) 的第一次迭代: 6 10 7 <-- 9
内层 for(j = 3) 的第二次迭代: 6 7 <-- 10 9

因此，数组转换为：4 6 7 10 9

外层 for(i = 4) 的第四次迭代
内层 for(j = 4) 的第一次迭代: 4 6 7 10 <-- 9

排序完成，数组转换为：4 6 7 9 10
若要降序排序数组，我们只需更改 if 语句：

```cpp
if (arr[j] > arr[j-1])
```

C.12.11 编写一个程序，读取 50 个国家的名称（每个少于 100 个字符）以及每月访问这些游客人数。程序应使用适当的数组来存储数据。然后，程序应读取一个国家名称并显示访问该国家的年度游客人数。程序在结束前显示访问最多的国家（检查是否有多个一个国家并列第五位）。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

const int CNTRS = 50;
const int MONTHS = 12;

void bubble_sort(char str[] [100], int arr[]);

int main() {
    bool flag;
    char cntr[CNTRS][100], str[100];
    int i, j, tmp, tour[CNTRS] = {0};

    for(i = 0; i < CNTRS; i++) {
        cout << "Enter name of country_ " << i + 1 << ": ";
        cin.getline(cntr[i], sizeof(cntr[i]));
        for(j = 0; j < MONTHS; j++) {
            cout << "Enter tourists of month_ " << j + 1 << ": ";
            cin >> tmp;
            tour[i] += tmp; /* 此数组存储每个国家的年度游客人数。 */
        }
        cin.get();
    }
    cout << "Enter country to search: ";
    cin.getline(str, sizeof(str));
```

```cpp
flag = 0;
for(i = 0; i < CNTRS; i++)
{
    if(strcmp(str, cntr[i]) == 0)
    {
        flag = 1;
        cout << tour[i] << " tourists visited " << str << "\n";
    }
}
if(flag == 0)
    cout << str << " not registered\n";
```

```cpp
bubble_sort(cntr, tour); /* 对排序游客数组进行排序并同步更新国家。 */
cout << "\n***** 降序的游客 *****\n";
for(i = 0; i < 5; i++)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
}
```

```cpp
// 检查是否有多个国家并列第五位。
while((tour[i] == tour[4]) && i < CNTRS)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
    i++;
}
return 0;
```

```cpp
void bubble_sort(char str[100], int arr[])
{
    bool reorder;
    char temp[100];
    int i, j, k;

    for(i = 1; i < SIZE; i++)
    {
        reorder = 0;
        for(j = SIZE-1; j >= i; j--)
        {
            if(arr[j] < arr[j-1])
            {
                // 交换值。
                temp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = temp;
                reorder = 1;
            }
        }
        if(reorder == 0)
            return;
    }
}
```

**注释：** `reorder` 变量检查排序是否已完成以避免不必要的迭代。如果交换了两个元素，它被设置为 1。否则，值 0 表示数组已排序完毕，函数终止。为了查看算法如何工作，假设数组元素为：10, 9, 4, 7, 6。

外层 **for**(i = 1) 的第一次迭代：

| 内层 **for**(j = 4) 的第一次迭代: 10 | 9 | 4 | 6 <-> 7 |
| 内层 **for**(j = 3) 的第二次迭代: 10 | 9 | 4 | 6 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 10 | 4 <-> 9 | 6 | 7 |
| 内层 **for**(j = 1) 的第四次迭代: 10 | 6 <-> 10 | 9 | 7 |

因此，数组转换为：4 10 9 6 7

| 外层 **for**(i = 2) 的第二次迭代: 4 | 10 | 9 | 6 | 7 |
| 内层 **for**(j = 3) 的第二次迭代: 4 | 10 | 6 <-> 9 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 4 | 6 <-> 10 | 9 | 7 |

# C++ 简介 

因此，数组转换为：4 6 10 9 7

外层 for(i = 3) 的第三次迭代: 4
内层 for(j = 4) 的第一次迭代: 6 10 7 <-- 9
内层 for(j = 3) 的第二次迭代: 6 7 <-- 10 9

因此，数组转换为：4 6 7 10 9

外层 for(i = 4) 的第四次迭代
内层 for(j = 4) 的第一次迭代: 4 6 7 10 <-- 9

排序完成，数组转换为：4 6 7 9 10
若要降序排序数组，我们只需更改 if 语句：

```cpp
if (arr[j] > arr[j-1])
```

C.12.11 编写一个程序，读取 50 个国家的名称（每个少于 100 个字符）以及每月访问这些游客人数。程序应使用适当的数组来存储数据。然后，程序应读取一个国家名称并显示访问该国家的年度游客人数。程序在结束前显示访问最多的国家（检查是否有多个国家并列第五位）。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

const int CNTRS = 50;
const int MONTHS = 12;

void bubble_sort(char str[] [100], int arr[]);

int main() {
    bool flag;
    char cntr[CNTRS][100], str[100];
    int i, j, tmp, tour[CNTRS] = {0};

    for(i = 0; i < CNTRS; i++) {
        cout << "Enter name of country_ " << i + 1 << ": ";
        cin.getline(cntr[i], sizeof(cntr[i]));
        for(j = 0; j < MONTHS; j++) {
            cout << "Enter tourists of month_ " << j + 1 << ": ";
            cin >> tmp;
            tour[i] += tmp; /* 此数组存储每个国家的年度游客人数。 */
        }
        cin.get();
    }
    cout << "Enter country to search: ";
    cin.getline(str, sizeof(str));
```

```cpp
flag = 0;
for(i = 0; i < CNTRS; i++)
{
    if(strcmp(str, cntr[i]) == 0)
    {
        flag = 1;
        cout << tour[i] << " tourists visited " << str << "\n";
    }
}
if(flag == 0)
    cout << str << " not registered\n";
```

```cpp
bubble_sort(cntr, tour); /* 对游客数组进行排序并同步更新国家。 */
cout << "\n***** 降序的游客 *****\n";
for(i = 0; i < 5; i++)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
}
```

```cpp
// 检查是否有多个国家并列第五位。
while((tour[i] == tour[4]) && i < CNTRS)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
    i++;
}
return 0;
```

```cpp
void bubble_sort(char str[100], int arr[])
{
    bool reorder;
    char temp[100];
    int i, j, k;

    for(i = 1; i < SIZE; i++)
    {
        reorder = 0;
        for(j = SIZE-1; j >= i; j--)
        {
            if(arr[j] < arr[j-1])
            {
                // 交换值。
                temp = arr[j];
                arr[j] = arr[j-1];
                arr[j-1] = temp;
                reorder = 1;
            }
        }
        if(reorder == 0)
            return;
    }
}
```

**注释：** `reorder` 变量检查排序是否已完成以避免不必要的迭代。如果交换了两个元素，它被设置为 1。否则，值 0 表示数组已排序完毕，函数终止。为了查看算法如何工作，假设数组元素为：10, 9, 4, 7, 6。

外层 **for**(i = 1) 的第一次迭代：

| 内层 **for**(j = 4) 的第一次迭代: 10 | 9 | 4 | 6 <-> 7 |
| 内层 **for**(j = 3) 的第二次迭代: 10 | 9 | 4 | 6 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 10 | 4 <-> 9 | 6 | 7 |
| 内层 **for**(j = 1) 的第四次迭代: 10 | 6 <-> 10 | 9 | 7 |

因此，数组转换为：4 10 9 6 7

| 外层 **for**(i = 2) 的第二次迭代: 4 | 10 | 9 | 6 | 7 |
| 内层 **for**(j = 3) 的第二次迭代: 4 | 10 | 6 <-> 9 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 4 | 6 <-> 10 | 9 | 7 |

# C++ 简介 

因此，数组转换为：4 6 10 9 7

外层 for(i = 3) 的第三次迭代: 4
内层 for(j = 4) 的第一次迭代: 6 10 7 <-- 9
内层 for(j = 3) 的第二次迭代: 6 7 <-- 10 9

因此，数组转换为：4 6 7 10 9

外层 for(i = 4) 的第四次迭代
内层 for(j = 4) 的第一次迭代: 4 6 7 10 <-- 9

排序完成，数组转换为：4 6 7 9 10
若要降序排序数组，我们只需更改 if 语句：

```cpp
if (arr[j] > arr[j-1])
```

C.12.11 编写一个程序，读取 50 个国家的名称（每个少于 100 个字符）以及每月访问这些游客人数。程序应使用适当的数组来存储数据。然后，程序应读取一个国家名称并显示访问该国家的年度游客人数。程序在结束前显示访问最多的国家（检查是否有多个国家并列第五位）。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

const int CNTRS = 50;
const int MONTHS = 12;

void bubble_sort(char str[] [100], int arr[]);

int main() {
    bool flag;
    char cntr[CNTRS][100], str[100];
    int i, j, tmp, tour[CNTRS] = {0};

    for(i = 0; i < CNTRS; i++) {
        cout << "Enter name of country_ " << i + 1 << ": ";
        cin.getline(cntr[i], sizeof(cntr[i]));
        for(j = 0; j < MONTHS; j++) {
            cout << "Enter tourists of month_ " << j + 1 << ": ";
            cin >> tmp;
            tour[i] += tmp; /* 此数组存储每个国家的年度游客人数。 */
        }
        cin.get();
    }
    cout << "Enter country to search: ";
    cin.getline(str, sizeof(str));
```

```cpp
flag = 0;
for(i = 0; i < CNTRS; i++)
{
    if(strcmp(str, cntr[i]) == 0)
    {
        flag = 1;
        cout << tour[i] << " tourists visited " << str << "\n";
    }
}
if(flag == 0)
    cout << str << " not registered\n";
```

```cpp
bubble_sort(cntr, tour); /* 对游客数组进行排序并同步更新国家。 */
cout << "\n***** 降序的游客 *****\n";
for(i = 0; i < 5; i++)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
}
```

```cpp
// 检查是否有多个国家并列第五位。
while((tour[i] == tour[4]) && i < CNTRS)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
    i++;
}
return 0;
```

```cpp
void bubble_sort(char str[100], int arr[])
{
    bool reorder;
    char temp[100];
    int i, j, k;

    for(i = 1; i < SIZE; i++)
    {
        reorder = 0;
```

# 快速排序算法

快速排序是一种分治治算法。它的思想是选择一个元素作为基准，并将数组分为两个子数组，一个包含小于基元的元素，另一个包含大于基准的元素。这个过程对两个子数组递归进行。

有几种方法可以选择基准：
- 第一个元素
- 最后一个元素
- 中间元素
- 随机元素

在这个例子中，我们使用最后一个元素作为基准。

（此处省略了后续重复的文本部分）

**注释：** `reorder` 变量检查排序是否已完成以避免不必要的迭代。如果交换了两个元素，它被设置为 1。否则，值 0 表示数组已排序完毕，函数终止。为了查看算法如何工作，假设数组元素为：10, 9, 4, 7, 6。

外层 **for**(i = 1) 的第一次迭代：

| 内层 **for**(j = 4) 的第一次迭代: 10 | 9 | 4 | 6 <-> 7 |
| 内层 **for**(j = 3) 的第二次迭代: 10 | 9 | 4 | 6 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 10 | 4 <-> 9 | 6 | 7 |
| 内层 **for**(j = 1) 的第四次迭代: 10 | 6 <-> 10 | 9 | 7 |

因此，数组转换为：4 10 9 6 7

| 外层 **for**(i = 2) 的第二次迭代: 4 | 10 | 9 | 6 | 7 |
| 内层 **for**(j = 3) 的第二次迭代: 4 | 10 | 6 <-> 9 | 7 |
| 内层 **for**(j = 2) 的第三次迭代: 4 | 6 <-> 10 | 9 | 7 |

# C++ 简介 

因此，数组转换为：4 6 10 9 7

外层 for(i = 3) 的第三次迭代: 4
内层 for(j = 4) 的第一次迭代: 6 10 7 <-- 9
内层 for(j = 3) 的第二次迭代: 6 7 <-- 10 9

因此，数组转换为：4 6 7 10 9

外层 for(i = 4) 的第四次迭代
内层 for(j = 4) 的第一次迭代: 4 6 7 10 <-- 9

排序完成，数组转换为：4 6 7 9 10
若要降序排序数组，我们只需更改 if 语句：

```cpp
if (arr[j] > arr[j-1])
```

C.12.11 编写一个程序，读取 50 个国家的名称（每个少于 100 个字符）以及每月访问这些游客人数。程序应使用适当的数组来存储数据。然后，程序应读取一个国家名称并显示访问该国家的年度游客人数。程序在结束前显示访问最多的国家（检查是否有多个国家并列第五位）。

```cpp
#include <iostream>
#include <cstring>
using std::cout;
using std::cin;

const int CNTRS = 50;
const int MONTHS = 12;

void bubble_sort(char str[] [100], int arr[]);

int main() {
    bool flag;
    char cntr[CNTRS][100], str[100];
    int i, j, tmp, tour[CNTRS] = {0};

    for(i = 0; i < CNTRS; i++) {
        cout << "Enter name of country_ " << i + 1 << ": ";
        cin.getline(cntr[i], sizeof(cntr[i]));
        for(j = 0; j < MONTHS; j++) {
            cout << "Enter tourists of month_ " << j + 1 << ": ";
            cin >> tmp;
            tour[i] += tmp; /* 此数组存储每个国家的年度游客人数。 */
        }
        cin.get();
    }
    cout << "Enter country to search: ";
    cin.getline(str, sizeof(str));
```

```cpp
flag = 0;
for(i = 0; i < CNTRS; i++)
{
    if(strcmp(str, cntr[i]) == 0)
    {
        flag = 1;
        cout << tour[i] << " tourists visited " << str << "\n";
    }
}
if(flag == 0)
    cout << str << " not registered\n";
```

```cpp
bubble_sort(cntr, tour); /* 对游客数组进行排序并同步更新国家。 */
cout << "\n***** 降序的游客 *****\n";
for(i = 0; i < 5; i++)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
}
```

```cpp
// 检查是否有多个国家并列第五位。
while((tour[i] == tour[4]) && i < CNTRS)
{
    cout << i+1 << ' '. ' << cntr[i] << '\t' << tour[i] << '\n';
    i++;
}
return 0;
```

