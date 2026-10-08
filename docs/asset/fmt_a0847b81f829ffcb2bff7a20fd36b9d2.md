
`x = 0.0`

`y = 0.0`

`a = Point()` ; `b = Point()`

`b.x = 5.0` ; `b.y = 5.0`

`sqrt((b.x-a.x)**2+(b.y-a.y)**2)`

```
- a = [0,0]; b = [5,5]
  sqrt((b[0]-a[0])**2+(b[1]-a[1])**2)
  sqrt(sum([b[i]-a[i])**2 for i in [0,1]))
```

示例的第一部分展示了使用面向对象的方法寻找两点 `a` 和 `b` 之间的距离。定义了一个类，它具有默认值为 `0.0` 的属性 `x` 和 `y`。实例化两个对象 `a` 和 `b`，保留了默认值，并为 `b` 的属性分配了新值。

```python
mag = self.pts[0]*self.pts[0]+self.pts[1]*self.pts[1]
return sqrt(mag)
```

```python
# ---
# ---
```

# 我们的脚本文件。
`from grid import GridPoint`

# 创建 `GridPoint` 类的实例 `mypoint`，并设置列表元素。
`mypoint = GridPoint()`
`mypoint.pts[0] = 1.0`
`mypoint.pts[1] = 2.0`

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

当数学运算涉及不同类型的操作数时，Python 会在执行操作前将整数转换为浮点数。它不会转换实际对象，而只是操作过程中使用的数学值。此外，在 Python 3 中，除法会将操作数转换为浮点数并返回浮点数。这与乘法运算符不同，如果操作数的类型为 `int`，则将返回 `int`。将 `int` 转换为 `float` 是很简单的；使用内置函数 `float()` 由数字或字符串提供的浮点数同样直接；如果你想向下取整，可以使用 `int()`，或者可以使用其他舍入操作：使用内置的 `round()` 获取最近的整数，或使用 `math` 模块中的 `ceil()` 向上取整。计算两点之间的距离有三种不同的方法。为了清晰起见，我们假设你正在解释器中运行，或者你会添加自己的 `print()` 函数。

```python
from math import *
class Point:
    x = 0.0
    y = 0.0
a = Point() ; b = Point()
b.x = 5.0 ; b.y = 5.0
sqrt((b.x-a.x)**2+(b.y-a.y)**2)
```

- `a = [0,0]`; `b = [5,5]`
  `sqrt((b[0]-a[0])**2+(b[1]-a[1])**2)`
  `sqrt(sum([b[i]-a[i])**2 for i in [0,1]))`

# 开始使用 Python 3

现在的开发主要发生在 `scipy` 等模块中；导入 `numpy` 以使用其 `ndarray` 对象和方法。

## 9.2.3 Scipy

`Scipy` 是 Press、Teukovsky、Vetterling 和 Flattery 编写的经典教材《Numerical Recipes》（C 或 Fortran 语言）在 Python 中的对应版本。它包含了用于特殊函数（例如贝塞尔函数）、积分、优化、插值、傅里叶变换、信号处理、线性代数、特征值、数学图形、统计和多维图像处理的子包。它在线性代数包上与 `numpy` 有功能重叠，但通常 `scipy` 的实现功能更丰富或更新更及时。然而，只导入程序必需的模块是一个良好的习惯。如果 `numpy` 的线性代数包能够正确且高效地解决你的问题，那么就不需要 `scipy`；它只是调用相同 `numpy` 函数的接口。让我们来看一个使用 `scipy` `optimize` 模块的快速示例，优化是科学和工程领域普遍存在的问题：

```python
from scipy.optimize import minimize
def func(x):
    return x**3-x**2
minimize(func, 0.1)          # option 1
minimize(lambda x: x**3-x**2, 0.1)  # option 2
```

