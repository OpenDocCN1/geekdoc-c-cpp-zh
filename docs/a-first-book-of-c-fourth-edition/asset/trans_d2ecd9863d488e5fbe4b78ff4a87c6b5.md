

**8. (Program)** a. 编写一个声明以将字符串 `"This is a test"` 存储在名为 `strtest` 的数组中。将该声明包含在一个程序中，使用下面的循环显示该消息：

```cpp
for (i = 0; i < NUMDISPLAY; i++)
    cout << strtest[i];
```

`NUMDISPLAY` 是数字 14 的命名常量。

b. 修改练习 8a 中的 `for` 语句以仅显示数组字符 `t`、`e`、`s` 和 `t`。

c. 将练习 8a 中编写的数组声明包含在一个程序中，该程序使用 `cout` 语句显示数组中的字符。例如，语句 `cout << strtest;` 会导致 `strtest` 数组中存储的字符串被显示。使用该语句需要使 `\0` 作为数组中最后一个字符的结束字符串标记。

d. 重复练习 8a，使用 `while` 循环。 *(提示：当检测到 `\0` 转义序列时停止循环。表达式 `while (strtest[i] != '\0')` 可以使用。)*

## 7.3 数组作为参数

数组元素以与标量变量相同的方式传递给被调用函数。它们在函数调用时简单地作为下标变量包含。例如，以下函数调用将元素 `grades[2]` 和 `grades[6]` 的值传递给函数 `findMax()`：

```
findMax(grades[2], grades[6]);
```

将完整数组的值传递给函数在许多方面比传递每个元素更容易。被调用函数接收对实际数组的访问权，而不是数组中值的副本。例如，如果 `grades` 是一个数组，函数调用 `findMax(grades);` 使完整的 `grades` 数组可供 `findMax()` 函数使用。此函数调用与将单个变量传递给函数不同。

回想一下，当单个标量参数传递给函数时（参见第 6.1 节），被调用函数仅接收传递值的副本，该副本存储在函数的一个参数中。如果数组以这种方式传递，则必须创建完整数组的副本。对于大型数组，每次函数调用都制作副本会浪费计算机存储，并挫败由被调用程序所做的多元素更改的返回努力。（请记住，一个函数最多返回一个值。）

为了避免这些问题，被调用函数被赋予对原始数组的直接访问权。³ 这样，被调用函数所做的任何更改都是直接对数组进行的。对于以下函数调用的示例，数组 `nums`、`keys`、`units` 和 `grades` 声明如下：

```
int nums[5];                 // an array of 5 integers
char keys[256];              // an array of 256 characters
double units[500], grades[500]; // two arrays of 500 doubles
```

## 数组

对于这些数组，可以进行以下函数调用；请注意，在每种情况下，被调用函数都直接访问命名的数组：

```
findMax(nums);
findCharacter(keys);
calcTotal(nums, units, grades);
```

在接收端，被调用函数必须被告知正在提供一个数组。例如，以下是前述函数的合适函数头：

```
int findMax(int vals[5])
char findCharacter(char inKeys[256])
void calcTotal(int arr1[5], double arr2[500], double arr3[500])
```

在每个函数头中，程序员选择参数列表中的名称。然而，函数使用的参数名称仍然引用函数外部创建的原始数组，正如程序 7.4 所阐明的那样。

## 程序 7.4

```
#include <iostream>
using namespace std;

const int MAXELS = 5;
int findMax(int [MAXELS]);  // function prototype

int main()
{
    int nums[MAXELS] = {2, 18, 1, 27, 16};

    cout << "The maximum value is " << findMax(nums) << endl;

    return 0;
}

// find the maximum value
int findMax(int vals[MAXELS])
{
    int i, max = vals[0];

    for (i = 1; i < MAXELS; i++)
        if (max < vals[i])
            max = vals[i];

    return max;
}
```

首先，注意符号常量 `MAXELS` 已在全局声明，而非在 `main()` 函数中。此声明的放置方式意味着此符号常量可在任何后续声明或函数中使用。接下来，注意 `findMax()` 的函数原型使用此符号常量并声明 `findMax` 返回一个整数并期望一个包含五个整数的数组作为参数。还重要的是要知道，程序 7.4 中只创建了一个数组。在 `main()` 中，此数组称为 `nums`，在 `findMax()` 中，数组称为 `vals`。正如图 7.5 所示，两个名称都引用同一个数组，因此 `vals[3]` 与 `nums[3]` 相同。

```
int main()
{
    int nums[5];
    .
    .
    .
    findMax(nums);
    returns 0;
}
int findMax(int vals[5])
{
    .
    .
    .
}
```

![](img/202cface8244f523c2641baa2e00d7dd_328_0.png)

**图 7.5**  只创建了一个数组

`findMax()` 原型和函数头中的参数声明实际上包含函数不需要的额外信息。`findMax()` 必须知道的全部是参数 `vals` 引用一个整数数组。因为数组已在 `main()` 中创建，并且在 `findMax()` 中不需要额外的存储空间，所以 `vals` 的声明可以省略数组大小。因此，以下是替代的函数头：

