
return 命令会退出函数，并将指定值返回——在此例中，即 'T'。

### 列表

变量只能保存单个值，但有时我们希望能够将一系列事物收集到一个列表中。你稍后将在摩尔斯电码示例中使用这个例子。Lua 列表中的项可以是任何类型的值。它们可以是数字、字符串，甚至是另一个列表。

下面的示例展示了如何定义一个颜色列表，然后一次一个地打印出来。

```lua
colors = {'red', 'orange', 'yellow',
          'green', 'blue',
          'white', 'black'}

for i, color in ipairs(colors) do
  print(color)
end
```

在此例中，列表被赋予了颜色名称的值，每个值都是字符串。for 循环使用了一个特殊命令 "ipairs"，它允许 "for" 循环同时使用列表中每个项目的位置 (i) 和颜色字符串 (color) 进行计数。

我们可以通过修改示例来证明这一点，同时打印列表中的位置和字符串，如下所示：

```lua
colors = {'red', 'orange', 'yellow',
          'green', 'blue', 'white', 'black'}
for i, color in ipairs(colors) do
  print(i, color)
end
```

这将产生如下输出：

```
1    red
2    orange
3    yellow
4    green
5    blue
6    white
7    black
```

你还可以通过方括号表示法，根据项目在列表中的位置来查找其值。尝试在 Lua 控制台中输入以下内容：

```lua
colors = { 'red', 'orange', 'yellow',
  'green', 'blue', 'white',
  'black' }
print(colors[3])
```

你会得到答案 yellow，即列表中的第三项。

你可以使用相同的 [] 表示法来更改特定项目。现在在控制台中输入以下内容：

```lua
colors[3] = "purple"
print(colors[3])
```

现在会得到答案 purple。该命令已将列表中的第三个元素从 yellow 改为 purple。

你还可以向列表中添加和移除项目。

要向列表末尾添加元素，请使用 table.insert 命令。如下面的示例所示，该示例会将颜色 gray 添加到列表末尾。

```lua
colors = { 'red', 'orange', 'yellow',
  'green', 'blue',
  'white', 'black' }
table.insert(colors, 'gray')

print(colors[8])
```

如果不想将颜色添加到列表末尾，而是想指定列表中应添加元素的位置，下面的代码将把新颜色添加到列表开头。

```lua
colors = { 'red', 'orange', 'yellow',
  'green', 'blue',
  'white', 'black' }
table.insert(colors, 1, 'gray')

print(colors[1])
```

作为 insert 的第二个参数，数字 1 表示新项目应插入到列表中第一个元素之前。

### 小结

对于一门相当复杂的编程语言来说，这是一个非常简短的介绍。不过，它应该能让你开始使用 Lua，并允许你使用 ComputerCraft 完成你想要的大多数事情。

如果你想了解更多关于 Lua 的信息，请访问官方网站 www.lua.org。

## 第四章：密码保护门

凭借我们对 Lua 和 ComputerCraft 的基础知识，我们可以开始制作一些非常酷的东西。密码保护门在服务器上非常有用，尤其是当你是唯一知道如何使用 ComputerCraft 模组的人时。

在开始这个程序之前，有一件非常重要的事情需要了解，那就是如果你的程序中有这样一行：

```lua
while true do
```

……一旦程序运行，你就无法停止它，除非你打破实际的计算机方块，或者按住 CTRL 键并按下 T。这一行在密码程序中是主要部分，因此记住 CTRL-T（用于终止）以停止程序以便编辑它非常重要，因为你可能在某个时候想要更改密码。

### 硬件

在开始编程之前，我们需要按照图 4-1 所示设置方块。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_36_0.png)

图 4-1. 密码保护门。

当然，你使用什么类型的方块或门并不重要，这只是一个示例。另外，如果你希望计算机位于门的上方或右侧，你必须将下面程序代码中使用的侧面从 "left" 改为门所在计算机的任意一侧。

你可以使用 "left"、"right"、"front"、"back"、"bottom" 或 "top"。

### 软件

控制门的程序相当短，可以轻松输入。如果你更喜欢下载包含代码的文件，可以从以下网址获取：https://github.com/simonmonk/computercraft_examples

要将此程序安装到你的 ComputerCraft 安装中，请遵循附录 A 中的说明。

```lua
while true do
  term.clear()
  term.setCursorPos(1, 1)
  print("Please enter the password:")
  password = read("*")
  if password == "password" then
    rs.setOutput("left", true)
    sleep(3)
    rs.setOutput("left", false)
  end
end
```

现在，我将逐行分解这个程序，并解释其工作原理。正如我上面提到的，`while true do` 这一行只是让程序在无限循环中运行。

```lua
term.clear()
```

这一行会在每次循环时清除屏幕。

```lua
term.setCursorPos(1, 1)
```

这会将光标位置设置在 (1, 1)，即屏幕的右上角。

```lua
print("Please enter the password:")
```

这是屏幕上显示的提示用户操作的文字。

下一行需要更多解释：

```lua
password = read("*")
```

password 是变量，必须用等号定义。命令 read 表示它正在等待输入内容，而 (*) 表示输入时，输入的内容会显示为 `*s`。请注意，这是 ComputerCraft 特有的功能，因此如果你在没有运行 ComputerCraft 的 Lua 上尝试，它可能无法工作。

```lua
if password == "password" then
```

这将查看变量 password，即我们输入的内容，而 == 表示将其与我们放在另一边的任何内容（即文本 "password"）进行比较。这意味着如果你想更改密码，就必须更改引号内的内容。该命令随后结束这一行，因此如果你输入的内容与引号内的内容（你的密码）匹配，它就会执行某些操作。

这里还有一个缩进，表示它位于 *if* 语句内部。

```lua
rs.setOutput("left", true)
```

这是说红石信号在计算机左侧开启，穿过方块，并触发门。

```lua
sleep(3)
```

这会让计算机等待 3 秒后再继续，然后 `rs.setOutput("left", false)` 会关闭计算机左侧的红石信号，从而关闭门。我个人认为让门保持开启 3 秒差不多合适，但你可以根据自己的需要更改。

最后，第一个 *end* 标记了 *if* 语句应执行内容的结束点，*then* 作为开始点，而第二个 *end* 标记了 *while true do* 循环应停止的位置。

由于这个程序只有 11 行长，你可以轻松地将其输入，但例如，下一个程序手动输入会非常繁琐，因此你也可以参考附录 A 获取下载本书所有 Lua 程序的说明。

### 小结

这是一个很好的入门小项目。你可以通过多种方式使其更复杂，例如增加最大尝试次数，或者添加一些无需编辑程序即可更改密码的选项。

在进入下一个项目（一个复杂得多的程序）之前，尽情实验和享受乐趣吧。

## 第五章：摩尔斯电码发送器

这个项目允许你在计算机中输入一条消息，然后使用红石灯以摩尔斯电码的形式闪烁显示该消息。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_40_0.png)

图 5-1. 摩尔斯电码发送器。

要构建摩尔斯电码发送器，你需要一台计算机和一个或多个红石灯。

### 硬件

使用红石将两者连接起来，根据你希望灯的距离多远，每 15 格红石就需要一个中继器。

像我这样隐藏红石的技巧是将输出设置为 bottom 而不是 left，如下面的程序代码所示。这意味着你可以根据需要轻松隐藏红石，因为它可以被其他材料覆盖。

图 5-1 展示了计算机位于红石下方的一种布置，但只要你将程序指定为连接到计算机的正确侧面，你就可以以任何你想要的方式连接它。
