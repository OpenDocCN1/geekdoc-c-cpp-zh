
224. # `alpha` 表示透明度。255 是不透明，0 是不可见的。

225. `checkBoxQuit()`

226. `flashSurf.fill((r, g, b, alpha))`

17.

18. # R G B

19. `WHITE = (255, 255, 255)`

20. `BLACK = (0, 0, 0)`

21. `BRIGHTRED = (255, 0, 0)`

22. `RED = (155, 0, 0)`

23. `BRIGHTGREEN = (0, 255, 0)`

24. `GREEN = (0, 155, 0)`

25. `BRIGHTBLUE = (0, 0, 255)`

26. `BLUE = (0, 0, 155)`

27. `BRIGHTYELLOW = (255, 255, 0)`

28. `YELLOW = (155, 155, 0)`

29. `DARKGRAY = (40, 40, 40)`

30. `bgColor = BLACK`

31.

32. `XMARGIN = int((WINDOWWIDTH - (2 * BUTTONSIZE) - BUTTONSIZE) / 2)`

33. `YMARGIN = int((WINDOWHEIGHT - (2 * BUTTONSIZE) - BUTTONSIZE) / 2)`

在这里我们使用了常用的常量，用于稍后修改的内容，例如四个按钮的大小、按钮的阴影颜色（当按钮亮起时使用亮色）以及玩家在游戏超时之前点击序列中下一个按钮可用的时间。

## 设置按钮

- 35. # 四个按钮的 Rect 对象
- 36. `YELLOWRECT = pygame.Rect(XMARGIN, YMARGIN, BUTTONSIZE, BUTTONSIZE)`
- 37. `BLUERECT = pygame.Rect(XMARGIN, YMARGIN + BUTTONSIZE, BUTTONSIZE, BUTTONSIZE)`, `YMARGIN = pygame.Rect(XMARGIN, YMARGIN, BUTTONSIZE, BUTTONSIZE)`
- 38. `REDRECT = pygame.Rect(XMARGIN, YMARGIN + BUTTONSIZE, BUTTONSIZE, BUTTONSIZE)`
- 39. `GREENRECT = pygame.Rect(XMARGIN, YMARGIN + BUTTONSIZE, BUTTONSIZE, BUTTONSIZE)`, `BUTTONSIZE + BUTTONSIZE = pygame.Rect(..., BUTTONSIZE, BUTTONSIZE, BUTTONSIZE)`

就像滑动谜游戏中的“重置”、“解决”和“新游戏”按钮一样，Simulate 游戏也有四个矩形对象，用于处理玩家点击这些区域内部的情况。程序需要为每个按钮都准备一个 Rect 对象，以便在它们上调用 `collidepoint()` 方法。第 36 到 39 行根据相应的坐标大小设置了这些 Rect 对象。

## main() 函数

``` 
41. def main():
```

``` 
42. global FPSCLOCK, DISPLAY, BASICFONT, BEEEP1, BEEEP2, BEEEP3, BEEP4
```

``` 
43. pygame.init()
44. FPSCLOCK = pygame.time.Clock()
45. DISPLAY = pygame.display.set_mode((WINDOWWIDTH, WINDOWHEIGHT))
46. pygame.display.set_caption('Simulate')
```

``` 
48.
49. BASICFONT = pygame.font.Font('freesansold.ttf', 16)
50.
51. infoSource = BASICFONT.render('Match the pattern by clicking on the
52. button or using the Q, W, A, S.keys()', 1, DARKGRAY)
53. infoRect = infoSource.get_rect()
54. infoRect.topleft = (10, WINDOWHEIGHT - 25)
55. # 加载声音文件
56. BEEP1 = pygame.mixer.Sound('beep1.ogg')
57. BEEP2 = pygame.mixer.Sound('beep2.ogg')
58. BEEP3 = pygame.mixer.Sound('beep3.ogg')
59. BEEP4 = pygame.mixer.Sound('beep4.ogg')
```

`main()` 函数将实现程序块并在需要时调用其他函数。调用通常的设置函数来初始化库、创建 Clock 对象、创建窗口并创建一个用于在窗口上显示分数和说明的 Font 对象。通过这些函数调用创建的对象将存储在全局变量中，以便在其他函数中使用。但它们本质上是常量，因为它们的值从未被改变。

