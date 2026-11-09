

### 8. 逼真的眨眼

眼睛只需要短暂闭合，并在两次眨眼之间保持睁开一会儿。将 `blink()` 这个函数添加到你第 7 步输入的代码下方。它会让眼睛眨动四分之一秒（250 毫秒），最后用一条命令告诉 `mainloop()` 在 3 秒（3,000 毫秒）后再次调用它。

```python
c.itemconfigure(eye_right, fill=new_color)

def blink():
    toggle_eyes()
    root.after(250, toggle_eyes)
    root.after(3000, blink)

root = Tk()
```

- 闭上眼睛。
- 等待 250 毫秒，然后睁开眼睛。
- 等待 3,000 毫秒，然后再次眨眼。

### 9. 动画效果！

将这行代码放在程序的主体部分，紧挨着最后一行上方。现在运行程序。你的宠物会“活”1 秒钟（1,000 毫秒），然后一直坐在那里眨眼，直到你关闭窗口。

```python
root.after(1000, blink)
root.mainloop()
```

- 等待 1,000 毫秒，然后开始眨眼。

## 改变心情

屏幕宠物现在看起来很开心，带着小小的微笑，但让我们让它更开心一些。我们会给它一个更灿烂的大笑容和明亮红润的脸颊。

![](img/6b18a113f7aa9338e32f3ac1fa217987_148_0.png)

### 10. 制作开心的表情

将这段代码添加到程序中绘制屏幕宠物的部分，放在创建“正常”嘴巴的代码行后面。除了开心的嘴巴和粉色的脸颊外，它还会绘制一张悲伤的嘴巴。它们目前都保持隐藏状态。

- 创建一个开心的嘴巴。
- 创建一个悲伤的嘴巴。

```python
mouth_normal = c.create_line(170, 250, 200, 272, 230, 250, smooth=1, width=2, state=NORMAL)
mouth_happy = c.create_line(170, 250, 200, 282, 230, 250, smooth=1, width=2, state=HIDDEN)
mouth_sad = c.create_line(170, 250, 200, 232, 230, 250, smooth=1, width=2, state=HIDDEN)

cheek_left = c.create_oval(70, 180, 120, 230, outline='pink', fill='pink', state=HIDDEN)
cheek_right = c.create_oval(280, 180, 330, 230, outline='pink', fill='pink', state=HIDDEN)

c.pack()
```

这几行代码会创建粉红色的、泛红的脸颊。

### 11. 显示开心的表情

接下来，创建一个名为 `show_happy()` 的函数，当你像抚摸屏幕宠物一样将鼠标指针移到它上面时，它会显示开心的表情。将这段代码输入到你在第 8 步添加的 `blink()` 函数下方。

![](img/6b18a113f7aa9338e32f3ac1fa217987_149_0.png)

### 事件处理程序

`show_happy()` 函数是一个事件处理程序。这意味着它只在特定事件发生时被调用，以便处理该事件。在你的代码中，抚摸宠物会调用 `show_happy()`。在现实生活中，你可能会调用一个“拖地”函数来处理“打翻饮料”事件！

![](img/6b18a113f7aa9338e32f3ac1fa217987_149_1.png)

这个 `if` 行用于检查鼠标指针是否位于宠物上方。

```python
root.after(3000, blink)

def show_happy(event):
    if (20 <= event.x <= 350) and (20 <= event.y <= 350):
        c.itemconfigure(cheek_left, state=NORMAL)
        c.itemconfigure(cheek_right, state=NORMAL)
        c.itemconfigure(mouth_happy, state=NORMAL)
        c.itemconfigure(mouth_normal, state=HIDDEN)
        c.itemconfigure(mouth_sad, state=HIDDEN)
    return
```

- event.x 和 event.y 是鼠标指针的坐标。
- 显示粉色的脸颊。
- 显示开心的嘴巴。
- 隐藏正常的嘴巴。
- 隐藏悲伤的嘴巴。

### 专家提示——焦点

除非窗口处于“焦点”状态，否则 Tkinter 无法看到你将鼠标指针移到窗口上来抚摸屏幕宠物。你可以通过在窗口中的任意位置单击一次来让窗口获得焦点。

![](img/6b18a113f7aa9338e32f3ac1fa217987_149_2.png)

### 12. 开心的动作

程序启动时，屏幕宠物会在你什么都不做的情况下眨眼。但要想让它在被抚摸时表现出开心的样子，你需要告诉它需要关注什么事件。Tkinter 将鼠标指针在窗口上移动称为 `<Motion>` 事件。你需要使用 Tkinter 的 `bind()` 命令将其链接到处理函数。将这行代码添加到程序的主体部分。然后运行代码并抚摸宠物来试试看。

```python
c.pack()
c.bind('<Motion>', show_happy)
root.after(1000, blink)
root.mainloop()
```

这条命令将移动的鼠标指针与开心的表情关联起来。

### 13. 隐藏开心的表情

你只希望在真正抚摸屏幕宠物时，它才看起来非常开心。在 `show_happy()` 代码下方添加一个新函数 `hide_happy()`。（这些新代码会将屏幕宠物的表情恢复为正常。）

```python
def hide_happy(event):
    c.itemconfigure(cheek_left, state=HIDDEN)
    c.itemconfigure(cheek_right, state=HIDDEN)
    c.itemconfigure(mouth_happy, state=HIDDEN)
    c.itemconfigure(mouth_normal, state=NORMAL)
    c.itemconfigure(mouth_sad, state=HIDDEN)
    return
```

- 隐藏粉色的脸颊。
- 隐藏开心的嘴巴。
- 显示正常的嘴巴。
- 隐藏悲伤的嘴巴。

