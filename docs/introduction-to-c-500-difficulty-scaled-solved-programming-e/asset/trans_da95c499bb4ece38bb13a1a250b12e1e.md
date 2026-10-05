

# 346 C++ 简介

简而言之，二分查找算法将数组分为两个部分。然后，将待查找的值与中间元素进行比较，并在适当的部分继续搜索。如果找到了待查找的值，或者起始位置大于结束位置，则算法终止。在具有包含 $n$ 个元素的排序数组中，使用二分查找算法的最大查找次数为 $\log_n$。在下面的程序中，`binary_search()` 函数实现了二分查找算法。

# # 练习

C.12.3 编写一个函数在整数数组中搜索一个数字。如果找到了该数字，函数应返回其位置，否则返回 -1。编写一个程序，初始化一个升序排列的整数数组。该程序应读取一个整数并使用该函数显示它在数组中的位置。

```cpp
#include <iostream>
```

```cpp
int binary_search(const int arr[], int size, int num);

int main()
{
    int num, pos, arr[] = {10, 20, 30, 40, 50, 60, 70};
    std::cout << "Enter number to search: ";
    std::cin >> num;

    pos = binary_search(arr, sizeof(arr)/sizeof(int), num); /* 第二个参数以通用方式计算元素的个数。 */
    if(pos == -1)
        std::cout << num << " isn't found\n";
    else
        std::cout << num << " is found in position " << pos << '\n';
    return 0;
}

int binary_search(const int arr[], int size, int num)
{
    int start, end, middle;

    start = 0;
    end = size-1;
    while(start <= end)
    {
        middle = (start+end)/2;
        if(num < arr[middle])
            end = middle-1;
        else if(num > arr[middle])
            start = middle+1;
        else
            return middle;
    }
    return -1; /* 如果执行到此点，说明没有找到该数字，函数返回 -1。 */
}
```

# 12 • 数组的搜索与排序 347

注释：为了查看算法如何工作，假设用户输入了数字 45。

第一次迭代。`start` 的初始值为 0，`end` 为 6，`middle` 变为 (start+end)/2 = 6/2 = 3。由于 `arr[middle]` 是 40，小于 45，下一个执行的语句是 `start = 3+1 = 4`。

第二次迭代。`middle` 变为 (start+end)/2 = (4+6)/2 = 5。由于 `arr[middle]` 是 60，大于 45，下一语句是 `end = middle-1 = 4`。

第三次迭代。`middle` 变为 (start+end)/2 = (4+4)/2 = 4。由于 `arr[middle]` 是 50，大于 45，下一语句是 `end = middle-1 = 3`。

由于 `start` 大于 `end`，循环终止，函数返回 -1。

# C.12.4 编写一个程序读取一个 [0, 1000] 之间的整数，并使用二分查找算法“猜”那个数字。程序应该通过提问来确定我们搜索的是否小于还是大于已检查区间的最大值。答案必须以 0（否）或 1（是）的形式给出。程序应显示找到该数字时用了多少尝试。

```cpp
#include <iostream>
using std::cout;
using std::cin;
int main() {
    int x, ans, low, high, middle, times;

    do
    {
        cout << "Enter number in [0, 1000]: ";
        cin >> x;
    } while (x < 0 || x > 1000);

    times = 1;
    low = 0;
    high = 1000;
    middle = (high+low)/2;
    while (high >= low)
    {
        cout << "Is " << middle << " the hidden number (0 = No, 1 = Yes)?" ";
        cin >> ans;
        if(ans == 1) {
            cout << "Num " << ans << " is found in " << times << " tries\n";
            return 0;
        }
        times++;
        cout << "Is the hidden number < " << middle << " (0 = No, 1 = Yes)?" ";
        cin >> ans;
        if(ans == 1) {
            high = middle-1;
            middle = (high+low)/2;
        }
        else
        {
            low = middle+1;
            middle = (high+low)/2;
        }
    }
    cout << "Num = " << x << " isn't found. You probably gave a wrong answer\n";
    return 0;
}
```

