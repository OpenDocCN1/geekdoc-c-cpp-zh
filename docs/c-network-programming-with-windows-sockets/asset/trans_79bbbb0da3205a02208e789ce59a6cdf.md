

![](img/5e551abe6e0cb0588043ee757a235ddb_189_0.png)

## WinSock 类库

- 9. 设计目标
- 10. CWinSock
- 11. CDatagramSocket
- 12. CStreamSocket
- 13. 整合所有内容

![](img/5e551abe6e0cb0588043ee757a235ddb_190_0.png)

![](img/5e551abe6e0cb0588043ee757a235ddb_190_1.png)

### 设计目标

上一章考察了几个使用 WinSock 函数的示例程序。你可能会注意到，这些应用程序中“充斥着”WinSock 专用的函数调用。尽管这种编程风格在几年前可能被认为是令人满意的，但如今的面向对象概念和语言允许应用程序更好地隔离显式功能，例如网络功能。

本书的其余部分介绍一个用于构建网络应用程序的框架，以及几个使用该框架的示例应用程序。该框架由一组 C++ 类构建而成。

### 目标

生成用于管理 WinSock 网络通信的类库，其目标与面向对象编程的目标相似，包括简化、泛化和封装。在设计类库时，你不应想着如何将所有 WinSock 函数都纳入一个类中；而应从应用程序的角度来看待它，并问：“应用程序需要做什么？”

从前面的示例程序可以看出，网络应用程序执行的功能相对较少。不过，不要把功能与函数调用混为一谈。最常用的 WinSock 功能如下：

- 启动和停止 WinSock。
- 将人们喜欢使用的名称解析为计算机可用的格式。
- 创建通信端点，并可选地为其分配名称。
- 销毁端点。
- 监听并接受对端点的连接。
- 连接到端点。
- 向端点发送数据以及从端点接收数据。

本质上，这就是 WinSock 提供给应用程序的全部功能。当然，细节决定成败。类库的目标是对应用程序隐藏这些细节。这使得应用程序可以与网络部分分开开发和调试。网络部分，即 WinSock 类库，会被开发和调试，直到完全可用。然后，应用程序就可以把类库当作一个简单的黑盒来使用；向黑盒输入特定内容，再从其中得到特定输出。

根据功能列表判断，良好的类划分可能包含三个类：

- 启动、停止 WinSock 并获取其信息
- 数据报套接字（发送到和接收自）
- 流式套接字（监听、接受、连接、发送和接收）

### 封装

类库封装了有效使用 WinSock 所需的许多细节。查看前面的示例，可以看到需要使用多个变量，其中许多变量只使用一次随后就被丢弃。类库封装这些变量，并且只向应用程序公开那些必不可少的变量。

### 简化

类库的另一个目标是简化应用程序对网络功能的访问。这种简化的一部分通过将变量和函数封装在类中来实现，另一部分则来自只公开应用程序绝对必需的内容。类库隐藏了执行某些功能的复杂细节。例如，考察发送流数据这一非常常见的 WinSock 功能。在之前的示例中，应用程序必须知道何时能够发送更多数据。它还必须在每次成功但仅部分发送之后，跟踪缓冲区中还剩多少数据需要发送。通过使用类库，应用程序只需对一块数据执行发送操作，而对象会跟踪何时可以发送数据以及还剩多少数据需要发送。然后，对象可以在发送完成时通知应用程序；但在此期间，应用程序已经摆脱了发送数据的细节。

### 泛化

设计类库要求功能必须通用化。这些类可能成为将来某些派生类的基类。它们必须足够通用，以免妨碍其作为基类使用；但同时也必须具有足够的功能，以便能够立即使用。

### 折中

为了保持类的通用性，需要做出一些折中。在考虑这些折中是什么时，你必须回顾描述应用程序所利用的 WinSock 功能的列表。

作为可以做出的折中的一个示例，请看一个示例服务器应用程序。上一章介绍的两个服务器 DESERV 和 SESERV 没有指定它们运行在哪个端口上。相反，它们让 WinSock 动态分配一个端口。在这种情况下，匹配的客户端程序需要知道这个端口号，才能与服务器通信。更常见的情况是，分配给服务的端口是硬编码的，或者被输入到主机上的 services 文件中，从而允许通过名称解析端口号。考虑到这一点，可以做出一个折中：强制服务器套接字指定端口号或服务名；从而避免让 WinSock 决定端口号。这种折中简化了服务器和客户端，因而也简化了类库本身。

### 实现细节

整个 WinSock 类库由几个类组成，实现在 CWINSOCK.CPP 文件中，而 CWINSOCK.H 包含类声明。只需将此源文件添加到每个需要 WinSock 功能的项目中。这与创建动态链接库再将其链接到应用程序的做法相反。如果要从 WinSock 类创建 DLL，则必须使用 Microsoft Foundation Class 扩展 DLL，因为某些 WinSock 类派生自 MFC 类。创建此类 DLL 超出了本书的范围，但有关如何创建它的文档可从 Microsoft 资源（如 Developer Network CD）获得。

WinSock 类库的实际代码遵循 Microsoft Foundation Class 库中使用的约定。所有类名都以大写字母 C 开头，如下所示：

```cpp
class CWinSock
```

所有类成员变量都以 m_ 前缀开头。匈牙利命名法附加在 m_ 前缀之后、实际变量名之前。例如，一个包含缓冲区长度的整数可能如下所示：

```cpp
int m_nBufLen;
```

这种命名约定应能确保在应用程序中快速、轻松地识别和理解 WinSock 类引用。

### 小结

本章介绍 WinSock 类库的概念，包括其要求和可能的限制。第 10 章至第 13 章描述组成 WinSock 类库的几个类。然后，第 14 章至第 16 章将在功能完整的程序中使用这些类。

![](img/5e551abe6e0cb0588043ee757a235ddb_194_0.png)

## 10 CWinSock

本章讨论 `CWinSock` 类。

该类负责初始化 WinSock 子系统、关闭 WinSock，以及获取 WinSock TCP/IP 协议栈信息。

类声明如下：

```cpp
///////////////////////////////////////////////////////////////
// CWinSock
//
class CWinSock
{
private:
    WORD m_wVersionRequired;   // WinSock version required by application
    int m_nLastError;          // last WinSock error
    WSADATA m_wsData;          // WinSock information

public:
    CWinSock(WORD wVersionRequired = MAKEWORD(1, 1));
    int Startup();
    int Shutdown();
    void Information(LPWSADATA pWSAData);
    int LastError() { return m_nLastError; }
};
```

该类包含三个私有成员变量，在类实现之外无法访问。

### CWinSock 构造函数

CWinSock 对象的构造函数仅初始化两个成员变量。`m_wVersionRequired` 变量是应用程序所需的 WinSock 版本。它由应用程序传入构造函数。如果未提供此参数，则默认为版本 1.1。该类的构造函数如下所示：

```cpp
///////////////////////////////////////////////////////////////
// CWinSock constructor
//
// Constructs the CWinSock object. Initializes member variables
//
CWinSock::CWinSock(WORD wVersionRequired/*= MAKEWORD(1, 1)*/)
{
    // initialize member variables
    m_wVersionRequired = wVersionRequired;
    m_nLastError = 0;
}
```

### CWinSock::Startup()

`Startup()` 成员函数实际上初始化 WinSock 子系统。必须在调用任何其他 WinSock 数据操作函数之前调用它。如果发生错误

