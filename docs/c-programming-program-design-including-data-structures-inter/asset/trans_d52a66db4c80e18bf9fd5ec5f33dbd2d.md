
```cpp
cout << endl;
for (j = 0; j < 5; j++)
{
    two[j] = 2 * one[j] - 1;
    two[j + 5] = one[4 - j] + two[j];
}

cout << "Two contains: ";
for (j = 0; j < 10; j++)
    cout << two[j] << " ";
cout << endl;

return 0;
}
```

- **27.** 以下 C++ 代码的输出是什么？

```cpp
const double PI = 3.14159;
double cylinderRadii[5] = {3.5, 7.2, 10.5, 9.8, 6.5};
double cylinderHeights[5] = {10.7, 6.5, 12.0, 10.5, 8.0};
double cylinderVolumes[5];

cout << fixed << showpoint << setprecision(2);

for (int i = 0; i < 5; i++)
    cylinderVolumes[i] = 2 * PI * cylinderRadii[i]
                         * cylinderHeights[i];

for (int i = 0; i < 5; i++)
    cout << (i + 1) << " " << cylinderRadii[i] << " "
         << cylinderHeights[i] << " " << cylinderVolumes[i] << endl;
```

- **28.** 当数组作为实参传递给函数时，实际传递的是什么？

- **29.** 在 C++ 中，数组作为实参可以按值传递吗？

- **30.** 使用本章讨论的选择排序算法对下列列表进行排序。显示外层 for 循环每次迭代后的列表。

  6, 45, 10, 25, 58, 2, 50, 30, 86

- **31.** 使用本章讨论的选择排序算法对下列列表进行排序。显示外层 for 循环每次迭代后的列表。

  36, 55, 17, 35, 63, 85, 12, 48, 3, 66

- **32.** 给定以下声明：

  ```cpp
  char string15[16];
  ```

  将下列语句标记为有效或无效。如果语句无效，请解释原因。

  - a. `strcpy(string15, "Hello there");`
  - b. `strlen(string15);`
  - c. `string15 = "Jacksonville";`

- **36.** 假设有以下声明：

  ```cpp
  char name[21];
  char yourName[21];
  char studentName[31];
  ```

  将下列语句标记为有效或无效。如果语句无效，请解释原因。

  - a. `cin >> name;`
  - b. `cout << studentName;`
  - c. `yourName[0] = '\0';`
  - d. `yourName = studentName;`
  - e.
    ```cpp
    if (yourName == name)
        studentName = name;
    ```
  - f. `int x = strcmp(yourName, studentName);`
  - g. `strcpy(studentName, name);`
  - h.
    ```cpp
    for (int j = 0; j < 21; j++)
        cout << name[j];
    ```

- **37.** 定义一个名为 `temp` 的 `int` 类型二维数组，三行四列，使得第一行初始化为 6, 8, 12, 9；第二行初始化为 17, 5, 10, 6；第三行初始化为 14, 13, 16, 20。

- **38.** 假设数组 `temp` 如习题 37 所定义。编写 C++ 语句完成以下操作：

  - a. 输出 `temp` 中第一行第一列元素的内容。
  - b. 输出 `temp` 中第一行最后一列元素的内容。
  - c. 输出 `temp` 中最后一行第一列元素的内容。
  - d. 输出 `temp` 中最后一行最后一列元素的内容。

- **39.** 考虑以下声明：

  ```cpp
  const int CAR_TYPES = 5;
  const int COLOR_TYPES = 6;

  double sales[CAR_TYPES][COLOR_TYPES];
  ```

  - a. 数组 `sales` 有多少个分量？
  - b. 数组 `sales` 有多少行？
  - c. 数组 `sales` 有多少列？
  - d. 要按 `CAR_TYPES` 对销售额求和，需要哪种处理？
  - e. 要按 `COLOR_TYPES` 对销售额求和，需要哪种处理？

- **40.** 编写完成以下操作的 C++ 语句：

  - a. 声明一个 `int` 类型的数组 `alpha`，10 行 20 列。
  - b. 将数组 `alpha` 初始化为 0。
  - c. 在第一行存储 1，在其余行存储 2。
  - d. 在第一列存储 5，并确保后续每一列的值是前一列值的两倍。
  - e. 打印数组 `alpha`，每行打印一行。
  - f. 打印数组 `alpha`，每行打印一列。

- **41.** 考虑以下声明：

  ```cpp
  int beta[3][3];
  ```

  下列每条语句执行后，`beta` 中存储的是什么？

  - a.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 0;
    ```
  - b.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i + j;
    ```
  - c.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i * j;
    ```
  - d.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 2 * (i + j) % 4;
    ```

- **42.** 假设你有以下声明：

  ```cpp
  int times[30][7];
  int speed[15][7];
  int trees[100][7];
  int students[50][7];
  ```

  - a. 编写函数 `print` 的定义，该函数可用于输出这些数组的内容。
  - b. 编写调用函数 `print` 以输出数组 `times`、`speed`、`trees` 和 `students` 内容的 C++ 语句。

## 编程练习

