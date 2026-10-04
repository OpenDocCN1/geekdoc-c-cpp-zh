

- 11. (Debug) 确定并纠正以下程序中的错误。

- a. 
```cpp
#include <iostream>
using namespace std;
int main() {
    int width = 15;
    int area = length * width;
    cout << "The area is " << area;
}
```

- b. 
```cpp
#include <iostream>
using namespace std;
int main() {
    int length, width, area;
    length = 20;
    width = 15;
    area = length * width;
    cout << "The area is " << area;
    return 0;
}
```

- c. 
```cpp
#include <iostream>
int main() {
    int length = 20, width = 15, area;
    area = length * width;
    cout << "The area is " << area;
    return 0;
}
```

- 12. (Debug) 错误地将程序 3.3 中的语句重新排序如下：

```cpp
#include <iostream>
using namespace std;

int main() {
    int sum;
    sum = 0;
    sum = sum + 96;
    sum = sum + 70;
    sum = sum * 85;
    sum = sum * 60;
    cout << "The value of sum is initially set to " << sum << endl;
    cout << "sum is now " << sum << endl;
    cout << "sum is now " << sum << endl;
    cout << "sum is now " << sum << endl;
    cout << "The final sum is " << sum << endl;

    return 0;
}
```

确定该程序的输出结果。

## 第 3 章 117 页
程序输出的数字格式化

13. **(通用数学)** 使用程序 3.1，通过确定具有以下半径和高度的圆柱体积，来完成下表：

| 半径 (in) | 高 (in) | 体积 |
|---|---|---|
| 1.62 | 6.23 | |
| 2.86 | 7.52 | |
| 4.26 | 8.95 | |
| 8.52 | 10.86 | |
| 12.29 | 15.35 | |

14. **(通用数学)** 椭圆的面积（见图 3.5）由以下公式给出：
$Area = \pi a b$ 

使用该公式，编写一个 C++ 程序来计算短轴 $a$ 为 2.5 英寸、长轴 $b$ 为 6.4 英寸的椭圆面积。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_136_0.png)

**图 3.5** 椭圆的短轴 $a$ 和长轴 $b$

15. **(修改)** 修改程序 3.1，计算该程序中确定的钢制圆柱的重量（磅）。确定重量的公式为：
$weight = 0.28 (\pi)(r^2)h$

$r$ 是半径（英寸）。
$h$ 是圆柱的高度（英寸）。

## 3.2 程序输出的数字格式化

除了显示正确结果外，程序还应该以具有吸引力的形式呈现结果。大多数程序的判断标准取决于数据录入的感易易程度以及输出的风格和呈现方式。例如，将货币结果显示为 1.897 不符合接受的报告规范。根据使用四舍五入还是截断，显示应为 $1.90 或 $1.89。

> “如第 2 章所述，`endl` 操纵符插入一个新行，然后强制所有插入的内容立即显示，这被称为‘刷新流’。”

## 第 3 章 119 页

程序输出的数字格式化
表 3.1 常用流操纵符（续）

```cpp
#include <iostream>
using namespace std;

int main() {
  cout << 6 << endl;
  cout << 18 << endl;
  cout << 124 << endl;
  cout << "-----\n";
  cout << (6+18+124) << endl;

  return 0;
}
```

## 赋值、格式化与交互输入

程序 3.5 的输出如下：

```
6
18
124
--
148
```

由于程序 3.5 中没有使用字段宽操纵符，`cout` 在接收每个数字时都会分配足够的空间。要强制数字在个位上对齐，需要的字段宽足以容纳最大的显示数字，对于程序 3.5 中的数字来说，宽度为三。程序 3.6 显示了字段宽的使用。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_139_0.png)

## 程序 3.6

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    cout << setw(3) << 6 << endl
    << setw(3) << 18 << endl
    << setw(3) << 124 << endl

    return 0;
}
```

程序 3.6 的输出如下：

```
  6
 18
124
```

## 章 121 页
程序输出的数字格式化

格式化数字需要字段宽操纵符。要强制数字在个位上对齐，需要的字段宽足以容纳最大的显示数字。

