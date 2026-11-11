
在父序列或切片序列中，两者中的数据都会发生变化。

## 序列检查

有时你需要创建一个序列检查，以验证某一项是否属于某个序列。这可以借助“in”关键字来完成，它是一个布尔值，会根据某条数据的成员关系返回 true 或 false。下面是一个使用前面代码的简单示例：

```
"pear" in buildings
False
```

如果你想要得到相反的结果，也可以加上“not”关键字：

```
"pear" not in buildings
True
```

此外，你还可以使用其他运算符来进行序列组合：

```
"sun" + "flower"
"sunflower"
```

你还可以使用 join() 方法来组合字符串。如你所见，我们有不同的方式来组合不同类型的数据。这也适用于我们执行的其他操作。根据数据类型的不同，所需的函数、方法和运算符也必须进行相应调整。不过，在大多数情况下，你要么使用加号和减号之类的数学运算符，要么使用“in”“or”等关键字。

虽然我们还没有介绍方法，但你应该知道，访问方法的方式是在某个变量后加一个句点。方法还在圆括号内包含参数。在我们的例子中，这种方法的一个示例是 `separator.join(seq)`。join 是方法本身，如你所见，它与函数相当相似。但是，它们绑定到特定对象，例如某种数据类型。我们将在后面的章节中更详细地讨论对象和方法。现在你应该知道，对象是数据类型的各种实例。

对于字符串而言，使用 join 方法时，序列将作为参数传入。结果将是一个单独的字符串，其中包含序列中的所有项，并与初始字符串的副本组合在一起。下面是它在代码中的样子：

```
", ".join(buildings)
"store, house, hospital, school"
```

如果这看起来有点令人困惑，你可以通过添加 `sep = ", "` 然后调用 join 方法来改变它，以提高可读性。

接下来，我们可以将字符串划分为各个元素，从而创建一个列表。这可以通过“split”方法完成，看起来会像这样：

```
string.split(separator, max)
```

如你所见，拆分时必须指定第二个参数，它表示我们可以拆分字符串多少次。

```
buildings = "store, house, hospital, school, church"
buildings = buildings.split(", ")
buildings
['store', 'house', 'hospital', 'school', 'church']
```

现在我们将字符串拆分为元素，就可以根据需要处理或操作它们了。我们甚至可以将序列转换为其他类型的序列。例如，我们可以使用 list 方法将一个序列转换为列表。下面是一个将字符串转换为字符列表的示例：

```
list('house')
['h', 'o', 'u', 's', 'e']
```

现在让我们改为将一个序列转换为元组：

```
tuple(buildings)
('store', 'house', 'hospital', 'school', 'church')
```

你也可以像下面的示例那样，将列表转换为字符串：

```
str(buildings)
"['store', 'house', 'hospital', 'school', 'church']"
```

另一个有用的指令是“len”，它允许你查明某个序列有多少个元素。这对我们的短序列来说可能并不重要，但想象一下一个包含数百甚至数千个元素的列表。你不会开始逐个计数。下面是它的工作方式：

```
len(buildings)
5
```

另外两个有用的命令是“max”和“min”，它们会获取序列中排序最高的元素和最低的元素。下面是它们的工作方式：

```
max(buildings)
'store'
min(buildings)
'church'
```

你可能以为 max 关键字会返回索引最高的项，而 min 关键字会做相反的事，对吧？事实并非如此。序列是有顺序的，你现在可能会注意到，它们是按字母顺序选择的。即使我们没有特意对元素排序，它们也有默认顺序。由于这种排序顺序，你也可以使用比较运算符来比较多个序列。假设我们有第二个名为“jobs”的序列，它也包含五个元素。如果你比较它们，Python 会判定其中一个大于另一个。它在代码中看起来会像这样：

```
jobs > buildings
False
buildings == jobs
False
```

请记住，如果你尝试与空序列进行比较，结果将始终显示 `False`。

## 元组

你之前了解到，元组是不可变数据结构之一，包含按特定顺序排列的若干元素。事实上，它们与列表几乎相同，只是不能被修改。本质上，它们是包含锁定在内部的信息的数据包。

元组是用逗号分隔并包含在圆括号之间的值列表。请注意，圆括号并不总是必需的，但尽管如此，你仍应使用它们，以避免任何混淆和可能的错误。元组的另一个特征是，它包含的值不必是相同的数据类型。元组甚至可以包含其他元组，或者完全不包含元素。下面是一个空元组的示例：

```
emptyTuple = ()
```

下面是一个包含一个元素的元组：

```
lonelyTuple = ('element',)
```

元组像列表一样以序列形式出现。但是，你不能更改它们的值。元组的目的不是为你提供可编辑的数据。它们被密封起来，因为其用途是在需要将某个值传递给其他对象而不改变其状态时使用。如果你需要操作任何数据，应该改为创建一个列表。

## 列表

与元组类似，列表包含若干用逗号分隔的元素，但它们放在方括号之间，而不是圆括号之间。列表也可以包含各种数据类型，包括其他列表。此外，我们可以对它们执行许多操作，例如连接、索引、切片等。本质上，你可以对其他类型的序列做的任何事情，都可以对列表做。然而，与其中一些不同，列表是可变结构，这意味着你可以编辑和操作其中包含的元素。你还可以对它们进行切片，然后为这些片段赋值或分配数据，从而大幅改变列表本身。下面是一个用 Python 编写列表的简单示例：

```
character_inventory = ['sword', ['more', 'lists'], 'bag of gold', '2 healing potions']
```

要编辑列表并添加新项，你可以借助索引执行以下操作：

```
character_inventory[1] = 'leather armor'
character_inventory
['sword', 'leather armor', 'bag of gold', '2 healing potions']
```

接下来，你甚至可以用另一个序列替换列表的一部分。方法如下：

```
character_inventory[::2] = ['spell scroll', 'healing herb', 'pet rock']
character_inventory
['spell scroll', 'leather armor', 'healing herb', 'bag of gold', 'pet rock']
```

当我们定义新切片时，没有说明它应该从哪里开始或结束。唯一提到的是它的步长应等于 2。这意味着列表中每隔一个项都会受到这次修改的影响。

接下来，我们有一些方便的方法，可以将新元素引入列表。例如，我们有“append”和“extend”。第一个选项只是添加新元素，而第二个选项会添加在其他列表中找到的项。下面是同时使用这两个方法的示例：

```
character_inventory.append('raw meat')
character_inventory
['spell scroll', 'leather armor', 'healing herb',
 'bag of gold', 'pet rock', 'raw meat']
character_inventory.extend(['mace', 'flask'])
character_inventory
['spell scroll', 'leather armor', 'healing herb',
 'bag of gold', 'pet rock', 'raw meat', 'mace', 'flask']
```

现在让我们删除一些元素。这就是“del”关键字的用途，但你需要记住，此操作不会从列表中删除数据本身。它只会移动对某个项的引用；如果该项在另一个数据结构中使用，内部不会有任何变化。下面是一个示例：

```
del character_inventory[4:]
character_inventory
['spell scroll', 'leather armor', 'healing herb', 'bag of gold']
```

如你所见，从第四个元素开始，列表的一整段被删除了。现在，让我们通过输入以下命令向列表添加一个元素：
