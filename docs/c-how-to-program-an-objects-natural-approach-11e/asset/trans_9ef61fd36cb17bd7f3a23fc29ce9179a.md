
```cpp
54        middle = (low + high + 1) / 2; // recalculate the middle
55    } while ((low <= high) && (location == -1));
56
57    return location; // return location of key
58
59 }
60
61 int main() {
62    // use the default random-number generation engine to produce
63    // uniformly distributed pseudorandom int values from 10 to 99
64    std::random_device rd; // used to seed the default_random_engine
65    std::default_random_engine engine{rd()}; // rd() produces a seed
66    std::uniform_int_distribution<int> randomInt{10, 99};
67
68    std::array<int, 15> arrayToSearch; // create 15-element array
69
70    // fill arrayToSearch with random values
71    for (int& item : arrayToSearch) {
72        item = randomInt(engine);
73    }
74
75    std::sort(arrayToSearch.begin(), arrayToSearch.end());
76
77    // display arrayToSearch's values
78    displayElements(arrayToSearch, 0, arrayToSearch.size() - 1);
79
80    // get input from user
81    std::cout << "\nPlease enter an integer value (-1 to quit): ";
82    int searchKey; // value to locate
83    std::cin >> searchKey; // read an int from user
84    std::cout << "\n";
85
86    // repeatedly input an integer; -1 terminates the program
87    while (searchKey != -1) {
88        // use binary search to try to find integer
89        int position{binarySearch(arrayToSearch, searchKey)};
90
91        // return value of -1 indicates integer was not found
92        if (position == -1) {
93            std::cout << std::format("{} was not found.\n", searchKey);
94        }
95        else {
96            std::cout << std::format("{} was found in position {}.\n",
97                searchKey, position);
98        }
99
100        // get input from user
101        std::cout << "\n\nPlease enter an integer value (-1 to quit): ";
102        std::cin >> searchKey; // read an int from user
103        std::cout << "\n";
104    }
105 }
```

**图 21.2** | 数组的二分查找。（第 2 部分，共 3 部分。）

```text
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97

Please enter an integer value (-1 to quit): 48
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
48 was found in position 3.

Please enter an integer value (-1 to quit): 92

10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
                         62 63 68 72 75 92 97
                                             *
                                             75 92 97
                                                *
92 was found in position 13.

Please enter an integer value (-1 to quit): 22
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
10 23 27
   *
10
*
22 was not found.

Please enter an integer value (-1 to quit): -1
```

**图 21.2** | 数组的二分查找。（第 3 部分，共 3 部分。）

## 函数模板 binarySearch

第 26–59 行定义了 `binarySearch` 函数模板。其函数参数为：

- 对要搜索数组的引用，以及
- 对搜索键的引用

第 28–30 行计算算法当前搜索的数组部分的低端索引、高端索引和中间索引。首次调用 binarySearch 时，low 为 0，high 为数组大小减 1，middle 为这两个值的平均值。第 31 行将 location 初始化为 −1——这是 binarySearch 在未找到搜索键时返回的值。第 33–56 行循环直到

- low 大于 high，表示未找到该元素，或
- location 不等于 -1，表示已找到搜索键。

第 45 行测试中间元素的值是否等于 key。若是，第 46 行将中间索引赋给 location，循环终止，函数将 location 返回给调用者。每个未找到搜索键的循环迭代都会测试单个值（第 48 行），并排除数组中剩余值的一半（第 49 行或第 51 行）。

## 函数 main

第 64–66 行设置一个用于生成 10–99 的 int 值的随机数生成器。第 68–73 行创建一个数组并用随机 int 填充。回想二分查找算法要求数组有序，因此第 75 行使用 `std::sort` 将 arrayToSearch 的元素按升序排序。然后，第 78 行显示 arrayToSearch 排序后的内容。

第 87–104 行循环直到用户输入值 −1。对于用户输入的每个搜索键，程序对 arrayToSearch 执行二分查找，以确定它是否包含该搜索键。首先，我们按升序显示 arrayToSearch 的内容。当用户指示程序查找 48 时，binarySearch 测试中间元素——60，如 * 所示。搜索键小于 60，因此程序排除数组的后半部分，并测试数组前半部分的中间元素。搜索键等于 48，因此程序仅进行两次比较后就返回索引 3。输出还显示了查找值 92 和 22 的结果。

