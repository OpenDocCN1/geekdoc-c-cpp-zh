

就我个人的偏好而言，如果有些功能是用来显示数据、有些是用来修改数据，我会更喜欢先实现显示数据的那些。它们更不容易把事情弄糟（因为我们并未修改数据），而且如果你连正确显示数据都做不到，那么正确修改数据的概率也非常低。

所以我们先来做那个“list”命令，它能显示文件中的若干行。

## 解决问题的步骤：制定计划

list 命令接受一个参数，表示开始列出的行号。然后它会列出 10 行。

既然我们已经把所有的行都放在一个列表里了，这个任务不算太可怕。我们只需要：

- 解析用户输入的起始位置。
- 如果输入的数字小于 1，就假定他们指的是 1。
- 从该数字开始循环，打印出 10 行。
- 如果遇到最后一行，就停止打印。

既然我们有这些不同类型的功能，就让我们把它们放到各自的函数中，以保持代码的良好组织。

我们会编写一个 `handle_list()` 函数，在用户要求列出文件时被调用。它需要几个参数：用户在命令后输入的参数，以及我们要操作的包含所有行的列表。

## 解决问题的步骤：执行计划

首先，让我们检查一下用户是否想列出文件，方法是看命令的第一个字母是否是 `l`。如果是，那就启动该功能。

但在 `l` 后面还有一个参数，对吧？用户必须指定从哪一行开始列出。而且我们得想办法把它传给 `handle_list()` 函数。

所以我们来做两件事。首先从完整命令中解析出那些参数（如果有的话）。我们用 `split()` 把命令按空格拆开，然后用切片 `[1:]`（也就是从第二个元素到末尾）来取得所有参数。

结果会是一个列表，里面包含命令后面的任何参数；如果没有参数，就是一个空列表。

然后我们把它传给处理函数：

```python
# 获取命令后面的所有参数
args = command.split(" ")[1:]

if command[0] == 'q':
    done = True

# 列出文件内容
elif command[0] == 'l':
    handle_list(args, lines)
```

然后让我们编写一个函数存根⁶ 来处理它，只是看看它是否正常工作：

```python
def handle_list(args, lines):
    print(f'Handle list: {args}, {lines}')
```

运行后，我们会得到：

```text
$ python lineedit.py lines.txt
> l
Handle list: [], ['This is line 1\n', 'This is line 2\n',
'This is line 3\n', 'This is line 4\n', 'This is line 5\n']
> l 99
```

⁶ 函数存根就是一个可调用的函数，它接受所有相同的参数，并且在必要的时候返回一个合理的值。但实际上它并不真正做任何有意义的事。这是一种很好的方式，用来测试你的整体调用流程是否正常。它还为你提供了一个整洁、方便的 TODO 填充位置。

## 2. 我们的差一错误⁷ 导致了行号偏差一位

没错，差一错误已经出名到拥有自己的维基百科页面了。

正如其名称所示，我们的计算出现了“一位”的偏差。但为什么会这样？怎么会这样？

这是人与计算机之间一个非常常见的分歧。我们人类喜欢让列表从索引“1”开始，而计算机喜欢让列表从索引“0”开始。这是一场由来已久的战斗。就连罗马人也是从“I”开始计数的，但那主要是因为罗马数字直到公元 725 年才有了零这个字符——真是后知后觉！

而在这种情况下，输入数字的是人，他们从索引“1”开始计数。我们打印给人类看的输出也从索引“1”开始……

但在 Python 中，行是放在一个从索引“0”开始的列表中的！

## 解决问题的步骤：制定计划

我们需要做一些数学计算。

- 当我们要从人类（1-based）索引转换为计算机（0-based）索引时，需要从数字中减去 1。1 变成 0。
- 当我们要从计算机（0-based）索引转换为人类（1-based）索引时，需要给数字加上 1。0 变成 1。

因为我们使用 start 和 end 来索引列表，我倾向于让它们是 0-based 的，因为列表本身就是 0-based 的。

这里有一个通用的经验法则：

- 当用户输入一个 1-based 的数字时，尽快将其转换为 0-based，供程序内部使用。
- 当你必须显示一个 1-based 的数字时，尽可能长时间地保持 0-based，只在最后输出时再转换。

尽量减少这些转换，只在输入和输出时进行，可以帮你省去很多头疼的问题。

不应该做什么：不要直接到处加上 +1 和 -1，然后指望一切顺利。那样做无疑会走向疯狂。停下来，理解问题，制定计划。然后再执行。

## 解决问题的步骤：执行计划

