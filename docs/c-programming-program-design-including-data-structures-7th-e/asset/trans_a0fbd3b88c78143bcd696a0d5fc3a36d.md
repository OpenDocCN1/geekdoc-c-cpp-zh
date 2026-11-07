
- d. 给定声明：

  ```cpp
  int list[10];
  ```

  语句：

  ```cpp
  list[5] = list[3] + list[2];
  ```

  会更新数组 list 第五个分量的内容。(2)

- e. 如果数组下标越界，程序总是会因错误而终止。(3)

- f. 对于 `int` 数组，唯一允许的聚合操作是递增和递减操作。(5)

- g. 数组既可以按值也可以按引用作为参数传递给函数。(6)

- h. 函数可以返回数组类型的值。(6)

- i. 在 C++ 中，字符串允许某些聚合操作。(11, 12, 13)

- j. 声明：

  ```cpp
  char name[16] = "John K. Miller";
  ```

  将 name 声明为包含 15 个字符的数组，因为字符串 "John K. Miller" 只有 14 个字符。(11)

- k. 声明：

  ```cpp
  char str = "Sunny Day";
  ```

  将 str 声明为长度未指定的字符串。(11)

- l. 作为参数时，二维数组既可以按值传递，也可以按引用传递。(15, 16)

### 2. 考虑以下声明：(1, 2)

```cpp
int accountNum[75];
```

在该声明中，指出以下各项：

- a. 数组名。
- b. 数组大小。
- c. 每个数组分量的数据类型。
- d. 数组下标的取值范围。
- e. 第一个元素的下标。
- f. 最后一个元素的下标。

### 3. 指出以下数组声明中的错误（如果有）。如果语句不正确，请提供正确的语句。(1, 2)

- a. `int primeNum[99];`
- b. `int testScores[0];`
- c. `string names[60];`
- d. `int list100[0..99];`
- e. `double[50] gpa;`
- f.

  ```cpp
  const double LENGTH = 26;
  double list[LENGTH - 1];
  ```

- g.

  ```cpp
  const long SIZE = 100;
  int list[2 * SIZE];
  ```

### 4. 判断以下数组声明是否有效。如果声明无效，请解释原因。(1, 2)

- a. `string customers[];`
- b. `int numArray[50];`
- c.

  ```cpp
  const int SIZE = 30;
  double list[20 - SIZE];
  ```

- d.

  ```cpp
  int length = 50;
  double list[length - 50];
  ```

- e. `int ids[-30];`
- f. `colors[30] string;`

### 5. 大小为 99 的数组，其下标的有效范围是什么？第一个元素的下标是什么？最后一个元素的下标是什么？(1, 3)

### 6. 编写 C++ 语句完成以下操作：(1, 2)

- a. 声明一个包含 50 个 `int` 类型分量的数组 `alpha`。
- b. 将 `alpha` 的每个分量初始化为 −1。
- c. 输出数组 `alpha` 第一个分量的值。
- d. 将数组 `alpha` 第二十五个分量的值设为 62。
- e. 将 `alpha` 第十个分量的值设为 `alpha` 第五十个分量的值的三倍加 10。
- f. 使用 `for` 循环输出 `alpha` 中下标为 2 或 3 的倍数的分量的值。
- g. 输出 `alpha` 最后一个分量的值。
- h. 输出 `alpha` 的值，使每行打印 15 个分量。
- i. 使用 `for` 循环对每隔一个元素（偶数下标元素）进行递增。
- j. 使用 `for` 循环创建新数组 `diffAlpha`，其元素为 `alpha` 中相邻元素的差值。

### 7. 以下程序段的输出是什么？(2)

```cpp
int temp[5];

for (int i = 0; i < 5; i++)
    temp[i] = static_cast<int>(pow(i, 2.0));

for (int i = 0; i < 5; i++)
    cout << temp[i] << " ";
cout << endl;

temp[4] = temp[3] * temp[2];
temp[3] = temp[4] - temp[2];
temp[0] = temp[5] - temp[1];

for (int i = 0; i < 5; i++)
    cout << temp[i] << " ";
cout << endl;
```

### 8. 以下 C++ 代码执行后，list 中存储的是什么？(2)

```cpp
int list[10];

for (int i = 0; i < 5; i++)
{
    list[i] = i * (i - 1);
    if (i % 2 == 0)
        list[i] = list[i] + i;
    else if (i % 3 == 0)
        list[i] = list[i] - i;
    else if (i > 0)
        list[i] = list[i] - list[i - 1];
}
```

