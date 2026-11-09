

### 22 生成移动序列

接下来，你需要编写一个函数，生成一系列动作并显示在屏幕上。你需要使用一个 for 循环生成 4 个 0 到 3 之间的随机数，每个数字代表你在第 15 步设置的一个动作。每次生成的动作都会被添加到两个列表中——move_list 和 display_list。用以下代码替换第 13 步 `def generate_moves()` 下方的 `pass`。

```python
def generate_moves():
    global move_list, dance_length, count
    global show_countdown, say_dance
    count = 4
    move_list = []
    say_dance = False
    for move in range(0, dance_length):
        rand_move = randint(0, 3)
        move_list.append(rand_move)
        display_list.append(rand_move)
        show_countdown = True
        countdown()
    return
```

这行代码会随机将 0、1、2 或 3 赋值给变量 `rand_move`。

这行代码将每个新动作添加到动作列表的末尾。

这行代码告诉 `draw()` 函数显示 `count` 的值，从而实现倒计时。

### 23 游戏结束

如果玩家犯了错误，你需要弹出一条“GAME OVER!”（游戏结束）消息。你可以通过在 `if not game_over` 语句中添加一个 `else` 分支来实现这一点。这样，如果 `game_over` 变为 `True`，舞者和方块将消失，取而代之的是“GAME OVER!”消息。将以下代码添加到 `draw()` 函数中，紧邻 `return` 语句上方。

以下代码在 `game_over` 为 `True` 时运行。

```python
    if show_countdown:
        screen.draw.text(str(count), color="black",
                         topleft=(CENTER_X - 8, 150), fontsize=60)
    else:
        screen.clear()
        screen.blit("stage", (0, 0))
        screen.draw.text("Score: " +
                         str(score), color="black",
                         topleft=(10, 10))
        screen.draw.text("GAME OVER!", color="black",
                         topleft=(CENTER_X - 130, 220), fontsize=60)
    return
```

这行代码在左上角绘制得分。

这行代码在屏幕中央用黑色绘制“GAME OVER!”。

![](img/3188b147f991a51de14dcd2bb4b4c42e_150_0.png)

### 24 生成测试

是时候测试你的新函数了，看看它们是否正常工作。在第 13 步中 `update()` 定义的上方添加对 `generate_moves()` 的调用。保存文件并运行。你应该会看到一个倒计时出现，然后你的舞者展示四个动作的序列。完成后应显示“Dance!”字样，但先不要开始跳舞！你还需要添加检查玩家输入动作是否正确的代码。

```python
generate_moves()

def update():
    pass
```

全局变量 `current_move` 用于标识你当前正在处理哪个动作。

### 25 获取下一个动作

你需要一种方法来遍历计算机生成的动作列表。这样你可以将玩家输入的第一个动作与计算机列表中的第一个动作进行比较，然后依次比较整个列表。你还需要知道何时到达列表末尾。为此，使用全局变量 `current_move` 来标识当前正在处理的动作。用以下代码替换第 13 步 `def next_move()` 下的 `pass`。

```python
def next_move():
    global dance_length, current_move, moves_complete
    if current_move < dance_length - 1:
        current_move = current_move + 1
    else:
        moves_complete = True
        return
```

如果还有剩余动作需要检查，此条件为 `True`。

这行代码将 `current_move` 移到下一个动作。

如果没有更多动作需要检查，则运行 `else` 块。

![](img/3188b147f991a51de14dcd2bb4b4c42e_151_0.png)

### 26 每个动作得分

现在你需要向 `on_key_up()` 函数添加一些代码。当玩家按下按键时，游戏需要检查按下的方向键是否与当前正在检查的动作匹配。如果匹配，玩家得一分，并且 `current_move` 更新到列表中的下一个动作。如果不匹配，游戏结束！将以下代码添加到你在第 17 步开始编写的 `on_key_up()` 函数中。注意要添加在正确的位置。

![](img/3188b147f991a51de14dcd2bb4b4c42e_151_1.png)

```python
if key == keys.UP:
    update_dancer(0)
    if move_list[current_move] == 0:
        score = score + 1
        next_move()
    else:
        game_over = True
elif key == keys.RIGHT:
    update_dancer(1)
    if move_list[current_move] == 1:
        score = score + 1
        next_move()
    else:
        game_over = True
elif key == keys.DOWN:
    update_dancer(2)
    if move_list[current_move] == 2:
        score = score + 1
        next_move()
    else:
        game_over = True
elif key == keys.LEFT:
    update_dancer(3)
    if move_list[current_move] == 3:
        score = score + 1
        next_move()
    else:
        game_over = True
return
```

如果玩家按下了正确的按键，此代码块运行。

如果玩家犯了错误，`game_over` 将被设置为 `True`。

### 专家提示

**事件处理**

