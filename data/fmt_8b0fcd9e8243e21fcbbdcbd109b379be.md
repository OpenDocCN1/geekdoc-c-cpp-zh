
```python
215.
216. def animateDroppingToken(board, column, color):
217.     x = XMARGIN + column * SPACESIZE
218.     y = YMARGIN - SPACESIZE
219.     dropSpeed = 1.0
220.
221.     lowestEmptySpace = getLowestEmptySpace(board, column)
222.
223.     while:
224.         y += int(dropSpeed)
225.         dropSpeed += 0.5
226.         if (y - YMARGIN) / SPACESIZE >= lowestEmptySpace:
227.             return
228.         drawBoard(board, {'x':x, 'y':y, 'color':color})
229.         pygame.display.update()
230.         FPSCLOCK.tick()
231.
232. def animateComputerMove(board, column):
233.     x = XMARGIN + column * SPACESIZE
234.     y = YMARGIN - SPACESIZE
235.     dropSpeed = 1.0
236.
237.     while:
238.         y += int(dropSpeed)
239.         dropSpeed += 0.5
240.         if (y - YMARGIN) / SPACESIZE >= lowestEmptySpace:
241.             return
242.         drawBoard(board, {'x':x, 'y':y, 'color':color})
243.         pygame.display.update()
244.         FPSCLOCK.tick()
245. def getComputerMove(board):
```

324 http://inventwithpython.com/pygame

```python
261.   for i in range(BOARDWIDTH):
262.     if potentialMoves[i] > bestMove:
263.         bestMove = potentialMoves[i]
264.     # 找到所有最高分的移动
265.     bestMoves = []
266.     for i in range(len(potentialMoves)):
267.         if potentialMoves[i] == bestMove and isValidMove(board, i):
268.             bestMoves.append(i)
269.     return random.choice(bestMoves)
270.
271. def getPotentialMoves(board, tile, lookAhead):
272.     if lookAhead == 0 or isFull(board):
273.         return [ ] * BOARDWIDTH
274.
275.     if tile == RED:
276.         enemyTile = BLACK
277.     else:
278.         enemyTile = RED
279.
280.     # 确定要的移动。
281.     potentialMoves = [ ] * BOARDWIDTH
282.     for firstMove in range(BOARDWIDTH):
283.         dupeBoard = copy.deepcopy(board)
284.         if not isValidMove(dupeBoard, firstMove):
285.             continue
286.         makeMove(dupeBoard, tile, firstMove)
287.         if isWinner(dupeBoard, tile):
288.             # 胜利移动会自动获得完美分
289.             potentialMoves[firstMove] = 1
290.             break # 不计算其他移动
291.         else:
292.             # 执行对方的反击移动并确定最佳一个
293.             if isFull(dupeBoard):
294.                 potentialMoves[firstMove] = 0
295.             else:
296.                 for counterMove in range(BOARDWIDTH):
297.                     dupeBoard2 = copy.deepcopy(dupeBoard)
298.                     if not isValidMove(dupeBoard2, counterMove):
299.                         continue
300.                     makeMove(dupeBoard2, enemyTile, counterMove)
301.                     if isWinner(dupeBoard2, enemyTile):
302.                         # 失败移动会自动获得最差分
303.                         potentialMoves[firstMove] = -1
304.                         break
305.                     if potentialMoves[counterMove] > bestMove:
306.                         bestMove = potentialMoves[counterMove]
307.             if lookAhead > 1:
308.                 potentialMoves[firstMove] = getPotentialMoves(dupeBoard, enemyTile, lookAhead - 1)
309.             else:
310.                 potentialMoves[firstMove] = bestMove
311.     return potentialMoves
```

# 第 10 章 – 四个额外游戏 325

```python
306.             else:
307.                 # 执行 getPotentialMoves() 的递归调用
308.             results = getPotentialMoves(dupeBoard2, tile, lookAhead - 1)
309.             potentialMoves[firstMove] += (sum(results)) / BOARDWIDTH
310.             return potentialMoves
311.
312.
313.     def getLowestEmptySpace(board, column):
314.         # 返回该列中最低行的行号。
315.             for y in range(BOARDHEIGHT-1, -1, -1):
316.             if board[column][y] == EMPTY:
317.                 return y
318.             return -1
319.
320.
321.     def isValid(board, column):
322.         # 如果列中有空位，则返回 True。
323.         # 否则返回 False。
324.         if column < 0 or column >= (BOARDWIDTH) or board[column][0] != EMPTY:
325.             return False
326.         return True
327.
328.
329.     def isFull(board):
330.         # 如果棋上任何地方都没有空位，则返回 True。
331.             for x in range(BOARDWIDTH):
332.             for y in range(BOARDHEIGHT):
333.                 if board[x][y] == EMPTY:
334.                     return False
335.         return True
336.
337.
338.     def isWinner(board, tile):
339.         # 检查水平空间
340.             for x in range(BOARDWIDTH):
341.             for y in range(BOARDHEIGHT):
342.                 if board[x][y] == tile and board[x+1][y] == tile and
343.                     board[x+2][y] == tile and board[x+3][y] == tile:
344.                     return True
345.         # 检查垂直空间
346.             for y in range(BOARDHEIGHT):
347.                 for x in range(BOARDWIDTH):
348.                     if board[x][y] == tile and board[x][y+1] == tile and
349.                         board[x][y+2] == tile and board[x][y+3] == tile:
```

