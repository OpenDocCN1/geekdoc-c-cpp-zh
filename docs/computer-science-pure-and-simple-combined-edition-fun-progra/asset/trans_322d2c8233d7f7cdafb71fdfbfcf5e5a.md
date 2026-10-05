

## to Main

talkto "t1"
launch [repeat 2000 [forward 3 direct reach ||
when [touching] "t1 [t2] [win]
waituntil [colorder = 15]
announce [You lose!]
reset
end

to direct:key
if (ascii:key) = 28 [seth 270 0 fd 1]
if (ascii:key) = 29 [seth 90 0 fd 1]
if (ascii:key) = 30 [seth 0 0 fd 1]
if (ascii:keykey) = 31 [seth 180 0 fd 1]
if (ascii:key) = 37 [seth 270 0 fd 1]
if (ascii:key) = 39 [seth 90 0 fd 1]
if (ascii:key) = 40 [seth 180 0 fd 1]
if (key = "s") [stopall]
end

to go
to Main
announce [You win!]
talko "t1"
setsh cloud wait 2
setsh random 10 wait 10
end

to reset
talko "t1"
setpos [-319 -164]
end

+ 4. 将 win 修改为此处，添加下划线：
to win
announce [You win!]
talko "t1"
setsh cloud wait 2
setsh random 10 wait 10
end

将 win 修改为，添加下划线：
to reset
talko "t1"
setpos [-319 -164]
seth 0
setsh 0
end

+ 5. 添加流程图来描述我们目前的内容：

![](img/242aaa06c3a3208f16d97cdd92303648_196_0.png)

## to Main

local "preference"
announce "t1" 如果你去城堡，你将变成一个男人。
question [你想成为王子还是公主？B 代表男孩，女孩 代表城堡]
else (answer = "B") make "preference" [41]
talko "t1"
launch [repeat 2000 [forward 3 direct reach ||
when [touching] "t1 [t2] [win "preference]
waituntil [colorder = 15]
announce [You lose!]
end

> 王子项目：游戏询问用户想成为王子还是公主，乌龟在进入城堡时会变成男孩或女孩。如果你有 MicroWorlds EX，男孩形状会变成空白数字 41，女孩形状会变成数字 40。如果你有 MicroWorlds 2.0，请使用 clear 代替 lightning！

to direct:key
if (ascii:key) = 28 [seth 270 0 fd 1]
if (ascii:key) = 29 [seth 90 0 fd 1]
if (ascii:key) = 30 [seth 0 0 fd 1]
if (ascii:key) = 31 [seth 180 0 fd 1]
if (ascii:key) = 37 [seth 270 0 fd 1]
if (ascii:key) = 39 [seth 90 0 fd 1]
if (ascii:key) = 38 [seth 0 0 fd 1]
if (ascii:key) = 40 [seth 180 0 fd 1]
if (key = "s") [stopall]
end

to gender
announce [You win!]
talkto "t1"
setsh "lightning1w wait 2
setsh "gender wait 10
reset
end

to go
Main

to reset
talko "t1"
setpos [-319-164]
seth 0
setsh 0
end

## #22 迷宫 III

to Main
talkto "t1"
launch [repeat 2000 [forward 3 direct reach | ]]

talkto "t3"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]

talkto "t4"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]
when [colourander = 15] [lose]
when [touching?] "t1" [t2] [win]
when [touching?] "t1" [t3] [lose]
when [touching?] "t1" [t4] [lose]
end

```
to direct :key
if (ascii:key) = 28 [set 270 fd 1]
if (ascii:key) = 29 [set 90 fd 1]
if (ascii:key) = 30 [set 0 fd 1]
if (ascii:key) = 37 [set 270 fd 1]
if (ascii:key) = 39 [set 90 fd 1]
if (ascii:key) = 38 [set 0 fd 1]
if (ascii:key) = 40 [set 180 fd 1]
end
```

to go
Main

to win
announce [You win!]
talkto "t1"
setsh cloud wait 2
setsh 60 wait 10
reset

to reset
talkto "t1"
setpos [-319-164]
seth 0
setsh 0
end

to lose
announce [You win!]
wait 5
reset
end

## #23 迷宫 IV

to easy
talkto "t1"
launch [repeat 2000 [forward 3 direct reach ]]
talkto "t3"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]

