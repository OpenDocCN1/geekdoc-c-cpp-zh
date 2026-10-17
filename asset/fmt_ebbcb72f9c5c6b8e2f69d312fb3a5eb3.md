
```python
return bbb

def t(vv, uu):

    ww = []

    for i in range(0, len(uu)):

        ww.append(uu[i])

    return ww

def aa(bb, ee):

    return (bb * 50 + 70, ee * 50 + 65)

def m(x, y):

    for bb in range(10):

        for ee in range(7):

            oo, ddd = aa(bb, ee)

            aaa = pygame.Rect(oo, ddd, 40, 40)

            if aaa.collidepoint(x, y):

                return (bb, ee)

    return (None, None)

def w(ss, tt, bb, ee):

    oo, ddd = aa(bb, ee)

    if ss == 'a':

        pygame.draw.circle(b, tt, (oo + 20, ddd + 20), 15)

        pygame.draw.circle(b, (60, 60, 100), (oo + 20, ddd + 20), 5)

    elif ss == 'b':

        pygame.draw.rect(b, tt, (oo + 10, ddd + 10, 20, 20))

    elif ss == 'c':

        pygame.draw.polygon(b, tt, [(oo + 20, ddd), (oo + 40, ddd), (oo + 20, ddd + 40)])

    elif ss == 'd':

        for i in range(0, 4):

            pygame.draw.line(b, tt, (oo, ddd + i), (oo + i, ddd))

            pygame.draw.line(b, tt, (oo + i, ddd + 39), (oo + 39, ddd))

    elif ss == 'e':

        pygame.draw.ellipse(b, tt, (oo + 10, ddd + 10, 40, 20))

def s(bbb, bbb, ee):

    return bbb[bb][ee][0], bbb[bb][1]

def dd(bbb, boxes):

    for box in boxes:

        oo, ddd = aa(box[0], box[1])

        pygame.draw.rect(b, (60, 60, 100), oo, ddd, 40, 40)

        ss, tt = s(bbb, box[0], box[1])

        w(ss, tt, box[0], box[1])

        if gg > 0:

            pygame.draw.rect(b, (255, 255, 255), oo, ddd, gg, 40)

    pygame.display.update()

    a.tick(30)

def o(bbb, cc):

    for gg in range(40, -8, -8):

        ddbb(bbb, cc, gg)

def ddbb(bbb, ff, gg):

    # 原文中此处未给出 ddbb 的实现，此处为占位

    pass

def p(bbb, ff):

    for gg in range(0, 48, 8):

        ddbb(bbb, ff, gg)

def f(bbb, pp):

    for bb in range(10):

        for ee in range(7):

            oo, ddd = aa(bb, ee)

            if not pp[bb][ee]:

                pygame.draw.rect(b, (255, 255, 255), oo, ddd, 40, 40)

            else:

                ss, tt = s(bbb, bb, ee)

                w(ss, tt, bb, ee)
```

```python
def n(bb, ee):
    oo, ddd = aa(bb, ee)
    pygame.draw.rect(b, (0, 0, 255), (oo - 5, ddd - 5, 50, 50), 4)
def g(bbbb):
    mm = d(False)
    boxes = []
    for x in range(10):
        for y in range(7):
            boxes.append((x, y))
    random.shuffle(boxes)
    kk = t(8, boxes)
def f(bbb, mm):
    for nn in kk:
        o(bbb, nn)
        p(bbb, nn)
```

以及同一个程序中的不同系统）为了保持本书的简短，将不再再次解释它们。

为了理解代码是如何运行的，可以尝试的一种方法是通过注释掉随机行来故意破坏它。对某些行执行此操作可能会导致语法错误，使得脚本完全无法运行。但注释掉其他行可能会导致奇怪的 Bug 和其他酷炫的效果。尝试这样做，并弄清楚为什么程序会出现那些 Bug。

