

```
i = -50
For s in spheres do
(
    s.position = [i,i,i]
    i = i + 10
)
```

研究这个脚本，确保你理解其含义。你使用一个 for 循环来处理球体集合中的每个球体。对于每一个球体，你将其位置设置为 [i, i, i]，然后改变 i 的值，以便下一个球体位于不同的位置。

## 函数

你将了解的基本 MAXScript 的最后一个特性是函数。函数是 MAXScript 中的小片段，它们像程序构建块一样工作。例如，假设你在编写脚本时需要多次计算一组数字的平均值。实现此功能的 MAXScript 可能如下：

```
Total = 0
Count = 0
For n in numbers do
(
    total = total + n
    count = count + 1
)
average = total / (count as float)
```

给定一个名为 numbers 的数字集合，这段 MAXScript 计算平均值。不幸的是，每次需要计算平均值时，你都必须重新输入所有这些 MAXScript。或者你可能很聪明，每次需要时直接剪切并粘贴。然而，你的脚本很快就会变得庞大且杂乱，而且你总是需要修改脚本以匹配你正在计算平均值的集合名称。

函数解决了你的问题。在脚本的开头，你可以定义一个 average 函数，如下所示：

```
Function average numbers =
    ( -- 用于计算集合中数字平均值的函数
    local Total = 0
    local Count = 0
    For n in numbers do
    (
        total = total + n
        count = count + 1
    )
    total / (count as float)
)
```

现在，无论何时你需要在脚本中计算任何数字集合的平均值，你都可以使用这个函数来获取名为 num 的集合中的所有数字，并将其平均值存储在名为 Ave 的变量中：

```
Ave = average num      -- 假设 num 是一个集合
```

这不仅使你的脚本在需要频繁计算平均值时变得更短，而且使其更具可读性。对于普通读者来说，很明显你正在计算一些数字的平均值。此外，如果你后来意识到你编写的 average 函数有误，你只需在脚本顶部修复它即可。

## 第十二部分：MAXScript 和插件

脚本。如果你不使用函数，你将不得不遍历脚本，找到每个计算平均值的地方，然后修复问题。（真是头疼！）

现在再看一下函数定义。第一行

```
Function average numbers =
```

告诉 Max 你正在创建一个名为 average 的新函数。它还告诉 Max，要使用这个函数，你必须传入一条数据，并且在函数内部，你使用一个名为 numbers 的变量来引用该数据。调用函数时实际变量的名称无关紧要；在函数内部，你只需将其称为 numbers 即可。

创建使用多条数据的函数也很容易。例如，

```
Function multEm a b c = (a * b * c)
```

创建一个将三个数字相乘的函数。要使用此函数将三个数字相乘并将结果存储在名为 B 的变量中，你只需输入

```
B = multEm 2 3 4
```

接下来的两行

```
local Total = 0
local Count = 0
```

创建两个变量并将它们都设置为 0。local 关键字告诉 Max 该变量属于此函数。函数外部的脚本部分无法看到此变量，并且如果函数外部存在同名变量，在函数内部更改该变量不会影响函数外部的该变量。这样，你永远不必担心有人调用 average 时使用了哪些其他变量；即使存在名为 Total 或 Count 的变量，它们也不会受到影响。

最后一行

```
total / (count as float)
```

## 教程：创建一群鱼

让我们看一个示例，将本章中学到的一些知识付诸实践。在这个多部分教程中，你将使用 MAXScript 创建一小群鱼，它们跟随一个虚拟对象沿路径移动。

## 第 1 部分：让鱼跟随路径

在本教程的这一部分，你将使用 MAXScript 将其中一条鱼沿场景中的路径移动。为此，请按照以下步骤操作：

- 1. 从 DVD 上的 Chap 49 目录打开 Fish scene.max 文件。
- 该场景由两条鱼和一个沿路径移动的虚拟对象组成。你需要做的是使用 MAXScript 创建一小群鱼，它们跟随虚拟对象沿路径移动。

