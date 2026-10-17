
```python
def next_boards(b, pl):
    if wins('O', b) or wins('X', b) or full(b):
        return (b, [])
    bs = []
    for i, e in enumerate(b):
        if e == '_':
            new_board = b.copy()
            new_board[i] = pl
            bs.append(new_board)
    return (b, [next_boards(x, swap_player(pl)) for x in bs])
```

我们必须小心使用列表的 `copy` 方法复制棋盘，以便每个列表都能被独立变异。现在我们需要让过程运行起来，从空盘开始：

```python
def game_tree(pl):
    return next_boards(emptyboard)

x_tree = game_tree('X')
```

这需要一些时间。

现在我们可以这样使用它：

```
Python
>>> process_pixels_in_place(grey, i)
```

**问题 1** 编写函数来增加或降低图像的亮度和对比度。亮度可以通过将每个像素的每个分量加上适当的因子来实现，对比度则可以通过乘法来实现。

**问题 2** 编写函数以原地对图像进行垂直或水平翻转，并将其旋转 180 度。

我们加载了一张图像，修改了它并保存了它。但我们如何创建一个新图像或组合图像呢？让我们使用函数给图像添加边框，就像画框一样：

```python
border(i, width, colour):
    sx, sy = i.size
    p = i.load()
    i2 = Image.new('RGB', (sx + width * 2, sy + width * 2), colour)
    p2 = i2.load()
    for x in range(sx):
        for y in range(sy):
            p2[x + width, y + width] = p[x, y]
    return i2
```

`border` 函数为图像添加给定宽度和颜色的边框，返回的原始图像保持不变。我们使用 `Image.new` 方法构建一个更大的新图像，并填充边框颜色。然后，我们逐个复制像素。现在我们可以用它了：

```python
Python
>>> bordered = border(i, 20, (150, 150, 150))
```

结果如下：

![](img/496c1aa28bc754c78c9a97aa8e66e6ea_108_0.png)

我们通过模糊图像来使其看起来失焦，方法是让每个像素成为其周围八个像素及其自身的平均值：

```python
def blur(i):
    p = i.load()
    i2 = i.copy()
    p2 = i2.size
    sx, sy = p2
    for x in range(1, sx - 1):
        for y in range(1, sy - 1):
            sumr, sumg, sum = 0, 0, 0
            for dx in range(-1, 2):
                for dy in range(-1, 2):
                    sourcec, sourceg, sourceb = p[x + dx, y + dy]
                    sumr += sourcec
                    sumg += sourceg
                    sum += sourceb
            p2[x, y] = (int(sumr / 9), int(sumg / 9), int(sum / 9))
    return p2
```

我们使用了 `copy` 方法创建并返回一个相同大小的新图像。现在我们可以使用它几次，确保开始时一个带白色边框的图像，以便为模糊留出空间：

```python
>>> white_bordered = border(i, 20, (255, 255, 255))
>>> x = blur(blur(white_bordered))
>>> x.save('blurred.png')
```

结果如下：

![](img/496c1aa28bc754c78c9a97aa8e66e6ea_109_0.png)

**问题 3** 重写模糊函数以便原地操作。结果有显著不同吗？

**问题 4** 对于任意给定次数的模糊操作，边框需要多宽？实现一个仅使用所需边框的版本。

到目前为止我们只查看了静态图像：Pillow 有一些处理动态图像的功能。我们将图像在若干帧的时间内逐渐淡化为白色。由于我们需要保留多个图像，且每个图像经过不同的处理，因此我们需要一个不是原地工作的版本，而是返回一个新的、处理过的图像：

```python
def process_pixels(f, i):
    p = i.load()
    i2 = i.copy()
    p2 = i2.size
    sx, sy = p2
    for x in range(sx):
        for y in range(sy):
            p2[x, y] = f(p[x, y])
    return p2
```

使用笔和纸，你可以验证以下函数是否正确：

```python
def fade_by(f, p):
    r, g, b = p
    r_out = int((r * (100 - f)) / 255)
    g_out = int((g * (100 - f)) / 255)
    b_out = int((b * (100 - f)) / 255)
    return (r_out, g_out, b_out)
```

