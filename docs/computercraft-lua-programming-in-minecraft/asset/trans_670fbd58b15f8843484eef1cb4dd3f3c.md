
向其他计算机发送无线网络命令，从而控制活塞或红石灯。可能性无穷无尽！

## 第7章：Minecraft中的推特

我们觉得，在玩Minecraft时能够阅读推文会很酷。在这个项目中，你不仅可以阅读推文，还可以设置在收到推文时通过红石激活活塞来通知你。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_50_0.png)

图7-1. Minecraft中的推特

当活塞被激活、你得知有推文到达后，就可以去计算机的控制台上查看它（图7-2）。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_50_1.png)

图7-2. 在Minecraft中阅读推文

### 硬件

你可以按任何方式使用计算机发出的红石信号，但在上述布局中，红石控制一个活塞，在收到推文时露出一个萤石块（图7-3）。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_51_0.png)

图7-3. 新推文到达后

### 代码

要让程序运行，首先必须启用ComputerCraft的网页访问功能。为此，你需要使用TextPad或NotePad等编辑器打开“minecraft/config”文件夹中的“ComputerCraft.cfg”文件，并将以下代码从：

```
enableapi http {
    general=false
}
```

改为：

```
enableapi http {
    general=true
}
```

然后在同一个文本文件中继续向下找到：

```
EnableAPI_http=false
```

改为：

```
EnableAPI_http=true
```

完成这些修改后，再次保存文件并重启Minecraft。

代码使用Twitter API从指定的推特用户名获取最新推文，因此你可能想更改第一行，使其指向你自己的推特用户名。

```
name = "Simonmonk2"
```

```lua
page = "http://api.twitter.com/1/statuses/" ..
       "user_timeline.xml?screen_name=" .. name ..
       "&count=1"
old_text = ""

while true do
    tweet_page = http.get(page)
    response = tweet_page.readAll()
    tweet_page.close()
    start_of_tag = string.find(response,
                     "<text>")
    end_of_tag = string.find(response,
                     "</text>")

    if (start_of_tag and end_of_tag) then
        text = string.sub(response,
             start_of_tag + 6, end_of_tag - 1)
        if (text ~= old_text) then
            print(text)
            old_text = text
            rs.setOutput("bottom", true)
            sleep(3)
            rs.setOutput("bottom", false)
            sleep(3)
        end
    end
    sleep(20)
end
```

Twitter API返回包含消息的XML。实际消息本身会处于一个`<text>`标签内，因此代码会找到`<text>`和`</text>`的位置，并截取中间的内容作为文本。

主循环会一直持续下去，但20秒的休眠确保了每20秒才检查一次Twitter上的推文。

我们不希望在没有新推文时触发通知，因此获取到的消息会与变量`old_text`中的消息进行比较，只有二者不同时，才会打印消息并激活红石。

当你收到消息并看到红石做出反应时，就可以去计算机控制台阅读消息了。

### 小结

这个项目开启了各种各样的可能性。这不仅意味着你在Minecraft中也能通过Twitter被联系到，而且稍加努力，你还可以在收到电子邮件或Facebook消息时得到提醒。

- 右键对应计算机的背面
- 前进键对应计算机的顶面
- 停止键对应计算机的正面

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_55_0.png)

### 代码

海龟通常在没有燃料的情况下不会移动。幸运的是，有一种方法可以绕过这个限制。我们可以通过修改配置文件`config/CCTurtle.cfg`，让海龟无需喂煤就能运行。

将这一行：

```
turtleNeedsFuel=true
```

改为：

```
turtleNeedsFuel=false
```

代码分为两部分。一个程序在计算机上运行（TurtleSend），另一个在海龟本身上运行，通过海龟的无线调制解调器接收来自计算机的命令。

### TurtleSend

这是在计算机上运行的程序。它打开一个连接到计算机“右侧”无线调制解调器的连接。如果你把调制解调器装到了其他侧面，记得修改这里。

```lua
while true do
    rednet.open("right")
    if rs.getInput("left") then
        rednet.broadcast("l")
    elseif rs.getInput("back") then
        rednet.broadcast("r")
    elseif rs.getInput("top") then
        rednet.broadcast("g")
    elseif rs.getInput("front") then
        rednet.broadcast("s")
    end
    rednet.close("right")
    sleep(0.9)
end
```

打开连接后，如果连接到按钮的红石处于激活状态，`rs.input`函数就会返回`true`。当按钮激活时，计算机就广播一条包含单个字母命令的消息：`'r'`、`'l'`、`'g'`或`'s'`，分别表示左转、右转、前进或停止。

### Turtle Receive

海龟上的接收代码与计算机上的代码相对应。但它不是检测按钮按下，而是检测来自无线调制解调器的传入消息。如果发现了消息，它就会发送相应的海龟移动命令。

变量`moving`用于决定是否执行`turtle.forward()`命令。这样海龟就可以自动前进，除非收到停止命令。

```lua
rednet.open("right")
while true do
    id, message = rednet.receive(1)
    if message == "r" then
        turtle.turnRight()
    elseif message == "l" then
        turtle.turnLeft()
    elseif message == "g" then
        moving = true
    elseif message == "s" then
        moving = false
    end
    if moving then
        turtle.forward()
    end
end
```

### 小结

扩展这个项目的一个明显方法是给海龟添加额外的命令，让它能够挖掘等。你也可以把这个项目和前面的项目结合起来，让海龟跳一小段舞，甚至让它来找你！

## 附录A：示例程序

本书中使用的示例程序都是开源的，可以从 https://github.com/simonmonk/computercraft_examples 下载。

### 在ComputerCraft中安装程序

你不必把示例程序手动输入到ComputerCraft中。如果你愿意，可以下载这些程序并将它们安装到ComputerCraft中。然后你只需要运行它们即可。

具体操作如下。

首先，在浏览器中打开 https://github.com/simonmonk/computercraft_examples ，然后点击标有ZIP的图标。它看起来像一朵云，下面有一个箭头。

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_58_0.png)

图A-1: GitHub仓库

这会下载一个包含这些程序的zip文件。将该文件解压到某个方便的位置，比如桌面。

接下来，在你的计算机上，你需要找到ComputerCraft的安装目录。

我们在安装章节中导航过的`.minecraft`文件夹就在这里。然后进入“saves”，你会注意到这些文件夹的名称就是你各世界的名称。接下来

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_63_0.png)

欢迎来到一个充满无限创意的世界，在这里你可以编写各种令人惊叹的程序，建造宏伟的建筑。

这本书将引导你从安装ComputerCraft模组开始，一直到让计算机联网或制作莫尔斯电码生成器。

有了可下载的脚本和相应的安装指南，在没有复制粘贴功能的游戏中进行编程从未如此简单！

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_63_1.png)

