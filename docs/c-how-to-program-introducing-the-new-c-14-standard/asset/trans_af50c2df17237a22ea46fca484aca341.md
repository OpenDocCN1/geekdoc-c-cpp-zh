
每次从键盘读取一个值，并将该值存储在元素 `a[0]` 中。

```cpp
// Fig. 7.6: Fig07_06.cpp
// Compute the sum of the elements of an array.
#include <iostream>
#include <array>
using namespace std;

int main() {
   const size_t arraySize{4}; // specifies size of array
   array<int, arraySize> a{10, 20, 30, 40};
   int total{0};

   // sum contents of array a
   for (size_t i{0}; i < a.size(); ++i) {
      total += a[i];
   }

   cout << "Total of array elements: " << total << endl;
}
```

```text
Total of array elements: 100
```

**图 7.6** 计算 `array` 各元素之和。

### 7.4.5 使用条形图以图形方式显示 `array` 数据

许多程序以图形方式向用户呈现数据。例如，数值通常以条形图中的条形显示，较长的条形表示按比例更大的数值。以图形方式显示数值数据的一种简单方法是使用条形图，将每个数值显示为由星号（`*`）组成的条形。

教授们常常喜欢查看考试的成绩分布。教授可能会用图表表示若干类别中每个类别的成绩数量，以可视化成绩分布。假设成绩为 87、68、94、100、83、78、85、91、76 和 87。其中有一个 100 分，两个 90–99 分的成绩，四个 80–89 分的成绩，两个 70–79 分的成绩，一个 60–69 分的成绩，没有低于 60 分的成绩。我们的下一个程序（图 7.7）将这些数据存储在一个包含 11 个元素的 `array` 中，每个元素对应一个分数段。例如，`n[0]` 表示 0–9 范围内的成绩数量，`n[7]` 表示 70–79 范围内的成绩数量，`n[10]` 表示 100 分的成绩数量。你将在图 7.13 和图 7.19 中看到的 `GradeBook` 类包含基于一组成绩计算成绩频率的代码。在此示例中，我们用频率值初始化数组 `n`。

