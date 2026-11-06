

## *二分查找示例*

**图 20.3** 实现并演示了二分查找算法。在程序执行过程中，我们使用函数模板 `displayElements`（第 11–23 行）来显示当前正在搜索的 `array` 部分。

```cpp
// Fig 20.3: BinarySearch.cpp
// Binary search of an array.
#include <algorithm>
#include <array>
#include <ctime>
#include <iostream>
#include <random>
using namespace std;

// display array elements from index low through index high
template <typename T, size_t size>
void displayElements(const array<T, size>& items,
    size_t low, size_t high) {
    for (size_t i{0}; i < items.size() && i < low; ++i) {
        cout << "  "; // display spaces for alignment
    }

    for (size_t i{low}; i < items.size() && i <= high; ++i) {
        cout << items[i] << " "; // display an element
    }

    cout << endl;
}

// perform a binary search on the data
template <typename T, size_t size>
int binarySearch(const array<T, size>& items, const T& key) {
    int low{0}; // low index of elements to search
    int high{static_cast<int>(items.size()) - 1}; // high index
    int middle{(low + high + 1) / 2}; // middle element
    int location{-1}; // key's index; -1 if not found

    do { // loop to search for element
        // display remaining elements of array to be searched
        displayElements(items, low, high);

        // output spaces for alignment
        for (int i{0}; i < middle; ++i) {
            cout << "    ";
        }

        cout << " ^ " << endl; // indicate current middle

        // if the element is found at the middle
        if (key == items[middle]) {
            location = middle; // location is the current middle
        }
        else if (key < items[middle]) { // middle is too high
            high = middle - 1; // eliminate the higher half
        }
        else { // middle element is too low
            low = middle + 1; // eliminate the lower half
        }

        middle = (low + high + 1) / 2; // recalculate the middle
    } while ((low <= high) && (location == -1));

    return location; // return location of key
}

int main() {
    // use the default random-number generation engine to produce
    // uniformly distributed pseudorandom int values from 10 to 99
    default_random_engine engine{
        static_cast<unsigned>(time(nullptr))};
    uniform_int_distribution<unsigned int> randomInt{10, 99};

    const size_t arraySize{15}; // size of array
    array<int, arraySize> arrayToSearch; // create an array

    // fill arrayToSearch with random values
    for (int &item : arrayToSearch) {
        item = randomInt(engine);
    }

    sort(arrayToSearch.begin(), arrayToSearch.end()); // sort the array

    // display arrayToSearch's values
    displayElements(arrayToSearch, 0, arrayToSearch.size() - 1);

    // get input from user
    cout << "\nPlease enter an integer value (-1 to quit): ";
    int searchKey; // value to locate
    cin >> searchKey; // read an int from user
    cout << endl;

    // repeatedly input an integer; -1 terminates the program
    while (searchKey != -1) {
        // use binary search to try to find integer
        int position(binarySearch(arrayToSearch, searchKey));

        // return value of -1 indicates integer was not found
        if (position == -1) {
            cout << "The integer " << searchKey << " was not found.\n";
        }
        else {
            cout << "The integer " << searchKey
                 << " was found in position " << position << ".\n";
        }

        // get input from user
        cout << "\n\nPlease enter an integer value (-1 to quit): ";
        cin >> searchKey; // read an int from user
        cout << endl;
    }
}
```

```text
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97

Please enter an integer value (-1 to quit): 48
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
The integer 48 was found in position 3.

Please enter an integer value (-1 to quit): 92
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
                              62 63 68 72 75 92 97
                                             *
                                                 75 92 97
                                                     *
The integer 92 was found in position 13.

Please enter an integer value (-1 to quit): 22
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                         *
10 23 27 48 52 55 58
             *
10 23 27
       *
10
  *
The integer 22 was not found.

Please enter an integer value (-1 to quit): -1
```

图 20.3 对数组进行二分查找。

## *函数模板* `binarySearch`

第 26–59 行定义了函数模板 `binarySearch`，它有两个参数——待搜索 `array` 的引用和搜索键的引用。第 28–30 行计算算法当前正在搜索的 `array` 部分的 `low` 端索引、`high` 端索引和 `middle` 索引。当首次调用 `binarySearch` 时，`low` 为 `0`，`high` 为 `array` 的大小减 `1`，`middle` 为这两个值的平均值。第 31 行将 `location` 初始化为 `−1`——如果未找到搜索键，`binarySearch` 将返回该值。第 33–56 行循环，直到 `low` 大于 `high`（表示未找到该元素）或 `location` 不等于 `−1`（表示已找到搜索键）。第 45 行测试 `middle` 元素中的值是否等于 `key`。如果是，第 46 行将 `middle` 索引赋给 `location`。然后循环终止，`location` 返回给调用者。循环中未找到搜索键的每次迭代都会测试一个值（第 48 行），并消除 `array` 中剩余值的一半（第 49 行或第 51 行）。

## 函数 `main`

第 64–66 行为 `10`–`99` 之间的 `int` 值设置了一个随机数生成器。第 68–74 行创建一个 `array` 并用随机 `int` 填充它。回想一下，二分查找算法要求 *有序* 的 `array`，因此第 76 行调用标准库函数 `sort` 将 `arrayToSearch` 的元素按升序排序。第 78 行显示 `arrayToSearch` 排序后的内容。

第 88–105 行循环，直到用户输入值 `-1`。对于用户输入的每个搜索键，程序对 `arrayToSearch` 执行二分查找，以确定它是否包含该搜索键。该程序输出的第一行按升序显示 `arrayToSearch` 的内容。当用户指示程序搜索 `48` 时，程序首先测试中间元素，即 `60`（如 `*` 所示）。搜索键小于 `60`，因此程序消除 `array` 的后半部分，并测试 `array` 前半部分的中间元素。搜索键等于 `48`，因此程序仅执行 *两次* 比较后便返回索引 `3`。输出还显示了搜索值 `92` 和 `22` 的结果。

## *二分查找的效率*

在最坏情况下，使用二分查找搜索包含 1023 个元素的有序 `array` 只需 10 次比较。反复将 1023 除以 2（因为每次比较后，我们可以从考虑范围中消除 *一半* 的剩余元素）并向下取整（因为我们也移除了中间元素）得到值 511、255、127、63、31、15、7、3、1 和 0。数字 1023 仅被 2 除 10 次就得到值 0，这表示没有更多元素需要测试了。除以 2 相当于二分查找算法中的一次比较。因此，包含 1,048,575（2<sup>20</sup> − 1）个元素的 `array` 最多需要 20 次比较即可找到键，而包含约十亿个元素的 `array` 最多需要 30 次比较即可找到键。这是相对于线性查找的 *巨大* 性能提升。对于一个包含十亿个元素的 `array`，这意味着线性查找平均需要 5 亿次比较，而二分查找最多只需 30 次比较！对任何有序 `array` 进行二分查找所需的最大比较次数是大于该 `array` 中元素数量的第一个 2 的幂的指数，用 log<sub>2</sub> *n* 表示。*所有对数大致以相同的速率增长*，因此在 Big O 表示法中，基数可以省略。这导致二分查找的 Big O 为 **O(log n)**，这也被称为 **对数级运行时间**，读作“log *n* 的量级”，或更简单地说“**阶 log n**”。

