

# 创建模块块

为了避免重复使用同一组模块块，可以通过创建新的模块块来简化径。每个新模块块都可以包含几个不同的指令。

# 创建你自己的模块块

你可以在 Scratch 中创建自己的模块块，它们在被使用运行时运行脚本。尝试这个示例来查看它们是如何工作的。程序员可以使用这些可重用的代码段作为“子程序”或“函数”。

- **创建一个新模块块**
点击“更多模块”（More Blocks）按钮，选择“建立模块块”（Make a Block）。输入单词“jump”并点击“确定”。

- **新模块块出现**
你的新模块块“jump”出现在模块面板中，脚本区域会出现一个“定义”（define）模块块。

![](img/72d218a7a73c4d4abc7be582ebd85385_73_0.png)

| 脚本 (Scripts) | 造型 (Costumes) | 声音 (Sounds) |
|---|---|---|
| 动作 (Motion) | 事件 (Events) | |
| 造型 (Looks) | 控制 (Control) | |
| 声音 (Sound) | 侦测 (Sensing) | |
| 笔画 (Pen) | 运算符 (Operators) | |
| 数据 (Data) | 更多模块 (More Blocks) | |

![](img/72d218a7a73c4d4abc7be582ebd85385_73_1.png)

点击此处创建新模块块

- **定义模块块**
“定义”块告诉 Scratch 在使用新模块块时运行哪些模块。添加此脚本来定义该模块块。

- **在脚本中使用模块块**
现在新模块块可以在任何脚本中使用。这就像是把跳跃块单独存在于脚本中一样。

```
define jump
change y by 50
wait 1 secs
change y by -50
```

```
when clicked
forever
jump
wait 1 secs
```

开始你的模块定义

向上跳跃

新模块块运行已经定义的跳跃脚本

向下掉

在重复循环之前等待 1 秒

# 带有输入内容的模块块

新模块块中的窗口可以给它提供数字和单词进行处理。这些空位可以用来改变角色移动的距离。

![](img/72d218a7a73c4d4abc7be582ebd85385_74_0.png)

点击此处查看所有选项

- **创建一个新模块块**
创建一个名为 'slide' 的新模块块，然后点击“选项”（Options）：选择“添加数字输入”并输入“steps”。选择“添加标签文本”并将其改为“and shout”。点击“添加字符串输入”并将其命名为“greeting”。然后点击“确定”。

- **定义模块块**
在“定义”块中，空位被名为 'steps' 和 'greeting' 的变量取代。将变量从“定义”块拖入到脚本中任何你需要的地方。将此内容添加到角色的脚本中。

![](img/72d218a7a73c4d4abc7be582ebd85385_74_1.png)

steps 变量

greeting 变量

> 从“定义”块中将变量拖入脚本中

- **在脚本中使用模块块**
现在向角色添加以下脚本。通过向模块块输入不同的步数和问候，你可以让你的角色表现得不同。

![](img/72d218a7a73c4d4abc7be582ebd85385_74_2.png)

此块使步数变为负数

> 为新模块块起一个合理的名称，这样程序将更容易阅读和修改。

```
when space key pressed
slide 20 and shout hello
wait 1 secs
slide 80 and shout how's it going?
```

按下空格键时启动脚本

角色滑动 20 步并大喊“hello”

现在角色滑动 80 步并大喊“how's it going?”

# 猴子大乱 (Monkey mayhem)

这个令人兴奋、节奏快速的游戏结合了你目前学的所有 Scratch 技能。按照这些步骤创建你自己的“猴子大乱”，看看是否能击中蝙蝠！

# 开始

启动一个新的 Scratch 项目。猫角色不适合这个项目。要删除它，在角色列表中右键点击它并选择“删除”。这将留下一个空白项目供你操作。

- 从背景库添加一个新的背景。此按钮位于角色列表的左侧。

舞台背景

背景

点击此处从背景库添加新背景

新背景：

- 双击选择“wall1”背景。砖墙背景适合这个游戏，但如果你更喜欢，可以使用不同的背景。

> 另：40–41 造型
38–39 让物体移动
66–67 侦测与检测

# 专家技巧

# 避免错误

这是你为止尝试过的最大的 Scratch 程序，因此你可能会发现游戏运行并不如预期。这里有一些提示可以让运行得更顺畅：

