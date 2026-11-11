
你希望为用户提供菜单式选择的不同程序。如果计算机程序员希望为其用户提供一些选项，而不仅仅是一两个选项，那么这些语句将最常被使用。

## 第3章：数据结构

Python 基于三种引用结构：元组、列表和字典。这些结构实际上是可能包含其他对象的对象。它们具有相当不同的用途，并允许你存储各种类型的信息。

这些结构具有一些共同特征：

- 要从结构中提取一个或多个对象，我们总是使用 `[]`
- 对于按数字索引的结构（元组和列表），结构的索引从 0 开始（第一个位置是位置 0）

### 元组

这是一种按索引顺序将多个对象分组的结构。它的形式一旦创建就不可修改（不可变），并使用圆括号定义。它只有一维。任何类型的对象都可以存储在元组中。例如，如果你想创建一个包含不同对象的元组，我们使用：

```python
tup1 = (1, True, 7.5, 9)
```

你也可以使用 `tuple()` 函数创建元组。访问元组的值通过经典的结构索引完成。因此，如果我们想访问元组的第三个元素，我们使用：

```python
In []: tup1[2]
Out []: 7.5
```

元组可能很有趣，因为它们需要很少的内存。另一方面，它们被用作返回多个值的函数的输出。元组作为结构是对象。它们具有简洁的方法。元组的方法很少：

```python
In []: tup1.count(9)
Out []: 1
```

我们通常更喜欢更灵活的列表。

### 列表

列表是 Python 中的引用结构。它是可修改的，并且可以包含任何对象。

### 创建列表

我们使用方括号创建列表：

```python
list1 = [3, 5, 6, True]
```

你也可以使用 `list()` 函数。列表的结构是可编辑的。它有许多方法：

- `.append()`：在列表末尾添加值
- `.insert(i, val)`：将值插入到索引 i
- `.pop(i)`：取出索引 i 的值
- `.reverse()`：反转列表
- `.extend()`：用值列表扩展列表
- `.remove(val)`：从列表中移除值 val 的第一次出现

注意——所有这些方法都会修改列表，经典代码中的等效写法如下：

```python
list1.extend(list2)
```

等价于

```python
list1 = list1 + list2
```

列表还有其他方法，包括：

- `.index(val)`：返回值 val 的索引
- `.count(val)`：返回值 val 出现的次数

### 从列表中提取一项

如上所述，可以使用方括号提取元素：

```python
list1[0]
```

我们经常对提取多个元素感兴趣。这是通过使用两个点来完成的：

```python
list1[0:2] or list1[:2]
```

在这个例子中，我们看到这个系统提取了两个元素：索引为 0 的元素和索引位置为 1 的元素。因此我们有一条规则：`i:j` 从包含元素 i 到不包含元素 j。以下是一些其他示例：

```python
# Extract the last element
list1[-1]
```

提取最后 3 个元素：`list1[-3:-1]` 或 `list1[-3:]`

### 一个具体示例

假设我们想创建一个国家列表。这些国家在列表中按其人口排序。我们将尝试提取前三个和最后三个。

```python
In []: country_list = ["China", "India", "United States", "France", "Spain", "Switzerland"]
In []: print(country_list[:3])
['China', 'India', 'United States']
In []: print(country_list[-3:])
['France', 'Spain', 'Switzerland']
In []: country_list.reverse()
print(country_list)
['Switzerland', 'Spain', 'France', 'United States', 'India', 'China']
```

### 列表推导式

这些是迭代构建的列表。它们通常非常有用，因为它们比使用循环构建列表更高效。这里有一个简单的例子：

```python
In []: list_init = [4, 6, 7, 8]
list_comp = [val ** 2 for val in list_init if val % 2 == 0]
```

`list_comp` 列表允许你存储 `list_init` 中设置为平方的偶数元素。

我们将得到：

```python
In []: print(list_comp)
[16, 36, 64]
```

列表推导式的概念非常有效。它避免了无用的代码（对列表的循环），并且比迭代创建列表表现更好。它也存在于字典中，但不存在于不可变的元组上。我们能够在数据表操作的框架中使用列表推导式。

### 字符串——字符列表

Python 中的字符串默认（自 Python 3 起）以 Unicode 编码。你可以通过三种方式声明字符串：

```python
string1 = "Python for the data scientist"
string2 = 'Python for the data scientist'
string3 = """ "Python for the data scientist" """
```

最后一种允许字符串跨越多行。我们将最常使用第一种。字符串实际上是一个字符列表，我们将能够像处理列表元素一样处理字符串的元素：

```python
In []: print(string1[:6])
print(string1[-14:])
print(string1[3:20])
```

**面向数据科学家的Python**

数据字符串可以轻松转换为列表：

```python
In []: # we separate the elements using space
list1 = string1.split()
print(list1)
['Python', 'for', 'the', 'Data', 'Scientist']
In []: # we join the elements with space
string1bis = " ".join(list1)
print(string1bis)
```

### 字典

字典构成了 Python 中要开发的第三种核心结构。它们允许键值存储。到目前为止，我们使用了基于数字索引的项。所以在列表中，你使用其位置 `list1[0]` 访问元素。在字典中，我们将使用创建字典时定义的键来访问元素。我们使用花括号定义字典：

```python
dict1 = {"key1": value1, "key2": value2, "key3": value3}
```

这种结构不要求值在类型上具有任何同质性。由此，我们可以有一个像 value1 这样的列表、一个像 value2 这样的布尔值，以及一个整数 value3。

要访问字典中的元素，我们使用：

```python
In []: dict1["key2"]
Out []: value2
```

要显示字典的所有键，我们使用：

```python
In []: dict1.keys()
Out []: ("key1", "key2", "key3")
```

要显示字典的所有值，我们使用：

```python
In []: dict1.items()
Out []: (value1, value2, value3)
```

可以轻松修改或向字典添加键：

```python
In []: dict1["key4"] = value4
```

你也可以删除字典中的键（以及关联的值）：

```python
In []: del dict1["key4"]
```

一旦你在 Python 中更有经验，你就会使用更多字典。起初，我们倾向于优先使用列表而不是字典，因为列表通常更直观（使用数字索引）。然而，更资深的 Python 专家会很快意识到字典的用处。特别是，我们将能够以非常简单的方式存储数据以及模型的参数。此外，Python 的 for 循环的灵活性非常适合字典，并且在字典构建良好时使其非常有效。

### 编程

### 条件

Python 中的条件实现起来非常简单；它是一个关键字。如前所述，Python 语言基于代码的缩进。我们将使用四个空格的偏移量进行缩进。幸运的是，像 Spyder 或 Jupyter notebooks 这样的工具会自动生成这种缩进。

这是我们的第一个条件，意思是“如果 a 为真，则显示”“它为真”：

```python
if a is True:
    print("it's true")
```

没有退出条件；正是缩进允许管理它。通常，我们也对这个条件的补集感兴趣；我们将为此使用 else：

```python
if a is True:
    print("it's true")
else:
    print("it's not true")
```

如果我们的变量 a 不一定是布尔值，我们可以有另一种情况，我们使用 elif：

```python
if a is True:
    print("it's true")
elif a is False:
    print("it's wrong")
else:
    print("it's not a boolean")
```

### 循环

循环是大多数编程语言的核心元素。Python 没有打破这条规则。然而，对于像 Python 这样的解释型语言，你必须非常小心。事实上，Python 中循环的处理很慢，我们将在迭代次数很少的循环中使用它。我们
