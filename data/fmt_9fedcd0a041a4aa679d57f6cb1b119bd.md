
```cpp
// 此代码有差一错误
const int SIZE = 100;
int numbers[SIZE];
for (int count = 1; count <= SIZE; count++)
    numbers[count] = 0;
```

此代码的意图创建一个包含 100 个元素的整数数组并在每个元素中存储 0。然而，此代码存在差一错误。循环执行期间，`count` 变量的值为 1 到 100，而它应该是 0 到 99。结果是下标为 0 的第一个元素被跳过了。循环在最后迭代中尝试使用 100 作为下标。因为 100 是无效下标，程序将在数组边界之外写入数据。

## 检查点

定义数组：

- A) `empNum`，一个 100 元素的 `int`数组
- B) `payRate`，一个 25 元素的 `double` 数组
- C) `miles`，一个 14 元素的 `long` 数组
- D) `stateCapital`，一个 50 元素的 `string` 对象数组
- E) `lightYears`，一个 1000 元素的 `double` 数组

8.2 以下数组定义有什么问题？

```cpp
int readings[-1];
double measurements[4.5];
int size;
string name[size];
```

8.3 在一个包含四个元素的 `double` 数组中，有效的下标值是什么？

8.4 假设程序包含以下两个语句。它们都使用方括号，但含义不同。

```cpp
int score[15];
score[6] = 45;
```

- A) 哪个数字是尺寸声明符？
- B) 哪个数字是下标？

8.5 什么是“边界检查”？`C++` 执行它吗？

8.6 以下代码的输出是什么？

```cpp
int values[5], count;
for (count = 0; count < 5; count++)
    values[count] = count + 1;
for (count = 0; count < 5; count++)
    cout << values[count] << endl;
```

8.7 完成以下程序框架，使其有一个名为 `fish` 的 10 元素 `int` 数组。完成后，程序应该询问渔民1到10钓了多少鱼，并将这些信息存储在数组中。然后它应该显示数据。

```cpp
#include <iostream>
using namespace std;
int main () {
    const int NUM_MEM = 10;
    // 定义一个名为 fish 的可以包含10个int值的数组。
    // 你必须完成这个程序使其按照上述
    // 描述工作。
    return 0;
}
```

# 8.4 数组初始化

> 概念：数组可以在定义时进行初始化。

有时，在程序内部设置变量值比输入它们更合适。然而，对于大型数组，为数组的每个元素编写单独的赋值语句意味着大量的输入。例如，考虑程序 8-5。

## 程序 8-5

1 // 此程序显示每个月的天数。
2 `#include <iostream>`
3 `#include <iomanip>`
4 `using namespace std;`
5
6 `int main()`
7 `{`
8     `const int NUM_MONTHS = 12;`
9     `int days[NUM_MONTHS];`
10
11    `days[0] = 31; // 一月`
12    `days[1] = 28; // 二月`
13    `days[2] = 31; // 三月`
14    `days[3] = 30; // 四月`
15    `days[4] = 31; // 五月`
16    `days[5] = 30; // 六月`

### 程序 8-5 (继续)

```cpp
days[6] = 31; // July
days[7] = 31; // August
days[8] = 30; // September
days[9] = 31; // October
days[10] = 30; // November
days[11] = 31; // December

for (int month = 0; month < NUM_MONTHS; month++) {
    cout << "Month " << setw(2) << " " << (month+1) << " has ";
    cout << days[month] << " days.\n";
}
    return 0;
}
```

### 程序输出

```
Month 1 has 31 days.
Month 2 has 28 days.
Month 3 has 31 days.
Month 4 has 30 days.
Month 5 has 31 days.
Month 6 has 30 days.
Month 7 has 31 days.
Month 8 has 31 days.
Month 9 has 30 days.
Month 10 has 31 days.
Month 11 has 31 days.
Month 12 has 31 days.
```

通常，还有另一种替代方案。正如你在程序 8-4 中简要看到的那样，`C++` 允许在定义数组时对其进行初始化。使用初始化列表，可以在创建数组时轻松地初始化数组的所有元素。以下语句定义了该数组，并用与程序 8-5 中赋值语句相同的值对其初始化。

```cpp
int days[NUM_MONTHS] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31};
```

