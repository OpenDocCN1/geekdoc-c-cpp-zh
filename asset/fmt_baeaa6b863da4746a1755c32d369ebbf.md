
`target_file.write("Using the write function multiple times will write multiple lines to the document. \n")`

就像我们可以使用 `for` 循环从文本文档读取一样，我们也可以使用 `for` 循环向文本文档写入。我们可以创建一个包含字符串的列表进行写入，然后使用 `for` 循环写入文档，这将我们的列表项写入不同的行。

```python
list_to_write = ["This", " is", " our", " word", " list"]
```

```python
for w in list_to_write:
    target_file.write(w)
```
`target_file.close()`

记住，你可以使用我们在字符串格式化章节中讨论过的转义字符和格式化选项来格式字符串写入文本文档的方式。

## 10.3 - 缓冲区大小/二进制文件

当你开始编写程序时，你可能只处理不占用大量内存的小型文本文件。然而，当你开始处理更大的数据集时，你会想要知道如何指定缓冲区大小。缓冲允许我们分小块读取，这样它就不会占用很多内存。我们通过使用 `read()` 函数并传入一个数值来指定缓冲区大小。假设我们想一次读取 20 字节。

```python
text = open("test_text.txt", "r")
print(text.read(20))
```

如果你想遍历整个文档，你需要使用 `while` 循环，将结束条件设置为文件，然后通过再次调用该函数更新 `text` 变量的值以获取下 20 字节。

```python
while text := text.read(20):
    print(text)
```

## 11.1 - 递归

每你需要处理一组数据时，必须以某种方式遍历该序列。你已经知道如何使用 `for` 循环来做到这一点。构建一个 `for` 循环并执行某些操作直到满足停止条件，这被称为处理顺序数据的迭代方法。然而，处理数据序列还有另一种方法：你也可以可以创建一个递归函数。

Python 允许你在函数定义内部调用自己。在函数调用自身的任何实例中都会使用“递归”一词。递归将继续执行函数内部指定的动作，直到满足结束条件。大多数迭代函数都可以写成递归函数，但递归函数的终止方式不同。`for` 循环会在序列结束时自然终止，但除非达到指定的结束条件，否则递归函数可能会持续进行。重要的一点是递归函数必须指定一个“基准情况（base case）”。基准情况就是递归结束时发生的情况。

让我们看看如何在 Python 中创建递归函数。假设我们需要一个函数来列出给定数字的阶乘。一个数字的阶乘是小于或等于该数字的所有数字的乘积。例如，3 的阶乘是 3 * 2 * 1。这是一个相对简单的计算，但在创建阶乘函数的递归实现之前，让我们先创建一个该函数的迭代版本，以查看我们需要采取的步骤。

如果我们正在创建该算法的迭代版本，我们需要执行以下操作：

- 创建一个变量，将其与序列中的下一个数字相乘。
- 将该变量初始化为一。
- 使用 `range` 函数和 `for` 循环，从值2（因为索引从0开始）运行到目标数字加一。
- 对于范围内的每个索引，将变量乘以当前序列索引，然后移动到范围中的下一个项目。

阶乘函数的迭代版本可能像这样：

```python
def factorial_calculation(num):
    current_value = 1
    for i in range(1, num + 1):
        current_value *= i
    return current_value

print(factorial_calculation(5))
```

当我们使用迭代方法时，我们需要对序列中的每个元素执行所需的操作。相比之下，当我们创建一个递归函数时，只需要指定基准情况以及函数在基准情况为真之前应该执行的操作。我们继续调用该函数，直到满足基准情况。

阶乘计算函数的递归版本可能像这样：

```python
def recursive_calculation(num):
    if num != 1:
        return num * recursive_calculation(num - 1)
    else:
        return num

print(recursive_calculation(5))
```

我们的基准情况/终止情况是相乘的数字达到了1。否则，我们获取输入数字并乘以1减去该数字，然后函数调用它自己。当我们运行程序时，这将返回值 120。

递归的概念可能有些令人困惑，但你处理递归函数越多，就越能理解它们。建议你花些时间尝试自己编写递归函数。

## 11.2 - Lambda 函数

有时，你可能会发现你需要一个函数来执行相对简单的任务。在编写整个函数似乎没有必要的情况下，你可以使用 Lambda 函数。Lambda 函数是没有名称的函数，但它们的操作方式与普通函数一样。它们通常被用作快速的、一次性的函数。

Lambda 函数可以接受你需要的任何数量参数，但它们只包含单个表达式，因此使用 lambda 函数只执行一段代码。注意，lambda 表达式返回函数对象。

Lambda 函数仅通过使用 `lambda` 关键字创建。这是创建 lambda 表达式的通用格式：

`lambda arguments: expression`