我要在这里写一个小辅助函数，用来把 0-based 索引转换为 1-based 索引，因为我想我们会在很多地方用到它。而且它能帮助让代码更清晰；与其到处写一堆 +1 和 -1，不如用一个对将来阅读代码的人具有一定意义的函数名。

```python
def one_to_zero(n):
    """将一个数字从1-based索引转换为0-based索引。"""
    return n - 1
```

现在我们可以使用这个函数了。让我们把 start 变为 0-based，然后试试。

```python
start = one_to_zero(int(args[0]))
```

现在运行它，会得到：

```text
$ python lineedit.py lines.txt
> l 1
0: This is line 1
1: This is line 2
2: This is line 3
3: This is line 4
4: This is line 5
Traceback (most recent call last):
  File "lineedit.py", line 76, in <module>
handle_list(args, lines)
```

```text
File "lineedit.py", line 48, in handle_list
print(f'{i}: {lines[i]}', end="")
IndexError: list index out of range
```

还是同样的报错，但让我们先看看之前的那些行。好消息是所有的行都打印出来了。坏消息是左边的行号使用的是计算机的 0-based 体系，而我们需要让它变成人类的 1-based 体系。让我们再加一个辅助函数：

```python
def zero_to_one(n):
    """将一个数字从0-based索引转换为1-based索引。"""
    return n + 1
```

然后在我们的打印输出行中调用它：

```python
print(f'{zero_to_one(i)}: {lines[i]}', end="")
```

现在运行一下：

```text
$ python lineedit.py lines.txt
> l 1
1: This is line 1
2: This is line 2
3: This is line 3
4: This is line 4
5: This is line 5
Traceback (most recent call last):
  File "lineedit.py", line 80, in <module>
    handle_list(args, lines)
  File "lineedit.py", line 52, in handle_list
    print(f'{zero_to_one(i)}: {lines[i]}', end="")
IndexError: list index out of range
```

好极了！这正是我们想要的。所有行都带正确的行号打印出来了。

现在，那个错误是怎么回事？它告诉我们列表索引超出范围，这其实并不意外，因为它已经走到文件末尾了。

在我们进入 for 循环之前，让我们加一些代码来确保 start 和 end 是合理的。（请记住我们已经决定它们是 0-based 的索引。）

```python
# 确保 start 不在列表开头之前
if start < 0:
    start = 0

# 确保 end 不超过列表结尾
if end > len(lines):
    end = len(lines)
```

然后你就可以放心地运行 for 循环了！

```text
$ python lineedit.py lines.txt
> l 1
1: This is line 1
2: This is line 2
3: This is line 3
4: This is line 4
5: This is line 5
> l 3
3: This is line 3
4: This is line 4
5: This is line 5
>
```

完美！这就是完整的 list 功能！

接下来的事情通常会越来越容易。实现的第一个部分是最糟糕的，但之后我们做的都只是同一主题的变体：

- 1. 在输入时检查正确的命令
- 2. 把参数传递给该命令的处理函数
- 3. 构建处理函数的完整实现
- 4. 重复以上步骤

接下来做什么最简单的事情？“删除一行”怎么样？

## 解决问题的步骤：理解问题

我们想要删除一行。这就像从包含所有行的列表中移除一个元素一样简单。

我们只需要知道要移除的元素编号。

当然，用户是在 `d` 命令后面输入它的，所以我们可以从那里获取。

但记住：用户输入的是 1-based 的！我们在用这个数字删除一行之前，必须将它转换为 0-based……否则我们会删除错误的行。

## 解决问题的步骤：制定计划

所以我们应该能够：

- 在主输入循环中添加一个处理函数
- 在删除处理函数中，获取要删除的行号
- 将其转换为 0-based
- 从所有行组成的列表中删除那一行

稍微查一下帮助文档就会发现，`pop()` 方法会从列表中移除指定索引处的元素：

```text
pop(self, index=-1, /)

    移除并返回索引处的项（默认是最后一项）。
```

## 解决问题的步骤：执行计划

让我们在主输入循环中添加对处理函数的调用，只要用户请求删除操作：

```python
# 删除一行
elif command[0] == 'd':
    handle_delete(args, lines)
```

现在让我们编写删除处理函数。一开始它和列出内容的处理函数很相似：我们要获取用户输入的行号，并将其转换为 0-based。

然后确保它在有效范围内。

然后用 `pop()` 方法删除那一行。

```python
def handle_delete(args, lines):
    """删除文件中的一行。"""
    if len(args) == 1:
        # 获取要删除的行号
        line_num = one_to_zero(int(args[0]))
    else:
        print("usage: d line_num")
        return
    # 确保行号在有效范围内
    if line_num < 0 or line_num >= len(lines):
        print("no such line")
```

