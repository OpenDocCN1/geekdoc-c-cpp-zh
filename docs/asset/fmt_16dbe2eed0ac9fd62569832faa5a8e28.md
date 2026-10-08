
函数可以使用 `return` 返回任何类型的对象，如果未指定 `return`，则返回 `return None`（`None` 是 Python 的等效值）。函数与其他语言之间的一个重要区别是调用样式。C/C++ 和 Fortran 的用户熟悉**按引用传递（call by reference）**；然而，Python 在处理**不可变对象**时的行为有所不同。我们在上面的示例中展示了这一点。在引用传递样式中，我们不需要返回 `parameter`——给 `parameter` 加 1 就会改变传入的 `age` 变量，变为 11。在 Python 中，不可变对象无法被“原地”修改。列表、字典或可变对象允许在函数内部进行修改。

Python 函数还可以设置变量默认值。如果没有为此参数传递参数，它将保留函数声明中设置的值。见下面的示例。

```python
def pet_shop(animal, alive=True):
    # 定义一个函数，并将 alive 变量默认设置为 True。
    print("Hello!")
    if animal == "parrot":
        if not alive:
            print("Refunds in Bolton!")
        else:
            print("What a lovely parrot!")
```

`my_pet = "parrot"`
`pet_shop(my_pet)`
    # Hello!
    # What a lovely parrot!

`pet_shop(my_pet, False)`
    # Hello!
    # Refunds in Bolton!

## 9.1.5 模块

Python 的优秀特性之一是它携带了大量的预写代码，这些代码被称为模块。这意味着如果你在用 Python 编写代码，很有可能某些编程工作已经为你完成了！无论是转换字符串和二进制数据、生成随机数、管理线程、与 Web 服务器交互还是压缩文件，所有这些代码都在 Python 源码中等待调用。现在让我们通过一些常用模块的描述和示例来查看如何访问它们。

### 9.1.5.1 sys 模块

`sys` 是一个常用的模块，提供了一些与 Python 解释器交互的基本方法。要使用 `sys`，只需在编写访问 `sys` 命令的代码之前，在脚本中添加 `import sys`。当你执行导入命令时，Python 将读取其源码中的一个文件，该文件的内容将成为 `sys` 对象。现在，`sys` 模块中的任何函数都可以通过 `sys.a_func()` 在你的脚本中访问，其中 `a_func` 是所需函数的名称。提示：当函数存在于对象内部时，它们被称为**方法（methods）**。`sys` 模块中有用的对象或方法是 `argv` 和 `exit()`。第一个是 Python 脚本名称和 Python 解释器命令行输入的列表。第二个方法 `exit()` 将终止 Python 程序和解释器。该方法的参数默认值为 0，但可以提供任何非零整数来返回退出状态。

```python
# myscript.py 的内容
import sys
print("Hello World!")
print("My name is", sys.argv[1]) # 访问 sys 模块中的 argv 列表
print("My script's name is", sys.argv[0])
```

```bash
# 在命令行中...
[user@host ~$] python myscript.py
    Hello World!
    My name is John
    My script's name is myscript.py
```

## 9.1.5 io 模块

另一个有用的模块是 `io`。这使得读取任何类型的文件变得简单。`io.open()` 方法获取文件句柄并打开流，`io.readline()` 或 `io.readlines(lines)` 读取文件的一行或多行，`io.close()` 关闭文件中的流。通过 `.open()` 方法，你可以指定许多参数来描述要打开的文件名、文件类型以及你是想读取 (r)、写入 (w) 还是追加 (a)。让我们来看使用空文件 `parrots.txt` 的示例，我们向其中添加了三行文本。

```python
import io
with io.open('parrots.txt', 'w') as my_file:
    my_file.write("Line 1\n")
    my_file.write("Line 2\n")
    my_file.write("Line 3\n")
with io.open('parrots.txt', 'r') as my_file:
    for line in my_file:
        print(line.strip())
```

## 9.1.6 其他本质模块

| 模块 | 说明 |
| :--- | :--- |
| `os` | 提供操作系统相关功能 |
| `re` | 用于模式匹配的正则表达式 |
| `time` | 时间函数和类 |
| `collections` | 内置之外的特殊容器类型 |
| `itertools` | 创建高效迭代器的函数 |
| `random` | 生成伪随机数 |
| `argparse` | 解析命令行参数的库 |
| `logging` | 应用程序日志框架 |

