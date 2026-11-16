

)?
RPAREN
SEMI
// ... RPC parameter
parameterDefinition :
IDENT // type
IDENT // name
;

函数标识符编号可以定义在任何位置，即使在 IDL 文件之外，但通常将定义保留在 IDL 文件中会不那么容易混淆。

我们的编译器后端应根据前端（由解析器发现）的语义信息生成这些文件。通常，IDL 输出包含多个源代码文件：

- 代理源代码及其头文件
- 存根源代码及其头文件

回过头来看看清单 6.4.1 和 6.4.2，我们可以看到这些代码模式与清单 6.4.4 相对应，其中 FunctionName 代表 RPC 函数名，ParameterDeclarations 代表 RPC 函数中所有函数参数的 C++ 声明，而 Parameters 代表由逗号分隔的参数列表。请参见清单 6.4.5。

## 清单 6.4.5 我们的代理和存根代码模式

```
// common
static const RPCMessage RPC_ID_FunctionName=(10+0);
//FunctionIdentifierDefinitionsForOtherFunctions

// proxy
RPCResult FunctionName(RPCSendTo sendTo, RPCSendContext sendContext, ParameterDeclarations)
{
    CMessage m;
    Message_Write(m, RPC_ID_FunctionName);
    Message_Write(m, FirstParameter);
    ...
    Message_Write(m, LastParameter);
    return RPC_Send(sendTo, sendContext, m);
}

ProxyDefinitionsForOtherFunctions

// stub
RPCResult RPC_DoStub(RPCSendTo recvFrom, RPCSendContext recvContext, CMessage& m)
{
    RPCHeader msgID;
    m.SetCursor(0);
    Message_Read(m,msgID);
    switch(msgID)
    {
    case RPC_ID_FunctionName:
    {
        FirstParameterDefinition;
        Message_Read(m,FirstParameter);
        ...
        LastParameterDefinition;
        Message_Read(m,LastParameter);
        FunctionName(
        recvFrom,
        recvContext,
        Parameters);
    }
    break;
    CasesForOtherFunctions
    }
}
```

请注意，RPCHeader、RPCSendTo 和 RPCSendContext 只是我们自己定义的局部类型。在这些示例中，它们被定义为 unsigned int。

为简单起见，此处描述的后端代码使用 printf() 或 cout，并带有多个 for() 语句。但是，当代码模式变得更复杂时，这会变得麻烦。因此，采用基于文本模板的文本生成器（例如 eNTTL [Breck99]）会很有帮助。

随着我们向 RPC 系统添加更多功能，维护和修改 IDL 编译器可能会变得困难。我们可以将其中一些部分提取到一个公共库中，该库包含多个 typedef、辅助函数和一些类。本文中的示例有一个非常小的公共库，名为 MyRPC。MyRPC 有一个名为 CMessage 的类，以及针对最常用的原始数据类型（如 int、float 和 std::string）的多个读写函数。

## RPC：用法

要在应用程序中使用我们的 RPC 实现，我们应该将 IDL 文件添加到项目中，并为 IDL 文件配置自定义生成选项。在 Visual Studio.Net 中，我们可以按照图 6.4.4 进行配置。

此外，编译后的输出文件和公共库需要添加到项目配置中。由于生成的代理和存根代码属于编译输出，建议使用 #include 语句将生成的代理和存根 .h 和 .cpp 文件间接添加到源代码中。

RPCHeader、RPCSendTo 和 RPCSendContext 用于通过网络模块发送和接收任务。如果定义的 RPC 函数数量少于 255，则节省流量的技巧是将 RPCHeader 改为 unsigned char。

![](img/672fe9a2d008ba627b1991e15d70f43e_687_0.png)

图 6.4.4 Test.IDL 的配置。

RPCSendTo 标识接收消息的远程计算机。RPCSendContext 定义其他参数，例如协议选择（TCP 或 UDP）、超时选项或多个异步响应的调用标识符。您可以随意更改这些 typedef。此 RPC 实现会自动将 RPCSendTo 和 RPCSendContext 添加到生成的 RPC 函数声明中，分别作为第一个和第二个参数。

然后，您需要向应用程序添加一个网络模块，因为我们的 RPC 系统本身没有网络模块。当代理构建消息时，它会调用 RPC_Send() 将其传递给您的网络模块。同时，当网络模块接收到消息时，应通过 RPC_Stub() 将消息传递给存根，RPC_Stub() 存在于生成的存根文件中。

## 示例程序

