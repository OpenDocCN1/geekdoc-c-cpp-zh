
## 运行关卡以实际开始游戏：

| 105. | `result = runLevel(levels, currentLevelIndex)` |

`runLevel()` 函数处理游戏的所有动作。它接收关卡对象列表以及列表中要运行的关卡的整数索引。当玩家完成关卡游戏后，`runLevel()` 将返回以下字符串之一：`'solved'`（因为玩家已完成将所有星星放入目标位置）、`'next'`（因为玩家想跳到下一关卡）、`'back'`（因为玩家想回到上一个关卡）和 `'reset'`（因为玩家想重新开始当前关卡，可能是因为他们把星星推进了角落）。

| 107. | `if result in ('solved', 'next'):` |
| 108. | # 进入下一关卡。 |
| 109. | `currentLevelIndex += 1` |
| 110. | `if currentLevelIndex >= len(levels):` |
| 111. | # 如果没有更多关卡了，回到第一关。 |
| 112. | `currentLevelIndex = 0` |
| 113. | `elif result == 'back':` |
| 114. | # 进入上一个关卡。 |
| 115. | `currentLevelIndex -= 1` |
| 116. | `if currentLevelIndex < 0:` |
| 117. | # 如果没有上一个关卡了，回到最后一关。 |
| 118. | `currentLevelIndex = len(levels)-1` |

当 `runLevel()` 返回字符串 `'solved'` 或 `'next'` 时，我们需要将 `levelNum` 加 1。如果这导致 `levelNum` 超过了关卡总总数，则将 `levelNum` 重置为 0。

如果返回 `'back'`，则执行相反操作，`levelNum` 减 1。如果这使得它低于 0，则将其设置为最后一关（即 `len(levels)-1`）。

| 119. | `elif result == 'reset':` |
| 120. | `pass` |

`runLevel()` 返回了字符串 `'solved'` 或 `'next'`，那么我们需要将 `levelNum` 加 1。如果这导致 `levelNum` 超过了关卡总数，则将 `levelNum` 重置为 0。

如果返回 `'back'`，执行相反操作，`levelNum` 减 1。如果这使得它低于 0，则将其设置为最后一关（即 `len(levels)-1`）。

如果结果为 `'reset'`，`pass` 语句什么都不做。调用 `runLevel()` 函数来重置关卡。

## 第 9 章 章 星推者 261

```python
123. def runLevel(levels, levelNum):
124.     global currentImage
125.     levelObj = levels[levelNum]
126.     gameState = levelObj['state']
127.     mapObj = levelObj['map']
128.     mapNeedsRedraw = True
```

地图的数据结构只是一个单字符字符串的二维列表。`TILEmapping` 字典将此地图数据结构中使用的字符与它们所代表的图像链接起来。（这在 `drawMap()` 函数的解释中会变得清晰。）

星推者中的角色将在地图上独立地移动。这就是为什么相机需要它自己的“移动”变量：`cameraUp`、`cameraDown`、`cameraLeft` 和 `cameraRight`。`cameraOffsetX` 和 `cameraOffsetY` 变量跟踪相机的位置。

向作者发送邮件问题：`al@inventwithpython.com`

# 第 9 章 – 星星推进者 263

| 165. | `playerMoveTo = UP` |
| 166. | `elif event.key == K_DOWN:` |
| 167. | `playerMoveTo = DOWN` |
| 168. | |
| 169. | # 设置摄像移动模式。 |
| 170. | `elif event.key == K_a:` |
| 171. | `cameraLeft = True` |
| 172. | `elif event.key == K_d:` |
| 173. | `cameraRight = True` |
| 174. | `elif event.key == K_w:` |
| 175. | `cameraUp = True` |
| 176. | `elif event.key == K_s:` |
| 177. | `cameraDown = True` |
| 178. | |
| 179. | `elif event.key == K_n:` |
| 180. | `return 'next'` |
| 181. | `elif event.key == K_b:` |
| 182. | `return 'back'` |
| 183. | |
| 184. | `elif event.key == K_ESCAPE:` |
| 185. | `terminate() # Esc 键退出。` |
| 186. | `elif event.key == K_BACKSPACE:` |
| 187. | `return 'reset' # 重置关卡。` |
| 188. | `elif event.key == K_p:` |
| 189. | # 将玩家图像切换为下一张。 |
| 190. | `currentImage += 1` |
| 191. | `if currentImage >= len(PLAYERIMAGES):` |
| 192. | # 在最后一张图像后，使用第一张。 |
| 193. | `currentImage = 0` |
| 194. | `mapNeedsRedraw = True` |
| 195. | |
| 196. | `elif event.type == KEYUP:` |
| 197. | # 取消摄像移动模式。 |
| 198. | `if event.key == K_a:` |
| 199. | `cameraLeft = False` |
| 200. | `elif event.key == K_d:` |
| 201. | `cameraRight = False` |
| 202. | `elif event.key == K_w:` |
| 203. | `cameraUp = False` |
| 204. | `elif event.key == K_s:` |
| 205. | `cameraDown = False` |

