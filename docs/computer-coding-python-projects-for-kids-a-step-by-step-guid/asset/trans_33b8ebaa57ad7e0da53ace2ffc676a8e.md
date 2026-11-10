

## 10 哎呀——鸡蛋掉了！

接下来在`move_eggs()`之后添加`egg_dropped()`函数。当鸡蛋掉落时，它会从鸡蛋列表中移除，并从画布上删除。使用`lose_a_life()`函数扣除一条生命，该函数将在第11步中创建。如果失去一条生命后没有剩余生命，则显示“游戏结束！”消息。

如果没有剩余生命，告诉玩家游戏结束。

```python
    root.after(egg_speed, move_eggs)

    def egg_dropped(egg):
        eggs.remove(egg)  # 将鸡蛋从鸡蛋列表中移除。
        c.delete(egg)  # 鸡蛋从画布上消失。
        lose_a_life()  # 此行调用lose_a_life()函数。
        if lives_remaining == 0:
            messagebox.showinfo('游戏结束！', '最终得分：' + str(score))
            root.destroy()  # 游戏结束。
```

## 11 失去一条生命

失去一条生命只需从`lives_remaining`变量中减去一条生命，然后在屏幕上显示新值。在`egg_dropped()`函数后添加这些行。

```python
    root.destroy()

    def lose_a_life():
        global lives_remaining  # 此变量需要设为全局变量，因为函数会修改它。
        lives_remaining -= 1  # 玩家失去一条生命。
        c.itemconfigure(lives_text, text='生命：' + str(lives_remaining))  # 此行更新显示剩余生命的文本。
```

## 12 检查是否接住

现在添加`check_catch()`函数。如果鸡蛋位于接蛋器的弧形范围内，则视为接住。为了判断是否接住，`for`循环获取每个鸡蛋的坐标，并与接蛋器的坐标进行比较。如果匹配，则鸡蛋被接住。然后将其从列表中删除，从屏幕上移除，并增加分数。

```python
    c.itemconfigure(lives_text, text='生命：' + str(lives_remaining))

    def check_catch():
        (catcher_x, catcher_y, catcher_x2, catcher_y2) = c.coords(catcher)  # 获取接蛋器的坐标。
        for egg in eggs:
            (egg_x, egg_y, egg_x2, egg_y2) = c.coords(egg)  # 获取鸡蛋的坐标。
            if catcher_x < egg_x and egg_x2 < catcher_x2 and catcher_y2 - egg_y2 < 40:  # 鸡蛋在水平方向和垂直方向上是否都在接蛋器内？
                eggs.remove(egg)
                c.delete(egg)
                increase_score(egg_score)  # 将分数增加10分。
        root.after(100, check_catch)  # 在100毫秒（十分之一秒）后再次调用此函数。
```

## 13 增加分数

首先，分数按`points`参数的值增加。接下来，通过将鸡蛋的速度和间隔值乘以难度系数来计算新的速度和间隔。最后，屏幕上的文本更新为新的分数。在`check_catch()`下方添加这个新函数。

![](img/1bd24ab186f69fb18194b4174ca15178_197_0.png)

```python
root.after(100, check_catch)

def increase_score(points):
    global score, egg_speed, egg_interval
    score += points
    egg_speed = int(egg_speed * difficulty_factor)
    egg_interval = int(egg_interval * difficulty_factor)
    c.itemconfigure(score_text, text='分数：' + str(score))
```

增加玩家的分数。

此行更新显示分数的文本。

## 接住那些鸡蛋！

现在你已经拥有了游戏所需的所有形状和函数，剩下的就是添加接蛋器的控制和启动游戏的命令。

### 14 设置控制

`move_left()`和`move_right()`函数使用接蛋器的坐标来确保它不会离开屏幕。如果仍有移动空间，接蛋器会水平移动20像素。这两个函数通过`bind()`函数与键盘上的左右箭头键关联。`focus_set()`函数允许程序检测按键。在`increase_score()`函数下方添加新函数。

