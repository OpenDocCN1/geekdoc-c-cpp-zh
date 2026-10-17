
```python
129. def enterPlayerTile():
130.     # 让玩家输入他们想成为棋子。
131.     # 返回一个以玩家棋子作为第一个元素、计算机棋子作为第二个元素的列表。
132.     tile = ''
133.     while not (tile == 'X' or tile == 'O'):
```

```python
134.    print 'Do you want to be X or O?'
135.    tile = raw_input().upper()
```

此函数询问玩家想扮演 `'X'` 还是 `'O'`。`for` 循环将持续进行直到玩家输入 `'X'` 或 `'O'` 为止。

```python
1371.    # the first element in the tuple is the player's
tile, the second is the computer's tile.
1372
    if tile == 'X':
1373.        return ['X', 'O']
1374.    else:
1375.        return ['0', 'X']
```

`enterPlayer()` 函数返回一个包含两个元素的列表，其中玩家的选择是第一个元素，计算机的棋子是第二个元素。我们使用列表而不是字典，这样调用此函数的赋值语句就可以使用多赋值技巧（参见第 252 行）。

```python
144. def whoGoesFirst():
145.    # Randomly choose the player who goes first.
146.    if random.randint(0, 1) == 0:
147.        return 'computer'
148.    else:
149.        return 'player'
```

`whoGoesFirst()` 函数随机选择谁先手，并返回字符串 `'computer'` 或字符串 `'player'`。

```python
152. def playAgain():
153.    # This function returns True if the player wants to
play again, otherwise it returns False.
154.    print 'Do you want to play again? (yes or no)'
155.    return raw_input().lower().startswith('y')
```

我们之前的之前的游戏中使用过 `playAgain()`。如果玩家输入以 `'y'` 开头的的内容，则函数返回 `True`。否则，函数返回 `False`。

```python
158. def makeMove(board, tile, xstart, ystart):
159. # Place the tile on the board at xstart, ystart,
and flip any of the opponent's pieces.
160. # Returns False if this is an invalid move,
True if it is valid.
161. tilesToFlip = isValidMove(board, tile, xstart, ystart)
```

`makeMove()` 是我们想要在棋盘上放置棋子并根据黑白棋（Reversi）规则翻转对方任何棋子时的函数。对直接传递的 `board` 变量的修改（因为它是一个列表）将作用于全局作用域。大部分工作由 `isValidMove()` 完成，它返回一个包含需要翻转的棋子的 XY 坐标列表（一个包含两个元素的列表）。（记住，如果 `xstart` 和 `ystart` 指向一个无效移动，`isValidMove()` 将返回布尔值）

```python
163. if tilesToFlip == False:
164.   return False
165.   board[xstart][ystart] = tile
166.   for x, y in tilesToFlip:
167.     board[x][y] = tile
168.   return True
```

如果 `isValidMove()` 的返回值为 `False`，那么 `makeMove()` 也会返回 `False`。否则，`isValidMove()` 将返回棋盘上可以放置棋子的位置列表（`'X'` 或 `'O'` 字符串）。第 166 行设置了玩家移动的位置，之后的 `for` 循环设置了所有在 `tilesFlip` 中的棋子。

```python
172. def getBoardCopy(board):
173.   # Make a duplicate of the board list and return the
duplicate.
174.   dupeBoard = getBoard()
175.   for x in range(8):
176.       for y in range(8):
177.           dupeBoard[x][y] = board[x][y]
```

`getBoardCopy()` 创建棋盘列表的副本并返回该副本。`getBoardCopy()` 不同于 `getBoard()`。它会创建一个棋盘的副本。`getBoard()` 会创建一个新的棋盘结构。玩家在棋盘上移动的位置是空间。

```python
183. def isOnCorner(x, y):
184.   # Returns True if the position is one of
corners.
185.   return (x == 0 and y == 0) or (x == 0 and y == 7) or \
186.          (x == 7 and y == 0) or (x == 7 and y == 7)
```

`isOnCorner()` 返回该位置是否是角落之一。由于黑白棋是 8x8 大小，`isOnCorner()` 返回布尔。

