

## 打开文件

在 Python 中，你可以在程序中读取文本文件和二进制文件。你还可以写入文件，这一点我们接下来会讲到。读写文件使你能够输出和存储程序中的数据。

### 打开、读取和写入

在 Python 中，你可以创建一个文件对象，类似于创建变量，只需使用 `open()` 函数传入文件即可。文件通常分为文本文件和二进制文件两类。

**步骤 1**

首先，在系统的文本编辑器中输入一些文本。最好使用文本编辑器，而不是文字处理器，因为文字处理器会包含背景格式和其他元素。在我们的示例中，使用的是罗伯特·E·霍华德（Robert E. Howard）创作的诗歌《The Cimmerian》。你需要将文件保存为 `poem.txt`。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_57_0.png)

**步骤 2**

你使用 `open()` 函数将文件作为对象传入一个变量。你可以随意命名文件对象，但你需要告诉 Python 你要打开的文本文件的名称和位置：

```python
poem=open("/home/pi/Documents/Poem.txt")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_57_2.png)

**步骤 3**

如果你现在在 Shell 中输入 `poem`，你会得到一些关于你刚刚要求打开的文本文件的信息。现在你可以使用 `poem` 变量来读取文件的内容：

```python
poem.read()
```

注意，文本中的 `\n` 表示换行符，正如你之前使用过的那样。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_57_1.png)

**步骤 4**

如果你第二次输入 `poem.read()`，你会注意到文件中的文本已经消失。你需要重新输入：`poem=open("/home/pi/Documents/Poem.txt")` 来重新创建文件对象。但这一次，请输入：

```python
print(poem.read())
```

这一次，`\n` 条目会被移除，转而显示为换行和可读文本。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_57_3.png)

**步骤 5**

就像使用列表、元组、字典等一样，你可以索引文本中的单个字符。例如：

```python
poem.read(5)
```

显示前五个字符，而再次输入：

```python
poem.read(5)
```

将显示接下来的五个字符。输入 `(1)` 将一次显示一个字符。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_0.png)

**步骤 6**

类似地，你可以使用 `readline()` 函数一次显示一行文本。例如：

```python
poem=open("/home/pi/Documents/Poem.txt")
poem.readline()
```

将显示文本的第一行；接下来再次输入：

```python
poem.readline()
```

将会再次显示下一行文本。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_1.png)

**步骤 7**

你可能已经猜到，你可以将 `readline()` 函数的结果传入变量，从而在需要时再次调用它：

```python
poem=open("/home/pi/Documents/Poem.txt")
line=poem.readline()
line
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_2.png)

**步骤 8**

进一步扩展，你可以使用 `readlines()` 获取文本中的所有行，并将它们作为多个列表存储起来。然后可以将这些列表存储到一个变量中：

```python
poem=open("/home/pi/Documents/Poem.txt")
lines=poem.readlines()
lines[0]
lines[1]
lines[2]
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_3.png)

**步骤 9**

你还可以使用 `for` 语句将文本行读取出来：

```python
for lines in lines:
    print(lines)
```

既然这是 Python，还有其他方法可以产生相同的输出：

```python
poem=open("/home/pi/Documents/Poem.txt")
for lines in poem:
    print(lines)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_4.png)

**步骤 10**

假设你想像老式点阵打印机那样，一次打印一个字符。你可以将 `time` 模块与这里所学的内容结合起来使用。试试这个：

```python
import time
poem=open("/home/pi/Documents/Poem.txt")
lines=poem.read()
for lines in lines:
    print(lines, end="")
    time.sleep(.15)
```

这个输出看起来很有趣，而且很容易融入你自己的代码中。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_58_5.png)

## 写入文件

在 Python 中读取外部文件的能力当然很方便，但写入文件更加有用。使用 `write()` 函数，你可以将程序的结果输出到文件中，之后还可以将其 `read()` 读回 Python。

### 写入与关闭

`write()` 函数比 `read()` 稍微复杂一些。除了文件名之外，你还必须指定一个访问模式，以决定所涉及的文件是处于读取还是写入模式。

**步骤 1**

首先打开 IDLE，然后输入以下内容：

```python
t=open("/home/pi/Documents/text.txt","w")
```

将目标路径从 `/home/pi/Documents` 更改为你自己的系统路径。这段代码将使用变量 `t` 以写入模式创建一个名为 `text.txt` 的文本文件。如果该位置没有同名文件，它会创建一个；如果已存在同名文件，则会覆盖它，所以要小心。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_59_0.png)

**步骤 2**

现在你可以使用 `write()` 函数向文本文件写入内容。这与 `read()` 相反，它是写入行而不是读取行。试试这个：

```python
t.write("You awake in a small, square room. A single table stands to one side, there is a locked door in front of you.")
```

注意其中的 109，这是你输入的字符数量。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_59_2.png)

**步骤 3**

然而，实际的文本文件仍然是空白的（你可以打开它来检查）。这是因为你已将文本行写入文件对象，但尚未将其提交到文件本身。`write()` 函数的一部分要求是你需要将更改提交到文件；你可以通过输入以下内容来做到这一点：

```python
t.close()
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_59_1.png)

**步骤 4**

如果你现在用文本编辑器打开该文本文件，你会看到你创建的那行文本已经写入文件中。这为我们奠定了一些有趣可能性的基础：也许可以创建你自己的日志文件，甚至是冒险游戏的开端。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_59_3.png)

要扩展这段代码，你可以使用 `'a'`（访问或追加模式）重新打开文件。这将在原始行的末尾追加任何文本，而不是清空文件并创建一个新文件。例如：

```python
t=open("/home/pi/Documents/text.txt","a")
t.write("\n")
t.write("You stand and survey your surroundings. On top of the table is some meat, and a cup of water.\n")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_0.png)

你可以逐行扩展文本，每行以换行符（`\n`）结尾。完成后，使用 `t.close()` 结束代码，并在文本编辑器中打开文件查看结果：

```python
t.write("The door is made of solid oak with iron strips. It's bolted from the outside, locking you in. You are a prisoner!\n")
t.close()
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_1.png)

使用 `open()` 函数时，有各种类型的文件访问模式需要考虑。每种模式都取决于文件的访问方式，甚至光标的位置。例如，`r+` 以读写模式打开文件，并将光标放在文件开头。

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_2.png)

你可以将变量传递给你在 Python 中创建的文件。也许你想将 Pi 的值写入文件。你可以从 `math` 模块中调用 Pi，创建一个新文件，并将 Pi 的输出传递到新文件中：

```python
import math
print("Value of Pi is: ",math.pi)
print("\nWriting to a file now...")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_3.png)

现在，让我们创建一个名为 `pi` 的变量，并将 Pi 的值赋给它：

```python
pi=math.pi
```

你还需要创建一个新文件，用于将 Pi 写入其中：

```python
t=open("/home/pi/Documents/pi.txt","w")
```

记得将文件位置改为你自己特定的系统设置。

```python
pi=math.pi
t=open("/home/pi/Documents/pi.txt","w")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_4.png)

最后，你可以使用字符串格式化来调用该变量并将其写入文件，然后提交更改并关闭文件：

```python
t.write("Value of Pi is: {}".format(pi))
t.close()
```

从结果中你可以看到，你可以将任何变量传递给文件。

```python
t.write("Value of Pi is: {}".format(pi))
t.close()
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_60_5.png)

