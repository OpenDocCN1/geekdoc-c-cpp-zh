

# 函数 341

$T(n)$ 三角形数表示组成等边三角形的对象数量，它等于从 1 到 $n$ 的所有数字之和。因此，$T(n)$ 表示为 $T(n)=1+2+3...(n-1)+n$

```
并且在递归形式下：$T(n) = \begin{cases} n, & 当 n=0 或 n=1 \\ n+T(n-1), & 当 n>1 \end{cases}$
```

编写一个程序，读取一个最多 20 的正整数（例如 n），并使用递归函数显示 $T(n)$ 三角形数。

## U.11.27 下一个程序的输出是什么？

```cpp
#include <iostream>
#include <cstring>

void test(char a, char str[], char *ptr);

int main() {
    char *tmp, txt[20] = "abcde";
    tmp = txt;
    test(*tmp+1, txt+3, &txt[1]);
    std::cout << txt << '\n';
    return 0;
}

void test(char a, char str[], char *ptr) {
    strcpy(str, "1234");
    str[0] = a;
    ptr[2] = *ptr + 5;
}
```

## U.11.28 编写一个程序，生成随机整数并存储在数组中。然后，程序应该调用递归函数来检查数组是否是对称的，即如果第一个元素的值等于最后一个元素，第二个元素的值等于倒数第二个元素，以此此类推。如果数组不是对称的，函数应该返回第一个破坏对称元素的位置。

## U.11.29 图像编辑程序使用洪填充算法用新颜色填充相同颜色的区域。假设图中的 8x8 二维数组表示图像的像素，其中 0 代表黑色；1：白色；2：红色；3：绿色；4：蓝色。只有当两个像素相邻且颜色相同时，我们才认为它们是连接的。例如，相同颜色的区域如图 B 所示。

| 0 0 0 1 1 2 2 | 0 0 0 1 1 2 2 | 3 3 3 1 1 2 2 |
| 0 4 4 4 1 1 2 | 0 4 4 4 1 1 2 | 3 4 4 4 1 1 2 |
| 4 4 4 4 2 2 2 | 4 4 4 4 2 2 2 | 4 4 4 4 2 2 2 |
| 0 0 3 3 3 3 3 | 0 3 3 3 3 3 3 | 0 3 3 3 3 3 3 |
| 0 0 0 3 3 3 3 | 0 0 0 3 3 3 3 | 0 0 0 3 3 3 3 |
| 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 |
| 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 |
| 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 | 0 0 0 0 0 0 0 |

(a)

(b)

(c)

为了实现洪填充算法，写一个递归的 `floodfill()` 函数，该函数将随机位置（例如 i, j）像素的颜色（例如 c）更改为新颜色，然后更改其颜色同样为 c 的相邻像素（即左、右、上、下像素）的颜色。注意，这个过程应该在被改变像素的邻居上递归地进行，直到没有其他像素需要检查为止。例如，如果我们选择将位置 0,0 像素的颜色从黑色（例如 0）更改为绿色（例如 3），则左上区域像素的颜色将变为绿色，如图 c 所示。

编写一个程序，为 8x8 数组的元素设置随机值 [0-4]。然后，程序应该读取一个像素的位置（例如 i, j）和一个新颜色，并使用 `floodfill()` 将其相同颜色区域的现有颜色更改为颜色。

# 搜索与排序

本章描述了某些用于在数组中搜索值以及按升序或降序对数组元素的常用算法。如需了解更多算法、性能分析和最佳实现，你应该阅读一本专注于该主题的书。本章的目的是让你了解数组，并让你对算法如何实现有一个感觉。

## 搜索数组

为了检查一个值是否存储在数组中，我们将描述线性搜索和二分搜索。

### 线性搜索算法

线性搜索算法（也称为顺序搜索）是在未排序数组中搜索某个值的最简单的算法。将要搜索的值与每个元素的值进行比较，直到找到匹配项为止。在包含 n 个元素的数组中，最大搜索次数为 n，这在搜索值是最后一个元素或不在数组中时发生。在接后的程序中，`linear_search()` 函数实现了该搜索算法。

# 练习题

**C.1.2** 编写一个函数在双精度浮数组中搜索一个数字。如果该数字被存储，函数应该返回它出现的次数和第一次出现的位置，否则返回 -1。编写一个程序读取最多 100 个双精度数并将它们存储在数组中。如果用户输入 -1，则终止插入。程序读取一个数字并使用该函数显示其出现的次数以及在数组中的第一个位置。

```cpp
#include <iostream>
#include <cout>
#include <cin>

const int SIZE = 100;

int linear_search(const double arr[], int size, double num, int *t);

int main() {
    int i, times, pos;
    double num, arr[SIZE];

    for(i = 0; i < SIZE; i++) {
        cout << "Enter number: ";
        cin >> num;
        if (num == -1)
            break;
        arr[i] = num;
    }
    cout << "Enter number to search: ";
    cin >> num;
    pos = linear_search(arr, i, num, &times); /* 变量 i 表示数组中元素的数量。 */

    if(pos == -1)
        cout << "isn't found\n";
    else
        cout << times << " times (first pos = " << pos << ")\n";
    return 0;
}
```

```cpp
int linear_search(const double arr[], int size, double num, int *t) {
    int i, pos;
    pos = -1;
    *t = 0;
    for(i = 0; i < size; i++) {
        if(arr[i] == num) {
            (*t)++;
            if(pos == -1) /* 存储出现的位置。 */
            pos = i;
        }
    }
    return pos;
}
```

**C.2** 编写一个函数，接收整数数组作为参数并返回相同元素出现的最大次数。例如，如果数组是 [1, 10, -3, 5, -3, 8]，该函数应该返回 2，因为 -3 出现的次数最多，即 2 次。编写一个程序读取十个整数，将它们存储在数组中，并使用该函数显示相同元素出现的最大次数。

```cpp
#include <iostream>
#include <cout>
#include <cin>

const int SIZE = 10;

int num_occurcs(const int arr[]);

int main() {
    int i, arr[SIZE];

    for(i = 0; i < SIZE; i++) {
        cout << "Enter number: ";
        cin >> arr[i];
    }
    cout << "\nMax occurrences is " << num_occurcs(arr) << '\n';
    return 0;
}

int num_occurcs(const int arr[]) {
    int i, j, k, max_times;

    max_times = 1;
    for(i = 0; i < SIZE; i++) {
        k = 1; // 每个数字至少出现一次。
        for(j = i+1; j < SIZE; j++) { /* 将 arr[i] 与剩余元素比较。 */
            if(arr[i] == arr[j]) {
                k++;
            }
            if(k > max_times) {
                max_times = k;
            }
        }
    }
    return max_times;
}
```

## 二分搜索算法

二分搜索算法用于在排序数组（无论是升序还是降序）中搜索值。为了理解算法如何工作，假设我们正在一个升序排序的数组中搜索一个值：

步骤 1：使用变量 start 和 end 来指示搜索该值的数组部分的起始和结束位置。变量 middle 用于存储该部分的位置：middle=(start+end)/2。例如，如果我们有一个包含 100 个整数的排序数组，start 初始化为 0，为 99，middle 变为 49。

步骤 2：我们将搜索的值与中间元素进行比较：
- 如果它们相等，则找到了搜索值，算法终止。
- 如果搜索值较大，则在从中间位置到结束的范围内继续搜索。start 的值变为 start=middle+1，算法返回步骤 1。
- 如果搜索值较小，则在从起始位置到中间的范围内继续搜索。end 的值变为 end=middle-1，算法返回步骤 1。

