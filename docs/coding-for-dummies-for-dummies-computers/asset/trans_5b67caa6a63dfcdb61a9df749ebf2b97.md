

## 使用字符串和特殊字符

除了数字之外，Python 中的变量还可以存储字符串。要为字符串赋值，可以使用单引号或双引号，如下所示：

```python
firstname = "Travis"
lastname = 'Kalanick'
```

![](img/5a907eb39993e80f28c82efc2e4632b3_233_0.png)

变量也可以将数字以字符串形式存储，而非数字类型。然而，即使字符串看起来像数字，Python 也无法对字符串和数字进行加、减或除运算。例如，考虑 amountdue = "18" + 24 —— 直接运行此代码会导致错误。Python 可以对字符串进行乘法运算，但方式很有趣——print 'Ha' * 3 的结果是 'HaHaHa'。

在字符串中包含单引号或双引号可能会引发问题，因为字符串内部的引号会过早终止字符串的定义。例如，如果我想存储一个值为“I'm on my way home”的字符串，Python 会认为第一个字母 I 后面的单引号是变量赋值的结束，其余字符将导致错误。解决方案是使用称为转义序列的特殊字符，来表示你想使用通常标志字符串开头或结尾的引号等字符，或制表符等其他不可打印字符。表 14-3 展示了一些转义序列的示例。

**表 14-3：常用的 Python 转义序列**

| 特殊字符 | 描述 | 示例 | 结果 |
|---|---|---|---|
| `\'` 或 `\"` | 引号 | `print "You had me at \"Hello\""` | `You had me at "Hello"` |
| `\t` | 制表符 | `print "Item\tUnits\tPrice"` | `Item Units`<br>`Price` |
| `\n` | 换行符 | `print "Anheuser?\nBusch?\nBueller?"` | `Anheuser?`<br>`Busch?`<br>`Bueller?` |

![](img/5a907eb39993e80f28c82efc2e4632b3_234_0.png)

转义序列仅对使用双引号的字符串生效。完整的转义序列列表，请参阅 http://docs.python.org/2/reference/lexical_analysis.html 中第 2.4 节“字面量（Literals）”下的表格。

## 使用条件判断：if、elif、else

变量中存储数据后，一项常见任务是将变量的值与固定值或另一个变量的值进行比较，然后根据比较结果做出决策。如果你之前阅读过关于 JavaScript 或 Ruby 的章节，这里的讨论和概念非常相似。if-elif-else 语句的一般语法如下：

```
if conditional1:
    statement1 to execute if conditional1 is true
elif conditional2:
    statement2 to execute if conditional2 is true
else:
    statement3 to run if all previous conditional are false
```

![](img/5a907eb39993e80f28c82efc2e4632b3_234_1.png)

注意这里没有花括号或分号，但别忘了冒号和语句缩进！

最初的 if 语句会求值为真或假。当 conditional1 为真时，执行 statement1。这是 if 语句所需的最小必要语法，elif 和 else 是可选的。当存在 elif 时，它会在 conditional1 为假时测试另一个条件。你可以使用 elif 测试任意多个条件。逐一指定每个要测试的条件会很繁琐，因此拥有一个“兜底”非常有用。当存在 else 时，它充当“兜底”，在所有先前的条件都为假时执行。

![](img/5a907eb39993e80f28c82efc2e4632b3_234_2.png)

你不能单独使用 elif 或 else，而不在前面使用 if 语句。你可以包含多个 elif 语句，但只能有一个且仅有一个 else 语句。

if 语句中的条件使用比较运算符来比较值，表 14-4 描述了常见的比较运算符。

**表 14-4：常见的 Python 比较运算符**

| 类型 | 运算符 | 描述 | 示例 |
|---|---|---|---|
| 小于 | `<` | 判断一个值是否小于另一个值 | `x < 55` |
| 大于 | `>` | 判断一个值是否大于另一个值 | `x > 55` |
| 等于 | `==` | 判断两个值是否相等 | `x == 55` |
| 小于或等于 | `<=` | 判断一个值是否小于或等于另一个值 | `x <= 55` |
| 大于或等于 | `>=` | 判断一个值是否大于或等于另一个值 | `x >= 55` |
| 不等于 | `!=` | 判断两个值是否不相等 | `x != 55` |