```python
188. def getPlayerMove(board, tile):
189.   # Let the player type in their move.
190.   # Returns the move as [x, y] (or returns
'hints' or 'quit')
191. DIGITSTO8 = '1 2 3 4 5 6 7 8'.split()
```

`DIGITSTO8` 是列表 `['1', '2', '3', '4', '5', '6', '7', '8']`。我们创建这个变量是因为比整个列表更容易处理黑白棋。

`getPlayerMove()` 函数被调用以让玩家输入下一个移动的坐标（并检查移动是否有效）。玩家也可以输入 `'hints'` 来开启/关闭提示，或者输入 `'quit'` 来退出游戏。

```python
192.   while True:
193.       print 'Enter your move, or type quit to end
game, or hints to turn off/on'
194.       move = raw_input().lower()
195.       if move == 'quit':
196.           return 'quit'
197.       if move == 'hints':
198.           return 'hints'
```

`while` 循环将持续运行直到玩家输入有效的移动。首先检查玩家是否想要退出或切换提示模式，并返回字符串 `'quit'` 或 `'hints'`。我们对 `raw_input()` 返回的字符串使用 `lower()` 方法，以便玩家输入 `'HINTS'` 或 `'Quit'` 仍被游戏理解。

```python
200.   if len(move) == 2 and move[0] in DIGITSTO8 \
201.       move[1] in DIGITSTO8:
202.           x = int(move[0]) - 1
203.           y = int(move[1]) - 1
204.           if isValidMove(board, tile, x, y):
205.               continue
206.       else:
207.           break
208.       print 'That is not a valid move. Type the x digit (1-8), then the y digit (1-8).'
209.       print 'For example, 8 will be the top-right corner.'
```

```python
214. def getComputerMove(board, computerTile):
215. # Given a board and the computer's tile, determine where to
216. move and return that move as a [x, y] list.
217. possibleMoves = getValidMoves(board, computerTile)
```

## The `random.shuffle()` Function

```python
219. # randomize the order of the possible moves
220. random.shuffle(possibleMoves)
```

```python
>>> random
>>> spam = [1, 2, 3, 4, 5, 6, 7, 8]
>>> spam
[1, 2, 3, 4, 5, 6, 7, 8]
>>> random.shuffle(spam)
>>> spam
[2, 6, 5, 1, 4, 7, 3]
>>> random.shuffle(spam)
>>> spam
[7, 4, 2, 3, 8, 1, 5, 6]
>>> random.shuffle(spam)
>>> spam
[7, 6, 1, 4, 5, 3, 2, 8]
```

你的结果可能有所不同，因为重新洗牌是随机的。正如你所见，`random.shuffle()` 本身没有返回值。它直接修改列表，就像我们的 `resetBoard()` 函数一样。这就是为什么你必须在 shell（终端）中输入 `spam` 来查看它获得的新值。

### 代码解释继续...

我们将解释为什么想要洗牌 `possibleMoves` 列表，但首先让我们看看我们的算法。

| | 222. | # 如果可用，始终选择角位置 |
| :--- | :--- |
| 223. | `for x, y in possibleMoves:` |
| 224. | `if isOnCorner(x, y):` |
| 225. | `return [x, y]` |

首先，我们遍历 `possibleMoves` 中的每一个移动，如果其中任何一个移动在角落上，我们就返回该移动。选择角落移动是一个好主意，因为棋子被放置在角落后，它永远不会被翻转。由于 `possibleMoves` 是一个包含两个元素的列表的列表，我们在 `for` 循环中使用多变量赋值技巧来设置 `x` 和 `y`。

由于我们在 `random` 中找到第一个角落移动时就会立即返回，如果 `random` 包含多个角落移动，我们总是选择第一个。但由于 `possibleMoves` 在第 220 行已经洗过过牌，所以列表中哪个角落移动排在第一个是完全随机的。

| | 227. | # 遍历所有可能的移动并记住得分最高的移动 |
| :--- | :--- |

