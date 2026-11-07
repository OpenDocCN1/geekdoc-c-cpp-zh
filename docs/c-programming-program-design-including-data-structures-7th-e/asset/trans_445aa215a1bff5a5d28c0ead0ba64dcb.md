

- 16. 操纵符 `setprecision` 将浮点数的输出格式化为指定的小数位数。
- 17. 操纵符 `fixed` 以定点小数格式输出浮点数。
- 18. 操纵符 `showpoint` 输出浮点数时带有小数点和尾随零。
- 19. 操纵符 `setw` 将表达式的输出格式化为特定列数；默认输出为右对齐。
- 20. 如果 `setw` 参数中指定的列数少于打印表达式值所需的列数，则输出不会被截断，表达式的输出会扩展至所需列数。
- 21. 操纵符 `setfill` 用于用空格以外的字符填充输出设备上未使用的列。
- 22. 如果 `setw` 操纵符中指定的列数超过下一个表达式所需的列数，则输出为右对齐。要使输出左对齐，使用操纵符 `left`。
- 23. 要对标准 I/O 使用流函数 `get`、`ignore`、`putback`、`peek`、`clear` 和 `unsetf`，程序必须包含头文件 `iostream`。
- 24. 要使用操纵符 `setprecision`、`setw` 和 `setfill`，程序必须包含头文件 `iomanip`。
- 25. 头文件 `fstream` 包含 `ifstream` 和 `ofstream` 的定义。
- 26. 对于文件 I/O，必须使用语句 `#include <fstream>` 在程序中包含头文件 `fstream`。还必须执行以下操作：为文件输入声明 `ifstream` 类型的变量，为文件输出声明 `ofstream` 类型的变量，并使用 open 语句打开输入文件和输出文件。可以将 `<<`、`>>`、`get`、`ignore`、`peek`、`putback` 或 `clear` 与文件流变量一起使用。
- 27. 要关闭由 `fstream` 变量 `inFile` 表示的文件，使用语句 `inFile.close();`。要关闭由 `ofstream` 变量 `outFile` 表示的文件，使用语句 `outFile.close();`。

## 练习

练习末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断下列语句的正误。
  - a. 输入流是从计算机到输入设备的字符序列。(1)
  - b. 要在程序中使用 `cin` 和 `cout`，程序必须包含头文件 `iostream`。(1, 2)
  - c. 假设 `pay` 是 `double` 类型的变量。语句 `cin >> pay;` 要求输入一个小数。(2)
  - d. 语句 `cin >> length;` 和 `length >> cin;` 等价。(2)
  - e. 当语句 `cin >> num1 >> num2;` 执行时，在向变量 `num1` 输入一个数字后，程序会跳过所有尾随空白字符。(2)
  - f. 要在程序中使用预定义函数 `pow`，程序必须包含头文件 `cmath`。(3)
  - g. 语句 `cin.get(ch);` 将下一个字符输入到变量 `ch` 中。(4)
  - h. 当输入流进入失败状态时，程序会以错误消息终止。(5)
  - i. 要使用操纵符 `fixed` 和 `showpoint`，程序不需要包含头文件 `iomanip`。(6)
  - j. 语句 `cin >> right;` 只将下一个变量的输入设置为右对齐。(7)
  - k. 要从文件输入数据，程序必须包含头文件 `fstream`。(10)

- 2. 假设 `num1` 和 `num2` 是 `int` 变量，`symbol` 是 `char` 变量。考虑以下输入：(2)

  ```text
  47 18 * 28 $
  ```

  在下列各语句执行后，分别向 `num1`、`num2` 和 `symbol` 赋了什么值（如果有）？（每个语句使用相同的输入。）

  - a. `cin >> num1 >> symbol >> num2;`
  - b. `cin >> symbol >> num1 >> num2;`
  - c.
    ```cpp
    cin >> num1;
    cin.get(symbol);
    cin >> num2;
    ```
  - d.
    ```cpp
    cin >> num1 >> num2;
    cin.get(symbol);
    ```
  - e.
    ```cpp
    cin.get(symbol);
    cin >> num1 >> num2;
    ```

- 3. 假设 `num1` 和 `num2` 是 `int` 变量，`x` 和 `y` 是 `double` 变量。假设输入数据如下：(2)

  ```text
  35 28.30 67 12.50
  ```

  在下列各语句执行后，分别向 `num1`、`num2`、`x`、`y` 赋了什么值（如果有）？（每个语句使用相同的输入。）

  - a. `cin >> x >> num1 >> y >> num2;`
  - b. `cin >> num1 >> x >> num2 >> y;`

  ![](img/d0be7fc6d804b63484835c6c8bc67a07_225_0.png)

  - c. `cin >> x >> y >> num1 >> num2;`
  - d. `cin >> num1 >> num2 >> x >> y;`
  - e. `cin >> num1 >> x >> y >> num2;`
  - f. `cin >> x >> num1 >> num2 >> y;`

