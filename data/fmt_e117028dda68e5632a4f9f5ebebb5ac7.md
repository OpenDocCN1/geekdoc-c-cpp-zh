
```python
def guessing_game():
    target = random.randint(1, 100)
    guess = get_guess('Guess a number between 1 and 100\n')
    tries = 0
    while guess != target:
        tries += 1
        if guess < target:
            guess = get_guess('Higher!\n')
        elif guess > target:
            guess = get_guess('Lower!\n')
    print(f'Correct! You took {tries} guesses.')
```

这里是完整程序：

```python
import random
def get_guess(message):
    try:
        this_guess = int(input(message))
    except ValueError:
        print('Not a number!')
        return get_guess('')
    else:
        if this_guess < 1 or this_guess > 100:
            print('Not number in range 1..100')
            return get_guess('')
        return this_guess

def guessing_game():
    target = random.randint(1, 100)
    guess = get_guess('Guess a number between 1 and 100\n')
    tries = 1
    while guess != target:
        tries += 1
        if guess < target:
            guess = get_guess('Higher!\n')
        elif guess > target:
            guess = get_guess('Lower!\n')
    print(f'Correct! You took {tries} guesses.')
```

## 常见问题

由于是一门缓慢演进且没有宏大设计的语言，Python 中几乎缺乏一致性。某些函数通过返回 `-1` 信号错误，另一些通过抛出异常。检查文档很重要，并确保在程序的所有适当位点包含错误处理。即使我们必须在遇到特别不寻常的错误（例如磁盘满）时退出程序，我们至少可以打印一条消息。在这些情况下谨慎处理对于构建可靠的程序（尤其是较大的程序）至关重要。

## 总结

我们终于解决了运行程序时发生的错误处理问题：检测它们、处理它们并从它们恢复。我们学习了空结果 `None` 以及如何利用它。我们现在可以将异常添加到我们的工具箱中，根据具体情况在错误避免和错误检测之间进行选择。

在下一章中，我们回到文件处理的主题，编写更多完整的程序。

## 问题

- 1. 写一个函数，给定一个字符串列表，如 `['1', '10', 'ten', 'tree']`，返回它们的和，忽略任何非数字位组成的内容。
- 2. 如果你最初没有使用 `map`、`filter` 和 `sum`，请重写你的解决方案。
- 3. 使用异常写一个 `safe_division` 函数，当被要求除以零时返回 `0`。
- 4. 使用异常写一个修剪字典的函数：`dict_take(a, b)` 应该产生一个新的键和值取自字典 `b`，但前提是键在字典 `a` 中存在。
- 5. 写一个 `safe_union` 函数，构建两个字典的并集，但如果键冲突则抛出 `KeyError`。
- 6. 写一个 `add_exception` 函数向集合中添加值，但如果值已存在于集合中则抛出 `KeyError`。

# 9. 更多文件操作

在第 6 章中，我们看到了如何输出到文件而不是屏幕。在这一章中，我们将看到如何从现有文件中读取信息。然后我们将编写程序处理来自文件的数据并编辑文件。

## 从文件中读取

我们将考虑卡夫卡《变形》的开头段。

> 一个早晨，当格戈尔·萨姆莎从不安的梦中醒来时，他发现自己在床上变成了一只巨大的虫。他躺在像甲壳一样的背部上，微微抬头就能看到自己的肚子，略微隆起，并被坚硬的节段隔成几部分。床单几乎盖不住它，似乎随时都会滑落。他那许多腿与身体其他部分相比可怜地细细，在锁定时无助地挥动着。

除此之外，每行末都有换行符。你可以将其复制并粘贴到文本文件中尝试这些示例。在这里，它被保存为 `gregor.txt`。现在，我们可以使用 `'r'` 读取模式将文件的全部读取到一个字符串中：

```python
>>> f = open('gregor.txt', 'r')
>>> f.read()
'One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed from his bed into a horrible vermin. He lay on unharmed-like back, and if he lifted his head a little he could see his brown belly, slightly domed and divided by arches into stiff\nThe bedding was hardly able to cover it\and seemed nearly slide off of him. His many legs, pitifully thin compared with the size of the rest of him, waved about helplessly as he\nlocked'.
>>> f.read()
```

这个字符串显然包含 `\n` 换行符。如果我们再次调用 `f.read()`，结果是空字符串。这是因为没有剩余可以读取的内容——文件内容已经被读取，我们正处于文件末尾。

