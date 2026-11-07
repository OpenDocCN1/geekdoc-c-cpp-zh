

- 13. 双向选择采用以下形式：

  ```cpp
  if (expression)
      statement1
  else
      statement2
  ```

  如果 expression 为真，则执行 statement1；否则执行 statement2。

- 14. `if` 或 `if...else` 结构中的表达式通常是逻辑表达式。

- 15. 在单向选择中，在语句前包含分号会产生语义错误。在这种情况下，`if` 语句的动作为空。

- 16. 在双向选择中，在 statement1 前包含分号会产生语法错误。

- 17. C++ 中没有独立的 `else` 语句。每个 `else` 都有一个相关的 `if`。

- 18. `else` 与最近一个尚未与任何其他 `else` 配对的 `if` 配对。

- 19. 用花括号 `{` 和 `}` 括起来的一系列语句称为复合语句或语句块。复合语句被当作单条语句处理。

- 20. 可以在 `if` 语句中使用输入流变量来确定输入流的状态。

- 21. 使用赋值运算符代替相等运算符会产生语义错误。这可能导致程序中出现严重错误。

- 22. `switch` 结构用于处理多路选择。

- 23. 在 `switch` 语句中执行 `break` 语句会立即退出 `switch` 结构。

- 24. 如果程序中某些条件未满足，可以使用 `assert` 函数终止程序。

## 练习

- 1. 将以下语句标记为真或假。

  - a. 逻辑表达式的结果不能赋给 `int` 变量。

  - b. 在单向选择中，如果在 `if` 语句中的表达式之后放置分号，则 `if` 语句中的表达式始终为真。

  - c. 每个 `if` 语句都必须有对应的 `else`。

  - d. `if` 语句中的表达式：

    ```cpp
    if (score = 30)
        grade = 'A';
    ```

    始终求值为真。

  - e. 表达式：

    `(ch >= 'A' && ch <= 'Z')`

    只要 `ch < 'A'` 或 `ch >= 'Z'` 之一成立，就求值为 **假**。

  - f. 假设输入为 5。以下代码的输出：

    ```cpp
    cin >> num;
    if (num > 5)
        cout << num;
        num = 0;
    else
        cout << "Num is zero" << endl;
    ```

    为：Num is zero

  - g. `switch` 语句中的表达式应求值为简单数据类型的值。

  - h. 表达式 `!(x > 0)` 仅当 x 为负数时为 **真**。

  - i. 在 C++ 中，`!` 和 `!=` 都是逻辑运算符。

  - j. 程序中语句执行的顺序称为控制流。

- 2. 选择最佳答案。

  - a.

    ```cpp
    if (60 <= 12 * 5)
        cout << "Hello";
        cout << " There";
    ```

    输出以下内容：

    (i) Hello There　(ii) Hello　(iii) Hello There　(iv) There

  - b.

    ```cpp
    if ('a' > 'b' || 66 > static_cast<int>('A'))
        cout << "#*#" << endl;
    ```

    输出以下内容：

    (i) `#*#`　(ii)

    ```
    #
    *
    #
    ```

    (iii) `*`　(iv) 以上都不是

  - c.

    ```cpp
    if (7 <= 7)
        cout << 6 - 9 * 2 / 6 << endl;
    ```

    输出以下内容：

    (i) -1　(ii) 3　(iii) 3.0　(iv) 以上都不是

  - d.

    ```cpp
    if (7 < 8)
    {
        cout << "2 4 6 8" << endl;
        cout << "1 3 5 7" << endl;
    }
    ```

    输出以下内容：

    (i)

    ```
    2 4 6 8
    1 3 5 7
    ```

    (ii)

    ```
    1 3 5 7
    ```

    (iii) 以上都不是

  - e.

    ```cpp
    if (5 < 3)
        cout << "*";
    else if (7 == 8)
        cout << "&";
    else
        cout << "$";
    ```

    输出以下内容：

    (i) *　(ii) &　(iii) $　(iv) 以上都不是

- 3. 假设 x、y 和 z 是 int 变量，且 x = 10、y = 15、z = 20。判断以下表达式的求值结果为真还是假。

  - a. `!(x > 10)`
  - b. `x <= 5 || y < 15`
  - c. `(x != 5) && (y != z)`
  - d. `x >= z || (x + y >= z)`
  - e. `(x <= y - 2) && (y >= z) || (z - 2 != 20)`

