
```python
def minmax(l):
    minimum = l[0]
    maximum = l[0]
    for x in l:
        if x < minimum: minimum = x
        if x > maximum: maximum = x
    print('Minimum is ' + str(minimum))
    print('Maximum is ' + str(maximum))
```

这个函数有一个微小的低效率问题：它查看了列表第一个元素两次。你能修复它吗？

## 4

我们需要一个步长为2的值，并且起始和结束值要涵盖整个列表：

```python
def evens(l):
    return l[0:len(l) + 1:2]
```

当然，这样的起始和结束值是默认的，所以我们也可以写：

```python
def reverse(l):
    return l[::1]
```

## 5

我们遵循上面第二个较短的 `evens` 函数的模式，简单地写道：

```python
def evens(l):
    return l[::2]
```

## 6

我们首先创建一个新的空列表。然后，对于原始列表中的每个元素，我们将其添加到新列表中，除非它已经存在于：

```python
def setify(l):
    l2 = []
    for x in l:
        if x not in l2: l2.append(x)
    return l2
```

## 7

我们使用 `setify` 函数来创建一个包含原始列表中唯一项的新列表。然后我们遍历这个新列表，使用 `count` 方法找到每个元素在原始列表中的次数，并将其打印。

```python
def histogram(l):
    unique = setify(l)
    for x in unique:
        print(str(x) + ' appears ' + str(l.count(x)) + ' times.')
```

## 8

这是一个关于 `in` 和布尔运算符的简单练习：

```python
def contains_all(s, a, b, c):
    return a in s and b in s and c in s
```

## 9

我们创建一个新的空列表，并逐个添加原始列表的元素：

```python
def copy_list(l):
    l2 = []
    for x in l: l2.append(x)
    return l2
```

或者，我们可以使用带有空起始和结束值的切片运算符：

```python
def copy_list(l):
    return l[::]
```

## 10

我们使用新的 `copy_list` 函数创建一个新列表，删除该值并返回该新列表：

```python
def remove_copy(l, x):
    l2 = copy_list(l)
    l2.remove(x)
    return l2
```

## 11

我们扩大字母表并使用列表切片写一个 `rotate` 函数，它可以将字符串旋转 1 到 25 个任意位置，并返回新字符串：

```python
alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
```

```python
def rotate(n, a):
    return a[n:] + a[:n]
```

现在我们的编码和解码函数变得简单，接收要编码或解码的文本以及旋转后的密文。正如你预期的那样，它们具有某种对称性：

```python
def encode(text, cipher):
    out = ''
    for x in text:
        if x == ' '; out = out + ' '
        else: out = out + cipher[alphabet.index(x)]
```

```python
def decode(text, cipher):
    out = ''
    for x in text:
        if x == ' '; out = out + ' '
        else: out = out + alphabet[cipher.index(x)]
    return out
```

我们记得特殊处理空格。

## 12

现在我们了解了 Python 列表，我们可以抛弃之前摩斯密码解决方案中巨大的结构，从两个列表开始工作：字母及其代码：

letters = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0']

codes = ['-', '.', '--', '...', '...', '...', '...', '...', '...', '...', '...', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-', '-']

现在修改我们之前的解决方案，使用列表的 `index` 方法在列表中查找代码就变得简单了：

```python
def print_morse_letter(l):
    if l not in letters: print('bad letter')
    else: print(codes[letters.index(l)], end=' ')
```

```python
def print_morse(s):
    for l in s:
        if l == ' ': print(' ', end='')
        else: print_morse_letter(l)
print('')
```

## 13

首先，我们将写一个函数来查看单个猜测，计算有多少个 a) 正确位置上的正确数字 b) 错误位置上的正确数字。这异常地微妙，因为我们必须确保不重复计算任何内容——例如，如果代码是 1441 而猜测是 4444，我们应该识别出两个 4 是正确位置上的正确数字，另外两个 4 不能被识别为错误位置上的正确数字，因为我们已经用了正确位置上所有的 4。

我们的函数将使用两个包含四个数字的列表，代码和猜测。我们复制它们，因为我们将更改列表中的值以标记它们为已用。然后我们设置两个计数器，以跟踪有多少数字是正确且在正确位置的，或者是正确但在错误位置的。

```python
import random

def check_code_guess(code, guess):
    code = code.copy()
    guess = guess.copy()
    correct = 0
    correct_place = 0
    for x in range(0, 4):
        if guess[x] == code[x]:
            correct = correct + 1
            code[x] = -1
    for x in range(0, 4):
        if guess[x] > -1:
            # (logic继续)
            pass
```

```python
def clip_list(l):
    return list(map(clip, l))
```

7

我们已经看到如何使用步长为 -1 的切片来反转列表。回文是指与其反转后相等的字符串，所以写出定义非常简单：

```python
def is_palindromic(s):
    return s == s[::-1]
```

我们可以使用这个 `is_palindromic` 函数作为过滤器，只返回列表中那些是回文的字符串：

```python
def palindromes(l):
    return list(filter(is_palindromic, l))
```

现在，我们可以构建范围内仅那些是回文的数字。

```python
def palindromic_numbers_in(x, y):
    ps = palindromes(list(map(str, list(range(x, y))))
    return list(map(int, ps))
```