# 348 C++ 简介

# 数组排序

有几种算法可以对数组进行排序。我们将描述一些最流行的：选择排序、插入排序、冒泡排序和快速排序算法。

# 选择排序算法

为了描述该算法，我们将按升序对数组进行排序。首先，我们找到值最小的元素并与数组的第一个元素交换。因此，最小值被存储在第一个位置。

然后，我们在剩余的元素（除去第一个）中找到最小值。与之前一样，我们将该元素与数组的第二个元素交换。因此，最小值被存储在第二个位置。此过程对剩余元素重复进行，算法在比较最后两个元素后终止。

要按降序对数组进行排序，唯一的区别是我们要找到最大值而不是最小值。在下面的程序中，`sel_sort()` 函数实现了选择排序算法，按升序对数组排序。

# # 练习

C.12.5 编写一个函数，接受一个双精度浮数组作为参数，并使用选择排序将其按升序排序。编写一个程序读取十学生的成绩，将其存储在数组中，并使用该函数进行排序。

```cpp
#include <iostream>

void sel_sort(double arr[]);

const int SIZE = 10;

int main()
{
    int i;
    double grd[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        std::cout << "Enter grade of stud " << i+1 << " ";
        std::cin >> grd[i];
    }
}
```

```cpp
void sel_sort(double arr[])
{
    int i, j;
    double tmp;

    for(i = 0; i < SIZE-1; i++)
    {
        for(j = i+1; j < SIZE; j++)
        {
            if(arr[i] > arr[j])
            {
                // 交换值。
                tmp = arr[i];
                arr[i] = arr[j];
            }
        }
        }
    

}
```

**注释：** 在内层循环的迭代中，`arr[i]` 与 `i+1` 到 `SIZE-1` 的元素进行比较。如果 `arr[i]` 小于 `arr[j]`，则交换这两个值。因此，在外层循环的迭代中，剩余元素中的最小值被存储在 `arr[i]`。要按降序对数组排序，我们只需将 `if` 语句改为：`if(arr[i] < arr[j])`。

C.12.6 为了继续练习，程序还应该读取十个学生的姓名（每个少于 100 个字符），并按升序显示最终排名。姓名应该存储在 `vector` 中，并作为额外的参数传递给 `sel_sort()`。

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

void sel_sort(vector<string>& str, double arr[])

const int SIZE = 10;

int main()
{
    int i;
    double grd[SIZE];
    vector<string> name(SIZE);

    for(i = 0; i < SIZE; i++)
    {
        cout << "Enter name: ";
        getline(cin, name[i]);

        cout << "Enter grade: ";
        cin >> grd[i];
        cin.get();
    }
    sel_sort(name, grd);

    cout << "\n***** Final Rating *****\n";
    for(i = 0; i < SIZE; i++)
        cout << name[i] << "\t <<" << grd[i] << "\n";
    return 0;
}
```

```cpp
void sel_sort(vector<string>& str, double arr[])
{
    int i, j;
    double k;
    string tmp;

    for(i = 0; i < SIZE-1; i++)
    {
        for(j = i+1; j < SIZE; j++)
        {
            if(arr[i] > arr[j])
            {
                // 平行交换成绩和姓名。
                k = arr[i];
                arr[i] = arr[j];
                arr[j] = k;

                tmp = str[j];
                str[j] = str[i];
                str[i] = tmp;
            }
        }
    }
}
```

C.12.7 编写 `add_sort()` 函数，将一个数字插入排序数组，使数组保持排序。编写一个程序读取九整数，将其存储在一个包含十个整数的数组中，并对这些元素进行升序排序。然后，程序读取最后一个整数，使用 `add_sort()` 将其插入数组并显示排序后的数组。

```cpp
#include <iostream>
using std::cout;
using std::cin;
```

```cpp
void sel_sort(int arr[], int size);
void add_sort(int arr[], int size, int num);
```

