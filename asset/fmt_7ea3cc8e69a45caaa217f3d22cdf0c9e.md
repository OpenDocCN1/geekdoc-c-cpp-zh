
## 12.1.2 以对象为中心的設計

### 12.1.2.1 行为

程序应在屏幕上显示输入文件名的提示，从键盘读取此名称，然后打开一个 `ifstream` 到该文件。它应然后通过 `ifstream` 读取每个测试电路板的组件故障数，统计 0、1、2、3、4 和 5 的出现次数，然后显示每次出现的数量和百分比。

### 12.1.2.2 对象

此问题中的对象如下：

| 问题对象 | 类型 | 種類 | 名称 |

|---|---|---|---|

| 输入文件名 | `string` | 变量 | `inputFileName` |

| 输入文件流 | `ifstream` | 变量 | `inStream` |

| 电路板数量 | `int` | 变量 | `numCircuitBoards` |

| 一个数据值 | `int` | 变量 | `numFailures` |

| 0 的数量 | `int` | 变量 | `count[0]` |

| 1 的数量 | `int` | 变量 | `count[1]` |

| 2 的数量 | `int` | 变量 | `count[2]` |

| 3 的数量 | `int` | 变量 | `count[3]` |

| 4 的数量 | `int` | 变量 | `count[4]` |

| 5 的数量 | `int` | 变量 | `count[5]` |

### 12.1.2.3 操作

解决此问题所需的操作是：

- i. 从键盘读取输入文件名并打开流到它。

- ii. 从流中读取故障计数，统计 0、1、2、3、4 和 5 的出现次数。

- iii. 显示 0、1、2、3、4 和 5 的出现次数和百分比。

这些操作要么在 C++ 中提供，要么只需几条语句即可轻松实现。

### 12.1.2.4 算法

程序必须从数据文件读取并计算文件中每个数字的出现次数。一种方法是将六个不同的计数器变量 `count0`、`...`、`count5` 声明，并使用 `switch` 语句选择要递增的适当变量：

```
inStream >> numFailures;
if (inStream.eof()) break;
```

```
switch(numFailures)
{
    case 0: count0++;
    break;
    case 1: count1++;
    break;
    case 2: count2++;
    break;
    case 3: count3++;
    break;
    case 4: count4++;
    break;
    case 5: count5++;
}
```

然而，这种解决方案很笨拙，因为它要求我们声明和管理六个不同的计数器。此外，它不可扩展；如果公司创建了一个具有 10 个组件或 100 个组件的新产品，则必须大幅修改程序。

C 风格数组提供更好的解决方案。我们定义一个具有六个不同整数值的空间的单个数组对象：

```
const int SIZE = 6;
int count[SIZE] = {0};
```

此定义创建了一个名为 `count` 的索引变量，可以存储六个整数。这些整数中的每一个在 0 到 5 范围内都有不同的索引。也就是说，`count` 中的第一个整数的索引为 0，第二个为 1，...，最后一个整数的索引为 5。该定义还将这些整数初始化为 0。我们可以按如下方式可视化此类对象：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_469_0.png)

由于 `count` 的索引值范围为 0 到 5，并且这些值与电路板上的组件数量一致，我们可以使用这一个数组来统计 0 到 5 每个值的出现次数，使用如下语句

```
instream >> numFailures;
if (instream.eof()) break;
count[numFailures]++;
```

将 1 加到 `count` 中索引为 `numFailures` 的整数上。例如，如果 `numFailures` 为 2，则执行

```
count[numFailures]++;
```

将递增 `count` 中索引为 2 的整数：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_470_0.png)

以下用于解决质量控制问题的算法使用这种方法。

## 质量控制分析算法

- 1. 提示并读取输入文件名到 `inputFileName`。

- 2. 打开一个名为 `inStream` 的 `ifstream` 到名称为 `inputFileName` 的文件。 （如果失败，显示错误消息并停止执行。）

- 3. 将 `numCircuitBoards` 初始化为 0。

- 4. 将数组 `count` 中的每个整数初始化为 0。

- 5. 循环：

- a. 从 `inStream` 读取一个整数 `numFailures`。

- b. 如果读取了文件结束标记，则退出循环。