talkto "t4"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]
when [colourander = 15] [lose]
when [touching?] "t1" [t2] [win]
when [touching?] "t1" [t3] [lose]
when [touching?] "t1" [t4] [lose]
end

to medium
talkto "t1"
launch [repeat 2000 [forward 3 direct reach ]]
talkto "t3"
launch [repeat 2000 [forward 3 wait 2]]
when [colourander = 15] [right 190]

talkto "t4"
launch [repeat 2000 [forward 3 wait 2]]
when [colourander = 15] [right 190]
end

to hard
talkto "t1"
launch [repeat 2000 [forward 3 direct reach ]]
talkto "t3"
launch [repeat 2000 [forward 4 wait 2]]
when [colourander = 15] [right 190]

talkto "t4"
launch [repeat 2000 [forward 4 wait 2]]
when [colourander = 15] [right 190]
when [colourander = 15] [lose]
when [touching?] "t1" [t2] [win]
when [touching?] "t1" [t3] [lose]
when [touching?] "t1" [t4] [lose]
end

## [touching?] "t1" "t4" [lose]

1. 添加传送门。在这里：在迷宫中放置另一个颜色的方块。当乌龟进入时，它会跳转到迷宫的另一个位置。要找到你想到达的位置坐标，移动鼠标，然后在 Command Center 显示 pow。
```
if (ascii :key) = 28 [set 270 0 fd 1]
if (ascii :key) = 29 [set 90 0 fd 1]
if (ascii :key) = 30 [set 0 0 fd 1]
if (ascii :key) = 31 [set 180 0 fd 1]
if (ascii :key) = 37 [set 270 0 fd 1]
if (ascii :key) = 39 [set 90 0 fd 1]
if (ascii :key) = 38 [set 0 0 fd 1]
if (ascii :key) = 40 [set 180 0 fd 1]
if (key = :stop) [stopall]
```

在你的 medium 迷宫某处创建一个蓝色方块（color = 95）。Medium 将包含此部分，并带有新的下划线：
+ talkto "t1"
when [color = 15] [lose]
when [color = 95] [set 18–16]
when [touching?] "t2" [win]

2. 使用形状列表并设置重复调用 forward 创建动画：
让乌龟在到达目标时播放动画。确保 Shape Center 中有用的形状。下划线部分：
to win
+ announce "You win!"
talkto "t1"
setsh "cloud wait 2
setsh random 60 10
setsh 90
repeat 10 [forward 1 wait 1]
reset
end

to easy
Maineasy
end

to hard
Mainhard
end

to index
Page1
end

to lose
+ announce "You lose!"
wait 5
reset
end

to medium
Mainmedium
end

to reset
+ talkto "t1"
setpos |319-164|
set 0
set 0
end

to win
+ announce "You win!"
talkto "t1"
setsh "cloud wait 2
setsh random 60 10
reset
end

为蜘蛛（t3 和 t4）在移动时创建一个动画，使其动作更真实。确保 Shape Center 中有用的形状。我将在 MicroWorlds EX 中使用 bird1 和 bird2，在 MicroWorlds 2.0 中使用 bee 和 bee2。下划线部分：
+ to Maineasy
talkto "t1"
launch [repeat 2000 [forward 3 direct reach]]
talkto "t3"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]

talkto "t4"
launch [repeat 2000 [forward 3 wait 3]]
when [colourander = 15] [right 190]

让乌龟在移动时播放动画。
+ talkto "t1"
launch [repeat 2000 [forward 3 direct reach]]

