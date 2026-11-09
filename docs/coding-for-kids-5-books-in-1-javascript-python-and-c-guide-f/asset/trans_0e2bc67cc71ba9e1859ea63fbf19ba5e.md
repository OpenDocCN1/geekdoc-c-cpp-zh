

含义。下面的真值表准确描述了它们的作用。

| X | Y | 非 X | X 或 Y | X 且 Y |
|---|---|---|---|---|
| 真 | 真 | 假 | 真 | 真 |
| 真 | 假 | 假 | 真 | 假 |
| 假 | 真 | 真 | 真 | 假 |
| 假 | 假 | 真 | 假 | 假 |

## 示例 1：比较运算符和逻辑运算符

以下代码片段展示了使用比较运算符和逻辑运算符的一些示例。

```python
# comparison operators

x = 0
y = 10

# number comparisons
print("y == x is", y == x)
print("y > x is", y > x)
print("y < x is", y < x)
print("y <= x is", y <= x)

print()

# logical operators
print("(not True) is", not True)
print("(True and True) is", True and True)
print("(True and False) is", True and False)
print("(True or False) is", True or False)
print("(False or False) is", False or False)

# Output:
y == x is False
y > x is True
y < x is False
y <= x is False

(not True) is False
(True and True) is True
(True and False) is False
(True or False) is True
(False or False) is False
```

## 条件语句

### if 条件语句

条件语句让程序变得智能。计算机能够做出决策，使程序根据某个求值为 True 或 False 的布尔表达式改变其行为。最简单的 if 条件语句形式是：

```python
if expression:
    statement
```

其中，仅当 expression 求值为 True 时才执行 statement。注意，语句必须在 if 语句下方缩进。缩进的空间称为块。

### if else 条件语句

if else 与 if 条件语句非常相似，区别在于我们有一个 else 块，当 expression 为 False 时执行。

```python
if expression:
    statement1
else:
    statement2
```

现在我们有 2 个分支，第一个分支是语句 1，第二个分支是语句 2。程序将执行与逻辑表达式求值结果相对应的分支。可以把分支想象成一条分岔成不同道路的路。

### if elif else 条件语句

如果我们想要多个分支而不是只有两个分支，该怎么办？if elif else 条件语句也称为链式条件语句。在链式条件语句中，只会执行一个分支。elif 代表 else if。根据程序逻辑需要，我们可以有任意数量的 elif 语句。

首先，对 if 的 expression 求值。如果它求值为 False，则程序继续求值属于第一个 elif 的 expression2。程序会持续求值每个表达式，直到某个表达式求值为 True，并执行相应的语句/块。如果所有表达式都求值为 False，则执行 else 块。

```python
if expression:
    statement1
elif expression2:
    statement2
elif expression2:
    statement3
else:
```

### 嵌套条件语句

如果我们想在其他分支内部创建分支，该怎么办？我们可以将 if 条件语句嵌套在其他 if 条件语句中。这称为嵌套条件语句。请记住，过多嵌套条件语句通常会使程序难以阅读，因此仅当你无法使用逻辑运算符的组合来表达程序逻辑时才使用它们。

```python
if expression:
    if expression1:
        statement1
    else:
        statement2
else:
    statement3
```

在这个代码片段中，使用 “and” 逻辑运算符将嵌套条件语句简化为扁平化的 if 条件语句。可以看到，第二个 if 条件语句更易于阅读。

```python
x = -1
y = 5

# nested conditional
if x < 0:
    if y < 10:
        print("nested conditional: x < 0 and y < 10")

print()
# Equivalent version using and
if x < 0 and y < 10:
    print("and version conditional: x < 0 and y < 10")
```

nested conditional: x < 0 and y < 10

and version conditional: x < 0 and y < 10

## 示例 2：条件语句：

在这个程序中，我们首先使用简单的 if 条件语句检查 x 是否为正数。使用 if else 条件语句检查 y 是正数还是负数。注意，当 y 为零时有一个未检查的边界情况，因此我们使用 if elif else 检查 z 是正数、负数还是零。

