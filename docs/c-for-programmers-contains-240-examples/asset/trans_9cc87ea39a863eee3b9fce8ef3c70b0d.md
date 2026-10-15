

在你的系统上，打开一个命令提示符，然后右键单击标题栏并选择属性。出现的“命令提示符”属性对话框中，单击颜色选项卡，并选择你偏好的文本和背景颜色。

## 从 Windows XP 命令提示符运行 C++ 应用程序

- 1. 检查你的设置。阅读本书开头 Before You Begin 部分，以确保你已将本书的示例复制到你的硬盘上。
- 2. 定位已完成的应用程序。打开一个命令提示符窗口。对于使用 Windows 95、98 或 2000 的读者，请选择 开始 > 程序 > 附件 > 命令提示符。对于 Windows XP 用户，请选择 开始 > 所有程序 > 附件 > 命令提示符。要更改到已完成的 GuessNumber 应用程序目录，输入 cd C:\examples\ch01\GuessNumber\Windows，然后按 Enter（图 1.2）。命令 cd 用于更改目录。
- 3. 运行 GuessNumber 应用程序。现在你已进入包含 GuessNumber 应用程序的目录，输入命令 GuessNumber（图 1.3）并按 Enter。[注意：GuessNumber.exe 是应用程序的实际名称；然而，Windows 默认会假设 .exe 扩展名。]
- 4. 输入你的第一次猜测。应用程序显示“Please type your first guess.”，然后在下一行显示问号（?）作为提示（图 1.3）。在提示符处，输入 500（图 1.4）
- 5. 输入另一次猜测。应用程序显示“Too high. Try again.”，意味着你输入的值大于应用程序选作正确答案的数字。因此，你应该为下一次猜测输入一个更小的数字。在提示符处，输入 250（图 1.5）。应用程序再次显示“Too high. Try again.”，因为你输入的值仍然大于应用程序选作正确答案的数字。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_52_0.png)

图 1.2 | 打开命令提示符窗口并更改目录。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_52_1.png)

图 1.3 | 运行 GuessNumber 应用程序。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_53_0.png)

图 1.4 | 输入你的第一次猜测。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_53_1.png)

图 1.5 | 输入第二次猜测并接收反馈。

- 6. 输入额外的猜测。继续玩游戏，输入值直到猜中正确数字。应用程序将显示“Excellent! You guessed the number!”（图 1.6）。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_53_2.png)

图 1.6 | 输入额外的猜测并猜中正确数字。

- 7. 再次玩游戏或退出应用程序。猜对后，应用程序会询问你是否想再玩一局（图 1.6）。在“Would you like to play again (y or n)?”提示符处，输入单个字符 y 会使应用程序选择一个新数字并显示消息“Please type your first guess.”，随后出现问号提示（图 1.7），以便你在新游戏中进行第一次猜测。输入字符 n 会结束应用程序并将你返回到命令提示符下的应用程序目录（图 1.8）。每次从头开始执行此应用程序（即步骤 3），它都会为你选择相同的数字进行猜测。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_54_0.png)

图 1.7 | 再次玩游戏。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_54_1.png)

图 1.8 | 退出游戏。

- 8. 关闭命令提示符窗口。

## 使用 GNU C++ 在 Linux 上运行 C++ 应用程序

在本节的图中，我们使用粗体高亮来指出每一步所需的用户输入。我们系统上的 shell 提示符使用波浪号（~）字符来表示主目录，并且每个提示符以美元符号（$）字符结尾。提示符在不同的 Linux 系统中会有所不同。

- 1. 定位已完成的应用程序。从 Linux shell 中，更改到已完成的 GuessNumber 应用程序目录（图 1.9），输入

```
cd Examples/ch01/GuessNumber/GNU_Linux
```

然后按 Enter。命令 cd 用于更改目录。

- 2. 编译 GuessNumber 应用程序。要在 GNU C++ 编译器上运行应用程序，你必须先通过输入以下命令进行编译

```
g++ GuessNumber.cpp -o GuessNumber
```

如图所示 1.10。此命令编译应用程序并生成名为 GuessNumber 的可执行文件。

```
~$ cd examples/ch01/GuessNumber/GNU_Linux
~/examples/ch01/GuessNumber/GNU_Linux$
```

图 1.9 | 登录到你的账户后更改到 GuessNumber 应用程序的目录。

