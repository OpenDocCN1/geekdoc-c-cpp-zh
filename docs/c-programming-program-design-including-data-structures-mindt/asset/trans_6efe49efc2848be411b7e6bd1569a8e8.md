

## 第 3 章

- **1.** a. 正确；b. 正确；c. 错误；d. 错误；e. 错误；f. 正确；g. 错误；h. 错误；i. 正确；j. 错误；k. 正确

- **3.**
  - a. `int1 = 67, int2 = 48, dec1 = 56.5, dec2 = 62.72`
  - b. `int1 = 48, int2 = -1, dec1 = 0.5, dec2 = 67`
  - c. `int1 = 48, int2 = 62, dec1 = 56.5, dec2 = 67`
  - d. `int1 = 56, int2 = 67, dec1 = 0.5, dec2 = 48`
  - e. 输入失败：`int1 = 56`；尝试将 `.`（句点）读入 `int2`。

- **5.**
  - a. `Samantha 168.5 46`
  - b. `Samantha 0.5 168`
  - c. `** 2.7 45`

  输入失败：尝试将 `s` 读入 `dec`，而 `dec` 是一个 `double` 类型的变量。`dec`、`num` 和 `str` 的值均未改变。

- **7.** 函数 `pow` 在程序中用于计算 x^y。也就是说，`pow(x, y) = x^y`。要使用此函数，程序必须包含头文件 `cmath`。

- **9.** 操作符 `scientific` 用于以科学计数法格式输出浮点数。要使用此函数，程序必须包含头文件 `iomanip`。

- **11.** 操作符 `setw` 用于在指定的列数中输出表达式的值。要使用此函数，程序必须包含头文件 `iomanip`。

- **13.** `iostream`

- **15.** 函数 `getline` 会一直读取，直到到达当前行的末尾。换行符也会被读取，但不会存储在 `string` 变量中。

- **17.**
  - a. `name = " Christy Miller", height = 5.4`
  - b. `name = " ", height = 5.4`

- **19.**

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

- **21.** `fstream`

- **23.**
  - a. 与之前相同。
  - b. 文件包含程序生成的输出。
  - c. 文件包含程序生成的输出。原有内容会被擦除。
  - d. 程序会准备文件并将输出存储到文件中。

- **25.**
  - a. `outfile.open("sales.dat");`
  - b. `outfile << fixed << showpoint << setprecision(2);`
  - c. `revenue = numOfJuiceBottlesSold * costOfaJuiceBottle;`
  - d. `outfile << numOfJuiceBottlesSold << " " << costOfaJuiceBottle << " " << revenue << endl;`
  - e. `outfile.close();`

## 第 4 章

- **1.** a. 错误；b. 错误；c. 错误；d. 错误；e. 正确；f. 错误；g. 错误；h. 错误；i. 错误；j. 错误；k. 错误

- **3.** a. 错误；b. 正确；c. 正确；d. 正确

- **5.**
  - a. `x == z: 0`
  - b. `y != z - 9: 0`
  - c. `x - y == z + 10: 1`
  - d. `!(z < w): 1`
  - e. `w - y < x - 2 * z: 0`

- **7.**
  - a. `++x`
  - b. `12 / 2 != 4 + 1`
  - c. `*`
  - d. **C++**
  - e. **低**  
    **高**

- **9.**
  - a. `%!!`
  - b. `a b c d`  
    `##`
  - c. `Flying Coding`

- **11.** don 的值为：0

- **13.** 删除 `else` 后面的分号。正确的语句为：

    ```cpp
    if (score >= 60)
        cout << "Pass" << endl;
    else
        cout << "Fail" << endl;
    ```

- **15.** 正确的代码为：

    ```cpp
    if (numOfItemsBought > 10)
        shippingCharges = 0.0;
    else if (5 <= numOfItemsBought && numOfItemsBought <= 10)
        shippingCharges = 3.00 * numOfItemsBought;
    else if (0 < numOfItemsBought && numOfItemsBought < 5)
        shippingCharges = 7.00 * numOfItemsBought;
    ```

- **17.** `20 10`

- **19.**

    ```cpp
    if (sale > 20000)
        bonus = 0.10;
    else if (sale > 10000 && sale <= 20000)
        bonus = 0.05;
    else
        bonus = 0.0;
    ```

- **21.**
  - a. 输出为：**折扣 = 10%**。`if` 语句末尾的分号终止了 `if` 语句。因此，`cout` 语句不属于 `if` 语句的一部分。无论 `if` 语句中的表达式计算结果为 `true` 还是 `false`，`cout` 语句都会执行。
  - b. 输出为：**折扣 = 10%**。`if` 语句末尾的分号终止了 `if` 语句。因此，`cout` 语句不属于 `if` 语句的一部分。无论 `if` 语句中的表达式计算结果为 `true` 还是 `false`，`cout` 语句都会执行。

