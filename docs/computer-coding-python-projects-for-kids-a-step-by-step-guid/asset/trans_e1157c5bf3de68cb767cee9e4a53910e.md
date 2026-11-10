

## 列表

当你想存储大量数据，或者数据的顺序很重要时，你可能需要使用列表。列表可以将许多条目集中在一起，并保持它们的顺序。Python 会给每个条目一个编号，用来表示它在列表中的位置。你可以随时修改列表中的条目。

![](img/1bd24ab186f69fb18194b4174ca15178_26_0.png)

### 1 多个变量

想象你正在编写一个多人游戏，想要存储每支队伍中玩家的名字。你可以为每个玩家创建一个变量，就像这样……

```python
>>> rockets_player_1 = 'Rory'
>>> rockets_player_2 = 'Rav'
>>> rockets_player_3 = 'Rachel'
>>> planets_player_1 = 'Peter'
>>> planets_player_2 = 'Pablo'
>>> planets_player_3 = 'Polly'
```

如果每队有 3 名玩家，你就需要 6 个变量。

### 2 将列表放入变量

……但若每队有 6 名玩家呢？管理和更新这么多变量会很困难。这时最好使用列表。要创建列表，你需要用方括号将要存储的条目括起来。请在 shell 中试试这些列表。

```python
>>> rockets_players = ['Rory', 'Rav',
'Rachel', 'Renata', 'Ryan', 'Ruby']
>>> planets_players = ['Peter', 'Pablo',
'Polly', 'Penny', 'Paula', 'Patrick']
```

列表中的条目必须用逗号分隔。

这个列表存储在变量 planets_players 中。

### 3 从列表中获取条目

一旦你的数据存入列表，处理起来就非常方便。要从列表中取出一个条目，先输入列表名，然后在方括号内加上该条目的位置。注意：Python 是从 0 而不是 1 开始对列表条目计数的。现在试着从你的队伍列表中取出不同玩家的名字。第一个玩家位于位置 0，而最后一个玩家位于位置 5。

```python
>>> rockets_players[0]
'Rory'
>>> planets_players[5]
'Patrick'
```

这行代码从位置 0 获取列表中的第一个条目。

这行代码从位置 5 获取列表中的最后一个条目。

按回车键即可取出该条目。

## 菠萝与斑马

让我们在 shell 中试一个例子。我们可以使用变量 `pineapples` 和 `zebras` 来表示有 5 个菠萝和 2 只斑马。请在 shell 中输入这些行。

```python
>>> pineapples = 5
>>> zebras = 2
```

这个变量存储菠萝的数量。

这个变量存储斑马的数量。

![](img/1bd24ab186f69fb18194b4174ca15178_28_0.png)

### 进行比较

现在试着输入以下代码行来比较这两个变量的值。每输完一行，按回车键，Python 会告诉你这些语句是 True 还是 False。

菠萝的数量大于斑马的数量。

```python
>>> pineapples > zebras
True
```

```python
>>> zebras < pineapples
True
```

斑马的数量小于菠萝的数量。

菠萝的数量和斑马的数量不相等。

```python
>>> pineapples != zebras
True
```

**术语**

### 布尔表达式

使用逻辑运算符对变量和值进行判断的语句，总会给出一个布尔值，例如 True 或 False。因此，这些语句被称为布尔表达式。我们所有关于菠萝和斑马的判断语句都是布尔表达式。

变量

逻辑运算符

```python
>>> pineapples != zebras
True
```

布尔值

变量

### 多重比较

你可以使用 `and` 和 `or` 组合多个比较。如果使用 `and`，比较的两个部分都必须正确，语句才是 True。如果使用 `or`，只需要有一部分正确即可。

```python
>>> (pineapples == 3) and (zebras == 2)
False
```

其中一部分（pineapples == 3）不正确，因此语句为 False。

```python
>>> (pineapples == 3) or (zebras == 2)
True
```

有一部分正确（zebras == 2），因此语句为 True。

## 乘坐过山车

