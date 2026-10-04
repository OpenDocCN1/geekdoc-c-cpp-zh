
轮到电脑时，我们做的第一件事是调用`drawBoard()`将棋盘打印给玩家。我们现在为什么要这样做？因为要么是电脑被选中执行游戏的第一步，在这种情况下，我们应该在电脑移动之前向玩家显示棋盘的原始起始画面；要么是玩家先走了棋，我们想要展示玩家移动后但电脑移动前的棋盘状态。

在用`drawBoard()`打印棋盘后，我们还想通过调用`showPoints()`来打印当前得分。

接下来，我们调用`raw_input()`来暂停脚本，让玩家可以查看棋盘。这与我们在“笑笑话”章节中使用`raw_input()`暂停游戏的方式非常相似。你不需要在调用`raw_input()`之前使用`print`语句来打印字符串，而是将字符串作为参数传递给`raw_input()`。`raw_input`有一个可选的字符串参数。我们在这次调用中传递的字符串是`'Press Enter to see the computer's move.'`

在玩家查看棋盘并按下回车键后（玩家输入的任何文本都会被忽略，我们没有将`raw_input()`的返回值赋值给任何变量），我们通过`getComputerMove()`获取电脑下次移动的 X 和 Y 坐标。我们将这些坐标分别存储在变量`x`和`y`中。

最后，我们将`x`和`y`以及游戏棋盘数据结构和电脑的棋子传递给`makeMove()`函数，以更改棋盘以反映电脑的移动。我们调用`getComputerMove()`获取了电脑的移动，而调用`makeMove()`则执行了该移动。

```
289.    if getValidMoves(mainBoard, playerTile) == []:
290.        break
291.    else:
292.        turn = 'player'
```

第 289 到 292 行与第 276 到 279 行非常相似。在电脑移动后，我们检查人类玩家是否还有任何可能的移动。如果`getValidMoves()`返回空列表，则说明没有可能的移动。这意味着游戏结束了，我们应该跳出所在的`while`循环。

否则，玩家至少有一个可以执行的移动，所以我们应该将`turn`设置为`'player'`。在第 292 行之后`while`块中没有更多代码了，因此执行循环回到第 257 行的语句。

```
294.    # Display the final score.
295.    drawBoard(mainBoard)
296.    scores = getScoreOfBoard(mainBoard)
297.    print 'X scored %s points. O scored %s points.' % (scores['X'], scores['O'])
298.    if scores[playerTile] > scores[computerTile]:
299.        print 'You beat the computer by %s points! Congratulations!' % (scores[playerTile] - scores[computerTile])
300.    elif scores[playerTile] < scores[computerTile]:
301.        print 'You lost. The computer beat you by %s points.' % (scores[computerTile] - scores[playerTile])
302.    else:
303.        print 'The game was a tie!'
```

第 294 行是第 257 行开始的`while`块之前的第一行。这段代码在我们跳出该`while`循环时执行，无论是在第 290 行还是 277 行。（第 257 行的`while`语句条件仅仅为`True`，所以我们只能通过`break`进入循环。）

到此时，游戏已经结束。我们应该打印棋盘和得分，并确定谁赢了游戏。`getScoreOfBoard()`将返回一个包含键`'X'`和`'O'`的字典，其值为两个玩家的得分。通过检查玩家得分是大于、小于还是等于电脑得分，我们可以知道玩家是胜了、输了还是双方平局。

用一个得分减去另一个得分是查看一方胜过对方多少分的简单方法。我们在第 297 行和 301 行的`print`语句使用了字符串插值，将此减法的结果放入要打印的字符串中。

```
305. if not playAgain():
306.     break
307.
```

游戏现在已经结束，胜者已经宣布。我们应该调用`playAgain()`函数，如果玩家输入想再玩一局，该函数将返回`True`。如果`playAgain()`返回`False`（使得`if`语句条件为`True`），我们跳出`while`循环（从 248 行开始的那个），由于该`while`块之后没有更多代码，程序终止。

否则，`playAgain()`为`True`（使得`if`语句条件为`False`），因此执行循环回到第 248 行的`while`语句并创建一个新棋盘。

## 发明自己的游戏的建议

关于游戏，本书就此为止了。下一章将扩展创建新的黑白 AI，并让 AI 相互对决而不是与人类玩家。使用书中的编程技巧，你可以构建自己的游戏。

- 在编写代码之前画流程图可能有助于你记住想在游戏中发生的一切。
- 使用交互式 shell 来测试表达式或函数调用的结果。shell 是尝试不同函数的极佳方法。
- 如果运行程序时发生奇怪的情况，可以在代码中间添加一些`print`语句来打印不同变量的值。你可以使用`print`语句检查某些函数是否按预期被调用，或者循环迭代了多少次。
- 如果你发现自己在程序的多个地方编写相同的代码，看看是否可以将这些代码放入一个函数并多次调用该函数。这样，如果你想更改函数中的代码，只需要在一个地方进行修改即可。

让我们再做一些更改。所有为黑白棋（Reversi）定义的函数都可以保持不变。但将程序的整个主部分（从 246 行开始）修改为如下所示：

### AISim1.py