- 4. 假设 `x` 和 `y` 是 `int` 变量，`symbol` 是 `char` 变量。假设输入数据如下：

  ```text
  38 26 * 67 33
  24 $ 55 # 34
  # & 63 85
  ```

  在下列各语句执行后，分别向 `x`、`y` 和 `symbol` 赋了什么值（如果有）？（每个语句使用相同的输入。）(2, 3, 4)

  - a.
    ```cpp
    cin >> x >> y;
    cin.ignore(100, '\n');
    cin >> symbol;
    ```
  - b.
    ```cpp
    cin >> x;
    cin.ignore(100, '*');
    cin >> y;
    cin.get(symbol);
    ```
  - c.
    ```cpp
    cin >> y;
    cin.ignore(100, '\n');
    cin >> x >> symbol;
    ```
  - d.
    ```cpp
    cin.get(symbol);
    cin.ignore(100, '*');
    cin >> x;
    cin.ignore(100, '\n');
    cin >> y;
    ```
  - e.
    ```cpp
    cin.ignore(100, '\n');
    cin >> x >> symbol;
    cin.ignore(100, '\n');
    cin.ignore(100, '&');
    cin >> y;
    ```

- 5. 给定输入：

  ```text
  12.8 Bill 15
  ```

  以及变量声明：(2, 8)

  ```cpp
  double x = 3.5;
  int y = 18;
  string name = "Lisa";
  ```

  输出是什么（如果有）？每个部分使用相同的输入。

  - a.
    ```cpp
    cin >> x >> name >> y;
    cout << x << " " << y << " " << name << endl;
    ```
  - b.
    ```cpp
    cin >> y >> x >> name;
    cout << x << " " << y << " " << name << endl;
    ```
  - c.
    ```cpp
    cin >> x >> y >> name;
    cout << x << " " << y << " " << name << endl;
    ```

- 6. 假设 `x` 和 `y` 是 `int` 变量，`z` 是 `double` 变量，`ch` 是 `char` 变量。假设输入语句为：

  ```cpp
  cin >> x >> y >> ch >> z;
  ```

  如果输入为以下内容，则 `x`、`y`、`z` 和 `ch` 中分别存储了什么值（如果有）？(2)

  - a. `35 62.78`
  - b. `86 32A 92.6`
  - c. `12 .45A 32`

- 7. 要使用函数 `pow`，必须包含哪个头文件？(3)
- 8. 要使用函数 `sqrt`，必须包含哪个头文件？(3)
- 9. 要使用函数 `setprecision`，必须包含哪个头文件？(7)
- 10. 要使用操纵符 `fixed` 和 `showpoint`，必须包含哪个头文件？(7)
- 11. 要使用函数 `setw`，必须包含哪个头文件？(7)

- 12. 下列程序的输出是什么？(2, 3, 6, 8)

  ```cpp
  #include <iostream>
  #include <cmath>
  #include <string>
  #include <iomanip>

  using namespace std;

  int main()
  {
      double first, second;
      int temp;
      string message;

      first = 2.5;
      second = 4.0;

      cout << fixed << showpoint << setprecision(2);

      cout << (pow(first, second)) << endl;
      cout << (pow(second, first)) << endl;

      temp = static_cast<int>(pow(second, 1.5));

      cout << temp << endl;

      cout << sqrt(56.25) << endl;

      cout << static_cast<int>(sqrt(pow(first, temp))) << endl;

      message = "Predefined functions simplify programming code!";

      cout << "Length of message = "
           << message.length() << endl;

      return 0;
  }
  ```

- 13. 要在程序中使用函数 `peek` 和 `putback`，程序中必须包含哪个（些）头文件？(4)

- 14. 假设 `num` 是 `int` 变量，`discard` 是 `char` 变量。假设输入数据如下：

  ```text
  #34
  ```

  在下列各语句执行后，分别向 `num` 和 `discard` 赋了什么值（如果有）？（每个语句使用相同的输入。）(2, 4)

  - a.
    ```cpp
    cin.get(discard);
    cin >> num;
    ```
  - b.
    ```cpp
    discard = cin.peek();
    cin >> num;
    ```
  - c.
    ```cpp
    cin.get(discard);
    cin.putback(discard);
    cin >> discard;
    cin >> num;
    ```

- 15. 假设 `name` 是 `string` 类型的变量。下列语句的作用是什么？(8)

  ```cpp
  getline(cin, name);
  ```

- 16. 编写一条 C++ 语句，使用操纵符 `setfill` 输出一行包含 35 个星号的内容，如下行所示：(7)

  ```text
  ***********************************
  ```

- 17. 假设 `age` 是 `int` 变量，`name` 是 `string` 变量。在下列输入语句执行后，`age` 和 `name` 的值是什么？(8)

  ```cpp
  cin >> age;
  getline(cin, name);
  ```

  如果输入为：

  - a. `23 Lance Grant`
  - b.
    ```text
    23
    Lance Grant
    ```

