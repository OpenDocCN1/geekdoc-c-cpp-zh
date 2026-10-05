

end

repeat 200

to Start

[walk 10 10]

Main

1

end

to colorCyanHit

to walk :fontsize :qsteps

doJump 80 200

repeat :qsteps

poof

[forward :fontsize wait 1]

wait 5

end

unpoof

# 练习 2

end

将 Main 修改：

to colorGrayHit

to Main

doJump 50 100

ce eg pu

end

talkto :t4

to doJump :height :distance

talkto :t1

local :originalY

setsh [horse1 horse2 horse3]

make sety cumor :height

setth 90

wait 1

repeat 200

forward :distance

[Walk 10 10]

wait 1

end

setY originalY

# 练习 3

end

将 Main 修改：

to jump

repeat 200

doJump 30 30

[Walk 2 8]

to poop

# 练习 4

将 walk 修改：

talkto :t4

to walk :fontsize :qsteps

setsh "cloud or "lightning2"

repeat :qsteps

end

sets sum xor :sksteps

to Start

wait 1

Main

end

to unproof

(注意：如果没有 forward，动物看起来就不再在移动了。)

talkto :t4

setsh :castle

# #13 建议答案

end

ex. 1 & 2. 添加两只乌龟；安装 tornado1 和 tornado2 形状，以及 lightning2。点击它为它设置一个城堡（castle）形状。编写程序使颜色对 colorCyanHit 响应。在城堡附近喷一些青色漆。

to Main

ce eg pu

talkto :t2

setsh [dog1 dog2]

setth 270

launch

repeat 200

[Walk 10 10]

talkto :t3

setsh [skater1 skater2 skater3]

setth 90

launch

repeat 200

ex. 3
使用绘图中心和粗灰色线画一个螺旋形迷宫。编写程序使灰色对 colorGrayHit 响应。
这里是迷宫的一种可能，也是最好的——你能做得更好吗？

# to Main

```
cc
talkalkto "t1"
setsh 0
repeat 2000 [ forward 1 ]
```

```
to colorGrayHit
back 3 wait 1
right random 270
wait 1
forward 3 wait 1
end
```

```
to Start
Main
end
```

# # 附录 III

# # 第 2 部分答案

# #15 MADLIBS 答案

所有的打印句子组合都将有效。请确保你先在第 1 页写一段文本。

伪代码

to madlibs
:Create 请求用户输入一个动物的名称。
:将动物名称存储在名为 noun1 的变量中。
:询问用户一个对象的名称。
:将此存储为 noun2。
:询问用户他或她喜欢做的事情。
:将其存储为 noun3。
:请求用户描述一种感觉。
:将此存储为 adj1。
:请求一个副词。

代码

```
local [noun1 noun2 noun3 noun4 adj1 adj1v1]
question [请输入一个动物的名称.]
make "noun1 answer"
question [请输入一个对象的名称.]
make "noun2 answer"
question [请输入你喜欢做的事情.]
make "noun3 answer"
question [请描述一种感觉。]
make "adj1 answer"
question 给我一个副词，例如缓慢地、快速地、重地等。
announce 这是你的 Madlib。
print (sentence [ 曾经有一个 :noun1 ])
print (sentence [ 有一天那个 :noun1 ])
print (sentence [ 去了公园并看到一个 :noun2 ])
print (sentence [ :noun1 吃了 :noun2 然后 ])
print (sentence [ 去进行了一次 :noun3 ])
print (sentence [ 在此之后 :noun1 有一种像 adj1 一样的感觉 ])
print (sentence [ :adj1 的 :noun1 ])
print (sentence [ 回到家坐在屋顶上。])
```

end

to Start
Main
end

#16 MADLIBS 答案

to Main
intro
end

to intro

