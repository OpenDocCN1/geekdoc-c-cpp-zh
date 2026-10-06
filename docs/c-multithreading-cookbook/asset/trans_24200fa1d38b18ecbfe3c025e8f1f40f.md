

# 本书所需的准备

要执行书中的示例，将需要以下软件：

- Visual Studio 2013
  - http://www.visualstudio.com/downloads/download-visual-studio-vsd-express-windows-8
- Windows Drivers Kit: WinDDK
  - http://msdn.microsoft.com/en-us/windows/hardware/hb852365.aspx
- MySQL Connector C
  - http://dev.mysql.com/downloads/connector/c/

# 本书的读者群体

本书主要面向中级和高级用户。同步概念从一开始就被考虑在内，因此对于任何不属于特定专业领域的开发者来说，本书都是易读的。最后两章将为高级用户提供丰富的知识，对并发设计和高级线程管理等概念提供极出色的概述。

# 约定

在书中，你会发现多种文本样式，用于区分不同类型的信息。以下是这些样式的一些示例及其含义解释。

文本中的代码、数据库表名、文件夹名称、文件名、文件扩展名、路径名、虚拟 URL、用户输入和 Twitter 标识显示如下：“我们可以通过 `include` 指令包含其他上下文。”

代码块设置如下：

```cpp
class CLock
{
  public:
    Clock(TCHAR* szMutexName);
    ~Clock();

private:
    HANDLE hMutex;
};

inline Clock::Clock(TCHAR* szMutexName)
{
    hMutex = CreateMutex(NULL, FALSE, szMutexName);
    WaitForSingleObject(hMutex, INFINITE);
}

inline Clock::~Clock()
{
    ReleaseMutex(hMutex);
    CloseHandle(hMutex);
}
```

当我们希望你注意代码块中的特定部分时，相关项目将加粗：

```cpp
class Clock
{
public:
**Clock(TCHAR* szMutexName);**
**~Clock();**
private:
HANDLE hMutex;
}
```

```cpp
inline Clock::Clock(TCHAR* szMutexName)
{
    hMutex = CreateMutex(NULL, FALSE, szMutexName);
    WaitForSingleObject(hMutex, INFINITE);
}

inline Clock::~Clock()
{
    ReleaseMutex(hMutex);
    CloseHandle(hMutex);
}
```

读者在直接从书中复制粘贴代码时，注意这一点非常重要。由于书籍尺寸的限制，某些代码行无法放在单行中。我们尝试解决这个问题，但在某些情况下这是不可可能的。我们强烈建议你检查此类情况。特别是在双引号字符串的情况下，如果不小心字符串被拆分不应该拆分的地方。

在“如何操作”章节中，这一点同样重要，例如当我们说“添加现有文件”时，我们的意思是你应该使用 Windows 资源管理器导航到文件所在的文件夹，并将文件连同所有依赖项一起复制到项目中，然后再使用“添加头文件”选项将其添加。**新术语和重要词汇**将加粗显示。你在屏幕、菜单或对话框中看到的文字显示如下所示：“打开资源管理器并右键点击**头文件**。”

![](img/412b0f5bbb36adc2ddd2d5b7416518_0.png)
![](img/412b0f5bbb36adc2ddd2d5b7419_0.png)

我们随时欢迎读者的反馈。让我们知道你对这本书的看法——你喜欢或不喜欢的地方。如需发送普通反馈，只需向 feedback@packpub.com 发送电子邮件，并在邮件主题中注明书名。如果你在某个领域拥有专长，并兴趣编写或贡献书籍，请参阅我们在 www.packpub.com/authors 上的作者指南。

现在你是 Packt 书籍的自豪主人，我们提供了许多方法帮助你从购买中获得收益。你可以从 http://www.packpub.com 账户下载你购买的所有 Packt 书籍的示例代码。如果你是在其他地方购买的本书，可以访问 http://www.packpub.com/support 并注册，以便文件通过电子邮件直接发送给你。

尽管我们已尽一切努力确保内容的准确性，但错误仍然会发生。如果你在我们的某书中发现错误——可能是文本或代码中的错误——如果你能向我们报告，我们将不胜感激。这样做可以避免其他读者沮丧，并帮助我们改进本书的后续版本。请访问 http://www.packpub.com/submit-errata，选择你的书籍，点击勘误提交表并输入勘误详情。一旦你的勘误通过验证，你的提交将被接受，勘误将上传到我们的网站，或添加到该书勘误部分下的任何现有勘误列表中。

互联网上对版权材料的盗版是所有媒体中持续存在的问题。在 Packt，我们非常重视保护我们的版权和许可。如果你在互联网上遇到任何形式的我们作品的非法副本，请立即向我们提供地址或网站，以便我们寻求补救。请通过 copyright@packpub.com 联系我们并附上疑似侵权材料的链接。感谢你帮助保护我们的作者以及我们为你提供此类价值内容的能力。

如果你对本书的任何方面有疑问，可以通过 questions@packpub.com 联系我们，我们将尽力解决。

## C++ 概念与特性导论

在本章中，我们将涵盖以下主题：

- 创建 C++ 项目
- 程序结构、执行流和运行时对象
- 结构化编程方法
- 理解面向对象的编程方法
- 解释继承、重载和重写
- 理解多态
- 事件处理器和消息传递接口 (MPI)
- 链表、队列和栈示例

## 引言

所有操作系统的核心概念都是执行程序的进程或其抽象。大多数现代操作系统可以同时执行多个操作。例如，如果用户正在 Word 文档中打字，计算机可以打印文档、从硬盘缓冲区读取数据、播放音乐等。在多任务操作系统中，中央处理器（下文简称 CPU）在程序之间进行快速切换，每个程序仅执行几毫秒。

虽然在单处理器系统上，严格来说，处理器在一个单位时间内只能执行一个进程——操作系统通过极快地在这些进程之间切换，营造出多个进程同时运行的错觉。这被称为“伪并行”，与多处理器系统中由硬件支持的原生并行形成对比。

多线程是当今现代操作系统中一个非常重要的概念。它允许存在多个执行线程，这对于并行任务以及用户友好的应用程序行为非常重要。

在传统的操作系统中，每个进程都有自己的地址空间和一个执行线程——通常称为主线程或主要线程。通常，单个进程的同一地址空间内需要多个线程，它们在准并行上下文中执行，并像独立的进程一样运行，但共享同一个地址空间。

