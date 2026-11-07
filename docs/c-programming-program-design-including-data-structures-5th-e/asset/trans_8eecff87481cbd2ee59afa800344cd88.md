
- 21. 在 C++ 中，空字符表示为 `\0`。
- 22. 在 ASCII 字符集中，空字符的排序序列为 0。
- 23. C字符串存储在字符数组中。
- 24. 字符数组可以在声明时使用字符串表示法进行初始化。
- 25. C字符串的输入和输出是 C++ 允许聚合操作的唯一地方。
- 26. 头文件 `cstring` 包含可用于 C字符串操作的函数规范。
- 27. 常用的 C字符串操作函数包括 `strcpy`（字符串复制）、`strcmp`（字符串比较）和 `strlen`（字符串长度）。
- 28. C字符串逐字符比较。
- 29. 因为 C字符串存储在数组中，所以可以使用数组分量访问表示法访问 C字符串中的单个字符。
- 30. 并行数组用于保存相关信息。
- 31. 在二维数组中，元素以表格形式排列。
- 32. 要访问二维数组的元素，需要一对索引：一个表示行位置，一个表示列位置。
- 33. 在二维数组中，行编号为 0 到 `ROW_SIZE − 1`，列编号为 0 到 `COLUMN_SIZE − 1`。
- 34. 如果 `matrix` 是二维数组，那么 `matrix` 的基地址是数组分量 `matrix[0][0]` 的地址。
- 35. 在行处理中，二维数组一次处理一行。
- 36. 在列处理中，二维数组一次处理一列。
- 37. 将二维数组声明为形参时，可以省略第一维的大小，但不能省略第二维的大小。
- 38. 当二维数组作为实参传递时，实参数组和形参数组的列数必须匹配。
- 39. C++ 在计算机内存中以行顺序形式存储二维数组。

## 练习

- 1. 将以下陈述标记为真或假。
  - a. `double` 类型是简单数据类型的一个例子。
  - b. 一维数组是结构化数据类型的一个例子。
  - c. 数组可以按值或按引用作为参数传递给函数。
  - d. 函数可以返回数组类型的值。
  - e. 数组的大小在编译时确定。
  - f. 对 `int` 数组唯一允许的聚合操作是递增和递减操作。
  - g. 给定声明：

    ```cpp
    int list[10];
    ```

    语句：

    ```cpp
    list[5] = list[3] + list[2];
    ```

    更新数组 `list` 的第五个分量的内容。
  - h. 如果数组索引越界，程序总是以错误终止。
  - i. 在 C++ 中，字符串允许某些聚合操作。
  - j. 声明：

    ```cpp
    char name[16] = "John K. Miller";
    ```

    声明 `name` 为一个包含15个字符的数组，因为字符串 "John K. Miller" 只有14个字符。
  - k. 声明：

    ```cpp
    char str = "Sunny Day";
    ```

    声明 `str` 为一个长度未指定的字符串。
  - l. 作为参数，二维数组按值或按引用传递。

- 2. 考虑以下声明：

  ```cpp
  double salary[10];
  ```

  在此声明中，确定以下内容：

  - a. 数组名。
  - b. 数组大小。
  - c. 每个数组分量的数据类型。
  - d. 数组索引的取值范围。

- 3. 指出以下数组声明中的错误（如果有）。
  - a. `int list[10];`
  - b. `const int size = 100;`

    ```cpp
    double list[SIZE];
    ```

  - c. `int numList[0..9];`
  - d. `string names[20];`
  - e. `scores[50] double;`

- 4. 判断以下数组声明是否有效。如果声明无效，请解释原因。
  - a. `int list[75];`
  - b. 
    ```cpp
    int size;
    double list[size];
    ```
  - c. `int test[-10];`
  - d. `double sales[40.5];`

- 5. 大小为50的数组的索引有效范围是什么？

- 6. 编写 C++ 语句完成以下操作：
  - a. 声明一个包含15个 `int` 类型分量的数组 `alpha`。
  - b. 输出数组 `alpha` 第十个分量的值。
  - c. 将数组 `alpha` 第五个分量的值设置为35。
  - d. 将数组 `alpha` 第九个分量的值设置为数组 `alpha` 第六个和第十三个分量之和。
  - e. 将数组 `alpha` 第四个分量的值设置为第八个分量的值的三倍减去57。
  - f. 输出 `alpha`，使每行打印五个分量。

