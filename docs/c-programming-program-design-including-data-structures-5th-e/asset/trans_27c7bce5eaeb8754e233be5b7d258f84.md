
## 示例 5-9

下面的 `for` 循环输出前 10 个非负整数：

```cpp
for (i = 0; i < 10; i++)
    cout << i << " ";
cout << endl;
```

初始语句 `i = 0` 将 `int` 变量 `i` 初始化为 0。接着计算循环条件 `i < 10`。因为 `0 < 10` 为真，输出语句执行并输出 0。然后执行更新语句 `i++`，将 `i` 的值设为 1。再次计算循环条件，它仍然为真，如此反复。当 `i` 变为 10 时，循环条件求值为假，`for` 循环终止，随后执行 `for` 循环之后的语句。

`for` 循环的循环体可以是简单语句或复合语句。

下面的示例进一步说明 `for` 循环如何执行。

## 示例 5-10

- 1. 下面的 `for` 循环输出 `Hello!` 和一个星号（各占一行）五次：

  ```cpp
  for (i = 1; i <= 5; i++)
  {
      cout << "Hello!" << endl;
      cout << "*" << endl;
  }
  ```

- 2. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 1; i <= 5; i++)
      cout << "Hello!" << endl;
      cout << "*" << endl;
  ```

这个循环输出 `Hello!` 五次，而星号只输出一次。注意，`for` 循环只控制第一个输出语句，因为这两个输出语句没有组成复合语句。因此，第一个输出语句执行五次，因为 `for` 循环体执行五次。`for` 循环执行完毕后，第二个输出语句只执行一次。这种缩进虽然会被编译器忽略，但仍然具有误导性。

## 示例 5-11

下面的 `for` 循环执行五次空语句：

```cpp
for (i = 0; i < 5; i++);      //Line 1
    cout << "*" << endl;       //Line 2
```

`for` 语句末尾的分号（位于输出语句之前，第 1 行）终止了 `for` 循环。这个 `for` 循环的动作是空的，即空操作。

前面的示例表明，要让 `for` 循环执行所需动作，需要格外小心。

以下是对 `for` 循环的一些说明：

- 如果循环条件初始为 `false`，则循环体不会执行。
- 更新表达式执行时会改变循环控制变量（由初始表达式初始化）的值，最终使循环条件的值为 `false`。如果循环条件始终为 `true`，则 `for` 循环体会无限执行。
- C++ 允许对 `double` 类型（或任何实数类型）的循环控制变量使用小数值。由于不同计算机可能会给这些循环控制变量带来不同结果，应避免使用这样的变量。
- `for` 语句末尾（正好在循环体之前）的分号是语义错误。在这种情况下，`for` 循环的动作为空。
- 在 `for` 语句中，如果省略循环条件，则假定其为 `true`。
- 在 `for` 语句中，可以省略全部三个语句——初始语句、循环条件和更新语句。下面是一个合法的 `for` 循环：

```cpp
for (;;)
    cout << "Hello" << endl;
```

这是一个无限 `for` 循环，会不断输出单词 `Hello`。

下面是更多 `for` 循环示例。

## 示例 5-12

如果正确设置 `for` 循环控制表达式，就可以使用 `for` 循环倒计数。

例如，考虑下面的 `for` 循环：

```cpp
for (i = 10; i >= 1; i--)
    cout << " " << i;
cout << endl;
```

输出为：

```text
10 9 8 7 6 5 4 3 2 1
```

在这个 `for` 循环中，变量 `i` 被初始化为 10。每次循环迭代后，`i` 递减 1。只要 `i >= 1`，循环就继续执行。

## 示例 5-13

可以按任意固定数值递增（或递减）循环控制变量。在下面的 `for` 循环中，变量初始化为 1；在 `for` 循环末尾，`i` 递增 2。这个 `for` 循环输出前 10 个正奇数。

```cpp
for (i = 1; i <= 20; i = i + 2)
    cout << i << " ";
cout << endl;
```

## 示例 5-14

假设 `i` 是一个 `int` 变量。

- 1. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 10; i <= 9; i++)
      cout << i << " ";
  cout << endl;
  ```

  在这个 `for` 循环中，初始语句将 `i` 设为 10。由于循环条件（`i <= 9`）初始为 `false`，所以什么也不会发生。

- 2. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 9; i >= 10; i--)
      cout << i << " ";
  cout << endl;
  ```

  在这个 `for` 循环中，初始语句将 `i` 设为 9。由于循环条件（`i >= 10`）初始为 `false`，所以什么也不会发生。

- 3. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 10; i <= 10; i++)       //Line 1
      cout << i << " ";              //Line 2
  cout << endl;                       //Line 3
  ```

  在这个 `for` 循环中，初始语句将 `i` 设为 10。循环条件（`i <= 10`）求值为 `true`，所以第 2 行中的输出语句执行，输出 10。接着，更新语句将 `i` 的值递增 1，因此 `i` 的值变为 11。现在循环条件求值为假，`for` 循环终止。注意，第 2 行中的输出语句只执行一次。

- 4. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 1; i <= 10; i++);   //Line 1
      cout << i << " ";        //Line 2
      cout << endl;            //Line 3
  ```

  这个 `for` 循环对第 2 行中的输出语句没有影响。`for` 语句末尾的分号终止了 `for` 循环；因此 `for` 循环的动作为空。输出语句独立存在，只执行一次。

- 5. 考虑下面的 `for` 循环：

  ```cpp
  for (i = 1; ; i++)
      cout << i << " ";
  cout << endl;
  ```

  在这个 `for` 循环中，由于 `for` 语句省略了循环条件，循环条件始终为真。这是一个无限循环。

## 示例 5-15

在这个示例中，`for` 循环读取五个数并求它们的和与平均值。考虑下面的程序代码，其中 `i`、`newNum`、`sum` 和 `average` 是 `int` 变量。

```cpp
sum = 0;

for (i = 1; i <= 5; i++)
{
    cin >> newNum;
    sum = sum + newNum;
}

average = sum / 5;
cout << "The sum is " << sum << endl;
cout << "The average is " << average << endl;
```

在前面的 `for` 循环中，读取一个 `newNum` 后，将该值加到此前已计算的（部分）和中，该和包含当前数之前读取的所有数。变量 `sum` 在 `for` 循环之前初始化为 0。因此，程序读取第一个数并将其加到 `sum` 的值之后，变量 `sum` 保存的就是第一个数的正确和。

**注意** `for` 循环的语法如下：

```cpp
for (initial expression; logical expression; update expression)
    statement
```

在功能上等价于下面的 `while` 语句：

```cpp
initial expression
while (expression)
{
    statement
    update expression
}
```

例如，下面的 `for` 循环和 `while` 循环是等价的：

```cpp
for (int i = 0; i < 10; i++)
    cout << i << " ";
cout << endl;

int i = 0;
while (i < 10)
{
    cout << i << " ";
    i++;
}
cout << endl;
```

如果循环的迭代次数已知或可以预先确定，程序员通常使用 `for` 循环。

## 示例 5-16（斐波那契数程序：再探）

上一节给出的编程示例：斐波那契数使用 `while` 循环来确定所需的斐波那契数。可以将 `while` 循环替换为等价的 `for` 循环，如下所示：

```cpp
for (counter = 3; counter <= nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
    counter++;
} //end for
```

使用 `for` 循环确定所需斐波那契数的程序的完整程序清单，在本书配套网站上给出。该程序名为 Ch5_FibonacciNumberUsingAForLoop.cpp。

在下面的 C++ 程序中，我们建议你逐步走查每个步骤。