Dance Challenge 使用名为 `on_key_up()` 的事件处理函数来响应玩家按下方向键的操作。在这种情况下，你不应该将处理按键的代码放在内置的 `update()` 函数中，因为它运行过于频繁。如果你只按下一秒钟按键，`update()` 会告诉游戏你按了数百次。这很可能与舞蹈序列不匹配，因此游戏会立刻结束。

> 别担心！我会处理好的。

![](img/3188b147f991a51de14dcd2bb4b4c42e_152_0.png)

### 继续前进！

为了让游戏更具挑战性，每次玩家成功完成一个舞蹈序列后，都需要显示一组新的动作。用下面的代码替换第 13 步 `update()` 函数中的 `pass` 来实现这一点。

```python
def update():
    global game_over, current_move, moves_complete
    if not game_over:
        if moves_complete:
            generate_moves()
            moves_complete = False
            current_move = 0
```

> 我已失控！

![](img/3188b147f991a51de14dcd2bb4b4c42e_152_1.png)

这行代码在你完成当前列表中的所有动作后运行。

这行代码生成一系列新动作并显示它们。

### 28 测试游戏

在添加游戏的最后润色之前，先测试一下。保存代码然后运行。尝试正确完成第一组动作，将得分增加到 4，然后在第二组动作时故意犯一个错误。你在屏幕上看到了什么？

![](img/3188b147f991a51de14dcd2bb4b4c42e_153_0.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_153_1.png)

### 29 开始音乐

目前，你的舞者没有音乐可跳，这不太有趣。在程序中添加一条命令，播放你之前保存到 music 文件夹中的音频文件。在第 24 步输入的命令下方输入以下代码。这将告诉 Pygame Zero 开始播放音乐文件，直到被告知停止。如果玩家在歌曲结束时仍在跳舞，它将循环播放并再次播放这首歌。

```python
generate_moves()
music.play("vanishing-horizon")

def update():
```

### 30 停止音乐

你不希望游戏结束后音乐继续播放。因此，你需要在 `update()` 函数中的第一个 `if` 语句中添加一个 `else` 分支，以便在游戏结束时停止音乐。将以下代码添加到你在第 27 步输入的代码中。

```python
if not game_over:
    if moves_complete:
        generate_moves()
        moves_complete = False
        current_move = 0
else:
    music.stop()
```

如果 `game_over` 为 `True`，这行代码将停止播放音频文件。

### 31 准备游玩

你的代码现在已经完成了，穿上你的舞鞋吧！保存文件，运行它，你应该会在命令提示符或终端窗口中看到它，看看你能坚持跳舞多久！

![](img/3188b147f991a51de14dcd2bb4b4c42e_153_2.png)

## 技巧与调整

你可以修改代码，让游戏变得更有趣。但前提是你在跳完那么多舞之后还有足够的精力！

![](img/3188b147f991a51de14dcd2bb4b4c42e_154_0.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_154_1.png)

- **创建你自己的角色**

  使用网上可用的 8 位编辑器制作你自己的舞者，或者使用 Python Games 资源包中提供的附加图像。你可以设置超过四个舞蹈动作，让变化更加有趣。只需在第 17 步的 `on_key_up()` 函数下添加一些代码，为每个额外动作分配按键即可。

- **与朋友对战！**

  你可以和朋友一起玩这个游戏。修改代码，使所有奇数序列的得分加到玩家 1 的得分上，偶数序列的得分加到玩家 2 的得分上。屏幕顶部应同时显示两个得分，并且你必须在倒计时开始前显示一条消息，告知接下来该哪位玩家操作。在 `on_key_up()` 函数中添加一些代码，让一位玩家使用 **W、A、S** 和 **D** 键输入动作，另一位玩家使用 **上、左、下、右** 方向键。

  ![](img/3188b147f991a51de14dcd2bb4b4c42e_154_2.png)

- **更长的舞蹈**

  你可以让游戏更具挑战性。每次你完成三个序列后，将 `dance_length` 增加 1。要找出已完成多少轮，可以将已跳的序列数除以 3。如果余数为零，说明自上次检查以来已成功完成三个序列，因此给 `dance_length` 加 1。你可以使用 Python 的取模运算符来计算余数。取模使用 `%` 符号表示，因此 `4 % 3` 会给出 4 除以 3 的余数。

  ```python
  if (rounds % 3 == 0):
      dance_length = dance_length + 1
  ```

  ![](img/3188b147f991a51de14dcd2bb4b4c42e_154_3.png)

- **更换音乐**

  你可以通过从 www.creativecommons.org 下载音频文件来更换游戏音乐。记得寻找 `.ogg` 格式的文件。你不必为音乐付费，但你应该在游戏中注明创作者，添加一行代码，在“GAME OVER!”屏幕上显示曲目名称及其创作者。

