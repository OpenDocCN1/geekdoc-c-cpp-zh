
**输出：**

```text
Example of math.ceil()
xc is 6
yc is 8
zc is 5

Example of math.floor()
xf is 5
yf is 7
zf is 4

Example of round()
xr is 5
yr is 8
zr is 4
```

## 加法、减法、乘法、除法

这似乎不言自明，但由于进行任何基本计算都至关重要，我将介绍 4 种基本数学运算。

```python
n1 = float(input('num1: '))
n2 = float(input('num2: '))

Sum = n1 + n2
difference = n1 - n2
product = n1 * n2
quotient = n1/n2

print()
print(f"The sum is {Sum}")
print(f"The difference is {difference}")
print(f"The product is {product}")
print(f"The quotient is {quotient}")
```

在这段代码中，我们使用 Python 的 input() 函数接收两个数字。这两个数字被赋给两个变量 n1 和 n2。然后我们计算和、差、积和商，并将它们赋给 4 个不同的变量。最后，使用 print() 将这 4 个变量打印出来。

**输出：**

```text
num1: 9
num2: 3

The sum is 12.0
The difference is 6.0
The product is 27.0
The quotient is 3.0
```

## 取模运算

取模运算返回两个数字之间的余数。它看起来像百分号 %。下面是一个示例：

```python
n1 = float(input('num1: '))
n2 = float(input('num2: '))

remainder = n1 % n2
print()
print(f"Remainder is {remainder}")
```

上面的代码通过输入接收两个数字，并求出两者之间的余数；如下面的输出所示。

**输出：**

```text
num1: 9
num2: 2

Remainder is 1.0
```

9 除以 2 的余数确实是 1。

## random.random()

```python
import random

n1 = random.random()
n2 = round(random.random() * 50)
n3 = round(random.random() * 50)
n4 = round(random.random() * 1000)

print(f"Random number between 0 and 1 {n1}")
print(f"1st random number between 0 and 50 {n2}")
print(f"2nd random number between 0 and 50 {n3}")
print(f"Random number between 0 and 1000 {n4}")
```

random.random() 返回 0 到 1 之间的随机数。如果我们想获得 0 到 10 之间的随机数，就乘以 10 并对结果取整（使用 round()）。让我们看几个示例。

在上面的示例中，n1 是 0 到 1 之间的随机数。n2 和 n3 是 0 到 50 之间的两个不同随机数。你应该大概能看出 n2 和 n3 不同，因为这两个数字都是随机生成的。n4 返回 0 到 1000 之间的随机数。我们可以在下面的输出中看到结果。由于数字是随机生成的，每次运行程序时我们都应该得到不同的结果。random.random() 是一个有趣的函数，本书中我们将在不少游戏中使用它。

**输出：**

函数。基本上，在这些情况下，x 被提升到 y 的幂，n1、n2 和 n3 给出指数。n4 显示 100 的自然对数，n5 显示以 10 为底的 100 的对数。

**输出：**

```text
6 raised to the power 2 = 36
7 raised to the power 3 = 343
7 raised to the power 3 = 343
The natural logarithm of 100 is 4.605170185988092
Logarithm base 10 of 100 is 2.0
```

## 平方根

math.sqrt() 用于求平方根，abs() 用于求一个数的绝对值。

注意：你也可以使用运算符 ** 通过将数字提升到 0.5 次幂来求平方根。

下面是一些示例：

```python
import math

n1 = 36 ** 0.5
n2 = 75 ** 0.5
n3 = math.sqrt(75)
n4 = abs(13)
n5 = abs(-14)

print(f"The square root of 36 = {n1}")
print(f"The square root of 75 = {n2}")
print(f"The square root of 75 = {n3}")
print(f"The absolute value of 13 = {n4}")
print(f"The absolute value of -14 = {n5}")
```

在上面的代码中，n1、n2 和 n3 是平方根函数的示例；而 n4 和 n5 是绝对值函数的示例。

如果你没听说过绝对值函数，它基本上会返回一个正值，无论数字是正数还是负数。因此，13 和 -13 都会返回绝对值 13。

**输出：**

```text
The square root of 36 = 6.0
The square root of 75 = 8.660254037844387
The square root of 75 = 8.660254037844387
The absolute value of 13 = 13
The absolute value of -14 = 14
```

## 三角函数

