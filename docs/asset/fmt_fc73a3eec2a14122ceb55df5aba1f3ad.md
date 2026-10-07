
键必须是不可变的。这意味着你可以使用字符串、数字或元组作为键。但是，你不能使用列表作为键。

你对提供的值没有限制。值可以是任何 Python 对象，所以你可以使用字典访问员工记录或其他复杂数据。以下步骤帮助你更好地理解如何使用字典。

### 1. 打开 Python Shell 窗口。

你看到 Python 提示符。

### 2. 输入 `Colors = {"Blue": "Amy", "Red": "Sarah", "Yellow": "John"}` 并按回车。

Python 创建了一个包含三个人喜欢的颜色的字典。注意你是如何创建键值对的。

### 3. 输入 `Colors` 并按回车。

你看到键和值对，如图 13-5 所示。但是，注意这些条目是按键排序的。字典会自动保持键排序以使访问更快，这意味着你获得了快速

## 250 第三部分：执行常用任务

即使在处理大型数据集时，搜索速度也非常快。缺点是创建字典比使用列表等结构花费长时间，因为计算机正忙于排序条目。

```
Python 3.3.4 Shell File Edit Shell Debug Options Windows Help
Python 3.3.4 ((v3.3.4:7ff62e4ite426, Feb 10 2014, 18:13:51) [MSC v-
1600 64 bit (AMD64)] on win32
Type "copyright", "credits" or "license()" for more information.
>>> Colors = {"Sam": "Blue", "Amy": "Red", "Sarah": "Yellow"}
>>> Colors['Amy']
'Red'
>>> Colors['Sarah']
'Yellow'
```

图 13-5：排序有序的字典条目。

### 4. 输入 `Colors["Sarah"]` 并回车。

你看到了与 Sarah 关联的颜色黄色，如图 13-6 所示。使用字符串作为键而不是数字索引，可以使代码更易读，并在某种程度上实现了自文档化。通过提高代码的可读性，字典长远来看为你节省了大量时间（这就是为什么它们如此流行）。然而，字典的便利性是以增加添加时间和更高的资源消耗为代价的，因此存在需要考虑的权衡。

```
Python 3.3.4 Shell File Edit Shell Debug Options Windows Help
Python 3.3.4 ((v3.3.4:7ff62e4ite426, Feb 10 2014, 18:13:51) [MSC v-
1600 64 bit (AMD64)] on win32
Type "copyright", "credits" or "license()" for more information.
>>> Colors = {"Sam": "Blue", "Amy": "Red", "Sarah": "Yellow"}
>>> Colors['Amy']
'Red'
>>> Colors['Sarah']
'Yellow'
```

图 13-6：字典实现了值的访问和自文档化。

### 5. 输入 `Colors.keys()` 并回车。

字典呈现了它包含的键的列表，如图 13-7 所示。你可以使用这些键来自动化对字典的访问。

## 第13 章：收集各种数据 251

```
Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
Python 3.3.4 (v3.3.4:ff6215e426, Feb 10 2014, 18:13:51) [MSC v-
1600 64 bit (AMD64)] on win32
Type 'copyright', 'credits' or 'license' for more information.
>>> Colors = {'Sam': 'Blue', 'Amy': 'Blue', 'Red': 'Red', 'Sarah': 'Yellow'}
>>> Colors['Sarah']
'Yellow'
>>> Colors.keys()
dict_keys(['Amy', 'Sarah', 'Sam'])
>>> _
```

图 13-7：你可以向字典索要键的列表。

### 6. 输入以下代码（每行按一次回车，最后一行按两次回车）：

```
for Item in Colors.keys():
    print("{0} likes the color {1}.")format(Item, Colors[Item]))
```

示例代码输出了每个用户名和用户喜好的颜色列表，如图 13-8 所示。使用字典可以让创建有用的输出变得简单得多。这个键的一个含义是键可以很容易成为输出的一部分。

![](img/ec69aa1535cd82c735ee14abfc05048f_266_0.png)

```
Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
Python 3.3.4 (v3.3.4:ff6215e426, Feb 10 2014, 18:13:51) [MSC v
1600 64 bit (AMD64)] on win32
Type 'copyright', 'credits' or 'license' for more information.
>>> Colors = {'Sam': 'Blue', 'Amy': 'Blue', 'Red': 'Red', 'Sarah': 'Yellow'}
>>> Colors['Sarah']
'Yellow'
>>> Colors.keys()
dict_keys(['Amy', 'Sarah', 'Sam'])
>>> for Item in Colors.keys():
    print("{0} likes the color {1}.")format(Item, Colors[Item])
>>> 
```

