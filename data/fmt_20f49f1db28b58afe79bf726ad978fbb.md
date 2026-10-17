
# 第 4 章 循环

这是该脚本的一个示例：

```matlab
>> aveposnum

Enter a positive number: -5

No positive numbers to average.

aveposnum

Enter a positive number: 8

Enter a positive number: 3

Enter a positive number: -6

Enter average was 5.00
```

等待，OCR 包含了一些碎片部分和重复。我将根据提供的片段重新构建流程以确保专业输出。

## 4.4 While 循环

`findval.m`

```matlab
% Reads data from a file, but only plots the numbers
% up to a flag of -99. Uses find and the colon operator.
load experdt.dat

where = find(experd) == -99;

newvec = experdt(1:where-1);

plot(newvec,'ko')
```

### 4.4.3 While 循环中的输入

以下脚本重复提示用户输入正数的过程，只要用户在提示时正确输入正数。一旦用户输入负数，程序将打印 `OK` 并结束。

`whileposnum.m`

```matlab
% Prompts the user and echo prints the numbers
% until the user enters a negative number
inputnum=input('Enter a positive number: ');

while inputnum >= 0
    fprintf('You found %d.\n',inputnum)
    inputnum = input('Enter a positive number: ');
end

fprintf('OK\n');
```

当程序执行时，输入/输出可能如下所示：

```matlab
>> whileposnum

Enter a positive number: 6

You entered a 6.
```

```
Enter a positive number: -2

OK!
```

如果用户第一次输入负数，则没有任何值会被回显打印：

```matlab
>> whileposnum

Enter a positive number: -33

OK!
```

这说明了 `while` 循环的一个非常重要的特性：如果条件的值在第一次求值时为假，则循环体可能不会执行。

# 第 4 章 循环

正如我们之前看到的，如果输入的是字符而不是数字，MATLAB 将给出错误信息。

```matlab
>> whileposnum

Enter a positive number: a

??? Error using -->input

Undefined function or variable 'a'.

Enter a positive number: -4

OK!
```

然而，如果该字符实际上是变量名，它将使用该变量的值作为输入。例如：

```matlab
>> a = 5;

>> whileposnum

Enter a positive number: a

You entered a 5.

Enter a positive number: -4

OK!
```

### 4.4.4 While 循环中的计数

当预先不知道脚本中会输入多少值时，通常需要统计输入值的数量。例如，如果将数字读取到脚本中并想要这些数字的平均值，脚本必须将它们相加并记录个数，以便计算平均值。上一个脚本的变体统计了用户输入的数字个数：

```matlab
countposnum.m
% Prompts the user for positive numbers and echo prints as
% long as the user enters positive numbers
% Counts the positive numbers entered by the user
counter=0;
inputnum=input('Enter a positive number: ');

while inputnum >= 0
    fprintf('You entered %d.\n\n',inputnum)
    counter = counter + 1;
    inputnum = input('Enter a positive number: ');
end

fprintf('Thanks, you entered %d positive numbers\n',counter);
```

### 4.4.5 在 While 循环中检查用户输入

在大多数应用程序中，当提示用户输入某些内容时，有一个有效的值范围。如果用户输入了错误值，程序不应该使用错误值继续运行或仅打印错误信息，而应该重复提示、读取值并进行检查，直到用户输入一个正确范围内的值。这是条件循环的一个非常常见的应用，即循环直到用户正确输入一个正数。这被称为错误检查。

```matlab
>> aveposnum

Enter a positive number: -5

No positive numbers to average.

aveposnum

Enter a positive number: 8

Enter a positive number: 3

Enter a positive number: -6

Enter average was 5.00
```

例如，以下脚本提示用户输入正数，并循环打印错误信息且重复提示，直到用户最终输入一个正数。

```matlab
readenum.m
# Loop until the user enters a positive number
inputnum=input('Enter a positive number: ');

while inputnum >= 0
    fprintf('You entered %d.\n',inputnum)
    inputnum = input('Enter a positive number: ');
end

fprintf('OK\n');
```

忘记了基于乘法的数组操作，必须在运算符中使用点乘（dot）。换句话说，对于逐项乘法、除法或幂运算，运算符是 `*`、`/` 和 `^`。

尝试在数组上使用 `||` 或 `&&`；在处理数组时始终使用 `| &`；`||` 和 `&&` 仅用于标量。

没有意识到 `while` 循环的操作可能永远不会执行。

没有在程序中进行错误检查。

## 编程风格指南

- 仅在必要时使用循环进行重复：
  - 使用 `for` 语句作为计数循环
  - 使用 `while` 语句作为条件循环

- 如果希望使用内置常量 `i` 和 `j`，则不要将 `i` 或 `j` 作为迭代变量名。

