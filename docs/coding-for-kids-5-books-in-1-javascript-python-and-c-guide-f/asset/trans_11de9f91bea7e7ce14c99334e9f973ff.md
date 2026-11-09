
Python 也提供了字符串比较运算符，就像你可以使用 ==、>、< 等比较数字一样。你也可以使用相同的运算符比较字符串。

| 运算符 | 名称 | 描述 | 示例 | 返回值 |
|---|---|---|---|---|
| `==` | 相等 | 如果字符串相等则返回 True，否则返回 False。 | "Python" == "c++" | False |
| `!=` | 不相等 | 如果字符串不相等则返回 True，否则返回 False。 | "Python" != "c++" | True |
| `>` | 大于 | 如果 len(str1) > len(str2) 则返回 True，否则返回 False | "Python" > "c++" | True |
| `>=` | 大于或等于 | 如果 len(str1) >= len(str2) 则返回 True，否则返回 False | "Python" >= "Python" | True |
| `<` | 小于 | 如果 len(str1) < len(str2) 则返回 True，否则返回 False | "Python" < "c++" | False |
| `<=` | 小于或等于 | 如果 len(str1) <= len(str2) 则返回 True，否则返回 False | "Python" <= "c++" | False |

### 示例 1：字符串方法

下面的脚本使用了我们学过的字符串方法，对字符串执行有趣的操作。这个程序通过 input 函数获取用户名，并对用户名执行有趣的字符串方法。代码中有注释。请阅读并研究代码。理解代码后，尝试修改它。

```python
name = "Nick John"

a = len(name)
index0 = name[0]
indexneg = name[-1]
index0_4 = name[0:4]

# Using f-string to concatenate sentences
job = f"{name} is an Engineer!"
print("using f-string output is", job)

#slicing and indexing
print(f"name length is: {a}")
print(f"name index 0 is {index0}")
print(f"name index -1 is {indexneg}")
print(f"name slice [0:4] is {index0_4}")

# in operation, split, replace, capitalize
is_in = "Nick" in name
print(f"\"Nick\" in name returns {is_in}")
splited = name.split()
print(f"name.split() returns {splited}")
name = name.replace("Nick", "Biden")
print(f"Nick John after replacing with name.replace() is {name}")
print(f"{name} capitalized is {'james'.capitalize()}")
```

```python
# count, isalnum, isalpha, isdigit
name = "Obama Jame"
count = name.count("Nick")
print(f"Nick occurs {count} times in \'{name}\'")

non_alphanum = "eoe12#"
non_alpha = "23"
digit = '223'

print(f"{non_alphanum} is alphanumeric is {non_alphanum.isalnum()}")
print(f"{non_alpha} is alphabetical is {non_alpha.isalpha()}")
print(f"{digit} is only digits {digit.isdigit()}")
```

**输出：**

```python
name = input("Enter your name: ")

n = len(name)
print("The length of your name is ", n)
print()
for char in name :
    print(char,end=".")

print()
print("The reverse is")

for i in range(1, n+1):
    print(name[-i], end=".")
```

```text
Enter your name: James Bond
The length of your name is  10

J.a.m.e.s. .B.o.n.d.
The reverse is
d.n.o.B. .s.e.m.a.J.
```

### 示例 3 – 元音计数器程序

这个程序统计字符串中的元音。它首先将 count 初始化为零，然后将所有文本字符转换为小写，以便我们可以将文本字符与小写元音字符进行比较。然后遍历文本中的字符，检查 char 是否在 vowels 中，如果为真，count 就加一。

```python
vowels = 'aeiou'

# returns the count of vowels in text
def count_vowels(text):
    count = 0
    # convert text to all lowercase so it compares correctly
    # to vowels
    text = text.lower()
    for char in text:
        if char in vowels:
            count += 1
    return count

text = "Learning programming is amazing tool to learn"
count = count_vowels(text)
print(f"There are {count} vowels in text.")
```

文本中有 15 个元音。

### 示例 4 – 从文本中移除负面词汇

这个程序首先使用 str.split() 将单词拆分，然后遍历这些单词。

str.split() 按空格将 negative_words 拆分成单词。例如 "I like CS".split() 返回 ["I", "like", "CS"]。block 函数遍历 negative_words 列表，如果任何单词出现在文本中，我们就用与负面单词长度匹配的星号字符串替换该单词。

