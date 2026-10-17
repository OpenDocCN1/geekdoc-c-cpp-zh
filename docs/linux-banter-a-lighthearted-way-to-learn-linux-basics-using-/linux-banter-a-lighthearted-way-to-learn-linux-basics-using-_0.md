
# Linux Banter：使用 C 语言学习 Linux 基础的轻松入门指南

Linux® 是 Linus Torvalds 在美国及其他国家的注册商标。

所有人物均为虚构。与任何在世或已故人士的相似纯属巧合。

# GNU 通用公共许可证

书中的源代码根据 GNU 通用公共许可证第 3 版提供，网址为：`http://www.gnu.org/licenses/gpl-3.0.en.html`

## 免责声明

某些依赖于机器的代码在某些机器上可能可以，也可能无法工作。所有代码都在我们的计算机上经过了测试，我们没有发现任何损坏系统的问题。然而，我们对误用这些程序对您的系统造成的任何损害不负责。

## 本书适用读者

本书适合那些对直观了解 Linux 技术感兴趣，并想知道通过 Linux 系统调用和某些 C 库函数可以做些什么的人。本书概述了用于编写程序的工具，以及 Linux 系统为普通读者提供的内容。请注意，本书旨在作为一种学习 Linux 基础知识的轻松读物。这不是一本关于 Linux 管理的书，也不传授关于 Linux 安装的知识。

我们还敦促您负责任且自信地使用计算机这一强大的系统，它是基于奉献人士多年心血的结晶，也是我们文明进步的典范和稳定的基础。编程具有巨大的潜力，它确实可以为世界带来积极的变化。希望您在本课程中得愉快。这些内容概述了使用编程语言编写系统的各种方法，其中也包含实用程序。从这里学习的方法也可以扩展到理解其他编程语言。当然，由于程序数量庞大以及全球各地的高效贡献，本书不可能涵盖 Linux 系统的所有方面。但它提供了一个读者可以借此入门的基础。

## 先决条件

你需要一个安装了 GNU C 编译器的 Linux 系统，并具备 `C` 基础知识。

| 索引 | 页码 |
| :--- | :--- |
| 引言 | 4 |
| Shell 脚本 | 51 |
| C 编译器 | 83 |
| 文件与目录 | 89 |
| 内存与命令行参数 | 126 |
| 与时间相关的调用 | 142 |
| 临时文件 | 146 |
| 用户 ID 与组 | 147 |
| 资源与限制 | 154 |
| 数据管理 | 157 |
| 文件锁 | 161 |
| 数据库 | 169 |
| 进程 | 172 |
| 信号 | 184 |
| 线程与互斥 | 193 |
| 进程间通信管道 | 216 |
| IPC：信号量 | 232 |
| IPC：共享内存 | 242 |
| IPC：消息队列 | 248 |
| 套字 | 256 |
| 结语 | 286 |

书中还讲述了 Lingaraj 的轶事，他开始向想学习的地质学专家 Seema 教授 Linux。本书使用比喻来介绍各种概念，请读者不要假设这些比喻是完全等同的。

# Linux 趣谈

版权所有作者。源代码和技术事务除外。

出版商：Purple Prose，印度班加罗尔。Purple Prose 是印度的注册商标。

查询请发送：`info@purpleprose.in`

作者：Sathyajit

插图：Nishant Khare

首次出版年份：2022 年

Linux 趣谈

# 引言

![](img/image_rsrc821.jpg)

这是一个春日，街道上的每个人都心情愉悦地欣赏着花朵。但这种情绪并没有感染到 Seema，她正焦虑地走向医院。Seema 年 26 岁，身材高挑，容易对技术感到不知所措，而且非常不长记忆密码。医院有优秀的![](img/image_rsrc822.jpg)医生，这对于大多数患者来说才是最重要的。

Seema 之所以来是因为她的未婚夫 Vijay 躺在其中一张病床上。她在听说了 Vijay 意外的消息后急匆赶来。她在接待台询问，接待人员将她引到一楼的特病房。她跑上楼梯，看到 Vijay 躺在床上睡觉，头上缠着绷带。

![](img/image_rsrc823.jpg)

Vijay 是一个 30 岁的年轻人，是一名室内设计师。Seema 作为一名地质学专家，大约在一年前见了 Vijay，当时 Vijay 出现在她运营的咨询办公室设计那里。他们有着相同的品味，关系一直向好发展。直到这次事故的发生。Seema 看着 Vijay，希望自己以某种方式帮到他。然后她去见了医生。

![](img/image_rsrc824.jpg)

医生是一位四十多岁的平易近人的人，特别注重让患者及其家属感到放松。

“他有轻微脑震。他在火车上旅行时，笔记本电脑掉在了头上。笔记本电脑里安装的软件缓冲了冲击，”医生说道。

他开始为自己的笑话笑了起来。

“我希望他会没事的。”忧心的 Seema 说。

![](img/image_rsrc825.jpg)

这时，Vijay 手里拿着键盘走了进来。

![](img/image_rsrc826.jpg)

他们到达了那里，当司机关闭引擎时，一个大约 28 岁的孤独男子走了出来，穿着一件印有“传奇被高估了”字样的 T 恤。

![](img/image_rsrc82M.jpg)

Seema 看到他后松了一口气，因为天快黑了，周围无人烟。

“我想你就是林加拉（Lingaraj）。我是 Seema。” Seema 自我介绍道。

“是的，”林加拉回答道。

![](img/image_rsrc82N.jpg)

“我的未婚夫 Vijay 吸收了机器意识。我来向你寻求帮助。”

“是的，医生告诉我了。我们曾想过，有一天机器会吸收人类意识。”

“那么，我们什么时候开始？”

“嗯，你们都经历了一段艰难的旅程。休息一下，我们明天开始。”

“我会回班加罗尔，先生，”司机说。

![](img/image_rsrc82P.jpg)

“如果你从这里离开，没有人知道你会去去哪里，至少你自己也不会知道。听我的，在这里吃顿顿晚餐，明天再回去。”林加拉说。

出租车司机同意了。

林加拉让他们停好车，他们朝营地走去。

![](img/image_rsrc82R.jpg)

他们的营地设在一个大片空地上，他们为自己建造了环保房屋。有些房子成群分布，有些则与众隔离开。Seema 被带进了她的私人住处，而司机被带到了林加拉的住处。

![](img/image_rsrc82S.jpg)

Seema 洗了脸，坐在外外的门廊上。氛围非常宁静，蟋蟋叫着。有很多鸟儿在歌唱，她沉浸其中了一会儿。

![](img/image_rsrc82T.jpg)

然后，林加拉和曼朱纳斯（Manjunath）来到她所在地。林加拉为她准备了豆芽和一些健康三明治做的晚餐。Seema 试图提到 Vijay 的问题，但林加拉正忙着给司机曼朱纳斯讲笑话。

![](img/image_rsrc82U.jpg)

等他们结束后，林加拉告诉她课程将于第二天早上 9 点开始。

Seema 回到家里立刻睡着了。她梦见 Vijay 和她在森林里散步。

![](img/image_rsrc82V.jpg)

第二天，Seema 醒来后去了林加拉的家。此时司机已经离开了。林加拉随后向她展示了一个装满食物物资的盒子，让 Seema 在晚上下课后把它们带回自己。她注意到有小米和水果，以及装有香料的小泥罐。然后，林加拉带她来到大厅里的电脑。

![](img/image_rsrc82W.jpg)

Seema 在整个期间除了林加拉外没有见过任何人，并向他询问了这件事。林加拉说大多数人都去徒步了。

![](img/image_rsrc82X.jpg)

“我们开始吧，”林加拉说，“你需要能够与机器交流。现在，对着这台机器说话，”林加拉指着正在充电的笔记本电脑说。电脑上插着很多电线。

![](img/image_rsrc82Y.jpg)

“嗨电脑，你会做我的朋友吗？”Seema 问道。

“那样是不行的。”

Seema 思考了很久。然后她取下发带，松开头发，迅速地将头发与电脑电线缠在一起。

![](img/image_rsrc82Z.jpg)

“那也不行。如果那有用，人们就会在 ATM 外排队，恳求 ATM 理解他们的困境并给他们钱了，”林加拉说。

“那我该怎么办？我不是软件工程师，我是一个地理专家，”Seema 绝望地说道。

“你需要先理解系统。然后编写程序来改变系统或利用它。”

“与这个系统（一个 Linux 系统）交互主要有两种方式：Shell 编程和使用编程语言。要制作一个程序，你需要精通像 C 这样的编程语言。为了让程序对系统有意义，你需要一个编译器。关于 C 的基础知识，你可以并行自学，但在那之前，我们需要看看系统能提供什么。”

“这个系统是一个 Linux 系统。Linux 是一个内核，它现在正在不断被完善中。一个叫 `Linus Torvalds` 的人主动发起让软件体现自由精神。他编写了操作系统的核心。在世界各地的贡献下，Linux 正在不断成长，”林加拉继续说道。

![](img/image_rsrc830.jpg)

“要操作系统，你需要登录。为此你需要访问权限，”他补充道。

“好的。Vijay 认得我，所以我有访问权限。”

“是的，他吸收了机器意识。你确定想让他变回原来？”

“他曾经是那么完美。他总是满足我的每一个愿望。每天给我送花。会为我唱歌。在争论中总是站在我这边。”

“你确定他现在不像在演戏吗。”

“什么？”

“不关我。反正，一旦你进入系统，就可以使用它。你可以让它执行任务并执行你的命令。所以无论他是否恢复，对你来说都是双赢的局面。”

“请专注于教我吧。”

“开玩笑的。Linux 有很多发行版本，被称为口味（flavours）。

要使用一个系统，你也需要对其进行编程。你可以使用 `C`、`C++`、`Java`、`Python`。”

“`ls`…..Lingaraj Seema?”

“`ls` 是一个告诉系统列出目录中所有文件的命令。`-al` 是传递给命令的选项。`-a` 代表所有文件，而 `l` 代表详细格式（long format，小写 L），它告诉系统显示详细信息。”

Lingaraj 随后按下了回车键（Enter）。屏幕上出现了一份文件列表：

| 文件名 | 权限 |
| :--- | :--- |
| Loveletter_Mythri | `rw-r--r--` |
| Loveletter_Chitra | `rw-r--r--` |
| Loveletter_Sanjana | `rw-r--r--` |
| Loveletter_Sangeetha | `rw-r--r--` |
| letterwriter | `rwxr-xr-x` |

“那些 `r` 是什么？还有 `x` 呢？”Seema 问道。

“也许我需要更改目录。我现在在哪个目录？”Lingaraj 自己输入了：

```bash
$ pwd
```

系统显示了当前目录（工作目录）。

“关于所有的 `r` 和 `x` 权限，我会告诉你。这个会话足够了。我们一小时后见。我现在的心情不错。”Lingaraj 说。

“我能理解。”Seema 说。

Seema 想着去散步，走上了路。她看到许多骑行者，有年轻人也有老年人，他们保持着健康。他们看着 Seema，向她挥了挥手。

![](img/image_rsrc34.jpg)

他们停好自行车回到各自的家。Seema 继续走路，在附近发现了一条小溪。她在岩石上坐了一会儿，把这纳入她的日常生活。

![](img/image_rsrc835.jpg)

“所以，你想开始吃西瓜还是面条？”Lingaraj 在他们回到房子时问。

“西瓜。”

“好，关于 shell。有很多方法可以访问内核。这是其中一种。你会发现有很多种 shell，比如 Korn shell、C shell 等。但我们使用 `Bash`。”

当我们输入：

```bash
$ /bin/bash –version
```

它会给你 shell 的版本。”

Lingaraj 发出一声奇怪的声音，一只鹦来到窗台。

“这是 Paresh 的鹦。说 Hi。”

“Hi。”Seema 对鹦说，鹦回答了，让 Seema 感到很高心。

![](img/image_rsrc36.jpg)

“你可以将输出重定向到文件。在我们的社区里，如果有人对我们说话而我们很忙，我们就让他们对着耳朵。所以，”

```bash
$ ls -al > lsoutput.txt
```

这里 `ls -al` 是列出所有文件的命令。输出可以发送到 `lsoutput.txt` 以供以后使用。当然，当有人胡说八道时，我们可以把它发送到空设备。在 Linux 中，我们有 `/dev/null`。一旦你发送到那里，就没有返回。”Lingaraj 继续道。

“所以，”

```bash
$ ls -al > /dev/null
```

什么都没有。

```bash
$ ls -al > lsoutput.txt
```

如果 `lsoutput.txt` 存在，它会被覆盖。要追加到文件中，正如昨天说的那样，使用：

```bash
$ ls -al >> lsoutput.txt
```

注意这里是双大于符号。有时你想知道某人的大脑在发生什么。”

“是的，我很好奇。”Seema 说。

“你可以看到正在运行的进程列表。使用 `ps` 命令。”Lingaraj 说。

```bash
$ ps
```

系统显示了进程列表。

“这非常有帮助。我可以看到某人的大脑在发生什么。”Seema 说。

“是的，如果他在想某辆车。”

“特别是他在想我。”

“我会告诉你一些方法。你甚至可以使用 `kill` 命令杀死一个进程。”

让我们快速完成这些事情。我有许多进程要杀死。我可以在他的大脑加一个进程吗，比如想想我的生日礼物？”

“那需要很多生日才能学会。”Lingaraj 停了下来。Seema 想他会问她的生日是什么时候。

“你可以听它的。在 Linux 中，你可以通过以下方式读取文件内容：

```bash
$ cat lsoutput.txt
```

还有：

```bash
$ more < lsoutput.txt
```

就像输出被重定向一样，在这种情况下，输入被重定向到了名为 `more` 的工具。

`wc` 命令告诉你字数。有一个选项是：

```bash
$ wc -m
```

它告诉你字符数。

`man` 命令……”

“帮助我们理解人类？”Seema 插话道。

“不，帮助我们理解 Linux 系统。`Man` 是 manual（手册）的缩写。如果你需要帮助，输入 `help`，比如：

```bash
$ ls –help
```

“你甚至可以尝试 `info ls`。我们去散步吧。”

Seema 和 Lingaraj 带了一些食物来到山脚。有一座小山，他们同意爬上去很好。Lingaraj 带了他的笔记本电脑。上山时，Seema 感到自己做得很轻松，没有气喘吁吁。空气没有污染，这让她充满了活力。

![](img/image_rsrc837.jpg)

他们到达了山顶，她可以看到河流并发现一些村庄聚居点。没有沥油路的迹象。

“大喊 Vijay 的名字。”Lingaraj 建议道。

“Vijay！”Seema 喊道。

出现了两次回声。

![](img/image_rsrc838.jpg)

“这是一个 Linux 中的命令。`echo` 命令。”Lingaraj 打开笔记本递给 Seema 说。

“哇，我可以让 Vijay 喊出我的名字，回声会一直共鸣。”

“它只是重复你说的话。一次。试试看。说点独特的。”

Seema 在笔记本上输入：

```bash
$ echo I am there for, Vijay
```

显示了如下内容：

```text
I am there for, Vijay
```

“和 `echo` 一样独特。”Lingaraj 评论道。

Lingaraj 静了一会儿。

“你想用 `pipe`（管道）吗？”Lingaraj 问道。

![](img/image_rsrc39.jpg)

“不，它将一个人的输出连接到另一个人的输出。”Lingaraj 指着笔记本电脑说。他输入并向 Seema 展示了回车键上面的管道键。

```bash
$ echo Seema is original | wc -m
```

`echo` 命令通过给了 `wc` 命令，它告诉你字符数。”

“运行时加载的程序，就像设备驱动程序。设备驱动程序是一个与打印机、扫描仪或外部硬盘等设备通信的程序。”

Lingaraj 望向远方。

“有什么事情困扰你吗？”Seema 问道。

“以前在图书馆读 Linux 编程时，我爱上过一个管理员。”（等等，不）“以前在图书馆读 Linux 编程时，我爱上过一个管理员。

我过去告诉她：‘自从见到你以后，我的心跳就停止了。我买了两张电影票。’”

![](img/image_rsrc83E.jpg)

她说：“把票退了。’”

Seema 不知道该怎么办。随着时间的推移，她会习惯 Lingaraj 的这些轶事。

“总之，我只是提一下这些。

`/proc`

动态创建的文件系统。内核的控制和信息中心。如果你需要信息，就去这里。例如，

```bash
$ cat /proc/cpuinfo
```

会给你关于 CPU 的信息。”

Lingaraj 指了指几个坐在一起八卦的人。

![](img/image_rsrc83F.jpg)

“我给你们讲个故事。外面有很多男士和女士，他们对我们社区的情况几乎无所不知。事实上，当有人想做婚亲时，他们会询问这组人关于那个人的性格。这是很久以前的事了，在我们听说手机之前。

在岛屿上还有另一个社区。那里的人与世隔绝，不知道任何技术进步。

![](img/image_rsrc83G.jpg)

他们由一位国王统治。我想既然我有一个吹风机，我想带给他给他留个深刻印象。我听说他有一个女儿。于是，我开始了耗时 4 周的危险旅行，去了那个岛屿。

![](img/image_rsrc83H.jpg)

我穿着现代衣服四溜，很快就被抓住了。这是我计划的一部分。我被带到了国王面前。

![](img/image_rsrc83J.jpg)

‘你是外星人吗？国王问我。

‘我来自远方，现在我要让你大眼界。’我说。

我要了一桶水，他们提供了。

![](img/image_rsrc83K.jpg)

然后我把水朝国王泼过去，他被淋透了。他非常生气。

‘我知道你很生气。但我会瞬间让你干透。’我说道。

![](img/image_rsrc83M.jpg)

‘如果你不这样做，我就让你淹在自己的血里。’国王吼道。

‘好的，这个我发明的魔法设备……’

![](img/image_rsrc83N.jpg)

我拿出了吹风机。

‘这个电源插座在哪里？’我问。

‘什么电源插座？’

‘哦，我明白了！’



![](img/image_rsrc83P.jpg)

国王拔出了剑。

我闭上眼睛。那些人没有电。

这时，当国王靠近并正要用剑时：

![](img/image_rsrc83R.jpg)

这些人来得救了我的命。他们带回了太阳能电池。

我急忙拿到电池，用吹风机把他吹干了。他消气了。他请我留下来，我告诉我会带来更多这种神奇的东西。

“多么棒的冒险！这真的是真的吗？”

Lingaraj 继续说道，忽略了这个问题。

“噢，这些人每会向每一个来找我相亲的人讲这个故事，然后就嘲笑我。”

“国王还在世吗？”Seema 问道。

“不，他在洗澡时用吹风机，触电去世了。

总之，这些人就像这些控制室，他们无无不晓，比如我在岛上在忙些什么等等。

`/root`

超级用户的家目录。

`/sbin`

必需系统二进制文件，需要超级用户权限执行。

`/tmp`

临时文件。”Lingaraj 解释道。

“临时文件。我觉得并不重要。”Seema 说。

“看看我们的世界。整个世界都存储在一个临时目录里。非常重要。

`/usr`

可共享和只读数据的根目录。

`/usr/include`

编译 C 语言程序的头文件。

`/usr/lib`

大多数二进制程序的库。

`/usr/sbin`

非核心系统二进制文件。

`/usr/share`

体系无关的数据。

`/usr/src`

源代码。

`/usr/x11r6`

X 窗口系统。

`/var`

可变数据，如电子邮件、打印机日志等。”

“有心目录（heart）吗？我想去 Vijay 的系统里看看，看看那里有没有我的痕迹。”Seema 忧伤地说。

“我假设这是一个修辞性问题。如果我把你放进一个迷宫，你会怎么出来？”

“我会从知道我在哪里开始。”

“在 Linux 系统中，你会怎么做呢？”

“我不知道。问系统我在哪里。”

“`pwd` 命令是什么？”

“它显示个人工作目录，在这种情况下，就是你的情书目录。我看到它了。”

“不，它是 print work directory（打印工作目录）。你现在所在的目录。所以，如果你困在某个地方的目录迷宫里，不知道自己在哪里，你就输入 `pwd`。如果你想回家，这很简单。输入：

```bash
$ cd
```

如果你想去其他某个目录，例如`/usr/lib`：

```bash
$ cd /usr/lib
```

```bash
$ cd ..
```

会带你回到一级。

```bash
$ file
```

告诉文件是什么。

```bash
$ cat
```

显示文件的内容。

```bash
$ clear
```

屏幕立即被清空。”

还有其他如`locate`和`find`这种名副其实的命令。

“我有一个问题。一旦你获取了对`Vijay`的权限，你打算做什么？”

“我会成为他的超级用户（superuser）。”

“明天，我们将学习 Shell 脚本，超级用户。”

# Shell 脚本

傍晚时，Seema 觉得录下 Lingaraj 的课程会比较好。这在她回到班加罗尔后会有所帮助。但课程里也包含了一些他个人的私故事，于是她决定不这样做了。她给自己做了一些三明治，那天早睡了。这将会变成一种习惯。

![](img/image_rsrc83S.jpg)

“这是一个 Shell 脚本。但它不是一个文件。我们将在提示符中输入它。”

```bash
$ for file in *>
```

Lingaraj 一边展示笔记本电脑屏幕一边说道。

“美元符号直接变成了这个‘>’符号！”Seema 惊呼道。

“我在现实生活中涉及到金钱时也会发生这种情况。不过那是小于号。”

Lingaraj 继续输入。整个程序看起来像这样：

```bash
$ for file in *>>do if grep -l failure $file> then more $file> fi done own
```

随后是输出结果：

```text
| Failed relationship 这是一个包含 failure 的文件。请看一些励志视频.$ |
```

“我稍后会解释上面的内容。”

“你是说失败的关系吗？”Seema 问道。

“是`grep`命令。”Lingaraj 正道。

“好的。”Seema 说。

## 变量与常量

“变量。变量是在程序执行过程中会变化的部分，而常量是不变化的部分。

你可以在程序运行过程中声明变量。变量是对大小写敏感的。大写字母和小写字母‘Linux’和‘linux’是不同的。”

“让我试试。”Seema 说并在提示符中输入：

```bash
$ var=Sonal$ constant=Seema
```

“我读了很多。要找到变量的值，在变量名前面加一个`$`符号。你可以使用`echo $var`来查看当前的……我的意思是，当前的变量是什么。”

Seema 在提示符中输入：

```bash
$ echo $var
```

随后屏幕上显示了输出：

```text
| Sonal |
```

她继续输入：

```bash
$ echo $constant |
```

显示了输出：

```text
| Seema |
```

Seema 感到很有成就感。

“有一种特殊情况。如果你给变量赋值为`3 + 4`，会发生什么？”Lingaraj 问道。

Seema 输入了：

```bash
$ result=3+4$ echo $result
```

显示了输出：

```text
| 3+4 |
```

“它没有相加。”Seema 说。

“所以我们学到了变量是以字符串存储的，而不是数值。

等号两边不能有空格。如果你想包含像‘Sonal Vijay’这样的空格，就要用引号括起来。”

Lingaraj 忽略了关于‘Sonal Vijay’连在一起的错误，Seema 以为他会纠正。她输入了：

```bash
$ constant=“Seema Vijay”echo $constant
```

显示了输出：

```text
| Seema Vijay |
```

“你还可以读取输入，并使用`read`命令在脚本请求用户输入后，将输入赋值给变量名。”Lingaraj 说。

Seema 输入了：

```bash
$ read earinput
```

接着她输入：

```text
| Let’s go to the movie. |
```

“现在，使用`echo $earinput`。”Lingaraj 说。

Seema 输入了：

```text
$ echo $earinputLet’s go to the movie. |
```

“我们在程序里试试这个。注意引号。”Lingaraj 说，并输入名为`vardemo.sh`的新 Shell 脚本。

```bash
#!/bin/shVijaysvar=“Are you in there”echo $Vijaysvarecho “$Vijaysvar”echo ‘$Vijaysvar’echo \$Vijaysvarecho Enter some textread Vijaysvarecho ‘$Vijaysvar’ now equals $Vijaysvarexit 0
```

他在提示符中执行了该 Shell 脚本，使用了：

```bash
$ sh vardemo.sh
```

输出显示在屏幕上：

```text
| Are you in thereAre you in there$Vijaysvar$VijaysvarEnter some text |
```

此时，Lingaraj 输入了一些文本：

```text
| All variables cleared |
```

程序继续执行：

```text
$Vijaysvar now equals All variables cleared |
```

“这展示了使用变量并回显它们的语法。”

Lingaraj 继续说道。

![](img/image_rsrc83T.jpg)

“假设你身处一个系统，想了解更多关于系统的信息。Shell 提供了一些脚本启动后即可使用的变量。

我允许你住在房子里了。”他突然换了话题。

“是的，你真是太好了。我想感谢你，但由于这些关于 Vijay 的事……”

“你打扫房间了吗？”

“我必须扫吗？我的意思是已经足够干净了。”

“那是因为在你来之前我就扫过了。现在，假设我没有打扫房子，你会怎么办？”

“我会扫的。”

“在执行任务时，你的认知中会有这些细节。

1. `Home`。你的家在哪里？
2. `PATH`：去哪里寻找扫帚、桶等工具。
3. 任务名称。在这里是清洁。但也可以消毒或熏蒸。
4. 传递的变量数量。如果你在打扫，我会告诉你使用苦楝膏、姜根提取物和苹果木醋作为清洁剂。所以，”

| 表达式 | 说明 |
| --- | --- |
| `expression1 -ge expression2` | 如果`expression1`大于或等于`expression2`，则为 True |
| `expression1 -lt expression2` | 如果`expression1`小于`expression2`，则为 True |
| `expression1 -le expression2` | 如果`expression1`小于或等于`expression2`，则为 True |
| `! expression` | 如果`expression`为假则为真，如果`expression`为真则为假。 |

它也可以用于测试文件。

### 文件条件

| 条件 | 说明 |
| --- | --- |
| `-d file` | 如果`file`是一个目录，则为 True |
| `-e file` | 如果`file`存在，则为 True |
| `-f file` | 如果`file`是一个普通文件，则为 True |
| `-x file` | 如果`file`可执行，则为 True |
| `-w file` | 如果`file`可写，则为 True |

以及更多。

现在，按照承诺的，来看‘`if`’逻辑。看这个程序。在处理字符串时，等号也用于测试。Lingaraj 在屏幕上向她展示了程序。

`deepa.sh`

```bash
echo Do you love me Deepa?
read deepip
if [ "$deepip" = "yes" ]
then echo Congrats
elif [ "$deepip" = "no" ]
then echo Think again
fi
```

“它的作用是……”

“把‘Think again’作为输出？”Seema 俏皮地建议道。

“你不需要计算那个，对吧。”

他继续说道：“我们还有`else`语句。”

`deepafriend.sh`