上面的示例使用 0.1 的初始估计值将函数 $f(x)=x^3-x^2$ 优化到局部最小值。使用的算法是拟牛顿法（BFGS，以其作者的首字母命名），尽管可以通过指定 `optimal method` 参数来更改它。找到的结果在默认容差范围内找到了最小值 2/3。对于本文作者来说，$x$ 的结果是 $0.66666539$。两次调用是等价的并返回相同的结果。包含第二个选项是为了演示 `lambda` 函数的使用，这是一种“即时”定义一次性使用函数的方法，而不是单独的代码块。`lambda` 是 Python 的一部分，但有时难以理解，且应该谨慎使用。`scipy` 包实现了多种优化方法，不仅用于局部最小化，还用于全局或最小二乘法最小化以及根寻器。每个特定方法通常都有许多用户可配置的参数，我们鼓励读者在将函数应用于自己的数据集之前咨询 `scipy` 文档。

## 9.2.4 数据科学

Python 是“数据科学”工作中极其受欢迎的语言，原因如下：

- 1. 能够利用以前在开源数值模块（如 `numpy`）中完成的工作，以及除统计建模之外的可用模块功能。
- 2. 与低级语言、数据库和 Web 框架具有良好的互操作性。这使得公司更容易将数据科学的输出集成到其生产环境中。

## 科学与技术计算简介

- 3. 高生产力设计和作为“趋势”语言的声誉。在数据科学作为一个高增长领域的时期（年轻开发者技能供应与雇主需求并存），Python 是“计算机科学导论”课程最流行的语言。与 C++ 或 R 相比，对于没有 CS 训练的领域专家来说更容易学习。

数据科学相关工作需要学习两个重要的库是 `pandas` 和 `scikit-learn`。`pandas` 是一个旨在处理“关系型”或“标记”数据的包。它内置为统计工作提供了大量功能，而这些功能以前可能需要在 Microsoft Excel、merge 或 R 中完成。它还允许你对 SQL 查询进行操作，快速检索复杂的数据集。`pandas` 最常用的对象是其 `DataFrame`，它是一个通用的二维可变对象，允许许多类型——简而言之，它就像一个 Excel 表格，但通过 `pandas` 和 Python 标准库提供的各种方法可以使用更多功能。`scikit-learn` 是一个机器学习库，提供了如贝叶斯回归、支持向量机、高斯过程、决策树、聚类、集成方法（包括随机森林）、主成分分析、因子分析和基础神经网络等技术。它通常应用于分类或回归问题。但 `pandas` 和 `scikit-learn` 也可以帮助你学习许多高级机器学习库，特别是神经网络或深度学习。这是一个高级模块，如果你想在 `scikit-learn` 提供的工具之外追求这一主题，这是一个起点。对于具体的示例，我们建议读者参考 `pandas` 和 `scikit-learn` 的当前网页。

## 9.3 Python 扩展

### 9.3.1 Python 风格

Python 最佳实践鼓励使用“PEP 8”（被称为 Python 增强提案 0008）中记录的编码风格。许多编辑器（如 Spyder，在第 9.3.5 节中讨论的 IDE）会在你编写 Python 代码时自动检查其是否符合 PEP 8 标准。这种将推荐的风格指南（而非语言标准）、即时检查工具以及将空格作为语言标准的一部分相结合的结合，使得由一个作者编写的 Python 代码对所有人来说都具有惊人的可读性。这是 Python 的设计原则之一，正如 PEP 20《Python 之禅》中所提到的：“代码的可读性至关重要。”例如，PEP 8 建议使用四个空格进行缩进，而不是两个空格。这使得你的代码对其他 Python 程序员来说是可读的——他们会习惯这种风格——并确保在大型代码库中缩进级别和类型不会混合。事实上，Python 不允许制表符（tabs）和空格混合。建议在赋值运算符周围留空格；例如，使用 `a = b` 而不是 `a=b`。空格会拉长源代码行，但 PEP 8 也建议限制每行 80 个字符。对于续行，PEP 8 建议使用圆括号、方括号或花括号进行隐式连接。
最后，记住这些是风格指南，而不是语言标准。PEP 8 还说“知道”何时保持一致——风格并不总是适用。”Python 及其风格旨在方便程序员并实现高生产力。

### 9.3.2 并行

