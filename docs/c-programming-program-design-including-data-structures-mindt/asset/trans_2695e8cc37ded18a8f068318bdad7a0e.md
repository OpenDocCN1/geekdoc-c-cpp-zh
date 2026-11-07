
```cpp
cout << num1 << " " << num2 << " " << first % 5
     << " " << (second % 7) << endl;

return;
}
```

- 31. 预测试循环和后测试循环有什么区别？(2, 4, 5)

- 32. 下列每个循环将执行多少次？每种情况下的输出是什么？(5)

  - a.
    ```cpp
    x = 5; y = 50;

    x = x + 10;
    while (x < y)
        cout << x << " " << y << endl;
    ```
  - b.
    ```cpp
    x = 5; y = 80;
    do
        x = x * 2;
    while (x < y);
    cout << x << " " << y << endl;
    ```
  - c.
    ```cpp
    x = 5; y = 20;
    do
        x = x + 2;
    while (x >= y);
    cout << x << " " << y << endl;
    ```
  - d.
    ```cpp
    x = 5; y = 35;
    while (x < y)
        x = x + 10;
    cout << x << " " << y << endl;
    ```
  - e.
    ```cpp
    x = 5; y = 30;
    while (x <= y)
        x = x * 2;
    cout << x << " " << y << endl;
    ```
  - f.
    ```cpp
    x = 5; y = 30;
    while (x <= y)
        x = x + 2;
    cout << x << " " << y << endl;
    ```

- 33. 编写一个输入语句验证循环，提示用户输入一个小于20或大于75的数。(2, 4, 5)

- 34. 将以下代码改写为for循环。(2, 4)

  ```cpp
  int i = 0, value = 0;

  while (i <= 20)
  {
      if (i % 2 == 0 && i <= 10)
          value = value + i * i;
      else if (i % 2 == 0 && i > 10)
          value = value + i;
      else
          value = value - i;
      i = i + 1;
  }

  cout << "value = " << value << endl;
  ```

  这个循环的输出是什么？

- 35. 将练习34中的while循环改写为do...while循环。(2, 5)

- 36. 下列程序中的do...while循环本应读取一些数，直到遇到哨兵值（本例中为-1）。它本应将除哨兵值之外的所有数相加。如果数据如下所示：(5)

  12    5    30    48    -1

  程序没有正确地将这些数相加。请改正程序，使其正确地将这些数相加。

  ```cpp
  #include <iostream>

  using namespace std;
  int main()
  {
      int total = 0,
          count = 0,
          number;

      do
      {
          cin >> number;
          total = total + number;
          count++;
      }
      while (number != -1);

      cout << "The number of data read is " << count << endl;
      cout << "The sum of the numbers entered is " << total
           << endl;

      return 0;
  }
  ```

- 37. 使用与练习36相同的数据，下面的循环也会失败。请改正它。(2)

  ```cpp
  cin >> number;
  while (number != -1)
      total = total + number;
      cin >> number;
      cout << endl;
      cout << total << endl;
  ```

- 38. 使用与练习36相同的数据，下面的循环也会失败。请改正它。(2)

  ```cpp
  cin >> number;
  while (number != -1)
  {
      cin >> number;
      total = total + number;
  }
  cout << endl;
  cout << total << endl;
  ```

- 39. 给定以下程序段：(2, 4, 5)

  ```cpp
  for (number = 1; number <= 10; number++)
      cout << setw(3) << number;
  ```

  编写一个while循环和一个do...while循环，使其具有相同的输出。

- 40. 给定以下程序段：(2, 4, 5)

  ```cpp
  int i;
  int value = 3;

  for (i = 0; i < 5; i++)
      value = value * (i + 1) + i;

  cout << "value = " << value << endl;
  ```

  编写一个while循环和一个do...while循环，使其具有相同的输出。

- 41. 考虑以下程序。(5)

  ```cpp
  #include <iostream>

  using namespace std;

  int main()
  {
      int num1, num2;
      int temp;

      cout << "Enter two integers: ";
      cin >> num1 >> num2;
      cout << endl;

      do
      {
          temp = 2 * (num1 + num2);
          num1 = num2;
          num2 = temp;
          cout << temp << " ";
      }
      while (((temp + num1) % 3) != 0);

      cout << endl;

      return 0;
  }
  ```

  - a. 如果输入为7 11，输出是什么？
  - b. 如果输入为-4 6，输出是什么？
  - c. 如果输入为6 9，输出是什么？
  - d. 如果输入为22 27，输出是什么？