```
int findMax(int vals[])
```

当你意识到在函数被调用时，实际上只向 `findMax()` 传递了一项时，此函数头的形式更有意义：`nums` 数组的起始地址，如图 7.6 所示。

## 数组

![](img/202cface8244f523c2641baa2e00d7dd_329_0.png)

**图 7.6**  传递数组的起始地址

由于只将 `vals` 的起始地址传递给 `findMax()`，因此无需在 `vals` 的声明中包含数组中的元素数。⁴ 事实上，通常建议从函数头中省略数组大小。例如，此更通用的 `findMax()` 形式可用于查找任意大小的整数数组的最大值：

```
int findMax(int vals[], int NUMELS)   // find the maximum value
{
    int i, max = vals[0];

    for (i = 1; i < NUMELS; i++)
        if (max < vals[i])
            max = vals[i];

    return max;
}
```

`findMax()` 的更通用形式声明函数返回一个整数值。函数期望整数数组的起始地址和数组中的元素数作为参数。然后，使用元素数作为搜索的边界，函数的 `for` 循环导致每个数组元素按顺序检查以定位最大值。程序 7.5 显示了在完整程序中使用 `findMax()` 的更通用形式。

## 程序 7.5

```
#include <iostream>
using namespace std;

int findMax(int [], int);  // function prototype

int main()
{
    const int MAXELS = 5;
    int nums[MAXELS] = {2, 18, 1, 27, 16};

    cout << "The maximum value is " << findMax(nums, MAXELS) << endl;

    return 0;
}

// find the maximum value
int findMax(int vals[], int numels)
{
    int i, max = vals[0];

    for (i = 1; i < numels; i++)
        if (max < vals[i]) max = vals[i];

    return max;
}
```

程序 7.4 和 7.5 显示的输出如下：

```
The maximum value is 27
```

## 练习 7.3

- 1. (Practice) 使用以下声明创建了 grades 数组：
  const int NUMGRADES = 500;
  double grades[NUMGRADES];
  编写两个不同的函数头，为名为 sortArray() 的函数接受 grades 数组作为参数名 inArray 并返回无值。

- 2. (Practice) 使用以下声明创建了 keys 数组：
  const int NUMKEYS = 256;
  char keys[NUMKEYS];
  编写两个不同的函数头，为名为 findKey() 的函数接受 keys 数组作为参数名 select 并返回一个字符。

- 3. (Practice) 使用以下声明创建了 rates 数组：

```
const int NUMRATES = 256;
double rates[NUMRATES];
```

编写两个不同的函数头，为名为 prime() 的函数接受 rates 数组作为参数名 rates 并返回一个双精度数。

- 4. (Modify) a. 修改程序 7.4 中的 findMax() 函数以定位传递数组的最小值。
  b. 将练习 4a 中编写的函数包含在完整程序中并运行该程序。

- 5. (Program) 编写、编译并运行一个 C++ 程序，该程序在 main() 中有一个声明以将以下数字存储在名为 rates 的数组中：6.5、7.2、7.5、8.3、8.6、9.4、9.6、9.8 和 10.0。应有一个对 show() 的函数调用，该函数接受 rates 数组作为参数名 rates，然后显示数组中的数字。

- 6. (Program) a. 编写、编译并运行一个 C++ 程序，该程序在 main() 中有一个声明以将字符串 "Vacation is near" 存储在名为 message 的数组中。应有一个对 display() 的函数调用，该函数接受 message 在参数名 string 中然后显示该消息。
  b. 修改练习 6a 中编写的 display() 函数以显示 message 数组的前八个元素。

- 7. (Program) 编写、编译并运行一个 C++ 程序，该程序声明三个一维数组名为 price、quantity 和 amount。每个数组应在 main() 中声明并能够容纳 10 个双精度数。要存储在 price 中的数字为 10.62、14.89、13.21、16.55、18.62、9.47、6.58、18.32、12.15 和 3.98。要存储在 quantity 中的数字为 4、8.5、6、7.35、9、15.3、3、5.4、2.9 和 4.8。你的程序应将这三个数组传递给名为 extend() 的函数，该函数应计算 amount 数组中的元素作为 price 和 quantity 数组中对应元素的乘积（例如，amount[1] = price[1] * quantity[1]）。extend() 将值传递给 amount 数组后，数组中的值应从 main() 中显示。

- 8. (Program) 编写、编译并运行一个 C++ 程序，该程序包含两个名为 calcavg() 和 variance() 的函数。calcavg() 函数应计算并返回存储在名为 testvals 的数组中的值的平均值。数组应在 main() 中声明并包含值 89、95、72、83、99、54、86、75、92、73、79、75、82 和 73。variance() 函数应计算并返回数据的方差。方差是通过从 testvals 中的每个值中减去平均值，对得到的值进行平方，将它们相加并除以 testvals 中的元素数得到的。从 calcavg() 和 variance() 返回的值应使用 main() 中的 cout 语句显示。

