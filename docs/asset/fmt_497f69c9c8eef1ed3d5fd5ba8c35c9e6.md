
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
"Error Number: {0}\r\n".format(e.errno) + 
"Error Text: {0}".format(e.strerror))
else:
    print("File opened as expected.")
    File.close();
```

此示例使用了一些高级特性。`import`语句从另一个文件获取代码。第10章将告诉你如何使用这一Python功能。

`open()`函数操作文件并通过`File`变量提供文件的访问。第15章将告诉你文件访问是如何运作的。由于`myfile.txt`在应用程序目录中不存在，操作系统无法打开它，并将告诉Python文件不存在。

尝试打开一个不存在的文件会生成一个`IOError`异常。这个特定异常提供了两个参数的访问：

- `errno`：提供作为整数的操作系统错误代码。
- `strerror`：包含作为人类可读字符串的错误信息。

`else`子句将信息捕获到变量`e`中，你可以根据需要访问它以获取额外信息。`except`块包含一个`print()`调用，将错误信息格式化为易读的错误消息。

如果你决定创建`myfile.txt`文件，则会执行`else`子句。在这种情况下，你使用一个消息表示文件已正常打开。代码随后关闭文件而不对其进行任何操作。

3. 选择运行（Run）：运行模块（Run Module）。

你会看到一个Python Shell窗口打开。应用程序显示了打开打开文件错误的信息，如图9-5所示。

```
Python 3.3.4 Shell

File Edit Shell Debug Options Windows Help

Python 3.3.4 (v3.3.4:77ff6241e526, Feb 20 2014, 18:13:51) [MSC v.
1600 64 bit (AMD64)] on win32

>>> help("credits" or "license") for more information.

>>> ======================================== RESTART
>>> Error opening file!
Error Number: 2
Error Text: No such file or directory
>>> 
Ln: 8 Col: 4
```

图9-5：尝试打开不存在的文件永远不会成功。

![](img/ec69aa1535cd82c735ee14abfc05048f_178_0.png)

# 获取异常参数列表

异常随提供的参数列表随异常类型以及发送者提供的内容而异。并不总是容易弄清楚通过这种方式可以获得哪些额外信息。处理此问题的方法之一是使用下面的代码打印一切（此示例也出现在下载源代码中，名为`GetExceptionArguments.py`）：

```python
import sys

try:
    File = open('myfile.txt')
except IOError as e:
    for arg in e.args:
        print(arg)
else:
    print("File opened as expected.")
    File.close();
```

（注：原文后续存在大量重复段落，已按要求合并核心逻辑翻译。）

# 166 第 II 部分：深入交流

以下步骤演示了如何使用多个`except`子句执行异常处理。此示例也出现在可下载源码`MultipleException2.py`中。

- 1. 打开一个Python文件窗口。

你可以在编辑器中看到并在其中输入以下代码。

- 2. 在窗口中输入以下代码 —— 每行完后按回车键：

```python
try:
    Value = int(input("Type a number between 1 and 10: "))
except ValueError:
    print("You must type a number between 1 and 10!")
except KeyboardInterrupt:
    print("You pressed Ctrl+C!")
else:
    if (Value > 0) and (Value <= 10):
        print("You typed: ", Value)
    else:
        print("The value typed is incorrect!")