### 9. 以下 C++ 代码执行后，list 中存储的是什么？(2)

```cpp
int list[8];

list[0] = 1;
list[1] = 2;
for (int i = 2; i < 8; i++)
{
    list[i] = list[i - 1] * list[i - 2];
    if (i > 5)
        list[i] = list[i] - list[i - 1];
}
```

### 10. 以下 C++ 代码执行后，myList 中存储的是什么？(2)

```cpp
double myList[6];

myList[0] = 2.5;

for (int i = 1; i < 6; i++)
{
    myList[i] = i * myList[i - 1];
    if (i > 3)
        myList[i] = myList[i] / 2;
}
```

### 11. 改正以下代码，使其正确地将 myList 的每个元素的值设置为其下标。(2, 3)

```cpp
int myList[10];

for (int i = 1; i > 10; i++)
    myList[i] = i;
```

### 12. 改正以下代码，使其正确初始化并输出数组 `myList` 的元素。(2, 3)

```cpp
int myList[10];

for (int i = 1; i <= 10; i++)
    cin >> myList;

for (int i = 1; i <= 10; i++)
    cout << myList[i] << " ";
cout << endl;
```

### 13. 什么是数组下标越界？C++ 会检查数组下标是否在边界内吗？(3)

### 14. 假设 `scores` 是一个包含 10 个 `double` 类型分量的数组，并且：

`scores = {2.5, 3.9, 4.8, 6.2, 6.2, 7.4, 7.9, 8.5, 8.5, 9.9}`

以下代码本应测试 scores 的元素是否按非递减顺序排列。但是，代码中存在错误。找出并改正这些错误。(1, 2, 3)

```cpp
for (int i = 1; i <= 10; i++)
    if (scores[i] >= scores[i + 1])
        cout << " " << i << " and " << (i + 1)
             << " elements of scores are out of order." << endl;
```

### 15. 编写 C++ 语句来定义并初始化以下数组。(4)

- a. 包含 10 个 `double` 类型分量的数组 `heights`。将此数组初始化为以下值：5.2、6.3、5.8、4.9、5.2、5.7、6.7、7.1、5.10、6.0。
- b. 包含 7 个 `int` 类型分量的数组 `weights`。将此数组初始化为以下值：120、125、137、140、150、180、210。
- c. `char` 类型的数组 `specialSymbols`。将此数组初始化为以下值：'$'、'#'、'%'、'@'、'&'、'!'、'^'。
- d. 包含 4 个 `string` 类型分量的数组 `seasons`。将此数组初始化为以下值："fall"、"winter"、"spring"、"summer"。

### 16. 判断以下数组声明是否有效。如果声明有效，请确定数组的大小。(4)

- a. `int list[] = {18, 13, 14, 16};`
- b. `int x[10] = {1, 7, 5, 3, 2, 8};`
- c. `double y[4] = {2.0, 5.0, 8.0, 11.0, 14.0};`
- d. `double lengths[] = {8.2, 3.9, 6.4, 5.7, 7.3};`
- e. `int list[7] = {12, 13, , 14, 16, , 8};`
- f. `string names[8] = {"John", "Lisa", "Chris", "Katie"};`

### 17. 假设你有以下声明：

```cpp
int list[8] = {6, 10, 14, 18, 22};
```

如果该声明有效，list 的八个分量中分别存储了什么？(4)

### 18. 考虑以下声明：(2)

```cpp
int list[] = {3, 8, 10, 13, 6, 11};
```

- a. 编写 C++ 代码，输出 list 的每个分量中存储的值。
- b. 编写 C++ 代码，按如下方式设置 list 前五个分量的值：第 i 个分量的值等于第 i 个分量的值减去第 (i+1) 个分量的值的三倍。

### 19. 以下 C++ 代码的输出是什么？(2)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int beta[7] = {3, 5};

    for (int i = 2; i < 7; i++)
    {
        beta[i] = 3 * i + 2;
        beta[i - 1] = beta[i - 1] + beta[i];
        beta[i - 2] = beta[i - 2] + beta[i - 1];
    }

    for (int i = 0; i < 7; i++)
        cout << beta[i] << " ";
    cout << endl;

    return 0;
}
```

### 20. 以下 C++ 代码的输出是什么？(2)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int list1[5];
    int list2[15];

    for (int i = 0; i < 5; i++)
        list1[i] = i * i - 2;

    cout << "list1: ";
    for (int i = 0; i < 5; i++)
        cout << list1[i] << " ";
    cout << endl;
```
