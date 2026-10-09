
`drawBoard(mainBoard, revealedBoxes)`

`pygame.display.update()`

`pygame.time.wait(1000)`

# 重新开始

`startGame(mainBoard)`

`firstSelection = None` # 重置 firstSelection

## 将游戏状态绘制到屏幕

| 120. | # 重绘屏幕并等待时钟刻度。 |
| 121. | `pygame.display.update()` |
| 122. | `FPSCLOCK.tick(FPS)` |

在此时，游戏状态已经根据玩家的输入进行了更新，并且最新的游戏状态位于游戏循环的最后，因此我们调用 `pygame.display.update()`。

第 9 行将 `FPS` 设置为整数 30，这意味着我们希望游戏每秒最多运行 30 帧。如果我们想让程序运行得慢一点，可以减小这个数字。它甚至可以设置为浮点数值 0.5，这将使程序每秒运行半帧，即每两秒一帧。

为了以每秒 30 帧的速度运行，每帧必须在 1/30 秒内绘制。这意味着 `pygame.display.update()` 和游戏循环中的所有代码必须在 33.3 毫秒内执行。任何现代计算机都可以轻松做到这一点并留有剩余时间。为了防止程序运行过快，我们调用 `FPSCLOCK` 中 `pygame.Clock` 对象的 `tick()` 方法，让它暂停剩余的 33.3 毫秒。

由于这是在游戏循环的最后，它确保了游戏循环的每次迭代至少持续 33.3 毫秒。如果由于某种原因 `pygame.display.update()` 调用和游戏循环中的代码超过了 33.3 毫秒，那么 `tick()` 方法将不会进行等待并直接返回。

我一直在说其他函数将在本章稍后进行解释。现在我们已经过过了 `main()` 函数，你已经对程序的通用工作方式有了大致的了解，让我们进入从 `main()` 调用所有其他函数的详细细节。

## 创建“揭示框”数据结构

```python
125 def generateRevealedBoxes(val):
126     revealedBoxes = []
127     for i in range(BOARDWIDTH):
128         revealedBoxes.append([val] * BOARDHEIGHT)
129     return revealedBoxes
```

`generateRevealedBoxes()` 函数需要创建一个包含布尔值的列表的列表。这个布尔值将作为参数 `val` 传递给函数。我们从 `revealedBoxes` 变量中的一个条目开始初始化该数据结构。

为了让数据结构具有 `revealedBoxes[x][y]` 的结构，我们需要让内部列表代表棋格的值，而不是水平行。否则，数据结构将具有 `revealedBoxes[y][x]` 的结构。

`for` 循环将创建列，并将它们追加到 `revealedBoxes` 中。列是使用列表复制创建的，因此列列表拥有的由 `BOARDHEIGHT` 决定的数量。

## 创建棋盘数据结构：步骤 1 – 获取所有可能的图标

```python
132 def getRandomizedBoard():
133     # 获取每种颜色所有可能的形状列表
134     icons = []
135     for color in ALLCOLORS:
136         for shape in ALLSHAPES:
137             icons.append((shape, color ))
```

棋盘数据结构只是一个包含元组的列表的列表，其中每个元组包含两个值：一个用于图标的形状，另一个用于图标的颜色。创建这个数据结构有点复杂。我们需要确保图标的数量与棋盘上的棋格数量完全一致，并确保每种类型的图标恰好两个。

执行此操作的第一步是创建一个包含形状和颜色所有可能组合的列表。记得我们在 `ALLCOLORS` 和 `ALLSHAPES` 中都有每种颜色和形状的列表，因此第 135 行和 136 行的嵌套 `for` 循环将遍历每种颜色下所有可能的形状。这些被添加到第 137 行的 `icons` 变量列表中。

向作者提问邮箱：`al@inventwithpython.com`

### 步骤 2 – 打乱并截断所有图标列表

| 行号 | 代码 |
| :--- | :--- |
| 139. | `random.shuffle(icons)` # 随机图标列表的顺序 |
| 140. | `numIconsUsed = int(BOARDWIDTH / 2)` # 计算需要多少图标 |
| 141. | `icons = icons[:numIconsUsed] * 2` # 使每种变为两个 |
| 142. | `random.shuffle(icons)` |

但请记住，可能的组合可能比棋盘上的空间多。我们需要通过将 `BOARDWIDTH` 乘以 `BOARDHEIGHT` 来计算棋盘上的空间数量。然后除以 2，因为我们将有成对的图标。在一个有 70 个空格的棋盘上，我们只需要 35 个图标，因为每个图标都会有两个。这个数字将存储在 `numIconsUsed` 中。

