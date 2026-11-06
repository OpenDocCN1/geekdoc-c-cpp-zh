

```cpp
if (digit == 1) return "one";
if (digit == 2) return "two";
if (digit == 3) return "three";
if (digit == 4) return "four";
if (digit == 5) return "five";
if (digit == 6) return "six";
if (digit == 7) return "seven";
if (digit == 8) return "eight";
if (digit == 9) return "nine";
return "";
}

/**
 * Turns a number between 10 and 19 into its English name.
 * @param number an integer between 10 and 19
 * @return the name of the given number ("ten" … "nineteen")
 */
string teen_name(int number)
{
    if (number == 10) return "ten";
    if (number == 11) return "eleven";
    if (number == 12) return "twelve";
    if (number == 13) return "thirteen";
    if (number == 14) return "fourteen";
    if (number == 15) return "fifteen";
    if (number == 16) return "sixteen";
    if (number == 17) return "seventeen";
    if (number == 18) return "eighteen";
    if (number == 19) return "nineteen";
    return "";
}

/**
 * Gives the name of the tens part of a number between 20 and 99.
 * @param number an integer between 20 and 99
 * @return the name of the tens part of the number ("twenty" … "ninety")
 */
string tens_name(int number)
{
    if (number >= 90) return "ninety";
    if (number >= 80) return "eighty";
    if (number >= 70) return "seventy";
    if (number >= 60) return "sixty";
    if (number >= 50) return "fifty";
    if (number >= 40) return "forty";
    if (number >= 30) return "thirty";
    if (number >= 20) return "twenty";
    return "";
}

/**
 * Turns a number into its English name.
 * @param number a positive integer < 1,000
 * @return the name of the number (e.g. “two hundred seventy four”)
 */
string int_name(int number)
{
    int part = number; // The part that still needs to be converted
    string name; // The return value
73  if (part >= 100)
74  {
75      name = digit_name(part / 100) + " hundred";
76      part = part % 100;
77  }
78
79  if (part >= 20)
80  {
81      name = name + " " + tens_name(part);
82      part = part % 10;
83  }
84  else if (part >= 10)
85  {
86      name = name + " " + teen_name(part);
87      part = 0;
88  }
89
90  if (part > 0)
91  {
92      name = name + " " + digit_name(part);
93  }
94
95  return name;
96  }
97
98  int main()
99  {
100     cout << "Please enter a positive integer: ";
101     int input;
102     cin >> input;
103     cout << int_name(input) << endl;
104     return 0;
105 }
```

### 程序运行

```text
Please enter a positive integer: 729
seven hundred twenty nine
```

![](img/23fb3582e93ebc95909e1de029c3d388_242_0.png)

- 23. 解释如何改进 int_name 函数，使其能够处理最大为 9,999 的参数。
- 24. 为什么第 87 行将 part 设置为 0？
- 25. 当你调用 int_name(0) 时会发生什么？如何修改 int_name 函数以正确处理这种情况？
- 26. 按照编程提示 5.4 中的描述，追踪函数调用 int_name(72)。
- 27. 使用逐步求精的过程，将打印以下表格的任务分解为更简单的任务。

  | i | i * i * i |
  |---|---|
  | 1 | 1 |
  | 2 | 8 |
  | ... | ... |
  | 20 | 8000 |

立即练习 你可以尝试本章末尾的这些练习：R5.12、P5.16、P5.19。

## 编程提示 5.3

![](img/23fb3582e93ebc95909e1de029c3d388_243_0.png)

### 保持函数简短

编写函数是有一定代价的。你需要设计、编码和测试函数。函数需要文档化。你需要花费一些精力使函数可复用，而不是与特定上下文绑定。为了避免这种代价，我们总是倾向于将越来越多的代码塞进一个地方，而不是费劲将代码拆分为独立函数。经常可以看到缺乏经验的程序员编写出数百行长的函数。

经验法则：如果一个函数长到其代码无法在你的开发环境的一屏中放下，那么它可能应该被拆分开。

## 编程提示 5.4

![](img/23fb3582e93ebc95909e1de029c3d388_243_1.png)

### 追踪函数

当你设计一组复杂的函数时，在将程序交给计算机之前，进行手动走查是一个好主意。

拿一张索引卡或其他纸片，写下你想要研究的函数调用。写下函数名以及参数变量的名称和值，像这样：