在返回之前，必须将它们转换回整数。我们可以通过 `map` 实现这一点。现在我们可以找到直到 500 的所有回文数：

```python
>>> palindromic_numbers_in(1, 500)

[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44, 55, 66, 77, 88, 99, 101, 111, 121, 131, 141, 151, 161, 171, 181, 191, 202, 212, 222, 232, 242, 252, 262, 272, 282, 292, 303, 313, 323, 333, 343, 353, 363, 373, 383, 393, 404, 414, 424, 434, 444, 454, 464, 474, 484, 494]
```

我们可以移除 `list` 的实例化，因为 `range`、`filter` 和 `map` 都能接受迭代器：

```python
def is_palindromic(s):
    return s == s[::-1]
```

```python
def palindromes(l):
    return filter(is_palindromic, l)
```

```python
def palindromic_numbers_in(x, y):
    ps = palindromes(map(str, range(x, y)))
    return list(map(int, ps))
```

然而，我们选择从最后的 `palindromic_numbers_in` 函数返回一个实际列表，而不是生成器。

这是一个简单的列表推导式，只是对列表中的每个项使用了 `clip`：

```python
def clip_list(l):
    return [clip(x) for x in l]
```

# 9

在这个例子中，我们在列表推导式中同时使用了 `for` 和 `if` 来处理字符串列表。

```python
def palindromic_numbers_in(x, y):
    strings = map(str, range(x, y))
    return [int(x) for x in strings if is_palindromic(x)]
```

将整个内容放在一个表达式中更具可读性：

```python
def palindromic_numbers_in(x, y):
    return [int(x) for x in map(str, range(x, y)) if is_palindromic(x)]
```

# 6. 更漂亮的打印

# 1

我们必须使用计数器来防止打印额外的逗号：

```python
def print_list(l):
    length = len(l)
    print('[', end='')
    for x in l:
        print(x, end='')
        length -= 1
        if length > 0: print(', end='')
    print(']')
```

这比让 `print` 工作要复杂得多，但它允许自定义：例如，如果我们不想打印逗号或空格。

# 2

在这种情况下，格式化字符串无法帮助我们消除复杂性。事实上，这个解决方案比不使用格式化的要长：

```python
def print_list(l):
    length = len(l)
    print('[', end='')
    for x in l:
        length -= 1
        if length > 0: print(f'{x}, ', end='')
        else:
            print(f'{x}', end='')
    print(']')
```

# 3

在没有格式化字符串，我们必须显式地对整数使用 `str` 来调用 `rjust` 方法。不过我们可以使用带有多个参数的 `print` 函数来处理整行：

```python
def print_powers(n):
    for x in range(1, n):
        x1 = str(x).rjust()
        x2 = str(x).rjust()
        x3 = str(x).rjust()
        x4 = str(x).rjust()
        x5 = str(x).rjust()
    print(x1, x2, x3, x4, x5)
```

# 4

这是 `rjust` 对 `zfill` 的简单替换：

```python
def print_powers(n):
    for x in range(1, n):
        x1 = str(x).zfill()
        x2 = str(x).zfill()
        x3 = str(x).zfill()
        x4 = str(x).zfill()
        x5 = str(x).zfill()
    print(x1, x2, x3, x4, x5)
```

事实上，我们可以使用 `rjust(5, '0')` 相同的效果。

# 5

我们使用 `...` 来安全地打开和关闭文件。然后是仔细构造 `while` 条件和变量赋值的问题，将其打印到文件中：

```python
def names_to_file(filename):
    with open(filename, 'w') as f:
        name = 'empty'
        while name != '':
            name = input('Title, forename and surname: ')
            if name != '':
                words = name.split()
                print(words[2], words[1], words[0], sep='', file=f)
```

# 6

使用格式化字符串允许我们移除 `sep=', '` 参数：

```python
def names_to_file(filename):
    with open(filename, 'w') as f:
        name = 'empty'
        while name != '':
            name = input('Title, forename and surname: ')
            if name != '':
                words = name.split()
                print(f'{words[2]}{words[1]}{words[0]}', file=f)
```

# 7

对于列表中的每个句子，我们找到单词的位置（如果有）。记住找到单词的结果为 -1，我们决定打印什么到屏幕：

```python
def number_found(sentences, word):
    n = 0
    for s in sentences:
        n += 1
        p = s.find(word)
        if p == -1:
            print(f'{word} not found in sentence {n}')
        else:
            print(f'{word} found at position {p} in sentence {n}')
```

# 8

这是上一个答案的简单修改：

```python
def number_found(sentences, word, filename):
    n = 0
    with open(filename, 'w') as f:
        for s in sentences:
            n += 1
            p = s.find(word)
            if p == -1:
                print(f'{word} not found in sentence {n}', file=f)
            else:
                print(f'{word} found at position {p} in sentence {n}', file=f)
```

# 7. 排列物品

# 1

这可以通过元组解包实现：

```python
>>> a = 1
>>> b = 2
>>> a, b = (b, a)
>>> a
2
>>> b
1
```

在对名称进行值的多次赋值时，我们不需要给元组加括号：

```python
>>> a = 1
>>> b = 2
>>> a, b = b, a
>>> a
2
>>> b
1
```

然而，我们不能这样写：

```python
def swap(a, b): a, b = b, a
```

为什么不能？

# 2
