
261.                 `adjY=i)`:
262.                 `break`
263.             `fallingPiece['y']` += `i - 1`

```
当玩家按下空格键时，落下方块将立即掉到棋板上尽可能远的地方落地。程序首先需要找到方块落地之前可以移动多少格。

第 256 到 258 行将所有变量设置为 `False`（这使得程序后续部分的代码知道用户已松开了任何按住的方向键）。这样做是因为这段代码会将方块移动到绝对并开始下一个方块，我们不希望玩家在按住方向键点击空格键时让方块立即开始。

为了找到方块可以掉落的最远距离，我们首先调用 `isValidPosition()` 并为 `adjY` 参数传递整数 1。如果 `isValidPosition()` 返回 `False`，我们知道方块无法进一步掉落，已经在底部。如果 `isValidPosition()` 返回 `True`，我们知道它可以掉落一个格。

在这种情况下，我们应该调用 `adjY` 设置为 2 的 `isValidPosition()`。如果再次返回 `True`，我们将调用 `adjY` 设置为 3 的 `isValidPosition()`，依此类推。这就是 259 行 `for` 循环处理的：通过递增的整数值调用 `isValidPosition()`，直到函数返回 `False`。此时，我们知道 `i` 的值比底部多了一个格。这就是为什么第 262 行将 `fallingPiece['y']` 增加了 `i-1`。

（注意 259 行 `for` 语句中 `range()` 的第二个参数设置为 `BOARDHEIGHT`，因为这是方块在撞底之前可能掉落的最大距离。）

## 按住按键移动

```
264.    # 根据用户输入移动块
265.    if (movingLeft or movingRight) and time.time() -
266.        lastMoveSidewaysTime > MoveewaysFREQ:
267.            if movingLeft and isValidPosition(board, fallingPiece, adjX=-1):
268.                fallingPiece['x'] -= 1
269.            elif movingRight and isValidPosition(board, fallingPiece, adjX=1):
270.                fallingPiece['x'] += 1
271.                lastMoveSidewaysTime = time.time()
```

180 http://inventwithpython.com/pygame

如果用户按住键的时间超过 0.15 秒（存储在 `MOIDESWAYSFREQ` 中的值为浮点数 0.15），那么表达式 `time.time() - lastMoveSidewaysTime > MOIDESWAYSFREQ` 的结果将为 True。如果用户同时按住了箭头键且已经过了 0.5 秒，并且在用户没有再次按下键的情况下将掉落的碎片向左或向右移动，第 265 行的条件即为 True。

这非常有用，因为玩家反复点击箭头键来让掉落碎片在棋板上移动多个位置会非常疲惫。相反，他们只需按住箭头键，碎片就会持续移动，直到他们松开按。当这种情况发生时，第 216 到 221 行的代码会将变量设置为 `False`，第 265 行的条件将变为 `False`。这就是停止碎片继续滑动的原因。

为了演示为什么 `time.time() - lastMoveSidewaysTime > MOIDESWAYSFREQ` 在经过 `MOIDESWAYSFREQ` 中的秒数后会返回 True，请运行这个短程序：

```python
import time

WAITTIME = 4

begin = time.time()

while True:
    now = time.time()
    message = '%s, %s, %s' % (begin, now, (now - begin))
    if now - begin > WAITTIME:
        print(message + ' PASSED WAIT TIME!')
    else:
        print(message + ' Not next...')