第 141 行使用列表切片来获取列表中前 `numIconsUsed` 个图标。（如果你忘记了列表切片如何工作，请查看 http://imgur/slicing。）此列表在第 139 行已被打乱，所以每次获取的图标都不相同。然后使用 `*` 运算符复制新列表，以便每个每种图标都有两个。新的双倍化列表将覆盖 `icons` 变量中的旧列表。由于此新列表的前部分与后半部分相同，我们调用 `shuffle()` 方法来随机混合。

### 步骤 3 – 将图标放入棋盘

| 行号 | 代码 |
| :--- | :--- |
| 144. | # 随机将图标放入列表 |
| 145. | `board = []` |
| 146. | `for x in range(BOARDWIDTH):` |
| 147. | `column = []` |
| 148. | `for y in range(BOARDHEIGHT):` |
| 149. | `column.append(icons.pop())` |
| 150. | # 创建棋盘 |
| 151. | `board.append(column)` |
| 152. | `return board` |

我们需要为棋盘创建一个列表的列表。现在我们像 `generateRevealedBoxes` 那样通过嵌套循环来完成。在第 149 行，`icons.pop()` 从列表中弹出图标。在第 151 行，将 `column` 添加到 `board`。

62 http://inventwithpython.com/pygame

![](img/9b1932f39c4ca4cfcc81c02125104271_79_0.png)

`leftTopCoordsOfBox` 函数将接收方框坐标并返回像素坐标。由于一个框在屏幕上占据多个像素，我们将始终返回该框左上角的单个像素点。该值将作为一个包含两个整数的元组返回。当我们需要为绘制这些框提供像素坐标时，经常会用到 `leftTopCoordsOfBox()` 函数。

## 从像素坐标转换为方框坐标

```
171. def getBoxAtPixel(x, y):
172.     for box in range(BOARDWIDTH):
173.         for box in range(BOARDHEIGHT):
174.             left, top = leftTopCoordsOfBox(boxx, boxy)
175.             boxRect = pygame.Rect(left, top, BOXSIZE, BOXSIZE)
176.             if boxRect.collidepoint(x, y):
177.                 return (boxx, boxy)
178.     return (None, None)
```

我们需要一个从像素坐标转换为方框坐标的函数（这样我们就能知道鼠标点击和移动事件发生在哪个方框上）。`Rect` 对象有一个 `collidepoint()` 方法，你可以向其传递 X 和 Y 坐标，如果坐标在 `Rect` 对象的区域内部（即与 `Rect` 区域碰撞），它将返回 `True`。

向作者提问邮箱：`al@inventwithpython.com`

## 第3章 – 记忆谜题 63

为了找到鼠标坐标位于哪个框上方，我们将遍历每个框的坐标，并在带有这些坐标的 `Rect` 对象上调用 `collidepoint()` 方法。当 `collidepoint()` 返回 `True` 时，我们就找到了被点击或移动过的框，并返回其坐标。如果没有一个一个返回 `True`，则 `getBoxAtPixel()` 将返回值 `(None, None)`。之所以返回这个元组而不是返回 `None`，是因为 `getBoxAtPixel()` 的调用者期望返回一个包含两个值的元组。

## 绘制图标与语法糖

```
181. def drawIcon(shape, color, box, body):
182.     quarter = int(BOXSIZE * 0.25) # 语法糖
183.     half = int(BOXSIZE * 0.5) # 语法糖
184.
185.     left, top = leftTopCoordsOfBox(box, body) # 从
         board 坐标获取像素坐标
```

`drawIcon()` 函数将在 `box` 和 `body` 参数给出的坐标处绘制一个指定形状和颜色的图标。每个形状都有一套不同的 Pygame 绘制函数调用，因此我们必须使用大量的 `if elif` 语句来区分它们。（这些语句位于第 187 到 198 行。）

框的左边缘和顶边缘的 X 和 Y 坐标可以通过调用 `leftTopCoordsOfBox` 函数获得。框的宽度和高度都设置在 `BOXSIZE` 常量中。然而，许多绘制函数调用使用了框尺寸的中点和四分之一点。我们可以计算这些值并将其存储在变量 `quarter` 和 `half` 中。我们本很容易地在代码中写 `int(BOXSIZE * 0.25)` 而不是使用变量 `quarter`，但这样做会让代码变得更易读，因为 `quarter` 的含义比 `int(BOXSIZE * 0.25)` 更直观。

