
```
return

# Delete the line
lines.pop(line_num)
```

就这样了。让我们试试：

```
> l 1
1: This is line 1
2: This is line 2
3: This is line 3
4: This is line 4
5: This is line 5
> d 3
> l 1
1: This is line 1
2: This is line 2
3: This is line 4
4: This is line 5
> d 0
no such line
> d 5
no such line
```

看起来不错！

下一步最容易的是什么？可能是“编辑”功能。

## 问题解决步骤：理解问题

当我们编辑单行时，我们希望用从键盘输入的新元素完全替换 lines 列表中的元素。

旧行将被丢弃。

为此，用户输入 e 表示“编辑”，后跟行号。

## 问题解决步骤：制定计划

让我们像删除一样操作，只是我们不用 pop() 来删除一行，而是直接使用 input() 获取另一行并将其存储到列表中。

## 问题解决步骤：执行计划

首先，让我们在主循环中添加该命令处理器：

```
# Edit a line
elif command[0] == 'e':
    handle_edit(args, lines)
```

其次，让我们实现编辑处理器。直到最后一行，代码和原理都相同：

```
def handle_edit(args, lines):
    """Edit a line in the file."""
    if len(args) == 1:
        # Get the line number to edit
        line_num = one_to_zero(int(args[0]))
    else:
        print("usage: e line_num")
        return
    # Make sure we're in range
    if line_num < 0 or line_num >= len(lines):
        print("no such line")
```

```
return

# Edit the line
lines[line_num] = input()
```

注意我们只是用 input() 返回的任何行替换列表中指定的行。

让我们试试！

```
> l 1
1: This is line 1
2: This is line 2
3: This is line 3
4: This is line 4
5: This is line 5
> e 2
NEW LINE 2!
> l 1
1: This is line 1
2: NEW LINE 2!
3: This is line 3
4: This is line 4
5: This is line 5
>
```

等一下！我编辑后第 2 行和第 3 行都挤在一起了！这不可能对。

## 问题解决步骤：理解问题

这都与我们保留在列表中各行末尾的换行符有关。

记住我们存储每一行时都附带末尾的换行符。

但 input() 会去掉换行符！这不是我们想要的。

## 问题解决步骤：制定计划

所以我们必须在刚刚输入的、呃、新行的末尾加上换行符。我们只需用 + 字符串连接运算符把它拼上去。

## 问题解决步骤：执行计划

```
# Edit the line, adding a newline to the end (since input() strips
# it off).
lines[line_num] = input() + '\n'
```

就这样完成了！

下一步最容易编写的是什么呢？看起来只剩下一个编辑命令：“追加”。

## 问题解决步骤：理解问题

这个有点不同。看起来我们会像处理其他命令一样先读取要追加的行。

但随后我们进入一种奇怪的模式，反复输入行，直到用户单独输入一个句点为止。

并且每一行都会依次被追加。

如果用户说在第 0 行后追加，行应该插入到文件顶部。

## 问题解决步骤：制定计划

所以让我们照常进行命令行解析，看看我们想在哪个行后插入。

然后让我们循环直到用户输入句点。

在循环内部，我们将读取一行并在正确的位置将其插入列表。

根据文档，列表有一个 append() 方法，但它只追加到列表末尾。

我们希望它能做到这一点，但也能把行放在中间或顶部。

让我们继续查看文档。

有 insert() 用于在索引前放置对象。这似乎适用于开头和中间，但对于追加到末尾呢？我们是否必须在这种特殊情况下使用 append() 方法？

文档对此并不完全清楚。让我们打开 REPL 并尝试一些测试。

我创建一个列表，然后尝试在各种位置插入值。

首先，让我们尝试在元素 0 之前插入，这应该插入到开头：

```
>>> a = [11, 22, 33]
>>> a.insert(0, 99)
>>> a
[99, 11, 22, 33]
```

太好了！99 被放在了最前面，就像我想要的那样。

让我们在索引 2 之前再插入一个数字：

```
>>> a.insert(2, 999)
>>> a
[99, 11, 999, 22, 33]
```

也成功了。

现在，列表只有到索引 4... 但让我们大胆尝试在索引 5 之前插入（不存在），看看是否会追加到末尾：

```
>>> a.insert(5, 9999)
>>> a
[99, 11, 999, 22, 33, 9999]
```

是的！成功了！我们不必特别调用 append()。

有点奇怪，但如果你为追加提供一个超过最后一个的索引，它会把值放在列表末尾。