记住，在处理 lambda 函数时只能使用单个表达式。你不能将任何语句与 lambda 运算符结合。然而，从 lambda 函数返回值并将其赋值给变量是很容易的，这只需要通过在 lambda 关键字之前使用赋值运算符即可完成。下面的代码声明了一个作用于参数变量 `num` 的 lambda 函数，而冒号后面的代码是函数应该如何操作的逻辑。然后它将 lambda 函数返回的值分配给变量，该变量可以作为参数传递给其他函数。

```python
multiplied_value = lambda num: num * 9
print(multiplied_value(3))
```

当你需要一个只需要很短时间的函数时，Lambda 函数非常有用。Lambda 函数的一个常见用途是当你需要为高阶函数赋予特定功能时，因为 lambda 函数可以在普通函数内部使用。Lambda 函数还可以与其他 Python 内置函数（如 `filter()` 和 `map()` 函数）一起使用。

## 11.3 - 高级字典处理：Min, Max 和 Sort

在处理字典时，你可能会发现你需要根据它们在字典中的排名检索某些键或值，或者你需要对字典进行排序。由于没有快速的函数可以完成这些任务，我们将花一点时间涵盖如何获取最小/最大字典项，以及如何排序字典。让我们先创建一个字典。

```python
ex_dict = {"key1": 31, "key2" : 29, "key3" : 45, "key4": 97, "key5": 72}
```

为了获取最小或最大的字典项，我们可以将字典转换为元组列表：

```python
min_entry = min(ex_dict.items(), key=lambda item: item[1])
max_entry = max(ex_dict.items(), key=lambda item: item[1])
print("Minimum entry:", min_entry)
print("Maximum entry:", max_entry)
```

如果你想对字典排序，可以使用 `sorted()` 函数：

```python
sorted_dict = sorted(ex_dict.items(), key=lambda item: item[0])
print(sorted_dict)
```

（注：此处根据原文逻辑对“由于没有快速的函数可以完成这些任务，我们将花一点时间涵盖如何获取最小/最大字典项，以及如何排序字典”后的描述进行了翻译）

## 11.4 - 线程 (Threading)

线程是在另一个旁边运行多个进程的想法。在代码并非精确执行的情况下，将进程拆分为不同的线程可以提供清晰度。线程可能会增强程序的执行速度，但它在所有情况下并不都适用。为了查看线程如何工作，让我们首先编写一个基础程序，允许我们在执行某些动作的同时跟踪它们所需的时间。我们可以使用内置的 `time` 模块和 `perf_counter()` 函数来跟踪执行的时间。当我们第一次调用 `perf_counter()` 时，它将开始记录时间，当我们第二次调用 `perf_counter()` 时，它将停止。

```python
from time import perf_counter, sleep
list_1 = ['microphone', 'cup', 'TV', 'wallet', 'hat']
start = perf_counter()
def print_function():
    sleep(1)
    for i in list_1:
        print("Value: " + i)
    print()
print_function()
end = perf_counter()
print('Time to finish: {} seconds '.format(round(end-start, 2)))
```

运行此程序所需大约是5秒。

如果我们有两个列表并想以同样的方式打印它们呢？你可能认为这会加倍我们的运行时间。然而，并非如此。我们可以利用计算机未使用的额外资源创建另一个线程，并在更短时间内运行第二个函数调用。当任务是 I/O 密集型的或只是等待输入输出完成时，我们应该在处理时间上看到收益。在 I/O 任务期间，计算机通常只是在等待输入，并没有实际大量的计算资源。线程允许我们在等待 I/O 任务完成时继续执行其他操作。我们可以通过使用 threading 模块中的 `Thread()` 函数创建线程。然后我们通过指定 `target` 将所需的函数传入线程。语法应该如下：

```python
import threading
thread_1 = threading.Thread(target=desired_function)
```

将线程实例保存为变量后，你需要在变量上使用 `start` 函数：

```python
thread_1.start()
```

我们需要确保在计算运行时间之前这些方法已经完成。我们可以通过使用 `join()` 函数来实现这一点。

```python
thread_1.join()
```

现在我们可以更新上面的代码来创建多个线程，并查看代码执行需要长时间。让我们创建一个 `for` 循环来多次运行我们创建的代码。

```python
from time import perf_counter, sleep
import threading
```

```python
list_1 = ['microphone', 'cup', 'TV', 'wallet', 'hat']
```

```python
start = perf_counter()
```

```python
def print_function():
    sleep(1)
    for i in list_1:
        print("Value: " + i)
    print()
```

```python
t1 = threading.Thread(target=print_function)
t2 = threading.Thread(target=print_function)
t3 = threading.Thread(target=print_function)
t4 = threading.Thread(target=print_function)
```

