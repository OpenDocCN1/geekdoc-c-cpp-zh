

- a. 首先，你设计一个算法来计算平均测试分数。要计算平均测试分数，首先需要统计班级中的学生人数，并将每个学生的测试分数相加。然后，将总和除以人数即可得到平均测试分数。计算平均测试分数的算法如下：
  - i. 将sum和count设置为0。
  - ii. 对班上的每个学生重复以下步骤。
    - 1. 获取testScore。
    - 2. 递增count，并将当前测试分数加到sum上以更新sum的值。
  - iii. 使用以下公式计算平均测试分数。

    ```text
    if (count is 0)
        averageTestScore = 0;
    otherwise
        averageTestScore = sum / count;
    ```

- b. 以下算法确定并打印所有测试分数低于平均测试分数的学生的姓名。

  对班上的每个学生重复以下步骤。

  - i. 获取studentName和testScore。
  - ii. 如果（testScore小于averageTestScore）  
    打印studentName

- c. 以下算法确定最高测试分数。

  - i. 获取第一个学生的测试分数并将其命名为highestTestScore。
  - ii. 对班上其余每个学生重复以下步骤
    - 1. 获取testScore
    - 2. 如果（testScore大于highestTestScore）  
      highestTestScore = testScore;

- d. 要打印所有测试分数与最高测试分数相同的学生的姓名，请将每个学生的测试分数与最高测试分数进行比较，如果相等，则打印该姓名。以下算法实现了这一点。对班上的每个学生重复以下步骤。

  - i. 获取studentName和testScore。
  - ii. 如果（testScore等于highestTestScore）  
    打印studentName

可以使用从a到d部分获得的子问题的解决方案来设计主算法，如下所示：

- 1. 使用a部分的算法计算平均测试分数。
- 2. 使用b部分的算法打印所有分数低于平均测试分数的学生的姓名。
- 3. 使用c部分的算法找到最高测试分数。
- 4. 使用d部分的算法打印所有测试分数与最高测试分数相同的学生的姓名。

## 第2章

- 1. a. 假；b. 假；c. 假；d. 真；e. 真；f. 假；g. 真；h. 真；i. 假；j. 真；k. 假
- 3. b、d、e
- 5. 标识符`firstName`和`FirstName`不相同。C++区分大小写。`firstName`的第一个字母是小写f，而`FirstName`的第一个字符是大写F。因此这些标识符是不同的。
- 7.
  - a. 3
  - b. 不可能。运算符`%`的两个操作数都必须是整数。因为第二个操作数`w`是浮点值，所以该表达式无效。
  - c. 不可能。运算符`%`的两个操作数都必须是整数。因为第一个操作数`y + w`是浮点值，所以该表达式无效。
  - d. 38.5
  - e. 1
  - f. 2
  - g. 2
  - h. 420.0
- 9. 7
- 11. a和c是有效的。
- 13.
  - a. `32 * a + b`
  - b. `'8'`
  - c. `"Julie Nelson"`
  - d. `(b * b - 4 * a * c) / (2 * a)`
  - e. `(a + b) / (e * e - f) - g * h`
  - f. `(-b + (b * b - 4 * a * c)) / (2 * a)`
- 15.
  - `x = 20`
  - `y = 15`
  - `z = 6`
  - `w = 11.5`
  - `t = 4.5`
- 17. a. 0.50；b. 24.50；c. 37.6；d. 8.3；e. 10；f. 38.75
- 19. a和c是正确的。
- 21.
  - a.

    ```cpp
    int num1;
    int num2;
    ```

  - b. `cout << "Enter two numbers separated by spaces." << endl;`
  - c. `cin >> num1 >> num2;`
  - d. `cout << "num1 = " << num1 << " num2 = " << num2 << endl;`  
       `cout << "2 * num1 - num2 = " << 2 * num1 - num2 << endl;`

- 23. 正确答案是：

  ```cpp
  #include <iostream>

  using namespace std;

  const char STAR = '*';
  const int PRIME = 71;

  int main()
  {
      int count, sum;
      double x;

      int newNum;    //declare newNum

      count = 1;
      sum = count + PRIME;
      x = 25.67;     // x = 25.67;
      newNum = count * 1 + 2;    //newNum = count * ONE + 2;
      sum = sum + count;         //sum + count = sum;
      x = x + sum * count;       // x = x + sum * COUNT;
      cout << " count = " << count << ", sum = " << sum
           << ", PRIME = " << PRIME << endl;
      return 0;
  }
  ```

- 25. 标识符必须先声明才能使用。
  - a. `x *= 2;`
  - b. `x += y - 2;`
  - c. `sum += num;`
  - d. `z *= x + 2;`
  - e. `y /= x + 5;`

```cpp
a = (b++) + 3;
c = 2 * a++ + (++b);
b = 2 * (++c) - (a++);
```

