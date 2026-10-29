
8. （程序题）a. 编写一个声明，将字符串 `"This is a test"` 存储到名为 `strtest` 的数组中。将该声明包含在一个使用以下循环显示该消息的程序中：

```
for (i = 0; i < NUMDISPLAY; i++)
    cout << strtest[i];
```

`NUMDISPLAY` 是表示数字 14 的命名常量。

b. 修改练习 8a 中的 `for` 语句，使其仅显示数组中的字符 t、e、s 和 t。

c. 将练习 8a 中编写的数组声明包含在一个使用 `cout` 语句显示数组中字符的程序中。例如，语句 `cout << strtest;` 会显示存储在 `strtest` 数组中的字符串。使用该语句要求数组的最后一个字符是字符串结束标记 `\0`。

d. 使用 `while` 循环重复练习 8a。*（提示：当检测到 `\0` 转义序列时停止循环。可以使用表达式 `while (strtest[i] != '\0')`。）*

## 7.3 数组作为参数

数组元素与标量变量一样，以相同的方式传递给被调函数。进行函数调用时，只需将它们作为下标变量包含在内即可。例如，以下函数调用将元素 `grades[2]` 和 `grades[6]` 的值传递给函数 `findMax()`：

```
findMax(grades[2], grades[6]);
```

在许多方面，将整个值数组传递给函数比逐个传递每个元素更容易。被调函数可以访问实际的数组，而不是数组中值的副本。例如，如果 `grades` 是一个数组，函数调用 `findMax(grades);` 会使完整的 grades 数组可供 `findMax()` 函数使用。这种函数调用与向函数传递单个变量不同。

回顾一下，当向函数传递单个标量参数时（参见第 6.1 节），被调函数只接收所传值的一个副本，该副本存储在该函数的一个参数中。如果以这种方式传递数组，就必须创建整个数组的副本。对于大型数组，为每次函数调用制作副本会浪费计算机存储空间，并且会使被调程序对多个元素所做的修改难以返回。（请记住，函数最多返回一个值。）

为了避免这些问题，被调函数被赋予对原始数组的直接访问权限。³ 这样，被调函数所做的任何更改都会直接作用于该数组。对于以下函数调用示例，数组 `nums`、`keys`、`units` 和 `grades` 的声明如下所示：

```
int nums[5];                 // an array of 5 integers
char keys[256];              // an array of 256 characters
double units[500], grades[500]; // two arrays of 500 doubles
```

对于这些数组，可以进行以下函数调用；请注意，在每种情况下，被调函数都可以直接访问所提到的数组：

```
findMax(nums);
findCharacter(keys);
calcTotal(nums, units, grades);
```

在接收方，必须告知被调函数将有一个数组可用。例如，以下是与上述函数相对应的合适函数头：

```
int findMax(int vals[5])
char findCharacter(char inKeys[256])
void calcTotal(int arr1[5], double arr2[500], double arr3[500])
```

在每个函数头中，程序员可以自行选择参数列表中的名称。但是，函数使用的参数名称仍然引用在函数外部创建的原始数组，正如程序 7.4 所阐明的那样。

### 程序 7.4

![](img/e9bf940282dfb289356f077151cc69dd_327_0.png)

