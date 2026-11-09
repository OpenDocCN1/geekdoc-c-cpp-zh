
### 22 保持稳定

如果气球碰到屏幕顶部或底部，你的游戏就需要结束。将以下代码输入到第21步的代码行下方。

```python
if balloon.top < 0 or balloon.bottom > 560:
    game_over = True
    update_high_scores()
```

这一行检查气球是否碰到了屏幕顶部或底部。

### 23 处理与障碍物的碰撞

最后，你需要添加一些代码，以便气球撞到三个障碍物中的任何一个时结束游戏。添加下面的代码。

```python
update_high_scores()

if balloon.collidepoint(bird.x, bird.y) or \
   balloon.collidepoint(house.x, house.y) or \
   balloon.collidepoint(tree.x, tree.y):
    game_over = True
    update_high_scores()
```

这项检查用于判断气球是否撞到了三个障碍物中的任何一个。

如果需要将一行长代码分成多行，请使用反斜杠字符。

这会将 `game_over` 设置为 `True`，从而告诉程序游戏结束了。

如有必要，这会更新高分。

### 24 测试你的代码

保存程序并从命令行运行它。现在你应该能够玩这个游戏了，但它还没有完全完成！接下来你将了解如何向游戏中添加高分。

![](img/3188b147f991a51de14dcd2bb4b4c42e_130_0.png)

现在所有障碍物看起来都会在屏幕上移动。

## 专家提示

### 记录分数

假设当前的高分是 12、10、8，而一名玩家得了 11 分。如果你的代码只是把每个被超越的分数替换成新分数，你最终会得到 12、11、11，这就不对了。为了避免这种情况，你的代码需要先将玩家的分数与最高分比较。11 小于 12，因此不会替换它。然后它需要继续比较第二高的分数。下一个分数 11 大于 10，因此替换它。现在 11 已经进入排行榜，代码需要检查刚刚被替换的分数是否大于当前第三名的分数。因为 10 大于 8，所以它替换了 8，而 8 被完全移除。

![](img/3188b147f991a51de14dcd2bb4b4c42e_132_0.png)

### 27 找出最高分

现在编写一些代码，检查当前分数是否超过了三个高分中的任何一个。将以下代码添加到第26步的代码行下方。

```python
high_scores = line.split()
for high_score in high_scores:
    if (score > int(high_score)):
        scores.append(str(score) + " ")
        score = int(high_score)
    else:
        scores.append(str(high_score) + " ")
```

这会遍历高分列表。

这会检查玩家的分数是否高于现有的高分。

这会将 score 设置为刚刚被超越的高分。

如果玩家没有超越所讨论的高分，那么当前的高分会被添加到列表中。

如果玩家的分数高于某个现有高分，这会将玩家分数添加到列表中。

### 28 将高分写入文件

使用 write() 将新的高分写入 high-scores.txt 文件。将以下代码添加到第27步的代码下方。

```python
scores.append(str(high_score) + " ")
with open(filename, "w") as file:
    for high_score in scores:
        file.write(high_score)
```

这个代码块会将新的高分写入 .txt 文件。

这会打开 high-scores.txt 文件以便写入。

## 专家提示

### 文件处理

在《气球飞行》中，你使用了 .txt 文件来存储高分。这样的文件可以被打开并赋值给一个变量。处理文件所需的主要函数是 open()、read() 和 write()。

![](img/3188b147f991a51de14dcd2bb4b4c42e_133_0.png)

- open() 接受两个参数：文件名和“模式”，模式告诉 Python 你想对文件做什么。Python 中有四种模式：r 表示读取，w 表示写入，a 表示追加到文件末尾，r+ 表示读取和写入。

```python
file = open("names.txt", "r")
```

文件名

模式

- 使用 read() 函数读取整个文件。

```python
names = file.read()
```

- 你也可以只读取一行，而不是整个文件。

```python
name = file.readline()
```

- 你甚至可以将所有行添加到一个列表中。