question [你叫什么名字？]; 弹出一个对话框
ann [ 我喜欢你的名字。]; 不带空格的对话
question [你想玩 Madlibs 吗？或者 N
if (answer = "Y") [madlibs]
announcement "再见!"
end
to madlibs
local [noun1 noun2 noun3 noun4 adj1 advv1]
question [请输入一个动物的名称.]
make "noun1 answer"
question [请输入一个对象的名称.]
make "noun2 answer"
question [请输入你喜欢做的事情.]
question [请描述一种感觉。]
make "adj1 answer"
question [给我一个副词，例如缓慢地、快速地、重地等。
announce [ 这里是你的。
print (sentence [ 曾经有一个 :noun1 ])
print (sentence [ 有一天那个 :noun1 ])
print (sentence [ 去了公园并看到一个 :noun2 ])
print (sentence [ :noun1 吃了 :noun2 然后 ])
print (sentence [ 去进行了一次 :noun3 ])
print (sentence [ 在此之后 :noun1 有一种像 adj1 一样的感觉 ])
print (sentence [ :adj1 的 :noun1 ])
print (sentence [ 回到家坐在屋顶上。])
end

现在，确保你添加 Main 和 Start 以得到完整的程序。to Main
madlibs

to Main
EXERCISE 1
to intro
question [你叫什么名字？]; 弹出一个对话框
ann [ 我喜欢你的名字。]; 不带空格的对话
question [你想玩 Madlibs 吗？或者 N
if (answer = "Y") [madlibs]
announcement "再见!]
end

# 练习 2, 带有 JIG 的猜测游戏：

to Main
oneq
to intro
question [你叫什么名字？]; 弹出一个对话框
announcement [我喜欢你的名字。] 不带空格的对话
question [你想玩猜测游戏吗？Y 或 N
else (answer = 'y') [oneq] [announcement [再见!]]
end
to oneq
local "quiznumber"
make "quiznumber 4"
question (输入一个 0 到 10 之间的数字.)
if (answer > quiznumber) [announcement [太大了!]]
if (answer < quiznumber) [announcement [太小了!]]
if (answer = quiznumber) [announcement [你对了!]]
print (sentence [ 数字是]: :quiznumber)
end

to Start
Main
if (answer > quiznumber) [announcement [太大了!]]
if (answer < quiznumber) [announcement [太小了!]]
if (answer = quiznumber) [jig]
print (sentence [ 数字是]: :quiznumber)
end

#18 漫游乌龟答案

to Main
repeat 60

end

to :stepSize
turn right by a random amount
right 100 50
move forward by stepSize, twice
repeat 2 [for:stepSize wait 1]
end

to Start
end

# #17 使用变量的动画

练习 2, 带有 JIG 的猜测游戏：

to Main
intro
end

to intro
question [你叫什么名字？]; 弹出一个对话框
announcement [我喜欢你的名字。] 不带空格的对话
question [你想玩猜测游戏吗？Y 或 N
else (answer = 'Y') [oneq] [announcement [再见!]]
end

to jig
announcement [你对了!]
talkto "ti"
pd
repeat 30 [fd 2 wait 1 right 10 wait 1 25]
end

to oneq
local "quiznumber"
make "quiznumber 4"
question (输入一个 0 到 10 之间的数字.)

to Main
setsh [horse1 horse2 horse3]
repeat 60 [wander 5]
end

to Start
end

1. 调整 stepSize。将 wander 5 改为任意值。
2. 调整输入使线条平滑。怎么做？将输入改为随机。你想调整数字吗？设置为随机。例如，difference 100 50 可以变成 difference 40 20
3. 让乌龟在漫游时改变形状。提示：在 Main 中使用 set。见下文。

to :stepSize
pd
turn right by a random amount
right 100 50
move forward by stepSize, twice
repeat 2 [for:stepSize wait 1]
end

# # #19 增强漫游乌龟答案

练习 5
to wander :stepSize :dizziness

```
; turn right by a random amount could be negative
; turn right by a random amount up to dizziness
right difference :dizziness quotient: :dizziness 2
n; move forward by stepSize, repeat twice
repeat 2 :stepSize wait 1
```

#21 迷宫 II：赢还是输？

基础迷宫
创建一个标记为“go”的按钮。使用绘图中心（画笔图标下方）的粗线画一个迷宫。确保你使用的颜色标记为 15；请将鼠标悬停在绘图中心的颜色上。

to Main
talko "t1"
launch [repeat 2000 [forward 3 direct leadcar || ]
waituntil [colorunder = 15]
announce [你输了!]
reset
end

```
to direct key
if (ascii:key) = 28 [set 270 fd 1]
if (ascii:key) = 29 [set 90 fd 1]
if (ascii:key) = 30 [set 0 fd 1]
if (ascii:key) = 31 [set 180 fd 1]
if (ascii:key) = 37 [set 270 fd 1]
if (ascii:key) = 39 [set 90 fd 1]
if (ascii:key) = 38 [set 0 fd 1]
if (ascii:key) = 40 [set 180 fd 1]
if (key = "s") [stopall]
```

end

to go
Main
talko "t1"
setpos [-319 -164]
set 0
end

练习题：

1. 使用乌龟填充线按钮在迷宫的终点放置一只新乌龟。这是 t2。
2. 在下划线处，并在你的形状中心添加一个 dog 形状
你有 Micro Worlds EX。

to Main
talko "t1"
launch [repeat 2000 [forward 3 direct leadcar || ]
when [touching :"t2" [set "dog" ]]
waituntil [colorunder = 15]
announce [你输了!]
reset
end

流程图添加：

![](img/242aaa06c3a3208f16d97cdd92303648_195_0.png)

3. 在 MicroWorlds 中，你需要从绘图中心的单形状列表中为形状中心构建一个城堡和一个云朵（在花朵图标下的裁剪窗口中）。点击按钮然后点击 T2 将形状更改为城堡。

乌龟1碰到城堡时改变形状：
在你的形状中心的前9空白处添加一些形状。这样我们就可以使用 random 10 来更改形状，并从那9个形状中随机选择一个。