```
#include <iostream>
using namespace std;

const int MAXELS = 5;
int findMax(int [MAXELS]); // function prototype

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

首先，请注意符号常量 `MAXELS` 是在全局范围内声明的，而不是在 `main()` 函数中。这种声明位置意味着该符号常量可以在任何后续声明或函数中使用。其次，注意 `findMax()` 的函数原型使用了该符号常量，并声明 `findMax` 返回一个整数，且期望一个包含五个整数的数组作为参数。同样重要的是要知道，在程序 7.4 中只创建了一个数组。在 `main()` 中，该数组称为 `nums`，而在 `findMax()` 中，该数组称为 `vals`。如图 7.5 所示，这两个名称引用的是同一个数组，因此 `vals[3]` 与 `nums[3]` 是同一个元素。

```
int main()
{
    int nums[5];
    .
    .
    .
    findMax(nums);
    return 0;
}
int findMax(int vals[5])
{
    .
    .
    .
}
```

![](img/e9bf940282dfb289356f077151cc69dd_328_0.png)

图 7.5  只创建一个数组

`findMax()` 原型和函数头中的参数声明实际上包含了一些该函数并不需要的信息。`findMax()` 只需要知道参数 `vals` 引用一个整数数组即可。由于数组已在 `main()` 中创建，且 `findMax()` 中不需要额外的存储空间，因此 `vals` 的声明可以省略数组大小。因此，以下是一个替代的函数头：

```
int findMax(int vals[])
```

当你意识到调用该函数时实际上只向 `findMax()` 传递了一项内容，即 nums 数组的起始地址（如图 7.6 所示），这种函数头形式就更容易理解了。

## 数组

![](img/e9bf940282dfb289356f077151cc69dd_329_0.png)

**图 7.6** 传递数组的起始地址

由于只将 vals 的起始地址传递给 `findMax()`，因此数组的元素个数不必包含在 vals 的声明中。[^4] 事实上，通常建议从函数头中省略数组大小。例如，下面这种更通用的 `findMax()` 形式可用于查找任意大小的整数数组中的最大值：

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

更通用的 `findMax()` 形式声明该函数返回一个整数值。该函数期望以整数数组的起始地址和数组元素个数作为参数。然后，函数以元素个数作为搜索边界，通过 `for` 循环按顺序检查每个数组元素，以找出最大值。程序 7.5 演示了在一个完整程序中使用更通用的 `findMax()` 形式。

## 数组

为一个名为 `findKey()` 的函数编写两个不同的函数头，该函数接受 keys 数组作为名为 select 的参数，并返回一个字符。

3. **（练习）** 以下声明用于创建 rates 数组：

```cpp
const int NUMRATES = 256;
double rates[NUMRATES];
```

为一个名为 `prime()` 的函数编写两个不同的函数头，该函数接受 rates 数组作为名为 rates 的参数，并返回一个双精度数。

4. **（修改）**
   a. 修改程序 7.4 中的 `findMax()` 函数，使其找出所传递数组中的最小值。
   b. 将练习 4a 中编写的函数包含在一个完整程序中并运行该程序。

5. **（程序题）** 编写、编译并运行一个 C++ 程序，在 `main()` 中声明一个名为 rates 的数组，用于存储以下数字：6.5、7.2、7.5、8.3、8.6、9.4、9.6、9.8 和 10.0。程序中应有一个对 `show()` 的函数调用，该函数接受 rates 数组作为名为 rates 的参数，然后显示数组中的数字。

6. **（程序题）**
   a. 编写、编译并运行一个 C++ 程序，在 `main()` 中声明一个名为 message 的数组，用于存储字符串 "Vacation is near"。程序中应有一个对 `display()` 的函数调用，该函数在名为 string 的参数中接受 message，然后显示该消息。
   b. 修改练习 6a 中编写的 `display()` 函数，使其显示 message 数组的前八个元素。

7. **（程序题）** 编写、编译并运行一个 C++ 程序，声明三个一维数组，分别名为 price、quantity 和 amount。每个数组都应在 `main()` 中声明，并且能够容纳 10 个双精度数。要存储到 price 中的数字为 10.62、14.89、13.21、16.55、18.62、9.47、6.58、18.32、12.15 和 3.98。要存储到 quantity 中的数字为 4、8.5、6、7.35、9、15.3、5.4、2.9 和 4.8。程序应将这三个数组传递给名为 `extend()` 的函数，该函数应将 amount 数组中的元素计算为 price 和 quantity 数组中对应元素的乘积（例如，`amount[1] = price[1] * quantity[1]`）。在 `extend()` 将值传递给 amount 数组之后，应在 `main()` 中显示该数组中的值。

8. **（程序题）** 编写、编译并运行一个 C++ 程序，其中包含两个函数，分别名为 `calcavg()` 和 `variance()`。`calcavg()` 函数应计算并返回存储在名为 testvals 的数组中的值的平均值。该数组应在 `main()` 中声明，并包含以下值：89、95、72、83、99、54、86、75、92、73、79、75、82 和 73。`variance()` 函数应计算并返回数据的方差。方差的求法为：用 testvals 中的每个值减去平均值，对得到的各个值求平方，将它们相加，再除以 testvals 中的元素个数。`calcavg()` 和 `variance()` 返回的值应通过在 `main()` 中使用 `cout` 语句进行显示。

