
![](img/9d932bec53e523b8d8b7b8134cf77ca7_90_0.png)

## 第七章

## Python

### 概述与基本语法

Python 是一种著名的编程语言，由 Guido van Rossum 于 1991 年开发。作为一种高级、面向对象且交互式的脚本语言，Python 可用于系统脚本编写、软件开发以及服务器端 Web 开发。

### 特性

作为一种基于解释型的语言，Python 允许一次执行一条指令，并且还支持大量数据类型。该编程语言易于学习和编码，因为它只有少量关键字且语法定义清晰。凭借广泛的标准库，Python 还提供对交互模式的支持，这使开发者更容易测试和调试代码。此外，该语言可用于 GUI 编程，以及开发具有系统调用、Windows 系统和库的应用程序。除了这些特性之外，Python 还支持自动垃圾回收，提供高级动态数据类型，并且可以与 C++、C、Java 和 CORBA 集成。用户可以直接与 Python 解释器交互来编写程序，因为它也提供低级模块。

需要在你的 PC 上安装 Python，源代码可在 GNU 通用公共许可证 (GPL) 下下载。不同的基于 GUI 的 Python 集成开发环境 (IDE) 包括 PyCharm、The Python Bundle、Python IDLE 和 Sublime Text。最新且当前的二进制文件、源代码、新闻和文档可在 Python 官方网站找到：[https://www.python.org](https://www.python.org)

### 变量类型、基本运算符和数据类型

**变量类型**

在 Python 编程中，变量不需要声明以保留内存位置，因为只要给变量赋值，声明就会自动发生。根据变量的数据类型，解释器会分配内存，并允许程序员存储小数、字符或整数。

以下是在 Python 编程语言中为变量赋值的语法：

```python
#!/usr/bin/python

ID = 100         # An integer assignment
Weight = 100.0   # A floating point
name = "William" # A string

print ID
print Weight
print name
```

Python 的保留关键字列表：

| Del | Else | And | Assert | In | Raise |
|---|---|---|---|---|---|
| From | Continue | If | Finally | Not | Pass |
| As | Return | Not | Pass | Yield | Break |
| Except | Import | For | Global | While | print |
| With | Try | Exec | Or | Is | Elif |

**基本运算符**

Python 具有内置运算符，例如算术运算符、赋值运算符、逻辑运算符、位运算符、比较运算符和成员运算符。

Python 运算符的详细信息简述于下表：

| 算术运算符 | 赋值运算符 | 比较运算符 | 逻辑运算符 | 位运算符 |
|---|---|---|---|---|
| 加法 (+) | 等于 (=) | 双等号 (==) | 逻辑或 (or) | 二进制与 (&) |
| 减法 (-) | 加且赋值 (+=) | 不等于 (<>) | 逻辑与 (and) | 二进制或 (\|) |
| 乘法 (*) | 减且赋值 (-=) | 大于 (>) | 逻辑非 (not) | 二进制异或 (^) |
| 除法 (/) | 乘且赋值 (*=) | 小于 (<) |  | 二进制左移 (<<) |
| 取模 (%) | 除且赋值 (/=) | 小于等于 (<=) |  | 二进制右移 (>>) |
| 整除 (//) | 取模赋值 (%=) | 大于等于 (>=) |  | 二进制反码 (~) |
| 幂 (**) | 整除赋值 (//=) |  |  |  |

**数据类型**

在 Python 编程语言中，每个对象都有自己的类型和值。  
Python 的内置数据类型：

- 数字包括整数、浮点数、分数以及复数。Python 中预定义的数据类型是 int、float、long 和 complex。
- 序列由字符串、字节、列表和元组组成。
- 布尔值保存 True 或 False。
- 字典包含以无序方式设置的键值对。
- 集合包含无序的值容器。

### 流程控制

控制流语句允许程序员更改程序流程，并执行特定操作。与其他高级编程语言一样，Python 中使用的三种主要控制流语句是 If、For 和 While。下图展示了控制流语句在程序中实际如何工作：

**条件语句**

**If 语句**

If 语句是一个布尔表达式，其结果以 TRUE 或 FALSE 的形式显示。

**If else 语句**

If else 语句也是一个布尔表达式，并且包含一个可选的 else 语句。如果表达式结果为 False，则执行 else 语句。

**嵌套语句**

语句中的语句称为嵌套语句。

**循环**

循环是一系列指令，允许程序员通过实现特定条件来执行特定任务。在 Python 编程中，循环可用于通过给定的控制结构执行若干语句或一组指令。

Python 中的循环类型：

**While 循环**

While 循环用于在程序中重复语句或迭代 ‘n’ 次。在 Python 中使用 While 循环的语法是：

```python
while expression:
    statement(s)
```

示例程序：

```python
#!/usr/bin/python

count = 0
while (count < 10):
    print 'The count is:', count
    count = count + 2
```

![](img/9d932bec53e523b8d8b7b8134cf77ca7_95_0.png)

**输出：**

![](img/9d932bec53e523b8d8b7b8134cf77ca7_95_1.png)

**For 循环**

为了迭代任何序列（包括字符串或列表）中的项，我们可以使用 For 循环。

语法：

```python
for iterating_var in sequence:
    statement(s)
```

示例程序：

```python
fruits = ["apple", "banana", "cherry"]
for x in fruits:
    print(x)
```

要在循环迭代完所有项之前停止循环，我们可以使用 Break 语句；而 Continue 语句可用于停止当前循环迭代并继续下一次迭代。

### 函数和模块

**什么是函数？**

函数是一组可复用且有组织的代码，用于在程序中执行特定任务和操作。尽管 Python 编程语言中有多个内置函数可用，开发者也可以创建自己的函数，这些函数也称为用户定义函数。在 Python 中定义函数的语法如下：

```python
def functionname( parameters ):
    "function_docstring"
    function_suite
    return [expression]
```

要引入函数定义，我们可以使用关键字 ‘def’，随后是函数体所需的语句。分配给函数的变量通常将其值存储在局部符号表中，这意味着除非将全局变量声明为 global 语句，否则不能在函数内为全局变量赋值。

**调用函数**

Python 编程语言中的函数可以通过提供所有参数、提供可选参数或仅提供必需参数来调用。Python 函数最大限度地提高了代码可复用性，并使程序更易于阅读和理解。

以下是用于在 Python 中定义和使用函数的语句：

```python
def display(message):
    print('Hi' + message)

# Call Expression
myfun('karl', 'os', *rest)

# global
x = 'hello'
def printer():
    global x
    x = 'hi'

# yield
def sq(k):
    for i in range(k):
        yield i**2

# return
def sum(a, b=2):
    return a+b

# nonlocal
def outer():
    a = 'old'
    def inner():
        nonlocal a
        a = 'new'
```

**模块**

模块化编程是一种将程序的不同组件或部分组织到系统中的方法。该方法绑定数据并允许程序员将其用作参考，从而使代码更易于理解和实现。在 Python 中，模块允许程序员将源代码保存在文件中并多次重新运行它们，因为它们可作为自然的编程工具。

Python 编程语言中有大量标准库模块集合，包含两百多个模块。此外，它们还提供平台无关的支持，以执行若干编程任务，例如对象持久化、文本模式匹配以及 Internet 脚本编写。

Python 中 import 语句的语法：

```python
import module_name1 [, module_name2 [, ... module_nameN]]
```

使用 ‘import’ 模块的运行时操作语句是：

- 查找
- 编译

要使用名为 newmodule 的模块，我们可以这样调用函数：

```python
import newmodule
newmodule.functionname("Name")
```

在 Python 中从模块导入的语法是：

```python
def newmodule(name):
    print("Hello, " + name)

person1 = {
    "name": "James",
    "age": 30,
}
```