```bash
echo Do you love me Deepa?
read deepip
if [ “deepip” = “yes” ]then echo Congratulations
else echo Please pass this question to your friends
fi
```

为了说服 Deepa，如果她在犹豫不决：

`deepades.sh`

```bash
echo Do you love me Deepa?
read deepip
if [ “deepip” = “yes” ]then echo Congratulations
elif [ “deepip” = “maybe” ]then echo Remember our previous incarnations
elif [ “deepip” = “no” ]then echo You will never meet another Lingaraj
fi
```

‘`fi`’是`if`的反过来，用于结束`if`条件语句。

现在，是`for`语句。你对 Vijay 有什么疑问吗？你觉得他暗中喜欢某人？”

“那么，你有解决方案吗？”Seema 问道。

“给我她的名字。”

“Swathi, Aarthi 和 Bharati。”

“看这个程序。”

Seema 看了看屏幕。

`vijaysab.sh`

```bash
#!/bin/sh
for interest in Swathi, Aarthi Bharati;
do
    echo Vijay is no longer interested in $interest
done
exit 0
```

输出显示在屏幕上：

```text
Vijay is no longer interested in Swathi
Vijay is no longer interested in Aarthi
Vijay is no longer interested in Bharati
```

“你懂了吗？只要变量的值为真，`for`循环中的语句就会一直执行。”

“谢谢！”Seema 说，“如果你知道需要重复的次数，就使用`for`循环。但如果你不知道他那许多……我的意思是确切的次数，请使用`while`循环。”

`fiancename.sh`

```bash
#!/bin/sh
echo “Enter fiance name”
read fianename
while [ “$fiancename” != “Seema” ]; do
    echo “Remember those times, Vijay.”
    read fianename
done
exit 0
```

这会一直持续，直到用户将你的名字输入为`fianename`。

现在，是`until`条件。

`vstate.sh`

```bash
echo Enter your state
read vstate
until [ "$vstate" = "human" ]
do
    echo Seema learn more Linux
    read vstate
done
```

“你能告诉我这是做什么的吗？”

“它的意思是直到 Vijay 回到人类状态之前，我会继续学习 Linux。我不介意这样做。”

“现在，你还没有正式加入我们的社区。”

“没问题。我是来学习的。”

“假设你有一个需求，我们有不同的人来处理。看这个。”

`requirement.sh`

```bash
#!/bin/sh
echo “What do you want?”
read requirement
case $requirement in
    inc)
        echo “You must contact Yashasvini”
        ;;
    herbs)
        echo “Contact Lingaraj’s father Ashwath”
        ;;
    treeclimbing)
        echo “Contact Gidaa ”
        ;;
    crocodileconversation)
        echo “Contact Lingaraj ”
        ;;
    *)
        echo "Lingaraj can help"
esac
```

所以，对于用户输入的每个`case`，都有不同的输出。用`esac`结束语句。

“这是要遵循的语法。”Lingaraj 说。

“你能帮我跟鳄鱼说话吗？”Seema 问道。

“你不想那样做。它一张嘴就很难合上了。如果‘`if`’必须筛选不同的语句，生活会变得困难。所以我们有`&&`列表。`&&`列表就像一个顺序测试。例如：

`seqtest.sh`

```bash
echo Can you climb trees?
read treeclimb
echo Do you know how to cook millets?
read cookmile
echo Can you run faster than a gazelle?
read gaze
echo Can you sing ghazals?
read ghaz
if [ $treeclimb=“yes” ] && [ "$cookmil"=“yes” ] && [ "$gaz"=“yes” ] && [ "$ghaz"=“yes” ] ; then
echo Will marry me?
fi
```

Lingaraj 说，他向 Seema 展示了他输入的。

“我预测到了求婚。”Seema 说。

“所以，只有当所有条件都满足时，才会显示最后的求婚。这是 4 年前写的。现在我修改了。看。”

Lingaraj 向她展示了程序的新版本。

`seqtest_or.sh`

```bash
echo Can you climb trees?
read treeclimb
echo Do you know how to cook millets?
read cookmile
echo Can you run faster than a gazelle?
read gaze
echo Can you sing ghazals?
read ghaz
if [ $treeclimb=“yes” ] || [ "$cookmil"=“yes” ] || [ "$gaz"=“yes” ] || [ "$ghaz"=“yes” ] ; then
echo Will marry me?
fi
```

“双管道是一个 OR 列表。只要满足一个条件，就会继续提案。”

“我觉得你真的需要订婚。我会向你介绍一些。”

（注：提供的源文本似乎在此中断或乱码）

（注：文本继续……）

“这是一个函数示例。”Lingaraj 向 Seema 展示了一个脚本。

`food.sh`

```bash
#!/bin/sh
food() {
    echo “Food is prepared.”
}
echo “script started”
food
echo “script ends”
exit 0
```

Lingaraj 运行了 Shell 脚本，输出显示在屏幕上：

```text
script started
Food is prepared.
script ends
```

（注：文本继续……）

`paramdiff.sh`



```bash我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。#!/bin/sh
paramshow() {
var="Lingaraj’s function"
echo The variable var inside the function is $var
echo The first parameter for this function is $1
}
var="Seema’s wedding"
echo The variable var in the program is $var
echo Original first parameter for this program is $1
paramshow Lingaraj
exit 0
```

Lingaraj 使用命令运行它：

```bash
$ sh ./paramdiff.sh Seema
```

“让我们看看输出：”

| 程序中的变量 `var` 是 Seema 的婚礼 Original | 该程序的第一个参数是 Seema |
| --- | --- |
| 函数中的变量 `var` 是 Lingaraj 的函数 The | 该函数的第一个参数是 Lingaraj |

尽管我们在程序和函数中都使用了 `$1` 且相同的变量名 `var`。

现在，我们来看一些在 Shell 编程中通常无法在命令行提示符上直接使用的命令。

```bash
break
```

“你可以使用 `break` 在条件满足之前跳出循环。`break` 语句会立即退出它所在的循环。如果 `break` 在一个 `if` 语句中，而 `if` 语句又在 `while` 或 `for` 循环中，那么 `break` 会让程序不仅跳出 `if` 语句，还会跳出 `while` 循环或 `for` 循环。”Lingaraj 说道。

“在我的情况下，当我准备演示稿时，我决定一直工作到完成。但如果闻到邻居家里传来的蛋糕的味道，我会休息（`break`）去烤一个。”Seema 说道。

“在我们的社区，如果邻居做了蛋糕，我们直接过去分一份。就好像那是为我们准备的一样。”

“就像 `break` 一样，我们还有 `continue`，它告诉程序继续执行。”

`continue` 会跳过当前迭代中循环内的剩余命令。

假设你正在为研讨会接待人们。这些你要做的事情：

```bash
do {
    你看到这个人
    向他们要身份证
    向他们要填好的申请表
    你收钱
}
while (people walking in)
```

如果必须对每个人都这样做，这必须是一个循环。但如果你在研讨会上看到了我呢？那么，我们就改变逻辑。

```bash
do {
    你看到这个人
    if person = Lingaraj
    continue
    向他们要身份证
    向他们要填好的申请表
    你收钱
}
while (people walking in)
```

基本上，`continue` 会根据条件跳过该特定迭代的循环。

暂时不用担心语法。如果你在研讨会上看到我，你就会跳过所有剩余任务，因为你很了解我，不会向我要身份证、申请表或钱。

“我懂了。`continue` 是用于像你这样的特殊情况，我们不希望走为普通人设计的后续流程。”

Lingaraj 像往常一样继续说道：

“回到命令。有时命令可以存储在变量中。例如：

```bash
CD="cd Lingaraj"
eval "$CD~/Lingaraj"
```

“你有没有遇到过这样的情况：你不告诉 Vijay 发生了什么，而是等他去猜？”Lingaraj 问。

“我必须承认。那是我的生日，我做了一道特殊的菜。Vijay 忘了。更糟糕的是他问：‘今天什么日子？’我说‘没什么’。”Seema 回道。

“现在，如果 `eval` 可以用于现实生活：

```bash
eval "$Nothing"
```

输出将会是：

```text
Today is my birthday, wish me!
```

在这里，`Nothing` 是一个变量，存储了一个命令，告诉 Vijay 告诉你些什么。

`eval` 查看存储在变量中的命令并执行它。

所以，如果你看这个现实程序：

```bash
Nothing="echo 'Today is my birthday, wish me!'"
eval "$Nothing"
```

输出将是：

```text
Today is my birthday, wish me!
```

`exec` 用另一个程序替换 Shell，就像废除 Shell 一样。

```bash
exec echo "This shell is gone!"
```

“文字显示在屏幕上，然后 Shell 就消失了。”

“这样好吗？Shell 消失？Shell 不重要吗？”Seema 问。

“从哲学上来说，不！”

Seema 明白他指的是人的外壳。Lingaraj 继续说道：

“你可以这样记忆它：遗嘱执行。一个人提名某人代替自己的位置然后消失。

我的曾祖父非常喜欢调制各种植物和蔬菜汁来制作他的特制饮料。之后他经常编些大故事。在宿命的一天，他做了一种饮料。他喝了一口，脸就蓝了。在去世之前，他宣布我的父亲——实际上是一位拥有生物技术工程学位和 MBA 学位的高望学者——是下一个调制者。我祖父的老客户现在仍然来我父亲那里买饮料，而我父亲把他们赶走了。

`exit` 命令。如果你在程序中的命令后输入 `exit`，你可以返回一个程序可以使用的值。我有一个请求。当你跟我一起上完这门课程后，有人问你进展得如何，告诉他们结果是 0。”

“你并不那么糟！”

“在 Linux 中，`exit` 状态码 `0` 通常表示成功。还有 125 种退出状态。

现在，是 `export` 命令。你说我并不那么糟。如果你觉得我很棒（我确信你会这么想），光告诉我是不够的。你还得告诉别人。所以：

```bash
Lingaraj=Great
```

除了赋值之外，你还必须将其导出（`export`）出来。

```bash
export Lingaraj
```

这样像你这样的人就可以来向我学习了。

在 Linux 中，当你使用 `export` 命令时，该变量就不再只是局部变量，它的值可以在由当前脚本调用的其他脚本和命令中使用。看这个 Shell 脚本，`echoexport1.sh`：

```bash
Lingaraj=great
export Lingaraj
echo "The value of Lingaraj is $Lingaraj"
echo "This is the shell script where Lingaraj=great is declared."
echo "Now calling the second script."
./echoexport2.sh
```

还有 `echoexport2.sh`：

```bash
echo "The value of Lingaraj is $Lingaraj"
echo "This is the shell script where Lingaraj=great is declared."
```

（注：由于原始文本存在大量重复和乱码，以上内容已根据逻辑进行了最核心的提取与翻译。）

```bash
$ find / -name test -print
```

你将找到所有名为 `test` 的文件并将它们打印在屏幕上。从 `/` 开始，那个……？”

“根目录。”Seema 回答道。

“所以，

```bash
$ find / -name Seema -print
```

将打印系统中所有名为 `Seema` 的文件。”

这些是其中的几个选项。

### `-atime N`

`N` 在这里是一个数字。该文件最后被访问是在 `N` 天前。当你知道 Vijay 上次访问某个特定文件的时间时，可以用来做一个类比。

### `-mtime N`

该文件在 `N` 天前被修改过。

### `-name pattern`

文件名（不包括任何路径），匹配提供的模式。为了确保模式被传递给 `find` 而不是立即被 shell 评估，模式必须始终放在引号中。

例如如下：

```bash
find . -name "*ma" -print
```

将打印所有以 `ma` 结尾的文件。注意那个点。它表示当前目录。

所以，我们了解到，如果你不知道任何名字，`*` 就非常有用。这在婚礼场合是一个很好的工具，当时有些亲戚来并问你：“记得我是谁吗？”如果这是一个被接受的习惯，人们会字面上地称呼你为“* 叔”或“* 姨”，他们会很开心，我们可以去追求更有价值的事情，比如设置状态消息。

既然提到了这个话题，如果你记得名字的一部分，比如必须是 Suresh 或 Ramesh，但无法精确确定，你可以使用 `???esh`。这样，你就能赢得更多的社交认可度分数，因为你偏离并不远。你甚至可以使用 `[SR][ua][rm]esh`。这样，人们会认为你正在研究人工智能。

```bash
find . -newer Seema
```

注意那个点（`.`）。

查找比文件 `Seema` 更新的文件。“自从你上次见到 Vijay 之后，是否有任何新增的内容，”Lingaraj 说，并想提供帮助。

“这有点过头了。”

“看看是谁在说话。”

输入 `-d` 表示目录，`-f` 表示普通文件。

```bash
$ find . \( -name "*ti" -o -newer Seema \) -a -type f -print
```

“它找到所有以 `ti` 结尾的文件或比 `Seema` 更新的文件，并且根据 `f` 的指示，必须是普通文件，然后打印。括号前的反斜杠 `\` 是转义字符。”

你已经见过如何通过文件名查找，但搜索文件内部的内容呢？你有 `grep` 命令。

我的祖父，正如我告诉过你的，制作了很多药剂，我在这台电脑上记录了它们。我有一个文件列表。现在，如果我想搜索所有包含葡萄的药剂，我是这样做的：

```bash
$ grep grapes pprosedrink.txt
```

你应该压碎这些葡萄：

```bash
$ grep -c grapes pprosedrink.txt
```

```text
pprosedrink.txt:24
```

`-c` 是计数，还有其他选项。比如 `-v` 是反向，显示不包含单词 `grapes` 的行数。如果你想看有多少文件包含 `grapes` 这个单词而不查看文件内容，只需添加 `-l`（小写 L）。

```bash
$ grep [a-h] pprosedrink.txt
```

方括号可以包含可以匹配的内容。

这将高亮所有包含 `a` 到 `h` 之间字母的单词。

```bash
$ grep a[[:blank:]] pprosedrink.txt
```

喝了这种酒后，我就成了一台战斗机器。

在 `a` 之后，`grep` 使用正则表达式 `a[[:blank:]]`，它告诉系统在 `a` 之后寻找空格。简而言之，就是一个以 `a` 结尾的单词。

```bash
grep th.[[:space:]] pprosedrink.txt
```

Seema 问起 `th` 之后的点。她接着告诉 Lingaraj，她知道括号里的内容是在寻找空格。Lingaraj 回答道：

“点告诉系统寻找单个字符。

所以结果是：

```text
Huge is the sky
But if it weren’t for the eye
```

元字符是一个具有其字面意思之外含义的普通字符。”

“`$` 是很好的例子。”Seema 提议道。

“锚点是文本行中正则表达式匹配的位置。例如，`^` 和 `$` 就是锚点。

`4 + 2` 等于？”

Seema 感到很惊讶。她想问 Lingaraj“为什么？”，但她直觉 Lingaraj 自己在做某事之前并没有问过自己“为什么？”她回答道：

“6。”

“5 + 1?”

“6。”

“12/2?”

“6。”

“3+3?”

“6。”

“3 * 2?”

“6。”

“想一种蔬菜。”

“好的。”

“那是胡萝卜吗？”

“是的，你怎么……”

“这对大多数人都有效。”

“现在，在键盘上，如果你使用 `shift 6`，你会得到一个符号。它叫什么？”

Seema 按下 `shift` 然后 `6`，得到了 `^` 符号。

“脱字符。”她回答道。

当你使用正则表达式时：

```bash
$ grep ^T Seema.txt
```

会在 `Seema.txt` 文件中查找以 `T` 开头的行。

接下来，你可能想执行一个命令，并将命令的输出作为另一个命令的一部分。简单地，把命令放在括号里：

```bash
$ echo $(who)
```

“今天就到这里。”

第二天，你可能想执行一个命令，并将命令的输出作为另一个命令的一部分。简单地，把命令放在括号里。

[注：提供的文本包含重复部分和碎片产物；我已保持了源文本的核心逻辑。]

“在下雨期间，我编写了这只猴子溜进酒类商店给我们买饮料。执行这个命令时，你竖起大拇指并说你喜欢的饮料。去吧。”

Seema 竖起大拇指说：

“苹果汁。”

猴子发出了尖叫。

“这是一个错误消息。它发生在使用了未定义的变量时。苹果汁就是未定义的变量。我们通常喝朗姆或威士忌。

```bash
$ sh -u <script>
$ set -o nounset
$ set -u
```

在使用未定义变量时给出错误消息。

Linux 中有一个 `dialog` 工具。

语法是：

```bash
dialog --msgbox "我需要朗姆" 9 18
```

9 和 18 是维度。

有各种选项。消息可以是消息框、信息框等。使用 `man` 命令并在我的笔记本电脑上试试吧。”

Seema 在她的笔记本电脑上尝试了一下，并探索了各种选项。接着 Lingaraj 打开包，给猴子们分了一些香蕉。

# C 编译器

当他们回到 Lingaraj 的家时，Seema 开始询问 Lingaraj 父母的情况。

“我父亲在瑞典参加一个生物技术会议。我母亲正在去拉达克和喜马拉雅山旅游。”

“是什么让你选择学习 Linux 的？对我来说，它是必需品。”

“我喜欢 Linux，是因为它让像我这样简单的程序员也能看到那些地位高大的资深程序员所看到的东西。这里的一切都是共享的，它是人类汇聚的例子之一，尽管在某种程度上是为了给世界带来一些贡献，而不是真正为了利润。

现在，我们来谈谈编译器。

编译器将你写的类人类可读的形式转换为机器可读的形式。”

Lingaraj 在他的笔记本电脑上向她展示了一个 C 程序的一部分。

```c
pthread_t t1, t2;
pthread_mutex_t mutex1;
pthread_mutex_init(&mutex1, NULL);
int iret1 = pthread_create(
    &t1,
    NULL,
    (void *) print_func,
    (void *) message
);
int iret2 = pthread_create(
    &t2,
    NULL,
    (void *) print_func,
    (void *) message
);
pthread_join(t1, NULL);
pthread_join(t2, NULL);
```

“哦！这是机器可读的形式。”

“不，那是人类可读的。”

Seema 大吃一惊。

“Linux 通常使用 `gcc`。它是一个 C 编译器，可以编译 C、C++ 等更多语言。”Lingaraj 继续说道。

秘诀在于能够用它自己的语言与其交流，并根据条件让它执行任务。

“你家里住着谁？”Lingaraj 问。

“我母亲。”

“你来这里之前给她下过什么指令吗？”

“是的，我说过‘除非你非常熟悉这个人，否则不要开门’。”

“看，这就是程序。你为了安全对她进行了编程。

机器也是一样。但它们只理解 0 和 1。最基础的是门，它们根据条件决定是否允许电流通过。所以，这种取决于条件的行为构成了计算机。一种在泥土中发现元素允许电流单向通过，这使得电子和计算机世界成为可能。

所以，你对计算机说的每一行话，电流都会以特定的方式流动并发生操作。你需要学习 C 语言。我本想建议你读读我写的书，但我还没写。我建议你参考这本书。”Lingaraj 说着递过一本关于 C 语言的书。

第二天 Seema 回来，她已经研读了这本书并做了笔记。

“我学了一点 C 语言。我现在知道‘Hello world!’程序了。”

“我们现在来看一下结构体和指针。结构体就像把不同类型的相关变量放在一个篮子里的方法。一个例子是：

```c
struct example_structure {
    int any_number;
    char one_letter;
};
```

可以这样访问成员：

```c
example_structure.any_number
example_structure.one_letter
```

大部分数据（如变量）都存储在内存中。现在，C 允许你根据内存地址来访问该变量。存储变量地址的变量被称为指针。可以获取变量的地址，也可以获取存储在那里的值。

例如：

```c
#include <stdio.h>

int main() {
    int variable1 = 20;
    int *vp;

    vp = &variable1;

    printf("The address of variable1 is %p\n", (void *) &variable1);
    printf("Address stored in variable vp is %p\n", vp);
    printf("The value of the variable variable1 is %d\n", variable1);
    printf("The value at the address given by variable vp is %d\n", *vp);
}
```

“我们可以尝试这个程序来找找感觉。我还不给你我是如何运行它的。”

Lingaraj 运行程序，输出显示在屏幕上。



`The address of variable1 is我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。0x7ffe17ff187cAddress stores in variable vp is 0x7ffe17ff187cThe value of the variable variable1 is 20The value at the address given by variable vp is 20`

地址是特定于机器和实例的。但如果你看到它，就能理解指针是如何工作的。

“让我们测试一下‘Hello World’程序。那么，你如何调用 `gcc`，即 GNU C 编译器？你只需要输入 `gcc` 和程序名。编译器会将可执行二进制文件保存为目录下的 `a.out`。但如果你灵感爆发，想给它起别的名字，可以使用 `-o` 选项。”

然后 Lingaraj 像往常一样，跳转了一个完全无关的话题。

“如果你带一只鳄鱼去兽医那里打疫苗，医生会看到它是南方鳄鱼，并用南方鳄鱼的语言与它交流。他不会用北方鳄鱼语和它交流。同样，`gcc` 是一个交叉编译器。这意味着它可以理解自己的身份并编译

## 文件和目录

让我们看看 Linux 系统。在此之前，我想向你介绍一下‘Thing Thimma’。”

他们散步到达一片甘蔗田。那里风景优美，他们注意到远处有一个精致的小屋。一如既常，Lingaraj 携带着他的笔记本电脑。当他们靠近小屋时，可以看到榨完汁后堆成山的甘蔗渣。小屋里有一个男人在工作。

“嗨，TT。这是 Seema。她正在学习 Linux。”Lingaraj 说。

Seema 继续与 TT 握手。

“Thimma 忙于制作甘渣板，用榨汁后的甘蔗渣做的盘子。告诉我 Thimma，你今天过得怎么样？一切还好吗？”

“噢，今天真是够呛的。我从那家伙那买的那个东西有个故障，我不得不在这个东西里找那个那个东西，好让这个东西像我习惯的那个那样运行。所以我去找了卖用来用那个东西的那个家伙，那家伙他问我要这个东西，你看……”

“住住。你可以走了。”林加拉杰（Lingaraj）说道。

蒂玛 回到了他的小屋。

“我明白意思了。“东西蒂玛’听起来挺好听。”西玛（Seema）说道。

“所以，蒂玛把一切都看作‘东西’。从螺丝、齿轮、压力机、机器、手机等等。Linux 也是如此。万物皆文件。从文本文件、程序、目录、设备，Linux 将一切都视为文件。”

“好。”

“在 Linux 中，有用于处理文件的命令。现在是 `open`。这个命令是做什么的？”林加拉杰问西玛。

“打开文件。”

“`close`？”

“关闭文件。”

“`read`？”

“读取文件。真希望我在学校得读那些书的时候有这个系统。它能替我全部读完。”

“要写一个程序让系统为你读取并将其全部传输到你的大脑里，那意味着需要更多的阅读。现在，`write`？”

“写入文件。这太简单了。我们本该从这个开始的。”

“`ioctl`？”

“呃……`ioctls` 文件？”

“有一天，当你得为维贾伊（Vijay）编程时，这对你来说就很重要。它将控制权交给设备驱动程序。”

西玛带着疑惑地看着他。

“他的心。你觉得他的心还在那里吗？关于他的最新进展是什么？”

“医生说，他盯着我们的一张照片——那是很久以前去那家披萨店时拍的——直直看了两个小时。”

“似乎是个积极的进展。”

“然后医生把我的电话号码放在他面前。他随后给我打了电话，并订了五个披萨。”

“可怜的家伙，你送过去了吗？”

“没有！”

“继续。。有用来存储文件的目录。在 Linux 中它们也被视为文件，但是特殊的。可以通过高层接口 `opendir` 或 `readdir` 访问。高层并不意味着高人一等。它的意思是层次更高，因为有很多编程工作在它下面。它不是直接访问系统，而是通过很多程序实现的。”

“作为一个男人，你告诉我是，他的爱情文件存放在哪个目录里。”

林加拉杰看起来深受灵感。

“实际上，这给了我写情诗的灵感。”

林加拉杰坐在一块石头上开始在笔记本电脑上打字。

```
I have your love files in my heart directory
My heart is now, a love producing factory
You just say opendir or readdir
And it will be like drinking elixir
```

林加拉杰梦幻地望着甘田地。

“你的问题是什么？”过了一会儿他问道。

“忘了吧。”

“无论如何，文件的创建、权限都存储在 `inode` 中。`Inode` 可以被看作文件的社会身份证。”

我曾和那个叫普塔普（Prathap）的家伙闹过架。是为了争夺能和野牛合影。

![](img/image_rsrc848.jpg)

“我太讨厌他了，以至于开始跟踪他。我得到了太多关于他的信息，甚至在他结婚时，他的未婚妻都来见我。”

![](img/image_rsrc849.jpg)

“为了让你们重归好？”

“不，她是想从我这里了解更多关于普塔普的信息，因为我比任何人都了解他。我变成了他的一个‘inode’。收集着所有的信息。”

“你是怎么摆脱这种……这种仇恨的？”

“噢，我原谅他了。”

“怎么做到的？”

“当我看到他在睡觉时，挡住三头野牛袭击我和我的家人。实际上我只是假装睡觉。如果他丧命了，我会出手自己制服那些野牛的。但他尽力所能了。”

“他现在在哪？”

“他现在在肯尼亚拍野牛的纪录片。几年前他发过视频链接给我。”

“好看吗？”

“我不清楚，我没看。”

“这有一种东西叫礼貌和感激。”

“无论如何，回到目录。目录简单地包含了其中所有文件的 `inode` 编号。如果一个文件被删除，目录中的 `inode` 条目就会被删除。该文件的链接数会减一。如果文件在另外两个目录中，意味着它有 2 个链接。如果两个目录中的文件都被删除，链接数就会归零。它所拥有的数据块会被标记为空。你如何回到主目录？”

“`cd`？对吧？”西玛问道。

“还有一种方法，`cd` 加波浪号。”

| `$ cd ~` |

“我有一个冷笑话。

咚，咚。”

“是谁呀？”

“波浪号（Tilde）。”

“波浪号是谁（Tilde who）？”

“直到今天还没有人为我敞开心扉。”

“我真的累了。”

课程结束了，林加拉杰向西玛介绍了一个开船的男人。船夫带她去划了次船，西玛非常享受。

第二天。林加拉杰在他家里继续。

“让我们来看一些硬件文件。三个。我们从这一个开始。”

| `dev/console` |

这是系统控制台。通常是显示消息的地方。

| `dev/tty` |

这是控制终端。

| `dev/null` |

这是空设备（设备）。写入这里的数据会被丢弃，从这里读取会返回 EOF（文件结束符）。

| `dev/zero` |

这是一个特殊设备，提供无限的空字节流。

| `dev/random` |

这是一个提供随机数的设备。

| `dev/urandom` |

这是一个提供伪随机数的设备。

| `dev/sda` |

这是第一块硬盘。

| `dev/sdb` |

这是第二块硬盘。

| `dev/sdc` |

这是第三块硬盘。

| `dev/sda1` |

这是第一块硬盘上的第一个分区。

Seema 一生中从未听过如此荒唐的话。但 Lingaraj 说得听起来非常有说服力。

“我们继续吧，”Seema 说道。

“你可以使用系统调用或 C 库函数。系统调用是昂贵的。”

“在哪个方面昂贵？”

“以前有一个叫 `Ceremony Seena` 的家伙。每当我们以前叫他时，他都会带着车队和随从来。邀请他以及接待他有一套巨大的仪式和礼仪。

他住在连接所有道路的主路上。他的随从会封堵道路几个小时。他人关系很广，与权力高层的人接触。如果有信息需要传给那些权人物，人们必须通过他。但每当有人叫他时，他就会举行盛大的仪式。我们还得养他、养他的追随者等等。我们必须在工作和照顾他之间来回。这是开销。所以，后来人们发明了这些方法，只叫他一次并一次性完成所有任务。系统调用就像叫 `Seena`。非常昂贵。但让人去处理细节并完成他所有的工作，就像是层级访问。所以，我们为这些操作提供了 C 库函数。

例如是标准 I/O 库。你可能有一个处理数据块的数据存储。标准 I/O 库会为发送到存储的数据量身定制，即使它是一个不是用于按块写入数据的文件。

那么，如何判断一个调用是系统调用还是函数？

C 库函数描述在 man 页（man pages）的第 3 节。第 2 节用于系统调用。

所以，如果你输入

```
$ man 2 fopen
```

它显示

```
No manual entry for fopen in section 2
```

然而，如果你输入

```
$ man 3 fopen
```

它显示了 `fopen` 的条目。

在其余大部分时间里，我使用“C 库函数”这个短语，并将 C 库函数称为“function”。对于程序内部的函数（如 routine），我直接用 function。你必须识别我谈论的是 C 库函数还是例程。

“文件描述符。你太想在 Vijay 的系统中打开一些文件了。”

“并且向它们写入。”

“你需要文件描述符来实现。”

“什么是文件描述符？”

“它是与文件关联的整数。它和 `inode` 有什么区别？`inode` 是一个包含文件信息的结构。文件描述符用于系统调用。它被系统用来引用一个已打开的文件。”

然后向她展示了一个程序。

`writestd.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
int main(){
    if ((write(1, “Standard output’s file descriptor is 1”, 38)) != 38)
        write(2, “Error writing to even standard output.”,39);
    exit(0);
}
```

上述程序的作用是，尝试将 `write` 指定的第一个消息“Standard output’s file descriptor is 1”写入文件描述符为 1 的标准输出。该字符串排除双引号有 38 个字符。它返回写入的字节数。每个字符一个字节。如果所有字节都没有被写入，它将移动到下一行并将错误信息“Error writing to even standard output.”打印到标准错误，标准错误的文件描述符为 2。标准输入的文件描述符是 0。

`readinp.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
void main(){
    printf(“Please input some text.\n”);
    char readinp[128];
    read (0, readinp, 17);
    printf("%s", readinp);
}
```

上述程序从标准输入读取 17 个字符，这是在你运行程序后输入时发生的。然后它迅速打印你输入的前 17 个字符。所以，`read` 和 `write` 系统调用的语法为：

```c
#include <unistd.h>
size_t read(int fildes, void *buf, size_t nbytes);
#include <unistd.h>
size_t write(int fildes, const void *buf, size_t nbytes);
```

`<unistd.h>` 是头文件。头文件包含声明和宏。与可以执行工作的库不同，它不包含实现。它只是调用了执行工作的函数。你可能奇怪过在某些组织中，有些领导什么工作都不做，但认识人脉，尤其是那些在图书馆学习的人，他们可以工作，即使领导自己对实现一无所知。我这么说只是为了帮你记忆。你可以写自己的头文件，但如果你想包含它，你可以使用

```c
#include “myheaderfile.h”
```

另外，让我谈谈系统调用。内核并不是所有人都可以自由使用的。分配内核一部分供用户使用系统是相当保留的。但有时你需要内核来执行某些操作。它们可以是进程控制、文件或设备管理等。用户没有胆量自己修改这些东西。他们需要请求内核的支持，内核根据它的规则允许程序在这些操作上运行。所以，这种模式被称为监控模式或内核空间，因为涉及到内核的监督。

每个系统调用 `read` 或 `write` 都返回读取的字节数。`filedes` 是文件描述符。`buf` 是你必须预先声明的字符字符串，`nbytes` 是字节数。

“这是 Ranganath 主管家吗？”

“是的，Ranganath，政府交通与旅游部门的主管。”

“我以为这种故事仅限于你的感情生活。在感情生活之外，你也没做过什么大事，”Seema 说道。

“如果你需要一个文件描述符，你就得打开文件。有几种模式可以打开它们。有时候，剧作家只想听听角色的对话，那就是只读模式。这必须在括号内的命令中指定。选项有：

- `O_RDONLY`: 以只读方式打开：（剧作家只想听。）

- `O_WRONLY`: 以只写方式打开（剧作家只提供新对话。不听。）

- `O_RDWR`: 以读读写方式打开（剧作家既听，又提供新对话。）

```
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>
int open(const char *path, int oflags);
int open(const char *path, int oflags, mode_t mode);
```

`char *path` 是要打开的文件路径。`oflags` 参数由上述特殊访问模式 `O_RDONLY`、`O_WRONLY` 和 `O_RDWR` 组成，必须通过“或”（`|`）操作与其他标志位一起。现在，排练中有很多场景。

让我们来看 `oflags` 参数：

| Flag | 描述 |

| :--- | :--- |

| `O_APPEND` | 将数据追加到文件末尾。可能需要追加一组新行。给那家伙更多台词，特别是如果他表现不错。 |

| `O_TRUNC` | 将文件截断为零，丢弃现有内容。通过删除给他的所有台词来侮辱并表示他不擅演技的一种方法。 |

| `O_CREAT` | 如果必要，则根据 mode 中给出的权限创建文件。可能需要创建一个新角色。 |

| `O_EXCL` | 与 `O_CREAT` 一起使用，确保只创建一个实例。如果该文件已存在，则不会创建。可能需要创建一个剧中独一无二的新角色。 |

现在，我们如何找到文件描述符编号呢？`open` 系统调用返回正整数作为文件描述符。如果失败则返回 -1。

当你使用 `O_CREAT` 时，需要使用以下后续模式。

| Mode | 描述 |

| :--- | :--- |

| `S_IRUSR` | 读取权限，所有者 |

| `S_IWUSR` | 写权限，所有者 |

| `S_IXUSR` | 执行权限，所有者 |

| `S_IRGRP` | 读取权限，用户组 |

| `S_IWGRP` | 写权限，用户组 |

| `S_IXGRP` | 执行权限，用户组 |

| `S_IROTH` | 读取权限，其他人 |

| `S_IWOTH` | 写权限，其他人 |

| `S_IXOTH` | 执行权限，其他人 |

如果你想指定更多选项，请使用 `|`（管道位或）选项。我稍后会在程序向你展示它是如何工作的。还有一个 `creat()` 系统调用，它是：

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int creat(const char *pathname, mode_t mode);
```