现在我们收集从 100 步到 0 级的图像：

```python
def make_images(i):
    images = []
    for x in range(100, -1, -5):
        faded = process_pixels(lambda p: fade_by(x, p), i)
        images.append(faded)
    return images
```

使用该函数从原始图像构建并保存动态 GIF：

```python
>>> images = make_images(i)
>>> images[0].save('fade.gif',
    ... append_images=images[1:],
    ... duration=100,
    ... loop=0)
```

这是直观的：它在第一张图像上列出剩余部分。持续时间是第十秒：[image_placeholder]

**问题 5** 产生一个你的图像重复模糊的 GIF。你会发现结果是颗粒状——由于历史原因，GIF 只有 256 种颜色。

## 问题答案

1. 错误：表达式是一个数字——没有工作。表达式值为 1，因为乘法的优先级高于加法。表达式值为 11。程序员似乎认为空格影响优先级。其实不是，这种用法是错误的。

2. `%` 运算符的优先级高于 `+` 运算符。所以 `1 + 2 % 3` 等于 `1 + (2 % 3)` 为 3。比较运算符 `<` 考虑字典顺序，所以 `'banana' < 'eggs'`。大写字母都比小写字母“小”，例如 `'B' < 'b'` 结果为 True。对于布尔值，False 被认为“小于” True。第一个完全符合预期：`1 + 2` 等于 3。

3. 结果显示 `+` 运算符用于数字时相加，用于字符串时拼接：

```python
>>> 'one' + 'two'
'onetwo'
```

然而，混合两种类型将不起：

```python
>>> 1 + 'two'
Traceback (most recent call last):
  File "stdin", line 1, in <module>
TypeError: unsupported operand type(s) for '+': 'int' and 'str'
```

`*` 运算符可以用于字符串和数字，多次拼接字符串：

```python
>>> 3 * '1'
'111'
>>> '1' * 3
'111'
>>> print('1' * 3)
111
```

最后一行，我们记得字符串和打印字符串的区别。当作为数字时，True 的值为 1，而 False 的值为 0：

```python
>>> True + 1
2
>>> False + 1
1
```

你注意到上一个示例引号前的 `f` 吗？这是一个格式字符串，我们将在第 6 章讨论：

```python
>>> print(f'One and two is {1 + 2} and that is all.')
One and two is 3 and that is all.
```

大括号 `{}` 部分部分已求值并打印。

# 2. 名称与函数

我们包含了 `return` 关键字以确保结果返回给我们：

```python
>>> times_ten(x):
    return x * 10
>>> times_ten(50)
500
```

# 2

这个函数将有两个参数。我们使用了 `and` 运算符以及不等于运算符 `!=`。

```python
>>> both_non_zero(a, b):
    return a != 0 and b != 0
>>> both_non_zero(1, 2)
True
>>> both_non_zero(1, 0)
False
```

# 3

这是一个带有三个参数的简单函数。我们记得使用 `return`：

```python
>>> volume(w, h, d):
    return w * h * d
>>> volume(10, 20, 30)
6000
```

我们现在可以写 `volume_ten_deep` 函数了：

```python
>>> def volume_ten_deep(w, h):
    return volume(w, h, 10)
>>> volume_ten_deep(5, 6)
300
```

注意这里也需要 `return`：`volume` 中的 `return` 是够够的。

# 4

如果 'a...'z' 范围内的小写字符不是元音，它必须是辅音。我们可以重用我们之前编写的 `is_vowel` 函数，并使用 `not` 对其取反：

```python
>>> def is_consonant(s):
...
    return not is_vowel(s)
...
>>> is_consonant('r')
True
>>> is_consonant('e')
False
```

## 5

我们可以对负参数返回 0。0 的阶乘是 1，所以我们也可以修改这一点，称我们的新函数可以找到任何非负整数的阶乘：

```python
>>> def factorial(x):
...
    if x < 0:
...
        return 0
...
    elif x == 0:
...
        return 1
...
    else:
...
        return x * factorial(x - 1)

>>> factorial(-1)
0
```