是的，Python 也可以用于执行三角函数。下面是其中一些。`math.sin(x)` 返回 x 弧度的正弦值。如果我们想求 x 度的正弦值，就必须将其转换为弧度。因此，我们应该将函数改为 `math.sin(x*math.pi/180)`。另外请记住，在 Python 中，我们用 `math.pi` 表示 π 的值。我们还可以使用 `math.cos(x)` 和 `math.tan(x)` 执行 cos 和 tan 函数，其中 x 以弧度为单位。让我们看下面的示例程序：

```python
import math

n1 = math.sin(5)
n2 = math.sin(5 * math.pi/180)
n3 = math.sin(90 * math.pi/180)
n4 = math.cos(10)
n5 = math.cos(10 * math.pi/180)
n6 = math.cos(0 * math.pi/180)
n7 = math.tan(30)
n8 = math.tan(30 * math.pi/180)
n9 = math.tan(45 * math.pi/180)

print(f"The sine of 5 radians = {n1}")
print(f"The sine of 5 degrees = {n2}")
print(f"The sine of 90 degrees = {n3}")
print(f"The cosine of 10 radians = {n4}")
print(f"The cosine of 10 degrees = {n5}")
print(f"The cosine of 0 degrees = {n6}")
print(f"The tan of 30 radians = {n7}")
print(f"The tan of 30 degrees = {n8}")
print(f"The tan of 45 degrees = {n9}")
```

在上面的代码中，我们展示了 3 个正弦、余弦和正切值的示例。并且我们展示了计算角度和弧度的三角函数值之间的差异。例如，对于 n1，我们计算 sin(5 弧度) 的值，而在 n2 中我们计算 sin(5 度) 的值。在 n2 中，我们必须通过执行 sin(5 * π/180) 将 5 度转换为弧度。

**输出：**

```text
The sine of 5 radians = -0.9589242746631385
The sine of 5 degrees = 0.08715574274765817
The sine of 90 degrees = 1.0
The cosine of 10 radians = -0.8390715290764524
The cosine of 10 degrees = 0.984807753012208
The cosine of 0 degrees = 1.0
The tan of 30 radians = -6.405331196646276
The tan of 30 degrees = 0.5773502691896257
The tan of 45 degrees = 0.9999999999999999
```

## 练习题

- 1. 编写一个程序，计算员工的工资。该程序通过输入接收员工的时薪和他一个月工作的总小时数。不要忘记 input 函数输出的是字符串输入，你需要将输入解析为 float。使用 round 函数将工资四舍五入到 2 位小数。
- 2. 编写一个计算器，要求用户输入 2 个数字和计算操作符号 *、/、+、^、%、log、平方根、三角函数。注意其中一些操作只需要一个数字，因此请相应地修改程序行为。
- 3. 创建一个程序，在给定到建筑物的距离 D 和角度 α 的情况下计算建筑高度 H。

Python 有用于数字的类型 int 和 float。类似地，它有用于条件值 True 和 False 的类型 bool。Bool 以英国数学家 George Boole 命名，他创立了数学学科布尔代数，这是现代计算机科学的基础。

Bool 类型在 Python 中极其重要，因为它们用于评估条件语句。条件语句是根据某种条件改变程序行为的语句。

```python
print(type(True))
print(type(False))
print(type(true))
```

```text
<class 'bool'>
<class 'bool'>

------------------------------------------------------------
Traceback (most recent call last)
<ipython-input-34-5bfe175a5f35> in <module>
      1 print(type(True))
      2 print(type(False))
----> 3 print(type(true))

NameError: name 'true' is not defined
```

在这个代码片段中，我们打印出 True 和 False 的类型。请注意，True 与 true 不同，因为当尝试打印 true 而不是 True 的类型时，代码会输出错误。布尔表达式是求值为 True 或 False 的表达式。我们使用比较运算符编写布尔表达式。

## 比较运算符

| 运算符 | 名称 | 描述 | 示例 | 返回值 |
|---|---|---|---|---|
| `==` | 相等 | 如果数字相等则返回 True，否则返回 False。 | `5 == 9` | False |
| `!=` | 不相等 | 如果数字不相等则返回 True，否则返回 False。 | `5 != 9` | True |
| `>` | 大于 | 如果 n1 > n2 则返回 True，否则返回 False | `10 > 1` | True |
| `>=` | 大于或等于 | 如果 n1 >= n2 则返回 True，否则返回 False | `10 >= 10` | True |
| `<` | 小于 | 如果 n1 < n2 则返回 True，否则返回 False | `5 < 10` | True |
| `<=` | 小于或等于 | 如果 n1 <= n2 则返回 True，否则返回 False | `1 <= 2` | True |

## 逻辑运算符

Python 有三个逻辑运算符 and、or 和 not。它们各自的作用与其直观含义相似
