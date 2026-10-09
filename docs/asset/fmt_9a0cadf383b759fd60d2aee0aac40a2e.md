
`getSpotClicked()` 函数是 `getLeftTop()` 的相反操作，并将像素坐标转换为棋盘坐标。第 205 行和 206 行遍历每一个可能的棋盘坐标，如果传入的像素坐标在棋盘的该空间内，它将返回这些棋盘坐标。由于所有瓷块的宽度和高度都在 `TILESIZE` 中设置过，我们可以通过获取左上角的像素坐标来创建一个代表棋盘上空间的 `Rect`，然后使用 `collidepoint()` 方法查看像素坐标是否在该 `Rect` 区域内。

如果传入的像素坐标不在任何棋盘空间，则返回值 `(None, None)`。

## 绘制瓷块

```python
214. def drawTile(tile, number, adjx=0):
215.     # 在 tiley 处绘制瓷块，可选的
216.     # 棋盘坐标的 adjx
217.     left, top = getLeftTop(tile)
218.     pygame.draw.rect(DISPLAY, TEXTCOLOR, (left, top, TILESIZE, TILESIZE))
219.     textSurf = FONT.render(str(number), True)
220.     tileRect = textSurf.get_rect()
221.     tileRect.center = (left + TILESIZE / 2, top + TILESIZE / 2)
222.     DISPLAY.blit(textSurf)
```

`drawTile` 函数绘制字符串。`adjx` 和 `adjy` 参数是棋盘上的调整。第 219 到 222 行创建带有数字的 `Surface`。`drawTile` 绘制在棋盘上。这些值会在 `pygame.update()` 之后放置在棋盘上。

## 在屏幕上制作文本

```python
225. def makeText(text, color, bgcolor, top, left):
226.     # 创建文本的 Surface 和 Rect 对象
227.     textSurf = FONT.render(text, True, color)
228.     textRect = textSurf.get_rect()
229.     textRect.topleft = (top, left)
230.     return (textSurf, textRect)
```

向作者提问请邮箱：alf@inventwithpython.com

`makeText()` 函数处理在屏幕上创建 Surface 和 Rect 对象。与其每次想在屏幕上制作文本，我们只需调用 `makeText()` 即可。这节省了我们的工作量（尽管 `draw()` 调用了 `render()` 和 `get_rect()`）。

## 绘制棋盘

```python
233. def drawBoard(board, message):
234.     DISPLAY.fill(BGCOLOR)
235.     if message:
236.         textSurface, rectText = makeText(message, MESSAGECOLOR, BGCOLOR, 5)
237.         DISPLAY.blit(textSurface, rectText)
238. 
239.     for tilex in range(len(board)):
240.         for tiley in range(len(board[0])):
241.             if board[tilex][tiley]:
242.                 drawTile(tilex, tiley, board[tilex][tiley])
```

该函数将整个棋盘和所有的瓷块绘制到 Surface 对象上。第 234 行的 `fill()` 方法完全覆盖之前绘制在表面上的任何内容，因此我们从头开始。

## 绘制棋盘边界

```python
244. left, top = getTopLeft(0, 0)
245.     width = BOARDWIDTH * TILESIZE
246.     height = BOARDHEIGHT * TILESIZE
247.     pygame.draw.rect(DISPLAY, BORDERCOLOR, (left - 5, top - 5, width + 11, height + 11), 4)
```

第 244 到 247 行在棋盘周围绘制一个边界。边界的左上角位于棋盘坐标 `(0, 0)` 的左侧 5 像素和上方 5 像素处。边界的宽度和高度是根据瓷块数量计算的

100 http://inventwithpython.com/pygame

在 `BOARDWIDTH` 和 `BOARDHEIGHT` 常数乘以碎片的大小（存储在 `TILESIZE` 常数中）。