这段代码处理了按下各种键时的逻辑。

| 207. | `if playerMoveTo != None and not levelComplete:` |
| 208. | # 如果玩家按了移动键，则执行移动 |
| 209. | # (如果可行）并推动任何可推动的星星。 |
| 210. | `moved = makeMove(mapObj, gameStateObj, playerMoveTo)` |
| 211. | |
| 212. | `if moved:` |
| 213. | # 增加步骤计数器。 |
| 214. | `gameStateObj['stepCounter'] += 1` |
| 215. | `mapNeedsRedraw = True` |
| 216. | |
| 217. | `if isLevelFinished(levelObj, gameStateObj):` |
| 218. | # 关卡已通过，我们应该显示“Solved!”图像。 |
| 219. | `levelIsComplete = True` |
| 220. | `keyPressed = False` |

如果 `playerMoveTo` 变量未被设置为 `None`，我们就知道玩家想要移动。调用 `makeMove()` 处理 `gameStateObj` 中玩家位置的 XY 坐标，以及推动任何星星。`makeMove()` 的返回值存储在 `moved` 中。如果该值为 `True`，则玩家角色已在该方向移动。如果值为 `False`，则玩家可能尝试进入已占据的格子，或者推一个后面有障碍物的星星。在这种情况下，玩家无法移动，且上没有任何变化。

| 221. | `pygame.fill(BGCOLOR)` |
| 222. | |
| 223. | `if mapNeedsRedraw:` |
| 224. | `mapSurface = drawMap(mapObj, gameStateObj, levelObj['goals'])` |
| 225. | `mapNeedsRedraw = False` |

地图不需要在游戏循环的每次迭代中重绘。事实上，该程序很复杂，这样做会导致轻微（但可见）的缓慢。当发生变化（例如玩家移动或星星被推动）时，地图才需要重绘。当 `mapNeedsRedraw` 变量设置为 `True` 时，通过调用 `drawMap()` 更新 `mapSurface` 变量中的对象。在第 225 行绘制地图后，`mapNeedsRedraw` 变量被设置为 `False`。如果你想通过在每次迭代中都绘图来观察程序的流程，可以注释掉第 226 行并重新运行程序。你会发现移动摄像会慢得多。

| 228. | `if cameraUp and cameraOffsetY < MAX_CAM_PAN:` |
| 229. | `cameraOffsetY += CAM_MOVE_SPEED` |
| 230. | `elif cameraDown and cameraOffsetY > -MAX_CAM_PAN:` |
| 231. | `cameraOffsetY -= CAM_MOVE_SPEED` |
| 232. | `if cameraLeft < MAX_CAM_Y_PAN:` |
| 233. | `cameraOffsetX += CAM_MOVE_SPEED` |
| 234. | `elif cameraRight and cameraOffsetX > -MAX_CAM_PAN:` |
| 235. | `cameraOffsetX -= CAM_MOVE_SPEED` |

如果移动变量设置为 `True` 且摄像没有超出 `MAX_CAM_PAN` 和 `MAX_CAM_Y_PAN` 边界，则摄像位置（存储在 `cameraOffsetX` 和 `cameraOffsetY` 中）应该移动 `CAM_MOVE_SPEED` 像素。注意第 228 和 230 行用于上下移动摄像的 `if` 和 `elif` 语句，而第 232 和 234 行是独立的 `if` 和 `elif` 语句。这使用户可以同时水平和垂直方向移动摄像。如果第 232 行是 `elif` 语句，将无法实现。