## 21.4.2 二分查找的效率

在最坏情况下，使用二分查找搜索一个包含 1,023 个元素（2¹⁰ − 1）的有序数组只需 **10 次比较**。该算法将搜索键与有序数组的中间元素进行比较。如果匹配，搜索结束。否则，如果搜索键大于中间元素，我们可以排除数组的前半部分，不再进一步考虑；如果小于，则可以排除数组的后半部分。这产生了折半效应——后续搜索只需搜索 511、255、127、63、31、15、7、3 和 1 个元素。数字 1,023（2¹⁰ − 1）只需折半 10 次，就能找到该键或确定它不在数组中。

将除以 2 等同于二分查找算法中的一次比较。因此，一个包含 1,048,575（2²⁰ − 1）个元素的数组最多需要 **20 次比较** 就能找到该键，而一个约十亿个元素的数组最多需要 **30 次比较** 就能找到该键——与线性查找相比，性能提升巨大。对于十亿个元素的数组，这就是线性查找平均 5 亿次比较与二分查找最多仅 30 次比较之间的差异！

对于任何有序数组的二分查找，所需的最大比较次数是大于数组元素个数的 2 的第一个幂的指数，表示为 log₂ n。所有对数都以“大致相同的速率”增长，因此为了大 O 表示，可以省略底数。这导致二分查找的大 O 为 O(log n)，称为对数运行时间，读作“log n 阶”。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1265_0.png)

## 检查点

1. *（填空）* 线性查找和二分查找是截然不同的搜索算法。然而，对于两者，最坏情况运行时间都发生在 ________ 时。
   **答案：** 未找到搜索键。

2. *（讨论）* 为了能用二分查找算法高效搜索而对数组进行排序，代价很高。请指出两种值得这样做的情况。
   **答案：** 1. 当数组将被搜索很多次时。2. 当应用有严格的性能要求时。

3. *（讨论）* 比较在未排序的万亿个元素数组上进行线性查找的最坏情况性能，与在已排序的万亿个元素数组上进行二分查找的最坏情况性能。
   **答案：** 线性查找将需要进行约一万亿次比较，才能确定搜索键与未排序数组中的任何一项都不匹配，或与接近数组末尾的元素匹配。二分查找将需要进行约 40 次比较，才能确定搜索键与已排序数组中的任何一项都不匹配，或在最后几次比较中与某一项匹配。

## 21.5 插入排序

接下来，让我们实现一种排序算法。插入排序算法的第一次迭代取数组的第二个元素，如果它小于第一个元素，就将其与第一个元素交换——也就是说，算法将第二个元素插入到第一个元素前面。第二次迭代查看第三个元素，并将其插入到相对于前两个元素的正确位置，使所有三个元素都有序。

### 第一次迭代

图 21.3 的第 27 行声明并初始化名为 `data` 的数组，其值如下：

```text
34   56   4   10   77   51   93   30   5   52
```

第 36 行将该数组传递给 `insertionSort` 函数，该函数在参数 `items` 中接收该数组。该函数首先查看 items[0] 和 items[1]，它们的值分别为 34 和 56。这两个元素已经有序，因此算法继续。如果它们无序，算法会交换它们。

### 第二次迭代

在第二次迭代中，算法查看 items[2] 的值（即 4）。该值小于 56，因此算法将 4 存储在临时变量中，并将 56 向右移动一个元素。然后算法确定 4 小于 34，因此将 34 向右移动一个元素。此时，算法已到达数组开头，因此将 4 放入 items[0]。数组现在为：

```text
4   34   56   10   77   51   93   30   5   52
```

### 第三次及后续迭代

在第三次迭代中，算法将 items[3] 的值（即 10）放到相对于前四个数组元素的正确位置。算法将 10 与 56 比较，因为 56 大于 10，所以将 56 向右移动一个元素。接下来，算法将 10 与 34 比较，将 34 向右移动一个元素。当算法将 10 与 4 比较时，它观察到 10 大于 4，并将 10 放入 items[1]。数组现在为：

```text
4   10   34   56   77   51   93   30   5   52
```

使用该算法，经过第 *i* 次迭代后，数组的前 *i* + 1 个元素已排序。然而，它们可能不在最终位置，因为算法之后可能会在数组后面遇到更小的值。