```python
# replace all instances negative words with stars matching the length of these words

negative_words = "bad kill haters"

def block(text):
    # split words into list of words
    for negative in negative_words.split():
        if negative in text:
            text = text.replace(negative, len(negative)*'*')
    return text

text = "haters kill love"
blocked_text = block(text)

print(f"Original text : {text}")
print(f"Blocked text : {blocked_text}")
```

```text
Original text : haters kill love
Blocked text : ****** **** love
```

### 练习题

- 1. 回文是一个正读和反读都相同的单词，例如 Civic、Level、Mom、Noon 和 radar。编写一个程序，如果短语是回文则返回 true。
- 2. 编写一个程序，打印给定文本中有多少个单字符重复。
- 3. 编写一个程序，生成随机 n 长度的字母数字密码。
- 4. 编写一个程序，将给定字符串中的逗号替换为点，例如将 "32,323,23" 替换为 "32.323.23"
- 5. 编写一个程序，计算字符串中数字的和，例如 "452" 的数字之和为 11。

## 用 Python 做数学

Python 是一种非常适合执行和分析用户数据的编程语言。我们将介绍几个帮助你熟悉 Python 的函数。现在，这一节并不适合所有人。它适合那些有兴趣在程序中实现数学运算的人，或者喜欢数学并希望看到它在 Python 中实现的人。有些概念在高中教授，所以这一节可能不适合年龄较小的学生。

### int/float

- **int** — 接收字符串变量并返回一个整数；如果传入浮点数，则返回浮点数的整数部分。
- **float** — 接收字符串变量并将其转换为浮点数。

让我们看下面的示例。

在这个示例中，我们将 3 个数字分别传给 int 和 float，并查看输出。

**输出：**

```python
x1 = int(5.2)
y1 = int(5)
z1 = int("5")
xf = float("5.2")
yf = float(5.01)
zf = float(5)

print(f"x1 is {x1} and it's type is {type(x1)}")
print(f"y1 is {y1} and it's type is {type(y1)}")
print(f"z1 is {z1} and it's type is {type(z1)}")
print(f"xf is {xf} and it's type is {type(xf)}")
print(f"yf is {yf} and it's type is {type(yf)}")
print(f"zf is {zf} and it's type is {type(zf)}")
```

```text
x1 is 5 and it's type is <class 'int'>
y1 is 5 and it's type is <class 'int'>
z1 is 5 and it's type is <class 'int'>
xf is 5.2 and it's type is <class 'float'>
yf is 5.01 and it's type is <class 'float'>
zf is 5.0 and it's type is <class 'float'>
```

我们可以从输出中看到 int 和 float 之间的区别。我们可以看到，将字符串传给 int，即把 "5" 传给 int 函数，会返回 int 类型。类似地，float 函数接收浮点数字符串，即 "5.2"，并返回浮点数。注意 "5" 和 "5.2" 是字符串，因为它们带有引号。如果不使用 int 或 float 将它们转换为数字，我们就不能在数学运算中使用它们。

我们还注意到，对于所有值，int 都会去掉小数部分并保留整数部分。它不会向上或向下舍入，只是去掉小数部分。float 会保留小数部分。因此，使用 float 将字符串中的十进制数字转换为实际的浮点数。

### 数字舍入 – math.ceil()、math.floor() 和 round()

Python 有一个名为 math 的内置库，它包含各种有用的数学函数。

要在 Python 中访问一个库，你必须先导入它，这样主程序才能访问库函数。

接下来，我们讨论数字舍入。我们使用 math.ceil()、math.floor() 和 round() 函数。math.ceil() 舍入到大于该小数的第一个整数，math.floor() 舍入到小于该小数的第一个整数，而 round() 舍入到最接近的整数（无论更大还是更小）。让我们看一个示例程序。

```python
# import the library
import math

xc = math.ceil(5.2)
yc = math.ceil(7.8)
zc = math.ceil(4.5)

xf = math.floor(5.2)
yf = math.floor(7.8)
zf = math.floor(4.5)

xr = round(5.2)
yr = round(7.8)
zr = round(4.5)

print(f"Example of math.ceil()")
print(f"xc is {xc}")
print(f"yc is {yc}")
print(f"zc is {zc}")
print()
print(f"Example of math.floor()")
print(f"xf is {xf}")
print(f"yf is {yf}")
print(f"zf is {zf}")
print()
print(f"Example of round()")
print(f"xr is {xr}")
print(f"yr is {yr}")
print(f"zr is {zr}")
```