主题公园的告示牌上写着：必须年满 8 岁且身高超过 1.4 米才能乘坐过山车。米娅 10 岁，身高 1.5 米。让我们用 shell 检查她是否能乘坐。输入以下代码行，为米娅的年龄和身高创建变量并赋予正确的值。将乘坐过山车的规则写成布尔表达式，然后按回车键。

![](img/1bd24ab186f69fb18194b4174ca15178_29_0.png)

这两行给变量赋值。

```python
>>> age = 10
>>> height = 1.5
>>> (age > 8) and (height > 1.4)
True
```

这是一个布尔表达式，表示“年龄大于 8 岁且身高超过 1.4 米”。

米娅可以乘坐过山车！

### 分支

计算机经常需要决定运行程序中的哪些部分。这是因为大多数程序设计为在不同情况下执行不同的操作。程序的路径如同一棵路径树，分叉出旁路，每条通向不同的地方。

![](img/1bd24ab186f69fb18194b4174ca15178_29_1.png)

**术语**

### 条件

条件是一种布尔表达式（一种 True 或 False 的比较），可帮助计算机在到达代码分支时决定走哪条路径。

#### 上学还是去公园？

想象一下，你必须根据“今天是工作日吗？”这个问题的答案来决定每天走哪条路。如果是工作日，就走去学校的路；如果不是，就走去公园的路。在 Python 中，程序的不同路径通向不同的代码块。一个代码块可以是一条语句或多条语句，它们都缩进四个空格。计算机使用一种叫作条件的测试来判断接下来应运行哪些代码块。

![](img/1bd24ab186f69fb18194b4174ca15178_29_2.png)

#### 单分支

最简单的分支命令是 `if` 语句。它只有一个分支，当条件为 True 时，计算机就会走这个分支。这个程序询问用户外面是否天黑。如果答案是“是”，程序就假装计算机要睡觉了！如果外面不黑，`is_dark == 'y'` 为 False，因此不会显示 “Goodnight!” 消息。

这一行要求用户回答 “y”（是）或 “n”（否）。

```python
is_dark = input('Is it dark outside? y/n')

if is_dark == 'y':
    print('Goodnight! Zzzzzzzzzzzzz....')
```

条件

如果条件为真，则走此分支。

该代码会在 shell 窗口中显示这条消息。

#### 双分支

你是否希望程序在条件为 True 时做一件事，在条件为 False 时做另一件事？如果是这样，你需要一个具有两个分支的命令，称为 `if-else` 语句。这个程序询问用户是否有触手。如果回答“是”，它就判断用户一定是一只章鱼！如果回答“否”，它就判断用户是人类。每次判断都会打印不同的消息。

这一行要求用户输入。

条件

```python
tentacles = input('Do you have tentacles? (y/n)')
if tentacles == 'y':
    print('I never knew octopuses could type!')
else:
    print('Greetings, human!')
```

如果条件为 True，则运行此代码块。

如果条件为 False，则运行此代码块。

#### 多分支

当可能的路径多于两条时，`elif` 语句（“else-if”的缩写）就派上用场了。这个程序要求用户输入天气预报：“rain”“snow”或“sun”。然后它会从三个分支和天气条件中选择一个。

```python
weather = input('What is the forecast for today? (rain/snow/sun)')

if weather == 'rain':
    print('Remember your umbrella!')
elif weather == 'snow':
    print('Remember your woolly gloves!')
else:
    print('Remember your sunglasses!')
```

第一个条件

如果第一个条件为 True，则运行此代码块。

第二个条件

如果第二个条件为 True，则运行此代码块。

如果两个条件都为 False，则运行此代码块。

![](img/1bd24ab186f69fb18194b4174ca15178_30_0.png)

#### 工作原理

`elif` 语句必须始终位于 `if` 之后、`else` 之前。在这段代码中，只有当 `if` 语句设置的条件为 False 时，`elif` 才会检查是否下雪。你可以插入更多 `elif` 语句来检查更多天气类型。

