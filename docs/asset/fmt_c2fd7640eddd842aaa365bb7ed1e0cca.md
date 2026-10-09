
`def getBounceAmount(currentBounce, bounceRate, bounceHeight):`

```
    # 根据弹跳返回偏移像素数。

    # 较大的 bounceRate 意味着弹跳越慢。

    # currentBounce 永远小于 bounceRate

    return int(math.sin(math.pi / float(bounceRate)) * currentBounce )
```

`def getRandomVelocity():`

```
    speed = random.randint(SQUIRRELMINSPEED, SQUIRRELMAXSPEED)

    if random.randint(0, 1) ==:

        return speed

    else:

        return -speed
```

`def getRandomOffCameraPos(camax, cameray, objWidth, objHeight):`

```
    # 创建相机视图的 Rect

    cameraRect = pygame.Rect(camax, cameray, WINWIDTH, WINHEIGHT)

    while True:

        x = random.randint(camerax - WINWIDTH, camerax + (2 * WINWIDTH))

        y = random.randint(cameray - WINHEIGHT, cameray + (2 * WINHEIGHT))

        # 使用随机坐标创建 Rect 对象并使用

        # colliderect()

        # 确保右边缘不在相机视图内。

        objRect = pygame.Rect(x, y, objWidth, objHeight)

        if not objRect.colliderect(cameraRect):

            return x, y
```

`def makeNewSquirrel(camerax, cameray):`

```
    sq = {}

    generalSize = random.randint(5,25)

    multiplier = random.randint(1,3)

    sq['width'] = (generalSize + random.randint(0, 10)) * multiplier

    sq['height'] = (generalSize + random.randint(0, 10)) * multiplier

    sq['x'], sq['y'] = getRandomOffCameraPos(camerax, cameray)

    sq['move'] = getRandomVelocity()

    sq['my'] = getRandomVelocity()

    if sq['move'] < 0: # 老鼠面向左

        sq['surface'] = pygame.transform.scale(L_SQUIR_IMG, (sq['width'], sq['height']))

    else: # 老鼠面向右

        sq['surface'] = pygame.transform.scale(R_SQUIR_IMG, (sq['width'], sq['height']))

    sq['bounce'] = 0

    sq['bouncerate'] = random.randint(10,18)

    sq['bounceheight'] = random.randint(10,50)

    return sq
```

`def makeNewGrass(camerax, cameray):`

```
    gr = {}

    gr['image'] = random.randint(0, len(GRASSIMAGES) - 1)

    gr['width'] = GRASSIMAGES[0].get_width()

    gr['height'] = GRASSIMAGES[0].get_height()

    gr['x'], gr['y'] = getRandomOffCameraPos(camerax, cameray)

    gr['width'], gr['height'] = pygame.Rect(gr['x'], gr['y'], gr['width'], gr['height'])

    return gr
```

`def isOutsideArea(camerax, cameray, obj):`

```
    # 如果 camerax 和 cameray 超过
```

# 第 8 章 – 老鼠吃老鼠 211

387. # 超出窗口边缘半个窗口长度。
388. boundsLeftEdge = kamerax - WINWIDTH
389. boundsTopEdge = cameray - WINHEIGHT
390. boundsRect = pygame.Rect(boundsLeftEdge, boundsTopEdge, WINWIDTH * 3, WINHEIGHT * 3)
391. objRect = pygame.Rect(obj['x'], obj['y'], obj['width'], obj['height'])
392. return not objRect.colliderect(cameraRect)
393. 394.
395. if __name__ == '__main__':
396. main()

## 设置
1. # 老鼠吃老鼠（一个克隆版）
2. # import random, sys
3. import pygame
4. from time import *
5. FPS = 30 # 每秒帧
6. WINWIDTH = 640 # 窗口宽度
7. WINHEIGHT = 480 # 窗口高度
8. HALF_WINWIDTH = int(WINWIDTH / 2)
9. HALF_WINHEIGHT = int(WINHEIGHT / 2)
10. GRAY = (128, 128, 128)
11. WHITE = (255, 255, 255)
12. RED = (255, 0, 0)
13. # 弹跳频率
14. # 弹跳频率
15. # 较大的 意味着弹跳越慢

| 常量 | 描述 |
| :--- | :--- |
| BOUNCERATE | 弹跳频率 |
| BOUNCEHEIGHT | 弹跳高度 |
| STARTSIZE | 玩家的大小 |
| WINSIZE | 玩家的大小 |
| INVULNTIME | 玩家无敌时间 |
| GAMEOVERTIME | 游戏结束持续时间 |
| NUMGRASS | 区域内草的数量 |
| NUMQUIRLS | 区域内老鼠的数量 |
| SQUIRRELMINSPEED | 老鼠最小速度 |
| SQUIRRELMAXSPEED | 老鼠最大速度 |
| DISCHARGEFREQ | 方向改变频率 |
| LEFT | 向左 |
| RIGHT | 向右 |

