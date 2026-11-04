
## 17 构建大型程序

一个非小型程序通常会被划分为多个文件，这样开发、测试、维护和升级等任务就更容易执行。由于在我们的工作经验中，我们深入参与了网络协议的开发，因此我们决定实现一个简单的协议，向你展示一个较大应用的示例。如果你将来决定专业从事这一领域，这个示例可能会对你有所帮助。

首先，什么是网络协议？简而言之，它是一组使系统能够通信的规则。协议可以在硬件、软件或两者中实现。一个协议示例是著名的*互联网协议（IP）*。它由互联网工程任务组（IETF）组织在 RFC 791 标准中规定。协议标准的核心是系统之间交换的信息、交换消息的格式、它们的含义以及消息处理过程。通常，协议实现的指导原则是一个有限状态机，它用状态和事件来对协议操作建模。

让我们描述一下将要实现的协议。它是 *ITU-T Q.931* 信令协议的过度简化版本。Q.931 协议用于在综合业务数字网（ISDN）中建立、维护和释放呼叫。当主叫用户拨打被叫用户的号码时，会创建一条名为 SETUP 的消息。SETUP 消息通过 ISDN 网络路由到被叫用户。如果被叫用户接受呼叫（例如拿起电话），一条名为 CONNECT 的消息会被传回主叫用户。被叫用户以 CONNECT ACK 响应，呼叫建立过程结束。在双方之间的路径上会预留一条电路以支持数据传输。现在，双方可以通信了。如果任一方关闭连接（例如挂机），一条名为 RELEASE 的消息会被发送给另一方，电路被释放。

我们的协议将从被叫用户一侧模拟消息交换。每条消息由唯一代码标识，并包含特定信息。例如，SETUP 消息的代码是 5，它包含若干信息元素，例如主叫用户的号码。为简单起见，我们假设每条消息只包含其代码。

在开始实现之前，让我们简要讨论一下如何编写较大的程序。首先，我们将应用需求分解为独立的模块。这种划分有助于项目管理和对程序结构的良好理解。每个模块的功能都应定义明确，不与其他模块重叠，以便不同的程序员可以并行实现它们。接下来，我们定义模块之间的交互、它们的依赖关系以及这些模块如何相互通信。一个通信示例是我们在 C.8 中看到的*回调*机制。每个模块的操作都映射为函数。对于每个模块，我们选择可能被其他模块共享的函数，并将其声明放入一个头文件，作为该模块的接口文件。例如，一个模块可以实现为一个库，向外部环境导出一个接口文件，如 `stdio.h`，该文件提供有关已实现函数的信息。

包含 main() 的文件通常以应用程序命名，例如 prtcl.c。常见做法是将函数定义和外部变量声明放入源文件，而将函数声明、类型定义、常量和宏放入头文件。通常，一个源文件会与一个头文件配套出现。头文件有助于阅读程序的人快速了解该源文件实现了程序的哪一部分。另一种做法是，我们可以将所有内容声明在一个头文件中，并让所有源文件都包含该文件。尽管这样只需编辑一个文件，但这并不是我们的偏好。原因之一是，每当其内容发生变化时，所有源文件都必须重新编译。对于大型应用程序来说，这可能会很耗时。被多个源文件使用的公共信息会放入一个头文件，并在需要时包含该文件。使用单个头文件的优点是，如果我们需要进行更改，不必在多个文件中搜索来进行更改。只查看一个地方既快捷又安全。

让我们开始实现。我们将程序的功能拆分为多个模块。每个源文件代表一个模块：

- prtcl.c。它包含与外部环境通信、并将接收到的消息转发给内部模块的函数。外部环境的一个示例可能是网卡，或者是使用数字键盘与协议通信的用户。
- send.c。它包含创建消息并将它们发送到上层和下层的函数。层的概念在*开放系统互连（OSI）模型*中描述，这是一个参考模型，描述应用程序如何通过网络进行通信。一个层可以用软件或硬件实现。例如，下层可能是网卡的驱动程序或网卡本身，而上层可能是向用户呈现数据的应用程序（例如 Web 浏览器）。
- recv.c。它包含解析接收数据的函数。
- fsm.c。它包含实现协议有限状态机的函数。

如前所述，我们将公共信息放入一个头文件。我们将其命名为 general.h。为避免多次编译，我们使用 #ifndef 指令。

```c
/* general.h */

#ifndef general_h
#define general_h

#include <stdio.h>

typedef unsigned char BYTE;

#define LOOPBACK_MODE

/* Message codes. */
#define SETUP         0x5
#define CONNECT       0x7
#define CONNECT_ACK   0xF
#define RELEASE 0x4D

typedef struct
{
    BYTE code;
    /* Typically, the format of the structure resembles that of
C.13.11. */
} Msg;

int fsm(Msg *p);
int forward_msg(Msg *p);
int rcv_msg(BYTE data[]);
int handle_rcvd_msg(BYTE data[]);
#endif
```

让我们描述 prtcl.c。它创建 SETUP 消息，并将该消息转发给 fsm.c。在实际情况下，这条消息是在被叫用户发起与主叫用户的通信（例如拨号）时创建的，并经过 ISDN 网络到达目的地。当应用程序从下层收到消息时，会调用函数 rcv_msg()。例如，驱动程序从网卡获取消息，并将该消息上传给应用程序。在实际实现中，我们将该函数放在一个线程中；可以把线程看作与主程序并行执行的独立程序。每当收到消息时，它会被异步调用。不必担心线程编程，我们只是给出一些提示，以防将来有人涉及类似的事情。消息包含在 data 数组中。变量 cur_state 保存协议的当前状态。我们以全局作用域声明它，向你展示如何在其他文件中将其用作 extern。

```c
#include "general.h"
#include "fsm.h"

int cur_state;

int main(void)
{
    Msg msg;

    cur_state = IDLE;

    msg.code = SETUP;
    fsm(&msg);
    return 0;
}

int rcv_msg(BYTE data[])
{
    handle_rcvd_msg(data);
    return 0;
}
```

接下来的文件是 fsm.c 和 fsm.h。协议状态机在这里实现。例如，如果在 IDLE 状态下收到 SETUP 消息，状态会变为 CALL_INIT，并且该消息会被转发以进行传输。为简单起见，我们将使用 switch 语句。然而，我们的典型选择是使用函数指针数组，如第 8 章示例中那样，以提高性能。

```c
#include "general.h"
#include "fsm.h"

extern int cur_state;

int fsm(Msg *p)
{
    switch(cur_state)
    {
        case IDLE:
            if(p->code == SETUP)
            {
                cur_state = CALL_INIT;
                forward_msg(p);
            }
            else
            {
                printf("Unexpected message %d in state %d\n",
                p->code, cur_state);
                return -1;
            }
            break;
        case CALL_INIT:
            if(p->code == CONNECT)
            {
                printf("Call activated\n");
                cur_state = ACTIVE;
                p->code = CONNECT_ACK;
                forward_msg(p);
            }
            else
            {
                printf("Unexpected message %d in state %d\n",
                p->code, cur_state);
                return -1;
            }
            break;
        case ACTIVE:
            if(p->code == RELEASE)
            {
                printf("Call released\n");
                cur_state = IDLE;
            }
            else
```