time.sleep(0.2)
```

该程序有一个无限循环，因此要终止它，请按 Ctrl-C。该程序的输出如下：

| 1322106392.2, 1322106392.2, 0.0 | 还没... |
| 1322106392.2, 1322106392.42, 0.219000101089 | 还没... |
| 1322106392.2, 1322106392.65, 0.449001201663 | 还没... |
| 1322106392.2, 1322106392.88, 0.689099994278 | 还没... |
| 1322106392.2, 1322106393.11, 0.910000085831 | 还没... |
| 1322106392.2, 1322106393.34, 1.1400001049 | 还没... |
| 1322106392.2, 1322106393.57, 1.3710000515 | 还没... |
| 1322106392.2, 1322106393.83, 1.6360001564 | 还没... |
| 1322106392.2, 1322106394.05, 1.8519999809 | 还没... |

向作者提问邮件：al@inventwithpython.com

# 第 7 章 - 俄罗斯块 181

```python
1322106392.2, 1322106394.28, 2.0800016212 还没...
1322106392.2, 1322106394.51, 2.3090001526 还没...
1322106392.2, 1322106394.74, 2.5410012779 还没...
1322106392.2, 1322106394.97, 2.7699998093 还没...
1322106392.2, 1322106395.22, 2.980001446 还没...
1322106392.2, 1322106395.45, 3.226999809 还没...
1322106392.2, 1322106395.65, 3.4560009865 还没...
1322106392.2, 1322106395.89, 3.6920005068 还没...
1322106392.2, 1322106396.12, 3.921000381 还没...
1322106392.2, 1322106396.36, 4.148999243 通过等待时间!
1322106392.2, 1322106396.59, 4.378999485 通过等待时间!
1322106392.2, 1322106396.81, 4.600701253 通过等待时间!
1322106392.2, 1322106397.04, 4.8370013161 通过等待时间!
1322106392.2, 1322106397.26, 5.0650005722 通过等待时间!
Traceback (most recent call last):File "timestest.py", line 13, in <module>
time.sleep(2)
KeyboardInterrupt
```

输出行的第一个数字是程序首次启动时 `time.time()` 的返回值（该值从未改变）。第二个数字是 `time.time()` 的最新返回值（该值每次迭代都会更新）。第三个是设置为开始时间的数字。这三个数字是自执行 `begin = time.time()` 代码以来的秒数。

如果这个数字大于 4，代码将开始打印“PASSED TIME!”而不是“Not yet...”。这就是我们判断某行代码运行后过了多久的方法。在俄罗斯块程序中，`time.time() - lastMoveSidewaysTime` 将计算自上次将 `MoveSidewaysTime` 设置为当前时间以来的秒数。如果此值大于 `MOIDESWAYSFREQ` 中的值，我们就知道该让掉落碎片移动移动。

不要忘记再次更新 `lastMoveSidewaysTime` 为当前时间！这是我们在第 270 行的操作。

```python
272. if movingDown and time.time() - lastMoveDown > MOVEDOWNFREQ \
    and isValidPosition(fallingPiece, adjY=1):