调用 `creat()` 等同于调用标志位等于 `O_CREAT|O_WRONLY|O_TRUNC` 的 `open()`。

此外，某些函数会设置全局变量 `errno` 并赋予它一个错误代码。我是这个 `errno` 的粉丝。当你约一个女性时，如果她拒绝了，她可以私下设置 `errno`。你可以查一下看看为什么被拒绝了。有一次我想和 Roshni 出去，给了她一封带有表格的信。表格包含了 `errno` 一列。她在信中像往常一样回答了“不”。她是一个程序员，知道这个 `errno` 的概念，知道我是它的粉丝。所以我去检查了 `errno`，上面写着 `errno`。我问她那是什么意思。她说：“err…………不！”

“理解 Linux 比理解你容易，”Seema 回答道。

“现在，在我们社区里，一个戏的字符数量限制在 16 个。同样，一个进程同时可以打开的文件数量也限制在 16 个。这由 `limits.h` 中的 `OPEN_MAX` 定义。这是是可以修改的。”

```
#include <unistd.h>
int close(int fildes);
```

成功返回 0，错误返回 -1。

这就是如何关闭文件的方法。我会向你展示一个名为 ‘filecopy.c’ 的程序。

```
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
int main(){
  char c;
  int in,out;
  in=open("inputfile", O_RDONLY);
  out=open("outputfile", O_WRONLY|O_CREAT,S_IWUSR|S_IRUSR);
  while(read(in,&c,1) == 1)
      {
      printf("%c",c);
      write(out,c,1);
      }
close(in);
close(out);
  exit(0);
}
```

`$ gcc filecopy.c -o filecopy`

`$ ./filecopy`

`$ cat outputfile`

这就是如何复制文件的方法。

“为了社会的利益，仪式官 Seena 必须传递这些信息。由于协议的成本太高，我们设置了消息信使。就像这些外卖伙伴一样。这些消息信使从人们那里收集信息，最后交给仪式官 Seena 让他们在傍晚进行打印。这样一来，大家都很开心。

所以这些高层调用就像这些消息信使，在不产生太多开销的情况下，让 Seena 参与进来。



有些 C 库函数可以节省系统开销。它们是：

| 函数 |
|---|
| `fopen` |
| `fclose` |
| `fread` |
| `fwrite` |
| `fflush` |
| `fseek` |
| `fgetc` |
| `getc` |
| `getchar` |
| `fputc` |
| `putc` |
| `putchar` |
| `fgets` |
| `gets` |
| `printf`、`fprintf` 和 `sprintf` |
| `scanf`、`fscanf` 和 `sscanf` |

```c
#include <stdio.h>
FILE *fopen(const char *filename, const char *mode);
```

`fopen` 打开由 `filename` 参数命名的文件并与其关联一个流。`mode` 参数指定了打开文件的方式。它是以下字符串之一：

| 模式 |
|---|
| “r” |
| “w” |
| “a” |
| “r+” |
| “w+” |
| “a+” |

它是作为流打开的，而不是作为文件。

“流（stream）和文件描述符（file descriptor）的区别是什么？”

“区别在于系统看待文件的方式。流是高层访问。如果你想对文件执行控制操作，你需要使用文件描述符。文件描述符可以简单发送或接收数据，但打开一个流使得格式化的输入输出成为可能。

这就像是微妙地、有技巧地处理情况与否。你以特定的方式交谈，展现各种礼仪。打开文件描述符更多是关于控制。

这是技术性与诗意之间的区别。”

“继续下去，如果你正在浏览 Vijay 大脑中的文件，而你遇到了一个描述了 Vijay 与一个名为 Asha 的女性约会记忆的文件，你会怎么做。”Lingaraj 问道。

“我会问他，Asha 是谁。”

“而 Vijay 会毫无畏惧地回答，因为他现在是一台机器了。更智能的选择是修改文件。你可以将它们设置为只读。或者更新文件将 Asha 的名字改为你的名字。或者追加，添加细节如 Asha 对 Vijay 并不好，她和他吵过架。或者完全删除所有内容。”

“我会完全删除所有内容。”

“再次，打开文件的语法是：

```c
FILE *fopen(const char *filename, const char *mode);
```

该 C 库函数返回指向相关文件流的指针。

```c
#include <stdio.h>
size_t fread(void *ptr, size_t size, size_t nitems, FILE *stream);
#include <stdio.h>
size_t fwrite(const void *ptr, size_t size, size_t nitems, FILE *stream);
```

在刚才提到的 C 库函数中，`fopen` 返回的文件流被用于读取和写入。`fread()` 和 `fwrite()` 返回已写入或读取的数据的大小。

```c
#include <stdio.h>
int fclose(FILE *stream);
```

`fclose` 关闭文件。即使没有调用 `fclose()`，文件也会关闭。但它并不是完全多余。`fclose()` 返回一个整数，可以用于失败时检查错误。

```c
#include <stdio.h>
int fflush(FILE *stream);
```

这会导致文件流上的数据被立即写入。如果你在使用 `fclose()`，则没需要使用它，因为调用 `fclose()` 会执行刷新操作。

```c
#include <stdio.h>
int fseek(FILE *stream, long int offset, int whence);
```

`fseek` 将你带到文件的特定位置。

```c
#include <stdio.h>
int fgetc(FILE *stream);
int getchar();
```

`fgetc` 从文件流中读取下一个字节作为字符。

`getchar` 从标准输入读取字符。

```c
#include <stdio.h>
int fputc(int c, FILE *stream);
```

`fputc` 将一个字符放入文件流。

```c
int putchar(int c);
```

`putchar` 将一个字符输出到标准输出。

```c
#include <stdio.h>
char *fgets(char *s, int n, FILE *stream);
char *gets(char *s);
```

`fgets` 从文件流读取字符并写入字符串。

“那 `gets` 呢？它是做什么的？”Lingaraj 突然问道。

“`gets` 从标准输入读取字符并写入字符串。”Seema 勤奋地回答道。

“据我所知，它的功能得多，建议不要使用它。”Lingaraj 警告道。

```c
#include <stdio.h>
int printf(const char *format, ...);
int sprintf(char *s, const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);
```

“我希望你在 C 语言中涵盖了这些。”Lingaraj 问道。

“是的，我会解释。

`printf` 在标准输出上产生输出。

`sprintf` 写入字符串。

`fprintf` 写入特定的流。”Seema 说道。

“好的。这是你所知道的打印格式。你会经常用到它，所以我们在这里来看一遍。”

| 格式 |
|---|
| `%d`、`%i` |
| `%o`、`%x` |
| `%c` |
| `%s` |
| `%f` |

```c
#include <stdio.h>
int scanf(const char *format, ...);
int fscanf(FILE *stream, const char *format, ...);
int sscanf(const char *s, const char *format, ...);
```

`scanf` 从标准输入获取数据。`fscanf` 从文件流获取，而 `sscanf` 从字符串获取。打印让我想起了这些。”Lingaraj 说。

“流和文件描述符并不是像油和水那样的，

```c
#include <stdio.h>
int fileno(FILE *stream);
FILE *fdopen(int fildes, const char *mode);
```

`fileno` 告诉你流的文件描述符。

`fdopen` 根据文件描述符和模式打开一个文件流。`fopen` 也打开了文件，但是使用文件名。

所以，文件描述符和流之间存在联系，它们并不是对立的选择路径。

接下来是伪代码。一种构建程序的方法。伪代码通常更易理解，但既然我在这里陪着，我想我们可以跳过详细的指导部分。这是一个使用 `FILE` 流从一个文件读取并写入另一个文件的程序。这并不是一个完整的程序，因为完整的程序可能是在喂饭给你你。我希望你根据这些信息写一个程序并在你的系统上尝试。”Lingaraj 向 Seema 展示了他笔记本电脑上的一个文本文件。

# 文件操作与权限

- 包含必要的头文件。
- 启动 `main()` 函数。
- 声明两个类型为 `FILE` 的流，一个用于输入，另一个用于输出。
- 使用 `fopen()` 以读模式打开输入文件。将返回的文件流赋值给已声明的文件流变量。
- 以写模式打开输出文件。再次将返回的文件流赋值给声明的变量。
- 使用 `while` 循环从输入文件流中获取一个字符，并使用输出文件流将其写入输出文件，直到到达文件结束符（`EOF`）。
- 退出。

## 文件权限故事

当你查看我目录中的文件时，你会看到很多像这样的字符：`rwx`。

它们是权限（permissions）。我来向你展示我的烹饪目录。

Lingaraj 在他的笔记本电脑上打开了烹饪目录。他展示了一个条目：

| 文件 | 权限 |
|---|---|
| 药草面包 | `rw_rw_r__` |

第一组三个字符代表用户（user），第二组代表有文件访问权限的用户组（group），第三组代表其他人（others）。

- `r` 代表读（read）。意味着我可以读取这个文件。
- `w` 代表写（write），意味着我可以向这个文件写入。
- 缺失的位 `x` 代表可执行（executable）。由于这是一个文本文件，它是无法执行的。”

Lingaraj 远视远方。Seema 感觉到一个故事要来了。

“我曾经拥有一群羊。我过去通过用基础技术训练羊来授予权限。我曾会把给那些签了合同的人的照片展示给这些羊看，羊就会信任那些家伙。羊毛给某一个人，牛奶给另一个人，粪便留给第三一个人。”

![](img/image_rsrc84M.jpg)

“后来我懒得维护它们了。我过去常让它们自由奔跑。这些羊被训练得非常好，如果一个拿了牛奶合同的人试图拿一些羊毛，羊就会咬他。所以，一个用户无法访问不属于他的文件。”

“我猜结局并不好。发生什么事了？”

“有一天，我发现它们不见了。”

“是有人杀了它们吃肉吗？”

“不是。一个邻国的国王把这些羊征兵进了他的军队。”

“为什么？”

“因为羊的叫声能把敌人身上的粪便逼出来。”

![](img/image_rsrc84N.jpg)

Seema 真心希望笔记本电脑没有掉在 Vijay 的头上。Lingaraj 继续说道。

## 用于设置所有权的系统调用

```c
#include <sys/stat.h>
int chmod(const char *path, mode_t mode);
```

这会更改文件或目录的模式。

```c
#include <sys/types.h>
#include <unistd.h>
int chown(const char *path, uid_t owner, gid_t group);
```

这会更改文件或目录的所有权。你从哪里获取 `uid_t` 和 `gid_t` 的值？通过 `getuid()` 和 `getgid()` 调用。`getuid` 和 `getgid` 分别返回用户 ID 和组 ID。它们不是整数，而是 `uid_t` 和 `gid_t` 类型，但它们看起来像整数。

“就像这样。我们有一只叫 Stupid（呆呆）的狗。我来演示一下。” Lingaraj 带着 Seema 到了外面。

“Stupid!” Lingaraj 大声喊道。

![](img/image_rsrc84P.jpg)

一只狗突然出现，看起来很调皮。然后它看向 Seema 并试图攻击。

![](img/image_rsrc84R.jpg)

Seema 吓了。狗走近并要向 Seema 跳过去时，Lingaraj 喊道：`chown Seema`。

狗立刻改变了态度，摇起了尾巴。

![](img/image_rsrc84S.jpg)

Seema 喘了一口气。Lingaraj 解释道：“这只狗 Stupid 既会玩也很凶。每当有新人来时，如果狗试图攻击他，人们会立即使用这个命令 `chown name`。狗就会更新自己，认为自己是新主人，不再攻击他。它会和他一起玩。不用说，这狗是我训练的。这只是一个教你关于所有权和 ID 的例子。”

“你的手段也太低了，我觉得这是一个很‘蠢（stoopid）’的教学方法。”

“得好。”他们回到室内，Lingaraj 继续讲解。他向她展示了一些系统调用。

## 文件和目录管理

```c
#include <unistd.h>
int unlink(const char *path);
int link(const char *path1, const char *path2);
int symlink(const char *path1, const char *path2);
```

`unlink()` 类似于删除。除了在最后一个使用文件的进程终止后，该文件占用的空间会被释放。

`link()` 将一个文件链接到另一个文件。因此，可以通过指定 `path2` 来访问由 `path1` 指定的文件。如果 `path2` 指定的文件已经存在，则会报错。所以，`path2` 中的文件不应该存在。

当然，当你执行 `ls` 时，`path2` 指定的文件会被列出来，但它打开的是 `path1` 指定的文件。

```c
#include <sys/types.h>
#include <sys/stat.h>
int mkdir(const char *path, mode_t mode);

#include <unistd.h>
int rmdir(const char *path);
```

创建和删除目录。你知道 `rmdir` 是移除目录的。关于模式，你是知道的。`rmdir` 只有在目录为空时才有效。

关于目录的切换：

```c
#include <unistd.h>
int chdir(const char *path);
```

切换目录。

## 目录遍历

```c
#include <unistd.h>
char *getcwd(char *buf, size_t size);
```

切换目录。为了说明，看这个程序：

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <unistd.h>

int main(){
    char word[1024];
    int fd = open("/tmp", O_CREAT | O_WRONLY);
    write(fd, "Lingaraj", 8);
    close(fd);
    getcwd(word, 1024);
    printf("当前目录是：%s\n", word);
    chdir("/tmp");
    getcwd(word, 1024);
    printf("当前目录是：%s\n", word);
}
```

## 目录项详情

目录函数定义在 `dirent.h` 中。它们使用结构体 `DIR`。`opendir` 函数打开目录并创建一个目录流。

```c
#include <sys/types.h>
#include <dirent.h>
DIR *opendir(const char *name);
```

`opendir` 在失败时返回空指针。

```c
#include <sys/types.h>
#include <dirent.h>
struct dirent *readdir(DIR *dirp);
```

上述库函数返回目录结构中的下一个项。为什么不是当前项？因为 `opendir` 已经返回了第一个项。我们需要之后的。

```c
#include <sys/types.h>
#include <dirent.h>
long int telldir(DIR *dirp);
```

它告诉你目录流中的当前位置。

```c
#include <sys/types.h>
#include <dirent.h>
void seekdir(DIR *dirp, long int loc);
```

这用于设置目录项指针。它与 `readdir` 的区别在于 `readdir` 返回下一个项，而这个库函数可以让 `readdir` 返回后面或之前的目录项。但位置 `loc` 必须预先通过 `telldir` 获取。

“如果调用 `telldir` 获取一个 `loc` 的位置，然后调用 `seekdir` 并传入相同的位置，我在实现什么？指针会停留在。”

“通常情况下，你需要创建一个循环，并使用 `telldir` 获取连续项的目录位置 `loc`。然后，你可以选择将 `loc` 值传递给 `seekdir`。”

```c
#include <sys/types.h>
#include <dirent.h>
int closedir(DIR *dirp);
```

以下程序将显示当前目录下的所有文件。

`displaydir.c`

```c
#include <unistd.h>
#include <stdio.h>
#include <dirent.h>
#include <stdlib.h>

void displayfiles(){
    DIR *dp;
    struct dirent *entry;
    char dir[1024];
    getcwd(dir, 1024);
    if((dp = opendir(dir)) == NULL) {
        printf("Cannot open the specified directory: %s\n", dir);
        exit;
    }
    while((entry = readdir(dp)) != NULL) {
        printf(" Name of file is : %s\n", entry->d_name);
    }
    closedir(dp);
}