第 55 到 58 行将加载声音，以便 Simulate 在玩家点击每个按钮时播放效果。`pygame.mixer.Sound()` 构造函数将返回一个 Sound 对象，将其存储在变量 `BEEP1` 到 `BEEP4` 中，这些变量在第 42 行已变为全局变量。

## 程序中的一些局部变量

``` 
60. # 为新游戏初始化一些变量
61. pattern = [] # 存储颜色模式
62. currentStep = 0 # 玩家必须按下一个颜色
63. lastClickTime = 0 # 玩家上次点击按钮的时间戳
64. score = 0
65. # 当为 False 时，模式正在播放。当为 True 时，等待
66. 玩家点击彩色按钮：
67. waitingForInput = False
```

`pattern` 将是一个颜色值的列表（`YELLOW`、`RED`、`BLUE` 或 `GREEN`）。

## 绘制并处理输入

```68. while True: # 主循环
69. clickedButton = None # 在每次迭代开始时
70. DISPLAY.fill(bgColor) # 重新绘制整个 Surface
71. drawButtons()
72.
73. scoreSurf = BASICFONT.render('Score: ' + str(score), 1, WHITE)
74. scoreRect = scoreSurf.get_rect()
75. scoreRect.topleft = (WINDOWWIDTH - 100, 10)
76. DISPLAY.blit(scoreRect, scoreRect)
77.
78. DISPLAY.blit(infoSurf, infoRect)
```

## 检查鼠标点击

| 80. | `checkForQuit()` |
| 81. | `for event in pygame.event.get(): # 事件处理循环` |
| 82. | `if event.type == MOUSEBUTTONUP:` |
| 83. | `mousex, mousey = event.pos` |
| 84. | `clickedButton = getMouseClicked(mouse, mousey)` |

第 80 行检查任何 QUIT 事件，第 81 行是处理循环的开始。任何鼠标点击的 XY 坐标将存储在变量中。如果是按钮，我们的 `getMouseClicked` 函数将返回点击按钮的颜色对象（否则返回 None）。

## 检查键盘按下

| 85. | `elif event.type == KEYDOWN:` |
| 86. | `if event.key == K_q:` |
| 87. | `clickedButton = YELLOW` |
| 88. | `elif event.key == K_w:` |
| 89. | `clickedButton = BLUE` |
| 90. | `elif event.key == K_a:` |
| 91. | `clickedButton = RED` |
| 92. | `elif event.key == K_s:` |
| 93. | `clickedButton = GREEN` |

第 85 到 93 行检查任何 KEYDOWN 事件（当用户按下键时创建）。Q、W、A、S 键对应于按钮，因为它们在键盘上排列成正方形。

我们可以通过将 `clickedButton` 变量设置为常量变量 `YELLOW` 的值来实现这一点。我们可以对其他三个键执行同样的操作。这样一来，用户可以使用鼠标或键盘来玩 Simulate（模拟游戏）。

## 游戏循环的两种状态

``` 
97.  if not waitingForInput:
98.      # play the pattern
99.      pygame.display.update()
100.     pygame.time.wait(1000)
101.     pattern.append(random.choice((YELLOW, BLUE, RED, GREEN)))
102.     for button in pattern:
103.         flashButtonAnimation(button)
104.         pygame.time.wait(FLASHDELAY)
105.     waitingForInput = True
```

程序处于两种“模式”或“状态”。当 `waitingForInput` 为 `False` 时，程序将显示模式动画。当 `waitingForInput` 为 `True` 时，程序将等待用户选择按钮。

第 97 到 105 行涵盖程序显示模式动画的情况。由于这是游戏开始或玩家完成一个模式时发生的，第 101 行将向 `pattern` 列表添加一种颜色，使模式增加一步。第 102 到 104 行遍历 `pattern` 列表中的每个值，并调用 `flashButtonAnimation()` 使该按钮闪烁。在闪完 `pattern` 列表中的所有按钮后，程序将 `waitingForInput` 变量设置为 `True`。

## 判断玩家是否按了正确的按钮

``` 
106.     else:
107.         # wait for the player to enter buttons
108.     if clickedButton and clickedButton == pattern[currentStep]:
109.         # pushed the correct button
110.         flashButtonAnimation(clickedButton)
111.         currentStep += 1
112.         lastClickTime = time.time()
```

如果 `waitingForInput` 为 `True`，则执行第 106 行 `else` 中的代码。第 108 行检查玩家在本次游戏循环的本次迭代中是否点击了按钮，以及该按钮是否正确。`currentStep` 变量跟踪玩家下一个应该点击的按钮在 `pattern` 列表中的索引。