- c. 递增 `count` 中由 `numFailures` 索引的元素。

- d. 递增 `numCircuitBoards`。

- 结束循环

- 6. 关闭 `inStream`。

- 7. 对于 0 到 5 范围内的每个索引：

- 显示索引和 `count[index]` 并附带适当的标签。

### 12.1.2.5 编码

示例 12.1 中的程序实现了此算法。

## 示例 12.1 质量控制故障频率分布

```
/* This program shows a distribution of component failure rates that
are stored in an input file.

Input(file):     a sequence of failure rates
Output(screen): the number and percentage of occurrences of each
                 failure rate
---------------------------------------------------------------*/

#include <iostream>      // cout, <<, fixed, showpoint
```

```
#include <fstream>          // ifstream, >>, eof(), close()
#include <iomanip>          // setprecision()
#include <string>           // string, getline()
#include <cassert>          // assert()
using namespace std;

const int CAPACITY = 6;      // # of array elements
int main()
{
    cout << "Quality Control: "
         "Component Failure Frequency Distribution.\n\n";

    ifstream inStream;
    string inFileName;
    cout << "Name of input file? ";
    getline(cin, inFileName);
    inStream.open(inFileName.data());
    assert(inStream.is_open());

    int count[CAPACITY] = {0},   // array of counters
        numFailures,             // input variable
        numCircuitBoards = 0;    // # of input values

    for (;;)                   // loop:
    {
        inStream >> numFailures;   // read input value
        if (inStream.eof()) break; // if done, stop reading
        count[numFailures]++;      // increment its counter
        numCircuitBoards++;        // one more input value
    }                          // end loop
    inStream.close();          // close the stream

    cout << "\nOut of " << numCircuitBoards << " circuit boards:\n"
         << setprecision(1) << fixed << showpoint;

    for (int i = 0; i < CAPACITY; i++)  // output counters
        cout << count[i] << " had " << i
             << " failed components ("  // and percentages
             << double(count[i]) / numCircuitBoards * 100
             << "%)" << endl;
}
```

## 样本运行：

Quality Control: Component Failure Frequency Distribution.

Enter the name of the input file: failureData.txt

Out of 120 circuit boards:

98 had 0 failed components (81.7%)

16 个有 1 个失效组件（13.3%）

3 个有 2 个失效组件（2.5%）

2 个有 3 个失效组件（1.7%）

1 个有 4 个失效组件（0.8%）

0 个有 5 个失效组件（0.0%）

## 12.2 C-STYLE ARRAYS

程序在示例 12.1 中使用了声明

```
const int CAPACITY = 6;      // # of array elements
.
.
int count[CAPACITY] = {0};    // array of counters
.
.
.
```

构造 `count` 为一个包含六个整数的数组，每个整数初始化为 0。声明的第一个部分

```
int count[CAPACITY] = {0};    // array of counters
```

指示编译器为存储六个整数值预留一块足够大的内存，并将名称 `count` 与该块关联。因为 `count` 可容纳六个整数，所以其容量被认为是 6。`count` 中的整数大小的空间称为元素，并从 0 到 5 索引：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_472_0.png)

与某些语言不同，C++ 数组是零基的；也就是说，任何 C++ 数组的第一个元素的索引始终为零。

声明的第二部分，

```
int count[CAPACITY] = {0};    // array of counters
```

将 `count` 的第一个元素初始化为零，并且如后面所述，其余元素默认初始化为零：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_472_1.png)

而数组的容量是它可以存储的值的数量，其大小是它实际包含的值的数量。`count` 的容量和大小均为 6。

在此示例中，`count` 是整数数组，但数组的元素可以是任何类型。例如，声明

```
const int NUM_ELEMENTS = 4;
char charArray[NUM_ELEMENTS];      // array of 4 char elements
double realArray[NUM_ELEMENTS];    // array of 4 double elements
string stringArray[NUM_ELEMENTS];  // array of 4 string elements
```

构造了三个数组，每个都有四个元素（即容量为 4），但每个都不包含值（即每个大小为 0）；`charArray` 为四个字符提供空间（每个存储在 1 字节中），

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_473_0.png)

`realArray` 为四个 `double` 值提供空间（每个通常存储在 4 字节中），

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_473_1.png)