- 缩进循环的操作。

- 如果循环变量仅用于指定循环执行的次数，使用冒号运算符 `1:n`，其中 `n` 是要执行操作的次数。

- 尽可能预分配向量和矩阵（当提前已知大小时）。

- 在循环中读取数据时，只有当需要再次访问单个数据值时，才将其存储在数组中。

- 尽可能将代码向量化。如果在 MATLAB 中没有必要使用循环，就不要使用！

- 在函数中使用数组运算符 `*`、`/`，以便输入参数可以是数组而不仅仅是标量。

| MATLAB 函数与命令 |
| :--- |
| `while` `sum` `cumprod` `any` |
| `for` `prod` `min` `all` |
| `end` `cumsum` `max` `find` |
| `factorial` |

# MATLAB 运算符
- 矩阵的逐元素乘法 `|` 
- 矩阵的逐元素与运算 `&`

## 练习题

- 1. 写一个 `for` 循环，打印从 1.1 到 2.9 步长为 0.1 的实数列。
- 2. 编写一个函数 `sumsteps2`，计算并返回从 1 到 `n` 步长为 2 的和，其中 `n` 是传递给函数的参数。如果传递 11，它将返回 `1 + 3 + 5 + 7 + 9 + 11`。使用 `for` 循环实现此功能。调用该函数的形式如下：

```
>> sumsteps2(11)

ans = 36
```
- 3. 编写一个函数 `prodby`，接收一个正整数 `n`，并计算并返回从 1 到 `n` 的奇数的乘积（如果 `n` 是偶数，则返回从 1 到 `n-1`）。
- 4. 编写一个名为 `geomser` 的函数，它接收 `r` 和 `n` 的值，并计算并返回几何级数和：

```
1 + r + r² + r³ + r⁴ + ... + rⁿ
```
调用该函数的示例说明了结果：

```
>> geomser(1,5)

ans = 6

>> disp(geomser(2,4))

31
```
- 5. 提示用户输入整数 `n` 并打印 "I love this stuff!" 次。
- 6. 在命令行窗口中，写一个 `for` 循环，遍历从 32 到 255 的整数。对于每个整数，显示字符编码中对应的字符。
- 7. 在命令行窗口中，写一个 `for` 循环，以句子格式打印向量变量中的元素。例如，如果向量是：

```
>> vec = [5.5 11 3.45];
```
结果将是：
Element 1 is 5.50.
Element 2 is 11.00.
Element 3 is 3.45.

# 练习 155

无论向量中有多少元素，`for` 循环都应该有效。

- 创建一个 `1 x 6` 的随机整数向量，每个范围在 1 到 20 之间。使用内置函数找到向量中的最小值和最大值。还使用 `cumsum` 创建一个累积和向量。

- 为向量变量编写一个关系表达式，以验证由 `cumsum` 创建的向量的最后一个值是否等于 `sum` 返回的结果。

- 输入此脚本并对结果感到惊讶！尝试更多点以获得更清晰的图景，但不要过头——这在你的计算机上可能需要一些时间。

```matlab
clear
clf
x = rand;
y = rand;
plot(x,y)
hold
for it = 1:2000
choice = round(rand*2);
if choice == 0
x = x/2;
y = y/2;
elif choice == 1
x = (x+1)/2;
y = y/2;
else
x = (x+0.5)/2;
y = (y+1)/2;
end
end
plot(x,y)
hold
end
```

- 音频工程师从麦克风录制了一个声音信号。声音经过了采样，这意味着是间隔记录的（而不是连续信号）。每个数据样本的单位是伏特。然而，麦克风有时未开启，因此低于某些阈值的样本被视为麦克风未开启时的数据，因此不是有效的数据样本。音频工程师想知道声音信号的平均电压。编写一个脚本要求用户输入阈值和数据样本数量，然后输入各个数据样本。程序将打印平均值和有效数据样本的数量，如果没有有效样本，则打印错误。命令行窗口中输入输出的示例：

Please enter the threshold below which samples will be considered invalid: 3.0

Please enter the number of data samples: 7

Please enter data sample: 0.4

Please enter data sample: 5.5

Please enter data sample: 2.1

Please enter data sample: 6.2

Please enter data sample: 0.3

Please enter data sample: 5.4

The average of the 4 valid samples is 5.5 volts. Note: 如果没有有效样本，程序将打印错误而不是最后显示的最后一行。

- 写一个脚本从矩阵中加载数据。创建数据文件，并确保文件中每行的值数量相同，以便将其加载到矩阵中。使用 `for` 循环，它将创建许多作为矩阵行的图形（Figures），并绘制每一行的数字。例如，如果文件包含：

4 9

30 18