```
~/examples/ch01/GuessNumber/GNU_Linux$ g++ GuessNumber.cpp -o GuessNumber
~/examples/ch01/GuessNumber/GNU_Linux$
```

图 1.10 | 使用 g++ 命令编译 GuessNumber 应用程序。

```
Too low. Try again.
? 375
Too low. Try again.
? 437
Too high. Try again.
? 406
Too high. Try again.
? 391
Too high. Try again.
? 383
Too low. Try again.
? 387
Too high. Try again.
? 385
Too high. Try again.
? 384

Excellent! You guessed the number.
Would you like to play again (y or n)?
```

图 I.14 | 输入额外的猜测并猜中正确数字。

- 7. 再次玩游戏或退出应用程序。猜中正确数字后，应用程序会询问你是否想再玩一局。在“Would you like to play again (y or n)?”提示符处，输入单个字符 y 会使应用程序选择一个新数字并显示消息“Please type your first guess.”，随后出现问号提示（图 I.15），以便你在新游戏中进行第一次猜测。输入字符 n 会结束应用程序并将你返回到 shell 中的应用程序目录（图 I.16）。每次从头开始执行此应用程序（即步骤 3），它都会为你选择相同的数字进行猜测。

```
Excellent! You guessed the number.
Would you like to play again (y or n)? y

I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
?
```

图 I.15 | 再次玩游戏。

```
Excellent! You guessed the number.
Would you like to play again (y or n)? n

~/examples/ch01/GuessNumber/GNU_Linux$
```

图 I.16 | 退出游戏。

## 1.8 软件技术

在本节中，我们讨论了你在软件开发社区中会听到的一些软件工程流行语。我们已在其中大多数主题上创建了资源中心，还有更多正在制作中。你可以在 www.deitel.com/ResourceCenters.html 找到我们完整的资源中心列表。

敏捷软件开发是一组方法论，试图以比以往方法论更少的资源更快地实现软件。查看 Agile Alliance（www.agilealliance.org）和 Agile Manifesto（www.agilemanifesto.org）。

重构涉及在保留其功能的同时重新处理代码以使其更清晰、更易于维护。它在敏捷开发方法论中被广泛采用。有许多重构工具可自动完成大部分重构工作。查看我们关于重构的资源中心。

设计模式是构建灵活且可维护面向对象软件的经过验证的架构。设计模式领域试图枚举这些反复出现的模式，鼓励软件设计师重用它们以用更少的时间、金钱和精力开发更高质量的软件。

游戏编程。计算机游戏业务比首映电影业务更大。大学课程甚至专业现在都致力于游戏编程中使用的复杂软件技术。查看我们关于游戏编程、C++ 游戏编程和编程项目的资源中心。

开源软件是一种开发软件的风格，与主导软件早期年的专有开发形成对比。在开源开发中，个人和公司为开发、维护和演进软件做出贡献，以换取使用该软件为自己目的的权利，通常是免费的。开源代码通常会被比专有软件大得多的受众审查，因此错误会被更快地删除。开源也鼓励更多的创新。Sun 最近宣布它正在开源 Java。你在开源社区会经常听到一些组织，例如 Eclipse Foundation（Eclipse IDE 在 C++ 和 Java 软件开发中很受欢迎）、Mozilla Foundation（Firefox 浏览器的创建者）、Apache Software Foundation（Apache Web 服务器的创建者）和 SourceForge（为管理开源项目提供工具，目前有超过 150,000 个开源项目正在开发中）。

Linux 是一种开源操作系统，也是开源运动最伟大的成功之一。MySQL 是一种开源数据库管理系统。PHP 是用于开发基于互联网的应用程序的最流行的开源服务器端“脚本”语言。LAMP 是许多开发人员用于构建 Web 应用程序的一组开源技术的缩写——它代表 Linux、Apache、MySQL 和 PHP（或 Perl 或 Python——用于类似目的的另外两种语言）。

软件通常被视为一种产品；大多数软件仍然以这种方式提供。如果你想运行一个应用程序，你从软件供应商那里购买一个软件包。然后你将该软件安装在你的计算机上并按需运行。随着新版本的软件出现，你升级你的软件，通常花费很大。对于必须在多样化的计算机设备上维护数万台系统的组织来说，这个过程可能变得繁琐。使用软件即服务（SaaS），软件在互联网上的其他地方的服务器上运行。当这些服务器更新时，全球所有客户端都会看到新功能；无需本地安装。你可以访问

