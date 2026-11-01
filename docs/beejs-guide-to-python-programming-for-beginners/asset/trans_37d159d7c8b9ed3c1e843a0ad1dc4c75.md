
```
try:
    print("This is what we're trying to do")
    print("and where exceptions might occur.")

except:
    print("Caught an exception!")

else:
    print("This only runs if there was no exception.")

finally:
    print("This runs no matter what.")
```

使用 else 可以在发生异常时让你更好地控制程序的流程。

## 14.13 异常对象

### 问题解决步骤：理解问题

到目前为止，我们已经讲解了捕获异常，在你使用 Python 的 99% 时间里，这就是你需要知道的全部内容。

但这并不意味着我们就此停止。成为一名优秀开发者的一部分，是对这些东西的工作原理有一个良好的心理模型，而不仅仅是记住一些使用模式。更深入的理解会让你受益匪浅。

所以让我们谈谈 Python 中异常是如何由对象表示的。

我们已经在上面提到过这一点，在我们谈论从异常中获取更多信息的地方。

我们发现有一个名为 ZeroDivisionError 的类，还有一个名为 ValueError 的类。的确，如果我们想要的话，可以直接创建这些类的新实例：

```
e = ValueError()  # Construct a new ValueError object
```

有一整套可直接使用的异常⁴，但如果没有一个合适，你也可以传入一些信息来创建一个新的 Exception：

```
e = Exception('Something went horribly awry')
```

最后，如果你愿意，你可以创建自己的新异常类。你不必这样做——你可以使用 Exception 或其他任何预先存在的异常。

但如果你自己创建，唯一的条件是它们必须继承自 Exception 基类。

哇哦，Beej，你在说什么？

好吧，你抓到我了。我在那里用了一些面向对象编程的术语。现在，我们会在后面的章节讨论这所有含义是什么意思，但现在，请相信我，你需要声明你的新异常，你必须使用类似这样的语法：

```
class MyAwesomeException(Exception):  # <-- Note "(Exception)"
    pass
```

这是在告诉 Python，“我正在创建一个名为 MyAwesomeException 的新类，但是，事情是这样的，MyAwesomeException 是一个 Exception。”

另外，如果你有一个构造函数，确保这样做：

```
class MyAwesomeException(Exception):  # <-- Note "(Exception)"
    def __init__(self, *args):  # <-- Get all positional args
        print("In my constructor")
```

但如果我们指定一个超出范围的值，我们会得到：

```
Enter a number 0-9: -1
Exception: out of range
```

如果我们输入字母 a 呢？那会在调用 int() 时出错……但它会以 ValueError 出现，就像我们在本章前面看到的那样。

而且，嘿！巧合的是，我们在上面的代码中已经捕获了 ValueError。

让我们试试：

```
Enter a number 0-9: a
Exception: invalid literal for int() with base 10: 'a'
```

捕获到了！注意错误信息与“超出范围”异常不同，所以我们可以区分。

所以，嘿！我们现在知道如何：

- 捕获异常
- 创建新异常
- 引发异常

到目前为止还不错！

## 14.15 重新引发异常

有时你可能对异常发生感兴趣，但又不想让它停止。你希望它继续传播，以便调用方也能看到它。

我们可以在 catch 中使用单独的 raise 很简单地做到这一点。

下面的函数如果发生 ValueError 会记录它，但随后会重新引发它，以便主代码中的 try 块可以捕获它：

```
def makeint(x):
    try:
        return int(x)
    except ValueError:
        print("Hey, I saw an exception!")
        print("But I'll let someone else handle it.")
        raise  # Re-raise the exception
try:
    x = makeint("bee")
except ValueError as v:
    print(f'Exception: {v}')
```

这会输出：

```
Hey, I saw an exception!
But I'll let someone else handle it.
Exception: invalid literal for int() with base 10: 'bee'
```

## 14.16 项目实现

如果需要，请回顾本章开头的项目规范。

### 问题解决步骤：理解问题

