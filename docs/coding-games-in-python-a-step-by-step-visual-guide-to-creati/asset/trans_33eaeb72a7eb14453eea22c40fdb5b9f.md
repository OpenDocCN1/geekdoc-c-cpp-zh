
## 单分支

最简单的分支命令类型是 if 语句。它只有一个分支，如果条件为 True，计算机就会执行该分支。

![](img/3188b147f991a51de14dcd2bb4b4c42e_36_0.png)

“看好了！我赐予你……‘附魔师’的称号！”

这个比较就是条件。

```python
spells = 11
if (spells > 10):
    print("You gained the title Enchanter!")
```

如果条件为 True，则运行此分支。

### 工作原理

在这个示例中，程序会检查你已施放的法术数量。如果超过十个，程序会打印“你获得了‘附魔师’称号！”如果你施放的法术数量少于十个，则不会打印该消息。

## 两个分支

如果你希望程序在条件为 True 时做一件事，而在条件为 False 时做另一件事，该怎么办？在这种情况下，你需要一个具有两个可能分支的命令，称为 if-else 语句。

```python
game_over = True
if game_over:
    print("Game Over!")
else:
    print("Keep playing!")
```

如果条件为 False，则运行此代码块。

![](img/3188b147f991a51de14dcd2bb4b4c42e_36_1.png)

如果条件为 True，则运行此代码块。

### 工作原理

在这个示例中，有一个名为 game_over 的变量，它被设置为 True。if 语句会检查 game_over 是否为 True。如果是，程序会打印“Game Over!”；如果不是，else 语句就会运行，打印“Keep playing!”试着将 game_over 设置为 True 再设置为 False 来运行这段代码，看看实际效果。

![](img/3188b147f991a51de14dcd2bb4b4c42e_36_2.png)

这是第一个条件。

```python
ghosts = 3
if ghosts > 1:
    print("It’s so spoooky!")
elif ghosts > 0:
    print("Get that ghost!")
else:
    print("Ghosts all gone!")
```

如果第二个条件为 True，则运行此代码块。

如果两个条件都为 False，则运行此代码块。

## 两个以上分支

当可能路径超过两条时，可以在程序中使用 elif 命令（“else-if”的缩写）。在下面的示例中，你需要一次性抓住几个幽灵。

### 工作原理

在这个程序中，变量 ghosts 已被设置为 3，因此第一个分支为 True，程序会打印“太吓人啦！”但如果 ghosts 的值是 1，第一个分支就会为 False，于是第二个分支会运行，打印“抓住那个幽灵！”如果上述两个分支都不为 True，程序会继续执行第三个分支，打印“幽灵全都没了！”elif 语句必须始终位于 if 之后、else 之前。

## 玩转循环

在编写游戏程序时，你经常需要多次运行同一小段代码，但如果每次都要手动输入，那就太无聊了。幸运的是，你可以使用循环反复运行同一代码块。循环有许多不同的类型。

### “For”循环

当你确切知道希望循环重复多少次时，可以使用 for 循环。在这个示例中，代码会打印“你是最高得分者！”十次。你可以在 shell 窗口中亲自试试这段代码。

```python
>>> for count in range(1, 11):
    print("You are the high scorer!")
```

这是循环变量。

被重复执行的代码称为“循环体”。

![](img/3188b147f991a51de14dcd2bb4b4c42e_37_0.png)

#### 循环变量

循环变量记录循环到目前为止已经运行了多少次。在循环开始时，它等于 range 中的第一个数字。第二次循环时，它等于 range 中的第二个数字，依此类推。一旦它完成 range 中倒数第二个数字，循环就会停止。

![](img/3188b147f991a51de14dcd2bb4b4c42e_37_1.png)

#### 循环体

在循环中被重复执行的代码块称为循环体。循环体中的命令必须始终相对于启动 for 循环的那一行行首缩进四个空格。

### 专家提示

#### range

在 Python 中，range 一词后面跟括号中的两个数字，表示“列表中从第一个数字到倒数第二个数字的所有数字”。因此，range(1, 5) 包含数字 1、2、3 和 4，但不包含 5，所以循环会运行四次。