## 9.1.7 Python 类

Python 是一种面向对象（OO）的语言，这意味着一切都是对象。类是创建对象的蓝图。它们定义了对象将拥有的数据（属性）和行为（方法）。

考虑这种情况：我们想在二维（2D）网格上表示 10 个点。这使用长度为 2 的列表来实现非常简单。如果我们想移动这些点（即更改列表中的值），我们可以通过 `for` 循环统一地为每个元素加 1.0。如果系统变得更复杂，例如每个点都有颜色、直径，并且能够判断它们距离原点的距离，我们的列表可能会迅速增长到难以管理和访问的大小。

与其跟踪点列表中的所有元素，我们可以创建一个具有直观命名且易于访问的变量和列表的 `GridPoint`。`GridPoint` 类中的函数第一个参数必须是 `self`。`self` 类似于 C++ 或 Java 中的 `this`，指的是被调用的类；然而，调用类方法时不需要包含 `self`。看下面的示例，我们在单独的文件 `grid.py` 中创建了 `GridPoint` 类，然后在我们的脚本中创建了同名的多个实例，但它们在 Python 命名空间中是独立的。

```python
# 独立文件 grid.py
from math import sqrt
class GridPoint(object):
    def __init__(self):
        # 在类创建时执行。
        self.color = None
        self.diameter = None
        self.pts = []
        self.pts.append(0.0)
        self.pts.append(0.0)
    def magnitude(self):
        # 调用时不需要参数，但定义时必须带有 "self"
        return sqrt(self.pts[0]**2 + self.pts[1]**2)
```

```python
mag = self.pts[0]*self.pts[0]+self.pts[1]*self.pts[1]
return sqrt(mag)
```

```python
# ---
# ---
```

# 我们的脚本文件。
from grid import GridPoint

# 创建 GridPoint 类的实例 mypoint，并设置列表元素。
mypoint = GridPoint()
mypoint.pts[0] = 1.0
mypoint.pts[1] = 2.0
```

```python
print(mypoint.magnitude())      # 2.2360679774997
grid = []                              # 创建一个列表。
for point in range(10):                   # 遍历序列
    # 创建 GridPoint 类的实例并将其添加到 grid 列表中。
    grid.append(GridPoint())
# 设置每个类实例中的某些变量。
grid[gridpoint].color = "blue"
grid[gridpoint].diameter = 5.0
grid[gridpoint].pts = [1.0,1,0.0]
```

## 9.2 Python 数字计算

### 9.2.1 Python 如何处理数字

Python 有两种常用的数字类型：`int`（整数）和 `float`（浮点数）。这与 C 等其他语言相似，但在 Python 中，每个 `float` 都以双精度 IEEE 754 表示形式存储。其他语言中关于 IEEE 754 浮点运算的所有注意事项也适用于 Python。基本运算符包括 `+`、`-`、`*`、`/=`（赋值）、`**`（幂）、`%`（取模）和 `//`（地板除）。标准库中的 `math` 模块提供了常用的数学函数。要打印 π 的浮点表示并打印它的余弦，可以执行以下操作：

```python
import math
print(math.pi)
print(math.cos(math.pi))
```

如果你频繁使用常用的数学函数，重复使用 `math` 前缀会使代码变得难以阅读。因此，对于 `math` 模块，使用 `from module import *` 而不是 `import module` 通常是可以接受的编码风格。本章通常遵循这一约定。

当数学运算涉及不同类型的操作数时，Python 会在执行操作前自动将整数转换为浮点数。它不会转换实际对象，而只是操作过程中使用的数学值。此外，在 Python 3 中，除法会将操作数转换为浮点数并返回浮点数。这与乘法运算符不同，如果操作数的类型为 `int`，则将返回 `int`。将 `int` 转换为 `float` 是很简单的；使用内置函数 `float()` 由数字或字符串提供的浮点数同样直接；如果你想向下取整，可以使用 `int()`，或者可以使用其他舍入操作：使用内置的 `round()` 获取最近的整数，或使用 `math` 模块中的 `ceil()` 向上取整。计算两点之间的距离有三种不同的方法。为了清晰起见，我们假设你正在解释器中运行，或者你会添加自己的 `print()` 函数。

```python
from math import *
class Point:
```