`stringArray` 为四个 `string` 对象提供空间，其存储需求根据存储的字符串值的长度而变化。

这些声明是以下（简化）数组声明形式的示例：

### ARRAY DECLARATION (SIMPLIFIED)

### Form:

```
type array_name[CAPACITY];
```

其中：

- `type` 是任何已定义的类型（预定义或程序员定义）；

- `array_name` 是被声明的数组对象的名称；并且

- `CAPACITY` 是对象可以包含的值的数量。

### Purpose:

指示编译器为存储 `CAPACITY` 个 `type` 类型的对象预留足够的存储空间，并将名称 `array_name` 与该存储空间关联。

为了理解数组声明的含义，有用的是将 `char` 数组与 `string` 对象进行对比：

```
const int CAPACITY = 16;
char charArray[CAPACITY];
string aString;
```

`charArray` 的容量固定为 16 字节，并且在程序执行期间不会改变。相比之下，对象 `aString` 是一个具有可变容量（初始容量为零）的容器；它会根据存储其中的字符数量按需自动增长。

必须记住 C 风格数组的这一属性：与 `string` 对象不同，C 风格数组的容量在程序编译时就已固定。如果我们尝试在运行时输入容量，如

```
cout << "Enter the number of components: ";
int arrayCapacity;
cin >> arrayCapacity;
int count[arrayCapacity];    // ERROR!
```

将导致编译错误。原因是 C 风格数组的内存由编译器分配，因此数组的容量必须在其定义被编译时可用。

良好的编程实践是使用整数常量来指定数组的容量，如

```
const int CAPACITY = 5;
double count[CAPACITY];
.
.
.
for (int i = 0; i < CAPACITY; i++)
    cout << count[i] << endl;
```

而不是使用整数字面量：

```
double count[5];
.
.
.
for (int i = 0; i < 5; i++)
    cout << count[i] << endl;
```

这使程序更具灵活性。有时在程序的最终版本完成之前需要多次调整数组的容量，或在程序使用一段时间后修改容量。如果使用字面量，则进行这些修改需要找到并更改整个程序中的每个字面量：

```
double count[100];
.
.
.
```

```
for (int i = 0; i < 100; i++)
    cout << count[i] << endl;
```

但如果在整个程序中使用命名常量（如 `CAPACITY`），则修改数组容量只需要一次修改——更改命名常量的声明：

```
const int CAPACITY = 100;
double count[CAPACITY];
.
.
for (int i = 0; i < CAPACITY; i++)
    cout << count[i] << endl;
```

重新编译程序后，编译器会将 `CAPACITY` 的所有使用更新为新值，节省时间并确保所有数组访问中的容量一致。

## 12.2.1 Array Initialization

如前所述，形式为

```
type array_name[CAPACITY];
```

的简单数组声明未为数组指定初始化。因为没有提供初始值，这样的数组通常会包含分配给数组的内存块先前使用时遗留的“垃圾”值。

因为数组可以在其元素中存储不同的值，所以它不能用单个值初始化：

```
int intArray[CAPACITY] = 0;    // ERROR!
```

相反，可以使用数组字面量；这是在大括号 `{` 和 `}` 之间列出的一系列初始化值，并用逗号分隔；例如，

```
const int CAPACITY = 10;
int intArray[CAPACITY] = {9,8,7,6,5,4,3,2,1,0};
```

列表中的第一个值存储在第一个数组元素中，第二个值存储在第二个元素中，以此类推，结果对象可以如下图所示：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_475_0.png)

如果列出的初始值数量少于数组的容量，则未提供初始值的那些元素各自设置为零。例如，声明

```
const int CAPACITY = 10;
double intArray[CAPACITY] = {9,8,7,6,5,4};    // Okay!
```

将按如下方式构造 `intArray`：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_476_0.png)

示例 12.1 中的程序使用了此功能来初始化计数器数组：

```
int count[CAPACITY] = {0};
```

此声明显式地将第一个元素初始化为 0，并隐式地将剩余元素初始化为零默认值。对于计数器数组需要这种初始化，因为如果在数组定义中未提供初始化，则数组中的值将未定义并且可能包含“垃圾”值。