- 确保将脚本添加到正确的角色上。
仔细遵循说明。在使用它之前记得创建一个变量。
- 检查模块中的所有数字是否正确。

![](img/72d218a7a73c4d4abc7be582ebd85385_75_0.png)

- 双击背景库中的背景使其出现在舞台上

# 猴子大乱

前往角色库为游戏添加新角色。从“动物”部分选择“Monkey1”。用户将控制这个角色。

| 角色 (Sprites) | 新角色 (New sprite:) |
|---|---|
| Monkey1 | |

点击此处从库中选择新角色

为猴添加下面的脚本。记住——所有模块可以在面板面板找到，按颜色分类。使用“侦测”块通过箭头键移动猴。完成后运行脚本进行检查。

> 这个“动作”块保持猴直立

键盘上的箭头键会让猴向左向右

- when clicked
set rotation style left-right
go to x: 0 y: (-90)

将猴移动到舞台底部起始位置

此“侦测”块检测左箭头

- if arrow pressed?
point in direction (-90)
move 10 steps
next costume

90 让猴向左

通过切换造型让猴看起来像在走路

- if arrow pressed?
point in direction (90)
move 10 steps
next costume

90 让猴向右

移动猴 10 步

不要忘记保存你的工作

# 从 Scratch 开始

# 猴子大乱

# 添加更多角色

现在可以使用左右键让猴穿过舞台。为了让游戏更有趣，添加一些角色。给一些香蕉去扔，给一只蝙蝠来扔它们！

![](img/72d218a7a73c4d4abc7be582ebd85385_77_0.png)

从角色库添加“Bananas”角色，然后给它脚本。游戏开始时，猴会隐藏香蕉。按下空格键时，它们将垂直射向上舞台。香蕉随后出现在舞台的一侧，可以再次捡起。

```
when clicked
  set rotation style left-right
point in direction 0
forever
  repeat until
    go to Monkey 1
    key space?
  repeat 35
    move 10 steps
  if
    pick random 1 to 2 = 1
    go to x: 210 y: -140
  else
    go to x: -210 y: -140
  show
wait until
  touching Monkey 1
```

这让香蕉保持直立

将香蕉的方向设置为向上

此块让香蕉在舞台上可见——稍后会被隐藏

在按下空格键之前，香蕉粘在猴身上

此循环让香蕉向上移动舞台

此“if-then-else”块让香蕉随机出现在舞台的右侧或左侧

这让脚本等待直到猴捡起香蕉

![](img/72d218a7a73c4d4abc7be582ebd85385_77_1.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_77_2.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_77_3.png)

# 猴子大乱

下一步是添加一只飞行蝙蝠，如果它击中了香蕉，就让它落在地上。从角色库添加“Bat2”，然后创建一个名为“Speed”的新变量（仅限蝙蝠）。要创建新变量，首先点击模块面板中的“数据”按钮，选择“建立变量”按钮。使用“数据”部分“Speed”变量旁边的复选框，它就不会出现在屏幕上。

| 新变量 | 为新变量命名 |
|---|---|
| 变量名: Speed | 此变量将仅用于蝙蝠 |
| 所有角色 | 仅限此 |
| 云变量（存储在服务器上） | OK 取消 |

将以下脚本添加到蝙蝠。在主“循环”循环中，蝙蝠移动到舞台左侧的随机位置，在舞台上移动直到香蕉击中它。当蝙蝠被击中时，它掉落在地上。

![](img/72d218a7a73c4d4abc7be582ebd85385_78_0.png)

```
when clicked
  set rotation style [left-right]
  forever
    go to x: [pick random (1) to (100)] y: [pick random (1) to (20)]
    point in direction [90]
    set [Speed] to
    repeat until [touching Bananas ?]
      move [Speed] steps
      if on edge, bounce
  broadcast [hitbybananas]
  point in direction [180]
  repeat [40]
    move [10] steps
```

> 这让蝙蝠角色直立

> 蝙蝠从舞台左侧开始，高度随机

> 设置蝙蝠的方向向右

> 随机选择一个速度

> 这让蝙蝠移动直到被击中

> 从“数据”部分将“Speed”变量拖入此块

> 创建此“广播”块以告诉其他角色蝙蝠被击中了。这将在项目的以后使用。

> 设置蝙蝠的方向向下

> 让蝙蝠掉落并离开舞台

![](img/72d218a7a73c4d4abc7be582ebd85385_78_1.png)

