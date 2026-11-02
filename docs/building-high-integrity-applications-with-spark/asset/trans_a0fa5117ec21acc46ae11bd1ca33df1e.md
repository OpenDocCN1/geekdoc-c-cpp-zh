
```ada
exception
    when Ex : Network.Socket.Network_Error =>
        Ada.Text_IO.Put_Line
            ("*** Unable to initialize network: " & Exception_Message(Ex));
end Thumper_Server;
```

包 SPARK_Boundary 对应于图 8.4 中的虚线框。Service_Clients 过程在无限循环中执行该框内的内容，并利用我们之前描述的（边界）变量包。SPARK_Boundary 的规范如下所示：

```ada
pragma SPARK_Mode(On);

with Cryptographic_Services;
with Logger;
with Network.Socket.Reader;
with Network.Socket.Writer;
with Serial_Generator;

use Network.Socket;

package SPARK_Boundary is

    procedure Service_Clients
    with
        Global =>
            (Input =>
                (Reader.Input_Message_Stream, Cryptographic_Services.Key),
            In_Out =>
                (Logger.Log_Stream,
                 Writer.Output_Message_Stream,
                 Serial_Generator.State)),
        Depends =>
            (Logger.Log_Stream =>+
                (Reader.Input_Message_Stream, Writer.Output_Message_Stream,
                 Cryptographic_Services.Key, Serial_Generator.State),
             Writer.Output_Message_Stream =>+
                (Reader.Input_Message_Stream,
                 Cryptographic_Services.Key,
                 Serial_Generator.State),
             Serial_Generator.State =>+ Reader.Input_Message_Stream);

end SPARK_Boundary;
```

注意，with 语句准确提到了那些属于边界变量包或包含状态的包。这些 with 语句是必要的，以便各种抽象状态可用于 Service_Clients 上的数据和流依赖契约。

日志记录器的存在使依赖契约变得复杂。这很不幸，因为日志记录器是次要需求，人们可能希望它不要搅乱关键信息。不幸的是，SPARK 工具要求到（以及通常来自）日志记录器状态的流必须像任何其他流一样被正确声明。

有些流令人意外。特别是输出消息流对自身的依赖。这是因为 Service_Clients 最终调用 Writer 包中的 Send 过程。如前所述，该过程可能使输出消息流保持不变。此外，如果 Service_Clients 在尝试接收请求时只得到错误，它甚至永远不会尝试写入输出消息流。因此，输出消息流必须是 In_Out 全局项。在最初编写 Service_Clients 的契约时，这些细节并未被充分认识到。随着这些问题显现，在 Service_Clients 的实现过程中做了一些调整。

值得注意的是，流依赖契约有助于安全审查。由于攻击者可以操纵输入消息流，任何依赖该流的项都需要仔细保护。在这种情况下，所有输出都可能受到攻击。尤其值得关注的是日志流。攻击者是否可能以某种方式发送畸形请求，从而导致畸形日志消息使服务器崩溃？鉴于包 Logger 的主体不在 SPARK 中，这个问题尤其有趣。类似地，攻击者能否通过发送适当构造的畸形请求，以某种方式操纵序列号生成器的状态？

Service_Clients 过程本身包含一个无限循环，如下所示：

```ada
procedure Service_Clients is
   use type Reader.Status_Type;
   use type Writer.Status_Type;

   Client_Address   : Network.Addresses.UDPv4;

   Network_Request  : Messages.Network_Message;
   Request_Message  : Messages.Message;
   Read_Status      : Reader.Status_Type;

   Response_Message : Messages.Message;
   Network_Response : Messages.Network_Message;
   Write_Status     : Writer.Status_Type;
begin
  loop
    Reader.Receive (Message => Network_Request,
                    From    => Client_Address,
                    Status  => Read_Status);

    if Read_Status /= Reader.Success then
      Logger.Write_Error(" Failure reading request message!");
    else
      Request_Message := Messages.From_Network (Network_Request);
      Timestamp_Maker.Create_Timestamp (Request_Message, Response_Message);
      Network_Response := Messages.To_Network (Response_Message);

      Writer.Send (Message => Network_Response,
                   To      => Client_Address,
                   Status  => Write_Status);

      if Write_Status /= Writer.Success then
        Logger.Write_Error(" Failure sending reply message!");
      end if;
    end if;
  end loop;
end Service_Clients;
```

变量 Network_Request 和 Network_Response 保存从网络接收和发送到网络的 Network.Octet 类型的原始八位字节。它们是记录，携带一个固定大小的数组以及该数组中实际使用的元素数量的计数。变量 Request_Message 和 Response_Message 保存 Hermes.Octet 类型的原始八位字节，其中包含 DER 编码的 ASN.1 数据。

函数 From_Network 和 To_Network 仅对数据执行从 Network.Octet 到 Hermes.Octet 以及相反方向的类型转换。尽管区分不同种类的八位字节可能显得学究气，但这是有意义的，因为底层网络上的数据可能有许多形式。Hermes 仅处理 DER 编码的 ASN.1。但将来，时间戳消息可能被封装在某种应用协议（如 HTTP）中。因此，在 Thumper 的未来版本中，区分原始网络数据和时间戳消息将是有用的。

过程 Create_Timestamp 将请求消息转换为响应消息。每个请求都会生成一个响应；无效或畸形的请求会生成错误响应。Create_Timestamp 是应用程序的核心，并且几乎是纯函数式的。它接受一个八位字节数组并返回另一个。然而，由于每个生成的时间戳都经过数字签名并且必须包含唯一序列号，Create_Timestamp 需要使用加密密钥和序列号生成器。Create_Timestamp 的 SPARK 声明如下：

```ada
procedure Create_Timestamp (Request_Message : in  Messages.Message;
                             Response_Message : out Messages.Message)
with
  Global =>
    (Input  => Cryptographic_Services.Key,
     In_Out => Serial_Generator.State),
  Depends =>
    (Response_Message =>
      (Request_Message, Cryptographic_Services.Key, Serial_Generator.State),
     Serial_Generator.State =>+ null);
```

程序的大部分实际上位于 Create_Timestamp 内部。然而，该过程的高度纯净性——它很少引用任何状态——意味着其实现原则上很直接。详情请参阅 GitHub 上的 Thumper 站点（Chapin, 2014）。

## 备选设计

考虑一些备选设计有助于理解我们迄今为止所开发的概念如何应用于它们。首先，考虑网络边界变量包 Network.Socket.Reader 和 Network.Socket.Writer。这两个包分别封装了从网络输入和向网络输出的外部状态抽象。为了进行准确的流分析，对输入和输出使用不同的状态抽象很重要。然而，即使要使用两个抽象，也并非严格需要创建两个单独的包。可以定义具有两个状态抽象的单个包。这种方法可能显得更自然，尤其是考虑到两个状态抽象都使用一个共同的底层套接字。

然而，我们预计 Thumper 的未来版本可能希望存储生成的时间戳以进行审计。这样的更改可以通过将 Network.Socket.Writer 包体替换为另一个也与数据库通信的包体来实现。此更改根本不会影响 Network.Socket.Reader 包。两个单独的包可能看起来有些过度，但它确实清楚地区分了系统的输入和输出，允许更改其中一个而不干扰另一个。

使用变量包来保存密钥和伪随机数生成器状态的做法也可以改变。特别是，可以将 Cryptographic_Services 和 Serial_Generator 转换为类型包，以提供合适的