```python
228.   bestScore = -1
229.   for x, y in possibleMoves:
230.       dupeBoard = getBoardCopy(board)
231.       makeMove(dupeBoard, computerTile, x, y)
232.       score = getScoreOfBoard(dupeBoard)
233.       if score > bestScore:
234.           bestMove = [x, y]
235.           bestScore = score
236.   return bestMove
```

如果没有剩余的移动，我们将遍历整个列表并找出哪个移动能带给我们最高分。循环将把 `x` 和 `y` 设置为 `possibleMoves` 中的每一个移动。`bestMove` 将是到目前为止我们找到的得分最高的移动，而 `bestScore` 将被设置为它的得分。当循环中的代码找到一个比 `bestScore` 更高的移动时，我们将该移动和得分作为 `bestMove` 和 `bestScore` 的新值存储起来。

为了计算当前正在迭代的可能移动的得分，我们首先通过调用 `getBoardCopy()` 创建一个副本盘数据结构。我们想要一个副本，这样可以在不修改存储在 `board` 变量中的真实游戏数据结构的情况下进行修改。

然后调用 `makeMove()`，传递副本盘而不是真实盘。`makeMove()` 将处理计算机棋子和翻转玩家的移动，并应用到副本盘上。

我们使用副本盘调用 `getScoreOfBoard()`，它会返回一个字典，其中键为 `'X'` 和 `'O'`，值为对应的得分。`getScoreOfBoard()` 并不知道计算机是 `'X'` 还是 `'O'`，这就是为什么它返回一个字典。

通过创建副本盘，我们可以模拟一次移动并测试移动的结果，而无需更改实际游戏的数据结构。这在决定哪个移动是最佳选择时非常有帮助。

假设 `getScoreOfBoard()` 返回字典 `{'X':22, 'O':8}` 且 `computerTile` 为 `'X'`。那么 `getScoreOfBoard(dupeBoard)[computerTile]` 的求值为 `{'X':22, 'O':8}`，然后求值为 22。如果 22 大于 `bestScore`，则 `bestScore` 被设置为 22，`bestMove` 被 设置为我们正在查看的当前 `x` 和 `y` 值。当 `for` 循环结束时，我们可以确定 `bestScore` 是我们能获得的最高分，并存储在 `bestMove` 中。

你可能注意到在第 228 行我们首先将 `bestScore` 设置为 -1。这样做是为了在 `possibleMoves` 循环中查看的第一个移动将设置为第一个 `bestMove`。这将保证在返回它时，`bestMove` 一定被设置为移动中的一个。

假设 `possibleMoves` 中得分最高的移动会给计算机带来 42 分。如果 `possibleMoves` 中有移动都能得到这个分呢？计算机将选择第一个得到 42 分的移动，因为只有当得分高于 `bestScore` 时我们才会更新它。

```python
239. def showPoints(playerTile, computerTile):
240.     # 输出当前得分
241.     scores = getScoreOfBoard(board)
242.     print('You have %s points. The computer has %s points.' % (scores[playerTile], scores[computerTile]))
```

`showPoints()` 仅仅调用 `getScoreOfBoard()` 并打印玩家和计算机的得分。记住 `getScoreOfBoard()` 返回一个键为 `'X'` 和 `'O'`，值为得分的字典。

这就是我们为 Reversi 定义的所有函数。从第 246 行的代码会在需要时调用这些函数。

如果 `False` 返回一个空列表，则计算机没有更多可以执行的移动了（最可能是棋盘已满）。在这种情况下，我们跳出 `while` 循环和当前游戏。

否则，我们将 `turn` 设置为 `'computer'`。执行流将跳过 `else` 块并到达 `while` 块的结束，因此执行跳转回第 257 行的 `while` 语句。这次，将轮到电脑了。

```python
281.     else:
282.         # Computer's turn.
283.         drawBoard(mainBoard)
284.         showPoints(playerTile, computerTile)
285.         raw_input('Press Enter to see the
286.             computer's move.')
287.         x, y = getComputerMove(mainBoard,
288.             computerTile)
289.         makeMove(mainBoard, computerTile, x, y)
```
