
## 6.3 使用 print 调试

调试的另一种强大技术（单步执行和检查程序变量的替代方案）是在代码中精心选择的位置插入 `print` 函数。然后，通过检查程序的输出，你可以检查算法是否在执行你期望执行的操作。请明确以下点：

- 你必须对问题有一个清晰的解决方案，并在调试程序之前知道应该发生什么。在考虑编写代码之前，先在纸上解决问题（也许可以使用流程图来记录你采取的步骤）。编写程序并不能解决问题——它只是将你将执行的手动步骤自动化。因此，首先确保你有一个行之有效的纸笔手动解决方案。编程就是让这些手动步骤自动发生。
- 不要编写“话匣筒”。话匣筒在其主要任务之外增加了有益的负担，它还会要求用户输入或打印输出，而在这些情况下，如果它只是闭嘴并快速完成工作会更有用。

例如，我们见过像 `max` 和 `abs` 这样的内置函数。如果这些函数在执行任务时提示用户输入或打印其结果，那么它们对其他程序来说将不再是有用的构建块。

所以，一个好的建议是避免在有益函数内部调用 `print` 和 `input`，除非你的函数的主要目的是执行输入输出。这条规则的唯一例外可能是临时在你的代码中点缀 `print` 调用，以帮助调试和理解代码运行时正在发生什么，但一旦让一切正常工作，就可以删除它们。

## 6.4 组合

正如你现在所预期的，你可以在一个函数内部调用另一个函数。这种能力被称为组合。

例如，我们将编写一个函数，接收两个点（圆心和圆周上一点），并计算圆的面积。

如何像计算机科学家一样思考：使用 Python 3 学习文档，第 3 版

假设中心点存储在变量 `xc` 和 `yc` 中，圆周点在 `xp` 和 `yp` 中。第一步是找到圆半径，即两点之间的距离。幸运的是，我们刚刚写了一个函数 `distance` 来这样做，所以现在我们只需要：

```python
radius = distance(xc, yc, xp, yp)
```

第二步是找到该半径圆的面积并返回。同样，我们将使用我们的函数之一：

```python
result = area(radius)
return result
```

将其封装在函数中，我们得到：

```python
def area2(xc, yc, xp, yp):
    radius = distance(xc, yc, xp, yp)
    result = area(radius)
    return result
```

我们调用这个函数 `area2` 是为了将其与之前定义的 `area` 函数区分开。

临时变量 `radius` 和 `result` 对于开发、调试和单步执行很有用，但一旦程序运行，我们可以通过组合函数调用使其更简洁：

```python
def area2(xc, yc, xp, yp):
    return area(distance(xc, yc, xp, yp))
```

## 6.5 布尔函数

函数返回布尔值，这对于在函数内部隐藏复杂的测试非常方便。例如：

```python
def is_divisible(x, y):
    """测试 x 是否被 y 整除"""
    if x % y == 0:
        return True
    else:
        return False
```

通常给布尔函数命名为听起来像是非疑问的问题。`is_divisible` 返回 `True` 或 `False` 以表示是否能被 y 整除。

我们可以利用 `if` 语句的条件本身就是布尔表达式这一特性，使函数更简洁。直接返回它：

```python
def is_divisible(x, y):
    return x % y == 0
```

如何像计算机科学家一样思考：使用 Python 3 学习文档，第 3 版

这一节展示了新函数的用法：

```python
>>> is_divisible(6, 4)
False
>>> is_divisible(6, 3)
True
```

布尔函数经常用于条件语句：

```python
if is_divisible(x, y):
   # 执行某些操作 ...
else:
   # 执行其他操作 ...
```

你可能想写成：

```python
if is_divisible(x, y) == True:
```

但额外的比较是不必要的。

## 6.6 风格编程

可读性对程序员来说非常重要，因为在实践中，程序的阅读和修改比编写频繁得多。但就像大多数规则一样，我们有时也会打破它们。书中的大多数代码示例将符合 Python 增强提案 8 (`PEP 8`)，这是 Python 社区的风格指南。

随着程序变得复杂，我们将会有更多风格的内容，但一些建议现在就会很有帮助：

- 使用 4 个空格（而不是制表符）进行缩进
- 将长度限制在 78 个字符
- 在命名标识符时，类使用驼峰命名法（我们会提到），函数和变量使用小写下划线
- 将导入放在文件顶部
- 将定义放在一起
- 使用 docstring 文档函数
- 使用两个空行分隔不同的函数定义
- 将顶层语句（包括函数调用）集中放在程序底部

## 6.7 单元测试

在软件开发中，对源代码进行自动单元测试是一种常见做法。单元测试提供了一种自动验证单个代码片段的方法。

# 如何像计算机科学家一样思考：使用 Python 3 学习文档，第 3 版

此类函数能够正常工作。这使得在以后可以更改函数的实现，并快速测试它是否仍然按照预期方式工作。

有些组织认为，他们宝贵的资产是程序代码和文档。现在，这些组织将其软件预算的大部分用于编写（以及维护）它们的测试用例。

