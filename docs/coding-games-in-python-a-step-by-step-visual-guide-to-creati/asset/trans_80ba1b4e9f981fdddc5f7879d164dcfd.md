
### 20 正确答案

现在你需要告诉 Python，如果玩家答对一题，你希望程序做什么。你需要增加当前得分，然后获取下一道题。如果没有剩余题目，游戏应结束。将第 3 步中 `def correct_answer()` 下方的 `pass` 替换为以下代码。

```python
def correct_answer():
    global question, score, time_left
    score = score + 1
    if questions:
        question = questions.pop(0)
        time_left = 10
    else:
        print("End of questions")
        game_over()
```

- 这会将得分增加一。
- 如果列表中还有更多题目，这会获取下一道题。
- 这会将计时器重置回十秒。
- 如果列表中没有更多题目，此代码块会运行。
- 这会在命令提示符或终端窗口中显示一条消息。

### 21 回答问题

接下来添加一些代码，当玩家点击答案框时运行。这段代码会检查点击了哪个框，然后在命令提示符或终端窗口中打印结果。将第 3 步中 `on_mouse_down(pos)` 函数下方的 `pass` 替换为以下代码。

这一行检查点击了哪个框。

```python
def on_mouse_down(pos):
    index = 1
    for box in answer_boxes:
        if box.collidepoint(pos):
            print("Clicked on answer " + str(index))
        index = index + 1
```

- 变量 index 保存一个数字，表示答案框在列表中的位置。
- 变量 index 增加一，并移动到列表中的下一个答案框。
- 这会在命令提示符或终端窗口中显示一条消息。

### 22 点击这些框

再次运行你的代码，并点击屏幕上出现的每个答案框。你应该会在命令提示符或终端窗口中看到消息，告诉你点击了哪个框。

![](img/3188b147f991a51de14dcd2bb4b4c42e_111_0.png)

### 23 检查答案

现在你需要更新第 21 步中 `on_mouse_down(pos)` 函数的主体。添加以下代码，当玩家点击正确答案框时运行。

```python
def on_mouse_down(pos):
    index = 1
    for box in answer_boxes:
        if box.collidepoint(pos):
            print("Clicked on answer " + str(index))
            if index == question[5]:
                print("You got it correct!")
                correct_answer()
        index = index + 1
```

- 这会检查玩家是否点击了正确答案框。
- 每个题目列表中第五个位置的项目是对应正确答案的数字。

> 哇！蒂娜把所有答案都答对了！

![](img/3188b147f991a51de14dcd2bb4b4c42e_112_0.png)

### 24 结束游戏

如果玩家点击错误答案，游戏应结束。最后一次更新 `def on_mouse_down(pos)` 下方的代码，并使用 else 语句在玩家选择错误答案时运行 `game_over()` 函数。添加下方以黑色显示的代码。

```python
def on_mouse_down(pos):
    index = 1
    for box in answer_boxes:
        if box.collidepoint(pos):
            print("Clicked on answer " + str(index))
            if index == question[5]:
                print("You got it correct!")
                correct_answer()
            else:
                game_over()
        index = index + 1
```

如果点击的框不是正确答案，此代码块会运行。

> 再得一分，游戏就结束了！

![](img/3188b147f991a51de14dcd2bb4b4c42e_112_1.png)

### 25 更新计时器

现在你需要更新第 3 步中 `def update_time_left()` 下方的代码。每次运行该函数时，这会将秒数减少一。输入以下代码。

```python
def update_time_left():
    global time_left

    if time_left:
        time_left = time_left - 1
    else:
        game_over()
```

- 如果计时器上还有剩余时间，这会将其减少一。
- 当计时器用完时，这会结束游戏。

![](img/3188b147f991a51de14dcd2bb4b4c42e_113_0.png)

### 26 安排计时器

最后，你需要更新 `update_time_left()` 函数，使其每秒自动运行一次。你可以使用 Pygame Zero 的时钟工具来实现这一点。将这一行代码添加到程序的最底部。

```python
clock.schedule_interval(update_time_left, 1.0)
```

这会每秒调用一次 `update_time_left()` 函数。

### 27 开始答题吧！

就这样！运行你的游戏并试一试。希望你能正确回答所有问题。记住，如果你的屏幕显示不正常，你需要回到代码并仔细检查。认真阅读每一行，确保你的代码与步骤完全一致。和朋友们一起愉快地答题吧！

![](img/3188b147f991a51de14dcd2bb4b4c42e_113_1.png)

玩家需要在时间用完之前点击正确答案。

## 技巧与调整

你已经制作了一款很棒的游戏，但不要只局限于五道题。通过调整一些规则，将“大型测验”提升到新的水平。以下是一些入门建议。

