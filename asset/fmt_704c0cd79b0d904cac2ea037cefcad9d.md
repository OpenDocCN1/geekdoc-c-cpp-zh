
## 问题 2
写一个函数 `list_dates`，列出为特定用户拥有卡路里数据的日期。例如，函数 `os.listdir('robert')` 会产生 `robert` 目录下的文件列表（未排序）。

现在，我们可以写一个函数来查找 `calories.txt` 中某某特定食物的卡路里数：

```python
def lookup_calories(food):
    table = table_of_file('calories.txt')
    vs = table[food]
    if vs is None:
        print(f'{food} not found')
    else:
        if len(vs) > 1:
            weight = vs[0]
            calories = vs[1]
            print(f'There are {calories} calories in {weight}g of {food}')
        else:
            print(f'Malformed entry for {food} in calories')
```

我们使用了字典来查找食物的卡路里和体重，并从列表中提取它们。

## 问题 3
写一个 `lookup_weight`，根据名称和日期，如果可用，则打印该日期的体重。为了计算特定日期的总卡路里，我们必须从用户的食物记录和卡路里数据中合并数据：

```python
def total_date(name, date):
    calories = table_of_file('calories.txt')
    table = table_of_file(os.path.join(name, date) + '.txt')
    total = 0
    for k, vs in table.items():
        weight_and_calories = calories[k]
        reference_weight = int(weight_and_calories[0])
        reference_calories = int(weight_and_calories[1])
        weight = int(vs[0])
        calories_per_gram = reference_calories / reference_weight
        total += weight * calories_per_gram
    print(f'Total calories for {date}: {total}')
```

## 问题 4
写一个 `new_user`，根据用户名创建一个新用户目录并创建一个空的 `weight.txt`：

```python
import os

def new_user(name):
    if not os.path.exists(name):
        os.mkdir(name)
        open(os.path.join(name, 'weight.txt'), 'w').close()
```

使用这种标准格式的优势在于可以用 Python 的 CSV 库替换自己的表格处理函数。此外，我们还可以使用程序创建 CSV 文件将数据导出到其他程序，例如电子。以下是我们的 csv 文件导入到 Microsoft Excel 的示例：

| A1 | | fx Food |
|---|---|---|
| A | B | C |
| 1 Food | Weight | Calories |
| 2 Carrots, Cooked | 100 | 109 |
| 3 Carrots, Raw | 100 | 111 |
| 4 Peas | | 350 |

我们如何将 `cal.py` 程序转换为新的 `csvcal.py` 程序呢？首先，我们导入 `csv` 模块并修改 `table_of_file` 函数：

```python
import csv
def table_of_file(filename):
    with open(filename) as c:
        r = csv.reader(c) # 读取 CSV 数据
        next(r) # 跳过列名行
        table = {}
        for row in r:
            table[row[0]] = row[1:] # 加载行的键和值
    return table
```

现在，修改我们的其他函数将文件名改为 `.csv` 很容易。因为我们修改了 `table_of_file` 函数，我们所有的表格读取和处理函数都能正常工作：

```python
def list_eaten(name, date):
    for k, v in table_of_file(os.path.join(name, date) + '.csv').items():
        print(f'{k} {v}')
```

我们需要进行更重大更改的地方位于创建的新函数中。我们将添加列标题：

我们必须在食物名称周围加上引号，并且如果文件不存在，则使用 `os.path.exists` 函数（该函数检查文件或目录已存在）添加 CSV 表头：

```python
def eaten(name, grams):
    filename = os.path.join(name, date_today()) + '.csv'
    is_new = not os.path.exists(filename)
    with open(filename, 'a') as f:
        if is_new: print('Food, Weight', file=f)
        print(f'{food},{grams}', file=f)
```

```python
def weighted(name, weight):
    filename = os.path.join(name, weight.csv')
    is_new = not os.path.exists(filename)
    with open(filename, 'a') as f:
        if is_new: print('Date, Weight', file=f)
        print(f'{date_today()},{weight}', file=f)
```

修改完成。

## 问题 6
完成从 `cal.py` 程序到 `csvcals.py` 的转换，并对其进行测试。

## 问题 7
在网上查找 Python CSV 模块文档，并使用它修改我们的 `csvals.py` 程序，使用该模块提供的函数来写入文件以及读取文件。

# 项目 3：井棋（Noughts and Crosses）

井棋这种儿童游戏是一个规模很大但可控的组合问题。让我们回顾一下规则，看看我们是否可以构建游戏树（即描述所有可能游戏的结构），并从中得出一些统计数据。