本文附带两个可执行示例：SimpleTest 和 RPCDuel。SimpleTest 基本上是一个 Hello World 应用程序。它有一个 IDL 文件和一个 main() 函数，该函数调用一些 RPC 代理函数，这些函数只是将生成的消息保存到本地内存中。然后假设它已经收到了代理发送的消息，它会调用一个存根函数，该函数解析消息并调用相应的 RPC 主体。虽然简单，但它应该能作为更复杂的 RPC 示例工作原理的快速示例。

RPCDuel 是 Microsoft DirectX SDK 示例中名为 Duel 的简单游戏的修改版本。RPCDuel 是基于 DirectPlay 的 RPC 示例，Duel 也是基于 DirectPlay 的。原始应用程序消息已更改为 MyRPC 消息，同时注释掉了原始部分。您可以通过搜索 RPCDuel 源文件中 RPC 前的注释来查看 RPC 的工作原理。

## 更多功能

韩国有一句谚语：“千里之行，始于足下。” 尽管这里的实现作为第一步，以简单的方式编写，仅开始展示 RPC 的实际用途，但根据您的需求改进和扩展系统应该很容易。以下是一些值得研究的改进领域。

## 允许程序中 IDL 的多个代理/存根实例

此实现生成全局函数和 typedef。这意味着对于多个游戏会话或其他重用，RPC 函数的多重实例化存在限制。一种解决方案是让 IDL 编译器生成一个代理类和一个抽象存根类，能够同时处理多个客户端。

## 错误检测与恢复

大多数在线游戏服务器或对等体都必须针对错误消息进行容错编程，这些消息可能导致各种异常，例如缓冲区溢出、无效消息格式和网络故障。解决方案之一是在我们的序列化和反序列化函数中添加边界检查。当然，如果您启用 IDL 语法以接受游戏程序员指定的值范围，可能会减少编写漏洞检查代码的工作。

## 更多数据类型

在我们的示例中，只有整数、浮点数和字符串等一些原始数据类型具有序列化和反序列化函数。但是，我们可能希望在 RPC 函数中支持更多数据类型，甚至数组和结构。SimpleTest 示例中有一个可序列化的类 Vector3D。它有这两个函数。

```
void Message_Write(CMessage& m, const Vector3D &val);
void Message_Read(CMessage& m, Vector3D &val);
```

我们可以根据需要继续定义尽可能多的序列化和反序列化函数。但是，一些 C++ 模板函数对于数组和列表等泛型结构可能更方便。

## 消息加密

在许多在线游戏中，并非所有消息都需要高度安全的加密，并且由于性能问题，只有少数几种通信消息被加密。

当我们向 IDL 语法添加加密选项，并向 IDL 输出代码模式和流式处理类添加加密功能时，我们可以通过仅一个定义轻松使用加密，例如：

```
[encrypted] RequestLogin(string id, string password);
```

## 消息压缩

通过增强我们的流式处理类和 IDL 语法，可以轻松实现消息压缩。例如，我们可能希望为每个参数添加一个“位数”选项，我们可以这样定义：

```
Knight_Attack(int type:4,int magicBuff:7,int critical:1);
```

变量 type 占用四位，magicBuff 占用七位，而 critical 占用一位。当然，我们随后需要修改流式处理类以进行位操作。

## Switch-Case 优化

为了获得更好的性能，将 RPC 存根中的 switch-case 替换为二叉搜索树也是一种好方法，这样对于 n 个 RPC 函数，可以获得 O(logn) 的复杂度。

## 调试和分析工具

通过向 RPC 代理和存根代码模板添加一些探测代码，分析服务器可能会更容易。例如，当我们想要跟踪每个传入或传出消息时，可以通过添加将函数名和参数值打印到控制台或调试输出的代码来实现。当然，我们还可以查看跟踪日志记录，显示传递了哪些函数和参数。这是一种很好的方法，有助于检测来自不良游戏客户端的粗俗内容，或导致长时间处理的 RPC 主体函数。

## 同步 RPC

大多数游戏通常不需要同步 RPC；但是，如果您的程序需要，可以在运行时向 RPC 添加此功能。

向我们的示例添加同步 RPC 需要一些额外的工作：

- 我们需要定义更多序列，等待 RPC 主体返回并将返回值传递给 RPC 函数调用者。
- 同步 RPC 仅接受可靠消息。
- 我们需要添加参数方向选项，即输入参数（inparam）和输出参数（outparam）。Inparam 发送到 RPC 服务器