273.     fallingPiece['y'] += 1
274.     lastMoveDown = time.time()
```

182 http://inventwithpython.com

第 272 到 274 行的作用与 265 到 270 行相同，不同的是让掉落碎片向下移动。它有一个独立的变量（`movingDown`）、“上次时间”变量（`lastMoveDown`）以及不同的“移动频率”变量（`MOVEDOWNFREQ`）。

## 让碎片“自然”落下

| 行号 | 代码 / 注释 |
|---|---|
| 276. | # 如果该掉了，让碎片落下 |
| 277. | if time.time() - lastTime > fallFreq |
| 278. | # 检查碎片是否落地 |
| 279. | if not isValidPosition(fallingPiece, adjY=1): |
| 280. | # 掉落碎片已落地，将其放置在棋板上 |
| 281. | addToBoard(board, fallingPiece) |
| 282. | score += removeCompleteLines(board) |
| 283. | level, fallFreq = calculateLevelAndFreq(score) |
| 284. | fallingPiece = None |
| 285. | else: |
| 286. | # 碎片未落地，仅将块向下移动 |
| 287. | fallingPiece['y'] += 1 |
| 288. | lastTime = time.time() |

`time.time() - lastTime` 将计算自上次将 `lastTime` 设置为当前时间以来的秒数。如果碎片掉落，那么让碎片掉落的程序追踪了 `lastTime`。

## 绘制所有内容

| 行号 | 代码 / 注释 |
|---|---|
| 290. | # 绘制所有内容 |
| 291. | SURFACE.fill(BGCOLOR) |
| 292. | drawBoard(board) |

向作者提问邮件：al@inventwithpython.com

# 第 7 章 - 俄罗斯块

| 行号 | 代码 / 注释 |
|---|---|
| 293. | drawStatus(score, level) |
| 294. | drawNextPiece(nextPiece) |
| 295. | if fallingPiece != None: |
| 296. | drawPiece(fallingPiece) |
| 298. | pygame.display.update() |
| 299. | FPSCLOCK.tick(FPS) |

184 http://inventwithpython.com/pygame

```
319. continue
320. return event.key
321. return None
```

`checkForKey()` 函数的工作原理与在 Wormy Game 中几乎相同。
首先，它调用 `checkForQuit()` 来处理任何 `QUIT` 事件（或针对 Esc 键的 `KEYUP` 事件），如果有这些事件则终止程序。然后它从事件队列中取出所有的 `KEYUP` 和 `KEYDOWN` 事件。它忽略 `KEYDOWN` 事件（因为在 `pygame.event.get()` 中仅指定了 `KEYDOWN`），以清空队列中的这些事件。

如果事件队列中没有 `KEYUP` 事件，该函数返回 `None`。

# showTextScreen (), 一个通用文本函数

```python
324. def showTextScreen(text):
325. # 此函数在屏幕中心显示大文本，
326. # 直到按下按键为止。
327. # 绘制文本投影
328. titleSurf,titleRect = makeTextObjs(text, BIGFONT, TEXTSHADOWCOLOR)
329. titleRect.center = (int(WINDOWWIDTH / 2), int(WINDOWHEIGHT / 2))
330. DISPLAYS.blit(titleSurf, titleRect)
331.
332. # 画文本
333. titleSurf,titleRect = makeTextObjs(text, BIGFONT, TEXTCOLOR)
334. titleRect.center = (int(WINDOWWIDTH / 2) - 3, int(WINDOWHEIGHT / 2)
335).
336. DISPLAYS.blit(titleSurf, titleRect)
337. # 画额外的“按下按键开始游戏”文本。
338. pressKeySurf,pressKeyRect = makeTextObjs('Press a key to play.',
BASICFONT, TEXTCOLOR)
339. pressKeyRect.center = (int(WINDOWWIDTH / 2), int(WINDOWHEIGHT / 2) +
100)
340. DISPLAYS.blit(pressKeySurf, pressKeyRect)
```

我们不再为开始屏幕和游戏结束屏幕创建单独函数，而是创建一个名为 `showTextScreen()` 的函数。`showTextScreen()` 函数将根据 `text` 参数绘制任何文本。此外，还会显示“按下按键开始游戏.”。

请注意，第 328 到 330 行先用较深色的投影颜色绘制文本，而第 333 到 335 行绘制相同的文本，但向左偏移了 3 像素并向上偏移了 3 像素。这创建了一个“投影影”，让文本看起来更漂亮。你可以通过注释掉第 328 到 330 行来对比在没有投影影的情况下会发生什么。

向作者发送邮件提问：al@inventwithpython.com

# 第 7 章 - 俄罗斯方块 185

`showText()` 将用于开始屏幕

```python
342. while checkKeyPressed() == None:
343. pygame.display.update()
344. FPSCLOCK.tick()
```

我们希望文本留在屏幕上，直到用户按下按键。这个小循环将不断计数 `pygame.display.update()` 和 `FPSCLOCK.tick()`，直到 `checkKeyPressed()` 返回 `None` 以外的值。这发生在用户按下按键时。

## TheCheckQuit() 函数

```python
347. for event in pygame.event.get(QUIT): # 获取所有的 QUIT 事件
349. terminate() # 如果存在任何 QUIT 事件则终止
350. for event in pygame.event.get(KEYUP): # 获取所有的 KEYUP 事件
351. if event.key == _ESCAPE:
352. # 如果 KEYUP 事件是 Esc 键则终止
353. terminate()
354. pygame.event.post(event) # 将其他 KEYUP 事件放回
```

可以调用 `CheckQuit()` 函数来处理任何导致程序终止的事件。如果事件队列中有任何 QUIT 事件（由第 348 和 349 行处理），或者存在 Esc 键的 KEYUP 事件，就会发生。玩家应该能够按下 Esc 键退出程序。

由于第 350 行的 `pygame.event.get()` 获取了所有的 KEYUP 事件（包括 Esc 键以外的按键），如果它不是 Esc 键，我们希望通过调用 `pygame.event.post()` 函数将其放回事件队列。

## ThecalculateLevelAndAllFreq() 函数

```python
356. def calculateLevelAndAllFreq(score):
357. # 根据分数，返回玩家所处的等级
358. # 下落方块下降一个空格需要经过多少秒。
359. level = int(score / 10) + 1
360. fallFreq = 0.27 - (level * 0.02)
361. return level, fallFreq
```