如果我们创建一个小列表并尝试在索引 99 处插入值 3490，它只是把它放在末尾：

```
>>> a = [1, 2, 3]
>>> a.insert(99, 3490)
>>> a
[1, 2, 3, 3490]
```

这种尝试看看什么有效什么无效的实验很常见，是探索和学习系统工作原理的好方法。

好吧，所以我们：

- 获取要追加后的行号。记住我们希望它是零基的，所以我们要从用户输入的值中减去 1。如果他们输入“2”，那意味着我们要在索引 1 后插入。
- 但由于 insert() 方法是在行前插入，而不是行后，我们最好再给行索引加一，这样才能在该行后追加。
- 然后循环直到用户输入句点，输入一行并在正确的位置插入到列表中。

现在，你可能会想，为什么要先减一然后马上再加一？

你说得对——这什么也没做。我们不必这样做。

但可以说这对代码的未来阅读者更清晰。我们一开始就尽快减一以得到零基索引方法。然后我们加一以让 insert() 在行后插入

```
2: NEW line 2
3: This is line 1
4: This is line 2
5: This is line 3
6: This is line 4
7: This is line 5
```

成功！

让我们在中间插入行：

```
> a 4
NEW line in the middle
.
> l 1
1: NEW line 1
2: NEW line 2
3: This is line 1
4: This is line 2
5: NEW line in the middle
6: This is line 3
7: This is line 4
8: This is line 5
```

成功！

让我们在末尾插入一些行：

```
> a 8
NEW end line 1
NEW end line 2
.
> l 1
1: NEW line 1
2: NEW line 2
3: This is line 1
4: This is line 2
5: NEW line in the middle
6: This is line 3
7: This is line 4
8: This is line 5
9: NEW end line 1
10: NEW end line 2
```

也成功了！太棒了！

虽然不是自动化的，但这是一个很好的测试覆盖。我们查看了常见情况（中间插入），但也查看了边缘情况（开头和末尾插入），以确保它们能正常工作。测试时，始终要考虑哪些情况不常见并明确测试这些情况。

现在只剩下一件事：使用“w”（写入）命令将文件保存到磁盘。

## 问题解决步骤：理解问题

我们很久以前就写了一些代码，一次读一行文件并将结果存储在列表中。

这次，我们想做相反的操作。遍历我们的列表并一次写一行文件，直到完成。

## 问题解决步骤：制定计划

与追加命令相比，这很简单。

- 打开文件进行写入
- 遍历所有行
- 将每一行写入文件

另外：

- 在主输入循环中挂接“w”命令。

并且：

- 解析“w”命令的参数以获取文件名

由于“将一堆行写入磁盘”是一个很好的自包含操作，我计划编写一个函数只做这一件事，什么也不多做。我会编写另一个函数在请求写入时被调用，以确保参数正确等等。保持模块化！

## 问题解决步骤：执行计划

首先，让我们添加一个函数将文件写入磁盘。作为参数，它将接受要写入的行列表和要写入到的文件名。

当我们打开文件时，我们会向它传递“w”参数以表示我们正在写入此文件。

请注意，一旦你打开文件进行写入，如果文件存在它会被擦除。但在这种情况下应该没问题，因为我们马上就要重写它。

并且由于每一行已经在末尾带有换行符，我们在写入磁盘时不必再添加一个。

```
```python
def write_file(lines, filename):
    """Write a file to disk"""
    with open(filename, "w") as f:
        for line in lines:
            f.write(line)
```
```

现在让我们为该命令编写处理器。这将检查是否指定了参数，如果没有则打印错误。然后写入文件。

```
```python
def handle_write(args, lines):
    """Handle the write command"""
    if len(args) == 1:
        filename = args[0]
    else:
        print("usage: w filename")
        return
    write_file(lines, filename)
```
```

最后，我们需要在主命令循环中添加一个处理器，以便当我们输入“w”时，它会保存文件：

```
```python
# Write (save) the file
elif command[0] == 'w':
    handle_write(args, lines, filename)
```
```

就这样！

## 问题解决步骤：回顾

这里有很多可以改进代码的地方。

- 为删除命令添加选项以指定结束行以及起始行，一次性删除一行块。
- 使其在用户在命令行上指定文件名并且在写入命令后未指定时，写入与命令行上指定的相同文件。
- 添加一个 insert 命令，其工作原理与 append 类似，只是它把新材料放在指定行之前。如何用最少的代码添加实现？毕竟 append 和 insert 很相似。