- **23.**
  - a. `(x == y) ? z = x + y : z = (x + y) / 2;`
  - b.

    ```cpp
    (hours >= 40.0) ? wages = 40 * 7.50 + 1.5 * 7.5 *
                             (hours - 40)
                      : wages = hours * 7.50;
    ```

  - c. `(loanAmount >= 200000) ? closingCosts = 10000 : closingCosts = 8000;`

- **25.** a. 40.00 b. 40.00 c. 55.00

- **27.** a. 8 b. 64 c. 1 d. 12

- **29.** a. 7 b. 12167 c. 8000 d. 3

- **31.**

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

- **33.**

    ```cpp
    switch (classStanding)
    {
        case 'f':
            dues = 150.00;
            break;
        case 's':
            if (gpa >= 3.75)
                dues = 75.00;
            else
                dues = 120.00;
            break;
        case 'j':
            if (gpa >= 3.75)
                dues = 50.00;
            else
                dues = 100.00;
            break;
        case 'n':
            if (gpa >= 3.75)
                dues = 25.00;
            else
                dues = 75.00;
            break;
        default:
            cout << "Invalid class standing code." << endl;
    }
    ```

## 第 5 章

- **1.** a. 正确；b. 错误；c. 正确；d. 错误；e. 正确；f. 正确；g. 正确；h. 错误；i. 错误；j. 正确

- **3.** 40

- **5.** `if (ch > 'Z' || ch < 'A')`

- **7.** Sum = 22

- **9.** temp = 0

- **11.**
  - a. 20  *
  - b. *
  - c. 41 70 111  *
  - d. 27 44 71  *

- **13.** 将 while 循环语句替换为以下内容：

    ```cpp
    while (response == 'Y' || response == 'y')
    ```

    将 cout 语句

    ```cpp
    cout << num1 << " + " << num2 << " = " << (num1 - num2)
         << endl;
    ```

    替换为以下内容：

    ```cpp
    cout << num1 << " + " << num2 << " = " << (num1 + num2)
         << endl;
    ```

- **15.** `2  3  4  5  6`

- **17.** `0  3  8  15  24`

- **19.**
  - 循环控制变量：`j`
  - 初始化语句：`j = 1;`
  - 循环条件：`j <= 10;`
  - 更新语句：`j++`
  - 更新 `s` 值的语句：`s = s + j * (j - 1);`

- **21.** `num = 485, y = 15`

- **23.**
  - a. `*`
  - b. `无限循环`
  - c. `无限循环`
  - d. `****`
  - e. `******`
  - f. `***`

- **25.** x 和 y 的关系为：`3^y = x`

  输出：`x = 19683, y = 10`

- **27.**

    ```
    0 - 24
    25 - 49
    50 - 74
    75 - 99
    100 - 124
    125 - 149
    150 - 174
    175 - 200
    ```

- **29.**
  - a. 两者皆可
  - b. do ... while
  - c. while
  - d. while

- **31.** 在前测循环中，循环条件会在执行循环体之前进行求值。在后测循环中，循环条件会在执行循环体之后进行求值。后测循环至少执行一次，而前测循环可能一次都不执行。

- **33.**

    ```cpp
    int num;
    do
    {
        cout << "Enter a number less than 20 or greater than 75: ";
        cin >> num;
    }
    while (20 <= num && num <= 75);
    ```

- **35.**

    ```cpp
    int i = 0, value = 0;
    do
    {
        if (i % 2 == 0 && i <= 10)
            value = value + i;
        else if (i % 2 == 0 && i > 10)
            value = value + i;
        else
            value = value - i;
        i = i + 1;
    }
    while (i <= 20);

    cout << "value = " << value << endl;
    ```

  输出为：`value = 200`

- **37.**

    ```cpp
    cin >> number;
    while (number != -1)
    {
        total = total + number;
        cin >> number;
    }
    cout << endl;
    cout << total << endl;
    ```

- **39.**
  - a.

    ```cpp
    number = 1;
    while (number <= 10)
    {
        cout << setw(3) << number;
        number++;
    }
    ```

  - b.

    ```cpp
    number = 1;
    do
    {
        cout << setw(3) << number;
        number++;
    }
    while (number <= 10);
    ```

- **41.**
  - a. 36 94 260
  - b. 4 20
  - c. 30
  - d. 98 250

- **43.** -1 0 3 8 15 24

- **45.** 12 11 9 7 6 4 2 1

## 第 6 章

- **1.** a. 错误；b. 正确；c. 正确；d. 正确；e. 错误；f. 错误；g. 正确；h. 错误；i. 正确；j. 正确；k. 错误；l. 错误；m. 错误；n. 正确

- **3.** a. 18 b. 20.50 c. 87.20 d. 16.00 e. 1717.82 f. 2.80 g. 14.00 h. 11.16 i. 27.00 j. 20.00 k. 19.00 m. 2.25 n. 4096.00 o. 0.01 p. 3.03

- **5.** a 和 b

- **7.** a、b、c、d 和 e 均有效。在 f 中，函数调用缺少第二个参数。在 g 和 h 中，函数调用还需要一个参数。

- **9.**
  - a. 2；double
  - b. 3；int
  - c. 3；string