## 6

我们可以使用递归函数：

```python
>>> def sum_nums(n):
...
    if n == 1:
...
        return 1
...
    else:
...
    return n + sum_nums(n - 1)

>>> sum_nums(10)
55
```

还有一个直接的数学公式。我们使用了整除运算符 `//`，这是我们之前没有过的：

```python
>>> def sum_nums(n):
...
    return (n * (n + 1)) // 2
...
>>> sum_nums(10)
55
```

你能看出为什么吗？

## 7

任何数的 0 次方都是 1。任何数的 1 次方都是它本身。否则，答案是当前的 n 乘以 x^(n-1)。

```python
>>> power(x, n):
...
    if n == 0:
...
        return 1
...
    else:
...
        if n == 1:
...
            return x
...
        else:
...
            return x * power(x, n - 1)

>>> power(2, 5)
32
```

注意，在这里我们必须在一个 `if` 和 `else` 内部嵌套另一个。缩进有助于显示结构。记住 Python 允许我们使用 `elif` 关键字来压缩代码：

```python
>>> power(x, n):
...
    if n == 0:
...
        return 1
...
    elif n == 1:
...
        return x
...
    else:
...
        return x * power(x, n - 1)

>>> power(2, 5)
32
```

这更容易读，部分原因是因为所有的 `return` 关键字都对齐了。事实上，我们可以移除 `n = 1` 的情况，因为 `power(x, 1)` 将还原为 `x * power(x, 0)`，而结果就是 `x`。

## 8

我们使用在第一章学过的 `%` 取模运算符来测试小于给定数字的数字是否能被整除，每次将测试除数加 1。如果可以整除，我们就打印出来。

```python
>>> factors(n, x):
...
    if x % n == 0: print(x)
...
    if n < x: factors(n + 1, x)
>>> factors(1, 12)
1
2
3
4
6
12
```

我们可以通过将解决方案封装在另一个函数中来清理，该函数提供从 1 开始的起点：

```python
>>> def factors_simple(x):
...
    factors(1, x)
>>> factors_simple(12)
1
2
3
4
6
12
```

## 3 再来一遍

1

我们将停止点设为 –1。我们必须小心起始点和停止点。我们将停止点设为 0，这样我们就在 1 处停止（即在到达 0 之前）：

```python
def print_down_from(n):
    for x in range(n, 0, -1):
        print(x)
```

2

我们修改了 `column_width` 的计算，将 `n * (n - 1)` 作为最大宽的项目，而不是 `n * n`：

```python
def times_table(n):
    column_width = len(str(n * (n - 1))) + 1
    for y in range(1, n + 1):
        for x in range(1, n + 1):
            print(x * y, end=' ' * (column_width - len(str(x * y))))
        print('*')
```

这是大小为十的表格的新结果：

```python
>>> times_table(10)
1 2 3 4 5 6 7 8 9 10
2 4 6 8 10 12 14 16 18 20
3 6 9 12 15 18 21 24 27 30
4 8 12 16 20 24 28 32 36 40
5 10 15 20 25 30 35 40 45 50
6 12 18 24 30 36 42 48 54 60
7 14 21 28 35 42 49 56 63 70
8 16 24 32 40 48 56 64 72 80
9 18 27 36 45 54 63 72 81 90
10 20 30 40 50 60 70 80 90 100
```

使用这种方法，某些列中仍然可能有多余的空间：

```python
>>> times_table(4)
1 2 3 4
2 4 6 8
3 6 9 12
4 8 12 16
```

你能修复它吗？

## 3

我们使用循环来检查字符串中的每个字母，每当看到空格时就给局部变量加 1：

```python
def count_spaces(s):
    c = 0
    for x in s:
        if x == ' ':
            c += 1
    return c
```

我们使用 `return` 来确保最终计数是函数的结果。我们可以使用 `+=` 运算符来缩短给变量加值的常用操作：

```python
def count_spaces(s):
    c = 0
    for x in s:
        if x == ' ':
            c += 1
    return c
```
