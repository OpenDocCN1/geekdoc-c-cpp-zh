
## 13 其他函数

你会在本游戏中使用大量函数。现在可以先列出其中一些，稍后在代码中定义它们。使用 pass 可以确保 Python 暂时不执行任何内容。将以下代码输入到第 10 步所添加内容的下方。

```python
def new_flower():
    pass

def add_flowers():
    pass

def check_wilt_times():
    pass

def wilt_flower():
    pass

def check_flower_collision():
    pass

def reset_cow():
    pass

def update():
    pass
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_163_0.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_163_1.png)

## 14 在花园中移动

目前，奶牛会出现在屏幕上，但不会做任何事。添加一些代码，让你可以移动奶牛。将 def update() 下方的 pass 一词替换为以下代码。

当按下**右**方向键时，这会让奶牛向右移动五个像素。

```python
def update():
    global score, game_over, fangflower_collision
    global flower_list, fangflower_list, time_elapsed
    if not game_over:
        if keyboard.left and cow.x > 0:
            cow.x -= 5
        elif keyboard.right and cow.x < WIDTH:
            cow.x += 5
        elif keyboard.up and cow.y > 150:
            cow.y -= 5
        elif keyboard.down and cow.y < HEIGHT:
            cow.y += 5
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_163_2.png)

## 15 另一次测试

测试你刚更新的代码，确保它正确。保存你的 IDLE 文件，并从命令行运行它。现在你应该可以在屏幕上移动奶牛了。

```text
pgzr run
```

在命令提示符或终端窗口中输入这条命令，然后拖放 garden.py 文件。

> 让我们查看第 24–25 页，了解具体做法。

![](img/3188b147f991a51de14dcd2bb4b4c42e_164_0.png)

## 16 添加一朵花

在这一步中，你将创建一个花朵 Actor 供奶牛浇水，并将其添加到 flower_list 的末尾。你还会将值 happy 添加到 wilted_list 的末尾，该列表保存每朵花已经枯萎的时间。happy 值会让程序知道这朵花还没有枯萎。将 new_flower() 函数中的 pass 替换为以下代码。

```python
def new_flower():
    global flower_list, wilted_list
    flower_new = Actor("flower")
    flower_new.pos = randint(50, WIDTH - 50), randint(150, HEIGHT - 100)
    flower_list.append(flower_new)
    wilted_list.append("happy")
    return
```

这些是该函数使用的全局变量。

这一行创建一个新的花朵 Actor。

这一行设置新花朵的位置。

这会让程序知道这朵花没有枯萎。

这会将新花朵添加到花朵列表中。

## 17 向花园添加更多花

只有一朵花需要浇水会让游戏太简单。你需要添加一些代码，每隔四秒创建一朵新花，让奶牛忙起来。添加以下代码，替换 def add_flowers() 下方的 pass 一词。

```python
def add_flowers():
    global game_over
    if not game_over:
        new_flower()
        clock.schedule(add_flowers, 4)
    return
```

这一行调用 new_flower() 函数来创建一朵新花。

这会每隔四秒添加一朵新花。

> 我想我需要一个更大的花园！

![](img/3188b147f991a51de14dcd2bb4b4c42e_164_1.png)

## 18. 开始添加花朵

尽管 `add_flowers()` 会每隔四秒安排一次对自身的调用，但你需要先在程序中调用它一次来启动这个过程。将第 13 步中上方以黑色显示的那一行添加进去（如果已更新！）。保存并运行代码，检查花朵是否开始出现！

```python
def reset_cow():
    pass

add_flowers()

def update():
```

## 19. 盛开的花园

如果代码中没有错误，你会看到屏幕上每隔四秒出现一朵新花。这是 20 秒后屏幕的样子。使用方向键移动奶牛。

![](img/3188b147f991a51de14dcd2bb4b4c42e_165_0.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_165_1.png)

## 20. 给花浇水

该让奶牛给枯萎的花浇水了。我们来添加一些代码，让玩家按下**空格键**时奶牛会向花朵洒水。代码还会检查奶牛是否站在一朵花旁边。将以下代码添加到 `update()` 函数中。

![](img/3188b147f991a51de14dcd2bb4b4c42e_165_2.png)

```python
global flower_list, fangflower_list, time_elapsed
if not game_over:
    if keyboard.space:
        cow.image = "cow-water"
        clock.schedule(reset_cow, 0.5)
        check_flower_collision()
        if keyboard.left and cow.x > 0:
            cow.x -= 5
```