这些值按照它们在列表中出现的顺序存储在数组中。（第一个值 31 存储在 `days[0]` 中，第二个值 28 存储在 `days[1]` 中，以此此类推）。程序 8-9 显示了初始化后的数组内容。

### 图 8-9

| 下标 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 31 | 28 | 31 | 30 | 31 | 30 | 31 | 31 | 30 | 31 | 30 | 31 |

程序 8-6 是程序 8-5 的修改版本。它在创建时初始化了 `days` 数组，而不是使用单独的赋值语句。注意初始化列表跨越了多行。程序还添加了一个字符串对象数组来存储月份名称。

### 程序 8-6

```cpp
// 此程序显示每个月份的天数。它使用一个
// 字符串对象数组来存储月份名称，使用一个 int 数组
// 来存储每个月份的天数。两者在创建时都通过
// 初始化列表执行了初始化。
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

int main() {
    const int NUM_MONTHS = 12;
    string name[NUM_MONTHS] = {
        "February", "March", "April",
        "May", "June", "July", "August",
        "September", "October", "November", "December"
    };

    int days[NUM_MONTHS] = {31, 28, 30, 31, 30, 31, 31, 31, 30, 31, 30, 31};

    for (int month = 0; month < NUM_MONTHS; month++) {
        cout << setw(9) << left << name[month] << " has ";
        cout << days[month] << " days.\n";
    }
    return 0;
}
```

### 程序输出

- January 有 31 天。
- February 有 28 天。
- March 有 31 天。
- April 有 30 天。
- May 有 31 天。
- June 有 30 天。
- July 有 31 天。
- August 有 31 天。
- September 有 30 天。
- October 有 31 天。
- November 有 30 天。
- December 有 31 天。

到目前为止，我们演示了如何用值填充数组然后显示所有值。有时，我们想从数组中检索一个特定的值。程序 8-7 是程序 8-6 的变体，它显示用户选择的月份有多少天数。

### 程序 8-7

```cpp
// 此程序允许用户选择一个月份，然后
// 显示该月份有多少天数。它是通过
// “查找”它存储在数组中的信息来实现的。
#include <iostream>
```