注释说明常量的作用。

## 描述数据结构

"""
程序使用三个数据结构来表示玩家、敌对老鼠和背景对象。这些数据结构是包含字典：

所有数据结构使用的键：
- 'x' - 对象在游戏世界的左边缘坐标（不是屏幕坐标）
- 'y' - 对象在游戏世界的上边缘坐标（不是屏幕坐标）
- 'rect' - 表示对象在屏幕上的 Rect 对象

玩家数据结构键：
- 'surface' - 存储绘制图像的 pygame.Surface 对象。
- 'facing' - 设置为 LEFT 或 RIGHT，存储玩家面向的方向。
- 'size' - 玩家的宽度和高度（两者相等）。
- 'bounce' - 代表弹跳的阶段。0 表示（不弹跳），到 BOUNCERATE 为完成弹跳。
- 'health' - 显示玩家死亡前被大老鼠击中的次数。

敌老鼠数据结构键：
- 'surface' - 存储绘制到屏幕图像的 pygame.Surface 对象。
- 'movex' - 老鼠每帧水平移动的像素数。负整数向左，正整数向右。
- 'movey' - 老鼠每帧垂直移动的像素数。负整数向上，正整数向下。
- 'width' - 老鼠图像的宽度（像素）。
- 'height' - 老鼠图像的高度（像素）。
- 'bounce' - 代表玩家弹跳的阶段。0 表示（不弹跳），到 BOUNCERATE 为完成弹跳。
- 'bouncer' - 老鼠如何弹跳。数值越小弹跳越快。
- 'bounceheight' - 老鼠弹跳的高度。

草数据结构键：
- 'grassImage' - 一个整数，指向 GRASSIMAGES 中使用的 pygame.Surface 对象的索引。
"""

## pygame.transform.flip() 函数

```
73. # 加图像文件

74. L_SQUIR_IMG = pygame.image.load('squirrel.png')

75. R_SQUIR_IMG = pygame.transform.flip(L_SQUIR_IMG, True, False)

76. GRASSIMAGES = []

77. for i in range(1, 5):

78. GRASSIMAGES.append(pygame.image.load('grass%s.png' % i))
```

玩家和敌人松鼠的图像是从 `squirrel.png` 加载的，请确保该 png 文件与 `squirrel.py` 位于同一个文件夹下，否则你将得到 `pygame.error: Couldn't open squirrel.png` 错误。

`squirrel.png` 中的图像（你可以从 http://invpy/squirrel.png 下载）是一只向左的松鼠。与其创建一个包含向右松鼠图像的 Surface 对象，或者创建一个第二个 png 图像文件，我们可以调用 `pygame.transform.flip()` 函数。该函数有三个参数：要翻转的图像 Surface 对象、用于水平翻转的布尔值以及用于垂直翻转的布尔值。通过向第二个参数传递 `True` 向第三个参数传递 `False`，返回一个松鼠向右的图像的 Surface 对象。我们传入的原始 Surface `L_SQUIR_IMG` 保持不变。

以下是水平和垂直翻转的图像示例：

![](img/9b1932f39c4ca4cfcc81c02125104271_231_0.png)

```
80. while True:
81.     runGame()
```

`main()` 中的设置已完成，游戏通过调用 `runGame()` 开始。

# 比通常更详细的游戏状态

```
84. def runGame():
85.     # 为新游戏的开始设置变量
```

向作者提问邮件：`al@inventwithpython.com`

# 第 8 章 – 松鼠吃松鼠 215

| 86. | invulnerableMode = False # 如果玩家处于无敌状态 |
| 87. | invulnerableStartTime = 0 # 玩家变为无敌状态的时间 |
| 88. | gameOverMode = False # 如果玩家已经失败 |
| 89. | gameOverStartTime = 0 # 玩家失败的时间 |
| 90. | winMode = False # 如果玩家已经胜利 |

“松鼠吃松鼠”游戏有几个变量用于跟踪游戏状态。这些变量将在稍后在代码中使用时进行更详细的解释。

# 通常的文本创建

| 92. | # 创建用于保存游戏文本的 surface |
| 93. | gameOverSurf = BASICONT.render('Game Over', True, WHITE) |
| 94. | gameOverRect = gameOverSurf.get_rect() |
| 95. | gameOverRect.center = (HALF_WIDTH, HALF_WINHEIGHT) |
| 96. | |
| 97. | winSurf = BASICONT.render('You have achieved OMEGA SQUIRREL!', True, |
| 98. | WHITE) winRect = winSurf.get_rect() |
| 99. | winRect.center = (HALF_WIDTH, HALF_WINHEIGHT) |
| 100. | winSurf2 = BASICONT.render('Press "r" to restart'), True, WHITE) |
| 101. | winRect2 = winSurf2.get_rect() |
| 102. | winRect2.center = (HALF_WIDTH, HALF_WINHEIGHT + 30) |

