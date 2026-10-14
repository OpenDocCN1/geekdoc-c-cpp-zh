

## 第 12 章

### 为你的代码编写文档

本章节中的部分内容借鉴自 *《Dive Into Python》*，这是一本面向资深编程人员的免费 Python 编程书籍。其他信息则来自 Python 风格指南以及 Python 增强提案（PEP）257。（请注意，本节中提供的信息可能与官方 Python 指南相悖。这些信息以通用格式呈现关于文档字符串（docstring）的内容，并使用了笔者开发的约定。鼓励读者查阅官方文档以获取更多详细信息。）

你可以通过为 Python 对象提供文档字符串（docstring）来记录它。文档字符串只是一个三重引号包裹的句子，用于简要概述该对象。该对象可以是函数、方法、类等。（在本节中，“函数”一词用于指代实际的函数或方法、类或其他 Python 对象。）

#### 列表 12.1：文档字符串示例

```python
def buildConnectionString(params):
    """ Build a connection string from a dictionary of parameters.
    Returns string. """
```

如前所述，三重引号表示多行字符串。起始引号和结束引号之间的所有内容都是单个字符串的一部分，包括回车符和其他引号字符。你通常会在定义文档字符串时看到它们的使用。

三重引号之间的所有内容都是该函数的文档字符串，用于记录该函数的功能。如果存在文档字符串，它必须是函数中定义的第一件事（即冒号后的第一件事）。

从技术上讲，你不需要为函数提供文档字符串，但你应该这样做；文档字符串在运行时可作为函数的属性获取。许多 Python IDE 利用文档字符串提供上下文敏感文档，这样当你输入函数名称时，其文档字符串会作为工具提示出现。

引自 Python 风格指南：

> *“脚本的文档字符串应能用作其‘用法’消息，当脚本在参数错误或缺失（或可能带有 '-h' 选项，即 'help'）时调用时打印出来。此类文档字符串应记录脚本的功能和命令行语法、环境变量以及文件。用法消息可以相当详细（几屏的内容），并且应足以让新用户使用该命令，同时也应为高级用户提供所有选项和参数的完整快速参考。”*

老实说，我并不是总能遵守这条规则。我通常只写一句简短的说明，描述函数、方法、类等旨在完成的任务。然而，随着程序的演变，我试图增强文档字符串，添加它接收的输入以及输出（如果有的话）。

文档字符串有两种形式：单行和多行。单行文档字符串正是如此：信息不需要大量的描述性文本来解释正在发生的事情。即使字符串适合在一行内显示，也使用三重引号，以便日后容易扩展。结束引号与开始引号在同一行，因为这样看起来更美观。文档字符串前后都没有空行。文档字符串是一个以句号结尾的短语。它描述函数的效果，如同命令（“执行此操作”，“返回该值”）。它不应重复函数的参数（或实参），但如果存在，可以说明预期的返回值。

#### 列表 12.2：文档字符串的良好使用

```python
def kos_root():
    """Return the pathname of the KOS root directory."""
    global _kos_root
    if _kos_root: return _kos_root
    # ...
```

再次，我必须承认我在这方面做得不是最好。我通常将结束引号放在单独的一行，并且在文档字符串和实际代码开始之间留一个空格；这使得添加信息更容易，并有助于将文档字符串与代码块的其他部分区分开来。是的，我有点随意。然而，只要你在整个项目中保持一致，盲目遵循“Python 方式”并不是必须的。

顺便提一下，将结束引号放在单独一行并不完全错误；多行文档字符串（根据 PEP 257）应该这样处理，而单行文档字符串则应将结束引号放在同一行。我只是习惯了在编写文档字符串时使用一种方法，这样我不必每次都思考。

多行文档字符串的开始方式与单行文档字符串相同。第一行是摘要，但随后跟一个空行。空行之后可以进行更具描述性的讨论。空行用于将摘要与描述性信息分隔开，供自动索引工具使用。它们将使用单行摘要来创建文档索引，从而减少程序员的工作量。

在空行后继续你的文档字符串时，请确保遵循 Python 的缩进规则，即在空行之后，你的所有文档字符串信息都应缩进到与初始三重引号相同的位置。否则，运行程序时会出错。

来自 Python 风格指南的更多信息：

> 模块的文档字符串通常应列出该模块导出的类、异常和函数（以及其他任何对象），并附上每行简要摘要。（这些摘要通常比对象文档字符串中的摘要行提供的细节少。）
>
> 函数或方法的文档字符串应总结其行为，并记录其参数、返回值（如有）、副作用、抛出的异常以及调用时的限制（如适用）。应标明可选参数。应记录关键字参数是否是接口的一部分。

类的文档字符串应总结其行为并列出公共方法和实例变量。如果该类旨在被子类化，并且拥有供子类使用的附加接口，则应单独列出该接口（在文档字符串中）。类的构造函数应在其 `__init__` 方法的文档字符串（即当类首次调用时调用的“初始化”方法）中记录。各个方法应由其自己的文档字符串记录。

如果一个类继承自另一个类，并且其行为主要继承自该类，其文档字符串应提及这一点并总结差异。使用动词“覆盖”（override）表示子类方法替代了父类方法且不调用父类方法；使用动词“扩展”（extend）表示子类方法调用了父类方法（除了自己的行为外）。

Python 对大小写敏感，且参数名可用于关键字参数，因此文档字符串应记录正确的参数名。最好在单独的一行列出每个参数，并用两个破折号将名称与描述分开。

如果你读到了这里，我将帮你总结刚刚学到的内容。Python 拥有一种称为“文档字符串”的文档功能，它允许你使用注释来自我记录源代码。一些 Python IDE，如 Stani’s Python Editor (SPE)，可以使用这些文档字符串来创建你的源代码结构列表，例如类和模块。这使程序员的工作更轻松，因为创建帮助文件和其他程序文档时需要更少的工作。文档索引器可以从你的代码中提取文档字符串并为你创建列表，或者你甚至可以自己编写脚本来生成它。你还能够手动读取对象的文档字符串，方法是调用对象的 `__doc__` 属性；这基本上就是上述 IDE 和索引器所做的。列表 12.3 展示了 Python 的 random 模块的文档字符串是什么样子的。

#### 列表 12.3：Python random 模块的文档字符串

```python
>>> import random
>>> print(random.__doc__)
Random variable generators.
Random -- uniform distribution over [0.0, 1.0).
...
[PAGE 94]
uniform within range

integers

- sequences
  - pick random element
  - pick random sample
  - generate random permutation

distributions on the real line:

- uniform
- triangular
- normal (Gaussian)
- lognormal
- negative exponential
- gamma
- beta
- pareto
- Weibull

distributions on the circle (angles 0 to 2 pi)

- circular uniform
- von Mises

General notes on the underlying Mersenne Twister core generator:
* The period is 2**19937-1.
* It is one of the most extensively tested generators in existence.
* Without a direct way to compute N steps forward, the semantics of jumpahead(n) are weakened to simply jump to another distant state and rely on the large period to avoid overlapping sequences.
* The random() method is implemented in C,
```

