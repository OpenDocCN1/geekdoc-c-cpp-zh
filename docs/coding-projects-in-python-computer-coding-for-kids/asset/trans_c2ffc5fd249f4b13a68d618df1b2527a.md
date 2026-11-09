

### 3 解密

解密消息非常容易。在你的消息的加密版本中，所有偶数位置上的字母都是原始消息中的字母。因此，你可以使用 `get_even_letters()` 函数来获取它们。

> 解密字母很简单。

![](img/6b18a113f7aa9338e32f3ac1fa217987_142_0.png)

```python
def decrypt(message):
    even_letters = get_even_letters(message)
    new_message = ''.join(even_letters)
    return new_message
```

获取原始消息中的字母。

将 `even_letters` 中的字母连接成一个字符串。

### 4 使用新函数

现在你需要更新程序中的无限循环部分，改用新的 `encrypt()` 和 `decrypt()` 函数，而不是 `swap_letters()`。为此，请对代码进行这些更改。

> 我必须更新我的无限循环！

![](img/6b18a113f7aa9338e32f3ac1fa217987_142_1.png)

```python
while True:
    task = get_task()
    if task == 'encrypt':
        message = get_message()
        encrypted = encrypt(message)
        messagebox.showinfo('Ciphertext of the secret message is:', encrypted)
    elif task == 'decrypt':
        message = get_message()
        decrypted = decrypt(message)
        messagebox.showinfo('Plaintext of the secret message is:', decrypted)
    else:
        break
root.mainloop()
```

新的 `encrypt()` 函数取代 `swap_letters()`。

新的 `decrypt()` 函数取代 `swap_letters()`。

### 多重加密

为了让事情更复杂，你可以修改代码，把本节中所有不同的技巧和调整组合起来。例如，它可以添加假字母、交换字母，然后再将它们反转！

> 我的密码现在更安全了！

![](img/6b18a113f7aa9338e32f3ac1fa217987_142_2.png)

## 屏幕宠物

你是否曾希望在做电脑作业时有一只宠物陪伴你？在这个项目中，你将创建一只“住”在电脑屏幕角落的宠物。它会让你忙起来，因为你需要照顾它，让它保持开心。

### 会发生什么

当你启动程序时，屏幕宠物会坐在那里，脸上带着一丝微笑，朝你眨眼。这只可爱的天蓝色伙伴会根据你在屏幕上与它的互动，把表情从正常（下图）变为开心、调皮或难过。但别担心，它很友好——即使无聊了也不会咬人！

![](img/6b18a113f7aa9338e32f3ac1fa217987_143_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_143_1.png)

**开心的脸**  
如果你用鼠标指针“抚摸”它，屏幕宠物会笑容满面并脸红。

![](img/6b18a113f7aa9338e32f3ac1fa217987_143_2.png)

**调皮的脸**  
如果你双击它来“挠痒痒”，这只调皮的宠物会伸出舌头。

![](img/6b18a113f7aa9338e32f3ac1fa217987_143_3.png)

**难过的脸**  
如果你不理它，屏幕宠物会变得难过。抚摸它会让它重新振作起来。

屏幕宠物会出现在一个 Tkinter 窗口中。

### 绘制你的屏幕宠物

我们开始吧。首先你需要创建屏幕宠物将要居住的窗口。然后你要编写一些代码，在屏幕上绘制这只宠物。

- 1. **新建文件**  
  打开 IDLE。转到“文件”菜单，选择“新建文件”，然后将文件保存为“screen_pet.py”。

- 2. **添加 Tkinter 模块**  
  你需要在程序开头导入 Python 的 Tkinter 模块中的部分内容。输入这段代码以引入 Tkinter，并打开一个窗口，让你的屏幕宠物住在里面。

- 3. **新建画布**  
  在窗口中创建一个名为“c”的深蓝色画布，你将在上面绘制宠物。把这行代码添加到打开 Tkinter 窗口的那行代码之后。这四行新代码是程序主要部分的开始。

- 4. **运行它**  
  现在试着运行程序。你注意到了什么？代码应该只会显示一个普通的深蓝色窗口。此刻它看起来有点单调和空荡——你需要的是一只宠物！

![](img/6b18a113f7aa9338e32f3ac1fa217987_145_0.png)

> “我给你画像时别动！”

这一行导入本项目所需的 Tkinter 模块部分。

```python
from tkinter import HIDDEN, NORMAL, Tk, Canvas
root = Tk()
```

这一行启动 Tkinter 并打开一个窗口。

画布宽 400 像素，高 400 像素。

背景颜色将是深蓝色。

```python
from tkinter import HIDDEN, NORMAL, Tk, Canvas
root = Tk()
c = Canvas(root, width=400, height=400)
c.configure(bg='dark blue', highlightthickness=0)
c.pack()
root.mainloop()
```