```python
246. print 'Welcome to Reversi!'
247.
248. while True:
249.     # 重置棋盘和游戏。
250.     mainBoard = getNewBoard()
251.     resetBoard(mainBoard)
252.     if whoGoFirst() == 'player':
253.         turn = 'X'
254.     else:
255.         turn = 'O'
256.     print ' ' + turn + ' will go first.'
257.
258.     while True:
259.         drawBoard(mainBoard)
260.         scores = getScoreOfBoard(mainBoard)
261.         print 'X has %s points. O scored %s points. %' % (scores['X'], scores['O'])
262.         raw_input('Press Enter to continue.')
263.
264.         if turn == 'X':
265.             # 'X' 的回合。
266.             otherTile = 'O'
267.             x, y = getComputerMove(mainBoard, 'X')
268.             makeMove(mainBoard, 'X', x, y)
269.
270.     else:
271.         # 'O' 的回合。
272.         otherTile = 'X'
273.         x, y = getComputerMove(mainBoard, 'O')
274.         makeMove(mainBoard, 'O', x, y)
275.
276.     if getValidMoves(mainBoard, otherTile) == []:
277.         break
278.     else:
279.         turn = otherTile
280.
281.         # 显示最终得分。
282.         drawBoard(mainBoard)
283.         scores = getScoreOfBoard(mainBoard)
284.         print 'X scored %s points. O scored %s points. %' % (scores['X'], scores['O'])
285. if not playAgain():
286.     sys.exit()
```

### 代码解释

当你运行`AISim1.py`程序时，你所能做的每回合按回车键，直到游戏结束。运行几局游戏并观察电脑自己对战。由于 X 和 O 玩家都使用相同的算法，谁获胜完全取决于运气。X 玩家会赢得一半的次数，O 玩家也会赢得另一一半的次数。

但如果我们创建一个新算法呢？那么我们就可以让新 AI 与`getComputerMove()`中实现的算法进行对比，看看哪一个更好。让我们对程序进行一些更改。点击“文件”并“保存”，将此文件保存为`AI2.py`，这样我们就可以不影响`AISim1.py`的情况下进行修改。

添加以下代码。新增的部分已**加粗**，并且删除了一些行：

```python
AISim2.py
246. print 'Welcome to Reversi!'
247.
248. xwins = 0
249. owins = 0
250. ties = 0
251. numGames = int(raw_input('Enter number of games to run: '))
252.
253. for game in range(numGames):
254.     print 'Game #%s' % (game),
255.     # 重置棋盘和游戏。
256.     mainBoard = getNewBoard()
257.     resetBoard(mainBoard)
258.     if whoGoesFirst() == 'player':
259.         turn = 'X'
260.     else:
261.         turn = 'O'
262.
263.     while True:
264.         if turn == 'X':
265.             # X 的回合。
266.             otherTile = 'O'
267.             x, y = getComputerMove(mainBoard, 'X')
268.             makeMove(mainBoard, 'X', x, y)
269.     else:
270.         # O 的回合。
271.         otherTile = 'X'
272.         x, y = getComputerMove(mainBoard, 'O')
273.         makeMove(mainBoard, 'O', x, y)
274.
275.         if getValidMoves(mainBoard, otherTile) == []:
276.             break
277.         else:
278.             turn = otherTile
279.
280.             # 显示最终得分。
281.             scores = getScoreOfBoard(mainBoard)
282.             print 'X scored %s points. O scored %s points. %' % (scores['X'], scores['O'])
283. if scores['X'] > scores['O']:
284.     xwins += 1
285. elif scores['X'] < scores['O']:
286.     owins += 1
287. else:
288.     ties += 1
289. numGames = float(numGames)
290. xpercent = round((xwins / numGames) * 100, 2)
291. opercent = round((owins / numGames) * 100, 2)
292. tiepercent = round((ties / numGames) * 100, 2)
293. print 'X wins %s games (%%%), O wins %s games (%%%), ties for %s games (%%%) of %s games total.' % (xpercent, opercent, tiepercent, numGames)
```

我们添加了变量`xwins`、`owins`和`ties`来记录 X 获胜、O 获胜以及平局的次数。第284到289行在每局游戏结束时增加这些变量，然后开始新游戏。我们删除了大部分`print`语句和`draw()`的调用。当你运行`Ai2.py`时，它会询问你想要运行多少局游戏。现在我们已经移除了`draw()`的调用并将`while True:`循环替换为`for game in range(numGames):`，我们可以在运行多局游戏而不需要停下来输入任何内容。

### 运行结果

欢迎来到黑白棋！

要运行的游戏数：10

游戏 #0
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #1
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #2
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #3
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #4
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #5
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #6
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #7
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #8
X 有 0 分。O 得了 0 分。按回车键继续。
游戏 #9
X 有 0 分。O 得了 0 分。按回车键继续。
X 赢了 5 局 (50.0%)，O 赢了 5 局 (50.0%)，平局 0 局 (0.0%)，总共 10.0 局。

```python
>>> round(10.0)
10.0
>>> round(10.2)
10.0
>>> round(8.7)
9.0
>>> round(4.5)
5.0
>>> round(3.5)
4.0
>>> round(3.4999)
3.0
>>> round(2.5422, 2)
2.54
```

如你所见，当数字的小数部分为 .5 或更大，数字会向上舍入。此外，`round()`函数还有一个可选参数，你可以在其中指定希望将数字舍入到哪位数。例如，表达式`round(2.5422)`的评估结果为 2.54。

### 代码解释继续...

```python
291. numGames = float(numGames)
292. xpercent = round((xwins / numGames) * 100, 2)
293. opercent = round((owins / numGames) * 100, 2)
294. tiepercent = round((ties / numGames) * 100, 2)
295. print 'X wins %s games (%%%%%), O wins %s games (%%%%%), ties for %s games (%%%%%) of %s games total. %%%%' % (xwins, xpercent, owins, opercent, tiepercent, numGames)
```