该程序（[图 7.7](#)）从 `array` 中读取这些数字，并将信息绘制成条形图，显示每个分数段，后跟一个由星号组成的条形，表示该分数段中的成绩数量。为了给每个条形加标签，第 17–25 行根据计数器变量 `i` 的当前值输出一个分数段（例如 `"70–79: "`）。*嵌套的* `for` 语句（第 28–30 行）输出当前条形，即适当数量的星号。注意第 28 行中的循环继续条件（`stars < n[i]`）。每当程序到达*内层* `for` 时，循环从 `0` 计数到 `n[i]`，从而使用 `array n` 中的一个值来确定要显示的星号数量。在此示例中，`n[0]–n[5]` 包含零，因为没有学生得到低于 60 分的成绩。因此，程序在前六个分数段旁边不显示星号。

```cpp
// Fig. 7.7: Fig07_07.cpp
// Bar chart printing program.
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main() {
   const size_t arraySize{11};
   array<unsigned int, arraySize> n{0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1};

   cout << "Grade distribution:" << endl;

   // for each element of array n, output a bar of the chart
   for (size_t i{0}; i < n.size(); ++i) {
      // output bar labels ("0-9:", ..., "90-99:", "100:")
      if (i == 0) {
         cout << " 0-9: ";
      }
      else if (i == 10) {
         cout << " 100: ";
      }
      else {
         cout << i * 10 << "-" << (i * 10) + 9 << ": ";
      }

      // print bar of asterisks
      for (unsigned int stars{0}; stars < n[i]; ++stars) {
         cout << '*';
      }

      cout << endl; // start a new line of output
   }
}
```

```text
Grade distribution:
 0-9:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: *
70-79: **
80-89: ****
90-99: **
 100: *
```

**图 7.7** 条形图打印程序。

### 7.4.6 使用 `array` 的元素作为计数器

有时，程序使用计数器变量来汇总数据，例如调查结果。在 **图 6.7** 中，我们在掷骰子程序中使用单独的计数器来跟踪骰子每一面的出现次数，程序掷骰子 60,000,000 次。该程序的 `array` 版本如 **图 7.8** 所示。此版本还使用了 **6.9 节** 中引入的 C++11 新随机数生成功能。

**图 7.8** 使用 `array` `frequency`（第 17 行）来统计骰子值的出现次数。该程序第 21 行中的*单条语句*替代了 **图 6.7** 第 22–43 行中的整个 `switch` 语句。第 21 行使用一个随机值来确定在循环的每次迭代中递增哪个 `frequency` 元素。

```cpp
// Fig. 7.8: Fig07_08.cpp
// Die-rolling program using an array instead of switch.
#include <iostream>
#include <iomanip>
#include <array>
#include <random>
#include <ctime>
using namespace std;

int main() {
    // use the default random-number generation engine to
    // produce uniformly distributed pseudorandom int values from 1 to 6
    default_random_engine engine(static_cast<unsigned int>(time(0)));
    uniform_int_distribution<unsigned int> randomInt(1, 6);

    const size_t arraySize{7}; // ignore element zero
    array<unsigned int, arraySize> frequency{}; // initialize to 0s

    // roll die 60,000,000 times; use die value as frequency index
    for (unsigned int roll{1}; roll <= 60'000'000; ++roll) {
        ++frequency[randomInt(engine)];
    }

    cout << "Face" << setw(13) << "Frequency" << endl;

    // output each array element's value
    for (size_t face{1}; face < frequency.size(); ++face) {
        cout << setw(4) << face << setw(13) << frequency[face] << endl;
    }
}
```

```text
Face    Frequency
  1       9997901
  2       9999110
  3      10001172
  4      10003619
  5       9997606
  6      10000592
```

**图 7.8** 使用 `array` 代替 `switch` 的掷骰子程序。

第 21 行中的计算生成一个从 1 到 6 的随机下标，因此 `array frequency` 必须足够大以存储六个计数器。我们使用一个包含七个元素的 `array`，其中忽略 `frequency[0]`——让骰子面值 1 递增 `frequency[1]` 比递增 `frequency[0]` 更清晰。因此，每个面值都*直接*用作 `array frequency` 的下标。我们还通过遍历 `array frequency` 来输出结果（**图 7.8**，第 27–29 行），从而替代 **图 6.7** 的第 46–51 行。

### 7.4.7 使用 `arrays` 汇总调查结果

我们的下一个示例使用 `arrays` 汇总调查中收集的数据结果。考虑以下问题陈述：

- *二十名学生被要求按 1 到 5 的等级评价学生食堂食物的质量，其中 1 表示“糟糕”，5 表示“极好”。将这 20 个回答放入一个整型 `array` 中，并确定每个评分的频率。*

这是一种常见的 `array` 处理应用类型（[图 7.9](#)）。我们希望汇总每个评分（即 1–5）的回答数量。`array` `responses`（第 14–15 行）是一个包含 20 个元素的整型 `array`，存储学生对调查的回答。`array` `responses` 被声明为 `const`，因为它的值不会（也不应）改变。我们使用一个包含六个元素的 `array` `frequency`（第 18 行）来统计每个回答的出现次数。`array` 的每个元素用作一个调查回答的计数器，并初始化为零。如 [图 7.8](#) 中那样，我们忽略 `frequency[0]`。

```cpp
// Fig. 7.9: Fig07_09.cpp
// Poll analysis program.
#include <iostream>
#include <iomanip>
#include <array>
using namespace std;

int main() {
   // define array sizes
   const size_t responseSize{20}; // size of array responses
   const size_t frequencySize{6}; // size of array frequency

   // place survey responses in array responses
   const array<unsigned int, responseSize> responses{
      1, 2, 5, 4, 3, 5, 2, 1, 3, 1, 4, 3, 3, 3, 3, 2, 3, 2, 2, 5};

   // initialize frequency counters to 0
   array<unsigned int, frequencySize> frequency{};

   // for each answer, select responses element and use that value
   // as frequency subscript to determine element to increment
   for (size_t answer{0}; answer < responses.size(); ++answer) {
      ++frequency[responses[answer]];
   }

   cout << "Rating" << setw(12) << "Frequency" << endl;

   // output each array element's value
   for (size_t rating{1}; rating < frequency.size(); ++rating) {
      cout << setw(6) << rating << setw(12) << frequency[rating] << endl;
   }
}
```

| 评分 | 频率 |
|---:|---:|
| 1 | 3 |
| 2 | 5 |
| 3 | 7 |
| 4 | 2 |
| 5 | 3 |

**图 7.9** 调查分析程序。

第一个 `for` 语句（第 22–24 行）从 `array responses` 中逐个取出回答，并递增 `frequency` 数组中的五个计数器之一（`frequency[1]` 到 `frequency[5]`）。关键