构建一个 3x3 的网格。两个玩家（O 和 X）轮替在空位上放置棋子。如果玩家在行、列或对角线上形成三个连续棋子，则获胜。如果棋盘满了且没有形成这种模式，则为平局。例如，在这个棋盘上，玩家 O 赢了，形成了一个对角线：

| X | O |
|---|---|
| O | X |
| O | X | O |

## 问题 1
1x1 和 2x2 的井棋游戏没有意义。为什么？

## 问题 2
根据你的经验，你能写下一些规则帮助玩家在 3x3 井游戏中胜利（或避免失败）吗？

## 表示棋盘

给棋盘上的每个位置分配一个数字：

| 0 | 1 | 2 |
| 3 | 4 | 5 |
| 6 | 7 | 8 |

棋盘可以表示为简单的字符串列表，对应 0..8 的每个位置。在空棋盘中，所有位置都是 `_`。

```python
emptyboard = ['_', '_', '_', '_', '_', '_']
```

你可能会奇怪我们为什么不使用长度为三的列表表示行，因为我们需要经常处理列和对角线。我们可以打印棋盘：

```python
print_board(b):
    for n, x in enumerate(b):
        print(x, end='')
        if n % 3 == 0: print('')
```

我们需要一些简单的函数来确定棋盘的属性。测试棋盘是否满（即平局）很容易：

```python
full(b):
    return '_' not in b
```

计算某个玩家是否胜利要困难得多，因为我们需要检查每一行、每一列和对角线。我们可以列出这些：

- `h1 = [0, 1, 2]` 行
- `h2 = [3, 4, 5]` 行
- `h3 = [6, 7, 8]` 行
- `v1 = [0, 3, 6]` 列
- `v2 = [1, 4, 7]` 列
- `v3 = [2, 5, 8]` 列
- `d1 = [0, 4, 8]` 对角线
- `d2 = [2, 4, 6]` 对角线

```python
lines = [h1, h2, h3, v1, v2, v3, d1, d2]
```

现在我们可以查找棋盘中每一行的位置，并将其与胜利行进行比较：

```python
def wins(p, b):
    win = [p, p, p]
    for l in lines:
        bl = [b[x] for x in l]
        if bl == win: return True
    return False
```

## 问题 3
写一个 `random` 函数，随机在空白处放置棋子。现在写一个 `random_game` 函数，使用它来玩任意合法的游戏。游戏在胜利、平局或棋盘未满时结束。在进行过程中打印棋盘。

## 人类玩家

人类玩家玩 'o'。`human_move` 要求用户选择下一个 'o' 的位置，确保用户的输入是合理的。然后它填充棋盘上的位置。

```python
>>> b = ['_', 'x', '_', '_', '_', '_', '_']
>>> human_move(b)
Position 0..8
不是有效的棋盘位置
Position 0..8
棋盘位置必须是 0..8
Position 0..8
>>> b
['_', 'x', '_', '_', 'o', '_', '_']
```

## 问题 4
写出符合此描述的 `human_move` 函数。可以使用内置方法 `isdigit` 来检查字符串是否为数字。

## 问题 5
扩展函数以玩 'x' 或 'o'。现在写一个允许两个人类对游戏的程序。在开始时打印空棋盘。

## 计算机玩家

人类玩家玩 'o'。`human_move` 要求用户选择下一个 'o' 的位置，确保用户的输入是合理的。然后它填充棋盘上的位置。

在问题 3 中，我们写了一个非常随机的玩家。面对这种玩家，人类在任何 3x3 井游戏中几乎都能胜利（或强制平局）。我们可以将计算机策略想象为“策略”列表。每个策略都会评估自己是否可以应用。如果没有，它将返回 `False`；否则，它将放置棋子并返回 `True`。

让我们实现可用时为 'x' 选择中心正格的策略。首先，我们写一个函数从列表中尝试获取第一个空格：

```python
def try_to_take(b, ps):
  for p in ps:
    if b[p] == '_':
      b[p] = 'X'
      return True
return False
```

那么，策略就是简单的：

```python
def tactic_centre(b):
  return try_to_take(b, [4])
```

事实上，“胜利”和“阻止”策略是相似的——如果一行中有一个空格且有两个我们的棋子，我们可以胜利。如果有一个空格且有两个对手的棋子，我们必须阻止。所以我们可以写一个检查这种这种情况的单一函数：