任何以 c. 开头的命令都与画布有关。

此命令在 Tkinter 窗口中安排内容。

这一行启动用于监视事件（例如鼠标点击）的函数。

![](img/6b18a113f7aa9338e32f3ac1fa217987_145_1.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_145_2.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_145_3.png)

别忘了保存你的工作。

### 开始绘制

要绘制宠物，请把这些指令添加到代码最后两行之上。每个身体部位都有一条单独的命令。这些数字称为坐标，用来告诉 Tkinter 要绘制什么以及在哪里绘制。

将身体颜色存储在变量 c.body_color 中，意味着你不必反复输入 'SkyBlue'。

```python
c.configure(bg='dark blue', highlightthickness=0)
c.body_color = 'SkyBlue'

body = c.create_oval(35, 20, 365, 350, outline=c.body_color, fill=c.body_color)
ear_left = c.create_polygon(75, 80, 75, 165, 10, 70, outline=c.body_color, fill=c.body_color)
ear_right = c.create_polygon(255, 85, 255, 165, 320, 70, outline=c.body_color, fill=c.body_color)

foot_left = c.create_oval(65, 320, 145, 360, outline=c.body_color, fill=c.body_color)
foot_right = c.create_oval(250, 320, 330, 360, outline=c.body_color, fill=c.body_color)

eye_left = c.create_oval(130, 110, 160, 170, outline='black', fill='white')
pupil_left = c.create_oval(140, 145, 150, 155, outline='black', fill='black')
eye_right = c.create_oval(230, 110, 260, 170, outline='black', fill='white')
pupil_right = c.create_oval(240, 145, 250, 155, outline='black', fill='black')

mouth_normal = c.create_line(170, 250, 200, 272, 230, 250, smooth=1, width=2, state=NORMAL)

c.pack()
```

在代码中，“left”和“right”指的是你观看窗口时的左侧和右侧。

这些坐标对定义了嘴巴的起点、中点和终点。

嘴巴是一条平滑的线，宽 2 像素。

### 专家提示

#### Tkinter 坐标

绘图指令使用 x 和 y 坐标。在 Tkinter 中，x 坐标从左侧的 0 开始，随着你在窗口中向右移动而增大，直到最右侧达到 400。y 坐标也从顶部的 0 开始。随着你向下移动，它们会变大，直到最底部达到 400。

坐标以成对形式书写，x 坐标在前。

![](img/6b18a113f7aa9338e32f3ac1fa217987_146_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_146_1.png)

### 再次运行

再次运行程序，你应该会看到屏幕宠物坐在 Tkinter 窗口的中间。

### 眨眼的宠物

你的屏幕宠物看起来很可爱，但它什么也没做！我们来写一些代码让它眨眼。你需要创建两个函数：一个用来睁开和闭上眼睛，另一个用来告诉眼睛保持睁开和闭上多长时间。

![](img/6b18a113f7aa9338e32f3ac1fa217987_147_0.png)

#### 睁开和闭上眼睛

在文件顶部、第一行代码下方创建这个函数 toggle_eyes()。它通过隐藏瞳孔并用与身体相同的颜色填充眼睛，让眼睛看起来是闭着的。它还会在睁开和闭上两种状态之间切换眼睛。

首先，代码检查眼睛的当前颜色；白色表示睁开，蓝色表示闭上。

这一行将眼睛的新颜色设置为相反的值。

为了眨眼，眼睛会填充天蓝色，瞳孔会消失。

```python
from tkinter import HIDDEN, NORMAL, Tk, Canvas

def toggle_eyes():
    current_color = c.itemcget(eye_left, 'fill')
    new_color = c.body_color if current_color == 'white' else 'white'
    current_state = c.itemcget(pupil_left, 'state')
    new_state = NORMAL if current_state == HIDDEN else HIDDEN
    c.itemconfigure(pupil_left, state=new_state)
    c.itemconfigure(pupil_right, state=new_state)
    c.itemconfigure(eye_left, fill=new_color)
    c.itemconfigure(eye_right, fill=new_color)
```

现在代码检查瞳孔的当前状态是 NORMAL（可见）还是 HIDDEN（不可见）。

这一行将瞳孔的新状态设置为相反的值。

这些行改变瞳孔的可见性。

这些行改变眼睛的填充颜色。

#### 切换

在两种状态之间切换称为“切换”（toggling）。所以，当你打开和关闭家里的灯时，你就是在“切换”灯。切换可以让屏幕宠物的眼睛在睁开和闭上之间转换，或者说切换。如果运行程序时眼睛是闭着的，它们会变成睁开的。如果它们是睁开的，就会变成闭着的。

打开灯！

再把那盏灯切换回关闭状态！

![](img/6b18a113f7aa9338e32f3ac1fa217987_147_1.png)

