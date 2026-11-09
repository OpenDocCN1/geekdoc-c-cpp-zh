
通过输入 `cd "folder address"` 进入你的 Python 文件所在的文件夹。如果你的文件在桌面上，那么

***输入 `cd C:\Users\USER_NAME\Desktop`***

![](img/443990a0ec620659ce8be783c0758bc6_510_0.png)

USER_NAME 取决于你桌面上的用户名，每台计算机都不相同。

![](img/443990a0ec620659ce8be783c0758bc6_510_1.png)

要运行程序，请输入 `python "program_name"`，例如程序名为 run.py。

![](img/443990a0ec620659ce8be783c0758bc6_511_0.png)

然后输入 **python "run.py"**

恭喜，现在你的第一个程序已经成功运行了。

## 变量

### 变量简介

可以将变量看作一个用于保存某个值的容器。变量是内存中保存某个值的位置。在 C、C++ 等静态类型编程语言中，必须事先声明变量类型，并且之后变量类型不能改变。这就是为什么我们要先声明变量并指定其值类型，然后再为变量赋值。

下面是在静态类型语言中声明和赋值变量的示例。

```c
int var;    // Variable declaration of type integer.
var = 8;    // Variable assignment to 8.
```

但由于 Python 是动态类型的，你不必先声明变量类型；它会自动为你推断出变量类型。要定义变量，只需使用等号将值赋给变量名。这被称为赋值运算符。下面的代码将三个变量分别赋值为字符串、整数和浮点数。

```python
# variables

lang = "python"
num1 = 2
num2 = 3.4

print(lang)
print(num1)
print(num2)
print('\n')

print(type(lang))
print(type(num1))
print(type(num2))
```

**输出：**

```text
python
2
3.4

<class 'str'>
<class 'int'>
<class 'float'>
```

可以看到，每个变量无需显式定义就具有了类型。字符串变量可以用单引号或双引号声明。我们也可以在一行内定义多个变量，例如 `var1, var2, var3 = 1, 2, 3`。

```python
x, y, z = 1, 2, 3
print(x, y, z)
```

**输出：**

1 2 3

### 变量命名规则

在 Python 中，变量名需要遵循一些规则。这些规则如下：

- 1. 变量名必须以字母或下划线“_”开头。
- 2. 变量名必须由字母或数字组成；不允许使用特殊字符。
- 3. 变量名区分大小写；A 和 a 是不同的变量。

不同变量名的示例。

```python
num = 1
NUM = 2
_2num = 3
num2 = 4
num2_ = 5

print(num, NUM, _2num, num2, num2_)
```

1 2 3 4 5

请注意，在上面的代码片段中，变量名被赋予了有含义的名称。这在编程中非常重要，因为它使程序易于阅读。

### 全局变量与局部变量

在函数外部创建的变量可以被任何函数访问，它们被称为全局变量。全局变量可以被任何函数访问。局部变量是在函数内部定义的变量，无法从函数作用域外部访问。

在下面的代码中，变量“lang”是全局变量，因此 `func()` 函数可以访问它。调用 `func()` 时输出为 Python。

```python
# this variable is global to this scope
lang = "Python"

def func():
    print(lang)

func()
```

Python

```python
# this variable is global to this scope
lang = "Python"

def func():
    # this variable is local to this function
    lang = "C++"
    print(lang)

func()
print(lang)
```

C++

Python

类似地，这里的“lang”变量是全局变量，但同时我们也有一个名为 `lang` 且值等于 C++ 的变量。调用 `func()` 时输出为 C++，因为 `func` 内部的局部变量优先于 `func` 外部的全局变量。然而，当我们打印变量 `lang` 时，发现全局变量并没有改变。这是因为即使我们在 `func` 内外都有 `lang` 变量，它们的作用域是分开的，彼此不会干扰或覆盖。

### 赋值运算符

赋值运算符用于在 Python 中给变量赋值。它们也用于操作和更新变量值。下表展示了赋值运算符及其名称。这些运算符用作其等价形式的简写。

| 运算符 | 名称 | 示例 | 等价形式 |
|---|---|---|---|
| `=` | 赋值运算符 | `j = 2` | `j = 2` |
| `+=` | 加法赋值 | `j += 2` | `j = j + 2` |
| `-=` | 减法赋值 | `j -= 2` | `j = j - 2` |
| `*=` | 乘法赋值 | `j *= 2` | `j = j * 2` |
| `/=` | 除法赋值 | `j /= 2` | `j = j / 2` |
| `%=` | 取模赋值 | `j %= 2` | `j = j % 2` |
| `**=` | 幂赋值 | `j **= 2` | `j = j ** 2` |