![](img/6b18a113f7aa9338e32f3ac1fa217987_150_0.png)

别忘了保存你的工作。

### 14. 调用函数

输入这行代码，以便在鼠标指针离开窗口时调用 `hide_happy()`。它将 Tkinter 的 `<Leave>` 事件与 `hide_happy()` 关联起来。现在测试你的代码。

```python
c.bind('<Motion>', show_happy)
c.bind('<Leave>', hide_happy)

root.after(1000, blink)
```

## 真调皮！

到目前为止，你的宠物一直表现得很乖。让我们给它一个调皮的性格吧！你可以添加一些代码，让屏幕宠物在你双击逗它时吐出舌头并斗鸡眼。

![](img/6b18a113f7aa9338e32f3ac1fa217987_150_1.png)

### 15. 绘制舌头

将这些代码行添加到绘制屏幕宠物的代码中，放在创建悲伤嘴巴的代码行下方。程序将分两部分绘制舌头，一个矩形和一个椭圆形。

```python
mouth_sad = c.create_line(170, 250, 200, 232, 230, 250, smooth=1, width=2, state=HIDDEN)
tongue_main = c.create_rectangle(170, 250, 230, 290, outline='red', fill='red', state=HIDDEN)
tongue_tip = c.create_oval(170, 285, 230, 300, outline='red', fill='red', state=HIDDEN)

cheek_left = c.create_oval(70, 180, 120, 230, outline='pink', fill='pink', state=HIDDEN)
```

### 16. 设置标志

在代码中添加两个标志变量，用来跟踪屏幕宠物的眼睛是否交叉（斗鸡眼）或舌头是否伸出。将它们输入到告诉屏幕宠物开始眨眼的代码行上方，也就是你在第 9 步添加到主程序部分的那一行。

```python
c.eyes_crossed = False
c.tongue_out = False

root.after(1000, blink)
```

这些是用于瞳孔和舌头的标志变量。

### 17. 切换舌头

这个函数会在屏幕宠物的舌头伸出和缩回之间进行切换。将下面显示的代码放在你在第 11 步创建的 `show_happy()` 函数上方。

```python
def toggle_tongue():
    if not c.tongue_out:
        c.itemconfigure(tongue_tip, state=NORMAL)
        c.itemconfigure(tongue_main, state=NORMAL)
        c.tongue_out = True
    else:
        c.itemconfigure(tongue_tip, state=HIDDEN)
        c.itemconfigure(tongue_main, state=HIDDEN)
        c.tongue_out = False

def show_happy(event):
```

- 代码检查舌头是否已经伸出。
- 如果舌头没有伸出，这些行会将其显示出来。
- 这行代码设置一个标志变量，表示舌头现在已伸出。
- 舌头已经伸出（else 分支）。
- 这行代码设置一个标志变量，表示舌头没有伸出。
- 这些行再次隐藏舌头。

### 专家提示：使用标志变量

标志变量可以帮助你跟踪程序中可能处于两种状态之一的某个东西。当你改变状态时，就更新标志。厕所门上的“使用中 / 空闲”标志就是一个标志——锁门时设置为“使用中”，开锁时再设回“空闲”。

![](img/6b18a113f7aa9338e32f3ac1fa217987_151_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_151_1.png)

### 18. 切换瞳孔

为了做出斗鸡眼的表情，瞳孔需要向内转动。这个 `toggle_pupils()` 函数将在屏幕宠物的瞳孔向内转动和正常外观之间切换。将它输入到你在第 8 步添加的 `blink()` 函数下方。

```python
root.after(3000, blink)

def toggle_pupils():
    if not c.eyes_crossed:
        c.move(pupil_left, 10, -5)
        c.move(pupil_right, -10, -5)
        c.eyes_crossed = True
    else:
        c.move(pupil_left, -10, 5)
        c.move(pupil_right, 10, 5)
        c.eyes_crossed = False
```

- 代码检查眼睛是否已经交叉（斗鸡眼）。
- 如果瞳孔没有交叉，这行代码会将它们向内移动。
- 这行代码设置一个标志变量，表示眼睛已交叉。
- 眼睛已经交叉（else 分支）。
- 这些行将瞳孔移回正常位置。
- 这行代码设置一个标志，表示眼睛没有交叉。

### 19. 协调调皮动作

现在创建一个函数，让屏幕宠物同时伸出舌头并交叉眼睛。将这段代码输入到你在第 17 步添加的 `toggle_tongue()` 函数下方。使用 `root.after()` 函数让屏幕宠物在 1 秒（1,000 毫秒）后恢复正常，就像你在 `blink()` 中所做的那样。

```python
def cheeky(event):
    toggle_tongue()
    toggle_pupils()
    hide_happy(event)
    root.after(1000, toggle_tongue)
    root.after(1000, toggle_pupils)
    return
```

- 伸出舌头。
- 交叉瞳孔。
- 隐藏开心的表情。
- 1,000 毫秒后收回舌头。
- 1,000 毫秒后恢复瞳孔。

![](img/6b18a113f7aa9338e32f3ac1fa217987_152_0.png)

别忘了保存你的工作。

### 20. 将双击关联到调皮动作

要触发屏幕宠物的调皮表情，请将任何双击事件关联到 `cheeky()` 函数。将这一行放在你在第 14 步添加的用于隐藏屏幕宠物开心表情的代码行下方。运行代码并双击，看看调皮的效果吧！

```python
c.bind('<Motion>', show_happy)
c.bind('<Leave>', hide_happy)
c.bind('<Double-1>', cheeky)
```

`<Double-1>` 是 Tkinter 对在窗口中使用鼠标双击事件的命名。

