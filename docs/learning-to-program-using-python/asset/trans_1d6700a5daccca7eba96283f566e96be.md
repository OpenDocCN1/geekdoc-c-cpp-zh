
## 14.1 异常类层次结构

```python
except ValueError:  #not enough numbers entered
    print "Two numbers are required."
except ZeroDivisionError:   #tried to divide by 0
    print "Zero can't be a denominator."
else:
    print str(num1) + "/" + str(num2) + "= " + str(result)
#alternative format
#a tuple is required for multiple values
#printed values have floating numbers with one decimal point
print "%.1f/%.1f=%.1f" % (num1, num2, result)
```

正如你所见，你可以在同一个*try*块中拥有多个“异常捕获器”。你还可以在末尾使用*else*语句来表示如果一切顺利时执行的逻辑；不过，这并不是必须的。如前所述，整个*try*块也可以写成*if/elif*语句，但那将要求 Python 处理每条语句以检查是否匹配。通过使用异常，“默认”情况被假定为真，直到实际发生异常为止。这加快了处理速度。

你可以对这段程序进行的一项修改是简单地将其全部放入*try*块中。`raw_input()`变量（从用户键盘捕获输入）可以放置在*try*块内，通过强制将用户输入转换为浮点值来替代"num1"和"num2"变量，如下所示：

> 清单 14.2：使用 try 语句处理用户输入

```python
try:
    numerator = float(raw_input("Enter the numerator."))
    denominator = float(raw_input("Enter the denominator."))
```

这样一来，你就减少了需要编写、处理和测试的逻辑数量。你仍然拥有相同的异常；只是简化了程序。

最后，最好在编写代码时就将错误检查（如异常处理）包含在你的代码中，而不是作为事后的补救措施。编程的一个特殊“类别”涉及编写测试用例，以确保代码中考虑了大多数可能的错误，尤其是在代码变更或创建新版本时。通过提前规划，并在程序初期将异常和其他错误检查代码放入程序中，你可以确保在问题造成严重后果之前就被捕捉到。随着程序的演进更新你的测试用例，可以确保版本升级保持兼容性，且修复不会引发错误状况。

表 14.1 展示了 Python 库参考中的异常层次结构。当发生异常时，它从尽可能低的级别（子级）开始，向上（通过父级）传播，等待被捕获。这对程序员意味着几件事：

- 1. 如果你不知道可能发生的异常是什么，你始终可以捕获更高级别的异常。例如，如果你不知道前例中的 `ZeroDivisionError` 是一个“独立”的异常，你可以使用 `ArithmeticError` 作为异常并捕获它；如图所示，`ZeroDivisionError` 是 `ArithmeticError` 的子级，而 `ArithmeticError` 又是 `StandardError` 的子级，依此类推，直到层次结构的顶端。
- 2. 多个异常可以以相同的方式处理。承接上面的例子，假设你计划使用 `ZeroDivisionError` 并想包含 `FloatingPointError`。如果你希望针对这两种错误采取相同的操作，只需使用父异常 `ArithmeticError` 作为要捕获的异常即可。这样，当发生浮点数错误或零除错误时，你就无需为每种错误单独编写案例。当然，如果你有需求或意愿分别捕获每一种异常，也许是因为你希望采取不同的操作，那么为每种情况编写异常是没问题的。

表 14.1：异常层次结构

| 异常层次结构 |
| :--- |
| BaseException |
| ├─ SystemExit |
| ├─ KeyboardInterrupt |
| ├─ GeneratorExit |
| └─ Exception |
|    ├─ StopIteration |
|    ├─ StandardError |
|    │  ├─ BufferError |
|    │  ├─ ArithmeticError |
|    │  │  ├─ FloatingPointError |
|    │  │  ├─ OverflowError |
|    │  │  └─ ZeroDivisionError |
|    │  ├─ AssertionError |
|    │  ├─ AttributeError |
|    │  ├─ EnvironmentError |
|    │  │  ├─ IOError |
|    │  │  ├─ OSError |
|    │  │  ├─ WindowsError (Windows) |
|    │  │  └─ VMSError (VMS) |
|    │  ├─ EOFError |
|    │  ├─ ImportError |
|    │  ├─ LookupError |
|    │  │  ├─ IndexError |
|    │  │  └─ KeyError |
|    │  ├─ MemoryError |
|    │  ├─ NameError |
|    │  │  └─ UnboundLocalError |
|    │  ├─ ReferenceError |
|    │  ├─ RuntimeError |
|    │  │  └─ NotImplementedError |
|    │  ├─ SyntaxError |
|    │  │  ├─ IndentationError |
|    │  │  └─ TabError |
|    │  ├─ SystemError |
|    │  ├─ TypeError |
|    │  ├─ ValueError |
|    │  ├─ UnicodeError |
|    │  │  ├─ UnicodeDecodeError |
|    │  │  ├─ UnicodeEncodeError |
|    │  │  └─ UnicodeTranslateError |
|    ├─ Warnings (various) |

### 14.2 用户定义的异常

我不会花太多时间讨论这个问题，但 Python 确实允许程序员创建自己的异常。你可能不常需要做这件事，但在必要时拥有这个选项是不错的。然而，在创建自己的异常之前，请确保没有适合你需求的内置异常。它们经过多年的“实战检验”，不仅工作有效，而且针对性能进行了优化，并且没有错误。

创建自己的异常涉及面向对象编程，这将在下一章中涵盖。为了创建一个自定义异常，程序员确定使用哪个基础异常作为继承的类，例如，为负数或虚数创建异常可能属于 `ArithmeticError` 异常类。要创建自定义异常，只需继承基础异常并定义它的行为。清单 14.3 给出了创建一个自定义异常的例子：

清单 14.3：定义自定义异常

```python
import math  #necessary for square root function

class NegativeNumberError(ArithmeticError):
    """Attempted improper operation on negative number"""
    pass

def squareRoot(number):
    """Computes square root of number. Raises
    NegativeNumberError
    if number is less than 0."""
    if number < 0:
        raise NegativeNumberError, \
            "Square root of negative number not permitted"

    return math.sqrt(number)
```

第一行创建了自定义异常 `NegativeNumberError`，它继承自 `ArithmeticError`。因为它继承了基础异常的所有特性，你不需要定义其他内容，因此使用了表示不执行任何操作的 `pass` 语句。然后，为了使用新的异常，创建了一个函数（`squareRoot()`），如果参数值小于 0，则引发 `NegativeNumberError`；否则，它返回该数的平方根。

## 第 15 章

# 面向对象编程

### 15.1 学习 Python 类

类是面向对象编程的最基本组件。之前，你学习了如何使用函数让程序执行某些操作。现在，你将进入庞大且略显复杂的面向对象编程（OOP）世界。

老实说，我花了几个月时间才掌握对象。当我最初学习 C 和 C++ 时，我表现得很棒；函数对我来说很直观。由于在 90 年代初玩过 BASIC，我意识到函数就像子程序，所以没有太多新东西要学。然而，当我修读 C++ 课程开始谈论对象、类以及 OOP 的所有新功能时，我的成绩肯定受到了影响。

一旦你学会了 OOP，你会发现它实际上是一个相当强大的工具。此外，许多 Python 库和 API 都使用类，因此你至少应该能够理解代码在做什么。

关于 Python 和 OOP 需要注意的一点是：在你的代码中使用对象并非强制性的。正如你之前所见，Python 使用函数也能运行得很好。与 Java 等语言不同，你不必局限于一种做事方式；你可以根据需要在同一程序中混合使用函数和类。这使得你构建代码