如果要进行数值计算，将 Python 与并行的 C 或 Fortran 程序对接，你最终将希望使用所有可用的 CPU 核心。Python 有许多实现方法：`multiprocessing` 适用于标准库和第三方库 `mip4py`。`multiprocessing` 是共享内存并行，而消息传递接口（MPI）编程适用于共享和分布式内存。除了位于标准库中任何人使用 Python 即可可用，`multiprocessing` 的流行是因为它通过使用 避免了“全局解释器锁（GIL）”。GIL 是一种锁，在 Python 解释器允许访问 Python 对象之前必须持有。它一次只能由一个线程持有；因此，避免 GIL 可以提高性能。对于下面的并行 Python 示例，我们假设使用命令行。这很重要，因为 `multiprocessing` 模块应该从脚本执行命令，而不是在交互式提示符逐逐输入命令。使用 `__name__=='main__` 结构来保护模块的“入口”；基本上，如果产生了一个进程，你不希望它认为自己是原始进程并重新执行脚本中的所有命令。Windows 和 Linux 处理产生的方式不同，如果你编写更复杂的进程进程代码，理解这种行为是非常重要的。让我们从“Hello, World.”开始。

```python
import multiprocessing
```

```python
def worker(n):
    my_name = multiprocessing.current_process().name
    return 'Worker %d using process %s' (n, my_name)
```

```python
def hello_world():
    pool = multiprocessing.Pool(2)
    results = pool.map(worker, range(4))
    pool.close()
    print(multiprocessing.active_children())
```

# 134 科学与计算导论

```python
for message in results:
    print (message)
```

```python
if __name__ == '__main__':
    hello_world()
```

该示例通过创建一个 `Pool()` 启动了两个进程，并创建一个包含四个工作线程（workers）的映射以使用这些进程。工作线程函数的结果通过关闭进程池来收集，随后由主线程打印结果。这是用于数值计算并行化的方法之一。计算机在这些进程上调度工作的方式取决于具体实现：例如，对于一个简单任务，所有的工作线程可能运行在同一个进程中（使用 Windows 系统）。重复调用将导致不同的负载均衡。你可以你自己也尝试几次，然后我们来看上一个使用 `mpi4py` 的示例。它已经安装以及及其依赖项；通常情况下，在 Linux 上尝试是最好的，而且取决于你手头的系统，在 Python 2.7 上尝试可能会更容易。

```python
from mpi4py import MPI
comm = MPI.COMM_WORLD
rank = comm.Get_rank()
size = comm.Get_size()
name = MPI.Get_processor_name()
print("Hello, World! I am process %d of %d on %s" % (rank, size, name))
MPI.Finalize()
```

最终，基于 MPI 的并行化在科学计算中更为常见，正如在超级计算机之间的通信中那样。我们经常看到传统的高性能计算（HPC）应用使用 C 和 Fortran 的 MPI 绑定，它们对于等效代码通常比 Python 更快，并且展示出比 Python 更好的扩展性（特别是在程序初始化期间）。上面的示例使用的是 `mpi4py`，但 Python 有多个 MPI 库，用户应该探索其他有用的选项。Python 标准库中也有与并发任务相关的选项，例如 `threading` 模块。

### 9.3.3 Matplotlib

`Matplotlib` 是一个 Python 库，允许用户通过数组或列表数据创建简单的图表，并只需几行代码将其输出为图像。它大量使用了 `numpy`，并为大型数组数据提供了良好的性能。该库可以轻松生成简单的图表、直方图、矢量场和三维等高线。下面是一个 `matplotlib` 直方图的示例，使用了变量 `resListX` 中的真实数据集和范围变量 `numResX`。如果你将此代码粘贴到解释器中它将无法执行——相反，我们鼓励读者生成生成 0 到 200 之间的随机数列表。

```python
from matplotlib import pyplot
```

```python
pyplot.hist(resListX, bins = numResX, range = [0.5,numResX+0.5], align = 'mid', facecolor = 'g', rwidth = 0.9, alpha = 0.75)
```

## 开始 Python 3

```python
plt.axis([0.5, numResX+0.5, 0, 15])
plt.xlabel("Residue on X")
plt.ylabel("Frequency")
plt.grid(True)
plt.savefig("contact_map_example")
```