- 7. 以下程序段的输出是什么？

  ```cpp
  int temp[5];

  for (int i = 0; i < 5; i++)
      temp[i] = 2 * i - 3;

  for (int i = 0; i < 5; i++)
      cout << temp[i] << " ";
  cout << endl;

  temp[0] = temp[4];
  temp[4] = temp[1];
  temp[2] = temp[3] + temp[0];

  for (int i = 0; i < 5; i++)
      cout << temp[i] << " ";
  cout << endl;
  ```

- 8. 假设 `list` 是一个包含五个 `int` 类型分量的数组。以下 C++ 代码执行后，`list` 中存储的是什么？

  ```cpp
  for (int i = 0; i < 5; i++)
  {
      list[i] = 2 * i + 5;
      if (i % 2 == 0)
          list[i] = list[i] - 3;
  }
  ```

- 9. 假设 `list` 是一个包含六个 `int` 类型分量的数组。以下 C++ 代码执行后，`list` 中存储的是什么？

  ```cpp
  list[0] = 5;
  for (int i = 1; i < 6; i++)
  {
      list[i] = i * i + 5;
      if (i > 2)
          list[i] = 2 * list[i] - list[i - 1];
  }
  ```

- 10. 改正以下代码，使其正确初始化并输出数组的元素。

  ```cpp
  int myList[10];

  for (int i = 1; i <= 10; i++)
      cin >> myList;

  for (int i = 1; i <= 10; i++)
      cout << myList[i] << " ";
  cout << endl;
  ```

- 11. 什么是数组索引越界？C++ 会检查数组索引是否在边界内吗？

- 12. 假设 `scores` 是一个包含10个 `double` 类型分量的数组。

  `scores = {2.5, 3.9, 4.8, 6.2, 6.2, 7.4, 7.9, 8.5, 8.5, 9.9}`

  以下代码旨在确保 `scores` 的元素按非递减顺序排列。但是，代码中存在错误。找出并改正错误。

  ```cpp
  for (int i = 1; i <= 10; i++)
      if (scores[i] > scores[i + 1])
          cout << scores[i] << " and " << scores[i + 1]
               << " elements of scores are out of order." << endl;
  ```

- 13. 编写 C++ 语句定义并初始化以下数组。
  - a. 包含10个 `double` 类型分量的数组 `heights`。将此数组初始化为以下值：5.2、6.3、5.8、4.9、5.2、5.7、6.7、7.1、5.10、6.0。
  - b. 包含7个 `int` 类型分量的数组 `weights`。将此数组初始化为以下值：120、125、137、140、150、180、210。
  - c. `char` 类型的数组 `specialSymbols`。将此数组初始化为以下值：'$'、'#'、'%'、'@'、'&'、'!'、'^'。
  - d. 包含4个 `string` 类型分量的数组 `seasons`。将此数组初始化为以下值："fall"、"winter"、"spring"、"summer"。

- 14. 判断以下数组声明是否有效。
  - a. `int a[5] = {0, 4, 3, 2, 7};`
  - b. `int b[10] = {0, 7, 3, 12};`
  - c. `int c[7] = {12, 13, 14, 16, 8};`
  - d. `double lengths[] = {12.7, 13.9, 18.75, 20.78};`
  - e. `char name[8] = "Samantha";`

- 15. 假设你有以下声明：

  ```cpp
  int list[10] = {8, 9, 15, 12, 80};
  ```

  `list` 的每个分量中存储的是什么？

- 16. 以下代码的输出是什么？

  ```cpp
  int list[] = {6, 8, 2, 14, 13};

  for (int i = 0; i < 4; i++)
      list[i] = list[i] - list[i + 1];

  for (int i = 0; i < 5; i++)
      cout << i << " " << list[i] << endl;
  ```

- 17. 考虑以下函数头：

  ```cpp
  void tryMe(int x[], int size);
  ```

  以及以下声明：

  ```cpp
  int list[100];
  int score[50];
  double gpa[50];
  ```

  以下哪个函数调用有效？

  - a. `tryMe(list, 100);`
  - b. `tryMe(list, 75);`
  - c. `tryMe(score, 100);`
  - d. `tryMe(score, 49);`
  - e. `tryMe(gpa, 50);`

- 18. 假设你有以下函数定义。

  ```cpp
  void sum(int x, int y, int& z)
  {
      z = x + y;
  }
  ```

  考虑以下声明：

  ```cpp
  int list1[10], list2[10], list3[10];
  int a, b, c;
  ```
