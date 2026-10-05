
我们需要修改 `Main`，使其在调用 `square` 时满足 `square` 对输入的新需求。让我们给它输入数字 30。因此，我们不再输入 `square`，而是输入 `square 30`。

```
Main
cc
talkto "t1"
setsh [horse1 horse2 horse3]
repeat 20 [square 30]
end
```

现在你可以尝试运行程序了，你会发现它可以运行，但实际上并没有比以前好在哪里。我们修改后的过程 `square` 需要一个输入，并且获取了输入，但它实际上并没有将其用于任何地方！

让我们修复 `square`，让它利用变量长度。我们希望存储在 `length` 中的值被作为 `forward` 的输入。你记得怎么做吗？花一分钟思考一下。

要获取变量的值（邮箱中的内容），在变量名前加一个冒号 `:`。按照如下方式修改你的 `square` 过程。修改的部分是*斜体*：

```
square :length
repeat 4
[forward :length right 90 wait 1]
end
```

现在，为了给 `forward` 找到输入，Logo 必须找到存储在 `length` 中的值。那个值是从哪里来的？当 `Main` 使用数字调用过程 `square` 时，该值就存储在那里。

![](img/242aaa06c3a3208f16d97cdd92303648_52_0.png)

通过更改 `Main` 中的这个调用值，玩玩你新的、更强大的 `square` 吧。正式来说，这个值被称为“参数”（argument）。（我不知道为什么。我不生气，你生气吗？）在过程内部，该变量被称为形参数（parameter）。

你也可以直接从命令中心（Command Center）调用 `square`，例如通过输入 `square 200` 并按回车。

我们现在创建了一个非常好的过程，我们任何时候都可以使用。这里是我们完成的程序：

```
===========
to Main
cc
talkto "t1"
setsh [horse1 horse2 horse3]
repeat 20 [square 30]
end
=============
```

```
to square :length
repeat 4
[forward :length 90 wait 1]
end
```

```
to Start
Main
end
```

测试它！在 `Main` 中调用 `square` 的那行输入不同的值。使用 `square 40` 和 `square 60`。检查你的过程页面（Procedures Page），确保它没有错误且整洁漂亮。然后保存你的项目。

## 我们的房子大小可以改变！

我们的下一个任务是将所学的知识应用到我们制作的房子上。我们将添加能够轻松调整房子大小的功能。在 `Main` 中，我们将修改调用过程的行，以添加一个数字输入。这样，当我们点击 Start 按钮时，`Main` 将画出一个和原来一样大或两倍大的房子。如果你思考一下，你会发现这个变量的想法非常强大。它是编程的基础思想。现在你也可以做到了。

进入文件（File）-打开项目（Open Project）并加载你的房子文件。使用“另存为”（save as）将其重命名，命名为“resize house”。

要做的第一件事是取一个过程，比如 `triangle`。让我们检查它，并列出所有用于 `forward` 或 `back` 输入的数字。你可以将每个“forward”或“back”的输入数字替换为数字乘以1。例如，`forward 50` 变成 `forward 50 * 1`。（把1放在最后。这可以防止以后出现愚的错误）。注意计算机语言中的乘法符号是星号 * 而不是 x，并且输入之间有空格。

不要替换角度，即 `right`、`left` 或 `seth` 的输入。如果我们把房子放大一倍，角度保持不变。

现在我们将把所有那些1替换为一个变量（一个存储值的地方）。让我们把变量命名为 `trisize`。为了创建并命名该变量，我们将在 `triangle` 过程的第一行添加一个参数，如下：

`to triangle :trisize`

再次使用我们的邮箱图，

![](img/242aaa06c3a3208f16d97cdd92303648_54_0.png)

为 trisize 创建新邮箱

现在我们需要修改 `triangle` 过程，以便使用变量 `trisize` 而不是数字 1。

你能猜到怎么做吗？让我们试一下：

- to triangle :trisize
- draws a triangle
- repeat 3 [forward 50 * :trisize right 120 wait 1]
- end