```

![](img/ec69aa1535cd82c735ee14abfc05048f_181_0.png)

记住在此例中使用多个`except`子句。每个`except`子句处理不同的异常。你可以结合多种技术，某些子句仅处理一种异常，而其他子句处理多个异常。Python允许你使用最适合错误处理情况的方法。

- 3. 选择Run:Module。

你看到一个Python Shell窗口打开。应用程序提示你输入一个1到10之间的数字。

- 4. 输入Hello并按回车。

应用程序显示了错误消息（参见图9-1）。

- 5. 再次执行步骤3和4，但输入22而不是Hello。

应用程序输出了预期的错误消息（参见图9-2）。

- 6. 再次执行步骤3和4，但按下Ctrl+C、Cmd+C或你平台的替代键而不是输入任何内容。

应用程序输出了一条特定消息，告诉用户发生了什么，如图9-6所示。

- 7. 再次执行步骤3和4，但输入7，你提供了一个正确的值7。

## 第9章：处理错误
# 167

```
>>> Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
>>> Python 3.3.4 bit (v3.3.4:7ff622415426, Feb 10 2014, 18:13:51) [MSC v.
1600 64 bit (AMD64)] on win
>>> Type "copyright", "help" or "license" for more information.
>>> RESTART
>>>
>>> Type a number between 1 and 10: Hello
>>> You must type a number between 1 and 10!
>>> RESTART
>>>
>>> Type a number between 1 and 10: 22
>>> The value you typed is incorrect!
>>> RESTART
>>>
>>> Type a number between 1 and 10:
>>> You pressed Ctrl-C!
>>>
```

图9-6：

使用多个`except`子句使得处理特定错误成为可能。

## 处理从具体到不具体的异常

处理异常的一种策略是为所有已知异常提供特定的子句，并提供通用子句来处理未知异常。你可以在https://docs.python.org/3.3/library/exceptions.html#exception-hierarchy查看Python使用的异常层次结构。查看此表时，`BaseException`是最顶层的。大多数错误派自`Exception`。在处理问题时，你可以使用通用的`ArithmeticError`或更具体的`ZeroDivisionError`。

Python按`except`子句在源代码文件中出现的顺序进行评估。首先检查第一个子句，然后检查第二个子句，依此类推。以下步骤帮助你检查一个示例，它演示了使用正确异常顺序的重要性。在此例中，你执行会导致数学错误的任务。此示例也出现在可下载源码`MultipleException.py`中。

# 168 第 II 部分：深入交流

- 1. 打开一个Python文件窗口。

你可以在编辑器中看到并在其中输入示例代码。

- 2. 在窗口中输入以下代码 —— 每行完后按回车键：

```python
try:
    Value1 = int(input("Type the first number: "))
    Value2 = int(input("Type the second number: "))
    Output = Value1 / Value2
except ValueError:
    print("You must type a whole number!")
except KeyboardInterrupt:
    print("You pressed Ctrl+C!")
except ArithmeticError:
    print("An undefined math error occurred.")
except ZeroDivisionError:
    print("Attempted to divide by zero!")
else:
    print(Output)
```

代码从获取两个输入开始：`Value1`和`Value2`。两个`except`子句处理意外输入。第二个`except`子句处理数学异常，例如除零。如果一切顺利，`else`子句将执行并打印结果。

- 3. 选择Run:Module。

你看到一个Python Shell窗口打开。应用程序要求输入第一个数字。

- 4. 输入Hello并按回车。

如预期，Python显示了`ValueError`异常。然而，始终检查潜在的问题。

- 5. 再次选择Run:Module。

你看到一个Python Shell窗口打开。应用程序要求输入第一个数字。

- 6. 输入8并按回车。

你看到一个Python Shell窗口打开。应用程序要求输入第一个数字。

## 第9章：处理错误
# 184

- 7. 输入0并按回车。

应用程序输出了预期的错误消息（参见图9-2）。

- 8. 再次执行步骤3和4，但输入22而不是Hello。

应用程序输出了预期的错误消息（参见图9-2）。

- 9. 再次执行步骤3和4，但按下Ctrl+C、Cmd+C或你平台的替代键而不是输入任何内容。

应用程序输出了一条特定消息告诉用户发生了什么，如图9-6所示。

- 10. 再次执行步骤3和4，但输入7，你提供了一个正确的值7。

![](img/ec69aa1535cd82c735ee14abfc05048f_184_0.png)

# 第 II 部分：深入交流
# 185

![](img/ec69aa1535cd82c735ee14abfc05048f_185_0.png)

## 嵌套处理

处理异常的策略之一是为所有已知异常提供子句，并提供通用子句处理未知异常。你可以在https://docs.python.org/3.3/library/exceptions.html#exception-hierarchy查看Python使用的异常层次结构。查看此表时，`BaseException`是最顶层的。大多数错误派自`Exception`。在处理问题时，你可以使用通用的`ArithmeticError`或更具体的`ZeroDivisionError`。

Python按`except`子句在源代码文件中出现的顺序进行评估。首先检查第一个子句，然后检查第二个子句，依此类推。以下步骤帮助你检查一个示例，它演示了使用正确异常顺序的重要性。在此例中，你执行会导致数学错误的任务。此示例也出现在可下载源码`MultipleException.py`中。

## 嵌套异常

你需要你需要嵌套处理处理。。处理时，可以根据需要深度嵌套。使用双层的原因之一是需要从用户输入。以下步骤演示了这如何工作。

- 1. 打开一个Python文件窗口。

你可以在编辑器中看到并输入示例代码。

- 2. 在窗口中输入以下代码 —— 每行完后按回车键：

```python
TryAgain = True
while TryAgain:
    try:
        Value = int(input("Type a whole number."))
    except ValueError:
        print("You must type a whole number!")
        try:
            DoOver = input("Try again (y/n)?")
        except:
            print("OK, see you next time!")
            TryAgain = False
        else:
            if str.upper(DoOver) == "N":
                TryAgain = False
    except KeyboardInterrupt:
        print("You pressed Ctrl+C!")
        print("See you next time!")
        TryAgain = False
    else:
        print(Value)
        TryAgain = False
