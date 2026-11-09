
## 嵌套条件语句

当我们希望检查多个条件时，使用关键字“and”和“or”会使代码难以阅读，因此我们使用嵌套条件语句。嵌套条件语句就是在 if、elif 或 else 块内部的 if..else 块。下面是一般语法：

```
if *condition is True*:
    if *condition is True*:
        ...... execute this code block .......
    elif *condition is True*:
        ...... execute this code block .......
    else:
        ...... execute this code block .......
else:
        ...... execute this code block .......
```

### 示例

在这个示例中，我们将接收一个4位年份作为输入，并检查它是否为闰年。现在，这比我们想象的要稍微复杂一些。我们知道每4年是一个闰年。所以这是我们的第一项检查。因此，像1996年这样的年份就是闰年。但是，每100年没有闰年。所以，1800年和1900年不是闰年。此外，还有另一个例外。每400年，它是闰年。所以，1600年和2000年是闰年。因此，共有3项检查。

```python
def check_leap(year):
    year = int(year)
    leap = False
    if year % 4 == 0:
        leap = True
        if year % 100 == 0:
            leap = False
            if year % 400 == 0:
                leap = True
    return leap

year = input("Enter the year ")

if check_leap(year):
    print("It is a leap year")
else:
    print("It is not a leap year")
```

函数 check_leap 接收年份作为参数，并根据条件返回 True 或 False。首先，我们声明一个布尔变量“leap”，并将其初始设为 False。然后我们执行以下检查：

- 如果年份能被4整除，我们将 leap 设为 True 并返回 True。然后进入第二个循环，检查它是否能被100整除。
  - 如果年份能被100整除，我们将 leap 设为 False，因为该年份可能不是闰年。如果它能同时被4和100整除，我们进入第三个循环，检查它是否能被400整除。
    - 如果年份能被400整除，它一定是闰年，因此我们将 leap 设为 True 并返回 True。
    - 如果年份不能被400整除，但能被100整除，则它不是闰年。我们将 leap 设为 False 并返回 False。
  - 如果年份不能被100整除，我们返回 True。
- 如果年份不能被4整除，我们将其设为 False，因为闰年必须能被4整除，并返回 False。

我们从用户那里接收年份作为输入，调用该函数并将输入作为参数传入，然后检查返回值是 true 还是 false。

- 如果 check_leap 返回 True，则该年份是闰年，我们打印“It is a leap year”。
- 如果 check_leap 返回 False，则该年份不是闰年，我们打印“It is not a leap year”。

以下是代码的几次执行：

```text
Enter the year? 1992
It is a leap year
>>>
Enter the year? 1995
It is not a leap year
>>>
Enter the year? 1900
It is not a leap year
>>>

Enter the year? 2000
It is a leap year
>>>
```

从上面的代码和结果可以看出，它使用3个嵌套的 IF 语句准确计算了闰年。

- 1992 年是闰年，因为它能被4整除。
- 1995 年不是闰年，因为它不能被4整除。
- 1900 年不是闰年，因为它既能被100整除，也能被4整除；但不能被400整除。
- 2000 年是闰年，因为它能被4、100和400整除。

### 练习

- 1. 编写一个程序，接收用户输入的降雪英寸数、结冰英寸数以及是否有盐。检查是否应宣布雪假。如果积雪超过15英寸，就是雪假。但是，如果有盐，则不放假。如果冰和雪同时存在，则无论是否有盐，都宣布雪假。
- 2) 编写一个程序，接收电视节目时间、电视节目类型以及父母是否在场。检查孩子们是否可以看电视。孩子们可以在下午6:00到7:00之间的任何时间看电视。7点之后，必须检查电视节目的分级。如果是面向普通观众，且在晚上10点之前，他们可以看电视。如果是面向成人观众，在晚上10点之前且有父母在场，他们可以观看。但是，如果父母不在场，他们就不能观看。晚上10点之后，无论分级如何、父母是否在场，他们都不能看电视。

## 作者短讯：

嘿，你喜欢这本书吗？我很想听听你的想法！

许多读者并不知道获得评价有多难，也不知道评价对作者有多大帮助。

![](img/443990a0ec620659ce8be783c0758bc6_452_0.png)

如果你能只花60秒在 Amazon 上写一段简短评价，哪怕只有几句话，我也会非常感激！

[>> 点击此处留下快速评价](#)

感谢你抽出时间分享你的想法！

你的评价会真正对我产生影响，并帮助我的作品获得曝光。

## 循环

Python 中的循环用于我们希望重复执行某段代码的情况。我们通常为代码块的重复设置条件，只要条件满足，代码块就会重复执行。一旦条件不再满足，循环就会结束，代码块也不再重复执行。

Python 有两种循环：

- 1. for 循环
- 2. while 循环

### FOR 循环

当我们知道希望循环执行多少次时，就使用 FOR 循环。for 循环也用于数组，这将在下一章讨论。下面是将代码块重复10次的 for 循环语法。

```
for i in range(0,10):
    ........ block of code ........
```

在上面的代码中，变量“i”最初被设为0，并且每次执行代码块时，“i”都会递增1。在执行代码块之前，会进行检查：如果“i”小于10，则执行循环；如果“i”大于或等于10，则不执行循环，Python 开始执行循环外的代码。一般来说，变量最初被设为 range 中的第一个参数，并在每次执行循环时递增1，直到其值达到第二个参数。

```
for i in range(0,10):
    print(i)
```

在上面的代码中，我们在循环的每次执行期间打印变量“i”的值。下面是输出：

```
0
1
2
3
4
5
6
7
8
9
>>>
```

在“i”=9之后，“i”递增到10，并且由于“i”不再小于10，我们退出循环。

#### 示例 1

我们将编写一个程序，从用户那里接收一个整数作为输入，并返回0到该数字之间所有偶数的和。

```python
def sum_even(number):
    number = int(number)
    sum = 0
    for i in range(0,number):
        if i%2 == 0:
            sum = sum + i
    return sum

number = input("Please input the number? ")
print(sum_even(number))
```

函数 sum_even 接收一个数字作为参数，并返回截至该数字（不包括该数字）的所有偶数之和。执行以下步骤：

- 1. 我们将变量“sum”设为0
- 2. 创建一个循环，从“i”=0开始，一直到“i”等于用户输入的数字，每次递增1
- 3. 在循环内部执行检查，以判断“i”是否为偶数
- 4. 如果“i”是偶数，我们将“sum”的值更新为“sum”+i
- 5. 一旦 i 等于输入的数字，我们就退出循环并返回 sum。

以下是输入为10时的输出

```text
Please input the number? 10
20
>>>
```

0到10之间的偶数是2、4、6、8，且2+4+6+8=20。

以下是输入为20时的输出

```
Please input the number? 20
90
>>>
```

0到20之间的偶数是2、4、6、8、10、12、14、16、18，且2+4+6+8+10+12+14+16+18=90。因此，我们的代码按预期工作。

#### 示例 2

我们将编写一个函数，用于打印一个用星号（*）填充的 $n \times n$ 正方形。

```python
def print_square(number):
    n = int(number)
    for row in range(n):
        for col in range(n):
            print("*",end='')
        print('')

number = input("Please enter the value of n:")
print_square(number)
```

函数 print_square 接收一个数字作为参数，并打印一个用 * 填充的 $n \times n$ 正方形。

- 1. 首先，我们需要一个循环来遍历正方形的每一行，这个迭代器称为“row”，从0到n-1。