我们在第 247 行绘制的矩形厚度为 4 像素，因此我们将边界向左移动 5 像素，并位于 `top` 和 `left` 变量的位置，这样线条的厚度就不会覆盖碎片。我们还会增加宽度和长度（增加 5 像素是为了补偿矩形向左和向上的移动）。

## 绘制按钮

| 行号 | 代码 |
|||||
| 249. | DISPLAYSUR.blit(RESET_SURF, RESET_RECT) |
| 250. | DISPLAYSUR.blit(NEW_SURF, NEW_RECT) |
| 251. | DISPLAYSUR.blit(SOLVE_SURF, SOLVE_RECT) |

最后，我们在屏幕侧面绘制按钮。这些按钮的文本和位置永远不会改变，这就是为什么它们在 `main()` 函数开始时被存储在常量变量中的原因。

## 碎片滑动的动画

```
254. def slideAnimation(board, direction, message, animationSpeed):
255.     # 注意：此函数不检查移动是否有效。
256.
257.
blankx, blanky = getBlankPosition(board)
258. if direction == UP:
259.     movex = blankx
260.     movey = blanky + 1
261. elif direction == DOWN:
262.     movex = blankx
263.     movey = blanky - 1
264. elif direction == LEFT:
265.     movex = blankx + 1
266.     movey = blanky
267. elif direction == RIGHT:
268.     movex = blankx - 1
269.     movey = blanky
```

我们的滑动动画需要计算的第一是是空白在哪里以及移动的碎片在哪里。第 255 行提醒我们，调用 `slideAnimation()` 的代码应该确保 `slide` 参数是一个有效的移动。

向作者发送问题邮件：al@inventwithpython.com

# 第4章 – 拼智游戏

空白的坐标来自调用 `getBlankPosition()`。根据这些坐标和滑动的方向，我们可以算出将滑动的碎片 XY 坐标。这些坐标将存储在 `movex` 和 `movey` 中。

## copy 方法

```
271. # 准备基础表面
272. drawBoard(board, message)
273. baseSurf = DISPLAY.copy()
274. # 在 baseSurf 上移动的碎片上方绘制一个空白区域。
275. moveLeft, moveTop = getLeftOffset(movex, movey)
276. pygame.draw.rect(baseSurf, BGCOLOR, moveLeft, moveTop, TILESIZE, TILESIZE)
```

`Surface` 对象的 `copy()` 方法将返回一个具有相同绘制图像的新 Surface。但它们是两个分离的 Surface。在调用 `copy()` 方法后，如果我们使用 `blit()` 或 Pygame 函数在其中一个 Surface 上绘制，它不会改变另一个 Surface 图像。我们在第 273 行将此副本存储在 `baseSurf` 变量中。

接下来，我们在将滑动的碎片上方绘制另一个空白区域。这是因为当我们绘制滑动动画的每一帧时，我们会在 `baseSurf` 的不同部分绘制滑动。如果我们不在 `baseSurf` 上擦除移动的碎片，那么当我们绘制滑动碎片时，它仍然在那里。在这种情况下，`baseSurf` 看起来会这样：

![](img/9b192f39c4cfcc81c021504271_18_0.png)

然后当在其上方绘制向上滑动的碎片时，它看起来是这样的：

![](img/9b192f39c4cfcc81c021504271_19_0.png)

你可以通过注释掉第 276 行并运行程序来亲自验证这一点。

```
278. for i in range(0, TILESIZE, animationSpeed):
279.     # 动画碎片滑动
280.     checkForQuit()
281.     DSURF.blit(baseSurf, (0, 0))
282.     if direction == UP:
283.         drawTile(movex, move, board[movex], 0, -i)
284.     if direction == DOWN:
285.         drawTile(movex, move, board[movex], 0, i)
286.     if direction == LEFT:
287.         drawTile(movex, move, board[movex], -i, 0)
288.     if direction == RIGHT:
289.         drawTile(movex, move, board[movex], i, 0)
290.   pygame.display.update()
291.   CLOCK.tick(FPS)
```