- 2. 按 F11 打开 MAXScript 侦听器窗口。在窗口中，选择“文件”⇨“新建脚本”以打开 MAXScript 编辑器窗口，并输入以下脚本：

## 第 49 章：使用 MAXScript 实现自动化

```
pathObj = $Dummy01
fishObj = $Fish1/FishBody
relPos = [0,-150,-50]   -- 鱼与路径的接近程度

animate on
(
    for t = 1 to 100 do at time t
    (
        fishObj.position = pathObj.position + relPos
    )
)
```

3. 选择 Camera01 视口。选择“工具”->“全部计算”（或按 Ctrl+E）来计算编辑器窗口中的所有 MAXScript，右键单击 Camera01 视口以将其激活，然后点击“播放动画”按钮。
鱼严格跟随虚拟对象的路径。图 49.15 显示了此动画的一帧。

# 图 49.15

首次尝试让鱼跟随路径

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1246_0.png)

现在你将解释上一个教程中输入的 MAXScript。前几行创建了脚本其余部分使用的一些变量。pathObj 指定鱼将跟随的对象的名称，fishObj 是鱼身体的名称。（请注意，你可以通过使用对象名称、正斜杠和子部分来引用组层次结构中的部分。）为什么要为鱼对象创建变量？在第一条鱼工作正常后，你想将相同的脚本应用于另一条鱼。你只需将 Fish1 重命名为 Fish2，重新执行脚本，就完成了！

脚本还创建了一个名为 relPos 的变量，用于引用鱼相对于虚拟对象的位置。如果场景中有多条鱼，你不希望它们都在完全相同的位置，因此这是一种轻松定位每条鱼的方法。

下一个 MAXScript 块是新的：你正在使用 animate on 构造。这告诉 Max 为你的动画生成关键帧。这与你按下 Max 的动画按钮、运行脚本然后关闭动画相同。因此，animate on 括号内的任何 MAXScript 都会创建动画关键帧。这些括号定义了你称之为块的脚本部分。

在动画块内部，你有一个从 1 到 100 计数的循环（对应于动画的每一帧）。在循环行的末尾，你有 at time t，它告诉 Max 每次循环时，你希望所有变量具有该时间点的值。例如，如果你希望鱼跟随虚拟对象，你必须知道对象在每个时间点的位置，而不仅仅是在开始时；因此每次循环时，Max 都会为你计算出虚拟对象的位置。

在循环内部，你将鱼对象的位置设置为虚拟对象（在该时间点）的位置，然后通过 relPos 调整鱼的位置。

## 第 2 部分：添加身体旋转和尾巴动画

接下来，你将通过动画化鱼的尾巴并使其旋转身体以实际跟随路径，让鱼看起来更逼真。此外，你还会为其运动添加一点不可预测性，这样当你添加其他鱼时，它们不会完全相同。

要改进鱼的动画，请按照以下步骤操作：

- 1. 输入脚本的修订版本（新行以粗体显示）：

```
pathObj = $Dummy01
fishObj = $Fish1/FishBody
fishTail = $Fish1/FishBody/FishTail
relPos = [0,-150,-50]  -- 鱼与路径的接近程度

fishTail.bend.axis = 0  -- 0 是 x 轴
zadd = 4  -- 每一步的垂直移动量
tailFlapOffset = (random 0 100)
tailFlapRate = 25 + (random 0 25)
animate on
(
for t = 0 to 100 do at time t
(
fishObj.position = pathObj.position + relPos
fishObj.position.z = relPos.z
relPos.z += zadd

-- 假设有 10% 的几率鱼会
-- 改变垂直方向
if ((random 1 100) > 90) then
(
zadd = -zadd
)

fishTail.bend.angle = 50 * sin (t * tailFlapRate +
tailFlapOffset)
)
```

