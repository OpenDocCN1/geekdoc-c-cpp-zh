

16. 下述代码段显示什么内容？

```
a = 1;
while (a < 5)
{
    Write("{0}", a);
    ++a;
}
```

- a. 1 2 3 4
- c. 4
- b. 1
- d. 无输出

17. 下述代码段的输出是什么？

```
s = 1;
while(s < 4)
    ++s;
    Write("{0}", s);
```

- a. 1
- c. 1 2 3 4
- b. 4
- d. 2 3 4

18. 下述代码段的输出是什么？

```
j = 5;
while(j > 0)
{
    Write("{0}", j);
    j--;
}
```

- a. 0
- c. 5 4 3 2 1
- b. 5
- d. 5 4 3 2 1

19. 下述代码段显示什么内容？

```
for(f = 0; f < 3; ++f)
    Write("{0}", f);
```

- a. 0
- c. 3
- b. 0 1 2
- d. 无输出

20. 下述代码段显示什么内容？

```
for(t = 0; t < 3; ++t)
    Write("{0}", t);
```

- a. 0
- c. 0 1 2
- b. 0 1
- d. 0 1 2 3

# 练习

## 编程练习

- 编写一个名为 `SumFiveInts` 的程序，允许用户输入五个整数并显示它们的和。

- 编写一个名为 `SumInts` 的程序，允许用户连续输入任意数量的整数，直到用户输入 999。显示所输入数值的和，但不包括 999。

- 编写一个名为 `EnterUppercaseLetters` 的程序，要求用户从键盘输入一个大写字母。如果输入的字符是大写字母，则显示 OK；如果不是大写字母，则显示错误信息。程序持续到用户输入感叹号为止。

- 编写一个名为 `DailyTemps` 的程序，不断提示用户输入一系列高温，直到用户输入一个哨兵值。有效温度范围为华氏 -20 到 130 度。当用户输入有效温度时，将其累加到总和中；当用户输入无效温度时，显示错误信息。在程序结束之前，显示输入的数量和平均温度。

- Daniel、Edward 和 Francis 是 Holiday Homes 的三名销售人员。编写一个名为 `HomeSales` 的程序，提示用户输入销售人员的首字母（D、E 或 F）。大写或小写首字母均有效。只要用户不输入 Z，就继续提示输入销售金额。对于任何无效输入，显示错误信息。记录每位销售人员的销售总额。用户输入 Z 或 x 来获取特定销售人员的总额、所有销售的总额以及总额最高的销售人员姓名。

- 编写一个名为 `DisplayMultiTable` 的程序，显示 1 到 10 之间两个整数所有组合的乘积表。

- 编写一个名为 `MultiplicationTable` 的程序，提示用户输入一个整数值，例如 7。然后显示该值与 1 到 10 的每个整数相乘的积。表格的前三行可能是 1 × 7 = 7, 2 × 7 = 14 和 3 × 7 = 21。

- 编写一个名为 `OddNums` 的程序，显示 1 到 99 之间的所有奇数。

- 编写一个名为 `Sum200` 的程序，对 1 到 200 的整数求和。在程序执行到一半时（前 100 个数字之后）以及结束时显示运行总和。

10. 编写一个名为 `Perfect` 的程序，显示 1 到 10,000 之间的每一个完美数。如果一个数等于所有能整除它的较小正整数的和，则该数为完美数。例如，6 是完美数，因为 1、2 和 3 能整除它，且它们的和为 6。

11. 在本章的“你来做”部分，我们在分析餐厅账单时为顾客创建了一个小费表。现在，创建一个名为 `TippingTable3` 的修改后的程序，其中以下每个值都从用户输入获取：

- 最低的小费百分比
- 最高的小费百分比
- 最低可能的餐厅账单
- 最高餐厅账单

12. 编写一个名为 `WebAddress` 的程序，要求用户输入公司名称。通过在名称前添加 `www.`、删除名称中的所有空格并添加 `.` 来建议一个良好的网络地址。

13. 编写一个名为 `CountVowels` 的程序，接受用户输入字符串并统计其中的大写字母数量。

14. 在上一章中，你创建了一个生成随机数、让用户猜测并显示是太低、太高还是正确的程序。现在创建一个名为 `GuessingGame2` 的程序，记录用户的尝试次数。

```
Random rand = new Random();
int target = rand.Next(1,101);
int guess = 0;
int attempts = 0;
while (guess != target)
{
    Write("输入1-100之间的数字:");
    guess = int.Parse(Console.ReadLine());
    attempts++;
    if (guess < target)
        Write("太低了!\n");
    else if (guess > target)
        Write("太高了!\n");
    else
        Write($"正确！你尝试了 {attempts} 次。\n");
```

## 调试练习

以下代码段包含错误。请找出并修复它们。

1. 下述代码旨在计算整数数组的平均值。
```c
int[] numbers = { 10, 20, 30, 40, 50 };
int sum = 0;
for (int i = 0; i <= numbers.Length; i++)
{
    sum += numbers[i];
}
double average = sum / numbers.Length;
Console.WriteLine("平均值是 {0}", average);
```

2. 下述代码旨在打印字符串数组的每个元素。
```csharp
string[] fruits = { "Apple", "Banana", "Cherry" };
for (int i = 0; i < fruits.Length; i++)
{
    Console.WriteLine(fruits[]);
}
```

3. 下述代码旨在查找整数数组中的最大值。
```csharp
int[] values = { 5, 12, 7, 21, 3 };
int max = values[0];
for (int i = 1; i < values.Length; i++)
{
    if (values[i] > max)
    {
        max = values[i];
    }
}
Console.WriteLine("最大值是 {0}", max);
```

4. 下述代码旨在反转数组。
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
Array.Reverse(numbers);
Console.WriteLine(numbers);
```

5. 下述代码旨在计算数组所有元素的和。
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };
int sum = 0;
foreach (int n in numbers)
{
    sum += n;
}
Console.WriteLine("和是 {0}", sum);
```

## 案例分析

1. 编写一个程序，询问用户想要输入的整数数量，然后创建一个相应大小的数组并允许用户填充它。最后，显示整数的和和平均值。

2. 编写一个程序，将名称列表存储在数组中并按字母顺序排序。然后，按排序后的顺序打印名称。

3. 编写一个程序，接收整数数组作为输入，并找到数组中的最小值和最大值。

4. 编写一个程序，使用二维数组表示 3x3 的网格。在控制台上打印该网格。

5. 编写一个程序，获取一个字符串数组并统计其中有多少个偶数。