- 42. 为了了解嵌套`for`循环如何工作，请对以下程序段进行一次走查，并在每种情况下确定确切的输出。(4, 7)

  - a.
    ```cpp
    int i, j;

    for (i = 1; i <= 5; i++)
    {
        for (j = 1; j <= 5; j++)
            cout << setw(3) << i;
        cout << endl;
    }
    ```
  - b.
    ```cpp
    int i, j;
    for (i = 1; i <= 5; i++)
    {
        for (j = (i + 1); j <= 5; j++)
            cout << setw(5) << j;
        cout << endl;
    }
    ```
  - c.
    ```cpp
    int i, j;
    for (i = 1; i <= 5; i++)
    {
        for (j = 1; j <= i; j++)
            cout << setw(3) << j;
        cout << endl;
    }
    ```
  - d.
    ```cpp
    const int M = 10;
    const int N = 10;
    int i, j;

    for (i = 1; i <= M; i++)
    {
        for (j = 1; j <= N; j++)
            cout << setw(3) << M * (i - 1) + j;
        cout << endl;
    }
    ```

## 编程练习

- 1. 编写一个程序，提示用户输入一个整数，然后输出该数的各位数字以及这些数字的和。例如，它应将`3456`的各位数字输出为`3 4 5 6`，将`8030`的各位数字输出为`8 0 3 0`，将`2345526`的各位数字输出为`2 3 4 5 5 2 6`，将`4000`的各位数字输出为`4 0 0 0`，并将`-2345`的各位数字输出为`2 3 4 5`。

- 2. π的值可以用以下级数近似：

  $$\pi = 4\left(1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots + \frac{1}{2n-1} + \frac{1}{2n+1}\right)$$

  下列程序使用该级数求π的近似值。但是，语句顺序不正确，而且程序中还有一个错误。重新排列语句并删除错误，使该程序可用于近似π。

  ```cpp
  #include <iostream>
  #include <iomanip>

  using namespace std;

  int main()
  {
      double pi = 0;
      long i;
      long n;

      cin >> n;
      cout << "Enter the value of n: ";
      cout << endl;

      if (i % 2 == 0)
          pi = pi + (1 / (2 * i + 1));
      else
          pi = pi - (1 / (2 * i + 1));

      for (i = 0; i < n; i++)
      {
          pi = 0;
          pi = 4 * pi;
      }

      cout << endl << "pi = " << pi << endl;

      return 0;
  }
  ```

- 3. 程序Telephone Digits只输出与大写字母对应的电话数字。重写该程序，使其同时处理大写和小写字母，并输出相应的电话数字。如果输入不是大写或小写字母，程序必须输出适当的错误消息。

- 4. 为了使电话号码更容易记住，一些公司使用字母来表示其电话号码。例如，使用字母，电话号码438-5626可以表示为GET LOAN。在某些情况下，为了使电话号码有意义，公司可能会使用超过七个字母。例如，225-5466可以显示为CALL HOME，其中使用了八个字母。编写一个程序，提示用户输入以字母表示的电话号码，并输出相应的数字电话号码。如果用户输入的字母超过七个，则只处理前七个字母。还要在第三位数字后输出-（连字符）。允许用户使用大写和小写字母以及单词之间的空格。此外，程序应处理用户想要处理的任意多个电话号码。

- 5. 编写一个程序，提示用户输入两个整数。程序输出这两个整数之间（含这两个整数）有多少个数是3的倍数，有多少个数是5的倍数。

- 6. 编写一个程序，提示用户输入一个正整数。然后输出一条消息，指出该数是否为素数。（注意：偶数如果是2，则为素数。奇数整数如果不是能被任何小于或等于该数平方根的奇数整除，则为素数。）

- 7. 设n = aₖaₖ₋₁aₖ₋₂…a₁a₀是一个整数，且t = a₀ − a₁ + a₂ − … + (−1)ᵏaₖ。已知n能被11整除当且仅当t能被11整除。例如，假设n = 8784204。则t = 4 − 0 + 2 − 4 + 8 − 7 + 8 = 11。因为11能被11整除，所以8784204能被11整除。如果n = 54063297，则t = 7 − 9 + 2 − 3 + 6 − 0 + 4 − 5 = 2。因为2不能被11整除，所以54063297不能被11整除。编写一个程序，提示用户输入一个正整数，然后使用此判定标准确定该数是否能被11整除。

- 8. 编写一个程序，使用while循环执行以下步骤：

  - a. 提示用户输入两个整数：`firstNum`和`secondNum`（`firstNum`必须小于`secondNum`）。
  - b. 输出`firstNum`和`secondNum`之间的所有奇数。
  - c. 输出`firstNum`和`secondNum`之间所有偶数的和。
  - d. 输出1到10之间的数及其平方。