![](img/3188b147f991a51de14dcd2bb4b4c42e_114_0.png)

### 获取提示

如果玩家按下 **H** 键，你可以通过在命令提示符或终端窗口中显示正确答案框来给玩家一个提示。以下是一些可用于实现此功能的代码。

```python
def on_key_up(key):
    if key == keys.H:
        print("The correct answer is box number %s" % question[5])
```

### 跳过一道题

你可以向 **on_key_up(key)** 函数添加更多代码，让玩家可以通过按**空格键**跳过一道题。跳过一道题意味着他们继续下一道题，但不得分。以下是一种实现方法。

```python
def on_key_up(key):
    global score
    if key == keys.H:
        print("The correct answer is box number %s" % question[5])
    if key == keys.SPACE:
        score = score - 1
        correct_answer()
```

此代码块首先将玩家得分减少一，然后运行 **correct_answer()** 函数，该函数会将得分增加一，从而保持得分不变。

### 更多题目

你可以反复玩这个游戏，但为了保持趣味性，你可以更改题目，甚至添加更多题目。以下是一些你可能会用到的题目示例。你随时可以添加自己的题目！如果添加额外题目，你还需要更新代码中的哪些其他内容？

```python
q6 = ["What is a quarter of 200?",
      "50", "100", "25", "150", 1]

q7 = ["Which is the largest state in the USA?",
      "Wyoming", "Alaska", "Florida", "Texas", 2]

q8 = ["How many wives did Henry VIII have?",
      "Eight", "Four", "Six", "One", 3]
```

### 增添一抹色彩

你可以通过更改背景、答案框或屏幕上文本的颜色，让界面更具吸引力。以下是一些颜色及其 RGB 值，供你尝试。请查看第 75 页，了解 RGB 值的工作原理。

|  |  |  |  |  |
|---|---|---|---|---|
| **香蕉鞭色**<br>(R 255, G 239, B 213) | **李子色**<br>(R 221, G 160, B 221) | **石板蓝**<br>(R 106, G 90, B 205) |  |  |
| **浅鲑鱼色**<br>(R 255, G 160, B 122) | **亮粉色**<br>(R 255, G 105, B 180) | **桃色**<br>(R 255, G 218, B 185) | **兰花紫**<br>(R 218, G 112, B 214) | **深石板蓝**<br>(R 72, G 61, B 139) |
| **鲑鱼色**<br>(R 250, G 128, B 114) | **深粉色**<br>(R 255, G 20, B 147) | **淡金菊色**<br>(R 238, G 232, B 170) | **中兰花紫**<br>(R 186, G 85, B 211) | **浅绿色**<br>(R 144, G 238, B 144) |
| **浅珊瑚色**<br>(R 240, G 128, B 128) | **中紫红色**<br>(R 199, G 21, B 133) | **黄色**<br>(R 255, G 255, B 0) | **蓝紫色**<br>(R 138, G 43, B 226) | **深海洋绿**<br>(R 143, G 188, B 143) |
| **深红**<br>(R 220, G 20, B 60) | **珊瑚色**<br>(R 255, G 127, B 80) | **金色**<br>(R 255, G 215, B 0) | **深紫色**<br>(R 148, G 0, B 211) | **黄绿色**<br>(R 173, G 255, B 47) |
| **红色**<br>(R 255, G 0, B 0) | **番茄红**<br>(R 255, G 99, B 71) | **卡其色**<br>(R 240, G 230, B 140) | **深兰花紫**<br>(R 153, G 50, B 204) | **查特酒绿**<br>(R 127, G 255, B 0) |
| **耐火砖红**<br>(R 178, G 34, B 34) | **橙红色**<br>(R 255, G 69, B 0) | **深卡其色**<br>(R 189, G 183, B 107) | **深洋红**<br>(R 139, G 0, B 139) | **草坪绿**<br>(R 124, G 252, B 0) |
| **深红色**<br>(R 139, G 0, B 0) | **深橙色**<br>(R 255, G 140, B 0) | **薰衣草紫**<br>(R 230, G 230, B 250) | **紫色**<br>(R 128, G 0, B 128) | **酸橙绿**<br>(R 0, G 255, B 0) |
| **淡紫红色**<br>(R 219, G 112, B 147) | **橙色**<br>(R 255, G 165, B 0) | **蓟色**<br>(R 216, G 191, B 216) | **靛蓝色**<br>(R 75, G 0, B 130) | **酸橙绿**<br>(R 50, G 205, B 50) |
| **粉色**<br>(R 255, G 192, B 203) | **浅黄色**<br>(R 255, G 255, B 224) | **紫罗兰色**<br>(R 238, G 130, B 238) | **中石板蓝**<br>(R 123, G 104, B 238) | **海绿色**<br>(R 46, G 139, B 87) |

