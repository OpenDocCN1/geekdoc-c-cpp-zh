

4. 每个 switch 语句和块必须包含匹配的大括号。缺少 } 可能很难定位。在某些情况下，编译器可能要到文件末尾才发现 { 未匹配。在这种情况下，会生成如下错误信息：

```
Error...: Compound statement missing } in function ...
```

5. switch 语句中的选择器必须是整数兼容的。特别是，case 列表中选择器的值
- 不得是实数常量，且
- 不得是字符串常量。

6. switch 语句具有贯穿行为。特定 case 中语句列表的执行会继续进入后续的 case，直到遇到 break、return 或 switch 语句结束为止。为了避免这种行为，你必须记住在每个 switch 语句的语句列表末尾加上 break 或 return 语句（最后一个语句列表除外，在那里不是必须的）。

## TEST YOURSELF

Section 8.3

对于以下问题，假设 number 是一个 int 变量，code 是一个 char 变量，x 是一个 double 变量。

1. 如果 number 的值为 99，请说明以下 switch 语句产生的输出，或指出为何会发生错误：

```
switch(number)
{
    case 99:
        cout << number + 99 << endl;
        break;
    case -1:
        cout << number - 1 << endl;
        break;
    default:
        cout << "default\n";
}
```

2. 按第 1 题进行，但假设省略了 break 语句。

3. 按第 1 题进行，但假设 number 的值为 50。

6. 按第 2 题进行，但假设 number 的值为 -1。

7. 如果 code 的值为字母 B，请说明以下 switch 语句产生的输出，或指出为何会发生错误：

```cpp
switch (code)
{
    case 'A': case 'B':
                       cout << 123 << endl;
                       break;

    case 'P': case 'R': case 'X':
                       cout << 456 << endl;
                       break;
}
```

8. 按第 7 题进行，但假设 code 的值为字母 X。

9. 按第 7 题进行，但假设 code 的值为字母 M。

10. 如果 x 的值为 2.0，请说明以下 switch 语句产生的输出，或指出为何会发生错误：

```cpp
switch (x)
{
    case 1.0:
              cout << x + 1.0 << endl;
              break;

    case 2.0:
              cout << x + 2.0 << endl;
              break;
}
```

## EXERCISES

Section 8.2

1. 描述以下缩进不良的程序段产生的输出：

```cpp
int number = 4;
double alpha = -1.0;
if (number > 0)
    if (alpha > 0)
        cout << "first\n";
    else
        cout << "second\n";
    cout << "third\n";
```

Exercises 2 and 3 refer to the following if statement, where honors, awards, and goodStudent are of type bool:

```
if (honors)
    if (awards)
        goodStudent = true;
    else
        goodStudent = false;
else if (!honors)
    goodStudent = false;
```

2. 写一个等价于此的更简单的 if 语句。

3. 写一个等价于此 if 语句的单个赋值语句。

4. 如果 y 的值为 (a) 10？(b) 20？语句

```
int x = 0,
    y;
if ((x = 15) > y)
    cout << "Yes\n"
else
    cout << "No\n";
```

会产生什么输出（如果有）？

For Exercises 5–12, you are asked to write functions. To test these functions, you should write driver programs as instructed in Programming Problems 1–8 for Section 8.2 at the end of this chapter.

5. 在某个地区，只有当温度至少为 70°、相对湿度在 15 到 35 百分比之间，并且风速最多为每小时 10 英里时，才允许从飞机喷洒农药。编写一个布尔值函数 okToSpray()，接收表示温度、相对湿度和风速的三个数字，如果条件允许喷洒则返回 true，否则返回 false。

6. 某家信贷公司会在申请人的收入至少为 $25,000 或申请人的资产至少为 $100,000 时批准贷款申请；此外，申请人的总负债必须少于 $50,000。编写一个布尔值函数 creditApproved()，接收表示收入、资产和负债的三个数字，如果满足贷款批准标准则返回 true，否则返回 false。

7. 编写一个函数，如果 int 参数 year 的值是闰年的年份则返回 true，否则返回 false。（闰年是 4 的倍数；如果是 100 的倍数，则还必须是 400 的倍数。）

8. 编写一个函数，返回给定 int 参数 month（1, 2, …, 12）的天数，该参数为给定参数 year 的月份。使用练习 7 来确定 month 的值等于 2 时的天数。

9. 按练习 8 进行，但假设 month 是一个字符串变量，其值为月份的名称。

## Section 8.3

- 1. 编写一个 switch 语句，如果字符变量 transCode 的值为 'D'，则通过将 amount 加到 balance 上来增加 balance；如果 transCode 为 'W'，则通过从 balance 中减去 amount 来减少 balance；如果 transCode 为 'P'，则显示 balance 的值；否则显示非法交易信息。

- 2. 编写一个 switch 语句，对于给定的两个整数 a 和 b 以及给定的字符 operation，根据 operation 是 '+'、'-'、'*' 或 '/' 来计算并显示 a + b、a - b、a * b 或 a / b，如果不是这些则显示非法运算符信息。

For Exercises 3–6, write functions that use switch statements to compute what is required. To test these functions, you should write driver programs as instructed in Programming Problems 1–4 for Section 8.3 at the end of this chapter.

- 3. 给定一个小于 1000 的距离，返回根据以下表格确定的运费：

| Distance | Cost |
|---|---|
| 0 through 99 | $5.00 |
| At least 100 but less than 300 | $8.00 |
| At least 300 but less than 600 | $10.00 |
| At least 600 but less than 1000 | $12.00 |

- 4. 给定一个表示电视频道的数字，返回对应于该频道的电台呼号，或显示频道未使用的信息。使用以下频道号和呼号（或使用你所在地区可用的频道）：
  - 2: WCBS
  - 4: WNBC
  - 5: WNEW
  - 7: WABC
  - 9: WOR
  - 11: WPIX
  - 13: WNET

- 5. 给定一个月份的数字，返回月份的名称（或指示非法月份数字的错误信息）。

- 6. 按练习 5 进行，但返回月份的天数。（闰年是 4 的倍数；但如果是 100 的倍数，则还必须是 400 的倍数。）

## Section 8.4

- 1. 描述以下函数执行的操作：

```
int doSomething1(int value)
{
    return ( (value >= 0) ? value : -value );
}
```

- 2. 描述以下函数执行的操作：

```
char doSomething2(char ch)
{
    return ( ( ('A' <= ch) && (ch <= 'Z') ) ? ch+32 : ch );
}
```

- 3. 编写条件表达式，可替换输出语句中的空白：

```
cout << ____ << month << '/'
    << ____ << day << '/'
    << ____ << year % 100<< endl;
```

使得产生的输出如下：

| month | day | year | Output |
| 12 | 25 | 1999 | 12/25/99 |
| 10 | 1 | 1980 | 10/01/80 |
| 7 | 4 | 1976 | 07/04/76 |
| 2 | 2 | 2002 | 02/02/02 |

- 4. 编写一个条件表达式，可替换输出语句中的空白

```
cout << ____ << number<< endl;
```

使得产生的输出如下：

| number | Output |
| 123 | 123 |
| 23 | 023 |
| 3 | 003 |

- 5. 编写一个函数 smallerOf()，返回两个给定整数值中较小的那个。

- 6. 使用嵌套条件表达式，编写一个函数：
  - a. largestOf()，给定三个 int 值，返回其中最大的一个。
  - b. smallestOf()，给定三个 int 值，返回其中最小的一个。