```python
## 根据摄像偏移调整 mapSurf 的 Rect。
mapSurf = mapSurf.get_rect()
mapRect.center = (HALF_WIDTH + cameraOffsetX, HALF_HEIGHT + cameraOffsetY)
## 将 mapSurf 绘制到表面上。
pygame.blit(mapSurf, mapRect)
pygame.blit(levelSurf, levelRect)
stepSurf = pygame.render('Steps: %s' % (gameStateObj['stepCounter']), 1, TEXTCOLOR)
stepRect = stepSurf.get_rect()
stepRect.bottomleft = (20, HEIGHT - 10)
pygame.blit(stepSurf, stepRect)
if levelIsComplete:
    # 关卡已解决，直到玩家操作显示“Solved!”图像
solvedRect = IMAGES['solved'].get_rect()
solvedRect.center = (HALF_WIDTH, HALF_HEIGHT)
pygame.blit(IMAGES['solved'], solvedRect)
if keyPressed:
    return 'solved'
pygame.display.update() # 将表面绘制到屏幕。
pygame.tick()
```

第 237 到 261 行定位摄像并将地图和其他图形绘制到 pygame 的显示 Surface 对象中。如果关卡已通过，胜利图像也将绘制在所有内容之上。如果用户在此迭代期间按下按键，`keyPressed` 变量将设置为 `True`，这指向 `runLevel()` 函数。

```python
def isWall(mapObj, x, y):
    """如果地图上的 (x, y) 位置是墙，返回 True，否则返回 False."""
    if x < 0 or x > len(mapObj) or y < 0 or y >= len(mapObj[x]):
        return False # x 和 y 实际上在地图之外。
    elif mapObj[x][y] in (' ', '#'):
        return True # 墙阻塞
    return False
```

```python
def decorateMap(mapObj, startxy):
    """复制并修改地图对象。
    处理方法如下：
    * 将墙转变为角块。
    * 区分外部和内部地板。
    * 在外部瓦上随机添加树木/岩石装饰。
    返回装饰后的地图对象。"""
    startx, starty = startxy # 语法糖
    # 复制地图以防修改原始对象
    mapCopy = copy.deepcopy(mapObj)
```

268 http://inventwithpython.com/pygame

| 317. | |
| 318. | `if isWall(mapObj, x, y):` |
| 319. | `return True` |
| 320. | |
| 321. | `elif x < 0 or x >= len(mapObj) or y < 0 or y >= len(mapObj[x]):` |
| 322. | `return True # x 和 y 实际上并不在地图上` |
| 323. | |
| 324. | `elif (x, y) in gameStateObj['stars']:` |
| 325. | `return True # 有星星阻挡了` |
| 326. | |
| 327. | `return False` |

地图上有空间被阻挡的三种情况：如果那里有星星，或者该空间的坐标位于地图边缘。`isBlocked()` 会检查这些情况，如果 XY 坐标有效则返回 True，否则返回 False。

```python
def makeMove(mapObj, gameStateObj, playerMoveTo):
    """移动并更新游戏状态对象，检查玩家是否可以执行
    指定的移动。如果是，则改变玩家的
    位置（以及任何被推星星的位置）。如果不是，则什么都不做。
    """
    如果玩家移动了则返回 True，否则返回 False。
    # 确保玩家可以向想要的方向移动。
    player, layer = gameStateObj['player']
    # 这个变量是“语法糖”。在你的代码中输入 "stars"
    stars = gameStateObj['stars'] in
    # 处理每个方向的代码非常相似，
    # 仅在 x/y 坐标上加或减 1。我们可以
    # 使用 xOffset 和 yOffset 变量来简化 playerMoveTo。
    if playerMoveTo == UP:
        xOffset = 0
        yOffset = -1
    elif playerMoveTo == RIGHT:
        xOffset = 1
        yOffset = 0
    elif playerMoveTo == DOWN:
        xOffset = 0
        yOffset = 1
    elif playerMoveTo == LEFT:
        xOffset = -1
        yOffset = 0
```