void main(){
    printf("Beginning to display contents of current directory.\n");
    displayfiles();
    exit(0);
}
```

`->` 实际上是一个特殊字符，但在程序中你使用 `->`，它是一个减号后跟着大于号。我们通常通过 `structure.member` 来访问结构体成员，但如果它是指向结构的指针，我们使用 `pointer_to_structure->member`。

你可能获得的错误类型有：

- `EPERM`
- `ENOENT`
- `EINTR`
- `EIO`
- `EBUSY`
- `EEXIST`
- `EINVAL`
- `EMFILE`
- `ENODEV`
- `EISDIR`
- `ENOTDIR`

```c
#include <string.h>
char *strerror(int errnum);
```

`strerror` 是一个 C 库函数，给它一个错误号时，它告诉你错误是什么。它返回一个指向包含消息字符串的指针。



```c
#include <stdio.h>
void perror(const char *s);
```

这会打印出跟随`s`中指定的字符串之后的最新错误。

## 内存与命令行参数

Lingaraj 开始说道。

“我们可以使用一个文件并将其存储在特定的内存位置。”

一个例子是将鸡尾酒配谱放在特定的位置。你可以指定该位置，也可以将其交给内核处理。通常，根据我爷爷的指示，我们把它放在池塘边的岩石上。你甚至可以指定它是可读、可写还是可执行。你甚至可以允许其他文件和进程访问内存位置。这很有用，因为当我们把它放在那些岩石上并回来收集时，会有昨晚进行实验的人添加更多的配谱。此外，我们还发现这个配谱的发明者仍然躺在那里神志不清。

![](img/image_rsrc84T.jpg)

语法是：

```c
#include <sys/mman.h>
void *mmap(void *addr, size_t len, int prot, int flags, int fildes, off_t off);
```

“很多参数。”Seema 说道。

“让我们想象我们有一种叫做‘冲突抑制器’的鸡尾酒，如果你看我爷爷关于这个的文本文件，文件的内容是：

‘这是一个冲突抑制器，那些卷入争吵的双方被给予了剂量，让他们忘记逻辑。这是通过……实现的’”

“忘掉内容，告诉我参数是什么。”Seema 说道。

- `addr` 是内存中的地址。通常为 `0`，让内核自行决定。
- `len` 是内存块的长度。
- `prot` 是设置权限的：
  - `PROT_READ`：你可以读取该段。
  - `PROT_WRITE`：该段可以被写入。
  - `PROT_EXEC`：该段可以执行。
  - `PROT_NONE`：无法访问段。
- `flags` 参数控制程序对段进行的更改如何反映在其他地方。
  - `MAP_PRIVATE`
  - `MAP_SHARED`
  - `MAP_FIXED`
- `filedes` 是文件描述符。
- `off_t` 是偏移量。

```c
#include <sys/mman.h>
int msync(void *addr, size_t len, int flags);
```

如果有更改，`msync()` 会更新映射的文件。类似于`fflush`。

这就像保存。

标志有：

- `MS_ASYNC`：调度一次更新，但调用立即返回。
- `MS_SYNC`：请求更新并等待其完成。
- `MS_INVALIDATE`：使对同一文件的其他映射失效。（当你想要用刚刚写入的最新值进行更新时非常有用。）

Seema 尝试解释这些标志。

“我不像你那么擅长类比或讲奇怪的故事。但`MS_ASYNC`就像让你的下属去做一项工作，告诉他然后回来。`MS_SYNC`就像一直在那里直到工作完成。

`MS_INVALIDATE`就像对你的下属说：‘不要听任何别人的指令。’”

```c
#include <sys/mman.h>
int munmap(void *addr, size_t len);
```

`munmap`释放内存段。如果 Vijay 的内存中充满了关于某个 Sanjana 或 Savitri 的信息，你会发现它很有用。”

Lingaraj 给她看屏幕。

“看这里。”

`mapandunmap.c`

```c
#include <string.h>
#include <unistd.h>
#include <stdio.h>
#include <sys/mman.h>
#include <fcntl.h>
#include <stdlib.h>
typedef struct {
    int integer;
    char string[1024];
} RECORD;
int main(){
    RECORD record, *mapped;
    int i, f;
    FILE *fs;
    fs = fopen("records.dat","w+");
    record.integer = 1234;
    strcpy( record.string , "Seema doesn't understand Linux.");
    fwrite(&record,sizeof(record),1,fs);
    fclose(fs);
    f = open("records.dat",O_RDWR);
    mapped = (RECORD *) mmap(0, sizeof(record), PROT_READ|PROT_WRITE, MAP_SHARED, f, 0);
    printf("Number before changing the mapped value : %d\n", record.integer);
    printf("Sentence before changing the mapped value : \n%s\n", record.string);
    mapped->integer = 5678;
    strcpy( mapped->string , "Seema has learnt Linux.");
    msync(mapped, sizeof(record), MS_ASYNC);
    munmap(mapped, sizeof(record));
    printf("Number after changing the mapped value : %d\n", record.integer);
    printf("Sentence after changing the mapped value : \n%s\n", record.string);
}
```

这需要一些解释。

```c
#include <string.h>
#include <unistd.h>
#include <stdio.h>
#include <sys/mman.h> // 是一个重要的文件。
#include <fcntl.h>
#include <stdlib.h>
typedef struct {
    int integer;
    char string[1024];
} RECORD; // 定义了一个名为 RECORD 的结构体类型，它包含一个整数和一个字符串。
int main(){
    RECORD record, *mapped; // 我们声明了 record 和 mapped，mapped 指向类型为 RECORD 的结构体。
    int i, f;
    FILE *fs;
    fs = fopen("records.dat","w+"); // 我们打开一个文件流，因为我们需要格式化输出。
    record.integer = 1234;
    strcpy( record.string , "Seema doesn't understand Linux."); // 我们将字符串拷贝到结构体的成员中。
    fwrite(&record,sizeof(record),1,fs);
    fclose(fs);
    f = open("records.dat",O_RDWR); // 我们打开文件 records.dat，因为我们需要文件描述符来使用 mmap。
    mapped = (RECORD *) mmap(0, sizeof(record), PROT_READ|PROT_WRITE, MAP_SHARED, f, 0); // 返回值赋值给 mapped，正如我们已经声明的那样，它指向类型为 RECORD 的结构体地址。
    printf("Number before changing the mapped value : %d\n", record.integer); 
    printf("Sentence before changing the mapped value : \n%s\n", record.string); // 在这里，我们打印映射前的值。
    mapped->integer = 5678;
    strcpy( mapped->string , "Seema has learnt Linux."); // 我们更改了值。注意，我们没有直接更改 records.dat 文件中的结构体成员。我们更改的是映射的值，这些值应该反映在 records.dat 文件中。
    msync(mapped, sizeof(record), MS_ASYNC); // 我们更新映射内存并取消映射。然后关闭打开了 records.dat 文件描述符。
    munmap(mapped, sizeof(record));
    close(f);
    fs = fopen("records.dat","r+"); // 我们再次打开指向 records.dat 的文件流，因为我们需要读取存储在 records.dat 中的结构体。
    fread(&record, sizeof(record),1, fs); // 然后我们继续使用 fread 进行读取，并打印出那些已经更改的值。
    printf("Number after changing the mapped value : %d\n", record.integer);
    printf("Sentence after changing the mapped value : \n%s\n", record.string);
    fclose(fs);
    exit(0);
}
```

| 当我们运行它时，输出是： |
| --- |

更改映射值前的数字：1234

更改映射值前的句子：

Seema 不懂 Linux。

更改映射值后的数字：5678

更改映射值后的句子：

Seema 已经学会了 Linux。

## `getopt()`

假设你派你的朋友去帮着买一个手包。你会告诉她什么呢？”

“我会告诉她买一个带拉链的、有一个放小镜子的口袋、一个可以放手机的隔层，而且设计是红色的。预算是 750 卢比。”

“好的，`fetchbag()`将包含获取手包的指令。

而你说的所有其他东西都是选项。现在，这些选项将是：

- `--zip`
- `--pocket`
- `--mirror`
- `--cellphone holder`
- `--design`：red
- `--amount`：750 rupees

注意这些冒号。”

我们会使用代码。`z`、`p`、`m`、`c`、`d`、`red`和`a`是这些选项的简写，”Seema 说。

“如果是那样，我们将使用`getopt()`。你所做的就是指定以`-`为前缀的代码选项。`getopt()`会捕获这些选项并使其对被调用的程序可用。否则，你将使用`argv`列表，并根据选项前的`-`前缀来区分参数和选项。”

如果你认识的朋友正在帮着买它们，那没关系。但如果是像我这样不一定了解手包选项的人，我必须有一个程序根据你指定的选项，在每一步都告诉我该做什么。让我们从一个 C 库函数开始。

### 语法如下

```c
#include <unistd.h>
int getopt(int argc, char *const argv[], const char *optstring);
extern char *optarg;
extern int optind, optterr, optopt;
```

- `argc` 是参数的数量，包含了调用的函数。
- `argv` 是参数列表。
- `optstring` 是调用`getopt()`的程序可以接受的有效选项列表。这意味着，程序必须知道用户将传递什么样的选项，并且程序最好准备好一个`switch case`语句，根据传递的选项执行相应的操作。

如果一个像我这样不懂手包术语的用户传递了`-b`选项作为啤酒杯架，那么`getopt()`会识别出这超出了程序的范围并将其放入`optopt`中。因此，查看`optopt`就可以得到由不懂手包的用户传递的选项。

由于这每次`getopt()`运行时都会更新，因此它通常在循环中运行。

- `optind` 是索引，帮助`getopt()`在下次被调用时使用。由于`getopt()`返回程序收到的下一个选项字符，`getopt()`会一直运行，直到`getopt()`返回`-1`，这意味着没有更多选项了。如果遇到未知选项，它将返回`?`，即问号字符。

每个选项可能还有进一步的参数。例如，当你提到预算时，必须指定金额。该特定选项存在后续参数是通过选项字符旁边的`:`冒号指示的。该选项的指定参数也可以通过`getopt()` C 库函数`optarg`访问。因此，你的程序将是：

#### `fetchbag.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <ctype.h>
int main(int argc, char *argv[]){
    int option;
    while((option = getopt(argc, argv, "zpmcd: a:")) != -1)
    {
        switch(option) {
            case 'z':
                printf("So you want a handbag with a zip.\n");
                continue;
            case 'p':
                printf("So you want a handbag with a pocket.\n");
                continue;
            case 'm':
                printf("So you want a handbag with a mirror.\n");
                continue;
            case 'c':
                printf("So you want a handbag with a cellphone holder.\n");
                continue;
            case 'd':
                printf("You want a particular design. The design is %s.\n", optarg);
                continue;
            case 'a':
                printf("You have a budget for this. The budget is %s.\n", optarg);
                continue;
            case '?':
                if (optopt == 'a')
                    fprintf(stderr, "You need to be more specific for the option, %c.\n", optopt);
                    continue;
                else if (optopt == 'd')
                    fprintf(stderr, "For this option, you need to specify a design %c\n", optopt);
                    continue;
                else
                    printf("Looks like you't know much about handbags. %c is an invalid option.\n", optopt);
        }
    }
}
```

为了解释，



```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    int option;

    while ((option = getopt(argc, argv, "zpmcd: a:")) != -1) // 开始一个 while 循环和 getopt 函数，我们在其中列出了有效选项。在 d 和 a 之后，有一个 :，表示该选项需要一个参数。
    {
        switch (option) {
            case 'z':
                printf("So you want a handbag with a zip.\n");
                continue;
            case 'p':
                printf("So you want a handbag with a pocket.\n");
                continue;
            case 'm':
                printf("So you want a handbag with a mirror.\n");
                continue;
            case 'c':
                printf("So you want a handbag with a cellphone holder.\n");
                continue;
            case 'd':
                printf("You want a particular design. The design is %s.\n", optarg);
                continue;
            case 'a':
                printf("You have a budget for this. The budget is %s.\n", optarg);
                continue;
            case '?':
                if (optopt == 'a')
                    fprintf(stderr, "You need to be more specific for the option, %c.\n", optopt);
                    continue;
                else if (optopt == 'd')
                    fprintf(stderr, "For this option, you need to specify a design %c\n", optopt);
                    continue;
                else
                    printf("Looks like you't know much about handbags. %c is an invalid option.\n", optopt);
        }
    }
}
```

如果我们运行这个：

```bash
$ gcc fetchbag.c -o fetchbag
$ fetchbag -z -p -m -c -d red -a 750
```

输出是：

```text
So you want a handbag with a zip.

So you want a handbag with a pocket.

So you want a handbag with a mirror.

So you want a handbag with a cellphone holder.

You want a particular design. The design is red.

You have a budget for this. The budget is 750.
```

下次运行：

```bash
$ /fetchbag -z -p -m -c -d red -a
```

输出是：

```text
So you want a handbag with a zip.

So you want a handbag with a pocket.

So you want a handbag with a mirror.

So you want a handbag with a cellphone holder.

You want a particular design. The design is red./fetchbag: option requires an argument -- 'a'You need to be more specific for the option, a.
```

所以，你看到如果用户漏掉了某个选项的参数，程序会通知用户。

这次运行是我请求一个啤酒杯架选项：

```bash
$ ./fetchbag -z -p -m -c -d red -a 750 -b
```

输出是：

```text
So you want a handbag with a zip.

So you want a handbag with a pocket.

So you want a handbag with a mirror.

So you want a handbag with a cellphone holder.

You want a particular design. The design is red.

You have a budget for this. The budget is 750./fetchbag: invalid option -- 'b'Looks like you don't know much about handbags. b is an invalid option
```

但我们看到了一个缺点。并不是说我要让程序万无一失，但如果漏掉了作为 d 的参数 red：

```bash
$ ./fetchbag -z -p -m -c -d -a 750
```

它会显示这个输出：

```text
So you want a handbag with a zip.

So you want a handbag with a pocket.

So you want a handbag with a mirror.

So you want a handbag with a cellphone holder.

You want a particular design. The design is -a.
```

这里发生的情况是 `getopt` 假设 `-d` 之后的下一个选项（即输入的 `-a`）是选项 `-d` 的参数。用户必须输入正确的顺序，并在提供选项时保持精确。否则，它将再次涉及到对 `argv` 数组大量的扫描，并寻找选项后面是否有“-”之类的操作。

如果你想让我工作起来更简单，并使用长格式的选项，你可以使用：

```c
int getopt_long_only(int argc, char * const argv[], const char *optstring, const struct option *longopts, int *longindex);
```

有一个类型为 `option` 的结构体如下：

```c
struct option {
    const char *name;
    int        has_arg;
    int        *flag;
    int        val;
};
```

“所以，你可以通过这个结构体访问这些值，”Lingaraj 说道。

“你有什么关于包包的故事吗？”

“有。”

“而且结果对你来说很悲惨。”

“你是怎么猜到的？！”Lingaraj 惊讶地问。

“坦率地说，我甚至不需要猜。”

“我上大学的时候有一个女孩的生日。”

![](img/image_rsrc84U.jpg)

她非常刻苦，擅长做笔记，很多学生都想向她的笔记学习。期末考试刚公布，安排在几周后。一天，我得知那是她的生日。所以我想送给她一个独特的惊喜。她正在草坪上吃午餐，我看到她的包放在那里。由于她正忙着说话，我便用气球系住那个包。她并没有注意到。

![](img/image_rsrc84V.jpg)

系了大约 100 个气球并大喊道：“惊喜！”她转过头来。我松开手展示我的杰作。包连着气球飞走了。她的考试挂格了。”

![](img/image_rsrc84W.jpg)

Seema 真心希望希望能为 Lingaraj 的感情生活做点什么。Lingaraj 继续说道：

“Linux 环境。我有两份简历。其中一份，写着以下内容：

吸烟：否

喝酒：否

最喜欢的电视节目：纪录片

过往感情：无

视频游戏：否

等等。

在另一份中：

吸烟：偶尔

喝酒：偶尔

最喜欢的节目：惊疑片

过往感情：很多

视频游戏：射击僵尸等等。

你认为哪一个是真实的？”

“显然是第二个，”Seema 充满心地回答道。

“第二个是留给真朋友的。第一个是留给婚姻联盟的。所以我在这两个环境之间切换。

当我必须记住某个特定环境变量的值时，我使用这个 C 库函数：

```c
char *getenv(const char *name);
```

它告诉我由 `name` 指定的环境变量值。

如果我必须更改某个特定值，我使用：

```c
int putenv(const char *string);
```

字符串应该是这种格式：

`name=value`

例如：

`drink=beer`

当我和朋友在一起且必须骑马回家时，我会使用这个设置。

“那是因为当你喝得更多时，你就不稳定了，我想。”

“如果我想找到所有变量的值，我使用：

```c
#include <stdlib.h>
extern char **environ;
```

这是一个字符串数组，包含了变量列表。你可以在程序中使用 `while` 循环逐个地访问它们。好了，那明天见，”Lingaraj 突然说道。

## 时间相关函数

第二天，Seema 早上早起去散步。她看到一组大约 4 到 5 个人正在慢运动。

她加入了他们并发现很有趣。过了一段时间，她才意识到自己迟到了。Seema 尽快准备好，去按了 Lingaraj 家的门铃。门铃是一个简单的铃装置，不需要电力。

![](img/image_rsrc84X.jpg)

Lingaraj 出现在门口，Seema 能看到他。他留了一下，虽然看到了 Seema，但花了 5 分钟才开门。

“你为什么这么才开门？”Seema 略带地问道。

![](img/image_rsrc84Y.jpg)

“不。是你迟了。是你先开始的。请进。”

Seema 安顿后，她告诉 Lingaraj。

“我做了一些慢运动。”

“既然说到时间，

有一个时间系统调用，它能告诉你自 1970 年 1 月 1 日以来经过了多少秒。”

“秒？那可不方便。”

Lingaraj 给她看屏幕。

```c
#include <time.h>
time_t time(time_t *tloc);
```

它返回一个在 `time.h` 中定义的 `time_t` 类型整数，如果你以 `tloc` 的形式指定位置，它会将值存储在那里。

所以，如果你必须找到两个时间之间的差，你就调用 `difftime`：

```c
#include <time.h>
double difftime(time_t time1, time_t time2);
```

这将给出秒差。

如果你必须将一个分解的结构转换为原始时间，使用这个：

```c
#include <time.h>
time_t mktime(struct tm *timeptr);
```

“谁会需要那个？”

“我祖父以前用过。”

“但看起来没那么多了。”

“谢天谢我错过了他。”

“如果你想获取本地时间，使用：

```c
#include <time.h>
struct tm *localtime(const time_t *time);
```

这给了你本地时间。对于格林尼治标准时间，使用：

```c
#include <time.h>
struct tm *gmtime(const time_t *time);
```

如果你想打印时间，有一个比 `printf` 更好的时间输出工具。

```c
#include <time.h>
size_t strftime(char *s, size_t maxsize, const char *format, struct tm *timeptr);
```

`s` 是结果字符串。`format` 是你指定格式的地方、`%` 符号等。

你可以使用 `strptime` 函数，它接收一个表示日期时间的字符串并创建一个表示相同日期和时间的 `tm` 结构：

```c
#include <time.h>
char *strptime(const char *buf, const char *format, struct tm *timeptr);
```

另一个 `time` 命令用于命令行运行程序并计算系统资源消耗。

```bash
$ time ./a.out
```

对于人类可读的字符串，使用：

```c
#include <time.h>
char *asctime(const struct tm *time);
char *ctime(const time_t *time);
```

`asctime` 和 `ctime` 返回的是人类可读的字符串。

## 临时文件

Lingaraj 开始了这个话题。

“让我们谈谈临时文件。有时你可能需要创建临时文件。

```c
#include <stdio.h>
char *tmpnam(char *s);
```

它返回一个系统中不存在的唯一字符串。它也会更新字符串 `s` 中的内容。但问题是，另一个程序在你开始使用它之前，可能会创建一个同名的文件。

```c
#include <stdio.h>
FILE *tmpfile(void);
```

上面的 C 库函数创建并打开一个具有唯一名称的文件并返回一个文件流供立即使用。

```c
#include <stdlib.h>
char *mktemp(char *template);
int mkstemp(char *template);
```

如果你希望新文件名遵循某种模式或模板，可以使用上面提到的 C 库函数。模板可以是你想要的内容，后面跟着六个 X 字符。这六个 X 字符会被替换以生成唯一的文件。

`mktemp` 和 `mkstemp` 的区别在于 `mktemp` 只提供文件名。`mkstemp` 在打开文件后返回一个文件描述符。然而，建议仅使用 `tmpfile()` 和 `mkstemp()`。

## 用户 ID 和组

Lingaraj 提出了一个新话题。

“用户信息。提供 `uid`（即人员的用户 ID）的系统调用是：

```c
#include <sys/types.h>
#include <unistd.h>
uid_t getuid(void);
char *getlogin(void);
```

`getuid()` 系统调用返回与程序关联的用户 ID。这通常是运行该程序的用户的 UID。

`getlogin()` C 库函数返回当前用户的登录名。

```c
#include <sys/types.h>
#include <pwd.h>
struct passwd *getpwuid(uid_t uid);
struct passwd *getpwnam(const char *name);
```

你可以获取关于已知 ID 或名称的用户许多详细信息。上述 C 库函数返回一个 `passwd` 类型的结构。访问其内容即可获得细节。我假设你读过 C 语言，已经知道如何访问结构。”

“是的。”

“`passwd` 结构的成员有：

| 成员 | 描述 |
| :--- | :--- |
| `char *pw_name` | 用户的登录名 |
| `uid_t pw_uid` | UID 号 |
| `gid_t pw_gid` | GID 号 |
| `char *pw_dir` | 用户的家目录 |
| `char *pw_gecos` | 用户的全名 |
| `char *pw_shell` | 用户的默认 shell |

你可以连续获取连续的条目：

```c
#include <pwd.h>
#include <sys/types.h>
void endpwent(void);
struct passwd *getpwent(void);
void setpwent(void);
```

`getpwent` 返回一个包含单个用户条目的结构。第一次调用它时，它返回第一个条目；第二次调用时，返回第二个条目。所以不需要设置一个变量并每次递增。

`endpwent` 停止这个 C 库函数。`setpwent` 将位置置到起始处。

```c
#include <sys/types.h>
#include <unistd.h>
uid_t geteuid(void);
gid_t getgid(void);
gid_t getegid(void);
int setuid(uid_t uid);
int setgid(gid_t gid);
```

你可以使用 `getgid` 获取用户/程序的组 ID。`setuid` 只能由超级用户或 root 使用，但建议谨慎使用，因为一旦你将进程的用户 ID 改为较小的值，就无法恢复了。这就像一位国王在他的王国里巡游，当他回来时，卫兵不让他进入。因此，通常使用设置有效用户 ID 的 `seteuid`。我会给你们看一个简单的程序，”他说，并展示了一个程序 `passwd.c`。



```c
#include <sys/types.h>
#include <pwd.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main() {
    uid_t userid;
    gid_t groupid;
    struct passwd *password;

    userid = getuid();
    groupid = getgid();

    printf("User is %s\n", getlogin());
    printf("User IDs: User id is %d, Group id is %d\n", userid, groupid);

    password = getpwuid(uid);

    printf(
        "User ID entry shows the following data :\n "
        "Name is %s, User id is %d, Home Directory is %s, "
        "The shell is %s\n",
        password->pw_name,
        password->pw_uid,
        password->pw_gid,
        password->pw_dir,
        password->pw_shell
    );

    exit(0);
}
```

“你明白了吗？这只是对密码结构的简单读取。”Seema 看了几分钟后说她懂了。

```c
#include <sys/utsname.h>

int uname(struct utsname *name);
```

`uname`系统调用将主机信息写入由`name`指向的`utsname`类型结构中。我说的“类型结构”，简单是指包含与相关文件中定义的相同字段的结构。`utsname`结构定义在`utsname.h`中。它必须至少包含这些成员：

| 成员 | 描述 |
| :--- | :--- |
| `char sysname[]` | 操作系统名称 |
| `char nodename[]` | 主机名 |
| `char release[]` | 系统的发布级别 |
| `char version[]` | 系统的版本号 |
| `char machine[]` | 硬件类型 |

```c
#include <unistd.h>

int gethostname(char *name, size_t namelen);
```

此系统调用将主机名写入字符串`name`中。`namelen`是假设的最小长度。

“为什么这很重要？我们通常知道主机的名字。”Lingaraj 回想起了某些事，决定告诉 Seema。Seema 准备好听他的另一个故事。

“当我当软件工程师工作时，我们中一些人去了这家酒店。我们看到一个大厅里在举办派对，决定闯进去。我们当时在另一家公司工作。派对是由一家名为 Some Software Solutions 的公司举办的。他们正在庆祝项目的成功。由于人很多，而且我们穿得正式，没有人怀疑我们来自另一家公司。但我们有一班午夜 12 点的飞机，我们不想错过航班。我们喝醉了，没有意识到时间的流逝。11 点时，我突然意识到我们只有一小时就要赶飞机了。我试图寻找我的朋友，但他们已经消失在人群中。所以我上 DJ 播放音乐的舞台。那里大约有 300 人。我跟 DJ 说话，但由于噪音太大他听不见。于是，我示意他停止音乐。我当时太兴奋了，直接接过了麦克风。”

大家都开始盯着他。然后我意识到，这就是使用`gethostname()`的重要性。让我给你们看这个程序。和密码文件的方法类似，只是获取细节的结构不同。`compdetails.c`

```c
#include <utsname.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    char machine[512];
    struct utsname comp_details;

    gethostname(machine, 511);
    uname(&comp_details);

    printf("The machine host name is %s\n", machine);
    printf(
        "The System is %s on %s hardware\n",
        comp_details.sysname,
        comp_details.machine
    );
    printf(
        "The nodename of the machine is %s\n",
        comp_details.nodename
    );
    printf(
        "The version is %s, %s\n",
        comp_details.release,
        comp_details.version
    );

    exit(0);
}
```

现在，日志。

```c
#include <syslog.h>

void syslog(int priority, const char *message, arguments...);
```

这是一个日志消息。但未来的文明可能会视为历史，并根据你独特的案例重建那个时代的精神。它就像日记，只不过这些消息的去向取决于优先级。优先级选项有这些：

| 优先级 |
| :--- |
| `LOG_EMERG` |
| `LOG_ALERT` |
| `LOG_CRIT` |
| `LOG_ERR` |
| `LOG_WARNING` |
| `LOG_NOTICE` |
| `LOG_INFO` |
| `LOG_DEBUG` |

```c
void openlog(const char *ident, int logopt, int facility);
```

如果你想“自定义”记录消息的方式，可以使用这个 C 库函数。`ident`是你可以加在消息前面的内容，比如“Seema 的活动是：”。`facility`参数记录了一个默认设施值，供未来的`syslog`调用使用。`logopt`参数配置未来`syslog`调行为。

## 资源和限制

Lingaraj 开始说道。

“一个程序，一组系统调用，用于对使用 Vijay 资源的人设置限制，并对他设定你的优先级。你想要那样吗？”

“Vijay 是个成年人，无论机器还是人，他都可以自己决定。但是的，我想学习这些调用。”

Linux 系统中的一些常见限制：

| 限制 |
| :--- |
| `NAME_MAX` |
| `CHAR_BIT` |
| `CHAR_MAX` |
| `INT_MAX` |

因此，为了尝试这些限制，你需要系统调用：

```c
#include <sys/resource.h>

int setpriority(int which, id_t who, int priority);
int getrlimit(int resource, struct rlimit *r_limit);
int setrlimit(int resource, const struct rlimit *r_limit);
int getrusage(int who, struct rusage *r_usage);
int getpriority(int which, id_t who);
```

如你所知，`id_t`是用于用户 ID 和组 ID 的特殊整数类型。`int which`告诉该 ID 是用户 ID 还是进程 ID。`int priority`是优先级值，一个`-20`到`20`之间的整数。默认值为`0`。`rlimit`是一个包含指针的结构体：

```c
struct rlimit {
    rlim_t rlim_cur;
    rlim_t rlim_max;
};
```

软限制（soft limit）你可以将其理解为会产生错误的限制，而硬限制（hard limit）则会导致程序终止。如果 Vijay 参加了很多，我猜你可以用这个来设置一个限制。让他只拥有有限的额度。

硬限制大于软限制。硬限制好比一个人可以喝多少酒。Prabhu 的硬限制是`750`毫升。但他妻子只允许他喝`180`毫升。这就是软限制。实施限制可能还有其他考虑，比如配给。其他人可能需要喝酒。你可以喝，但不敢喝。你可以喝，但非常小心。如果符合你的情况，硬限制和软限制就不重要了。只有超级用户（superuser）可以增加硬限制，就像医生可以增加容量一样。否则，普通用户只能减小软限制。

这些是对应的资源及其描述：

| 资源 |
| :--- |
| `RLIMIT_AS` |
| `RLIMIT_CORE` |
| `RLIMIT_CPU` |
| `RLIMIT_DATA` |
| `RLIMIT_FSIZE` |
| `RLIMIT_NOFILE` |
| `RLIMIT_STACK` |

`rusage`结构包含更多成员，其类型同样为`timeval`。它的成员是：

```c
struct rusage {
    struct timeval utime;
    struct timeval stime;
};
```

```c
int setpriority(int which, id_t who, int priority); // 设置进程的优先级。
int getpriority(int which, id_t who); // 返回优先级值。
int getrlimit(int resource, struct rlimit *r_limit); // 返回某个资源的限制值，如 RLIMIT_CPU 包含硬限制和软限制值。
int setrlimit(int resource, const struct rlimit *r_limit); // 设置软、硬限制的值。
int getrusage(int who, struct rusage *usage); // 提供进程消耗的用户时间和系统时间。
```

`who`选自：

| 选项 |
| :--- |
| `RUSAGE_SELF` |
| `RUSAGE_CHILD` |

### 数据管理

Lingaraj 说话了。让我们谈谈 Linux 是如何管理内存。虚拟内存是一种抽象。这意味着它被组织并使其看起来非常有规律且易于访问。

```c
#include <stdlib.h>

void *malloc(size_t size);
```

`size_t size`的类型是`unsigned long`。想象你城市里有一个仓库。Linux 中的内存就像那个仓库。假设我想存储`50`公斤檀香，我在仓库里预订了`10`英尺乘以`10`英尺的空间。仓库管理员（我们叫他 Varadaraj 吧）会把它存放在仓库里并给我收据。

`image_rsrc852.jpg`

现在，我有`10`英尺乘以`10`英尺的空间存放檀香。我通常不会问他仓库内部物理空间的位置。如果我问，我可以查到，但并不一定要这样做。所以，这`10`英尺乘以`10`英尺就是你通过`malloc()`分到的内存数量。

我不能在仓库的某个房间里放大象粪，然后问 Varadaraj 隔壁放了什么。他会立即把我从系统中移除。我连大象粪都拿不回来。我不能写一个程序去查询程序不关心的其他内存地址。同样，我不能请求`10`英尺乘以`10`英尺的空间，却要一个长`12`英尺的木鹿雕塑。所以我不能写一个尝试写入超出其分配的独立地址空间的程序。

如果仓库很小，比如是一个初创公司，没有足够的空间处理额外订单，仓库管理员 Varadaraj 会把额外的物品带回家里存放。但当然，他不会告诉我。如果他对我的订单这么做了，当我要求提取时，我能发现送货需要更长时间。对硬盘驱动的使用被称为交换空间（swap space）。

如果他觉得某个物品一段时间不会被使用，他也会把物品移到家里。如果我去仓库向他要，他会再次从后面把它搬回仓库，给我一种它直一直在仓库里的印象。

调用`malloc`让`malloc`库能够管理内存。

```c
#include <stdlib.h>