| a | b | c |
|---:|---:|---:|
| 9 | 7 | 未定义 |
| 9 | 8 | 26 |
| 10 | 45 | 27 |

- 31. （用户输入以阴影显示。）

  ```text
  a = 25
  Enter two integers: 20 15

  The numbers you entered are 20 and 15
  z = 45.5
  Your grade is A
  The value of a = 65
  ```

  ```cpp
  #include <iostream>
  #include <string>

  using namespace std;

  const double X = 13.45;
  const int Y = 34;
  const char BLANK = ' ';

  int main()
  {
      string firstName, lastName;
      int num;
      double salary;

      cout << "Enter first name: ";
      cin >> firstName;
      cout << endl;

      cout << "Enter last name: ";
      cin >> lastName;
      cout << endl;

      cout << "Enter a positive integer less than 70: ";
      cin >> num;
      cout << endl;

      salary = num * X;

      cout << "Name: " << firstName << BLANK << lastName << endl;
      cout << "Wages: $" << salary << endl;
      cout << "X = " << X << endl;
      cout << "X + Y = " << X + Y << endl;

      return 0;
  }
  ```

## 第3章

- 1. a. 真；b. 真；c. 假；d. 假；e. 真；f. 真
- 3.
  - a. x = 37, y = 86, z = 0.56
  - b. x = 37, y = 32, z = 86.56
  - c. 输入失败：z = 37.0, x = 86，试图将.（句点）读入y。
- 5. 输入失败：试图将A读入y，而y是一个int变量。x = 46，y = 18，z = 'A'。y和z的值不变。
- 7. iomanip
- 9. getline(cin, name);
- 11.
  - a. name = "Lance Grant", age = 23
  - b. name = " ", age = 23
- 13.

  ```cpp
  #include <iostream>
  #include <fstream>

  using namespace std;

  int main()
  {
      int num1, num2;
      ifstream infile;
      ofstream outfile;

      infile.open("input.dat");
      outfile.open("output.dat");

      infile >> num1 >> num2;
      outfile << "Sum = " << num1 + num2 << endl;

      infile.close();
      outfile.close();

      return 0;
  }
  ```

- 15. `fstream`
- 17.
  - a. 与之前相同。
  - b. 该文件包含程序产生的输出。
  - c. 该文件包含程序产生的输出。旧内容被删除。
  - d. 程序将准备文件并将输出存储在文件中。
- 19.
  - a. `outfile.open("travel.dat");`
  - b. `outfile << fixed << showpoint << setprecision(2);`
  - c. `outfile << day << " " << distance << " " << speed << endl;`
  - d. `travelTime = distance / speed;`  
       `outfile << travelTime;`
  - e. `fstream`和`iomanip`。

## 第4章

- 1. a. 假；b. 假；c. 假；d. 真；e. 假；f. 假；g. 假；h. 假；i. 假；j. 真
- 3. a. 真；b. 假；c. 真；d. 真；e. 假
- 5.
  - a. `x == y: 0`
  - b. `x != z: 1`
  - c. `y == z - 3: 1`
  - d. `!(z > w): 0`
  - e. `x + y < z: 0`
- 7. 省略else后面的分号。正确的语句是：

  ```cpp
  if (score >= 60)
      cout << "You pass." << endl;
  else
      cout << "You fail." << endl;
  ```

- 9. `3 1`
- 11.

  ```cpp
  if (sale > 20000)
      bonus = 0.10;
  else if (sale > 10000 && sale <= 20000)
      bonus = 0.05;
  else
      bonus = 0.0;
  ```

- 13.
  - a. 输出为：`Discount = 10%`。`if`语句末尾的分号终止了`if`语句。因此`cout`语句不是`if`语句的一部分。无论`if`语句中的表达式求值为`true`还是`false`，`cout`语句都会执行。
  - b. 输出为：`Discount = 10%`。`if`语句末尾的分号终止了`if`语句。因此`cout`语句不是`if`语句的一部分。无论`if`语句中的表达式求值为`true`还是`false`，`cout`语句都会执行。
- 15.
  - a. `(x >= y) ? z = x - y : z = y - x;`
  - b. `(hours >= 40.0) ? wages = 40 * 7.50 + 1.5 * 7.5 * (hours - 40) : wages = hours * 7.50;`
  - c. `(score >= 60) ? str = "Pass" : str = "Fail";`
- 17.
  - a. 40.00
  - b. 40.00
  - c. 55.00
- 19. 15
- 21. 96

```cpp
#include <iostream>

using namespace std;
const int SECRET = 5;

int main()
{
    int x, y, w, z;

    z = 9;

    if (z > 10)
    {
        x = 12;
        y = 5;
        w = x + y + SECRET;
    }
    else
    {
        x = 12;
        y = 4;
        w = x + y + SECRET;
    }

    cout << "w = " << w << endl;

    return 0;
}
```