326 http://inventwithpython.com/pygame

```python
348.   return True
349.   # 检查对角线空间 - 3):
350.   for x in range(BOARDWIDTH):
351.       for y in range(3, BOARDHEIGHT):
352.           if board[x][y] == tile and board[x+1][y-1] == tile and
               board[x+2][y-2] == tile and board[x+3][y-3] == tile:
353.               return True
354.   # 检查对角线空间
355.   for x in range(BOARDWIDTH - 3):
356.       for y in range(BOARDHEIGHT - 3):
357.           if board[x][y] == tile and board[x+1][y+1] == tile and
               board[x+2][y+2] == tile and board[x+3][y+3] == tile:
358.               return True
359. return False

362. if __name__ == '__main__':
363.   main()
```

向作者提问邮件：al@inventwithpython.com

# Gemgem，一个“宝石消除”（Bejeweled）的克隆游戏

![](img/9b1932f39c4ca4cfcc81c02125104271_344_0.png)

“宝石消除”是一个宝石掉落在面板上的游戏。玩家可以交换任意两个相邻的宝石，使三个宝石排对齐（垂直或水平，但不包括对角线）。匹配的宝石随后会消失，为来自顶部的新宝石留出空间。匹配三个以上的宝石并引起宝石匹配的连锁反应将获得更多分数。玩家的得分随时间推缓慢下降，因此玩家必须不断进行匹配。当面板上不再有任何可能的匹配时，游戏结束。

# Gemgem 源代码

可以从 http://invpy.com/gemgem.py 下载此源代码。

来自 Flippy 的图像文件可以从 http://invpy.com/gemgemimages.zip 下载。

```python
1. # Gemgem (一个宝石消除克隆游戏)
2. # 由 Al Schweigart@inventwithpython.com 
3. # http://inventwithpython.com/pygame
4. # 根据“简化 BSD”许可证发布
5. ""
6. 此程序拥有“宝石数据结构”，它们本质上是带有
7. 以下键的字典：
8. - 'x' 和 'y' - 宝石在面板上的位置。0,0 是左上角。
9. 还有一个 ROWBOARD，其中 'y' 可以被设置为：
10. 表示它在面板正上方。
11. - 'direction' - UP, DOWN, LEFT, RIGHT 四个常量之一。
12. 这是宝石移动的方向。
13. - 'imageNum' - GEMIMAGES 中的索引索引用于指定
14. - 该宝石使用的图像。
```

```python
18. import random, time, pygame, copy
19. from pygame.locals import *
20. FPS = 30 # 每秒更新帧
21. WINDOWWIDTH = 600 # 程序窗口宽度（像素）
22. WINDOWHEIGHT = 600 # 高（像素）
23.
24. BOARDWIDTH = 8 # 面板列数
25. BOARDHEIGHT = 8 # 面板行数
26. GEMIMAGESIZE = 64 # 每个格子的宽和高（像素）
27.
28. # GEMIMAGES 是宝石的种类。你需要名为
29. gem0.png, gem1.png 到 gem(N-1) 的文件。
30. NUMGEMIMAGES = 7
31. assert GEMIMAGES >= 5 # 游戏至少 5 种宝石才能运行
32.
33. # NUMSOUNDS 是匹配时可选的不同声音数量。
34. .wav 文件为 match0.wav, match1.wav 等。
35. NUMSOUNDS = 6
36.
37. MOVERATE = 25 # 1 到 100，越大动画越快
38. DEDUCTSPEED = 0.8 # 每个 DCTSPEED 减少 1 分
39.
40. # RGB
41. PURPLE = (255, 0, 255)
42. LIGHTBLUE = (170, 190, 255)
43. BLUE = (0, 0, 255)
44. RED = (255, 0, 100)
45. BLACK = (0, 0, 0)
46. BROWN = (85, 65, 0)
47. HIGHLIGHTCOLOR = PURPLE # 选中宝石的边框颜色
48. BGCOLOR = BLUE # 面板颜色
49. GRIDCOLOR = RED # “游戏结束”文本的颜色
50. GAMEOVERBGCOLOR = BLACK # “游戏结束”文本的背景颜色
51. SCORE = BROWN # 玩家得分文本的颜色
52.
53. # 面板距离窗口边缘的距离
54. 使用多次，计算一次并存储在变量中
55. XMARGIN = int((WINDOWWIDTH - GEMIMAGESIZE) / 2)
56. YMARGIN = int((WINDOWHEIGHT - GEMIMAGESIZE) / 2)
57.
58. # 方向值的常量
59. UP = 'up'
60. DOWN = 'down'
61. LEFT = 'left'
```