```python
def win_or_block(b, piece):
  for l in lines:
    bl = [b[x] for x in l]
    if bl.count('_') == 1 and bl.count(piece) == 2:
      for x in l:
        if b[x] == '_': b[x] = 'X'
      return True
return False
```

胜利和阻止策略是简单的：

```python
def tactic_win(b):
  return win_or_block(b, 'X')

def tactic_block(b):
  return win_or_block(b, 'O')
```

```python
def tactic_first_blank(b):
  return try_to_take(b, [0, 1, 2, 3, 4, 5, 6, 7, 8])
```

现在我们可以将这些策略组合起来，构建我们的 `computer_move` 函数：

```python
def computer_move(b):
    print('Computer has played:')
    if tactic_win(b):
        print('Used tactic_win')
        return
    if tactic_block(b):
        print('Used tactic_block')
        return
    if tactic_play_centre(b):
        print('Used tactic_centre')
        return
    if tactic_first_blank(b):
        print('Used tactic_first_blank')
        return
    print('No tactic applied: error in tactic implementations')
```

注意，这里的 `return` 结构被用于提前结束函数，而不是返回一个值。

事实上，有一种万无一失的获胜或强制平局策略。正如我们所建议的，它由一系列按顺序应用的规则组成，采用第一个有效的规则即可。以下描述来自 Ken Crowley 和 Robert S. Sieg 的《Flexible Strategy Use in Young Children's Tic-Tac-Toe》。

## 显式性能模型

| 战术 | 规则 |
| :--- | :--- |
| 获胜 | 如果某行、列或对角线上有两个我的棋子和一个空格，则占据该空格（赢得游戏）。 |
| 阻止 | 如果某行、列或对角线上有两个对手的棋子和一个空格，则占据该空格（阻止对手潜在的获胜）。 |
| 分叉 | 如果存在相互相交的行、列或对角线，且它们各有一个我的棋子和两个空格，则移动到交点处（从而在下回合创造出两种获胜方式）。 |
| 阻止分叉 | 如果存在相互相交的行、列或对角线，且它们各有一个对手棋子和两个空格，如果交点是空的，那么如果存在一个能为我制造“连三”的空位置（会让对手倾向于阻止而非分叉），否则移动到交点处（占据对手可能用于分叉的位置）。 |
| 占据中心 | 如果有中心，则占据中心。 |
| 占据对角 | 如果对手在角上，且对应的对角线是空的，则占据该对角线。 |
| 空白角落 | 如果有空的角落，则移动到空的角落。 |
| 空白侧边 | 如果有空的侧边，则移动到空的侧边。 |

你可以看到，“获胜”、“阻止”和“中心”规则是我们已经实现的规则。

## 问题 6
添加“空白角落”和“空白侧边”规则，允许我们移除“第一个空白”规则。添加“对角”规则。

## 问题 7
使用你的新玩家制作一个人机大战游戏。允许任何一方先走，并确保打印棋盘的中间状态和最终状态。

## 问题 8
实现剩下的两个战术，“分叉”和“阻止分叉”，它们更复杂一些。

## 所有可能的游戏

有多少种可能不同的井字棋（Noughts and Crosses）游戏？先手的胜率是多少，后手的胜率是多少，平局的概率又有多大？为了回答这些以及更多问题，我们将构建所谓的“游戏树”。它之所以被称为树，因为它具有分支结构。

让我们考虑当 X 开始时，游戏树的形状。显然，在顶层，它会分支九次，因为起始玩家 X 可以放置在任何方格中。然后是八种方式、七种方式，依此类推。一旦我们到达第五层级，有些游戏已经结束（因为玩家 X 的三个棋子可能组成一条线），因此分支数量可能会减少。树必须在九层后结束，因为即使没有人获胜，棋盘至少也是满的。这是游戏树的一个片段：

![](img/496c1aa28bc754c78c9a97aa8e66e6ea_104_0.png)

我们如何表示并构建这棵树？我们需要在每一层切换玩家以模拟回合，因此我们为此写了一个简单的函数：

```python
def swap_player(p):
    if p == 'X': return 'O'
    else: return 'X'
```

我们的树结构是一个元组 `(b, bs)`，其中 b 是当前棋盘，bs 是一个代表移动后后继树的列表。

构建这棵树的函数是递归的，就像数据结构一样。它首先检查当前棋盘是否获胜或平局，如果是这种情况，就没有后继棋盘。否则，我们为每种可能的移动产生一个子树，即棋盘上每个可能的空白方格。我们返回棋盘和后继树列表（通过递归产生），每次切换玩家。