![](img/23fb3582e93ebc95909e1de029c3d388_243_2.png)

然后写下函数变量的名称和初始值。将它们写在表格中，因为在走查代码时你会更新它们。

![](img/23fb3582e93ebc95909e1de029c3d388_243_3.png)

我们进入条件测试 part >= 100。part / 100 是 4，part % 100 是 16。digit_name(4) 很容易看出是 "four"。（如果 digit_name 很复杂，你会另外拿一张纸来算出那个函数调用。用这种方式积累好几张纸是很常见的。）

现在 name 已变为 name + " " + digit_name(part / 100) + " hundred"，即 "four hundred"，而 part 已变为 part % 100，即 16。

![](img/23fb3582e93ebc95909e1de029c3d388_243_4.png)

现在你进入 part >= 10 的分支。teen_name(16) 是 sixteen，因此变量现在有以下值：

| part | name |
|---|---|
| 416 | "--" |
| 16 | "four hundred" |
| 0 | "four hundred sixteen" |

现在就很清楚了，为什么需要在第 87 行将 part 设为 0。否则，你会进入下一个分支，结果将是 "four hundred sixteen six"。追踪代码是理解函数微妙之处的有效方法。

## 编程提示 5.5

![](img/23fb3582e93ebc95909e1de029c3d388_244_0.png)

### 桩函数

在编写大型程序时，不可能总是同时实现和测试所有函数。你经常需要测试一个调用另一个函数的函数，但另一个函数尚未实现。这时，你可以用一个桩函数临时替代缺失的函数。桩函数是一个返回简单值的函数，该值足以用来测试另一个函数。以下是桩函数的示例：

```cpp
/**
   Turns a digit into its English name.
   @param digit an integer between 1 and 9
   @return the name of digit ("one" ... "nine")
*/
string digit_name(int digit)
{
   return "mumble";
}

/**
   Gives the name of the tens part of a number between 20 and 99.
   @param number an integer between 20 and 99
   @return the tens name of the number ("twenty" ... "ninety")
*/
string tens_name(int number)
{
   return "mumblety";
}
```

如果你将这些桩函数与 int_name 函数组合，并用参数 274 进行测试，你会得到结果 "mumble hundred mumblety mumble"，这表明 int_name 函数的基本逻辑工作正常。

![](img/23fb3582e93ebc95909e1de029c3d388_244_1.png)

桩函数是不完整的函数，可用于测试。

在同一作用域中定义两个同名变量是不合法的。例如，以下代码是*不*合法的：

```cpp
int main()
{
    double volume = cube_volume(2);
    double volume = cube_volume(10);
    // ERROR: cannot define another volume variable in this scope
    ...
}
```

但你可以在一个**嵌套块**中定义另一个同名变量。这里，我们定义了两个名为 amount 的变量。

```cpp
double withdraw(double balance, double amount)
{
    if (...)
    {
        double amount = 10; // Another variable named amount
        ...
    }
    ...
}
```

嵌套块中的变量会遮蔽外部块中同名的变量。

参数变量 amount 的作用域是整个函数，但嵌套块内部除外。在嵌套块内部，amount 指的是在该块中定义的变量。我们说内部变量遮蔽了外部块中定义的变量。你编写的函数应避免这种可能引起混淆的情况，只需重命名其中一个变量即可。

定义在函数内部的变量称为**局部变量**。C++ 还支持**全局变量**：定义在函数外部的变量。全局变量对其定义之后的所有函数可见。例如，`<iostream>` 头文件定义了全局变量 `cin` 和 `cout`。

以下是一个全局变量的示例：

局部变量定义在函数内部。全局变量定义在函数外部。

```cpp
int balance = 10000; // A global variable

void withdraw(double amount)
{
    if (balance >= amount)
    {
        balance = balance - amount;
    }
}

int main()
{
    withdraw(1000);
    cout << balance << endl;
    return 0;
}
```

变量 balance 的作用域同时覆盖 withdraw 函数和 main 函数。

通常，全局变量不是个好主意。当多个函数更新全局变量时，结果可能难以预测。尤其是在由多个程序员开发的大型程序中，每个函数的效果清晰且易于理解非常重要。你应该在程序中避免使用全局变量。

在你的程序中避免使用全局变量。