- **1.** 编写一个 C++ 程序，声明一个包含 50 个 `double` 类型分量的数组 `alpha`。初始化该数组，使前 25 个分量等于索引变量的平方，后 25 个分量等于索引变量的三倍。输出该数组，使每行打印 10 个元素。
- **2.** 编写一个 C++ 函数 `smallestIndex`，它接收一个 `int` 数组及其大小作为参数，并返回该数组中最小元素第一次出现的索引。同时，编写一个程序测试你的函数。
- **3.** 编写一个 C++ 函数 `largestIndex`，它接收一个 `int` 数组及其大小作为参数，并返回该数组中最大元素最后一次出现的索引。同时，编写一个程序测试你的函数。

- **8.** 考虑以下函数 `main`：

  ```cpp
  int main()
  {
      int inStock[10][4];
      int alpha[20];
      int beta[20];
      int gamma[4] = {11, 13, 15, 17};
      int delta[10] = {3, 5, 2, 6, 10, 9, 7, 11, 1, 8};

      .
      .
      .
  }
  ```

  - a. 编写函数 `setZero` 的定义，该函数将任意 `int` 类型的一维数组初始化为 0。
  - b. 编写函数 `inputArray` 的定义，该函数提示用户输入 20 个数字，并将这些数字存储到 `alpha` 中。
  - c. 编写函数 `doubleArray` 的定义，该函数将 `beta` 的元素初始化为 `alpha` 中对应元素的两倍。确保防止该函数修改 `alpha` 的元素。
  - d. 编写函数 `copyGamma` 的定义，该函数将 `inStock` 第一行的元素设置为 `gamma`，并将 `inStock` 其余行设置为 `inStock` 前一行的三倍。确保防止该函数修改 `gamma` 的元素。
  - e. 编写函数 `copyAlphaBeta` 的定义，该函数将 `alpha` 存储到 `inStock` 的前五行，将 `beta` 存储到 `inStock` 的后五行。确保防止该函数修改 `alpha` 和 `beta` 的元素。
  - f. 编写函数 `printArray` 的定义，该函数打印任意 `int` 类型的一维数组。每行打印 15 个元素。
  - g. 编写函数 `setInStock` 的定义，该函数提示用户输入 `inStock` 第一列的元素。然后，该函数应将剩余列中的元素设置为前一列对应元素的两倍减去 `delta` 中对应元素。
  - h. 编写 C++ 语句，调用 a 到 g 部分中的每个函数。
  - i. 编写一个 C++ 程序，测试函数 `main` 以及 a 到 g 部分讨论的函数。（根据需要添加其他函数，例如打印二维数组。）

- **9.** 编写一个程序，使用二维数组存储一年中每个月的最高和最低温度。该程序应输出全年平均最高温度、平均最低温度以及最高和最低温度。你的程序必须包含以下函数：

  - a. **函数 `getData`：** 该函数读取数据并存储到二维数组中。
  - b. **函数 `averageHigh`：** 该函数计算并返回全年平均最高温度。
  - c. **函数 `averageLow`：** 该函数计算并返回全年平均最低温度。
  - d. **函数 `indexHighTemp`：** 该函数返回数组中最高高温的索引。
  - e. **函数 `indexLowTemp`：** 该函数返回数组中最低低温的索引。

  *（这些函数都必须具有适当的参数。）*

- **10.** 第 6 章中的编程练习 10 要求你求五个数的均值和标准差。扩展该编程练习，求最多 100 个数的均值和标准差。假设 *n* 个数 *x₁, x₂, ..., xₙ* 的均值（平均数）为 *x̄*。那么，这些数的标准差为：

  $$s = \sqrt{\frac{(x_1 - \bar{x})^2 + (x_2 - \bar{x})^2 + \cdots + (x_i - \bar{x})^2 + \cdots + (x_n - \bar{x})^2}{n}}$$

- **11.（大整数相加）** 在 C++ 中，最大的 `int` 值是 2147483647。因此，比它更大的整数不能作为整数存储和处理。同样，如果两个正整数的和或积大于 2147483647，结果将不正确。存储和操作大整数的一种方法是将数字的每一位分别存储在数组中。编写一个程序，输入两个最多 20 位的正整数，并输出这些数的和。如果这些数的和超过 20 位，请输出该和并给出适当消息。你的程序必须至少包含一个函数，用于读取数字或将数字存储到数组中，以及另一个函数，用于输出这些数字的和。*（提示：将数字作为字符串读取，并按相反顺序存储该数字的各位数字。）*

- **12.** Jason、Samantha、Ravi、Sheila 和 Ankit 正在为即将到来的马拉松做准备。一周中的每一天，他们都会跑一定数量的英里，并把它们写进笔记本。周末时，他们想知道每天跑过的英里数、本周总英里数以及每天平均跑过的英里数。编写一个程序帮助他们分析数据。你的程序必须包含并行数组：一个数组存储跑步者的姓名，一个五行七列的二维数组存储每位跑步者每天跑过的英里数。此外，你的程序必须至少包含以下函数：一个函数用于读取并存储跑步者的姓名以及每天跑过的英里数；一个函数用于求每位跑步者跑过的总英里数以及平均数值