这会检查是否按下了**空格键**。

这会将奶牛图像更改为水从浇水壶中流出的图像。

这会在半秒后重置奶牛的图像。

这一行会检查奶牛是否在一朵花旁边。

## 21 停止浇水

第 20 步的代码使用了两个你尚未编写的函数——`reset_cow()` 和 `check_flower_collision()`。我们来添加代码，将奶牛使用浇水壶的图像改回只是拿着浇水壶的版本。将第 13 步中 `reset_cow()` 函数下方的 `pass` 一词替换为下方以黑色显示的代码。

```python
def reset_cow():
    global game_over
    if not game_over:
        cow.image = "cow"
    return

add_flowers()
```

如果游戏尚未结束，这段代码就会运行。

这会将奶牛的图像改回原来的图像。

> 呃……我觉得水已经够了。

![](img/3188b147f991a51de14dcd2bb4b4c42e_166_0.png)

## 22 精准得分！

你需要让代码在按下**空格键**时检查奶牛是否靠近一朵花。如果是，这朵花就会被浇水，并且它在 `wilted_list` 中的“花朵枯萎后经过的时间”值会被设置为 happy。为此，你将使用 Pygame Zero 内置的 `colliderect()` 函数来检查花朵和奶牛是否发生碰撞或彼此相邻。将第 13 步中 `def check_flower_collision()` 下方的 `pass` 替换为如下所示的代码。

```python
def check_flower_collision():
    global cow, flower_list, wilted_list
    index = 0
    for flower in flower_list:
        if (flower.colliderect(cow) and
            flower.image == "flower-wilt"):
            flower.image = "flower"
            wilted_list[index] = "happy"
            break
        index = index + 1
    return
```

这些是你将在该函数中使用的全局变量。

这个变量帮助程序按顺序遍历列表。

这段代码会循环遍历列表中的所有花朵。

如果奶牛与你正在查看的这朵花相邻，就会应用这个条件。

这会将枯萎花朵的图像改回原始版本。

这一行会停止程序计算花朵已经枯萎了多长时间。

这一行会更新 index 的值，以便程序遍历列表。

这会停止循环继续检查其他花朵。

## 23 让一朵花枯萎

该给你照料花园的奶牛一点挑战了。奶牛不再每三秒让一朵随机的花枯萎，而是必须冲到枯萎的花那里给它浇水。将第 13 步中 `wilt_flower()` 函数里的 `pass` 一词替换为以下代码。

|  | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| `flower_list` | 🌸 | 🌸 | 🌸 | 🌸 |
| `wilted_list` | happy | 枯萎的花 | happy | 枯萎的花 |

这两个列表在相同索引编号处存储某一朵特定花朵的信息。

```python
def wilt_flower():
    global flower_list, wilted_list, game_over
    if not game_over:
        if flower_list:
            rand_flower = randint(0, len(flower_list) - 1)
            if flower_list[rand_flower].image == "flower":
                flower_list[rand_flower].image = "flower-wilt"
                wilted_list[rand_flower] = time.time()
        clock.schedule(wilt_flower, 3)
    return
```

这一行会将 `wilted_list` 中这朵花的时间重置为当前时间。

这会在三秒后再次安排调用 `wilt_flower()`。

这一行会在花朵列表中生成一个随机索引。

这会检查该索引处的花朵是否已经枯萎。

这会将花朵图像设置为枯萎花朵的图像。

## 24 不开心的花园！

接下来，你需要检查是否有任何花朵已经枯萎超过十秒。如果有，花园就会不开心，游戏也就结束了！复制第 13 步中的 `check_wilt_times()`，并将 `pass` 替换为这里显示的代码。

```python
def check_wilt_times():
    global wilted_list, game_over, garden_happy
    if wilted_list:
        for wilted_since in wilted_list:
            if (not wilted_since == "happy"):
                time_wilted = int(time.time() - wilted_since)
                if (time_wilted > 10.0):
                    garden_happy = False
                    game_over = True
                    break
    return
```

这会检查 `wilted_list` 中是否有任何项。

这段代码会遍历 `wilted_list` 中的每一项。

这些行会检查花朵是否已经枯萎，并计算它已经枯萎了多长时间。

这一行会检查花朵是否已经枯萎超过十秒。