这也是你能够向程序中添加自己的“秘密外挂”或黑客功能的第一步。通过打破程序的正常运行，你可以学习如何将其改变为某些奇妙的效果（例如秘密地给你提供如何解谜的提示）。请尽管进行实验。如果你想再次玩普通游戏，可以随时将未修改的源代码保存到另一个文件中。

事实上，如果你想练习修复 Bug，这个游戏的源代码有几个带有微小 Bug 的版本。你可以从 http://invpy.com/buggy/memorypuzzle 下载这些带有错误的版本。尝试运行程序以找出 Bug 是什么，以及程序为什么会那样运行。

向作者发送邮件提问：`al@inventwithpython.com`

## 第 4 章 – 数字滑块游戏

![](img/9b1932f39c4ca4cfcc81c02125104271_94_0.png)

### 如何玩滑块游戏

游戏是一个 4x4 的网格，包含十五块滑块（从左到右编号 1 到 15）和一个空白区域。滑块初始处于随机位置，玩家必须滑动滑块，直到滑块恢复原始顺序。

### 滑块游戏的源代码

可以从 http://invpy.com/slidepuzzle.py 下载此源代码。如果你收到任何错误消息，请查看错误消息中提到的行，并检查你的代码是否有任何类型错误。你也可以将代码复制并粘贴到 http://invpy.com/slidepuzzle 的网页表单中，查看你的代码与书中代码之间的差异。

```python
1. # Slide Puzzle
2. # Al Schweigart al@inventwithpython.com
3. # http://inventwithpython.com/pygame
4. # Creative Commons BY-NC-SA 3.0 US
5.
6. import pygame, sys, random
7. from pygame.locals import *
8.
9. # Create the constants (go ahead and experiment with different values)
10. BOARDWIDTH = 4 # number of columns in the board
11. BOARDHEIGHT = 4 # number of rows in the board
12. TILESIZE = 80
13. WINDOWWIDTH = 640
14. WINDOWHEIGHT = 480
15. FPS = 30
16. BLANK = None
17.
18. #             R G B
19. BLACK = (0, 0, 0)
20. WHITE = (255, 255, 255)
21. BRIGHTBLUE = (0, 50, 255)
22. DARTURQUISE = (3, 54, 73)
23. GREEN = (0, 204, 0)
24.
25. BGCOLOR = DARKTURQUISE
26. TILECOLOR = GREEN
27. TEXTCOLOR = WHITE
28. BORDERCOLOR = BRIGHTBLUE
29. BASICFONSIZE = 20
30.
31. BUTTONCOLOR = WHITE
32. BUTTONTEXTCOLOR = BLACK
33. MESSAGECOLOR = WHITE
34.
35. XMARGIN = int((WINDOWWIDTH - (TILESIZE * BOARDWIDTH + (BOARDWIDTH - 1)) / 2))
36. YMARGIN = int((WINDOWHEIGHT - (TILESIZE * BOARDHEIGHT + (BOARDHEIGHT - 1)) / 2))
37.
38. UP = 'up'
39. DOWN = 'down'
40. LEFT = 'left'
41. RIGHT = 'right'
42.
43. def main():
44.     global FPSCLOCK, DISPLAYFACE, BASICFONT, RESET_SURF, RESET_RECT,
45.     NEW_SURF, NEW_RECT, SOLVE_SURF, SOLVE_RECT
46.
47.     pygame.init()
48.     FPSCLOCK = pygame.time.Clock()
49.     DISPLAYFACE = pygame.display.set_mode((WINDOWWIDTH, WINDOWHEIGHT))
50.     pygame.display.set_caption('Slide Puzzle')
51.     BASICFONT = pygame.font.Font('freesansfont.ttf', BASICSIZE)
52.
53.     # Store option buttons and their rectangles in OPTIONS.
54.     RESET_SURF, RESET_RECT = makeText('Reset', TEXTCOLOR, TILECOLOR,
55.     WINDOWWIDTH - 120, WINDOWHEIGHT - 90)
```

## 第 4 章 – 滑块游戏