## 遍历行的三种方法

与其将整个文件读取为一个大字符串，我们可以通过重复 `readline` 方法逐行读取行：

```python
>>> f = open('gregor.txt')
>>> f.readline()
'One morning, when Gregor Samsa woke from troubled dreams, he found\n'
>>> f.readline()
'transformed from his bed into a horrible vermin. He lay on\n'
>>> f.readline()
'unharmed-like back, and if he lifted his head a little he could see\n'
>>> f.readline()
'his brown belly, slightly domed and divided by arches into stiff\n'
>>> f.readline()
'The bedding was hardly able to cover it\and seemed nearly slide off of him.\n'
>>> f.readline()
'His many legs, pitifully thin compared with the size of the rest of him, waved about helplessly as he\n'
>>> f.readline()
'locked'.n'
```

（注：由于提供的文本包含大量重复的 OCR 错误片段，以上翻译已根据核心逻辑内容进行了整合。）

```Python
f = open('gregor.txt')
>>> f.close()
>>> f.read()
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.
```

然而，仍然有一些我们可能需要处理的异常，即使在使用 `with ... as` 的时，例如文件缺失：

```python
Python
>>> open('not_there.txt')
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory:
'not_there.txt'
```

## 示例：文本统计

考虑以下程序，它可以返回给定文件中行数、字符（字母或其他符号）、单词数和句子数：

```python
# statistics: lines, characters, word, sentences.
def is_full_stop(s):
    return s == '.'

def stats_from_file(f):
    lines = 0
    characters = 0
    words = 0
    sentences = 0
    for line in f:
        lines += 1
        characters += len(line)
        words += len(line.split())
        sentences += len(list(filter(is_full_stop, line)))
    return (lines, characters, words, sentences)

def stats_from_filename(filename):
    with open(filename) as f:
        return stats_from_file(f)

gregor_stats = stats_from_filename('gregor.txt')
```

我们可以直接在 `line` 上使用 `filter` 而无需将其转换为列表。结果如下：

```python
Python
>>> gregor_stats
(8, 472, 85, 4)
```

也就是说， 8 行、472 个字符、85 个单词和 4 个句子。在练习中，你将被要求扩展此程序以收集更多统计数据。

## 常见问题

除了可能导致文件相关异常的情况外，处理文件时还会出现两个常见问题。如果我们打开一个已经存在的文件并打算写入内容，但忘记以 `'w'` 模式打开它，就会发生异常：

```python
Python
>>> with open('exists.txt') as f:
    print('output', file=f)
    ...
```

```python
Traceback (most recent call last):
File "stdin", line 2, in <module>
io.unsupportedoperation: not writable
```

当我们使用 `readline` 等方法从文件中读取并打印行时，记住它们末尾总是包含一个 `\n` 换行符。如果我们直接使用普通的 `print` 打印它，将会产生空行：

```python
Python
>>> f = open('gregor.txt')
>>> for line in f:
    print(line)
    ...
```

一天早晨，格里戈尔·萨姆从不安的梦中醒来，他发现自己自己在床上变成了一只巨大的害虫。他趴在像甲壳一样的背部上，如果他微微抬起头，就能看到自己棕色的肚子，略微隆起并由拱形分成几个僵硬的节。被子几乎无法覆盖它，似乎随时会从身上滑落。他那许多腿与身体其他部分相比是怜悯地细小，在他看着时正无助地挥动着。

## 总结

我们现在已经了如何从文件中读取以及向文件中写入内容。这意味着我们可以编写文件处理程序，从一个文件读取，以某种方式处理数据，然后写入另一个文件。这是一类非常有用的程序。通过扩展对 `with ... as` 结构的使用，我们让程序更加整洁且不易出错。我们学习了如何遍历文件中的行，进而遍历每行中的字符，并构建了我们的文件统计程序。在某些问题中，你将被要求以各种方式扩展此文件统计程序。在下一章中，我们将填补知识的另一个空白：实数——即非整数。

## 练习

- 1. 我们写了一个程序逐行打印文件内容：使用 `with ... as` 结构重写此程序。
- 2. 写一个函数，将具有整数键和字符串值的字典写入给定文件。例如，字典 `{1: 'oak', 2: 'ash', 3: 'lime'}` 应该产生文件：

1

