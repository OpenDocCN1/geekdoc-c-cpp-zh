

退出循环。）

所以现在，我们已经能打印玩家位置，也能让用户输入命令了。不过，我们还需要处理方向命令，并真正移动玩家。

我们计划根据当前位置和用户输入来计算玩家的新位置。例如，如果用户在屏幕上向北（上）移动，玩家的列保持不变，但行号减 1。

```python
# The map

map_data = [
    "################",
    "#.#...........#",
    "#.#...#...#...#",
    "#...........#",
    "#.#...#...#.#",
    "#...........#",
    "#.#...#...#.#",
    "################"
]

# Player position

player_row = 4
player_column = 9

quit = False

while not quit:
    # Print map and player indicator
    for row_index, row in enumerate(map_data):  # for each row
        for col_index, map_character in enumerate(row):  # for each col
            if row_index == player_row and col_index == player_column:
                print("@", end="")  # end="" no newline
            else:
                print(map_character, end="")
        print()
    # Get input
    command = input("Enter a move (n,s,w,e,q): ")
    # Figure out the new row and column of the player
    # Make sure input is valid
    if command == "n":
        new_row = player_row - 1
        new_column = player_column
    elif command == "s":
        new_row = player_row + 1
        new_column = player_column
    elif command == "w":
        new_row = player_row
        new_column = player_column - 1
    elif command == "e":
        new_row = player_row
        new_column = player_column + 1
    elif command == "q":
        quit = True
        continue  # jump right back to the top of the while
    else:
        print(f'Unknown command {command}')

    # Set the current position to the new position
    player_row = new_row
    player_column = new_column
```

这样已经很好了，但我们仍然可以穿墙而过。让我们修改程序的最后几行，在把玩家移动过去之前，先验证新位置是一个空房间。（注意行号！）

```python
if map_data[new_row][new_column] != ".":
    print("You can't move that way!")
else:
    # Set the current position to the new position
    player_row = new_row
    player_column = new_column
```

哇！你已经写出了属于你自己的 Roguelike¹⁰ 游戏！

问题解决步骤：回顾。

对于接下来的步骤，可以考虑添加以下内容：

- 宝藏
- 怪物
- 属性
- 武器
- 任何你想要的东西！这是你的游戏！

只需回到“理解问题”这一步，然后实现其中的一些功能。

另外，如果在打印地图之前清屏，游戏看起来会更整洁，但遗憾的是，目前还没有一种简单的跨平台方式来实现这一点¹¹。不过，有一个取巧的办法。

如果你的终端支持 ANSI 转义序列¹²（很可能支持），我们可以向它发送特殊的字符序列来清屏，然后将光标归位（移到左上角）。

神奇的咒语如下：

```python
print("\x1b[2J\x1b[H", end="")  # Clear the screen
```

把它放到你开始打印地图的代码上方，你就会看到效果。如果你的终端不支持 ANSI 序列，你只会看到一些奇怪的字符。真糟糕¹³。

如果你真的想深入研究字符图形，有一个库值得一试：curses¹⁴。它可以让你清屏、定位光标、获取输入而无需将其回显到屏幕或等待回车、输出彩色内容等等。

虽然我们已经有足够的知识来添加怪物、宝藏等内容，但等到后续章节学习了字典和对象之后再做会更容易。我们手头有更多工具可用！

（解答¹⁵。）

- ¹⁰ https://en.wikipedia.org/wiki/Roguelike
- ¹¹ 嗯，至少在我们目前的学习阶段还不行。
- ¹² https://en.wikipedia.org/wiki/ANSI_escape_code
- ¹³ https://www.youtube.com/watch?v=q3f6xTugN7g
- ¹⁴ https://docs.python.org/3/howto/curses.html
- ¹⁵ https://beej.us/guide/bgpython/source/examples/adv1.py

### 8.15 练习

记住：要想从这本书中获得价值，你必须做这些练习。在一个问题上卡了 20 分钟之后，你才允许看解答。

解决这些问题时，可以使用你拥有的任何知识，而不仅仅是本章所学的内容。

始终使用解决问题的四个步骤来解决这些问题：理解问题、制定计划、执行计划，并回顾反思，看看自己哪里可以做得更好。

