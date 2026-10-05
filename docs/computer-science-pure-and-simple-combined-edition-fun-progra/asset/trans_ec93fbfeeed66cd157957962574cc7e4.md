
第 4 步和第 5 步，编码和测试通常是混合在一起的。在开发过程的过程中，你倾向于多次编码、测试、修复和修复。现在进入你的程序页面并点击 Start（开始）。我们收到了一个错误信息！噢！我们忘记修复从 Main 对 `wander` 的调用了！这里是修改后的 `Main`：

```
to Main
repeat 60
[wander 5]
end
```

现在测试一下。噢又错了！我们的乌龟移动得太快了！我们忘记添加等待了。另外，让我们放下笔，这样我们就能看到乌龟去了哪里。既然我们已经翻译了伪代码，现在可以把它删删了。这里是修改后的 `wander`：

```
to wander :stepSize
pd
right difference random 100 50
repeat 2 [forward :stepSize wait 1]
end
```

```
to Start
Main
end
```

尝试一下。很酷！

## 练习题

- 1. 在 Main 中，调整 `stepSize`。测试一下。

- 2. 调整输入使线条更平滑。你是如何做到的？你需要如何从随机数中减去那个数字？测试一下。

- 3. 让乌龟在周围游荡时改变形状。提示：在 Main 中使用 `setsh`。在 MicroWorlds EX 中，记得先在 Shape Center（形状中心）安装一些形状。

## #19 增强版游荡乌龟

在上一节的练习中，我们调整了乌龟绘制的线条的平滑度。你还记得怎么做的吗？我们调整了 `random` 的输入。这里有一个想法：为什么不修改程序，让用户更更容易进行这种更改呢？让我们把 **random** 的输入变成一个变量。我们可以通过改变从 **Main** 传递它的数字来改变它的值，就像我们之前传递 `stepSize` 值一样。

## 重新决定目标

我们的目标是*稍微*改变乌龟前进的方向，然后朝那个“方向”迈一步。现在我们将增强这个目标。

**wander** :stepSize 的新目标是：*基于过程的参数*来改变乌龟前进的方向。参数是传递给变量的值。我们已经有一个从 **Main** 传递的参数 `stepSize` 了。我们将新的参数命名为 *dizziness*（眩晕）。我们对 **wander** 的调用将是 **wander 5**。现在它将是 **wander 5 2**，例如。第一个数字进入 `stepSize`，第二个数字进入 `dizziness`。

![](img/242aaa06c3a3208f16d97cdd92303648_111_0.png)

to wander :stepSize :dizziness 将 5 存储在 `stepSize` 中，将 2 存储在 `dizziness` 中。

这个新变量将使 **wander** 更灵活。乌龟将沿着轨道移动，或者偏离轨道，它还能做出更夸张的转弯，最终无处可去。我们需要做的是改变 **random** 的输入数字，这将改变 **right** 转的输入数字。

## 再次通过沙箱获取必要的知识

这是我们现有的 `wander`：

- wander :stepSize
- pd
- right difference random 100 50
- repeat 2 [forward :stepSize wait 1]

我们将变成参数而不是“硬编码”的数字是 100，它是 random 的输入。正是这个数字决定了乌龟方向改变的程度。然而，数字 50 与 100 绑定。记得吗，我们需要从 100 的结果中减去 50，这样乌龟的头部才能以正或负量改变。我们是如何确定数字 50 的？它是 100 的一半，或者说是 random 输入的一半。所以我们将参数除一半。

我们需要知道如何使用 Logo 将一个数字除以另一个数字。快速查看 Help Vocabulary（帮助词汇表）可以让我们发现那里没有 `divide`，但进一步查找发现了 `quotient`（商），如下所示。你在数学课上记得过，quotient 是除法题答案的雅致说法。

quotient number1 number2

报告 number1 除以 number2 的结果。见 /.

 示例：

```
show quotient xcor 10
```

我们以前在 `sum` 和 `difference` 中用过这种类型的逻辑块。为了沙箱测试，我们应该直接在 Command Center（命令中心）中输入几行，以确保我们理解它是如何工作的。尝试 `show quotient 80 2`。这就可以完成沙箱测试了。

## 再次伪代码

在伪代码步骤中，让我们在过程的第一行添加 `dizziness` 变量。让我们把这第二行伪代码作为注释。我会下划出新内容。

```
to wander :stepSize :dizziness
pd
;向右随机旋转角度，最高为 dizziness
right difference random 100 50
```

repeat [forward :stepSize wait 1]
end

## 再次代码

现在我们可以编写代码，然后再次测试它。
让我们逐步构建它。其中一种方法是创建另一个局部变量（仅在此过程中使用的变量）来存储 `dizziness` 中数值的一半。还记得如何创建和命名变量吗？我们像这样使用 `local`：

```
local "halfdizziness
```

然后我们需要将 `dizziness` 中的内容除以 2。它看起来像这样：

quotient xcor 10![](img/242aaa06c3a3208f16d97cdd92303648_113_0.png)

现在我们需要将 `dizziness` 中的内容除以 2。它看起来像这样：

quotient xcor 10![](img/242aaa06c3a3208f16d97cdd92303648_113_0.png)

现在我们需要将 `dizziness` 中的内容除以 2。它看起来像这样：

quotient xcor 10![](img/242aaa06c3a3208f16d97cdd92303648_113_0.png)