void free(void *ptr);
```

这就像告诉仓库你已经用完了该空间，不再需要了。当然，在使用`free`之后，你不能再尝试访问该空间。

```c
#include <stdlib.h>

void *calloc(size_t number_of_elements, size_t element_size);
```

`calloc`分配空间。`number_of_elements`和`element_size`的类型都是`size_t`。

```c
void *realloc(void *ptr, size_t size);
```

`realloc`修改之前分配内存的大小。它返回指向更新内存的指针。

这应该很直观。我们来看看分配到底。Lingaraj 展示了一个程序。

`memory_less.c`

Lingaraj 展示了程序：

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

int main() {
    char *some_memory;
    int exit_code;

    some_memory = (char *)malloc(5);

    if (some_memory != NULL) {
        sprintf(some_memory, "Will this be printed?\n");
        printf("%s", some_memory);
        exit_code = EXIT_SUCCESS;
    }

    exit(exit_code);
}
```

输出不多，但它说明了由于我们只分配了`5`字节，它无法处理这个超过`20`字节的长字符串。所以，我们这次修改了程序，分配了`30`字节。

```text
malloc(): corrupted top size
Aborted (core dumped)
```

当程序结束或文件描述符关闭时，所有的锁都会清除。

在文件锁定过程中，不要使用`fread`或`fwrite`。请使用`read`和`write`。这是因为`fread`或`fwrite`是带缓冲的，也就是说缓冲区中会有更多的待读或待写字节。”

这样一个 C 库函数：

```c
#include <unistd.h>

int lockf(int fildes, int function, off_t size_to_lock);
```

`function`的选项有：

- `F_ULOCK`
- `F_LOCK`
- `F_TLOCK`
- `F_TEST`

这些锁在本质上是建议性的，也就是说程序必须要有礼貌地检查锁并尊重锁。

我将向你展示两个程序：一个锁定数据文件的某个区域（在某些字节之间），另一个程序检查它是否可以获取该区域的锁。首先，我们将测试排他性访问。`lock_reg_ex.c`

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>

const char *file_with_regions = "/tmp/test_lock";

int main() {
    int fd;
    int count;
    char *fill_string = "Seema";
    struct flock region;

    // 我们进行了重要的声明，并决定测试文件将填充为“Seema”。
    // 我们声明了一个类型为 `flock` 的结构体 `region`，
    // 它将包含有关锁定、解锁锁或测试的详细信息。

    int res;

    fd = open(file_with_regions, O_RDWR | O_CREAT, 0666);

    if (!fd) {
        fprintf(stderr, "Unable to open %s.\n", file_with_regions);
        exit(EXIT_FAILURE);
    }

    // 因为之前提到的原因，我们明智地使用了 `open` 而不是 `fopen`。

    for (count = 0; count < 100; count++) {
        (void)write(fd, fill_string, 1);
    }

    // 我们只是用“Seema”这个单词填充它。

    region.l_type = F_WRLCK;
    region.l_whence = SEEK_SET;
    region.l_start = 40;
    region.l_len = 10;

    // 我们使用 `F_WRLCK`，它是写锁或排他锁。

    printf("Process %d locking file\n", getpid());

    res = fcntl(fd, F_SETLK, &region);

    // 我们对打开的文件使用文件描述符 `fd` 调用 `fcntl`，
    // 使用 `SETLK` 创建锁并指定 `region` 结构体。

    if (res == -1) {
        fprintf(stderr, "Failed to lock region.\n");
    }

    sleep(20);

    printf("Process %d closing file\n", getpid());

    close(fd);
    exit(EXIT_SUCCESS);
}
```

显然，我们可以通过编写一个访问相同文件的程序来测试它，并继续使用`fcntl`查询是否存在锁，以及是否可以获取新锁。

`lock_reg_ex_test.c`



```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>
const char *file_with_regions = "/tmp/test_lock";
#define SIZE_INCREMENT 5
int main() {
    int fd;
    int res;
    struct flock region_of_interest;
    int start_byte;
    fd = open(file_with_regions, O_RDWR | O_CREAT, 0666);
    if (!fd) {
        fprintf(stderr, "Unable to open %s for read/write", file_with_regions);
        exit(EXIT_FAILURE);
    }
    for (start_byte = 0; start_byte < 99; start_byte += SIZE_INCREMENT) {
        region_of_interest.l_type = F_WRLCK;
        region_of_interest.l_whence = SEEK_SET;
        region_of_interest.l_start = start_byte;
        region_of_interest.l_len = SIZE_INCREMENT;
        region_of_interest.l_pid = -1;
        // 在测试之前，我们填充了结构体。我们每次递增 5 个字节。
        printf("Testing for exclusive lock on region from %d to %d\n", start_byte, start_byte + SIZE_INCREMENT);
        res = fcntl(fd, F_GETLK, &region_of_interest);
        if (res == -1) {
            fprintf(stderr, "F_GETLK failed!");
            exit(EXIT_FAILURE);
        }
        if (region_of_interest.l_pid != -1) {
            printf("No opportunity to lock exists by the process : %d\n", getpid());
            printf("Because of a lock by another process.");
            printf("The details including the process number of the locking process are:\n");
            printf("l_type %d, ", region_of_interest.l_type);
            printf("l_whence %d, ", region_of_interest.l_whence);
            printf("l_start %d, ", (int)region_of_interest.l_start);
            printf("l_len %d, ", (int)region_of_interest.l_len);
            printf("l_pid %d\n", region_of_interest.l_pid);
        } else {
            printf("F_WRLCK - Opportunity to lock exists by this process with pid, %d\n", getpid());
        }
    }
    close(fd);
    exit(EXIT_SUCCESS);
}
```

我们在后台运行`lock_reg_ex.c`：

`./lock_reg_ex.c &`

在另一个终端中运行：

`./lock_reg_ex_test.c`

第一个终端的输出是：

`Process 34974 locking file`

`Process 34974 closing file`

第二个终端的输出是：

`Testing for exclusive lock on region from 0 to 5`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 5 to 10`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 10 to 15`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 15 to 20`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 20 to 25`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 25 to 30`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 30 to 35`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 35 to 40`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 40 to 45`

`No opportunity to lock exists by the process : 34980`

`Because of a lock by another process.`

`The details including the process number of the locking process are:`

`l_type 1, l_whence 0, l_start 40, l_len 10, l_pid 34974`

`Testing for exclusive lock on region from 45 to 50`

`No opportunity to lock exists by the process : 34980`

`Because of a lock by another process.`

`The details including the process number of the locking process are:`

`l_type 1, l_whence 0, l_start 40, l_len 10, l_pid 34974`

`Testing for exclusive lock on region from 50 to 55`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 55 to 60`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 60 to 65`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 65 to 70`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 70 to 75`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 75 to 80`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 80 to 85`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 85 to 90`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 90 to 95`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

`Testing for exclusive lock on region from 95 to 100`

`F_WRLCK - Opportunity to lock exists by this process with pid, 34980`

## 数据库

Lingaraj 开始说道：

“让我们聊聊数据库吧。你们知道，数据库是用来存储数据的。鹦鹉 Paresh 是一个后来变成强匪的人。他从人们那里偷了许多财物，并训练了鹦鹉来维护数据库。他也偷了我的财物。Paresh 只需要说出被劫者的名字，鹦鹉就会告诉详细信息，从人的名字开始，财物是什么以及隐藏在哪里。”

![](img/image_rsrc854.jpg)

检查员把 Ravi 的名字告诉鹦鹉。鹦鹉开始吐出详细信息。

‘Name : Ravi.

贵物品：2 颗钻石，4 条金项链，6 条珍珠项链，20 万卢比现金。

“藏在 Sohi 山顶的橡树树下，”鹦鹉说。

然后警察员把我的名字告诉了鹦鹉。

“名字：Lingaraj。

贵物品：关于如何改善世界的电影剧本和诗歌。

丢在他房子外的侧水沟里。”

所以，鹦鹉有一个数据库，可以通过名称（键）进行请求。

当你创建一个数据库时，会创建两个文件，一个扩展名为`.dir`，另一个扩展名为`.pag`。它们构成了由单一`dbm`指针标识的对。你只能通过`dbm`例程来修改它们。

### 主要函数

主要函数有这些：

```c
#include <ndbm.h>
DBM *dbm_open(const char *filename, int file_open_flags, mode_t file_mode);
```

- `filename` 是你给数据库的没有扩展名的名称。
- `file_open_flags` 与`O_CREAT`进行“或”位运算。
- `mode` 用于设置权限。
- 它返回一个数据库描述符。

```c
int dbm_store(DBM *database_descriptor, datum key, datum content, int store_mode);
```

- `datum` 是一种数据类型，至少包含 2 个成员：
  - `void *dptr;`
  - `size_t dsize`
- `dsize` 指定数据的大小，`dptr` 指向存储的数据。
- `datum key` 是我们在鹦鹉故事中提到过的键，一个标识符。
- `datum content` 是实际内容。
- `store_mode`：当你尝试使用已存在的键存储某些数据时，会发生什么。如果设置为`dbm_insert`，则值不会被存储。但是，如果设置为`dbm_replace`，则值会被替换。

```c
datum dbm_fetch(DBM *database_descriptor, datum key);
```

“这根据键取取数据，”Seema 说。Lingaraj 继续说道。

```c
void dbm_close(DBM *database_descriptor);
```

“关闭数据库并移除进程对指定数据库的访问。”

```c
int dbm_delete(DBM *database_descriptor, datum key);
```

它删除数据库中的某特定记录。

```c
int dbm_error(DBM *database_descriptor);
```

这检查数据库中的错误。

```c
int dbm_clearerr(DBM *database_descriptor);
```

这清除任何错误状态标志位。

```c
datum dbm_firstkey(DBM *database_descriptor);
datum dbm_nextkey(DBM *database_descriptor);
```

这用于按顺序访问记录。关于数据库的部分就这些。

## 进程

“我们去散散步吧，”Lingaraj 说。

他们去散了步去了一个椰子林。Seema 对这个地方感到惊为观止，那里有很多高树。树上有一些蜂巢，Lingaraj 告诉 Seema，他带她来这里是为了谈论蜜蜂。

![](img/image_rsrc855.jpg)

“蜜蜂总是在忙碌。蜂王准许许多蜜蜂的请求。但只有一只蜂王。请求可能是‘我得到了这些花蜜，我该把它放在哪儿？’

而蜂王的回答是：

‘花蜜？绝对不要在路上。’”

Seema 没有笑，Lingaraj 指出 nectar（花蜜）是道路建设中使用的 tar（焦油）一词的双关语。Seema 还是没有笑。Lingaraj 就放过了。

“所以每个工蜂与蜂王的每次听见都是一个时间片。蜂王往往有注意力缺陷症。她通过给一只工蜂大约 5 分钟的时间，要求他等待并移动到下一只蜜，那只蜜可能会询问如何对熊。她可能会说：

‘请忍耐（bear with it）。’

当然，蜂王的听众中会有更多的蜂。

![](img/image_rsrc856.jpg)

这给人一种她在同时处理所有人的印象。但事实并非。要理解的一点是，所有的蜜蜂都执行所有的任务，但在不同的时间片轮中进行。所以，当蜂王正在处理一个想做饭的厨蜂的请求时，她和所有其他蜜蜂都在积极处理这项工作。然后他们暂停该工作，转到下一个任务，可能是由于人类唱了一首反复重复的歌曲而去刺他。他们包围他，当这个人在震惊中准备挨刺时，他们停下来并回来。然后，他们承担巢内部的清洁工作。然后他们重复所有工作，从他们暂停的地方继续。告诉他们他们在何处的——例如，他们包围人类时所在的位置——是该进程的程序计数器。

在 Linux 中，处理器一次处理一个任务，以时间片的形式进行，但它们都发生得非常快，给人一种它正在同时做这一切的印象。

“所以，蜂王就像内核。当蜂王要求采取后续行动时，工蜂的请求就可以转换为一个操作，”Seema 说。

“或者你可以把一切都看作一个进程。每个进程都有一个`PID`，一个进程标识符。有一个进程的`PID`为 1。它被称为‘init’。它被称为所有进程的父进程。

当程序存储在内存中，没有程序可以修改代码。它是只读的。其他程序可以共享它，”Lingaraj 说。

“当蜂王下命令并放在告示板上，没有人能改变它。它们可以共享它，”Seema 说。

Lingaraj 笑了。“我们也有共享库。库是现成的代码。就像薯片。你不需要烹饪它们，而是采购现成的。蜂王告诉蜜蜂去烹饪。”

制作配料的方法（对于两者）都在共享库中，命令引用它。制作配料的指令没有针对每道菜指定。也就是说，它在内存中。

当然变量不能共享。例如，如果 Idly 的配料是辣椒粉，而 Dosei 的配料是香菜，你不能只有一个配料项。在两种情况下都需要两个实例。

进程拥有：

- 它自己的栈空间。
- 它自己的环境空间。
- 它自己的程序计数器。

执行`ps -ef`命令查看更多信息。在这里你可以看到：

- 进程的用户 ID
- `PID`
- 父 PID
- 进程调度信息
- 开始时间
- 终端
- 持续时间
- 启动进程的命令

与之相似，`system`调用就像一个代理人，通过让别人来完成工作。假设我有一个家庭管家。我请他为派对叫一个厨师，当我在办公室时，他在家里做饭。管家会收取佣金，并让厨师执行这项任务。水管维修、开车以及排队付账单也是同样的。

但如果你有一个全能的人才，他既会做饭，又会开车，还会付账单，那将会非常有帮助。

它们有很多类型。有些只接受一个参数。有些接受参数数组，还有的要求你提供路径。



```c
#include <unistd.h>
char **environ;
int execl(const char *path, const char *arg0, ..., (char *)0);
```

`path` 显然是命令可执行文件存储的位置。

`arg0`、`arg1` 等是所调用程序的参数。如果你自己写了一个程序，这些参数就是该程序中 `main` 函数的参数。`(char *) 0` 告诉 `execl` C 库函数，参数列表结束了。

现在，`execl` 类的 C 库函数，你可以把它们想象成“全能阿伦”（Mr All round Arun）。

“全能阿伦是我请过的一个管家。他无所不知。他是个好司机、好厨师、电影导演、火箭科学家和水管工。每当我要求他做某项工作时，他就会戴上那顶特定的帽子。我的工作变成了他的工作，他执行得非常好。”

“你的意思是没有启动新进程吗？就像是你自己在做一样？”Seema 问。

“没错。当 `exec` 类的函数启动一个新进程时，它使用调用进程的进程 ID（PID）。记得 Shell 脚本中的执行吗？我祖父去世时想让我父亲接手配方工作。这很像，但它是 C 库函数的形式。它们调用的是可执行文件，”Lingaraj 说。他继续道：

“阿伦从不向我收钱，因为他很有钱。”

“后来发生了什么？他去世了吗？”

“不，我解雇了他。”

“为什么？”

“有一天他戴上了我的帽子，开始认为自己就是我。他指使我，我为他工作，直到我有机会把他的帽子摘下来。”

被调用的进程实际上会消除调用进程。调用进程消失了。

```c
int execlp(const char *file, const char *arg0, ..., (char *)0);
```

在这里，`path` 被替换为 `file`。这意味着命令将自动在 `PATH` 变量中查找文件。如果文件不在路径中，你必须指定完整路径名。

```c
int execle(const char *path, const char *arg0, ..., (char *)0, char *constenvp[]);
```

在这里，`e` 象征“额外的”（extra）。通常指新进程应该运行的环境。如果没有定义，则使用当前进程的环境。

```c
int execv(const char *path, char *const argv[]);
```

在这里，该函数接受一个参数数组。

```c
int execvp(const char *file, char *const argv[]);
```

它将 `PATH` 中的文件名或完整路径，以及一个数组作为参数传递。

```c
int execve(const char *path, char *const argv[], char *const envp[]);
```

同样，将 `PATH` 中的文件名或完整路径，以及数组同环境作为参数传递。

所以，如果函数名中包含 `p`，它会在路径中搜索；`e` 意味着额外的（环境）；而 `v` 意味着数组。

```c
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);
```

如果你想让 Vijay 在赞美你亲戚的同时启动另一个进程……”

“我会使用 `Ctrl+C` 和 `Ctrl+V`，复制粘贴。”

“`Ctrl+C` 是一个停止前台进程的信号。所以，如果你对 Vijay 使用 `Ctrl+C`，你将立即停止他正在赞美你亲戚的前台进程。”

`fork` 就像是进程的复制粘贴，但它为生成的每个进程分配了不同的 `PID`。

你为什么需要 `fork`？为了创建一个子进程。

无论如何，`fork` 会将子进程的 `PID` 返回给父进程。对于子进程，它返回 `0`。在失败的情况下，它向父进程返回 `-1`。这在编程语文中非常重要。它给了我们一种方法来判断程序是在父进程还是子进程中。因此类型为 `pid_t`。所以，当你 `fork` 时，你创建了进程的另一个实例，即子进程。如果失败，它返回 `-1`。可能失败的原因有：

- 子进程过多，限制由 `CHILD_MAX` 指定。当你看到 `errno` 时，它将是 `EAGAIN`。
- 如果进程表中没有空间或没有内存，`errno` 被设置为 `ENOMEM`。

```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *stat_loc);
```

让我再次提一下。在程序执行过程中，如何发现你是在子进程还是父进程中？通过返回值。在子进程中是零，在父进程中是子进程的 `pid`。

父进程（创建子进程的进程）可以使用 `wait()` 查询状态，判断它是运行还是停止。状态存储在 `stat_loc` 中。列表如下：

- `WEXITED`
- `WSTATUS`
- `WSIGNALED`
- `WTERMSIG`
- `WSTOPPED`

```c
#include <sys/types.h>
#include <wait.h>
pid_t waitpid(pid_t pid, int *stat_loc, int options);
```

`pid` 是子进程的进程 ID。现在，`options`：

- 与 `wait()` 相同，但 `WNHANG` 不阻塞调用者。如果子进程仍在运行，它返回 `0`。
- 如果调用被中断或参数无效，它返回 `-1`。

另一个需要知道的重要是：如果进程打开了文件描述符，当调用 `exec` 类函数时，这些描述符会被保留。当进程终止时，该项会留在进程表中，直到父进程终止（此时父进程变为 `init`）。让我们来看一个程序：`maker.c`。

```c
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    pid_t pid;
    char *message;
    int exit_code;
    printf("Fork starting\n");
    pid = fork();
    switch(pid)
    {
        case -1:
            exit(1);
        case 0:
            printf("This is the child\n");
            printf("With PID : %d\n", getpid());
            exit(EXIT_SUCCESS);
            break;
        default:
            printf("\n\nThis is the parent\n");
            printf("With PID : %d\n", getpid());
            sleep(30);
            break;
    }
    exit(EXIT_SUCCESS);
}
```

上面的程序通过 `fork` 创建了一个子进程。我们可以识别（当程序运行时）进程是在父进程还是子进程中。如果进程 ID 为 `0`，意味着它是子进程。它立即结束了。父进程允许继续运行 30 秒。然后程序退出。我为什么要这么做？为了给你们展示僵尸进程。如果子进程在父进程之前终止且父进程没有调用 `wait()`，则子进程被称为僵尸进程。

正如你们所知，`wait` 将子进程的状态返回给父进程。当我们运行这个程序时，会得到以下输出：

```text
This is the parent
With PID : 35916
This is the child
With PID : 35917
```

在另一个终端，如果你输入：

```bash
$ ps -al
```

在其他进程中，你会发现一个项：

```text
1 Z  1000  35917  35916  0  80  0 -       0 -       pts/0   00:00:00
```

注意这个代表僵尸进程的“Z”，以及进程号 `35917`。当然，你也会看到 `35916`，但那是 `ppid`，即父进程 ID。在父进程结束之前，它会将此进程显示为僵尸进程。

我们使用 `wait` 来修复这个问题。

`zwait.c`

```c
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main(){
    pid_t pid;
    char *message;
    int exit_code;
    printf("Fork program starting\n");
    pid = fork();
    switch(pid)
    {
    case -1:
        exit(1);
    case 0:
        printf("This is the child\n");
        printf("With PID : %d\n", getpid());
        exit(24); /* 在这里，我们给出一个退出码，以查看它是否能在父进程中获取到。 */
        break;
    default:
        printf("\n\nThis is the parent\n");
        printf("With PID : %d\n", getpid()); /* 从这里开始，添加了行 */
        int stat_val;
        pid_t child_pid;
        child_pid = wait(&stat_val); /* 调用了 wait，它返回子进程的 pid 并释放资源。子进程之所以显示为僵尸是因为它的资源没有被释放。 */
        printf("Child has finished: PID = %d\n", child_pid);
        if(WIFEXITED(stat_val))
            printf("Child exited with code %d\n", WEXITSTATUS(stat_val)); /* 在这里，我们使用 WIFEXITED 查看子进程是否正常终止，如果是，我们就继续使用 WEXITSTATUS(stat_val) 显示子进程是以什么代码退出的。 */
        else
            printf("Child terminated abnormally\n");
        sleep(30);
        break;
    }
    exit(EXIT_SUCCESS);
}
```

当我们运行它时：

```text
This is the parent
With PID : 36960
This is the child
With PID : 36961
Child has finished: PID = 36961
Child exited with code 23
```

所以，子进程 ID 和退出码被父进程获取了。

而且如果我们用 `ps -al` 检查，尽管父进程又运行了 30 秒，但并没有关于僵尸进程的记录。

一个好的 Shell 命令是 `pstree -p`，通过它可以看到带有进程 ID 的进程树。我建议你在运行上述程序时自己尝试一下，看看是哪个进程产生了哪个进程。

# 信号（Signals）

Lingaraj 开始说道。

“在一个商场发生过这样一起事。我正试着给女朋友挑礼物，这时我注意到一个年轻女性正试图为耳朵挑选耳饰。她一直在尝试各种耳饰，我们都能在镜子眼里看到彼此。我针对她尝试的东西向她发出信号。当她试戴一对耳环时，我向她比了一个大拇指反对的手势。”

![](img/image_rsrc857.jpg)

她拒绝了。接下来的两次尝试也发生了同样，然后她问我为什么。我让她等一下，去上了手语课程然后回来。她还在那里试着合适的款式。于是我开始向她发手势。

“你发了什么信号？”Seema 问。

这里有一组信号信息：

- 耳环这个想法本身就错了。
- 你决定得太久了。
- 请停止打电话并尝试其他东西。
- 有人挡住了镜子里的视线。
- 在不记得的情况下重复穿戴同样的东西。
- 向镜子扔大大石头把它砸碎，因为你已经站在那里了很久，而她又决结不定。

“然后发生了什么？”Seema 问。

“她挑选了大约 8 处耳环、12 条项链和 7 枚鼻钉。然后迅速消失了。我本也会这么做的，但她告诉店员我是她的丈夫。店员相信了，因为挑选是我做的。由于我当时赖她生活，我不得不用女朋友的信用卡买单。我一直和女朋友在一起，直到信用卡账单寄到。我正在吃她做的‘洋葱饼（onion dosei）’，我不得不从饼面前抽出身来。她以前做的洋葱饼总是非常好吃。”

Seema 看到 Lingaraj 喉结哽了一下，她不确定 Lingaraj 是对那个女人还是对那些洋葱饼产生了感情。

Lingaraj 缓过来继续说道。

“我告诉过你们关于 `Ctrl+C`。在 Linux 上，它发送的是 `SIGINT`。如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉它。”

这里是一些信号的列表：

- `SIGABORT`
- `SIGALRM`
- `SIGFPE`
- `SIGHUP`
- `SIGILL`
- `SIGINT`
- `SIGKILL`

```text
kill [options] <pid> [...]
```

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉它。”

这里是一些信号的列表：

- `SIGABORT`
- `SIGALRM`
- `SIGFPE`
- `SIGHUP`
- `SIGILL`
- `SIGINT`
- `SIGKILL`

```text
kill [options] <pid> [...]
```

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉到它。”

这里是一些信号的列表：

- `SIGABORT`
- `SIGALRM`
- `SIGFPE`
- `SIGHUP`
- `SIGILL`
- `SIGINT`
- `SIGKILL`

```text
kill [options] <pid> [...]
```

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉到它。”

这里是一是一些信号的列表：

- `SIGABORT`
- `SIGALRM`
- `SIGFPE`
- `SIGHUP`
- `SIGILL`
- `SIGINT`
- `SIGKILL`

```text
kill [options] <pid> [...]
```

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉到它。”

这里是一是一些信号的列表：

- `SIGABORT`
- `SIGALRM`
- `SIGFPE`
- `SIGHUP`
- `SIGILL`
- `SIGINT`
- `SIGKILL`

```text
kill [options] <pid> [...]
```

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

注意这个代表僵尸进程的“Z”，以及进程号 `35917`。当然，你也会看到 `35916`，但那是 `ppid`，即父进程 ID。在父进程结束之前，它会将此进程显示为僵尸。

我们使用 `wait` 来修复这个问题。

`zwait.c`



```c
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
int main(){
    pid_t pid;
    char *message;
    int exit_code;
    printf("Fork program starting\n");
    pid = fork();
    switch(pid)
    {
    case -1:
        exit(1);
    case 0:
        printf("This is the child\n");
        printf("With PID : %d\n", getpid());
        exit(24);/*在这里，我们给出一个退出码，以查看它是否能在父进程中获取到。 */
        break;
        default:
        printf("\n\nThis is the parent\n");
        printf("With PID : %d\n", getpid());/*  从这里开始，添加了行 */
        int stat_val;
        pid_t child_pid;
        child_pid = wait(&stat_val);/*调用了 wait，它返回子进程的 pid 并释放资源。子进程之所以显示为僵尸是因为它的资源没有被释放.*/
        printf("Child has finished: PID = %d\n", child_pid);
        if(WIFEXITED(stat_val))
            printf("Child exited with code %d\n", WEXITSTATUS(stat_val));在这里，我们使用 WIFEXITED 查看子进程是否正常终止，如果是，我们就继续使用 WEXITSTATUS(stat_val) 显示子进程是以什么代码退出的。
        else
            printf("Child terminated abnormally\n");
        sleep(30);
        break;
    }
    exit(EXIT_SUCCESS);
}
```

当我们运行它时：

```
This is the parentWith PID : 36960This is the childWith PID : 36961Child has finished: PID = 36961Child exited with code 23
```

所以，子进程 ID 和退出码被父进程获取了。

而且如果我们用 `ps -al` 检查，尽管父进程又运行了 30 秒，但并没有关于僵尸进程的记录。

一个好的 Shell 命令是 `pstree -p`，通过它可以看到带有进程 ID 的进程树。我建议你在运行上述程序时自己尝试一下，看看是哪个进程产生了哪个进程。

# 信号 (Signals)

Lingaraj 开始说道。

“在在一个商场发生过这样一起事。我正试着给女朋友挑礼物，这时我注意到一个年轻女性正试图为耳朵挑选耳饰。她一直在尝试各种耳饰，我们都能在镜子眼里看到彼此。我针对她尝试的东西向她发出信号。当她试戴一对耳环时，我向她比了一个大拇指反对的手势。”

![](img/image_rsrc857.jpg)

她拒绝了。接下来的两次尝试也发生了同样，然后她问我为什么。我让她等一下，去上了手语课程然后回来。她还在那里试着合适的款式。于是我开始向她发手势。

“你发了什么信号？”Seema 问。

这里有一组信号信息：

- 耳环这个想法本身就错了。

- 你决定得太久了。

- 请停止打电话并尝试其他东西。

- 有人挡住了镜子里的视线。

- 在不记得的情况下重复穿戴同样的东西。

- 向镜子扔大石头把它砸碎，因为你已经站在那里了很久，而她又决不定。

“然后发生了什么？”Seema 问。

“她挑选了大约 8 处耳环、12 条项链和 7 枚鼻钉。然后迅速消失了。我本也会这么做的，但她告诉店员我是她的丈夫。店员相信了，因为挑选是我做的。由于我当时赖她生活，我不得不用女朋友的信用卡买单。我一直和女朋友在一起，直到信用卡账单寄到。我正在吃她做的‘洋葱饼 (onion dosei)’，我不得不从饼面前抽出身。她以前做的洋葱饼总是非常好吃。”

Seema 看到 Lingaraj 喉结哽了一下，她不确定 Lingaraj 是对那个女人还是对那些洋葱饼产生了感情。

Lingaraj 缓过来继续说道。

“我告诉过你们关于 `Ctrl+C`。在 Linux 上，它发送的是 `SIGINT`。如果 Vijay 的行为变得无常，你可以用 `Ctrl+C` 停止它。除非 Vijay 能捕捉它。”

这里是一些信号的列表：

| `SIGABORT` |

| `SIGALRM` |

| `SIGFPE` |

| `SIGHUP` |

| `SIGILL` |

| `SIGINT` |

| `SIGKILL` |

| `kill [options] <pid> [...]` |

你能猜到 `kill` 命令能对一个进程做什么吗？

“它杀掉它。”Seema 说。

“它向进程发送一个信号来杀死它。而 `kill` 命令可以发送一个信号，甚至在进程处于运行状态时告诉它继续。除非 Vijay 能捕捉到它。”

## 要阻塞的信号

我们在这里讨论的是这一点：当一个信号发生时，处理函数会被调用并运行到结束。如果在此时间内出现了另一个信号，这个健壮的系统调用 `sigaction` 就可以阻塞这个新信号。

`int sa_flags`

## 信号动作修饰

它告诉我们是否要返回位置以捕获新信号。当你将其设置为 `SA_RESETHAND` 时，`sigaction` 系统调用将处理一次信号。

手册页（man pages）中还有其他可用的标志。

`oact` 是一个位置，将保存之前之前的信号动作。

```c
#include <signal.h>
int sigaddset(sigset_t *set, int signo);
int sigemptyset(sigset_t *set);
int sigfillset(sigset_t *set);
int sigdelset(sigset_t *set, int signo);
```

这些是 C 库函数。你可以让程序专门处理一个信号，或者制定一个通用的策略来处理信号。因此，你可以创建一个所有这些信号的集合并指定做什么。此外，可能会出现这样的情况：你的程序正在处理一个接收到的信号，而另一个信号又来了。这时你可能需要暂停该函数并杀死进程。无需困惑，你可以使用信号集来处理所有这些信号。

信号集的类型为

`sigset_t`

因此，你可以通过 `sigfillset()` C 库函数用所有可用信号填充你的信号集。同样，你可以使用 `sigemptyset()` C 库函数清空所有信号集合。

你可以通过 `sigaddset()` 指定信号编号将单个信号添加到集合中。

你可以通过 `sigdelset()` 指定信号编号从集合中删除单个信号。

此外，你可以通过查询确定某个信号是否是集合的成员。

```c
int sigismember( const sigset_t *set, int signum)
```

如果信号是集合的成员，则返回 1；否则返回 0；出错时返回 -1。

```c
#include <signal.h>
int sigprocmask(int how, const sigset_t *set, sigset_t *oset);
```

上述系统调用用于更改进程的信号掩码。如果信号被进程阻塞，它将不会被递送，而是保持挂起状态。程序可以通过调用 C 库函数 `sigpending` 来确定哪些被阻塞的信号是挂起的。

```c
#include <signal.h>
int sigpending(sigset_t *set);
```

该系统调用将一组信号写入由 `set` 指向的信号集中，这些信号是被阻塞递送的。如果成功则返回 0，否则返回 -1 并设置 `errno` 以指示错误。

```c
#include <signal.h>
int sigsuspend(const sigset_t *sigmask);
```

`sigsuspend` 系统调用将进程信号掩码替换为 `sigmask` 提供的信号集，然后挂执行。它将在信号处理函数执行后恢复。

## 示例：ayyo.c

让我们来看一个使用 `sigaction` 的程序。

`ayyo.c`

```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void ctrlc(int sig){
    printf("我建议你不要停止我，%s\n", getlogin());
}