将创建两个图形，如图 4 所示。

- 机器切割了 N 根管子。切割后，每根管子都测量了重量和长度并存储在名为 `'pipe'` 的文件中（忽略单位，管子重量在 1 到 10 之间）。使用 `for` 循环，并编写一个脚本计算总和。该脚本会打印：

1 4

2 6

3 9

4 12

5 15

20

- 风寒指数（WCF）测量体感有多冷，它取决于给定的温度 T（华氏度）和风速 V（英里/小时）。公式为：
`WCF = 35.7 + 0.6T - 0.35V - 0.06TV²`
编写一个函数接收温度和风速作为参数，并返回 WCF。使用循环，打印温度从 -20 到 55（步长为 5）、风速从 0 到 55（步长为 5）的表格。调用函数进行计算。

- 20. 不要像上一个问题那样打印风寒指数，创建一个风寒指数矩阵并写入文件。

- 21. 生成随机整数 `n`，创建一个从 1 到 `n` 步长为 2 的整数向量，平方这些值并绘制。

- 22. 向量 `v` 存储了 Green Cells 公司员工每周的工作时间，以及小时薪率。例如，如果变量存储：

```
>> v

v = 33.0000 10.5000 40.0000 18.0000 20.0000 7.5000
```
第一个员工工作了 33 小时，每小时 10.50 元；第二个工作了 40 小时，每小时 18 元。编写代码将其分成两个向量，一个存储工作时间，另一个存储薪率。然后使用数组乘运算符创建一个向量，在新向量中存储每个员工的总薪水。

- 23. 数学家欧拉证明了以下公式：
`π = 1 + 1/4 + 1/9 + 1/16 + ...`
与其寻找数学证明，不如尝试验证该猜想是否正确。注意：处理此问题的基本方法：或者选择项的个数，或者循环直到和接近 `π/6`。

- 24. 写一个脚本提示用户输入圆锥的半径和高度，对用户输入的半径和高度进行错误检查，然后计算并打印圆锥的体积。

- 25. 写一个脚本（例如 `findmine`），提示用户输入最小和最大整数，然后输入另一个在最小到最大范围内的整数。脚本将在该范围内生成随机整数，直到生成匹配用户的选择。脚本将打印在找到用户的选择之前生成了多少个随机整数。

```
>> findmine

请输入最小值值: -2

请输入最大值: 3

现在在此范围内输入您的选择: 0

共花费了 3 次尝试生成了您的数字
```

- 26. 编写一个脚本 `>0`，该脚本提示用户输入 N 个整数，并将正数 `=0` 写入名为 `pos` 的 ASCII 文件中，将负数写入名为 `neg` 的 ASCII 文件中。进行错误检查以确保用户输入了正数 N 个整数。

- 27. 编写一个脚本，该脚本将持续提示用户输入正数并将其存储在变量中，直到用户输入负数为止。

- 28. 编写一个脚本，使用 `menu` 函数为用户提供 `fix`、`floor` 和 `ceil` 函数的选择。通过循环菜单进行错误检查，直到用户按下其中一个按钮（如果用户点击菜单栏上的 X，可能会发生错误）。生成一个随机数，并打印用户对该数执行的函数的结果（例如 `fix(5)`）。

- 29. 编写一个脚本 `echoletters`，回字母表中的字母并打印，直到用户输入一个非字母表的字符为止。此时，脚本将打印该非字母字符以及输入的字母计数。以下是运行该脚本的示例：

```
>> echoletters

输入一个字母: T

感谢，你输入了 T

输入一个字母: a

感谢，你输入了 a

输入一个字母: 8

8 不是字母

你输入了 2 个字母
```

```
>> echoletters

输入一个字母: !

! 不是字母

你输入了 0 个字母
```
格式必须与所示完全一致。

- 30. 编写一个名为 `ptemps` 的脚本，提示用户输入 -16 到 20之间的最大摄氏度值；进行错误检查确保其在该范围内，打印一个显示华氏度和摄氏度的表格，直到达到最大值。第一个超过最大值的值不应被打印。表格应从 0 度华氏开始，每隔 5 度增加一次，直到达到最大值（摄氏度）。两个温度都应以宽度为 6 一位小数的形式打印。公式为 `C = 5/9 (F - 32)`。例如，脚本的执行情况可能如下（格式应与所示完全一致）：

```
>> prtemps

在提示时，输入 -16 到 20 范围内的摄氏度温度。

输入最大温度: 30

错误！请输入最大温度: 9

F           C

0.0         -17.8

5.0         -15.0

10.0        -12.2

15.0         -9.4

20.0         -6.7

25.0         -3.9

30.0         -1.1

35.0         1.7

40.0         4.4

45.0         7.2
```