单元测试还迫使程序员考虑函数需要处理的不同情况。你只需要在脚本中编写一次测试用例，而不需要在开发代码时反复保留相同的测试数据。

程序中那些为了方便调试或测试而存在的额外代码被称为“脚手架”（`scaffolding`）。

Python 中针对某些单元的测试用集——但在现阶段，我们将忽略 Python 社区通常的做法，并在两个我们自己编写的函数上进行测试。我们使用这些函数来编写单元测试。

让我们从在本章之前编写的 `absolute_value` 函数开始。回一下，我们写了几个不同的版本，其中最后一个是错误的，并且包含一个 bug。测试能发现这个 bug 吗？

首先，我们计划测试。我们想知道当参数为负数、正数或零时，函数是否返回正确的值。在计划测试时，你总是想要考虑“边界情况”（edge cases）——在这里，向 `absolute_value` 传递参数 0 是函数行为改变的边缘，正如我们在章节开头看到的，这是程序员很容易出错的地方！因此，它是包含在我们的单元测试中的一个很好的用例。

我们将编写一个辅助函数来检查某个测试的结果。它接收一个布尔参数，并打印一条告诉我们测试通过的消息，或者打印一条告知我们测试失败的消息。函数体的第一行（函数文档字符串之后）会神奇地确定调用它在脚本中的行号。这允许我们打印测试的行号，当我们想要识别哪些测试通过或失败时将非常有帮助。

这里还有使用 `format` 方法的略微复杂的字符串格式化，我们目前暂略过，并在将在后的章节中详细介绍。但有了这个函数，我们可以开始构建单元测试了：

```python
def test_suite():
    """ 运行此模块（文件）代码的测试套件
    """
    test(absolute_value(17) == 17)
    test(absolute_value(-17) == 17)
    test(absolute_value(0) == 0)
    test(absolute_value(3.14) == 3.14)
    test(absolute_value(-3.14) == 3.14)

test_suite()  # 这里是运行测试的调用
```

在这里，你构建了我们套件中的第一个测试。我们可以针对 `absolute_value` 的第一个或第二个版本（即正确的版本）运行它，并得到类似下面的输出：

- 第 25 行测试 ok。
- 第 26 行测试 ok。
- 第 27 行测试 ok。
- 第 28 行测试 ok。
- 第 29 行测试 ok。

但让我们把函数更改为如下所示的错误版本：

```python
def absolute_value(n):  # 有错误的版本
    """ 计算 n 的绝对值 """
    if n < 0:
        return 1
    elif n > 0:
        return n
```

你能在这段代码中找到至少两个错误吗？我们的测试套件可能会得到：

- 第 25 行测试 ok。
- 第 26 行测试 FAILED。
- 第 27 行测试 FAILED。
- 第 28 行测试 ok。
- 第 29 行测试 FAILED。

这些是测试失败的示例。Python 有一个名为 `assert` 的语句，功能与我们的 `test` 函数几乎相同（除了断言失败时会停止程序）。你可能想阅读它，并用它代替 `test` 函数。

## 6.8 词表

**布尔函数 (Boolean function)** 返回布尔值的函数。可能的值是 `False` 和 `True`。

**喋话框函数 (chatterbox)** 与用户交互（使用输入或 `print`）的函数。

**沉默函数 (Silent functions)** 只将输入参数转换为输出结果的函数。

**函数组合 (composition of functions)** 在一个函数体内调用另一个函数，或将一个函数的返回值作为另一个函数的参数。

**死代码 (dead code)** 程序中永远不会被执行的代码部分。

**有收获的函数 (fruitful function)** 返回结果而非 `None` 的函数。

**增量开发 (incremental development)** 通过每次添加和测试少量代码来简化调试的开发方法。

**None** 一个特殊的 Python 值。

**返回值 (return value)** 作为函数调用结果提供的值。

**脚手架 (scaffolding)** 在开发期间用于辅助开发和调试的代码。

**临时变量 (temporary variable)** 用于存储中间值的变量。

**测试套件 (test suite)** 针对某些代码的测试用集。

**单元测试 (unit testing)** 验证单个代码单元是否正常工作的自动化程序。拥有测试套件在有人修改或扩展代码时非常有用：它提供了一个防止引入新 bug 的安全网。回归测试 (regression testing) 经常用于捕捉这种情况——我们不想倒退！

## 6.9 练习

下面的所有练习都应该添加到单个文件中。在该文件中，你还应该添加上面显示的 `test_suite` 函数，并在练习过程中，将新的测试添加到你的测试套件中。（如果你打开在线版，可以很容易地复制测试。）

完成每个练习后，确认所有测试均通过。

1. 四个方向点可以缩写为字符串 "N" "E" "S" 和 "W"。编写一个 `turn_clockwise` 函数，它接受这些方向点之一作为参数，并返回顺时针方向的下一个方向点。以下是通过的测试：