```python
# simple if case
x = 5
y = -3
z = 0

# only check for positivity
if x > 0:
    print("x is positive number !")

print()

# Check if number is positive or negative using if else
if y > 0:
    print("y is positive number !")
else:
    print("y is positive number !")

print()

# Check if number is positive, negative or zero using if elif else
if z > 0:
    print("z is positive number !")
elif z < 0:
    print("z is positive number !")
else:
    print("z is zero !", z)
```

x is positive number !  
y is positive number !  
z is zero ! 0

## 函数

函数是一段可复用的代码块，在被调用时执行特定任务。可以把它们想象成一台机器/黑箱，接收输入并将其转换为输出。每次调用时都会运行这个黑箱。函数有助于将代码拆分成简单、易维护、可复用的模块。事实上，你在本书中一直不知不觉地使用函数。例如，print() 是一个接收字符串输入并将其显示在屏幕上的函数。此外，你在上一章学到的字符串方法也是操作字符串的函数。

表示平方函数的黑箱

![](img/443990a0ec620659ce8be783c0758bc6_557_0.png)

### 函数定义

在 Python 中，使用 def 关键字定义函数。

```python
def function_name(input_parameters):
    statements
```

要调用函数，请输入函数名并带上输入参数。

```python
function_name(input_parameters)
```

在下面的代码中，我们定义了一个按名字向用户问候的函数。它接收一个输入（名字），并向该用户名打印 hello。

```python
# function example
my_name = 'Jame'

# say hello to name
def hello(name):
    print("Hello !", name)

# function call
hello(my_name)
```

Hello ! Jame

### return 语句

在之前的脚本中，我们在 hello 函数内部运行了 print 函数，但如果我们需要只向调用者返回一个值，该怎么办？

在这个代码片段中，hello 函数返回一个字符串。首先调用 hello 函数，并将返回的值存储在赋值的变量中。

```python
# function example
my_name = 'Jame'

# return hello to name
def hello(name):
    return "Hello !" + name

# function call
returned_name = hello(my_name)
print(returned_name)
```

Hello !Jame

### 空 return

当函数的 return 语句为空时，它会终止函数运行并返回 None。

在这个示例中，调用 func 时它只执行第 4 行，因为当它到达第 5 行的 return 语句时就会终止。另外请注意，它返回 None。

```python
# None return

def func():
    print("Before return nothing")
    return
    print("After return nothing")

m = func()
print()
print("func returned ", m)

# Output:
# before return nothing
#
# func returned  None
```

值。

## 示例 3：is divisible

在这个示例中，is_divisible 函数检查 a 是否能被 b 整除；如果可以，它会打印一条消息并将 div 设为 true。如果 a 不能被 b 整除，else 语句将处理这种情况，打印一条消息并将 div 设为 false。

```python
# is_divisible
# checks if a is divisible by b, print a message
# return true else false

def is_divisible(a, b):
    div = None
    if a % b == 0:
        print(f"{a} is divisible by {b}")
        div = True
    else:
        print(f"{a} is not divisible by {b}")
        div = False

    return div

n1 = is_divisible(8, 2)
n2 = is_divisible(8, 3)

print(n1)
print(n2)
```

```
8 is divisible by 2
8 is not divisible by 3
True
False
```

## 练习题

- 1. 编写一个程序，找出 1 到 5000 之间能被 11 整除的数。
- 2. 编写一个函数，测试一个数是否为质数。质数是只能被自身和 1 整除的数。
- 3. 编写一个函数，测试一个数是否为奇数。

## 循环

编程中的循环是一系列会重复一定次数的指令。可以把循环想象成一种重复操作，它会一直重复，直到满足某个条件。根据执行条件，循环主要分为 2 种类型。它们是：

- a. **FOR 循环：** FOR 循环包含一系列会执行一定次数的指令。例如，从 1 到 10 的 FOR 循环会将循环内的代码执行 10 次。
- b. **WHILE 循环：** WHILE 循环是一系列会一直执行直到满足某个条件的指令。

现在，如果我们想要执行 execute 函数 1000 次，就使用 FOR 循环。下面的 FOR 循环从 0 开始，到 999 结束，因此会运行 execute 函数 1000 次。

```python
for i in range(1000):
```