void shutdown_req(int sig){
    printf("我是进程 %d，我知道是谁在尝试杀掉我。是你，%s\n", getpid(), getlogin());
}

/*
void finish(int sig){
    printf("这个函数非常没用，因为它试图处理 SIGKILL 信号。");
}
*/

/*
我们声明了上述三个函数，每个对应一个特定的信号：`SIGINT`、`SIGTERM` 和 `SIGKILL`。处理 `SIGINT` 的函数 `ayyo` 在按下 Ctrl+C 后只运行一次，因为我们使用了 `SA_RESETHAND` 标志。我们打印相关消息，这就是该函数做的所有。
*/

int main(){
    struct sigaction act;
    act.sa_handler = ctrlc;
    sigemptyset(&act.sa_mask);
    act.sa_flags = SA_RESETHAND;
    sigaction(SIGINT, &act, 0);

    act.sa_handler = shutdown_req;
    sigemptyset(&act.sa_mask);
    act.sa_flags = 0;
    sigaction(SIGTERM, &act, 0);

    /*
    这与此无关，因为 SIGKILL 会立即杀死进程且无法被处理。
    act.sa_handler = finish;
    sigemptyset(&act.sa_mask);
    act.sa_flags = 0;
    sigaction(SIGKILL, &act, 0);
    */

    /*
    然后指定处理函数并将信号集 sa_mask 置为空。我们不希望任何信号被阻塞。因为你放在此这里的任何内容都不会被递送给进程。指定了是否需要 `SA_RESETHAND`。在第一种情况下，指定了 `SA_RESETHAND`，这意味着信号只会被处理一次，因为信号不会被重置。如果你希望它每次都生效。
    */
    while(1) {
        printf("我很快乐\n");
        sleep(1);
    }
}
```

“所以，我想要更多的控制权。此外，我发现开支很大。我必须共享我的品牌标识、网站等内容。因此，我关闭了特许经营体系，并开始开设分公司。当然，这并不是经营业务的方法。那是我个人的特殊情况。”

“我不知道你为什么要告诉我这些。”

“第一个案例，即我以前在那里建立一个小规模的运营，类似于在程序中调用一个函数。我的进程独立管理了它。

第二个案例是我给出特许经营权，这创建了另一个进程，例如通过调用 `fork`。大量的信息必须被复制。

第三个案例是开设分公司。只共享信息，而不进行复制。这就像执行一个线程。

线程是程序的一部分，会执行多次，但不是作为函数执行。如果你同时处理两个文件，让 `kernel` 使用函数并作为单体块运行将非常繁琐。它可以让代码的另一个实例实例运行，但不会像进程那样对所有内容都进行复制。在线程执行中，正在运行的程序拥有它自己的栈，新的执行线程也拥有自己的栈，因此也有局部变量。但它与创建它的进程共享（请注意不是复制，而是共享）全局变量、文件描述符、信号处理程序和当前目录状态。

所以，特许经营有它自己的财务记账、工资，而分公司共享财务账目。进程是复制，而线程是共享，且复制涉及更多资源。”

“是的，现在说说‘重入’代码。重入函数是指一个可以运行、被中断然后再次运行的函数。

同一个例程可以在不同的实例中重用，一个实例的变量值对其他实例可能无效。所以，如果一个例程改变了变量的值并被再次调用，它不会记住旧的一组值。它会采用调用程序发送的值。

在我们的社区里，饮酒年龄是 21 岁。我朋友的父亲，一位历史老师 Ritesh（他坚持传统就像 sambhar 汤坚持穿衬衫一样），曾是那家酒吧的老板。这没什么问题，除了他从不让我们进入酒吧。他以前会喝醉，当我们出现在酒吧门口时，对话是这样的：

![](img/image_rsrc859.jpg)

‘哦，Lingaraj。你好吗？’他以前这样问。

‘我很好，先生。我的编程表现不错，而且……’

‘我是想问你，你多大了？’

‘25 岁，叔叔。’

‘别骗我。你 20 岁。我记得你告诉过我。’

‘那是 5 年前了，先生。’

‘那又怎样？记录就是记录。出去吧。’

他不符合重入例程的标准。他唯一做的重入就是进入酒吧加水。所以，一个重入函数会为各种实例进行更新。

它基本上意味着，只对调用者提供的数据操作。

```c
#include <pthread.h>
int pthread_create(pthread_t *thread, pthread_attr_t *attr, void*(*start_routine)(void *), void *arg);
```

成功时返回 `0`。

C 库函数 `pthread_create()` 方便例程作为线程运行。它有一个名称，除了函数名外，你可以通过它识别线程。它由 `pthread_t *thread` 提供。类型是 `pthread_t`。

`pthread_attr_t *attr` 是一个属性，我稍后会解释。

`void *(*start_routine)(void *), void *arg` 是将作为线程运行的例程，`arg` 是它的参数。

```c
#include <pthread.h>
void pthread_exit(void *retval);
```

这会退出线程。与函数不同，你不能返回一个变量。因为……？”

“对。”

```c
#include <pthread.h>
int pthread_join(pthread_t th, void **thread_return);
```

这个 C 库函数类似于进程中的 `wait` 系统调用。在这里，`pthread_t th` 代表例程标识符，记得 `pthread_create` 吗？

它返回一个指向线程返回值的指针的指针。

他在他的笔记本电脑上打开了一个文件。

`thread_program.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>
void *print_func(char* message){
   printf("%s - Before sleep\n", message);
   sleep(4);
   printf("%s - After waking up\n", message);
}
int main(){
  pthread_t t1, t2;
  printf("Main program now running\n");
  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");
  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  printf("Back to main after thread join\n");
}
```

然后他继续解释道。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>
void *print_func(char* message){
  printf("%s - Before sleep\n", message);
  sleep(4);
  printf("%s - After waking up\n", message);
}
```

（上面的代码展示了 `print_func` 是如何工作的。

```c
int main(){
  pthread_t t1, t2;
  printf("Main program now running\n");
  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");
  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  printf("Back to main after thread join\n");
}
```

线程通过 `pthread_create` 创建。

```c
struct thread_args {
    char *message;
};
```

为了传递参数给线程，我们使用结构体。



```c
void *print_func(void *arg) {
    struct thread_args *args = (struct thread_args *)arg;
    printf("%s - Before sleep\n", args->message);
    sleep(4);
    printf("%s - After waking up\n", args->message);
    return NULL;
}
```

这是我们向线程传递值。

```c
struct thread_args args1, args2;
args1.message = "First call to pthread";
args2.message = "Second call to pthread";
pthread_create(&t1, NULL, (void *)print_func, (void *)&args1);
pthread_create(&t2, NULL, (void *)print_func, (void *)&args2);
```

输出将会是：

```
Main program now running
First call to pthread - Before sleep
Second call to pthread - Before sleep
First call to pthread - After waking up
Second call to pthread - After waking up
Back to main after thread join
```

然而，因为调度器可能会切换，输出可能是：

```
Main program now running
First call to pthread - Before sleep
Second call to pthread - Before sleep
Second call to pthread - After waking up
First call to pthread - After waking up
Back to main after thread join
```

让我给你说一个场景。当我叔叔是一名医生，在他私立医院的手术室里，他们会把门锁上以防手术正在进行。一旦手术结束，他们就会通过解锁门来打开门。

如果门没锁上，电影剧组就会进去拍摄视频，因为那是唯一一个有大灯的房间。在他们进行期间，他们会把门锁上。工作完成后，剧组通常会解锁门。

让我们来聊互斥线程（mutually exclusive threads）。它们是什么？它们是能够被阻塞的资源。例如，如果你和 `Vijay` 在一起，而他一直被足球赛分散注意力，你该如何阻塞他的资源，让无论是足球赛还是摔跤都无法吸引他的兴趣呢？”

“简单，我会对他使用一个互斥线程程序。”Seema 正在进行研究，而且速度很快。

“简单？祝你好运吧，那不是因为互斥程序很难，而是要把他的注意力从足球中夺回来很难。`mutex` 是 `mutually exclusive` 的缩写，它会锁定代码的临界区域，使得锁定程序在其他人尝试之前先完成操作。记得‘锁锁拉什什曼’（Lock Lakshman）吗？”Lingaraj 展示了一个 C 库函数。

```c
#include <pthread.h>
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t*mutexattr);
```

初始化一个互斥锁 `*mutex`，它基于线程函数。

`const pthread_mutexattr_t *mutexattr` 这需要一些解释。留以后以后说。

```c
int pthread_mutex_lock(pthread_mutex_t *mutex));
```

这锁定了资源。

```c
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

这解锁了资源。

```c
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

这将销毁互斥锁并进行清理。

“让我们进入程序吧。”

“好的。”

“互斥程序。在那之前，是我们讨论过的线程程序。”

`thread_program.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>

void *print_func(char* message){
   printf("%s - Before sleep\n", message);
   sleep(4);
   printf("%s - After waking up\n", message);
}

int main(){
  pthread_t t1, t2;
  printf("Main program now running\n");
  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");
  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  printf("Back to main after thread join\n");
}
```

输出结果为：

```
Main program now running
First call to pthread - Before sleep
Second call to pthread - Before sleep
First call to pthread - After waking up
Second call to pthread - After waking up
Back to main after thread join
```

正如之前解释的那样，并没有同步性。我们使用互斥线程。回到程序，现在加上了互斥锁。

`thread_with_mutex.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;

void *print_func(char* message){
   pthread_mutex_lock(&mutex1);
   printf("%s - Before sleep\n", message);
   sleep(4);
   printf("%s - After waking up\n", message);
   pthread_mutex_unlock(&mutex1);
}

int main(){
  pthread_t t1,t2;
  pthread_mutex_t mutex1;
  pthread_mutex_init(&mutex1, NULL);
  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");
  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  printf("Back to main after thread join\n");
}
```

我将解释这个。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;
```

这初始化了互斥锁 `mutex1`。

```c
void *print_func(char* message){
   pthread_mutex_lock(&mutex1);
```

我们在这里锁定了互斥锁。之后是代码的临界区域。

```c
   printf("%s - Before sleep\n", message);

   sleep(4);

   printf("%s - After waking up\n", message);

   pthread_mutex_unlock(&mutex1);
}
```

在这里我们解锁了互斥锁。

```c
int main(){
  pthread_t t1,t2;
  pthread_mutex_t mutex1;
  pthread_mutex_init(&mutex1, NULL);
  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");
  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  printf("Back to main after thread join\n");
}
```

`sem_open()` 创建一个新的 POSIX 信号量或打开一个已存在的信号量。信号量通过名称标识。它返回信号量的地址。

```c
#include <semaphore.h>

int sem_destroy(sem_t * sem);
```

该函数正如其名所示会销毁信号量。它还会清理资源。

回到灯光开关并并行的类比。一个挑剔的电影星在等待时，如果他在外面而医生们在里面，他会一直要求导演检查灯的状态。这种行为是不被鼓励的，无论是不是电影星，该演员都会被踢出剧组。当灯熄灭时，团队会知道的。因为程序一直在关注这一点。就像那些一直在寻找折扣或免费优惠券的人一样。

所以，在编写程序时，你可以使用 `pthread` 启动一个线程。它将一直运行。你创建一个信号量，并告诉内核当信号量值为 `0` 时会发生什么。这会启动一个例程。你可以告诉当信号量有值时会发生什么。但你不需要告诉程序不断查找该变量并检查它是否变为 `0` 或为正数。这是系统的工作。让我们修改程序并命名为 `thread_sem_program.c`，这次使用信号量。确保包含 `semaphore.h`。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#include <unistd.h>
#include <semaphore.h>

sem_t semap1;

void *print_func(char* message){
    sem_wait(&semap1);
    printf("%s - Before sleep\n", message);
    sleep(4);
    printf("%s - After waking up\n", message);
    sem_post(&semap1);
}

int main(){
  sem_init(&semap1,0,1);
  pthread_t t1, t2;
  printf("I am in main\n");
  int iret1 = pthread_create(&t1, NULL,(void *) print_func, (void *) "First Instance");
  int iret2 = pthread_create(&t2, NULL, (void *) print_func, (void *) "Second Instance");
  pthread_join(t1, NULL);
  pthread_join(t2, NULL);
  sem_destroy(&semap1);
  printf("Back to main after thread join\n");
}
```

我将这样运行它：

```bash
cc -D_REENTRANT thread_sem_program.c -lpthread -lrt
```

输出再次如下：

```
Main now running
First Instance - Before sleep
First Instance - After waking up
Second Instance - Before sleep
Second Instance - After waking up
Back to main after thread join
```

“Vijay 现在怎么样了？”

“他不记得我们相处时的一些事了。”

“你说的那个键盘，他会把它交给任何每一个人来让自己被编程吗？”

“你让我很焦虑。”

“那你最好学快点。”

“谢谢理解。我需要休息几天。我需要见 Vijay。”

“好的。”

Seema 叫了同一辆出租车司机前往班加罗尔。几天后她回来了，走进了 Lingaraj 的家。

“你的旅程得怎么样？”Lingaraj 问道。

“见到他很好，他变得更好了。但我觉得他变得很守秘。你做了什么？”她向 Lingaraj 问。

“我站在悬崖边想自拍时，一阵强风吹……”

“他几乎没有注意到我在那里。他一直在计算足球动作，并预告了结果。”Seema 打断道。

“那太棒了！”

Seema 盯着 Lingaraj。Lingaraj 移开目光继续说下去。

## 线程属性

你举办了一个派对，安排了厨师和调酒师参加。有些朋友可能带着司机来，有的坐出租车，有些是走来的。有这样的人。派对结束后，你的朋友回去了。你想知道一个朋友是否到了家。所以，你给她打电话，确认她是否安全到家。现在，那个来的厨师，你不会打电话去询问他是否安全到家。更何况，如果准备的菜不好吃，而你发现他未经许可也喝了一些酒。

所以，如果你把这两个回家的过程想象成线程，一个是连接线程（attached thread），另一个是分离线程（detached thread）。因此，你可以为线程指定属性，告诉它以特定的方式运行。以下是列表：

```c
#include <pthread.h>

int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);

int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);

int pthread_attr_setschedpolicy(pthread_attr_t *attr, int policy);

int pthread_attr_getschedpolicy(const pthread_attr_t *attr, int *policy);

int pthread_attr_setschedparam(pthread_attr_t *attr, const struct sched_param*param);

int pthread_attr_getschedparam(const pthread_attr_t *attr, struct sched_param*param);

int pthread_attr_setinheritsched(pthread_attr_t *attr, int inherit);

int pthread_attr_getinheritsched(const pthread_attr_t *attr, int *inherit);

int pthread_attr_setscope(pthread_attr_t *attr, int scope);

int pthread_attr_getscope(const pthread_attr_t *attr, int *scope);

int pthread_attr_setstacksize(pthread_attr_t *attr, int stacksize);

int pthread_attr_getstacksize(const pthread_attr_t *attr, int *stacksize);

#include <pthread.h>

int pthread_attr_init(pthread_attr_t *attr);

int pthread_attr_destroy(pthread_attr_t *attr);
```

第一个函数初始化线程属性，第二个函数销毁它。

“你创建了线程，很快就需要它。”

“可能你在销毁线程对象。”

```c
int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
```

它有两个参数，属性对象指针和 `detachstate`。在标志中你可以指定：

- `PTHREAD_CREATE_JOINABLE`：默认值，你必须等待线程（join）。
- `PTHREAD_CREATE_DETACHED`：你不需要等待线程。

“所以你永远不知道厨师是否到了家。”

```c
int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);
```



这告诉你线程当前的状态。注意，`int detachstate` 是你指定的。这里，你指定了一个指针，将返回当前状态的值。

“一个线程是否会被另一个线程抢占。”

“没有同等对待。”

“如果一个资源上有互斥锁，你可以调度哪个线程获取资源，在多个线程运行时，一旦互斥锁解锁。”

第二个函数返回`*policy`中的状态。

```c
int pthread_attr_setschedparam(pthread_attr_t *attr, const struct sched_param *param);

int pthread_attr_getschedparam(const pthread_attr_t *attr, struct sched_param *param);
```

这允许你控制运行调度策略为`SCHED_OTHER`的线程。

```c
int pthread_attr_setinheritsched(pthread_attr_t *attr, int inherit);

int pthread_attr_getinheritsched(const pthread_attr_t *attr, int *inherit);
```

这意味着新线程的调度是由属性设置的还是从创建它的线程继承。这可以取两个值：

- `PTHREAD_EXPLICIT_SCHED`
- `PTHREAD_INHERIT_SCHED`

```c
int pthread_attr_setscope(pthread_attr_t *attr, int scope);

int pthread_attr_getscope(const pthread_attr_t *attr, int *scope);
```

这控制线程调调的计算方式。

```c
int pthread_attr_setstacksize(pthread_attr_t *attr, int scope);

int pthread_attr_getstacksize(const pthread_attr_t *attr, int *scope);
```

这用于需要更多栈空间的线程。根据局部变量的大小或例程的数量，为特定目的指定栈大小。

```c
int pthread_attr_setstackaddr(pthread_attr_t *attr, void *stackaddr);
```

“你可以指定栈地址，”Seema 回道。

### 线程取消

```c
#include <pthread.h>

int pthread_cancel(pthread_t thread);
```

这取消一个线程。但线程是否可以取消取决于线程本身。这就像是一种侮辱。一位大师曾说：“侮辱的刀掉落在我的脚边。我不会捡起来用它刺自己。”

所以，取消取决于线程。如果线程是否愿意被取消，在编码时，你使用以下函数：

```c
#include <pthread.h>

int pthread_setcancelstate(int state, int *oldstate);
```

在这里，`int state` 可以有两个值：

`PTHREAD_CANCEL_ENABLE`

或

`PTHREAD_CANCEL_DISABLE`

`oldstate` 参数获取之前的状态。

“我第一次听到关于你的哲学。非常深奥。”

“我曾有自己的哲学。我曾在一个摩天大楼里当管道工，有一天，我收到投诉说水箱漏水了。我爬上去，在平台上看到一个女人。我感觉到她在忙些什么，我和她交谈了。”![](img/image_rsrc85.jpg)

我开始谈论生活，持续了一个小时。然后她说：“我刚刚爬上这栋楼是为了展示信仰的力量。但在听了你的之后，我想跳。”

Seema 拍了拍额头。

那些日子，我正试图用我的性格影响世界。无论如何，如果线程被取消，你可以使用 C 库函数：

```c
#include <pthread.h>

int pthread_setcanceltype(int type, int *oldtype);
```

`type` 是：

`PTHREAD_CANCEL_ASYNCHRONOUS`

这在接收到请求时立即取消线程。

`PTHREAD_CANCEL_DEFERRED`

这取消线程直到指定的`pthread`函数被调用。

我想我们关于线程的话多了。

# 进程间通信

## 管道

让我们接触进程间通信。

从一个故事开始。我喜欢那个女孩并想更了解她。所以，我为她写了这首诗。

你，  
看到我的心在徘徊  
在平静的河流中  
在童真的斜坡上  
掉进海洋  
我们能多聊聊吗？  
关于北方的山脉  
关于如何在那里点燃篝火  
关于南方的草原  
在那里坐着喝着咖啡  
延伸的沙漠  
把骆驼系在绿洲的棕榈树上  
西方的海洋  
拿着海壳贴在耳朵  
东方的天空  
被它的许多月亮点亮  
珠宝躺在床上  
清澈的水流下  
羚羊护着你  
在起伏的水域中  
森林变成了长笛  
生命是和谐的  
那里无事可做  
所有发生的一切  
源于包容之，一片叶子

我想把这封信读给她听，于是到了她家。我响了铃，她的父亲叫他“pop”，打开了门。那是一个大房子。我告诉我想见 Suparna。

![](img/image_rsrc85F.jpg)

“你想告诉她？”他问。

“是私事的，”我回答道。

“你想告诉她的，告诉我，我会告诉她的。”

我很惊讶。我告诉他关于 Linux 中的多线程以及它是如何实现的，这持续了一小时。

“我会告诉她的，”他说并关上了门。

我重复了这一周，深入研究多线程。第八天，他打开了门。

“在多线程中……”我开始。

“你想告诉她的，直接告诉她。”

“那也无果了，我想。”

“以后我会告诉你的。所以，她的 pop 就像一个管道。这引出了第一个 C 库函数。”

```c
#include <stdio.h>

FILE *popen(const char *command, const char *open_mode);
```

所以，这通常用于向进程传递命令。`open_mode` 是`r`或`w`。

调用程序可以使用`"r"`从被调用进程接收输出。

调用程序可以使用`"w"`将其输出发送到被调用进程的输入，”Lingaraj 说。

```c
int pclose(FILE *stream_to_close);
```

这关闭管道。如果被调用进程仍在运行，`pclose` 将等待它完成然后关闭管道。

它返回进程的退出码，其文件流为。

“这是一个示例，”Lingaraj 展示给她并开始解释。