```python
lines = []
for line in file:
    lines.append(line)
```

- 现在使用 write() 函数写入文件。

```python
file = open("names.txt", "w")
file.write("Martin")
```

- 使用完文件后，你应该关闭它，以告诉程序你已经用完了。

```python
file.close()
```

- 如果使用完文件后忘记关闭，部分数据可能不会写入其中。使用 with 语句可以防止这种情况发生。该语句会打开文件，并在执行完 with 语句的主体后自动关闭它。

```python
with open("names.txt", "r") as file:
    name = file.readline()
```

函数主体。

![](img/3188b147f991a51de14dcd2bb4b4c42e_133_1.png)

### 29 显示高分

现在你已经编写了一个收集高分的函数，还需要编写一个在屏幕上显示高分的函数。将第9步中 def display_high_scores() 下方的单词 pass 替换为以下代码。

```python
def display_high_scores():
    screen.draw.text("HIGH SCORES", (350, 150), color="black")
    y = 175
    position = 1
    for high_score in scores:
        screen.draw.text(str(position) + ". " + high_score, (350, y), color="black")
        y += 25
        position += 1
```

这一行会在屏幕上写入 HIGH SCORES。

这一行会在屏幕上写入高分。

这会增加 y 坐标，使每个高分都显示在前一个高分下方 25 像素处。

这一行会在屏幕上显示高分。

## 技巧与调整

有很多方法可以改编这个游戏，使它更复杂。以下是一些你可以尝试的想法。

![](img/3188b147f991a51de14dcd2bb4b4c42e_134_0.png)

Pygame Zero 游戏

高分榜
1. 12
2. 9
3. 8
4. 6
5. 3

![](img/3188b147f991a51de14dcd2bb4b4c42e_134_1.png)

呼！我还剩两条命。

lives = 3

### 更多高分

目前游戏只存储前三名高分。你能把它改成存储前五名或前十名吗？还记得你在第3步创建的那个包含三个分数的文本文件吗？你怎样才能编辑这个文件来存储更多高分？

### 生命值

为什么不给玩家更多完成游戏的机会呢？引入一个新变量来跟踪玩家的生命值。每次玩家撞到障碍物时，将生命值减一。当没有剩余生命值时，游戏结束。

### 升级

通过添加关卡并让每一关速度更快，使游戏更有趣。为此，你可以将每关的障碍物数量设为十个。要完成关卡，玩家必须清除所有障碍物并获得十分。每当分数达到十的倍数时，就让障碍物移动得更快。在原始游戏中，鸟每次移动四个像素，房子和树每次移动两个像素。如果你想在每一关提高速度，就需要将速度存储在变量中。只要记住，鸟的移动速度应始终是树和房子的两倍。

```python
speed = 2
bird.x += speed * 2
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_136_0.png)

### 拉开障碍物间距

有时所有障碍物——树、房子和鸟——可能会出现在 x 轴上的同一位置。这样也能正常运行，但你可能想避免这种情况。尝试修改 update() 函数，使障碍物在发生冲突时选择新的随机 x 坐标。以下代码可以帮助你入门：

```python
if bird.x == house.x
```

## 专家提示

### 取模运算符

当 Python 执行除法时，它会忽略余数。但有时知道是否有余数以及余数是多少会很有用。例如，如果你想测试一个数是否为偶数，可以通过将它除以 2 并检查是否有余数来实现。为此，你可以使用取模运算符 %。

```python
>>> print(2 % 2)
0
```

> 结果为 0，因为 2 除以 2 没有余数。

```python
>>> print(3 % 2)
1
```

> 这是 3 除以 2 的余数。

在《气球飞行》中，你可以使用取模运算符来判断分数是否为 10 的倍数，从而判断玩家是否应该进入下一关。

```python
score % 10
```

> 这会返回分数除以 10 的余数。

![](img/3188b147f991a51de14dcd2bb4b4c42e_136_1.png)