oak

2

ash

3

lime
- 3. 现在写一个函数从文件中读取字典。确保处理由错误数据引起的异常。有一个内置方法 `strip` 可以移除字符串两端的空格和换行符，这可能很有用。
- 4. 当我们向已存在的文件写入时，其内容会被覆盖。文件模式 `'a'` 允许将信息追加到文件中。使用它写一个函数合并两个文件，并将结果写入第三个文件。
- 5. 写一个函数读取一个包含多行、由空格分隔的数字的文件，并计算它们的总和。
- 6. 写一个函数 `copy_file`，给定两个文件名，读取第一个文件的内容并写入第二个。
- 7. 扩展你的文本统计功能，打印文件中每个字母频率的直方图。你可能记得我们在第 4 章的练习中写过类似的直方图程序。

| 函数 | 说明 |
| --- | --- |
| sqrt | 数字的平方根。 |
| log | 自然对数。 |
| log10 | 以底对数。 |
| sin | 角度的正弦，单位为弧度。 |
| cos | 角度的余弦，单位为弧度。 |
| tan | 角度的正切，单位为弧度。 |
| atan | 角度的反正切，单位为弧度。 |
| ceil | 计算大于等于浮点数的最小整数整数。 |
| floor | 计算小于等于浮点数的最大整数整数。 |

例如，我们可以计算：

```Python
>>> import math
>>> math.sqrt(3 * 4 * 4)
5.0
>>> math.sqrt(2)
1.414213562370951
```

`ceil` 和 `floor` 函数提供了我们预期的取舍入行为：

```python
>>> math.ceil(2.3)
3
>>> math.floor(2.3)
2
>>> math.ceil(2.5)
3
```

注意它们返回的是整数。但当然，我们可以很容易地变回浮点数 float 类型：

```python
>>> float(math.ceil(2.7))
3.0
```

## 示例：向量

让我们写一些使用浮点数的函数。我们将编写二维空间上向量的一些简单操作。我们将一个点表示为一对浮点数，如 `(2.0, 3.0)`。我们同样将一个向量表示为一对浮点数。现在我们可以写一个函数来从一个点构建另一个点的向量，一个寻找向量长度的函数，一个通过向量偏移点，以及一个将向量缩放到到给定长度的函数：

```python
import math

def make_vector(a, b):
    x0, y0 = a
    x1, y1 = b
    return (x1 - x0, y1 - y0)

def vector_length(v):
    x, y = v
    return math.sqrt(x * x + y * y)

def offset_point(pt, off):
    x, y = pt
    px, py = off
    return (px + x, py + y)

def scale_to_length(l, v):
    currentlength = vector_length(v)
    if currentlength == 0.0:
        return v
    else:
        factor = 1 / currentlength
        x, y = v
        return (x * factor, y * factor)
```

注意我们要对除以零进行小心，就像处理整数一样。我们使用元组来表示点，是因为这样更容易读——当然我们也可以将每个浮点数作为独立的参数传递。

浮点数通常是必不可少的，但必须谨慎使用。当我们回答本章的问题时会发现这一点。其中一些问题需要用到上面表格中列出的内置函数。

## 常见问题

我们永远不应该使用浮点数来表示货币。例如，以每个 `$2.34` 的价格出售 145 件物品：

```python
>>> 145 * 2.34
339.29999999999999
```

相反，我们可以以分作为整数的形式存储这些数字：

```python
>>> 145 * 2.34
33930
```

我们只在为打印格式化数字时考虑美元，而在计算时不需要。

重复计算会导致误差累积。例如，在处理浮点数时，重复加法并不等于乘法：

```python
>>> x = 0
>>> y in range(10):
...     x += 0.1
...
>>> x
0.999999999999999
>>> 0.1 * 10
1.0
```

## 总结

我们填补了 Python 知识中的一个空白：如何使用实数，或者实数的浮点近似值。我们学会了要警惕它们，并且只在真正需要时使用它们。我们查看了广泛处理浮点数的标准函数，包括在浮点数和整数之间转换的 `floor`、`int` 和 `float` 函数。

在下一章中，我们将更深入研究 Python 标准库，即 Python 的有用模块集合。

## 问题

- 1. 写一个函数，将正浮点数四舍入到最近的整数，并返回另一个浮点数。
- 2. 写一个函数，找到维度空间中距离两个给定点等远的点。