```c
pipe_fork.c

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <fcntl.h>

int main(){

    int total_bytes;
    int filed_pipe[2];
    const char chars_passed[] = "Crocodile Doctor";
    char buffer[BUFSIZ +1];
    pid_t fork_success;

    memset(buffer,'\0',sizeof(buffer));
    pipe(filed_pipe);
    fork_success = fork();

    if (fork_success == -1)
    {
        fprintf(stderr,"Fork Failure");
        exit(EXIT_FAILURE);
    }
    else if (fork_success == 0)
    {
        total_bytes = read(filed_pipe[0],buffer, BUFSIZ);
        printf("This program has read %d bytes - %s\n",total_bytes, buffer);
        exit(EXIT_SUCCESS);
    }
    else
    {
        total_bytes = write(filed_pipe[1],chars_passed, strlen(chars_passed));
        printf("This program wrote %d bytes\n", total_bytes);
    }

    exit(EXIT_SUCCESS);
}
```

输出是：

```text
This program wrote 16 bytes

This program has read 16 bytes - Crocodile Doctor
```

顺序看起来不对，仅仅是因为父进程在子进程之前结束了。所以，写入操作是先进行的。

上述程序中发生的情况是：使用`fork`创建了一个子进程，我们通过`fork`的返回值判断程序现在是处于父进程还是子进程中。在第一次实例中，它处于子进程中，因为`fork`返回值为`0`。然后我们从第一个文件描述符中进行读取。现在，一个与正在执行的程序不同的进程成功地从你编写的程序中读取了内容，尽管这是一个子进程。因此，某种通信正在发生。这很容易，因为子进程继承了文件描述符。但如果程序是完全不同的呢？

我们需要两个程序。让我们把这一个称为生产者程序，因为它提供了要传递的数据。我们将将其命名为`pipe_prod.c`。

### pipe_prod.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>

int main(){

    int total_bytes;
    int filed_pipe[2];
    const char chars_passed[] = "Crocodile Doctor";
    char buffer[BUFSIZ + 1];
    pid_t fork_success;

    memset(buffer, '\0', sizeof(buffer));
    pipe(filed_pipe);
    fork_success = fork();

    if (fork_success == -1)
    {
        fprintf(stderr,"Fork Failure");
        exit(EXIT_FAILURE);
    }
    else if (fork_success == 0)
    {
        sprintf(buffer,"%d", filed_pipe[0]);
        (void) execl("pipe_cons","pipe_cons", buffer, (char*) 0);
        printf("This is the child process,but this text won't be displayed because execl finishes off the calling process.");
        exit(EXIT_FAILURE);
    }
    else
    {
        total_bytes = write(filed_pipe[1],chars_passed, strlen(chars_passed));
        printf("This program wrote %d bytes - %s\n", total_bytes, buffer);
    }

    exit(EXIT_SUCCESS);
}
```

“第一个变化是`sprintf`函数。它将传递给`pipe`的数组中的第一个文件描述符捕获到缓冲区`buffer`中。也就是说，它将存储在`filed_pipe[0]`中的文件描述符值打印到`buffer`中。因为我们之后调用的第二个程序将不会继承这些文件描述符，”Lingaraj 解释道。

“但是有一个对`fork`的调用，”Seema 说。

“是的。逻辑是，如果我们使用`execl`调用另一个程序（我们确实会这么做），调用进程就会被消除，尽管进程 ID 仍然存在。这就像 Arun 完全接管了我的位置，而我不再那里了。所以，该进程结束了。我们调用`fork`创建子进程，然后从子进程中调用`execl`。这样，父进程被保留，而子进程结束。因此，在调用`execl`后，你不会看到`printf`语句中的文本‘This is the child process,but this text won't be displayed because execl finishes off the calling process.’”

在`execl`中，我们调用了要执行的程序`pipe_cons`，并提供了两个信息：其一是作为调用程序参数的程序名称；另一个是存储存储在`buffer`中的文件描述符。因此，通过`execl`调用的程序将拥有这些信息。

让我们来看看接收数据的消费者程序。它命名为`pipe_cons`。

### pipe_cons.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>

int main(int argc,char *argv[]){

    int bytes_ex;
    char buffer[BUFSIZ + 1];
    int file_des;

    memset(buffer,'\0',sizeof(buffer));
    sscanf(argv[1],"%d", &file_des);

    printf("The argument to the consumer program is %s\n", *argv);
    bytes_ex = read(file_des, buffer, BUFSIZ);
    printf("The process %d has read %d bytes. Content : %s \n", getpid(), bytes_ex, buffer);

    exit(EXIT_SUCCESS);
}
```

这是通过`sscanf`传递的数据。但还有一个对`memset`的调用。

```c
#include <string.h>

void *memset(void *s, int c, size_t n);
```

这是通过`sscanf`传递的数据。但还有一个对`mkfifo`的调用。

```c
#include <sys/types.h>
#include <sys/stat.h>

int mkfifo(const char *filename, mode_t mode);
```

一个错误，`-1`，且 FIFO 将无法打开。如果已经有一个进程打开了 FIFO 进行读取，那么返回的文件描述符可以用于写入 FIFO。”

“好的，所以助手会给你打电话，但如果你没法联系，他就会将其记录为错误。但如果你在电话那头接听，他就可以进行沟通。听起来有点不公平。正如你所说，这很奇怪。”Seema 说道。

“你可能不会相信的，但这真的发生了。他在屋里给我打电话想直接和她交谈后，就不再让我们独处。他以前会审视我的每一个字句。我心起大意，尝试在所有的多线程概念之间溜插一条消息。

我写道：

```c
free();

printf("Lunch and ice cream\n");
```

在行间某处。我本以为只有 Suparna 能看懂。她爸也看懂了。

“所以，本该吃午餐的地方，出现了一个拳头，然后你就尖叫了？”

“不，那家伙穿得整整齐齐的准备好了。他脸上洋着微笑。他告诉女儿：‘这个家伙在请我们吃免费的午餐和冰淇淋。我们不应该拒绝客人的请求。’然后我们大家一起去了，我不得不在这五星级酒店为他们准备了午餐和冰淇淋。

![](img/image_rsrc85G.jpg)

他甚至带了一个保温盒准备带走晚餐。我告诉他们我没钱。但他们还是开始吃了起来。在他吃完冰淇淋后，服务员来了。

‘先生，荣幸为您我们的老板服务。’服务员说道。

我震惊了。Suparna 的父亲是这家五星级酒店的老板。所以从头到尾这是一个计。他其实喜欢我，这是一个惊喜。Suparna 的父亲接下来的话让我大吃口呆。

‘请把账单交给这位年轻人。’

“但是……”我开始说。他们两个起身离开了。

然后服务员告诉我，Suparna 的父亲是镇上最吝啬的人。

我当然得洗碗。我后来还发现，那家伙一直在复印我关于 Linux 多线程的笔记并卖掉它们。

总之，我们继续吧。在创建 FIFO 后，我们可以使用文件描述符对其进行读写操作。

```c
#include <unistd.h>

int access(const char *pathname, int mode);
```

上述命令检查由`pathname`提供的文件是否存在。`mode`通常是`F_OK`。

如果写入的字节数大于`limits.h`中定义的`PIPE_BUF`，我们就说写入失败了。存在一种情况：多个程序正在向 FIFO 写入，在这种情况下，与其数据交错，只要大小不超过`PIPE_BUF`，你就是安全的。

让我们来看一个示例程序。

这是生产者程序：`fifo_prod.c`

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>

#define FIFO_NAME "/tmp/my_fifo"

int main(){

    int pipe_fd;
    int res;
    int bytes_sent = 0;
    char buffer[100];
```



```c
printf("Input text to be passed\n");

fgets(buffer, sizeof(buffer), stdin);

printf("%s", buffer);

res = mkfifo(FIFO_NAME, 0777);

if (res != 0) {
    fprintf(stderr, "Could not create the FIFO %s\n", FIFO_NAME);
    exit(EXIT_FAILURE);
}

printf("Process %d is opening the FIFO in O_WRONLY mode\n", getpid());

pipe_fd = open(FIFO_NAME, O_WRONLY);

if (pipe_fd != -1) {
    printf("Pipe succesful\n");

    res = write(pipe_fd, buffer, sizeof(buffer));

    if (res == -1) {
        fprintf(stderr, "Write error on pipe\n");
        exit(EXIT_FAILURE);
    }

    bytes_sent += res;
    (void)close(pipe_fd);
} else {
    printf("Pipe not successful\n");
    exit(EXIT_FAILURE);
}

printf("Process %d finished. Bytes sent - %d\n", getpid(), bytes_sent);

exit(EXIT_SUCCESS);
}
```

这要求用户输入一些要通过 FIFO 传递的文本。然后它在`/tmp/my_fifo`创建一个 FIFO。然后它打开 FIFO 并获取其文件描述符。接着我们向 FIFO 写入存储在`buffer`中的用户输入文本。写入后，我们关闭 FIFO。如果打开成功，我们就向管道写入。这一切都是通过返回值来测试条件的。注意这里没有`fork`或`execl`。所以，我们需要另一种方法来并排运行程序。我稍后会告诉你。

这是消费者程序`fifo_cons.c`。

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>

#define FIFO_NAME "/tmp/my_fifo"
#define BUFFER_SIZE PIPE_BUF

int main() {
    int pipe_fd;
    int res;
    int open_mode = O_RDONLY;
    char buffer[100];
    int bytes_sent = 0;

    memset(buffer, '\0', sizeof(buffer));

    pipe_fd = open(FIFO_NAME, O_RDONLY);

    if (pipe_fd != -1) {
        res = read(pipe_fd, buffer, sizeof(buffer));

        if (res == -1) {
            fprintf(stderr, "Read error on pipe\n");
            exit(EXIT_FAILURE);
        }

        bytes_sent += res;
        (void)close(pipe_fd);
    } else {
        printf("Pipe not successful\n");
        exit(EXIT_FAILURE);
    }

    printf("Process %d finished. Bytes sent - %d\n", getpid(), bytes_sent);

    exit(EXIT_SUCCESS);
}
```

- 根据变量的状态等待资源可用的进程。
- 根据变量的状态，在资源可用时使用该资源的进程。
- 进程在任务完成后更改变量的状态。
- 进程在开始任务之前更改变量的状态。

“好的。”

“在医生与电影制作人的案例中，开关是关键。”

“灯泡。”Seema 试图纠正道。

“它们是一个包的一部分。开关随灯泡免费赠送。它们必须连接在一起，否则为什么会导致触电呢？”

“不，灯泡必须和开关连接在一起，否则它怎么会亮呢？”

“很有见。”

## 与信号量相关的系统调用

### `semget`

```c
int semget(key_t key, int num_sems, int sem_flags);
```

`key`基本上是资源标识符。

“就像手术室。对手术室的引用。”

如果存在资源，`num_sems`是信号量的数量。通常为 1。

`sem_flags`允许你修改行为。上述系统调用可以返回由`key`标识的现有信号量的值，或者当标志为 0 时返回。

`sem_flags`的其他值类似于`open()`中的模式。写入（Write）意味着信号量的值可以被修改。而执行权限则没有意义。`sem_flags`的低 9 位表示权限。

它返回信号量标识符，一个非负整数。如果失败，它会设置`ERRNO`并返回 -1。

“就像开关。更确切地说，是对开关的引用。”

### `semop`

```c
int semop(int sem_id, struct sembuf *sem_ops, size_t num_sem_ops);
```

`sem_id`是`semget`返回的内容，即信号量标识符。

`sem_ops`是指向结构体数组的指针。重要的成员有：

```c
struct sembuf {
    short sem_num;
    short sem_op;
    short sem_flg;
};
```

`sem_num`是按计数定义的信号量编号。如果只有 1 个信号量，则为 0。

`sem_op`可能是最重要的，因为它是信号量必须改变的值。通常使用的是 -1 和 +1。

`sem_flag`设置为`SEM_UNDO`，它可以帮助操作系统在进程在释放信号量之前终止时释放该信号量。

### `semctl`

```c
int semctl(int sem_id, int sem_num, int command, ...);
```

此系统调用允许你直接控制信号量信息。

第一个参数是`semget()`返回的信号量标识符。`sem_num`同样是按计数定义的信号量编号。只有 1 个信号量时为 0。

`command`参数可以是：

- `SETVAL`：用于在开始时将信号量初始化为一个值。
- `IPC_RMID`：当你使用后需要删除信号量时。

可能存在命名信号量。但我不会深入探讨这一点。

## 没有信号量的程序

### `seema_loves_yoga.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int i;
    pid_t pid;

    pid = fork();

    if (pid < 0) {
        printf("Fork failed.\n");
        exit(1);
    } else if (pid == 0) {
        char *ca1 = "Vijay";
        char *ca2 = "loves football";

        puts(ca1);
        fflush(stdout);
        sleep(4);
        puts(ca2);
    } else {
        char *ca1 = "Seema";
        char *ca2 = "loves Yoga";

        puts(ca1);
        fflush(stdout);
        sleep(4);
        puts(ca2);
    }
}
```

在这里，调用了`fork`，父进程和子进程都会在`sleep`之后在`for`循环中打印两次字符。我们假设一个进程中的字符是一个一个打印的。但看输出：

```text
Seema
Vijay loves football
```

内核在父进程处于循环时偷偷插进了子进程，并尝试捕获几个，不允许任何父进程或子进程顺序打印字符串。因此，我们使用信号量来确保临界区的提交。

### `seema_loves_yoga_sem.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/sem.h>

#define KEY 0x1254

union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};

struct sembuf p = {0, -1, SEM_UNDO};
struct sembuf v = {0, +1, SEM_UNDO};

int main(int argc, char *argv[]) {
    int id = semget(KEY, 1, 0666 | IPC_CREAT);

    if (id < 0) {
        printf("Couldn't create semaphore.\n");
        exit(EXIT_FAILURE);
    }

    semun u;
    u.val = 1;

    if (semctl(id, 0, SETVAL, u) < 0) {
        printf("Semctl failed.\n");
        exit(EXIT_FAILURE);
    }

    int i;
    pid_t pid;

    pid = fork();

    if (pid < 0) {
        printf("Fork failed.\n");
        exit(1);
    } else if (pid == 0) {
        char *ca1 = "Vijay";
        char *ca2 = "loves football";

        if (semop(id, &p, 1) < 0) {
            printf("Semop failed.\n");
            exit(EXIT_FAILURE);
        }

        puts(ca1);
        fflush(stdout);
        sleep(4);
        puts(ca2);

        if (semop(id, &v, 1) < 0) {
            printf("Semop failed.\n");
            exit(EXIT_FAILURE);
        }
    } else {
        char *ca1 = "Seema";
        char *ca2 = "loves Yoga";

        if (semop(id, &p, 1) < 0) {
            printf("Semop failed.\n");
            exit(EXIT_FAILURE);
        }

        puts(ca1);
        fflush(stdout);
        sleep(4);
        puts(ca2);

        if (semop(id, &v, 1) < 0) {
            printf("Semop failed.\n");
            exit(EXIT_FAILURE);
        }
    }
}
```

## 解析

- `KEY` `0x1254`定义了一个信号量标识符。
- `union semun`包含`val`、`struct semid_ds *buf`和`unsigned short *array`，有些技术性，但对于实际操作，只需要知道定义它。这对于`semctl`是必要的。
- `struct sembuf p = {0, -1, SEM_UNDO}`和`struct sembuf v = {0, +1, SEM_UNDO}`表示信号量的减法和增操作，类似于`sem_wait`和`sem_post`。
- `semget(KEY, 1, 0666 | IPC_CREAT)`创建信号量，后续是测试其是否成功。
- `semctl(id, 0, SETVAL, u)`初始化信号量。
- `fork()`让我们判断是在子进程还是父进程中以执行相应的代码。
- 在子进程中，我们开始信号量减法。正如你可能注意到的，这是一个二值信号量。
- `semop(id, &p, 1)`和`semop(id, &v, 1)`处理减和增操作，并延迟 4 秒以确保同步。

| Seema loves Yoga | Vijay loves football |
|---|---|

部分输出在 4 秒之后打印，因为父进程比子进程先结束了。

你可能会怀疑并没有发生任何真实的通信。没有消息交换。但如果你留意，它们在时间上正在进行协调。这已经足以被称为进程间通信（IPC）了。

## IPC：共享内存

Lingaraj 说道：

“想一想我给出的那个例子，我们在岩石附近的某个地方放了一个鸡尾酒配方。敲开那些石头。你甚至允许其他进程访问该内存位置。我告诉过你这很有用，因为当我们把配方放在那些石头上并回来收集时，会有那些昨晚上实验过的人添加更多的配方。”

![](img/image_rsrc84T.jpg)

配方纸可以被看作内存。通过这张纸，醉鬼和我们之间共享信息。这比创建管道（pipes）或 FIFO 要快得多。在这里应该确保没有两个进程在同时写入。

系统调用如下：

```c
#include <sys/shm.h>

int shmget(key_t key, size_t size, int shmflg);
```

`key_t key`是内存段的标识符。你可以使用`#define`来定义键，但这个键必须被两个进程共同知道，以便于进程间通信。

值`IPC_PRIVATE`使共享内存对进程是私有的。当我的人生处于低谷时，我想分享我的故事。但我找不到任何人。所以，那曾是一个`IPC_PRIVATE`的情况。

“那真可悲。”

“确实如此，直到我开始去拜那些敲开的石头。”

“不，这不是在开玩笑。你告诉我了这么多关于你自己的故事。它们是悲伤的故事，但你让它们听起来很有趣。我笑了，我觉得很有趣，我感到有些措手不及，并对你的一些故事感到惊讶。我不是精神分析学家，但我也是人，我想告诉你，我佩服那个勇敢于自嘲的哥们。在这种情况下，我很怀念 Vijay，但在你这里我找到了一个盟友、一个朋友和一个老师。我对你有极大的尊重。根据家族传统，当我们结婚时，有一个仪式，新娘的哥哥会用甜点迎接客人。这是给家族中最受荣誉成员的特权，我无法想象还有别人能做这件事。我知道我还没和你商量过，但我已经决定由你来。”

Lingaraj望向远方。对于 Seema 而言，他第一次感到情感波动。接着他说：

“我做这件事时会开心得忘掉（‘jamoon’）的。”

“而且会有很多人你可以联系。向你介绍一位值得信赖的女性并让你嫁出去是我的责任。”

“那我们就不要浪费时间了，姐姐。大小以字节为单位。”

`shmflag`类似于`open`中的`mode`。它是`I_CREAT`与权限进行位或（OR）操作的结果，用于创建一个新的段。如果该段已经打开，它不会报错，这与使用信号量（semaphores）时不同，它会被忽略。

返回值是内存段标识符。错误时返回 -1。

```c
void *shmat(const void *shm_addr, int shmflg);
```

这用于指定哪些进程有权访问共享内存。这就像是将共享内存段挂载到进程中。

`shm_id`是你从`shmget()`获取的共享内存标识符。

`shm_addr`是共享内存挂载到进程的地址。将其留为空指针（null pointer），系统将处理分配。

但如果你想控制内存地址，可以结合`shmflg`使用。但我建议不要这样做。如果你真的想控制内存段的地址，则使用`SHM_RND`。

`shmflg`的其他值之一是`SHM_RDONLY`，它使内存段变为只读。

更多的一些值包括：

`SHM_EXEC`允许执行共享内存段中的代码。

如果`shmat`执行成功，它返回一个指向共享内存第一个字节的指针。

```c
int shmdt(const void *shm_addr);
```

这会删除共享内存段。但不是删除内容。它接收`shmat()`返回的地址。

```c
int shmctl(int shm_id, int command, struct shmid_ds *buf);
```



这用于控制共享内存。

`shm_id` 是来自`shmget`的返回值。

命令可以是`IPC_STAT`，用于获取共享内存段的状态信息。

`IPC_RMID`意味着控制。它从系统中移除共享内存段，销毁它并销毁`shmid_ds`数据结构。

`shmid_ds`结构包含了关于内存段的更多细节。

让我们来看这个写入程序：`shm_writer_1254.c`

```c
#include <sys/shm.h>
#include <stdio.h>

#define key 0x1254

int main(){

    int shmid = shmget(key,BUFSIZ,0666 | IPC_CREAT);

    char *str = (char *)shmat(shmid,0, 0);

    printf("Input some data\n");

    fgets(str,BUFSIZ, stdin);

    printf("Data written in memory is %s", str);

    shmdt(str);

}
```

在这里，有一个定义的键。这必须被调用进程已知。我们通过`shmget`创建共享内存。`BUFSIZ`通常是 8192，但取决于系统。然后挂载到内存。同样，我们将字符串分配到挂载的内存中。下一个程序也是一个写入程序，但键改成了 2995。

`shm_writer_2995.c`

```c
#include <sys/shm.h>
#include <stdio.h>

#define key 0x2995

int main(){

    int shmid = shmget(key,BUFSIZ,0666 | IPC_CREAT);

    char *str = (char *)shmat(shmid,0, 0);

    printf("Input some data\n");

    fgets(str,BUFSIZ, stdin);

    printf("Data written in memory is %s", str);

    shmdt(str);

}
```

现在，我们来看读取程序。不需要创建内存段，所以`shmget`不需要使用`IPC_CREAT`。接下来，挂载到内存段。

`shm_reader_1254.c`

```c
#include <sys/shm.h>
#include <stdio.h>

#define key 0x1254

int main(){

    int shmid = shmget(key,1024,0666);

    char *str = (char *)shmat(shmid,0, 0);

    printf("Data read from memory is %s", str);

    shmdt(str);

    shmctl(shmid,IPC_RMID,NULL);

    return 0;

}
```

在读取程序中，不需要创建内存。只需要键。

`shm_reader_2995.c`

```c
#include <sys/shm.h>
#include <stdio.h>

#define key 0x2995

int main(){

    int shmid = shmget(key,BUFSIZ,0666);

    char *str = (char *)shmat(shmid,0, 0);

    printf("Data read from memory is %s", str);

    shmdt(str);

    shmctl(shmid,IPC_RMID,NULL);

    return 0;

}
```

“那是那个提示他切换话题的信号。”

“那是信号（CUE）。信号（CUE）。我说的是队列（QUEUE）。”

“哦，好的。”

### Lingaraj

```c
#include <sys/msg.h>

int msgctl(int msqid, int cmd, struct msqid_ds *buf);

int msgget(key_t key, int msgflg);

int msgrcv(int msqid, void *msg_ptr, size_t msg_sz, long int msgtype, int msgflg);

int msgsnd(int msqid, const void *msg_ptr, size_t msg_sz, int msgflg);
```

消息队列就像你的即时通讯软件。如果我给你发送消息，消息就会排队。所以，当你打开应用时，它们就会被送达。

```c
int msgget(key_t key, int msgflg);
```

你可以使用上述系统调用创建或访问消息队列。`key`，你知道的可以取`IPC_PRIVATE`，它的作用是……？”

“创建一个只能由创建它的进程访问的消息队列。而`msgflg`通常是`IPC_CREAT`与九位权限位进行位或操作。如果使用了`IPC_CREAT`，即使已经存在消息队列，也不会报错。

返回一个消息队列标识符。错误时返回 -1。”Seema 回答。

```c
int msgsnd(int msqid, const void *msg_ptr, size_t msg_sz, int msgflg);
```

这是你发送消息的操作。

`msqid`是`msgget`的返回值。

`msg_ptr`参数是一个指向调用者定义的结构的指针，其通用形式如下：

```c
struct msgbuf {

  long mtype;      /* 消息类型，必须 > 0 */

  char mtext[1];   /* 消息数据 */

};
```

`msgflg`决定了当当前消息队列满或达到系统消息队列限制时发生什么。有两种场景：

| `IPC_NOWAIT`（设置） |
| --- |
| `IPC_NOWAIT`（清除） |

`msgsnd`成功时返回 0，失败时返回 -1。

```c
int msgrcv(int msqid, void *msg_ptr, size_t msg_sz, long int msgtype, int msgflg);
```

这从消息队列中接收消息。

`msqid`再次是由`msgget`返回的。

`msg_ptr`是指向要接收消息的指针。

`msg_sz`是消息的大小。

`long int msgtype`指定消息的类型。

`msgflg`设置要检索消息的优先级。

```c
int msgctl(int msqid, int command, struct msqid_ds *buf);
```

这是用于控制消息队列的。命令之一是：

`IPC_RMID`用于删除消息队列。

`ipcs`命令。

`ipcs -s`、`ipcs -m`、`ipcs -q`将告诉你是否有任何信号量、共享内存或消息队列仍然留存。如果进程完成后仍残留某些信号量、共享内存或消息队列，你可以分别使用`ipcrm -s`、`ipcrm -m`和`ipcrm -q`来移除它们。

消息队列程序在外观步骤上与共享内存的工作方式基本相同。

让我们看两个程序，先看发送者，再看接收者。

### `mqsender.c`

```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>
#include <sys/msg.h>

#define key 0x1254

struct message_st {

  long int msg_type;

  char text[BUFSIZ];

};

int main(){

  int loop_cond = 1;

  struct message_st data_passed;

  int msgid;

  char buffer[BUFSIZ];

  msgid = msgget((key_t)key, 0666 | IPC_CREAT);

  if (msgid == -1) {

    fprintf(stderr, "msgget failed with error: %d\n", errno);

    exit(EXIT_FAILURE);

  }

  while(loop_cond) {

    printf("Enter text to be passed. Type 'enough' to stop: ");

    fgets(buffer, BUFSIZ, stdin);

    data_passed.msg_type = 1;

    strcpy(data_passed.text, buffer);

    if (msgsnd(msgid, (void *)&data_passed, BUFSIZ, 0) == -1) {

      printf("msgsnd failed\n");

      exit(EXIT_FAILURE);

    }

    if (strncmp(buffer, "enough", 6) == 0) {

      loop_cond = 0;

    }

  }

  exit(EXIT_SUCCESS);

}
```

“你能解释一下发生了什么吗？”Lingaraj 问道。

Seema 此时对编程已经很熟悉，并开始解释。

```c
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <errno.h>
#include <unistd.h>
#include <sys/msg.h>

#define key 0x1254

struct message_st {

  long int msg_type;

  char text[BUFSIZ];

};
```

我们包含了必要的头文件。

我们定义了结构`message_st`。

我们声明了`data_passed`变量来传递数据。

```c
int main(){

  int loop_cond = 1;

  struct message_st data_passed;

  int msgid;

  char buffer[BUFSIZ];

  msgid = msgget((key_t)key, 0666 | IPC_CREAT);

  if (msgid == -1) {

    fprintf(stderr, "msgget failed with error: %d\n", errno);

    exit(EXIT_FAILURE);

  }
```

我们使用`msgget`来获取队列。如果失败，向标准错误打印错误信息。