图 13-8：你可以更轻松地创建有用的键来输出信息。

Amy likes the color Red.

Sarah likes the color Yellow.

Sam likes the color Blue.

>>> _

## 第三部分：执行常用任务

### 7. 输入 `Colors["Sarah"] = "Purple"` 并回车。

字典内容已更新，Sarah 的颜色变成了紫色而不是黄色。

### 8. 输入 `Colors.update("Harry": "Orange")` 并回车。

字典中添加了一个新条目。

### 9. 将光标放在你输入的代码的第三行末尾并按回车。

编辑器为你创建了代码的副本。这是一种节省时间的技巧，当 Python Shell 中的代码需要耗时间输入时可以使用它。尽管第一次必须手动输入，但你没有理由再输入一遍。

### 10. 按两次回车。

你在图 13-9 中看到了更新后的输出。注意 Harry 是按排序添加的。Sarah 的条目被更改为紫色。

![](img/ec69aa1535cd82c735ee14abfc05048f_267_0.png)

```
Python 3.3.4
(v3.3.4:ff6215e426, Feb 10 2014, 18:13:51) [MSC v-1600 64 bit (AMD64)] on win32
>>> "copyright"
...
>>> Colors = {'Sam': 'Blue', 'Amy': 'Blue', 'Red': 'Red', 'Sarah': 'Yellow'}
>>> Colors['Sarah']
'Yellow'
>>> Colors["Sarah"] = "Purple"
>>> Colors.update("Harry": "Orange")
>>> for Item in Colors.keys():
    print("{0} likes the color {1}.")format(Item, Colors[Item])
>>> 
```

图 13-9：字典易于修改。

## 第13 章：收集各种数据

### 11. 输入 `del Colors["Sarah"]` 并回车。

这删除了字典中的 Sarah 条目。

### 12. 重复步骤 9 和 10。

你验证了 Sarah 条目已删除。

### 13. 输入 `len(Colors)` 并回车。

输出显示字典只剩下三个条目。

### 14. 输入 `Colors.clear()` 并回车。

### 15. 输入 `len(Colors)` 并回车。

Python 显示 `Colors` 有 0 个条目，因此字典是空的。

### 16. 关闭 Shell 窗口。

## 用字典替换 switch 语句

大多数编程语言都提供某种 switch 语句。switch 语句提供了优雅的选择。用户可以选择其中之一。通过使用字典，你可以模拟 switch 语句的使用。以下步骤帮助你创建一个演示该技术的示例。该示例也以 PythonSwitch.py 的源码形式出现。

```
switch (n)
{
  case 0:
    print("You selected blue.");
    break;
  case 1:
    print("You selected yellow.");
    break;
  case 2:
    print("You selected green.");
    break;
}
```

应用程序通常呈现一个界面，根据用户的选择选择正确的操作。这比使用一系列 if 语句来实现相同任务要直接且整洁得多。

## 254 第三部分：执行常用任务

遗憾的是，Python 并不带 switch 语句。你所能做的就是使用 if...elif 语句完成任务。然而，通过使用字典，你可以模拟 switch 语句。

### 1. 打开一个 Python 文件窗口。

你可以在编辑器中输入示例代码。

### 2. 在窗口中输入以下代码——每行按一次回车：

```
def PrintBlue():
    print("You chose blue!\r\n")

def PrintRed():
    print("You chose red!\r\n")

def PrintOrange():
    print("You chose orange!\r\n")

def PrintYellow():
    print("You chose yellow!\r\n")
```

在代码为你做任何之前，必须定义任务。每个函数都定义了一个与屏幕选项相关的任务。任何时间只调用一个。

### 3. 在窗口中输入以下代码——每行按一次回车：

```python
ColorSelect = {
    0: PrintBlue,
    1: PrintRed,
    2: PrintOrange,
    3: PrintYellow
}
```

代码就是字典。每个键就像 switch 语句的 case 部分。值指定了要做什么。换句话说，这就是 switch 结构。你之前创建的函数是 switch 语句的动作部分——位于 case 语句和 break 子句之间的部分。

## 第 13 章：收集各种数据

### 4. 在窗口中输入以下代码 —— 每行后按回车：

Selection = 0

```python
while (Selection != 4):
    print("0, Blue")
    print("1, Red")
    print("2, Orange")
    print("3, Yellow")
    print("4, Quit")
```

