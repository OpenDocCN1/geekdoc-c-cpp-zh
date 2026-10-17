
```
sq['width'] = (generalSize + random.randint(0, 10)) * multiplier

sq['height'] = (generalSize + random.randint(0, 10)) * multiplier

sq['x'], sq['y'] = getRandomOffsetCameraPos(camerax, cameray)

sq['move_x'] = getRandomVelocity()

sq['move_y'] = getRandomVelocity()
```

创建松鼠游戏对象与创建草游戏对象相似。每个松鼠的数据也存储在字典中。宽度和高度在第 360 行和 361 行设置为随机大小。`generalSize` 变量用于确保每个的宽度和高度

# 第 8 章 – 松鼠吃松鼠

松鼠之间并没有区别。否则，使用完全随机的数字作为宽度和高度可能会得到高而瘦的松鼠或非常矮宽的松鼠。松鼠的宽度和高度是这个基础尺寸，并加上一个 0 到 10 之间的随机数（以产生细微变化），然后乘以倍率变量。

松鼠的原始 XY 坐标位置将是一个相机看不见的随机位置，以防止松鼠直接在屏幕上“砰”地一下出现。

速度和方向也由 `getRandomVelocity()` 函数随机选择。

## 翻转松鼠图像

```
if sq['movex'] < 0: # 松鼠面向左
    sq['surface'] = pygame.transform.scale(SQUIR_IMG, (sq['width'],
    sq['height'])
else: # 松鼠面向右
    sq['surface'] = pygame.transform.scale(SQUIR_IMG, (sq['width'],
    sq['height'])
    sq['bounce'] = 0
    sq['bounceerate'] = random.randint(10, 18)
    sq['bounceheight'] = random.randint(10, 50)
    return sq
```

`L_SQUIR_IMG` 和 `R_SQUIR_IMG` 常量包含带有面向左和面向右松鼠图像的 `Surface` 对象。新的 `Surface` 对象将使用 `pygame.transform.scale()` 函数创建，分别匹配 `sq['width']` 和 `sq['height']` 中的松鼠宽度和高度。

之后，会随机生成三个与跳跃相关的数值（`sq['bounce']` 除 0，因为松鼠总是从跳跃开始，且在第 372 行返回字典）。

## 创建草地数据结构

```
def makeNewGrass(camerax, camay):
    gr = {}
    gr['grassImage'] = random.randint(0, len(GRASSIMAGES) - 1)
    gr['width'] = GRASSIMAGES[0].get_width()
    gr['height'] = GRASSIMAGES[0].get_height()
    gr['x'], gr['y'] = getRandomOffCameraPos(camerax, camay,
    gr['rect'] = pygame.Rect(gr['x'], gr['y'], gr['width'],
    gr['height'])
    return gr
```

草地游戏对象是字典，具有常用的 `'x'`、`'y'`、`'width'`、`'height'` 和 `'rect'` 键，还有一个 `'grassImage'` 键，其值是从 0 到小于 `GRASSIMAGES` 列表长度的数字。这个数字将决定草地游戏对象包含的内容。例如，如果草地对象的 `'grassImage'` 键值为 3，那么它将使用存储在 `GRASSIMAGES[3]` 中的 `Surface` 对象作为图像。

## 检查是否在活动区域

```
def isOutsideActiveArea(camax, cameray, obj):
    # 如果 camerax 和 cameray 超过窗口边缘
    # 半个宽度长度，则返回 False。
    boundsLeftEdge = camerax - WINWIDTH
    boundsTopEdge = cameray - WINHEIGHT
    boundsRect = pygame.Rect(boundsLeftEdge, boundsTopEdge, WINWIDTH * 3,
    WINHEIGHT * 3)
    objRect = pygame.Rect(obj['x'], obj['y'], obj['width'], obj['height'])
    return not boundsRect.colliderect(objRect)
```

如果对象位于由 `camerax` 和 `cameray` 参数决定的“活动区域”之外，`OutsideActiveArea()` 将返回 `True`。记住，活动区域是相机周围的一个区域，大小与相机视图相同（宽度和高度由 `WINWIDTH` 和 `WINHEIGHT` 设置），如下：

![](img/9b1932f39c4ca4cfcc81c02125104271_257_0.png)

我们可以通过传递 `camerax - WINWIDTH` 作为左边缘、`cameray - WINHEIGHT` 作为顶边缘值，然后使用 `WINWIDTH * 3` 和 `WINHEIGHT * 3` 作为宽度和高度，创建一个表示活动区域的 `Rect`。一旦我们把活动区域表示为 `Rect`，我们就可以使用 `colliderect()` 来判断 `obj` 参数中的对象是否与（即属于）活动区域 `Rect` 对象碰撞。

向作者提问邮件：`al@inventwithpython.com`

由于玩家松鼠、敌人松鼠和草地对象都具有 `'x'`、`'y'`、`'width'` 和 `'height'` 键，`isOutsideActiveArea()` 代码可以处理任何类型的游戏对象。

```
if __name__ == '__main__':
    main()
```