这些变量包含了 Surface 对象，带有“Game Over”、“You have achieved OMEGA SQUIRREL!”以及“Press 'r to restart.'”，这些文本会在游戏结束时（无论玩家失败还是胜利）显示。

## 摄像机

| 105. | # camerax 和 cameray 是摄像视图中心的位置 |
| 106. | camerax = 0 |
| 107. | cameray = 0 |

`camerax` 和 `cameray` 变量跟踪“相机”的游戏坐标。想象世界是一个无限的 2D 空间。显然，这永远无法完全呈现在任何屏幕上。我们只能在屏幕上绘制无限 2D 空间的一部分。我们将这部分区域称为相机，因为我们的屏幕只是相机能看到的游戏世界前方区域。这里是游戏世界（无限的绿色区域）和相机可以查看区域的图片：

## 游戏世界继续
(Y 坐标变小)

![](img/9b1932f39c4ca4cfcc81c02125104271_233_0.png)

你可以看到，游戏世界的 XY 坐标不断增大和减小。游戏世界的原点是 (0, 0) 世界坐标的地方。你可以看到三只松鼠位于（世界坐标为）(-384, -84)、(384, 306) 和 (585, -234)。

我们只能在屏幕上显示 640 x 480 像素的区域（尽管通过向 `pygame.display.set_mode()` 传递不同的数字可以改变这种变化），因此我们需要跟踪摄像机原点在游戏世界中的位置。在上面的图中，相机位于游戏世界的 (-486, -330)。

下面的图片显示了相同的草地和松鼠，但都是以相机坐标给：

![](img/9b1932f39c4ca4cfcc81c02125104271_234.png)

相机可以看到的区域（称为相机视图）其中心（即其原点）位于游戏世界坐标 (-486, -330)。由于相机看到的内容显示在玩家的屏幕上，“相机”坐标与“像素”坐标相同。要找到松鼠的像素坐标（即它们出现的位置），将松鼠的游戏坐标减去摄像机的原点。

所以，左侧的松鼠游戏坐标为 (-384, -84)，但在屏幕上的像素坐标为 (102, 246)。对于 X 坐标，-384 - (-486) = 102；对于 Y 坐标，-84 - (-330) = 246。）当我们对另外两只松鼠进行相同的计算时，发现它们位于屏幕范围之外。这就是为什么它们没有出现在相机视图中。

## 活跃区域 (Active Area)

“活跃区域”只是我用的一个名称，用来描述相机查看的游戏区域，加上相机周围的区域：

![](img/9b1932f39c4ca4cfcc81c02125104271_234_1.png)

某物是否在活跃区域将在本文的 `isOutsideArea()` 函数中解释。当我们创建新的松鼠或草地对象时，我们不希望它们在相机视图内创建，因为它们会凭空出现。

但也不希望距离相机太远的地方创建，因为它们可能会回到相机视图中。活跃区域内相机外可以安全地创建松鼠和草地对象。

此外，当松鼠和草地对象处于活跃边界时，它们足够远，不会占用更多内存。如果你玩过任天堂上的超级马里，有一个很好的 YouTube 视频解释了超级马里的相机系统。你可以在 http://invpy.com/mariocamera 找到这个视频。

# 跟踪游戏世界物体的位置

```
grassObjs = [] # 存储游戏中所有的草地对象

110. squirrelObjs = [] # 存储所有非玩家松鼠

111. # 存储玩家对象：

112. playerObj = {'surface': pygame.transform.scale(L_SQUIR_IMG, (STARTSIZE, STARTSIZE)),

113. 'facing': LEFT,

114. 'size': STARTSIZE,

115. 'x': HALF_WINWIDTH,

116. 'y': HALF_WINHEIGHT,

117. 'bounce': 0,

118. 'health': MAXHEALTH}

120. moveLeft = False

121. moveRight = False

122. moveUp = False

123. moveDown = False
```

`grassObjs` 变量持有游戏中所有草地对象的列表。当创建新的草地对象时，它们被添加到此列表中。当草地对象被删除时，它们从列表中移除。`squirrelObjs` 变量和敌人松鼠对象也是如此。

`playerObj` 变量不是列表，而是字典本身。

第 120 到 123 行的变量跟踪哪些方向键（或 WASD 键）正被按住，就像之前的几个游戏程序一样。

向作者提问邮件：`al@inventwithpython.com`

## 开始时一些草地

```
125. # 在屏幕上从随机草地图像开始

126. for i in range(10):
```