1. 下面的代码会打印出 99：

   ```python
   a = [1, 2, 3]
   b = a

   b[0] = 99

   print(a[0])
   ```

   如何只修改第 2 行，使 `b` 成为 `a` 的副本，从而让程序打印出 1 呢？（解答 16。）

2. 编写一个循环，打印出以下列表的总和：

   ```python
   [14, 31, 44, 46, 54, 59, 45, 55, 21, 11, 8, 34, 66, 41]
   ```

   总和是 529。

   （解答 17。）

3. 给定以下列表：

   ```python
   [11, 22, 33]
   ```

   编写一行 Python 代码，将列表改为：

   ```python
   [11, 22, 33, 99]
   ```

   然后编写另一行代码，将该列表改为：

   ```python
   [11, 33, 99]
   ```

   最后，再编写一行代码，将该列表改为：

   ```python
   [11, 33, 88, 99]
   ```

   这个练习应该操作同一个列表，而不是创建新列表。

   （解答 18。）

4. 用不超过 20 个字符的 Python 代码创建以下列表：

   ```python
   [1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3]
   ```

   （解答 19。）

5. 使用列表推导式，从下面的列表中筛出所有 5 的倍数，构成一个新列表：

   ```python
   [14, 31, 44, 46, 54, 59, 45, 55, 21, 11, 8, 34, 66, 41]
   ```

   （解答 20。）

6. 使用列表推导式，从下面的列表中生成一个新列表，其中只包含以辅音开头的单词的全大写版本。

   ```python
   ["alice", "beeJ", "chris", "dave", "eve", "frank"]
   ```

   示例输出：

   ```python
   ['BEEJ', 'CHRIS', 'DAVE', 'FRANK']
   ```

   （解答 21。）

7. 编写一个程序，生成一个列表的列表（二维列表），其中包含一张最大到 12 × 12 的乘法表。

   你应该能够像这样打印出 7 × 5 的结果：

   ```python
   print(multable[7][5])  # prints 35
   ```

   （解答 22。）

### 8.16 小结

看看本章我们涉及了多少内容！

- 一种全新的数据结构，用于保存信息列表
- 理解可变类型的赋值
- 如何访问和修改列表中的元素
- 如何修改和复制列表
- 如何创建包含重复值的新列表
- 列表推导式！哇！
- 列表的列表！

列表是我们武器库中一件强大的工具。随着我们的程序越来越复杂，我们会大量使用它们。

## 第 9 章

## 字典

### 9.1 目标

- 理解什么是字典
- 初始化字典
- 访问字典中的单个元素
- 检查字典中是否存在某个键
- 使用 for 遍历字典
- 使用常见的字典内置函数
- 使用字典推导式构造新字典
- 构建字典的字典
- 理解字典是可变的

### 9.2 章节项目规格

让我们来存储一些家谱¹数据！

我们将会为每个人关联多条数据记录：

```
Bee Jorgensen:
Born: 1993 [yes, I'm 29, is my story I'm sticking to]
Mother: Mom Jorgensen
Father: Dad Jorgensen
Siblings: [Brother Jorgensen, Sister Jorgensen, Little Sister Jorgensen]

Mom Jorgensen:
Born: 1970
Mother: Grandma Jorgensen
Father: Grandpa Jorgensen
Siblings: [Auntie Jorgensen]

Dad Jorgensen:
Born: 1965
Mother: Granny Jorgensen
Father: Grandad Jorgensen
Siblings: [Uncle Jorgensen]
```

（好吧，我听到你在说：“等等，你妈妈和你爸爸都姓 Jorgensen？这很可疑。我不是在暗示什么，只是随口一说。” 住口！我可以向你保证他们没有血缘关系²。）

- ¹ 这完全是在讲家族树。你知道吗，我和伊丽莎白二世女王有亲戚关系（通过联姻）？我是她母亲的妹妹的丈夫的父亲的姐妹的女儿的丈夫的妻子的（戏剧性！）姐妹的丈夫的父亲的兄弟的儿子的儿子的女儿的儿子。实事求是地说：我敢打赌，你和伊丽莎白二世也有亲戚关系。那这样一来，我们就是表亲了！
- ² 除了通过伊丽莎白二世，就像我们其他人一样。

