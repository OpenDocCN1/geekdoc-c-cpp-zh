

```
character_inventory.insert(2, 'staff')
```

```
character_inventory
```

```
['spell scroll', 'leather armor', 'staff', 'healing herb', 'bag of gold']
```

在这种情况下，我们在索引为 2 的项之后添加了一个新元素。接下来，让我们用下面一行代码从列表中删除一个特定元素：

```
character_inventory.remove('leather armor')
```

```
character_inventory
```

```
['spell scroll', 'staff', 'healing herb', 'bag of gold']
```

但是，如果你想删除一个元素并同时返回它的值，该怎么办？当然，你可以发出两条单独的指令，但这可以用一条命令完成。记住，如果有办法让你的代码更简单、更易读，就应该采用它。此操作通过“pop”方法完成，它接受元素的位置作为参数。请记住，如果不指定索引，默认会选择最后一个元素。它在代码中如下所示：

```
character_inventory.pop(-2)
```

```
'healing herb'
```

```
character_inventory
```

```
['spell scroll', 'staff', 'healing herb', 'bag of gold']
```

如你所见，我们选择了一个负索引位置，这导致倒数第二个元素被删除，随后返回了它的值。

最后，让我们看看如何对列表进行排序。有两种常见方法。第一，你可以使用“sort”方法，它直接对列表进行修改。第二，你可以改用“sorted”方法，它会返回一个新的已排序列表，而不修改原列表。这两种方法非常相似，所以尽量不要把它们混淆。下面是一个示例：

```
sorted(character_inventory)
```

```
['bag of gold', 'healing herb', 'staff', 'spell scroll']
```

```
character_inventory.sort()
```

现在，让我们借助“reverse”方法反转原列表的顺序：

```
reversed(character_inventory)
```

```
<listreverseiterator object at 0x81abf0c>
```

```
character_inventory.reverse()
```

```
character_inventory
```

```
['spell scroll', 'staff', 'healing herb', 'bag of gold']
```

请注意，当我们使用某些方法和函数改变序列时，有时响应中不会得到一个新序列，而是返回一个对象。例如，在我们的示例中，我们有一个迭代器对象。它会在“for”循环中像序列一样使用。因此，当我们使用“reversed”函数时，我们获得了一个反转的迭代器对象。它的工作方式如下：

```
for element in reversed(character_inventory):
    print element
```

```
spell scroll
staff
healing herb
bag of gold
```

## 进入矩阵

不，不是那部电影，而是多维列表！这是一种花哨的说法，意思是我们可以在其他列表内部嵌套列表，从而形成矩阵或多维列表。这样，我们就可以用列表以表格形式保存数据。下面是一个将嵌套列表赋值给变量的示例：

```
my_matrix = [[11, 12, 13], [21, 22, 23], [31, 32, 33]]
```

这是一个三乘三矩阵。如果你还记得小学数学课，它可能看起来很熟悉。

遍历列表时，你大概应该使用“for”循环，因为这被视为标准做法。为什么？因为如果你不确定列表包含多少个元素，你的系统知道。计算机就是这样神奇。然而，如果你处理的是矩阵，则应在“for”循环中使用“for”循环。换句话说，你需要嵌套循环，而且列表的每一维都需要嵌套循环。接下来，你可以使用“enumerate”函数来获取索引值。让我们先看一个列表示例，然后看一个矩阵示例：

```
for x, value in enumerate(character_inventory):
    print x, value
```

```
0 spell scroll
1 staff
2 healing herb
3 bag of gold
```

现在让我们看看矩阵版本：

```
for row in my_matrix:
    for x, value in enumerate(row):
        print x, value,
    print
```

```
0 11 1 12 2 13
0 21 1 22 2 23
0 31 1 32 2 33
```

### 字典

这类数据序列类似于黄页。只要有一个名字可供搜索，你就能找到他的电话号码和其他信息。在这个示例中，人的名字称为键，数据以值的形式出现。键本身不可变，这意味着它只能是字符串、元组或数字，而值可以是任何类型的数据。然而，字典是可变结构。这意味着你可以编辑若干值。这包括添加和删除它们，以及更改键。顺便说一句，字典也称为映射，因为它们的键被映射到特定对象。这使它们与其他序列显著不同，这也是它们还有一个替代名称的原因。

如果你熟悉其他编程语言，可能会注意到，与字典结构类似的数据类型称为哈希或关联数组。这些差异很重要，因为决定键的值实际上是哈希值。这意味着什么？哈希键可用于存储较大的键，因为它们实际上是由键定义的小值。现在这一切可能听起来非常令人困惑，然而 Python 会根据哈希键来排列字典内部的数据，而不是按字母顺序排列。因此，如果你修改值，由它产生的哈希也会被修改，于是程序将无法找到存储在其中的值。这就是键不可变的原因。

现在让我们把理论放在一边，看看字典在代码中是什么样子。请记住，它们由键值对定义。它们用冒号分隔，并包含在花括号中。确保不要将花括号与方括号和圆括号混淆，因为如果把它们弄混，应用程序将无法正确响应。话虽如此，下面是一个示例：

```
character_profile = {'Name':'','Description':'', 'Race':'',
'Sex':'','Strength':0,'Intellect':0,'Dexterity':0,'Charisma':0}
```

```
character_profile['Name'] = "Player"
```

```
print character_profile['Name'], "has", character_profile['Intellect'], "Intellect"
```

```
Player has 0 Intellect
```

当你传入对字典内部某个元素的引用时，需要使用方括号。然而，请记住，它的工作方式与列表不同，在列表中我们可以使用表示元素位置的索引值。字典项没有位置。相反，我们有键以及与之匹配的值。这意味着我们需要调用键来引用其值。语法大致如下“dictionary[key] = value”。请记住，键的名称必须位于引号之间，否则它将被视为变量。在字典元素中导航的另一种方法是使用‘for’循环。如你所见，循环在多种情况下都非常方便。下面是一个示例：

```
for key in character_profile:
    print key,
```

```
Intellect Name Sex Race Charisma Strength Dexterity Description
```

如果你需要访问值，需要输入“profile[key]”，但如果你需要检查某个键是否存在，则需要在 profile 中查找该键。检查的结果要么为 true，要么为 false。唯一的其他可能性是错误。然而，假设你不确定某个键是否已经存在。在这种情况下，你可以使用以下方法：

```
get(key, default)
```

这里我们需要使用参数。第一个表示你感兴趣的键。第二个参数表示键不存在时的默认值。现在，让我们看一些代码：

```
character_profile.get('Name')
```

```
'Player'
```

```
character_profile.get('Sex', 'unknown')
```

```
''
```

```
character_profile.get('Health', 'not found')
```

```
'not found'
```

你会注意到我们有这个键，但只有一个空值，而不是一条消息。现在，让我们看看如何从字典中删除一个元素：

```
character_profile
{'Name': 'Player', 'Sex': '', 'Race': '',
'Charisma': 0, 'Strength': 0, 'Dexterity': 0, 'Description': ''}
```

```
del character_profile['Sex']
```

```
character_profile
{'Name': 'Player', 'Race': '', 'Charisma': 0, 'Strength': 0, 'Dexterity': 0,
'Description': ''}
```

如你所见，与其他序列一样，为了删除一个元素，我们必须使用“del”方法。此外，如果你需要从字典中删除一个值，可以像前面演示的那样使用“pop”方法。

### 排序