```python
test(turn_clockwise("N") == "E")
test(turn_clockwise("E") == "S")
test(turn_clockwise("S") == "W")
test(turn_clockwise("W") == "N")
```

如果给函数无效参数，它应该返回 `None`：

```python
test(turn_clockwise("North") == None)
test(turn_clockwise(42) == None)
```

2. 编写一个 `day_name` 函数，将整数 0 到 6 转换为日期。假设是 "Sunday"。以下是通过的测试：

```python
test(day_name(0) == "Sunday")
test(day_name(1) == "Monday")
test(day_name(2) == "Tuesday")
test(day_name(3) == "Wednesday")
test(day_name(4) == "Thursday")
test(day_name(5) == "Friday")
test(day_name(6) == "Saturday")
```

再次，如果给函数无效参数，它应该返回 `None`：

```python
test(day_name(7) == None)
test(day_name("Halloween") == None)
```

3. 编写一个逆函数 `day_num`，它接收日期名称并返回其数字：以下是通过的测试：

```python
test(day_num("Sunday") == 0)
test(day_num("Monday") == 1)
test(day_num("Tuesday") == 2)
test(day_num("Wednesday") == 3)
test(day_num("Thursday") == 4)
test(day_num("Friday") == 5)
test(day_num("Saturday") == 6)
```

如果给函数无效参数，它应该返回 `None`：

```python
test(day_num("Halloween") == None)
```

4. 编写一个提问此类问题的函数：“今天是周三。我在 19 小时后离开。那是哪一天？”该函数必须接受一个日期名称和一个增量参数（要增加的天数），并返回结果日期：以下是通过的测试：

```python
test(day_add("Monday", 4) == "Friday")
test(day_add("Tuesday", 0) == "Tuesday")
test(day_add("Tuesday", 14) == "Tuesday")
test(day_add("Sunday", 100) == "Sunday")
```

5. 你的 `day_add` 函数可以处理负增量工作吗？

```python
test(day_add("Sunday", -1) == "Saturday")
test(day_add("Sunday", -7) == "Sunday")
test(day_add("Tuesday", -100) == "Sunday")
```

如果你的函数有效，请解释原因。如果无效，请让它工作。提示：在某些情况下可以使用模函数 `%`（在上一章开头引入）。具体来说，当 `x` 为负数时，`x % 7` 会发生什么。

# 像计算机科学家一样思考：Python 3 学习文档，第3版

```python
test(to_secs(2, 30, 10) == 9010)
test(to_secs(2, 0, 0) == 7200)
test(to_secs(0, 2, 0) == 120)
test(to_secs(0, 0, 42) == 42)
test(to_secs(0, -10, 10) == -590)
```

- 8. 扩展 `to_secs` 使其能够处理实值输入。它应该始终返回一个整数秒数（截断小数）：

```python
test(to_secs(2.5, 0, 10.71) == 9010)
test(to_secs(2.433, 0, 0) == 8758)
```

- 9. 编写三个作为 `to_secs` “逆运算”的函数：

    - (a) `hours_in` 返回总秒数所代表的整数小时数。
    - (b) `minutes_in` 在减去小时数后，返回总秒数剩余的整数分钟数。
    - (c) `seconds_in` 返回总秒数中剩余的秒数。

你可以假设传递给这些函数的总秒数是一个整数。这里是一些测试用例：

```python
test(hours_in(9010) == 2)
test(minutes_in(9010) == 30)
test(seconds_in(9010) == 10)
```

想要的结果并不总是显而易见的……

在第三种情况下，该需求看起来是相当模糊且不确定的。但通过测试用例明确了我们实际上需要做什么。

单元测试具有明确规范的次要益处。当你编写自己的测试套件时，它将成为问题解决过程的一部分，因为你会不断问自己你真正期待发生什么，以及你是否考虑了所有可能的情况。

由于我们的书标题是《像计算机科学家一样思考……》，你可能会喜欢读一些关于思考的参考文献，以及关于像流体智力（解决问题的关键因素）这类有趣的观点。例如，查看 http://psychology.about.com/od/cognitivepsychology/a/fluid-crystal.htm。学习计算机科学需要流体智力和结晶智力的良好结合。

- 10. 在这些测试中哪些失败了？请解释原因。

```python
test(3 % 4 == 0)
test(3 % 4 == 3)
test(3 / 4 == 0)
```

# 像计算机科学家一样思考：Python 3 学习文档，第3版

```python
test(3 // 4 == 0)
test(3+4 * 2 == 14)
test(4-2+2 == 0)
test(len("hello, world!") == 13)
```

- 11. 编写一个比较函数 `compare`，如果 $a > b$ 返回 1，如果 $a == b$ 返回 0，如果 $a < b$ 返回 -1

```python
test(compare(5, 4) == 1)
test(compare(7, 7) == 0)
test(compare(2, 3) == -1)
test(compare(42, 1) == 1)
```

- 12. 编写一个函数 `hypotenuse`，使用两个参数返回直角三角形的斜边长度：

```python
test(hypotenuse(3, 4) == 5.0)
```