下面是一个 if 语句示例。

```
carSpeed=55
if carSpeed > 55:
    print "You are over the speed limit!"
elif carSpeed == 55:
    print "You are at the speed limit!"
else:
    print "You are under the speed limit!"
```

如图 14-1 的示意图所示，有两个条件，每个条件由菱形框表示，按顺序进行求值。在此示例中，carSpeed 等于 55，因此第一个条件（carSpeed > 55）为假，然后第二个条件（carSpeed==55）为真，语句执行并打印“You are at the speed limit!”。当某个条件为真时，if 语句停止执行，永远不会到达 else。

![](img/5a907eb39993e80f28c82efc2e4632b3_236_0.png)

图 14-1：带有 `elif` 的 `if-else` 语句。

## 输入与输出

Python 可以收集用户输入，并向用户显示输出。要收集用户输入，请使用 raw_input("Prompt") 方法，该方法将用户输入存储为字符串。在下面的示例中，用户输入其全名，该全名存储在名为 full_name 的变量中。

```
full_name = raw_input("What’s your full name?")
```

假设用户输入了他的名字“Jeff Bezos”。你可以使用 `print(full_name)` 显示该变量的值，你会看到

```
Jeff Bezos
```

与 Ruby 不同，Python 不会在用户输入后存储换行符 `\n` 转义序列。

此时，你可能会觉得在 Python 解释器控制台窗口中打印变量和值与使用 Python 创建的变量动态生成网页有很大不同。要将 Python 集成到网页中以响应用户请求并生成 HTML 页面，通常使用 Python Web 框架（如 Django 或 Flask），这些框架带有预先编写好的代码，使过程更简单。这些框架通常需要一些安装和设置工作，并且通常将显示的数据与用于向用户展示页面的模板分离开来。

![](img/5a907eb39993e80f28c82efc2e4632b3_236_1.png)

## 字符串整形

每当你从用户处收集输入时，都需要清理输入以去除错误和不一致之处。以下是一些常见的数据清理任务：

- 标准化字符串，使大小写保持一致
- 移除用户输入中的空白字符
- 在向用户显示的字符串中插入变量值

Python 包含许多内置方法，使字符串处理变得简单。

### 使用点号表示法的 upper()、lower()、capitalize() 和 strip()

将用户输入标准化为正确的大小写并移除多余的空白字符，通常是为了以后能轻松地对数据进行排序。例如，假设你正在为纽约尼克斯队设计一个网站，让球迷可以在赛后与球员见面。页面要求球迷输入他们的名字，这样球队保安可以在入场前对照此列表检查球迷姓名。查看过去的球迷输入时，你会发现球迷以多种方式输入同一个名字，如“Mark”、“mark”、“marK ”以及其他类似变体，这些变体会在按字母顺序排序列表时导致问题。要使输入和这些名字保持一致，可以使用表 14-5 中描述的字符串函数。

**表 14-5：精选的 Python 字符串函数**

| 函数名 | 描述 | 示例 | 结果 |
|---|---|---|---|
| `string.upper()` | 返回所有大写字符 | `"nY".upper()` | `"NY"` |
| `string.lower()` | 返回所有小写字符 | `"Hi".lower()` | `"hi"` |
| `string.capitalize()` | 首字母大写，其余字母小写 | `"wake UP".capitalize()` | `"Wake up"` |
| `string.strip()` | 移除开头和结尾的空白字符 | `" Ny ".strip()` | `"Ny"` |

### 使用 % 进行字符串格式化

要将变量值插入到向用户显示的字符串中，可以使用字符串格式化运算符 %。在字符串定义中，%d 用于指定整数，%s 用于指定字符串，而要格式化的变量（映射键）在字符串定义后的括号中指定。请参见下面的示例代码和结果：

代码：

```
yearofbirth = 1990
pplinroom = 20
name = "Mary"
print "Your year of birth is %d. Is this correct?" % (yearofbirth)
print "Your year of birth is %d. Is this correct?" % (yearofbirth)
print "There are %d women in the room born in %d and %s is one of them." %
      (pplinroom/2, yearofbirth, name)
```