http://inventwithpython.com/pygame

例如，如果 `pattern` 被设置为 `[YELLOW, RED, RED]` 且 `currentStep` 变量被设置为 `0`（就像玩家首次开始游戏时那样），那么玩家正确的按钮将是 `pattern[0]`（黄色按钮）。

如果玩家点击了正确的按钮，我们希望通过调用 `flashButtonAnimation()` 来闪烁玩家点击的按钮，然后将 `currentStep` 增加到下一步，最后将 `lastClickTime` 更新为当前时间。`time.time()` 函数返回自 1970 年 1 月 1 日以来的秒数浮点值，因此我们可以跟踪时间。

``` 
currentStep == len(pattern):
# pushed the last button in the pattern
changeBackgroundAnimation()
score += 1
waitingForInput = False
currentStep = 0 # reset back to first step
```

第 114 到 119 行位于第 106 行开始的 `else` 语句内部。如果执行位于 `else` 语句中，我们就知道玩家点击了按钮，而且它也是正确的按钮。第 114 行通过检查 `currentStep` 中存储的整数是否等于 `pattern` 列表中的值数量，判断这是否为模式列表中的最后一个正确按钮。

如果是 `True`，我们希望通过调用 `changeBackgroundAnimation()` 来更改背景颜色。这是让玩家知道他们正确输入模式的一种简单方法。分数加1，`currentStep` 重置为 0，并将 `waitingForInput` 变量设置为 `False`，这样在游戏循环的下次迭代中，代码将向 `pattern` 列表添加新颜色并闪烁按钮。

``` 
elif (clicked and clickedButton != pattern[currentStep]) or (currentStep != 0 and time.time() - TIMEOUT > lastClickTime):
```

如果玩家没有点击正确的按钮，第 121 行的 `else` 语句处理玩家点击了错误按钮或玩家等待点击按钮过长的情况。无论哪，我们都希望显示“游戏结束”并开始新游戏。

`else` 语句中的 `(clickedButton and clickedButton != pattern[currentStep])` 部分检查是否点击了按钮且按钮是错误的。你可以将其与第 108 行的语句条件 `clickedButton and clickedButton == pattern[currentStep]` 进行对比，如果玩家点击了按钮且该按钮是正确的，则该条件为 `True`。

给作者的邮件：`al@inventwithpython.com`

## 第5章 – Simulate 121

第 121 行 `elif` 条件的另一部分是 `(currentStep != 0 and time.time() - TIMEOUT > lastClickTime)`。这负责确保玩家没有“超时”。注意，该条件的这部分由 `and` 关键字连接两个表达式组成。这意味着 `and` 的两边都需要评估为 `True`。

为了发生“超时”，不能是玩家的第一次点击。但一旦他们开始点击按钮，就必须足够快速地点击按钮，直到输入整个模式（如果他们点击了错误的模式并导致“游戏结束”）。如果 `currentStep` 不为 0，我们就知道玩家没有超时。

## Epoch Time

如果玩家点击了正确的按钮，我们希望通过调用 `flashButtonAnimation()` 来闪烁玩家点击的按钮，然后将 `currentStep` 增加到下一步，最后将 `lastClickTime` 更新为当前时间。`time.time()` 函数返回自 1970 年 1 月 1 日以来的秒数浮点值，因此我们可以跟踪时间。

``` 
currentStep == len(pattern):
# pushed the last button in the pattern
changeBackgroundAnimation()
score += 1
waitingForInput = False
currentStep = 0 # reset back to first step
```

第 114 到 119 行位于第 106 行开始的 `else` 语句内部。如果执行位于 `else` 语句中，我们就知道玩家点击了按钮，而且它也是正确的按钮。第 114 行通过检查 `currentStep` 中存储的整数是否等于 `pattern` 列表中的值数量，判断这是否为模式列表中的最后一个正确按钮。

如果是 `True`，我们希望通过调用 `changeBackgroundAnimation()` 来更改背景颜色。这是让玩家知道他们正确输入模式的一种简单方法。分数加1，`currentStep` 重置为 0，并将 `waitingForInput` 变量设置为 `False`，这样在游戏循环的下次迭代中，代码将向 `pattern` 列表添加新颜色并闪烁按钮。

``` 
elif (clicked and clickedButton != pattern[currentStep]) or (currentStep != 0 and time.time() - TIMEOUT > lastClickTime):
```
