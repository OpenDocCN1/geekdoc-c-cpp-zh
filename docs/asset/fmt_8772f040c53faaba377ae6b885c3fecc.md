
92.                              apple = getRandomLocation() # 在某处设置一个新苹果

93.                      else:

94.                              del wormCoords[-1] # 移除虫的尾部段

95.                  # 通过在移动方向添加段来移动虫

96.                  if direction == UP:

93.     newHead = {'x': wormCoords[HEAD]['x'], 'y':

94.     wormCoords[HEAD]['y'] - 1}

95.     elif direction == DOWN:

96.     newHead = {'x': wormCoords[HEAD]['x'], 'y':

97.     wormCoords[HEAD]['y'] + 1}

98.     elif direction == LEFT:

99.     newHead = {'x': wormCoords[HEAD]['x'] - 1, 'y':

100.    wormCoords[HEAD]['y']}

101.  elif direction == RIGHT:

102.     newHead = {'x': wormCoords[HEAD]['x'] + 1, 'y':

103.     wormCoords[HEAD]['y']}

104.  wormCoords.insert(0, newHead)

105.  DISPLAYS.fill(BGCOLOR)

106.  drawGrid()

107.  drawWorm(wormCoords)

108.  drawApple(apple)

109.  drawScore(len(wormCoords) - 3)

110.  pygame.display.update()

111.  FPSCLOCK.tick(FPS)

112. def drawKeyPressMsg():

113.     pressKeySurf = BASICFONT.render('Press key to play.', True,

114.     DARKGRAY)

115.     keyRect = pressKeySurf.get_rect()

116.     keyRect.topleft = (WINDOWWIDTH, WINDOWHEIGHT - 30)

117.     DISPLAYSURF.blit(pressKeySurf, keyRect)

118. def checkForKey():

119.     if len(pygame.event.get(QUIT)) > 0:

120.         terminate()

121. 

122.     keyEvents = pygame.event.get(KEYUP)

123.     if len(keyEvents) == 0:

124.         return None

125.     if keyEvents[0].key == K_ESCAPE:

126.         terminate()

127.         return keyEvents[0].key

128. 

129. def drawStartScreen():

130.     titleFont = pygame.font.Font('freesansbold.ttf', 100)

131.     titleSurf1 = titleFont.render('Wormy!', True, WHITE, DARKGRAY)

132.     titleSurf2 = titleFont.render('Wormy!', True, GREEN)

133.     degrees1 = 0

134.     degrees2 = 0

135.     while True:

136.         DISPLAYS.fill(BGCOLOR)

137.         rotatedSurf1 = pygame.transform.rotate(titleSurf, degrees1)

138.         rotatedRect1 = rotatedSurf1.get_rect()

139.         rotatedRect1.center = (WINDOWWIDTH / 2, WINDOWHEIGHT / 2)

140.         DISPLAYS.blit(rotatedSurf1, rotatedRect1)

141. 

142.         rotatedSurf2 = pygame.transform.rotate(titleSurf, degrees2)

143.         rotatedRect2 = rotatedSurf2.get_rect()

144.         rotatedRect2.center = (WINDOWWIDTH / 2, WINDOWHEIGHT / 2)

145.         DISPLAYS.blit(rotatedSurf2, rotatedRect2)

146. 

147. 

148.         drawPressKeyMsg()

149. 

150.         if checkKeyPress():

151.             pygame.event.get() # 清空事件队列

152.             return

153.         pygame.display.update()

154.         FPSCLOCK.tick(FPS)

155.         degrees1 += 3 # 每帧旋转 3 度

156.         degrees2 += 7 # 每帧旋转 7 度

157. 

158.     def terminate():

159.         pygame.quit()

160.         sys.exit()

161. 

162.     def getRandomLocation():

163.         return {'x': random.randint(0, CELLWIDTH - 1), 'y': random.randint(0, CELLHEIGHT - 1)}

164. 

165.     def showGameOver():

166.         gameOverFont = pygame.font.Font('freesansbold.ttf', 150)

167.         gameSurf = gameOverFont.render('Game', True, WHITE)

168.         overSurf = gameOverFont.render('Over', True, WHITE)

169.         gameRect = gameSurf.get_rect()

170.         overRect = overSurf.get_rect()

171.         gameRect.midtop = (WINDOWWIDTH / 2, 10)

172.         overRect.midtop = (WINDOWWIDTH / 2, gameRect.height + 25)

173. 

174.         DISPLAYS.blit(gameSurf, gameRect)

175.         DISPLAYS.blit(overSurf, overRect)

176.         drawPressKeyMsg()

177.         pygame.display.update()

178.         pygame.time.wait(500)

179.         checkKeyPress() # 清空事件队列中的任何按键

180. 

181.     while True:

182.         if checkKeyPress():

183.             pygame.event.get() # 清空事件队列

184.             return

185.     def drawScore(score):

186.         scoreRect = BASICFONT.render('Score: %s ' % (score), True, WHITE)

187.         scoreRect = scoreRect.get_rect()

188.         scoreRect.topleft = (WINDOWWIDTH, 120)

189.         DISPLAYS.blit(scoreRect, scoreRect)

190. 

191.     def drawWorm(wormCoords):

192.         for coord in wormCoords:

193.             x = coord['x'] * CELLSIZE

194.             y = coord['y'] * CELLSIZE

195.             wormSegment = pygame.Rect(x, y, CELLSIZE, CELLSIZE)