![](img/3188b147f991a51de14dcd2bb4b4c42e_37_2.png)

### 遍历列表

游戏程序经常使用按列表分组在一起的物品集合。如果你想对列表中的每个项执行某些操作，可以使用 `for` 循环。

> 第 31 页会帮助你了解列表。

![](img/3188b147f991a51de14dcd2bb4b4c42e_38_0.png)

#### 列出机器人

在这个示例中，有一个列表，其中包含玩家在游戏中必须逃离的三个机器人的名字。

```python
>>> robots = ["Bing", "Bleep", "Bloop"]
>>> for robot in robots:
    print("I am a robot. My name is " + robot)
```

Python 会在这里添加其中一个机器人的名字。

robot 是一个临时变量，每次循环运行时都会沿着 robots 列表移动。

#### 工作原理

我们创建一个名为 robot 的临时变量，用来保存列表中的单个项。每轮循环都会更新 robot 中的值，使它依次保存 Bing、Bleep，最后是 Bloop。一旦到达列表末尾，循环就会停止。

### 遍历两个列表

Python 可以或多或少自动地从头到尾遍历一个列表。但如果你想同时遍历两个列表，就需要使用一个额外的变量来告诉 Python 依次遍历这两个列表。

![](img/3188b147f991a51de14dcd2bb4b4c42e_38_1.png)

#### 带颜色的机器人

在这个示例中，我们有两个列表。一个名为 robots，保存机器人的名字。另一个名为 colors，告诉你每个机器人的颜色。这个程序使用一个名为 index 的变量来遍历这两个列表，打印出每个机器人的名字以及它的颜色。

index 将帮助 Python 按顺序遍历这两个列表。

这一行更新 index，使 Python 在每次循环时遍历列表。

```python
>>> robots = ["Bing", "Bleep", "Bloop"]
>>> colors = ["red", "orange", "purple"]
>>> index = 0
>>> for each in robots:
    print("My name is " + robots[index] + " I am " + colors[index])
    index = index + 1
```

index 变量记录每个列表当前所在的位置。

![](img/3188b147f991a51de14dcd2bb4b4c42e_39_0.png)

#### 工作原理

`robots[index]` 和 `colors[index]` 都使用 `index` 的值来决定打印各自列表中的哪一项。由于 `index` 一开始被设置为 0，两个列表都会从第一项开始——记住，Python 列表中的第一个位置总是 0，而不是 1。由于 Bing 位于 robots 列表的位置 0，而 red 位于 colors 列表的位置 0，这意味着 Bing 是红色的。每次循环运行时，它都会给 `index` 加 1，使每个列表移到下一项，因此 Bleep 将是橙色，Bloop 将是紫色。循环会一直持续到列表末尾。

### “While”循环

有时，在编写程序时，你可能并不确切知道希望循环重复多少次。别担心！在这种情况下，你可以使用 while 循环。

#### 循环条件

while 循环包含一个问题，其答案可以是 `True` 或 `False`。这称为循环条件。只有当循环条件的答案为 `True` 时，while 循环才会开始。想象你在玩一个游戏，一座城堡由一条龙守卫，它会检查你是否有魔法钥匙。“你有魔法钥匙吗？”就是循环条件，而城堡就是循环体。如果你有魔法钥匙，循环条件为 `True`，你就可以进入城堡。但如果你没有钥匙，循环条件为 `False`，所以你就无法进入循环！

![](img/3188b147f991a51de14dcd2bb4b4c42e_39_1.png)

> 老兄，我们到底什么时候才能停下来？

![](img/3188b147f991a51de14dcd2bb4b4c42e_39_2.png)

> 没有魔法钥匙，谁也别想进来！

#### 专家提示

##### 缩进错误

就像 `for` 循环一样，`while` 循环主体中的代码必须比启动循环的那一行再缩进四个空格。如果不这样做，Python 会显示一条错误消息：“unexpected indent”。

![](img/3188b147f991a51de14dcd2bb4b4c42e_39_3.png)