```

代码从创建一个输入循环开始。在应用程序中使用为此目的循环非常常见，因为你不希望每次输入错误时应用程序就结束。这是一个简化的循环，通常你会创建一个单独的函数来存放代码。

## 第9章：处理错误
# 186

- 2. 在窗口中输入以下代码 —— 每行完后按回车键：

```python
try:
    Value1 = int(input("Type the first number: "))
    Value2 = int(input("Type the second number: "))
    Output = Value1 / Value2
except ValueError:
    print("You must type a whole number!")
except KeyboardInterrupt:
    print("You pressed Ctrl+C!")
except ArithmeticError:
    print("An undefined math error occurred.")
except ZeroDivisionError:
    print("Attempted to divide by zero!")
else:
    print(Output)
```

# 第172 第二部分：交流技巧

`KeyboardInterrupt`异常会显示两条消息并通过将`TryAgain`设置为`False`自动退出。`KeyboardInterrupt`仅在用户按下旨在结束程序的特定组合键时发生。此时，用户不太可能继续使用应用程序。

![](img/ec69aa1535cd82c735ee14abfc05048f_187_0.png)

- 3. 选择运行（Run）：运行模块（Run Module）。

你看到一个Python Shell窗口。程序要求用户输入整数。

- 4. 输入Hello并按回车。

应用程序显示一条错误消息，并询问你是否要重试。

- 5. 输入Y并按回车。

应用程序要求你输入整数，如图9-9所示。

![](img/ec69aa1535cd82c735ee14abfc05048f_187_1.png)

图9-9
使用循环意味着应用程序可以从错误中恢复。

| Python 3.3.4 Shell |
| :--- |
| File Edit Debug Options Windows Help |
| Python 3.3.4 (v3.3.4:Tff6215e426, Feb 10 2014, 18:13:51) [MSC v 1600 64 bit (AMD64)] on win32 |
| Type "help" or "license()" for more information. |
| >>> RESTART ================== |
| >>> Type a whole number. Hello |
| You must type a whole number! |
| Try again (y/n)? |
| >>> Type a whole number. | |
| Ln: 8:Col: 21 |

- 6. 输入5.5并按回车。

应用程序显示错误消息，并询问你是否要重试。

- 7. 按Ctrl+C、Cmd+C或另一个组合键中断程序。

应用程序结束，如图9-10所示。注意该消息来自内部异常（inner exception）。应用程序永远不会到达外部异常（outer exception），因为内部异常处理了通用的异常处理。

- 8. 选择运行（Run）：运行模块（Run Module）。

你看到一个Python Shell窗口。程序要求用户输入整数。

## 第9章：处理错误

```
Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
Python 3.3.4 (v3.3.4:ff66215e426, Feb 10 2014, 18:13:51) [MSC v.1600 64 bit (AMD64)] on win32
Type "copyright", "credits" or "license()" for more information.
============================ RESTART =
>>>
>>> Type a whole number. Hello
```