### 程序 8-7 (继续)

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    const int NUM_MONTHS = 12;
    int choice;
    string name[NUM_MONTHS] = {
        "February", "March", "April",
        "May", "July", "August",
        "September", "October", "November",
        "December"
    };

    int days[NUM_MONTHS] = {31, 28, 31, 30, 31, 31, 31, 30, 31, 30, 31};

    cout << "此程序将告诉你每个月份有多少天。\n";

    // 显示月份
    for (int month = 1; month <= NUM_MONTHS; month++)
        cout << setw(2) << month << " " << name[month-1] << endl;

    cout << "输入月份数字: ";
    cin >> choice;

    // 使用输入的数字从数组中获取名称
    // 和天数
    cout << "The month of " << name[choice-1] << " has " << days[choice-1] << " days.\n";
    return 0;
}
```

带有示例输入的程序输出：

此程序将告诉你每个月份有多少天。

1 January
2 February
3 March
4 April
5 May
6 June
7 August
8 September
9 October
10 November
11 December

输入月份数字: 4

The month of April has 30 days.

### 从元素 1 开始

有些老师倾向于让你不要使用元素 0，而是当你在建模从 1 开始的真实世界事物时从元素 1 开始。月份就是一个很好的例子。在这种情况下，你会声明 `name` 和 `days` 拥有 13 个元素，并像这样初始化：

```cpp
string name[NUM_MONTHS+1] = {"", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"};
int days[NUM_MONTHS+1] = {0, 31, 28, 31, 30, 31, 31, 30, 30, 31};
```

注意数组元素 0 没有被使用。它只包含一个占位值。这允许第一个月份 January 存储在 `name[1]` 中，第二个月份 February 存储在 `name[2]` 中，以此此类推。同样，January 的天数在 `days[1]` 中，February 的天数在 `days[2]` 中，以此此类推。

如果按照我们这样做定义和初始化数组，程序 8-6 中第 22 到 26 行的循环将所示。它显示的是数组 1 到 12 的内容。

```cpp
for (int month = 1; month <= NUM_MONTHS; month++) {
    cout << setw(9) << left << name[month] << " has ";
    cout << days[month] << " days.\n";
}
```

如果实际数据存储在元素 1，则没有必要通过偏移下标 1 来定位特定数据。程序 8-7 中第 26 和 27 行列出每个月份及其名称的循环如下：

```cpp
for (int month = 1; month <= NUM_MONTHS; month++)
    cout << setw(2) << month << " " << name[month] << endl;
```

程序 8-7 中第 34 和 35 行显示用户选择月份天数的代码将如下：

```cpp
cout << "The month of " << name[choice] << " has " << days[choice] << " days.\n";
```

从元素 1 开始存储数据的程序 8-5、8-6 和 8-7 版本可以在书籍辅助网站的第 8 文件夹中找到，分别对应 `pr8-05B.cpp`、`pr8-06B.cpp` 和 `pr8-07B.cpp` 文件：

### 部分数组初始化

在初始化数组时，`C++` 并不要求每个元素都有值。可以只初始化数组的一部分，如下：

```cpp
int numbers[7] = {1, 2, 4, 8};
```

此定义只初始化了七元素数组中的前四个元素，如图 8-10 所示。

### 图 8-10

```cpp
int numbers[7] = {1, 2, 4, 8};
```

| 1 | 2 | 4 | 8 | 0 | 0 | 0 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| numbers[0] | numbers[1] | numbers[2] | numbers[3] | numbers[4] | numbers[5] | numbers[6] |

未初始化的元素都已设置为零。这就是当数值数组被部分初始化时发生的情况。当字符串对象数组被部分初始化时，未初始化的元素将都包含空字符串，即长度为 0 的字符串。这仅在部分初始化数组定义为局部时成立。然而，如果局部数组完全没有初始化，它的元素将像其他局部变量一样包含“垃圾值”。程序 8-8 显示了部分初始化后的数组内容。

### 程序 8-8

```cpp
// 此程序有一个部分初始化的数组。
#include <iostream>
using namespace std;

int main () {
    const int SIZE = 7;
    int numbers[SIZE] = {1, 2, 4, 8}; // 初始化前四个元素

    cout << "这里是数组的内容:\n";
    for (int index = 0; index < SIZE; index++)
        cout << numbers[index] << " ";
    cout << endl;
    return 0;
}
```

### 程序输出

这里是数组的内容:

1 2 4 8 0 0 0

# 隐式数组大小

你可以通过提供一个包含每个元素值的初始化列表，在不指定大小的情况下定义数组。`C++` 会计算初始化列表中的项目数量，并为该数组分配相应数量的元素。例如，接的定义创建了一个包含五个元素的数组：

```cpp
double ratings[] = {1.0, 1.5, 2.0, 2.5, 3.0};
```

> 注意：如果你省略了大小声明符，则必须指定一个初始化列表。否则，`C++` 不知道该如何将数组设为多大。

# 初始化变量的新方法

到目前为止，你已经学会了使用赋值运算符来定义和初始化普通变量，如下所示：

```cpp
int value = 5;
```

然而，既然你已经学习了函数（第 6 章）、数组（第 8 章），并可能还有类（第 7 章），现在是时候在定义变量时引入两种额外的初始化方法了。

初始化变量的第一种新方法使用函数表示法。它看起来类似于向函数传递参数的方式。如果你已经学习了第 7 章，你会发现它也镜像了在创建对象时向构造函数传递值的方式。以下是使用函数(5)定义并初始化 `value` 变量的方法：

```cpp
int value(5);
```

初始化变量的第二种新方法由 `C++11` 引入，使用大括号表示法。它看起来类似于你刚刚看到的初始化数组的方式。然而，它有两点不同。由于普通变量一次只能存储一个值，因此大括号内只有一个值。而且，与数组初始化列表不同，大括号之前没有运算符。以下是使用大括号表示法定义 `value` 变量并将其初始化为 5 的方法：

```cpp
int value{5}; // 这在 C++ 11 或更高版本中有效。
```

大多数程序员继续使用赋值运算符来初始化普通变量，正如我们在本书中所做的那样。大括号表示法提供了一个优势：它会检查你初始化的变量是否与变量的数据类型。例如，`doubleVal` 是一个存储了 6.2 的 `double` 类型。使用赋值，我们可以编写以下内容之一：

```cpp
int value1 = 4.9; // 这将在 value1 中存储 4
int value2 = doubleVal; // 这将在 value2 中存储 6
```