```python
c.itemconfigure(score_text, text='分数：' +
                str(score))

def move_left(event):
    (x1, y1, x2, y2) = c.coords(catcher)
    if x1 > 0:
        c.move(catcher, -20, 0)

def move_right(event):
    (x1, y1, x2, y2) = c.coords(catcher)
    if x2 < canvas_width:
        c.move(catcher, 20, 0)

c.bind('<Left>', move_left)
c.bind('<Right>', move_right)
c.focus_set()
```

接蛋器是否到达了左侧墙壁？

如果没有，向左移动接蛋器。

接蛋器是否到达了右侧墙壁？

如果没有，向右移动接蛋器。

这些行会在按下按键时调用相应函数。

### 15 启动游戏

三个循环函数通过定时器启动。这可以确保它们不会在主循环启动之前运行。最后，`mainloop()`函数启动Tkinter主循环，该循环管理你的所有循环和定时器。全部完成——享受游戏吧，别让那些鸡蛋摔碎！

```python
c.focus_set()
root.after(1000, create_egg)
root.after(1000, move_eggs)
root.after(1000, check_catch)
root.mainloop()
```

三个游戏循环在短暂的1,000毫秒（1秒）暂停后开始。

此行启动Tkinter主循环。

## 技巧与微调

为了让游戏看起来更好，你可以尝试添加一些自己的酷炫场景。有趣的声音和音乐也是让游戏更刺激的好方法。

### 专家提示

### 安装模块

一些最实用的Python模块（例如Pygame）并不包含在标准Python库中。如果你想使用任何其他模块，需要先安装它们。查找模块安装说明的最佳位置是模块的官方网站。https://docs.python.org/3/installing/ 上有说明和技巧。

![](img/1bd24ab186f69fb18194b4174ca15178_198_0.png)

### 设置场景

Tkinter允许使用自定义图像作为画布的背景。如果你的文件是GIF，可以使用`tkinter.PhotoImage`加载该文件。如果你的图像是其他格式，可以了解一下Pillow——一个有用的图像处理模块。

### 制造一些声音

要让游戏真正活起来，可以添加背景音乐或接住鸡蛋/失去生命时的音效。用于添加声音的模块是`pygame.mixer`。记住，pygame不是标准Python模块，所以需要先安装它。你还需要有要播放的声音文件的副本，并将其放在与代码文件相同的文件夹中。完成之后，播放声音只需要几行代码。

播放声音。

```python
import time

from pygame import mixer

mixer.init()
beep = mixer.Sound("beep.wav")
beep.play()
time.sleep(5)
```

让混音器准备好播放声音。

告诉混音器要播放哪个声音。

让程序运行足够长的时间以听到声音。

## 6

## 参考

![](img/1bd24ab186f69fb18194b4174ca15178_200_0.png)

```python
'white', 'proud', 'brave']
nouns = ['apple', 'dinosaur', 'ball',
         'toaster', 'goat', 'dragon',
         'hammer', 'duck', 'panda']

print('欢迎使用密码选择器！')

while True:
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    number = random.randrange(0, 100)
    special_char = random.choice(string.punctuation)

    password = adjective + noun + str(number) + special_char
    print('你的新密码是：%s' % password)

    response = input('你想要另一个密码吗？输入y或n： ')
    if response == 'n':
        break
```

## 九条命（第60页）

```python
import random

lives = 9
words = ['pizza', 'fairy', 'teeth', 'shirt', 'otter', 'plane']
secret_word = random.choice(words)
clue = list('?????')
heart_symbol = u'\u2764'
guessed_word_correctly = False

def update_clue(guessed_letter, secret_word, clue):
    index = 0
    while index < len(secret_word):
        if guessed_letter == secret_word[index]:
            clue[index] = guessed_letter
        index = index + 1

while lives > 0:
    print(clue)
    print('剩余生命：' + heart_symbol * lives)
    guess = input('猜一个字母或整个单词： ')

    if guess == secret_word:
        guessed_word_correctly = True
        break

    if guess in secret_word:
        update_clue(guess, secret_word, clue)
    else:
```