此类变量是**语法糖**的例子。语法糖是指我们添加了本可以写的代码（可能使用更少的代码和变量），但它让源代码更易于阅读。常量变量是语法糖的一种形式。计算一个值并将其存储在变量中是另一种类型的语法糖。（例如，在 `getRandomizedBoard()` 函数中，我们可以很容易地将第 140 行和第 141 行的代码合并为一行。但分成两行写会更易读。）我们不需要额外的 `quarter` 和 `half` 变量，但拥有它们会让代码更易读。易读的代码在未来更容易进行调试和升级。

```
186. # 绘制形状
187.     if shape == DONUT:
```

64 http://inventwithpython.com/pygame

```
188.   pygame.draw.circle(DISPLAYSURF, color, (left + half, top + half),
189.   pygame.draw.circle(DISPLAYSURF, BGCOLOR, (left + half, top +
half), quarter - 5)
190.   elif elf_shape == SQUARE:
191.     pygame.draw.rect(DISPLAYSURF, color, (left + quarter, top +
quarter, BOXSIZE - half))
192.   elif elf_shape == DIAMOND:
193.     pygame.draw.polygon(DISPLAYSURF, color, ((left + half, top), left
BOXSIZE - 1, top + half), (left + half, top + BOXSIZE - 1), (left, top +
half))
194.   elif elf_shape == LINES:
195.     for i in range(0, BOXSIZE, 4):
196.       pygame.draw.line(DISPLAYSURF, color, (left, top + i), (left +
i, top))
197.       pygame.draw.line(DISPLAYSURF, color, (left, top + i), (left +
i, top))
198.   elif elf_shape == OVAL:
199.     pygame.draw.ellipse(DISPLAYSURF, color, (left + quarter, top + half))
```

`drawIcon()` 函数将在 `box` 和 `body` 参数给出的坐标处绘制一个指定形状和颜色的图标。每个形状都有一套不同的 Pygame 绘制函数调用，因此我们必须使用大量的 `if elif` 语句来区分它们。（这些语句位于第 187 到 198 行。）

框的左边缘和顶边缘的 X 和 Y 坐标可以通过调用 `leftTopCoordsOfBox` 函数获得。框的宽度和高度都设置在 `BOXSIZE` 常量中。然而，许多绘制函数调用使用了框尺寸的中点和四分之一点。我们可以计算这些值并将其存储在变量 `quarter` 和 `half` 中。

```
202. def getShapeAndColor(board, boxx):
203.   # x 值存储在
204.   # y 值存储在
205.   return shape, color
```

`getShapeAndColor` 函数返回框的形状和颜色。你可能会奇怪为什么我们使用常量变量：这提高了代码的可读性。

## 绘制框罩

```
208. def drawCovers(board, boxes, coverage):
209.   # 绘制被覆盖的框。
210.   for box in boxes:
211.     left, top = leftTopCoordsOfBox(box[0], box[1])
212.     pygame.draw.rect(DISPLAYSURF, BCOLOR, left, top)
213.     shape, color = getShapeAndColor(board, box)
214.     drawIcon(shape, color, box, box[1])
215.     if coverage > 0: # 只有在有覆盖时才绘制
216.         pygame.draw.rect(DISPLAYSURF, BOXCOLOR, left, top, coverage)
217.     pygame.display.update()
```

`drawCovers` 有三个参数：板数据结构、需要覆盖的每个框的 (X, Y) 元组列表，以及覆盖量。对 `boxes` 列表中的每个框使用相同的绘制方法。对于循环，代码应该执行三件事：绘制背景颜色（覆盖掉原本的内容）、绘制图标，然后是所需的图标覆盖层。`leftTopCoordsOfBox` 函数将返回框左上角的像素坐标。

当 `coverage` 参数为 0 时，完全没有覆盖。当 `coverage` 设置为 20 时，有一个 20 像素宽的白色框覆盖图标。我们希望将覆盖量设置为 `BOXSIZE` 的值，这样整个图标将被完全覆盖。

`drawCovers` 将从与游戏循环独立的循环中调用。由于由于，它需要单独调用 `pygame.display.update()` 和 `FPSCLOCK.tick(FPS)` 来显示动画。这意味着在这个循环期间，没有代码在运行以处理生成的任何动画。不过，覆盖和显示动画只需要运行一秒钟。

## 处理显示与覆盖动画

```
222. def revealBoxesAnimation(board, boxesToReveal):
223.     # 执行“显示”动画。
224.     for coverage in range(BOXSIZE, (-REVEALSPEED) - 1, REVEALSPEED):
225.         drawCovers(board, boxesToReveal, coverage)
226.
227.
228. def coverBoxesAnimation(board, boxesToCover):
229.     # 执行“覆盖”动画。
```

```
230. for coverage in range(0, BOXSIZE + REVEALSPEED, REVEALSPEED):
231.     drawBoxesCovers(board, boxesToCover, coverage)
```