196.             pygame.draw.rect(DISPLAYS, DARKGREEN, wormSegment)

197.             wormInnerSegment = pygame.Rect(x + 4, y + 4, CELLSIZE - 8)

198.             pygame.draw.rect(DISPLAYS, GREEN, wormInnerSegment)

199. 

200.     def drawApple(coord):

201.         x = coord['x'] * CELLSIZE

202.         y = coord['y'] * CELLSIZE

203.         appleRect = pygame.Rect(x, y, CELLSIZE, CELLSIZE)

204.         pygame.draw.rect(DISPLAYS, RED, appleRect)

205. 

206.     def drawGrid():

207.         for x in range(0, WINDOWWIDTH, CELLSIZE): # 绘制垂直线

208.             pygame.draw.line(DISPLAYS, DARKGRAY, (x, 0), (x, WINDOWHEIGHT))

209.         for y in range(0, WINDOWHEIGHT, CELLSIZE): # 绘制水平线

210.             pygame.draw.line(DISPLAYS, DARKGRAY, (0, y), (WINDOWWIDTH, y))

211. 

212. if __name__ == '__main__':

213.     main()

```

向作者提问邮件：`al@inventwithpython.com`

程序开头的代码设置了游戏中用到常量变量。单元格的宽度和高度存储在 `CELLSIZE` 中。第 13 行和 14 行的 `assert` 语句确保单元格能够完美适应窗口。例如，如果 `CELLSIZE` 为 10，而 `WINDOWWIDTH` 或 `WINDOWHEIGHT` 设置为 15，那么只能容纳 1.5 个单元格。`assert` 语句确保只有整数倍的单元格能放入窗口中。

```
18. #               R G B

19. WHITE = (255, 255, 255)

20. BLACK = (0, 0, 0)

21. RED = (255, 0, 0)

22. GREEN = (0, 255, 0)

23. DARKGREEN = (0, 155, 0)

24. DARKGRAY = (40, 40, 40)

25. BGCOLOR = BLACK

26.

27. UP = 'up'

28. DOWN = 'down'

29. LEFT = 'left'

30. RIGHT = 'right'

31.

32. HEAD = 0 # 语法糖: 蛇蛇的索引
```

第 19 行到 32 行设置了更多常量。`HEAD` 常量将在本章稍后解释。

## `main()` 函数

```
34. def main():

35.     global FPSCLOCK, DISPLAYFACE, BASICFONT

36.

37.     pygame.init()

38.     FPSCLOCK = pygame.time.Clock()

39.     DISPLAYFACE = pygame.display.set_mode((WINDOWWIDTH, WINDOWHEIGHT))

40.     BASICFONT = pygame.font.Font('freesansold.ttf', 18)

41.

42.     pygame.display.set_caption('Wormy')

43.

44.     showStartScreen()

45.     while True:

46.         runGame()

47.         showGameOver()
```

在 Wormy 游戏程序中，我们将主体代码放在了一个名为 `runGame()` 的函数中。因为我们只想在程序启动时显示一次“启动屏幕”（带有旋转的“Wormy”文本的动画）（通过调用 `showStartScreen()` 函数）。然后我们想要调用 `runGame()`，它将启动一局 Wormy 游戏。当玩家的蛇撞到墙或自己导致游戏结束时，该函数将返回。

此时，我们将通过调用 `showGameOver()` 显示游戏结束屏幕。当该函数返回时，循环将回到开头并再次调用 `runGame()`。第 44 行的 `while` 循环将一直循环，直到程序终止。

## 独立的 `runGame()` 函数

```
49. def runGame():

50. # 设置随机起点。

51. startx = random.randint(5, CELLWIDTH - 6)

52. starty = random.randint(5, CELLHEIGHT - 6)

53. wormCoords = [{'x': startx, 'y': starty},

54. {'x': startx - 1, 'y': starty},

55. {'x': startx - 2, 'y': starty}]

56. direction = RIGHT

57.

58. # 在随机位置生成苹果。

59. apple = getRandomLocation()
```

在游戏开始时，我们希望蛇从随机位置开始（但不要离棋盘边缘太近），我们将随机坐标存储在 `startx` 和 `starty` 中。（记住 `CELLWIDTH` 和 `CELLHEIGHT` 是单元格的宽度和高度，而不是像素的宽度和高度）。

蛇的身体将存储在一个字典列表中。字典将具有 'x' 和 'y' 键，用于该身体段的 XY 坐标。身体的头部位于 `startx` 和 `starty`。另外两个身体段位于头部左侧一个和两个格的位置。

蛇的头部始终是 `wormCoords[0]` 处的身体部分。为了让代码更具可读性，我们在第 32 行将 `HEAD` 设置为 0，这样我们就可以使用 `wormCoords[HEAD]` 而不是 `wormCoords[0]` 了。

## 事件处理循环

```
61. while True: # 主游戏循环

62. for event in pygame.event.get(): # 事件处理循环

63. if event.type == QUIT:

64.     terminate()

65. elif event.type == KEYDOWN:

66.     if (event.key == K_LEFT or event.key == K_a) and direction != RIGHT:

67.         direction = LEFT

68.     elif (event.key == K_RIGHT or event.key == K_d) and direction != LEFT:

69.         direction = RIGHT

70.     elif (event.key == K_UP or event.key == K_w) and direction != DOWN:

71.         direction = UP

72.     elif (event.key == K_DOWN or event.key == K_s) and direction != UP:

73.         direction = DOWN
```