```python
a, b, c, d, e, f = 1, 1, 1, 1, 1, 1

a += 2

b -= 2

c *= 2

d /= 2

e %= 2

f **= 2

print("a is ", a)
print("b is ", b)
print("c is ", c)
print("d is ", d)
print("e is ", e)
print("f is ", f)

# Output:
# a is 3
# b is -1
# c is 2
# d is 0.5
# e is 1
# f is 1
```

下面的脚本在第 1 行将变量 a、b、c、d、e、f 都赋值为 1。然后使用赋值运算符更新变量值。请查看输出以理解赋值运算符的工作方式。

### 字符串方法

Python 最强大的特性之一是它开箱即用地提供了强大的函数，无需你重新实现。Python 中的字符串方法非常灵活且功能强大，让你不必花费时间从头实现它们。你可以轻松地使用它们来操作字符串。在本节中，我们将学习一些 Python 字符串方法。

下面是一些常见的 Python 字符串方法列表。

- 字符串拼接：只需使用 `+` 运算符即可将两个字符串拼接在一起。

    ```python
    A = "Hello"
    B = "World"
    A + B  # returns "Hello World"
    ```

    另外，将字符串乘以任意数字 `n` 会将该字符串重复 `n` 次。

    ```python
    A = 5 * "hi"
    A  # returns "hihihihihi"
    ```

- `len(str)` – 长度函数，返回字符串的字符数。

    `len("python is amazing")` 返回 17。请注意，`len` 也会计算空格！

- `str[index]` – 索引运算符，从字符串中选择单个字符。方括号中的数字称为索引，它是一个整数值。Python 中的索引从零开始。

    ```python
    a = "Python"
    a[0]  # value is "P"
    a[5]  # value is "n"
    ```

    你还可以使用负索引，它将从最后一个字符开始向前索引。

    ```python
    a[-1]  # value is "n"
    a[-2]  # value is "o"
    ```

- `str[starting_index: ending_index]` – 切片运算符，从起始索引开始切片，并在结束索引之前一个字符处结束。

    ```python
    a = "Programming is amazing"
    a[0:11]  # value is "Programming"
    a[15:19]  # value is "amaz"
    ```

- `in` – `in` 运算符，如果字符在字符串中则返回 `True`。

    ```python
    lang = "language"
    "a" in lang  # returns True
    ```

- `str.split(char)` — 按字符 `char` 将字符串拆分为字符串列表。

    ```python
    langs = "Python,C++,C"
    langs.split(",")  # returns ['Python', 'C++', 'C']
    ```

- `str.replace(oldval, newval)` – 将字符串 `str` 中的 `oldval` 替换为 `newval`。

    ```python
    A = "Python is powerful"
    A.replace("Python", "C++")  # returns 'C++ is powerful'
    ```

- f-string — 是一种格式化字符串和变量的简便方式；它们易于使用且速度更快。

    ```python
    n = 7
    print("number is ", n)  # outputs "number is 7"
    print(f"number is {n}")  # outputs "number is 7"
    ```

- `str.capitalize()` – 将字符串的首字母大写；如果首字母已大写，则返回原字符串。

    ```python
    sent = "message was sent"
    sent.capitalize()  # returns "Message was sent"
    ```

- `str.count(substring)` – 返回子字符串在 `str` 中出现的次数。

    ```python
    mess = "Life is beautiful"
    mess.count('is')  # returns 1
    ```

- `str.isalnum()` – 如果字符串是字母数字组合（即字母和/或数字的组合），则返回 `True`。

    ```python
    a = 'door2'
    b = 'door'
    c = 'door#$'

    a.isalnum()  # returns True
    b.isalnum()  # returns True
    c.isalnum()  # returns False
    ```

- `str.isalpha()` – 如果字符串中的所有字符都是字母，则返回 `True`。

    ```python
    a = 'door1'
    a.isalpha()  # returns False
    ```

- `str.isdigit()` – 如果 `str` 只包含数字，则返回 `True`。

    ```python
    n = '324235'
    m = 'd4ds'

    n.isdigit()  # returns True
    m.isdigit()  # returns False
    ```

- `str.islower()` – 如果字符串字符全部为小写，则返回 `True`。

    ```python
    s = "People"
    s.islower()  # returns False
    ```

- `str.isupper()` – 如果字符串字符全部为大写，则返回 `True`。

    ```python
    S = "ALL"
    S.isupper()  # returns True
    ```