为了绘制滑动动画的帧，我们必须在显示 Surface 上绘制 `baseSurf` 表面，然后在动画的每一帧中，绘制滑动碎片使其靠近其原始空白区域的最终位置。相邻碎片之间的距离与单个碎片的大小相同，我们将其存在 `TILESIZE` 中。代码使用 `for` 循环从 0 运行到 `TILESIZE`。

通常情况下，这意味着我们会绘制 0 像素偏移碎片，然后下一帧绘制 1 像素，然后是 2 像素、3 像素，依此类推。每一帧都将占据 1/30 秒。如果我们将 `TILESIZE` 设置为 80（如本书中的程序在第 12 行所示），那么滑动一个碎片将花费两半秒以上，这实际上有点慢。

因此，我们将让循环每帧跳过几个像素，从 0 迭代到 `TILESIZE`。它跳过的像素数存储在 `animationSpeed` 中，该值在调用 `slideAnimation()` 时传递。例如，如果 `animationSpeed` 设置为 8 且常量 `TILESIZE` 设置为 80，那么 `range(0, TILESIZE, animationSpeed)` 循环将 `i` 设置为值 0, 8, 16, 24, 32, 40, 48, 64, 72。它不包含 80，因为 `range()` 达到但不包含第二个参数。这整个滑动动画将在 10 帧内完成，游戏以 30 FPS 运行，耗时为 10/30 秒（即三分之一秒）。

第 282 行到 289 行确保我们按照正确的方向绘制滑动碎片（基于 `direction` 变量包含的值）。动画完成后，函数返回。

## 创建新拼智游戏

```
295. def generatePuzzle(numSlides):
296.   # 从开始
297.   board = drawBoard()
298.   sequence = []
299.   pygame.time.wait(500)
300.   lastMove = None
301.   for i in range(numSlides):
302.     move = getRandom(board)
303.     slideAnimation(board, move, 'Generating puzzle...')
304.     makeMove(board, move)
305.     sequence.append(move)
306.     lastMove = move
307. return board, sequence
```

`numSlides` 参数将告诉你要执行多少次移动。`generatePuzzle` 函数将在开始时调用。

## 棋板重置动画

```
313. def resetAnimation(board, allMoves):
314.     # 反向 allMoves 中的所有移动。
315.     revAllMoves = allMoves[:] # 获取列表副本
316.     revAllMoves.reverse()
317.
318.     for move in revAllMoves:
319.         if move == UP:
320.             oppositeMove = DOWN
321.         elif move == DOWN:
322.             oppositeMove = UP
323.         elif move == RIGHT:
324.             oppositeMove = LEFT
325.         elif move == LEFT:
326.             oppositeMove = RIGHT
327.         slideAnimation(board, oppositeMove, '', int(TILESIZE/2))
```

当玩家点击“重置”或“解决”时，拼智游戏需要撤销对棋板进行的所有移动。滑动的方向变量列表将作为 `allMoves` 参数传递。

# 第4章 – 滑块游戏 105

allMoves 列表。这创建了实际列表的副本并存储在 `revAllMoves` 中，而不仅仅是列表引用的副本。（详情请参见 http://invpy.com/references。）

若要撤销 `allMoves` 中的所有操作，我们需要执行 `allMoves` 中操作的反向操作，并按反序进行。有一个名为 `reverse()` 的列表方法，它可以反转列表项的顺序。我们在第 316 行调用了此 `revAllMoves` 列表。

第 318 行的 `for` 循环遍历了方向值。记住，我们需要的是相反的操作，因此第 319 行到 326 行的 `if` 和 `elif` 语句会在 `oppositeMove` 变量中设置正确的方向值。然后我们调用 `slideAnimation()` 执行动画，并调用 `makeMove()` 更新棋盘数据结构。

```
331. if __name__ == '__main__':
332. main()
```