在命令中心输入 `triangle 5`。你正在调用过程并向它传递一个值（参数）。成功了吗？哎呀，没成功！

我们忘了！在过程中，我们需要告诉计算机获取存储在 `trisize` 中的值！

- to triangle :trisize
- draws a triangle
- repeat 3 [forward 50 * :trisize right 120 wait 1]
- end

现在，用同样的方法，为 `Main` 之外的所有过程添加一个变量（你可以自己起名字）。首先在过程的第一行前用冒号加上变量名，例如 `doorsize`；将 `forward` 和 `back` 的值重置为数字 * 1，然后将 1 替换为 `:doorsize`（或其他）。不要在两个不同的过程中使用相同的变量名。这会让计算机困惑。我们希望所有的变量都是局部的——也就是说，我们只在创建它的过程内部使用该变量名。

通过在命令中心输入过程名来测试每个过程。

`square 2`
`climb.to.roof 2`
`triangle 2`
`door 2`

看看计算机是否正确画出了每一个。根据你的错误信息进行故障排除。有时 Logo 不喜欢你使用的标记。确保它们是双引号。

现在，让我们把一切整合在一起。将你的 `Main` 过程变成你调用的过程列表，每个过程旁边都输入 2，就像上面一样。

现在，按下 Start 按钮。它画出了一个两倍大的房子吗？应该是的。

你可以修改 `Main` 画出一个只有只有一半的房子吗？提示：使用 0.5 表示一半；这意味着五十分之一，也就是二分之一。

向你的老师展示你半大小的房子和双倍大的房子吧！

额外加分练习：

为 `Main` 创建一个变量，包含用于重新调整所有组件的值。
提示：`Main` 的第一行看起来是：`to Main :housesize`。要向变量放入值，直接从命令中心调用 `Main`，例如：`Main 2`。

## #11 执行 Logo 步行

现在，让我们多做一些动画。我想开发一个名为 `walk` 的过程。从文件菜单中，打开你之前课程保存的名为 `Square1` 项目。然后从文件菜单选择“另存项目”（Save Project As）并将项目保存为 `Walk`。记住，这是小马在隐形正方形中慢跑的项目。在过程页面上，你的程序应该像这样：

```
to Main
  cg
  cc
  pu
  talkto "t1"
  setsh [horse1 horse2 horse3]
  repeat 20
    [square 30]
end
```

```
to square :length
  repeat 4
    [forward :length right 90 wait 1]
end
```

```
to Start
  Main
end
```

## 我们的方法

我们将尝试创建一个 `walk` 过程。我们先对要做的事情有一个大致的想法，但我们将根据哪些可行、哪些不可行，一点地构建这个过程。过程中我们会犯错，并从中学习，利用它们来让我们的过程更好。

在完成 `walk` 之后，我想做 `jump`。最终，我想让小生物沿着路径行走并跳过障碍。

## 你是如何行走的？

在 `Main` 中，编辑 `setsh` 行使其看起来像这样：

```
setsh [dog1 dog2]
```

将形状 `dog1` 和 `dog2` 安装到你的形状中心（Shape Center）中。确保它们面向左侧。要改变它们的朝向，双击形状中心中的形状，然后点击翻转图标。

在开始编写 `walk` 过程之前，让我们实际坐下来思考一下。我设想乌龟在移动时在形状之间切换。这意味着 `forward` 过程必须被多次调用。我们会调用它两次，每个形状一次，然后重复该序列。我们应该包含一个 `wait` 命令来减慢动作，让我们能看到。

`walk` 需要什么输入？我们把什么设为变量？嗯，在改变形状之前将移动作为过程的输入怎么样？

好了，思考够了，写代码吧！

在命令中心输入 `cg` 清除图形，以便我们可以从头开始。然后在你的过程页面输入此过程。

```
to walk :stepsize
repeat 2
[forward :stepsize
wait 1]
end
```

并修改 `Main` 使其看起来像这样：

```
to Main
cg
cc
pu
talkto "t1"
setsh [dog1 dog2]
repeat 200
[walk 5]
end
```