- 4. 假设 str1、str2 和 str3 是 string 变量，且 str1 = "English"，str2 = "Computer Science"，str3 = "Programming"。求以下表达式的值。

  - a. `str1 >= str2`
  - b. `str1 != "english"`
  - c. `str3 < str2`
  - d. `str2 >= "Chemistry"`

- 5. 假设 x、y、z 和 w 是 int 变量，且 x = 3、y = 4、z = 7、w = 1。以下语句的输出是什么？

  - a. `cout << "x == y: " << (x == y) << endl;`
  - b. `cout << "x != z: " << (x != z) << endl;`
  - c. `cout << "y == z - 3: " << (y == z - 3) << endl;`
  - d. `cout << "!(z > w): " << (!(z > w)) << endl;`
  - e. `cout << "x + y < z: " << (x + y < z) << endl;`

- 6. 以下 C++ 代码的输出是什么？

  ```cpp
  x = 100;
  y = 200;
  if (x > 100 && y <= 200)
      cout << x << " " << y << " " << x + y << endl;
  else
      cout << x << " " << y << " " << 2 * x - y << endl;
  ```

- 7. 改正以下代码，使其打印正确的消息。

  ```cpp
  if (score >= 60)
      cout << "You pass." << endl;
  else;
      cout << "You fail." << endl;
  ```

- 8. 编写 C++ 语句：如果 gender 为 'M'，输出 Male；如果 gender 为 'F'，输出 Female；否则输出 invalid gender。

- 9. 以下程序的输出是什么？

  ```cpp
  #include <iostream>

  using namespace std;

  int main()
  {
      int myNum = 10;
      int yourNum = 30;

      if (yourNum % myNum == 3)
      {
          yourNum = 3;
          myNum = 1;
      }
      else if (yourNum % myNum == 2)
      {
          yourNum = 2;
          myNum = 2;
      }
      else
      {
          yourNum = 1;
          myNum = 3;
      }

      cout << myNum << " " << yourNum << endl;

      return 0;
  }
  ```

- 10. a. 如果 myNum = 5 且 yourNum = 12，练习 9 中程序的输出是什么？
- 10. b. 如果 myNum = 30 且 yourNum = 33，练习 9 中程序的输出是什么？

- 11. 假设 sale 和 bonus 是 double 变量。编写一个 if...else 语句，按如下方式给 bonus 赋值：如果 sale 大于 $20,000，则赋给 bonus 的值为 0.10；如果 sale 大于 $10,000 且小于或等于 $20,000，则赋给 bonus 的值为 0.05；否则，赋给 bonus 的值为 0。

- 12. 假设 overSpeed 和 fine 是 double 变量。按如下方式给 fine 赋值：如果 0 < overSpeed <= 5，则赋给 fine 的值为 $20.00；如果 5 < overSpeed <= 10，则赋给 fine 的值为 $75.00；如果 10 < overSpeed <= 15，则赋给 fine 的值为 $150.00；如果 overSpeed > 15，则赋给 fine 的值为 $150.00 加上超过 15 的每英里 $20.00。

- 13. 假设 score 是 int 变量。考虑以下 if 语句：

  ```cpp
  if (score >= 90)
      cout << "Discount = 10%" << endl;
  ```

  - a. 如果 score 的值为 95，输出是什么？说明理由。
  - b. 如果 score 的值为 85，输出是什么？说明理由。

- 14. 假设 score 是 int 变量。考虑以下 if 语句：

  - i.

    ```cpp
    if (score == 70)
        cout << "Grade is C." << endl;
    ```

  - ii.

    ```cpp
    if (score < 70)
        cout << "Grade is C." << endl;
    ```

  回答以下问题：

  - a. 如果 score 的值为 70，(i) 和 (ii) 中的输出是什么？if 语句执行后 score 的值是什么？
  - b. 如果 score 的值为 80，(i) 和 (ii) 中的输出是什么？if 语句执行后 score 的值是什么？

- 15. 使用条件运算符重写以下表达式。（假设所有变量均已正确声明。）

  - a.

    ```cpp
    if (x >= y)
        z = x - y;
    else
        z = y - x;
    ```

  - b.

    ```cpp
    if (hours >= 40.0)
        wages = 40 * 7.50 + 1.5 * 7.5 * (hours - 40);
    else
        wages = hours * 7.50;
    ```

  - c.

    ```cpp
    if (score >= 60)
        str = "Pass";
    else
        str = "Fail";
    ```

- 16. 使用 if...else 语句重写以下表达式。（假设所有变量均已正确声明。）