这里最大的挑战是如何对所有用户输入进行完整的错误检查，以确保一切合理？

可能出现的所有问题是什么？

先自己列一个清单，然后你可以将其与我下面的清单进行比较。

前方剧透！

我能想到的情况有：

- 用户没有输入正确数量的命令行参数。
- 用户为第二个命令行参数输入了非数字。
- 用户输入的文件名不存在。
- 用户输入了非正数。
- 文件不是普通文件（例如它是目录或其他特殊文件）。
- 用户没有权限读取文件。
- 用户输入的数字大于文件中的行数。

其中一些你可以用简单的 if 语句处理。其他一些我们必须用异常来捕获。

关于输入的数字大于文件中的行数时会发生什么，这是一个很好的问题。规范中没有说明。所以我们应该向规范的创建者寻求澄清。

> “嘿，BeeJ！规范中没有说明如果指定的行数大于文件中的行数该怎么办。这种情况下我们该怎么做？”

我们这样做：我们将在用户指定的行数或文件末尾处停止输出，以先到者为准。无论哪种情况，都不需要向用户发送消息。

好的，让我们计划一下！

### 问题解决步骤：制定计划

根据规范，程序可以分解为若干部分。

- 读取用户输入
- 打开文件以便读取
- 读取到用户指定的行数（或 EOF）为止的行数

对于这些部分中的每一个，我们都必须进行输入验证，并在出现问题时通知用户。

### 问题解决步骤：执行计划

其中一些内容我们以前见过，所以我们会略过一点。

首先，让我们从命令行获取用户输入，检查是否传递了正确数量的参数，并检查输入以确保其合理。

```
import sys

if len(sys.argv) != 3:
    print("usage: head.py filename count")
    sys.exit(1)

filename = sys.argv[1]
total_count = int(sys.argv[2])

if total_count < 1:
    print("head.py: count must be a positive integer")
    sys.exit(2)
```

到目前为止还不错，但我们缺少一个错误情况。你看到了吗？

如果用户为 count 输入“bananas”怎么办？如果我们尝试运行它来看看会发生什么，果然，我们会得到一个异常。

```
Traceback (most recent call last):
  File "foo.py", line 8, in <module>
    total_count = int(sys.argv[2])
ValueError: invalid literal for int() with base 10: 'bananas'
```

这是我们之前见过的 ValueError 异常。让我们修改代码来捕获该异常并处理它。

```
import sys

if len(sys.argv) != 3:
    print("usage: head.py filename count")
    sys.exit(1)

filename = sys.argv[1]

try:
    total_count = int(sys.argv[2])
except ValueError:
    print("head.py: count must be a positive integer")
    sys.exit(2)

if total_count < 1:
    print("head.py: count must be a positive integer")
    sys.exit(2)
```

搞定！这修复了它。而且这段代码可以工作，但...

注意到有什么乱的地方吗？没错——我们确实重复了很多。让我们重构一下，看看能否去掉那些重复的行。

一个选择是在任一情况下设置一个标志，如果有错误则设为 True，然后打印消息并退出。这会起作用，而且也不是一个糟糕的解决方案。

但我们可以更聪明一些，实际上让异常处理器为我们完成所有工作，只需在 total_count 小于一时简单地引发 ValueError 异常即可。这样在两种情况下我们都会得到 ValueError，并且可以在一个地方处理它。

```
try:
    total_count = int(sys.argv[2])
    if total_count < 1:
        raise ValueError()
except ValueError:
    print("head.py: count must be a positive integer")
    sys.exit(2)
```

看看这个。如果 int() 引发异常，我们会捕获它。如果我们自己引发异常，我们也会捕获它。而且所有用于测试输入值正确性的逻辑都很好地放在同一个 try 块中。

好！我们已经获得了正确的输入代码。让我们继续下一步，打印文件中的行。

我们可以先简化问题，只打印所有行，先不考虑计数。

让我们使用之前打印文件的代码：

```
with open(filename) as f:
    for line in f:
        print(line, end="")
```