```c
  while(loop_cond) {

    printf("Enter text to be passed. Type 'enough' to stop: ");

    fgets(buffer, BUFSIZ, stdin);

    data_passed.msg_type = 1;

    strcpy(data_passed.text, buffer);

    if (msgsnd(msgid, (void *)&data_passed, BUFSIZ, 0) == -1) {

      printf("msgsnd failed\n");

      exit(EXIT_FAILURE);

    }

    if (strncmp(buffer, "enough", 6) == 0) {

      loop_cond = 0;

    }

  }

  exit(EXIT_SUCCESS);

}
```

在循环中，我们提示输入要传递的文本，输入`'enough'`停止。

我们设置消息类型为 1，并将缓冲区拷贝到结构中。

如果`msgsnd`失败，则打印失败并退出。

如果缓冲区内容是`"enough"`，则结束循环。

最后成功退出程序。

我们在循环中接收消息，并从`data.received`结构中获取它。由于没有包含消息类型的大小（`BUFSIZ`），因此字符数组的大小就足够了。如果`msgrcv`失败，我们会打印相关信息。

我们退出循环并打印结构中第二个成员的文本。如果消息恰好是‘enough’，我们将`loop_cond`设置为 0，这样它就会跳出循环。

我们使用`msgctl`根据`msgid`删除消息队列。

退出程序。”

“当我们运行程序时，我们在一个终端运行`mq_sender.c`，在另一个终端运行`mq_receiver`。输出如下：”

在终端 1 上：

```text
| $ ./mq_senderEnter text to be passed. Type 'enough' to stop: This is from the queueEnter text to be passed. Type 'enough' to stop: Going onEnter text to be passed. Type 'enough' to stop: Getting boredEnter text to be passed. Type 'enough' to stop: ByeEnter text to be passed. Type 'enough' to stop: enough |
```

在终端 2 上：

```text
| $ ./mq_receiverThe writer program sent this text: This is from the queueThe writer program sent this text: Going onThe writer program sent this text: Getting boredThe writer program sent this text: ByeThe writer program sent this text: enough |
```

## 套接字（Sockets）

“在准备面试的背景下，你可以自己对自己说话。我曾为了充分准备面试做过这种事。我以前会模拟面试小组，在脑子里组建三位绅士，并使用信号量、管道和消息队列与他们通信。当我懒得回答时，还会使用共享内存。有一次我上了一辆公交，除了我以外车上是空的，务员问我要票的数量。我说我有 4 张，包括我脑子里的面试小组。”

![](img/image_rsrc85H.jpg)

“噢，天哪！你是怎么脱困的？”

“噢，我想象的面试小组里的那些人非常老。他们最终一个接一个地去世了。那时一切就停止了。总之，重点是，你需要一套不同的工具来与他人通信。

让我们聊聊位于不同系统上的进程之间的通信。套接字。当然，你可以使用套接字在同一系统上通信，但它通常用于两个连接的系统之间的通信。

有一次，我和一个女人被困在一个岛上。这是因为跳伞伞故障导致的。我们都降落在了岛上。当时是傍晚。

我问她：

‘你想吃晚饭吗？’

她正打着电话，沉浸在她的社交网站中。

然后她抬头说：

‘我不认识你。’

于是我给她发了好友请求，她接受了。然后她给我发消息：

‘我在哪里见过你。’

![](img/image_rsrc85H.jpg)

所以，你打开一个套接字连接来处理两个不同的系统。有一种构建套接字的方法。

让我给你描述一个背景。我祖父制作了一台鸡尾酒售卖机。它有 3 个不同的出出口和额外的功能。这三个不同的出口是：

1. 用于实际饮料。这种饮料根据客户的故事而变化。如果是财务危机，就是一种饮料；如果是关于无法原谅他人，就是另一种饮料；失败的感情又是另一种饮料，以此类推。
2. 用于零食。这些是饮料的配菜，用户可以选择低脂肪和无罪恶感版本。
3. 用于个性化消息。我祖父以前写过很多名言。我很喜欢他的一句特定的名言：‘别担心你赚了多少钱，你仍然是可以生物降解的。’所以，会根据客户的情况发放合适的消息。

每个售卖口都是通过贴上贴纸来命名的，贴纸上方有一个数字，它们还配有一个放置硬币的槽。当然，没有什么是免费的，如果你只需要消息而不需要饮料，你可以单独为之付费并获取它。”

所以，如果我必须给你一个类比的话。

这些出出口在他制作时被称为端口（`ports`）。一个用于饮料，一个用于零食，另一个用于消息。

然后他必须进行组织。他必须决定关于如何提供饮料的某些技术细节，是必须倒出来，还是以小包提供。

这是他向他人提供服务并赚钱的想法。

他是一个很活跃的人，不相信被动收入，更多是因为他想听听别人的的故事。所以，他没有自动化这个过程。他用笔记本来分配端口号、技术细节以及鸡尾酒售卖机放置的位置。这构成了一个包：端口号、技术细节和地址。他把这个包称为套接字（`socket`）。虽然我们只在讨论一台机器，你可能会质疑地址的必要性，但他有扩张计划。

## 技术细节

这些分配器每一个都有一个关联的按钮。当新客户来并按下按钮时，他会向外看并竖起耳朵表示他在听。傍晚时，会有很多客户过来。

现在，我的祖父正在听并已准备好了。客户不能走进来就开始讲述他的诉苦故事。他必须先投一个硬币，投到分配出口旁相关的硬币槽里。然后我的祖父会看到硬币，一眼就能验证其真伪。

在接受后，我的祖父会写一个数字告诉客户他的连接现在已被接受。在客户端侧，客户需要意识到他需要什么，他是需要饮料还是消息，以及它们在哪个端口被提供。

让我们看一些系统调用。

```c
#include <sys/types.h>
#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

套接字就像一个文件描述符。

```c
#include <sys/socket.h>

int bind(int socket, const struct sockaddr *address, size_t address_len);
```



`socket` 是套接字数字。` sockaddr` 结构包含了服务器端口号、族和 IP 地址，通过将其绑定到套接字数字，并将 socket 文件描述符封装成一个包，因此，对 socket 文件描述符的引用意味着我们正在访问特定的端口和网络地址。

端口（port）和 socket 的区别在于：端口是 socket 的一部分。

地址是包含内容的结构：

```c
struct sockaddr_in {
    short int sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
};
```

`sin_family` 可以是 `AF_INET`，尽管还有其他可能性。

`sin_port` 是端口号，`in_addr` 是 IP 地址。

如果客户端必须通过 socket 跨网络连接，它需要服务器计算机的 IP 地址。IP 地址类似于 `255.255.255.255` 这种格式，其中 `255` 是最大值。这是一种识别设备的方式。

`sin_addr` 是 IP 地址结构：

```c
struct in_addr {
    unsigned long int s_addr;
};
```

成功时返回 `0`，错误时返回 `-1`。

### 错误类型

| Error | Description |
| :--- | :--- |
| `EBADF` | 无效的文件描述符 |
| `ENOTSOCK` | 不引用 socket。 |
| `EINVAL` | 已经存在相同命名标识符的 socket。 |
| `EADDRNOTAVAIL` | 地址不可用 |
| `EADDRINUSE` | 该地址已绑定了 socket。 |

```c
#include <sys/socket.h>

int listen(int socket, int backlog);
```

这使得 socket 能够监听传入的连接并分配一个连接队列。`backlog` 是等待处理连接的最大数量。

一旦服务器在执行上述调用后准备好监听，客户端就可以发起请求了。

服务器可以使用此系统调用来接受连接：

```c
#include <sys/socket.h>

int accept(int socket, struct sockaddr *address, size_t *address_len);
```

`accept()` 系统调用会创建一个新的 socket 与该特定客户端通信，并返回其文件描述符。如果服务器必须为许多客户端提供服务，这将非常有帮助。这是一个重要的这一点：对于每个连接到服务器 socket 的客户端，在执行 `accept` 之后都会分配另一个数字。客户端的地址被存放在 `sockaddr` 结构中。

如果没有客户端，`accept` 调用将阻塞。但你可以通过以下方式更改它：

```c
int flags = fcntl(socket, F_GETFL, 0);

fcntl(socket, F_SETFL, O_NONBLOCK|flags);
```

在 `flags` 中使用 `O_NONBLOCK` 设置。

在客户端侧，我们只需要连接、发送或接收以及关闭。

```c
#include <sys/socket.h>

int connect(int socket, const struct sockaddr *address, size_t address_len);
```

该 socket 是客户端的 socket 而不是服务器的 socket。服务器的规范在 `sockaddr` 结构中给出，包含 IP 地址、端口号等。

成功时返回 `0`，错误时返回 `-1`。错误可能是：

| Error | Description |
| :--- | :--- |
| `EBADF` | 无效的文件描述符 |
| `EALREADY` | 该 socket 正在进行连接 |
| `ETIMEDOUT` | 连接超时 |
| `ECONNREFUSED` | 连接被服务器拒绝。 |

你可以像对待文件描述符一样对 socket 使用 `write` 和 `read` 系统调用。

当我们进入编程阶段时，你将看到这一点。

```c
int close(int socket)
```

关闭 socket。这既可以用于服务器端，也可以用于客户端。

在之前的进程间通信（Inter-process Communication）示例中，我们必须使用 socket。这是理解通信的基本方法。

`writefds` 用于写入就绪，`errorfds` 用于我们想要检查错误条件的文件描述符集合。

`timeval` 结构体包含两个成员，一个指定用户时间，另一个指定微秒为单位的时间。

这是超时值，当这段时间过去后，`select` 将带有已激活的文件描述符返回。

```c
#include <sys/types.h>
#include <sys/time.h>

void FD_ZERO(fd_set *fdset);
void FD_CLR(int fd, fd_set *fdset);
void FD_SET(int fd, fd_set *fdset);
int FD_ISSET(int fd, fd_set *fdset);
```

上述是一组宏。

- `FD_ZERO` 初始化文件描述符集合，无论是 `readfds`、`writefds` 还是 `errorfds`。
- `FD_CLR` 从文件描述符集合中移除一个文件描述符。
- `FD_SET` 向文件描述符集合中添加一个文件描述符。
- `FD_ISSET` 检查属于特定文件描述符集合的文件描述符是否激活。这在 `select` 返回后进行，以查看我们感兴趣的文件描述符是否准备好进行读、写或是否存在错误条件。

我们很快将在一个程序中看到这些操作的运行情况。

还有几个函数需要过一遍。

不同类型的计算机在通过网络传输的多字节整数值上达成了一致，并使用了网络字节序，特别是端口号。不同的计算机可能使用不同的方式来表示所需的数字。我的门牌号是 `1\.`。在我的脑海中，我把它看作：

```text
((-b) ± √(b²-4ac))
```

`2a`

其中：

`a = 3`  
`b = -6`  
`c = 3`

出于某种原因，如果我从外卖服务点餐，我不能把这个放在地址框里。我必须输入 `1\.`。因此，我们有函数充当原生主机格式与标准网络之间的中介桥梁。

```c
#include <netinet/in.h>

unsigned long int htonl(unsigned long int hostlong);
```

将主机格式转换为标准网络长整型。

```c
unsigned short int htons(unsigned short int hostshort);
```

主机格式转换为网络格式短整型。

```c
unsigned long int ntohl(unsigned long int netlong);
```

网络格式转换为主机长整型。

```c
unsigned short int ntohs(short int unsigned short int netshort);
```

网络格式转换为主机短整型。

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

in_addr_t inet_addr(const char *cp);
```

直白地说，这个函数将你的 IP 地址转换为网络格式。

“如果服务器和客户端不知道端口号或地址怎么办？”

在这种情况下，可以使用一些函数来获取计算机的完整细节。例如：

```c
#include <netdb.h>

struct hostent *gethostbyaddr(const void *addr, size_t len, int type);
struct hostent *gethostbyname(const char *name);
```

这将返回一个结构体：

```c
struct hostent {
    char *h_name;
    char **h_aliases;
    int h_addrtype;
    int h_length;
    char **h_addr_list
};
```

对于服务相关的端口号：

```c
#include <netdb.h>

struct servent *getservbyname(const char *name, const char *proto);
struct servent *getservbyport(int port, const char *proto);
```

它返回一个结构体：

```c
struct servent {
    char *s_name;
    char **s_aliases;
    int s_port;
    char *s_proto;
};
```

```c
#include <arpa/inet.h>

char *inet_ntoa(struct in_addr in);
```

这会将 Internet 主机地址转换为点分位格式的字符串。

```c
#include <unistd.h>

int gethostname(char *name, int namelength);
```

这将主机名写入 `name` 提供的字符串中。当然，你必须对想要建立网络的系统有所了解。

## UDP

正如我所说，UDP 是没有保证的。你以与 TCP/IP 类似的方式构建程序，但不是使用 `read` 和 `write`，而是使用以下系统调用。UDP 是获取某些不重要数据的一种廉价方法。

```c
int sendto(int sockfd, void *buffer, size_t len, int flags, struct sockaddr *to, socklen_t tolen);
```

`sendto` 向 socket 发送。

```c
int recvfrom(int sockfd, void *buffer, size_t len, int flags, struct sockaddr *from, socklen_t *fromlen);
```

`recvfrom` 系统调用在 socket 上等待来自指定地址的数据包，并将其接收到缓冲区中。

现在让我们来看一些使用 `select` 的程序。

## 首先是服务器：`server_select.c`

```c
#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <netinet/in.h>
#include <sys/select.h>
#include <string.h>

int create_tcp_socket() {
    struct sockaddr_in saddr;
    int fd, ret_val;

    fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    printf("Created a socket with fd : %d\n", fd);

    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(7000);
    saddr.sin_addr.s_addr = htonl(INADDR_ANY);

    ret_val = bind(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));
    ret_val = listen(fd, 5);

    return(fd);
}

int main() {
    fd_set read_set, testfds;
    struct sockaddr_in client_address;
    int nread, server_fd, lc = 0, ret_val, i;
    char buf[100];

    server_fd = create_tcp_socket();

    while (1) {
        FD_ZERO(&testfds);
        FD_SET(server_fd, &testfds);

        printf("Starting loop %d\n", lc);
        ret_val = select(server_fd + 1, &testfds, NULL, NULL, NULL);
        printf("Return from select value is : %d\n", ret_val);

        if (ret_val < 1) {
            perror("server_select");
            exit(1);
        } else {
            int new_lc = lc + 3;

            for (fd = 3; fd <= new_lc; fd++) {
                if (FD_ISSET(fd, &testfds)) {
                    if (fd == server_fd) {
                        printf("It is a new connection to the server. So grant it\n");

                        socklen_t addrlen = sizeof(client_address);
                        fd = accept(
                            server_fd,
                            (struct sockaddr *)&client_address,
                            &addrlen
                        );

                        FD_SET(fd, &testfds);
                        printf("Added client with fd %d\n", fd);
                    } else {
                        printf("The client %d is an already connected one. So read data\n", fd);

                        nread = read(fd, buf, sizeof(buf));
                        printf(
                            "\nSize of buf is : %ld and received message: %s\n",
                            nread,
                            buf
                        );

                        FD_CLR(fd, &testfds);
                    }
                }
            }
        }

        lc++;
    }
}
```

```c
printf("Starting select in loop %d and waiting\n", lc);

while (1) {
    FD_ZERO(&testfds);
    testfds = read_fd_set;

    printf("Loop %d starting\n", lc);
    printf("Starting select in loop %d and waiting\n", lc);

    ret_val = select(FD_SETSIZE, &testfds, NULL, NULL, NULL);
}
```

启动 `select` 并开始监控是否有任何活动。当它返回时，它并不会告诉你活动具体的发生的位置，但有一种方法可以知道。在这里，由于只对 `testfds` 进行读取监控，因此不需要将任何其他文件描述符集合传递给 `select` 用于写入或检查异常。也没有设置超时值，因此该调用只有在发生某种活动时才会返回。

在这里，我们使用 `testfds` 作为 `read_fd_set` 的扩展，因为我们想在 `read_fd_set` 中填充值，但在每次迭代的开始时初始化 `testfds`。某种意义上，我们想保持 `read_fd_set` 中的数据完好无损。这使得 `testfds` 可以在修改而不丢失我们之前设置的文件描述符。

```c
printf("Return from select value is : %d\n", ret_val);

if (ret_val < 1) {
    perror("server_select");
    exit(1);
}
```

如果 `select` 失败，这将打印相关消息。

```c
else {
    int new_lc = lc + 3;
}
```

谈到上面那行代码，我们依赖一些系统知识。我们知道 `0`、`1` 和 `2` 分别代表标准输入、标准输出和标准错误。如果创建了更多文件描述符，对于特定的进程，它们将按照顺序进行分配，因为它们对于该进程是唯一的。所以，我们利用这一点。在这种情况下，进程开始后创建的第一个文件描述符是 `3`，即套接字。随后，客户端文件描述符从 `4` 开始。



```c
for(fd = 3; fd <= new_lc; fd++)
```

在这里，我们启动了一个从文件描述符 3 开始并递增的`for`循环。`fd`是文件描述符编号。

```c
{
    if(FD_ISSET(fd, &testfds))
```

我们检查属于`testfds`的`fd`文件描述符是否已变为活动。如果是，我们就继续。

```c
{
    if(fd == server_fd)
```

查看`server_fd`是否被激活。只有当客户端尝试与服务器进程建立新连接时，它才会被激活。你可能记得，接受连接后，会使用一个特定客户端的文件描述符。

```c
    {
        printf("It is a new connection to the server. So grant it\n");
        addrlen = sizeof(client_address);
        client_particular_fd = accept(server_fd, (struct sockaddr *)&client_address, &addrlen);
        FD_SET(client_particular_fd, &read_fd_set);
        printf("Added client with client_particular_fd %d\n", fd);
    }
```

在这里，我们接受连接并分配一个特定的客户端`fd`用于通信。

```c
else{
    printf("The file descriptor %d is an already connected one. So read data\n", fd);
    read(fd, &buf, sizeof(buf));
```

在这里，如果激活的不是`server_fd`，即如果它不是新连接的请求，那么意味着一个已经连接的客户端正在尝试传递消息。我们向用户打印相关消息。然后使用文件描述符编号`fd`读取它。

```c
    printf("\nSize of buf is : %ld and received message: %s\n",sizeof(buf), buf);
    FD_CLR(fd, &read_fd_set);
}
```

我们向用户打印从已连接客户端收到的消息内容。我们使用`FD_CLR`从集合中清除该文件描述符，因为如果不这样做，它将仍然留在下一次迭代中，并且会再次从该套接字读取消息。但这带来了一些局限性，我们将在看到输出后进行讨论。

```c
    }
lc++;
}
}
```

为了测试这个服务器的效率，我们需要两个客户端。一个连接到服务器并在 15 秒后传递消息；另一个连接到服务器并立即传递消息。我们交替运行它们，服务器必须在处理传入的消息和接受连接之间进行切换。

### `client_select_1.c`

```c
#include <sys/types.h>
#include <sys/time.h>
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdlib.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <errno.h>
#define DATA_BUFFER "Seema learnt"
int main(){
    char input[100];
    struct sockaddr_in saddr;
    int fd, ret_val;
    struct hostent *local_host;
    fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    printf("Created a socket with fd : %d\n", fd);
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(7000);
    saddr.sin_addr.s_addr = inet_addr("127.0.0.1");
    ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));
    if (ret_val == 0) {
        printf("Connected to the server.\n");
        printf("Sleep 15 seconds before sending data.\n");
        sleep(15);
        ret_val = write(fd, DATA_BUFFER, strlen(DATA_BUFFER));
        printf("Sent data: %d bytes\n", ret_val);
    }
    close(fd);
    return 0;
}
```

### `client_select_2.c`

```c
#include <sys/types.h>
#include <sys/time.h>
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdlib.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <errno.h>
#include <string.h>
#define DATA_BUFFER "Vijay has changed"
int main(){
    char input[100];
    struct sockaddr_in saddr;
    int fd, ret_val;
    fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    printf("Created a socket with fd : %d\n", fd);
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(7000);
    saddr.sin_addr.s_addr = inet_addr("127.0.0.1");
    ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));
    if (ret_val == 0) {
        printf("Connected to the server.\n");
        ret_val = read(fd, input, sizeof(input));
        if (ret_val > 0) {
            input[ret_val] = '\0';
            printf("Received message: %s\n", input);
        }
    }
    close(fd);
    return 0;
}
```

我们首先运行`server_select.c`，然后在不同的终端中运行`client_select_1.c`和`client_select_2.c`。

我们在启动服务器的终端上得到以下输出：

```text
Created a socket with fd : 3
Loop 0 starting
Starting select in loop 0 and waiting
Return from select value is : 1
It is a new connection to the server. So grant it
Added client with client_particular_fd 4
Loop 1 starting
Starting select in loop 1 and waiting
Return from select value is : 1
It is a new connection to the server. So grant it
Added client with client_particular_fd 5
Loop 2 starting
Starting select in loop 2 and waiting
Return from select value is : 1
The client 5 is an already connected one. So read data
Size of buf is : 100 and received message: Vijay has changed
Loop 3 starting
Starting select in loop 3 and waiting
Return from select value is : 1
The client 4 is an already connected one. So read data
Size of buf is : 100 and received message: Because Seema learnt Linux
Loop 4 starting
Starting select in loop 4 and waiting
```

这是在`client_select_1.c`发送消息之前等待 15 秒后的输出。这至少等待了 15 秒。

二. 如果`client_select_1`进程在第一条消息（“Because Seema learn Linux”）之后等待 10 秒并决定发送另一条消息，它将不会被服务器读取。因为我们已经从`read_fd_set`中移除了该`fd`。在客户端关闭连接之前，理想情况下我们希望它留在`read_fd_set`中。

有一种方法可以绕过这个限制。一种方法是获取 socket 上`read`调用的返回值。如果激活时返回值为 0，则意味着客户端已关闭连接。随后我们会在服务器端关闭客户端的 socket 文件描述符。由于我们只关闭了客户端端已完成的 socket，而没有清除客户端端尚未完成的 socket，因此在下一次迭代中，开启的客户端 socket 文件描述符将留在检查读取活动的文件描述符集中。已关闭的则不会再次被激活。

此外，它显示“Loop 0”开始。这看起来并不对。因此，我们在`server_select2.c`中引入了这些更改。

### `server_select2.c`

```c
#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <netinet/in.h>
#include <errno.h>
#include <string.h>
#include <sys/select.h>
#include <sys/socket.h>
int create_tcp_server_socket() {
    struct sockaddr_in saddr;
    int fd, ret_val;
    fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    printf("Created a socket with fd : %d", fd);
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(7000);
    saddr.sin_addr.s_addr = htonl(INADDR_ANY);
    ret_val = bind(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));
    ret_val = listen(fd,5);
    return(fd);
}

int main() {
    int nread;
    fd_set read_fd_set, testfds;
    struct sockaddr_in client_address;
    int server_fd, lc = 1, ret_val, i;
    int addrlen, fd;
    char buf[100];
    server_fd = create_tcp_server_socket();
    FD_ZERO(&read_fd_set);
    FD_SET(server_fd, & read_fd_set);
    while (1) {
        FD_ZERO(&testfds);
        testfds = read_fd_set;
        printf("Loop %d starting\n", lc);
        printf("Starting select in loop %d and waiting\n", lc);
        ret_val = select(FD_SETSIZE, &testfds, NULL, NULL, NULL);
        printf("Return from select value is : %d\n", ret_val);
        if(ret_val < 1) {
            perror("server5");
            exit(1);
        } else {
            for(fd = 3; fd <= FD_SETSIZE; fd++) {
                if(FD_ISSET(fd, &testfds)) {
                    if(fd == server_fd) {
                        printf("It is a new connection to the server. So grant it\n");
                        addrlen = sizeof(client_address);
                        fd = accept(server_fd, (struct sockaddr *)&client_address, &addrlen);
                        FD_SET(fd, &read_fd_set);
                        printf("Added client with fd %d\n", fd);
                    } else {
                        printf("%d is already connected one. So read data\n", fd);
                        sleep(5);
                        printf("Client fd is : %d", fd);
                        if(read(fd, &buf, sizeof(buf)) == 0) {
                            printf("The client has closed the connection\n");
                            FD_CLR(fd, &read_fd_set);
                            close(fd);
                        } else {
                            printf("\n of buf is : %ld and received message: %s\n", sizeof(buf), buf);
                            sleep(5);
                        }
                    }
                }
            }
        }
        lc++;
    }
}
```

而修改后的`client_select_twice.c`如下所示。

### `client_twice.c`



```c
#include <sys/types.h>
#include <sys/time.h>
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdlib.h>
#include <netinet/in.h>
#include <errno.h>
#include <arpa/inet.h>

#define DATA_BUFFER "Because Seema learnt Linux"
#define DATA_BUFFER2 "New message from connected client"

int main() {
    char input[100];
    struct sockaddr_in saddr;
    int fd, ret_val;
    struct hostent *local_host;

    fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    printf("Created a socket with fd : %d\n", fd);

    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(7000);
    saddr.sin_addr.s_addr = inet_addr("127.0.0.1");

    ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));
    printf("Socket is now connected.\n");

    printf("Sleep 15 seconds before sending data.\n");
    sleep(15);

    ret_val = write(fd, DATA_BUFFER, sizeof(DATA_BUFFER));
    printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER2);

    printf("Sleep 10 seconds before sending another message\n");
    sleep(10);

    ret_val = write(fd, DATA_BUFFER2, sizeof(DATA_BUFFER2));
    printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER2);
}
```

我曾做过一次关于人必须诚实的演讲。在演讲结束时，现场只有一个人在听讲。

![](img/image_rsrc85K.jpg)

我又又讲了一个小时，结束后，我问他为什么还留在那儿，尽管其他人已经离开，活动也已经结束了。

“哦，我玩了‘真话大冒险’。我选了大冒险。下次我会选真话，”他说。

“我把它当成了赞美，”林加拉吉（Lingaraj）说道。

“我可以告诉你那并不是赞美。但你这辈子会得到足够的。”

“去吧，让维杰（Vijay）恢复正常吧。随时告诉我进展。”

“没问题。”

西玛（Seema）拥抱了林加拉吉离开了。

# 结语

西玛已经学到了足够。这从维杰开始的行为中显而易见。西玛开始使用非人格化的陈述，并在一段时间后，逐渐访问了他的记忆，并提醒他人性的一面。这起作用了。维杰恢复了正常，并带着西玛去了他最喜欢的披萨店。他开始向西玛倾注爱意，并对她非常感激。

他们结婚了，林加拉吉被荣幸用甜点迎接客人。

![](img/image_rsrc85M.jpg)

他被西玛介绍给了桑鲁普提（Santrupthi），两人发现有很多共同兴趣。

![](img/image_rsrc85N.jpg)