```python
Selection = int(input("Select color option: "))
if (Selection >= 0) and (Selection < 4):
    ColorSelect[Selection] =
```

最后，你将看到示例的用户界面部分。通过创建一个输入变量 `Selection`，程序进入一个循环，直到用户输入值 4 为止。

在每次循环中，应用程序都会显示选项列表并等待用户输入。当用户提供输入时，应用程序会进行范围检查。0 到 3 之间的任何值都会使用字典作为切换机制，选择之前定义的函数之一。

### 5. 选择运行 (Run)：运行模块 (Run Module)

你看到一个 Python Shell 窗口打开。应用程序显示了如图 13-10 所示的菜单。

![](img/ec69aa1535cd82c735ee14abfc05048f_270_0.png)

### 6. 输入 0 并按回车。

应用程序告知你选择了蓝色，然后再次显示菜单，如图 13-11 所示。

![](img/ec69aa1535cd82c735ee14abfc05048f_271_0.png)

图 13-11：在执行你的选择后，应用程序会再次显示菜单。

### 7. 输入 4 并按回车。

应用程序结束。

## 使用列表创建栈 (Stacks)

栈（Stack）是一种实用的编程结构，因为你可以用它来保存应用程序执行环境（在任何给定时间变量的状态以及应用程序环境的其他属性），或作为确定执行顺序的手段。遗憾的是，Python 没有提供作为集合的栈。但是，它提供了列表（lists），你可以将列表作为完全可以的栈。以下步骤帮助你创建一个使用列表作为栈的示例。该示例也会出现在可下载源码 `ListStack.py` 中。

### 1. 打开 Python 文件窗口。

你看到一个编辑器，可以在其中输入示例代码。

### 2. 在窗口中输入以下代码 —— 每行后按回车：

```python
MyStack = []
StackSize = 3
```

```python
def DisplayStack():
    print("Stack currently contains:")
    for Item in MyStack:
        print(Item)
```

```python
def Push(Value):
    if len(MyStack) < StackSize:
        MyStack.append(Value)
    else:
        print("Stack is full!")
```

```python
def Pop():
    if len(MyStack) > 0:
        MyStack.pop()
    else:
        print("Stack is empty.")
```

```python
Push(1)
Push(2)
Push(3)
DisplayStack()
input("Press any key when ready...")
```

```python
Push(4)
DisplayStack()
input("Press any key when ready...")
```

```python
Pop()
DisplayStack()
input("Press any key when ready...")
```

```python
Pop()
Pop()
Pop()
DisplayStack()
```

在这种情况下，应用程序创建了一个列表和一个变量来确定栈的最大尺寸。栈通常有一个特定的尺寸范围。诚然这是一个非常小的栈，但它很好地满足示例的需求。

通过向栈顶推入（push）值和从栈顶弹出（pop）值来工作。`Push()` 和 `Pop()` 函数执行这两个任务。代码添加了 `DisplayStack()` 以在需要时查看栈的内容。

剩余代码通过向栈中推入值然后移除它们来练习栈（演示其功能）。共有四个主要的栈练习会。

### 3. 选择运行 (Run)：模块。

你看到一个 Python 窗口打开。应用程序向栈中填充信息并在屏幕上显示，如图 13-12 所示。在这种情况下，3 是栈顶，因为它是最后添加的值。

![](img/ec69aa1535cd82c735ee14abfc05048f_273_0.png)

```text
Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
Python 3.3.4 (v3.3.4:7ff62415e426, Feb 10 2014, 18:13:51) [MSC v.
1600 x64 bit (AMD64)] on
Type 'copyright', 'credit' or 'license()' for more information.
>>> RESTART ==================
Stack currently contains:
Press any key when ready...]
```

### 4. 按回车。

应用程序尝试向栈中推入另一个值。然而，栈已经满了，因此任务失败，如图 13-13 所示。

### 5. 按回车。

应用程序从栈顶弹出一个值。记住 3 是栈顶，如图 13-14 所示。

```text
Python 3.3.4 Shell
File Edit Shell Debug Options Windows Help
Python 3.3.4 (v3.3.4:7ff62415e426, Feb 10 2014, 18:13:51) [MSC v.
1600 x64 bit (AMD64)] on
Type 'copyright', 'credit' or 'license()' for more information.
>>> RESTART ==================
Stack currently contains:
1
2
```

# 262 第三部分：执行常见任务

图 13-16：

当应用程序将新条目放入队列时，队列不再报告为空。