```python
t1.start()
t2.start()
t3.start()
t4.start()
```

```python
t1.join()
t2.join()
t3.join()
t4.join()
end = perf_counter()
print('Time to finish: {} seconds'.format(round(end-start, 2)))
```

如果我们运行这个程序，会发现它运行只需要大约一秒钟。这是因为计算机的输入输出操作花费的时间非常短，当程序在等待 `sleep` 时间时，可以在其他线程中执行打印操作。

线程无法加速 CPU 密集型任务（CPU-bound tasks）的速度。因此，对于正在计算数据的任务，如果使用多线程，可能需要更长时间才能完成。

## 11.5 - 软件包与 Pip 包管理器

Python 最优特性之一是，它允许你轻松且高效地在自己的 Python 项目中安装和使用他人编写的代码。Python 社区为其他开发者创建了许多实用且强大的函数和工具。你能想象一下，如果你必须自己手写每一个想要使用的函数会是什么吗？如果是这样，构建复杂的项目将耗费你永远的时间。坦率地说，在 Python 中，有一种简单的方法，通过 `Pip` 包管理器来安装模块和库（即他人编写的脚本和脚本集合）。

如果从源码包（例如 Python 官网）安装了 Python，你应该能够立即访问 `Pip`。你可以通过打开命令行并运行以下命令来确认：

```bash
pip --version
```

如果你的系统中已经存在 `Pip`，它将给你版本号以及它的安装位置。如果你的系统中没有安装 `Pip`，你需要安装它。请查找适用于你特定操作系统和 Python 版本的安装说明。在本书的后面，我们将使用 `Pip` 安装一些模块并处理一些示例项目，因此请确保已正确安装了 `Pip`。

当你想要用 `Pip` 安装 Python 库或模块时，只需打开命令行并按照如下语法编写：

```bash
pip install ItemToInstall
```

你还可以通过等号运算符指定所需的版本来安装特定版本。

```bash
pip install ItemToInstall==1.5
```

输入 `pip help` 将提供你可以使用的所有选项和命令，`pip search SearchTerm` 将允许你搜索想要安装的特定包，并为你提供该包的简要描述。`pip list` 将提供所有已安装包的列表。

例如，假设你正在运行一个项目，需要告诉其他人需要安装哪些包。你可以使用 `pip freeze` 命令来实现。这将把所有的包名和版本号整合在一个文件中。这意味着你可以执行以下操作，让 `pip` 生成一个包含你所有包名和版本的文本文件：

```bash
pip freeze > requirements.txt
```

你还可以下载其他项目的 requirements 文件，并使用 `pip` 安装必要的文件。语法如下：

```bash
pip install -r requirements_file.txt
```

你还可以使用 `pip list --outdated` 来检查哪些包已经过时。然后你可以检查并更新这些过时的包。

如果你经常使用 `pip`，你安装的包将应用于全局——贯穿整个系统。但是，如果你对安装的包有更大的控制需求怎么办呢？假设你正在的一个项目与某个版本的库兼容，而另一个项目不兼容。全局安装该包将迫使你的项目在不同版本之间做出选择。坦率地说，有一种处理这个问题的方法；我们可以设置虚拟环境，以增强对使用哪些包的控制力。

## 11.6 - 虚拟环境

虚拟环境允许你将依赖项拆分为隔离的、包含的软件包集合。正如前面提到的，这在创建依赖于特定版本库或包的项目时非常有用。有了虚拟环境，你只可以在环境中安装你需要的库和模块，它们的存在不会影响你计算机上的任何其他环境。

在 Python 中设置虚拟环境最简单的方法是使用名为 `virtualenv` 的包。可以通过以下命令将其安装到你的全局 Python 中：

```bash
pip install virtualenv
```

将所有创建的环境放在一个地方将是有益的，这样更容易找到它们。因此，建议你打开命令行并创建一个目录来放置你的环境：

```bash
mkdir Environments
```

```bash
cd Environments
```

```bash
virtualenv test_environment
```

创建后，你需要激活它才能使用。在这种情况下，我们会激活：

```bash
source test_environment/bin/activate
```

如果你没有看到（提示符），可以使用 `python` 命令检查你当前处于哪个环境中。如果你成功激活了虚拟环境并运行 `pip list`，你应该看到已安装列表除了 `setuptools` 包之外几乎是空的。让我们尝试使用以下命令向新环境中安装一些包：

```bash
pip install requests
pip install numpy
pip install PIL
```

如果我们再次运行 `pip list`，就会看到安装的库现在包含在列表中。与全局包一样，我们可以使用 `pip freeze` 命令保存环境包的列表。

最后，你可以通过输入 `deactivate` 退出虚拟环境，并通过输入以下命令删除它：

```bash
rm -rf test_environment
```
