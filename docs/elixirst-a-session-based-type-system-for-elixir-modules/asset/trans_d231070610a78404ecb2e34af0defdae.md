

![](img/21b2a144330b93d666562c91ebc20aff_17_0.png)

图 12. 与 Duelf API 的交互。

仅接受 HTTP 消息（例如 GET 或 POST 请求），因此我们使用一个网关，它充当客户端和第三方服务器之间的中间人。

从 Duelf API 文档中，我们可以获取可进行的 API 调用列表及其详细信息。因此，我们可以推断出调用顺序（即协议），即需要按正确顺序调用以实现我们想要的目标。例如，我们考虑一个搜索并预订航班的客户端。具体来说，客户端需要按正确顺序与多个终端节点交互，包括 !offer_requests、!offers 和 !orders。这种交互顺序在 S_client 协议中被形式化，随后由 ElixirST 用于确保客户端进程遵循该协议，从而安全地（通过将请求转换为 HTTP 消息的网关进程）与 Duelf 服务器交互。

```
S_client = \oplus {
    |request(origin: binary, destination: binary,
    dep_date: binary, class: atom, pass_no: number).S_offers,
    |cancel()
}
S_offers = rec Y.& {
    ?offer(offer_no: number, total_amount: number,
    currency: binary, duration: number,
    stops: number, segments: binary).S_details,
    ?error(binary).S_client
}
S_details = \oplus {
    |more_details().& {
        ?details(...).\oplus {
            |make_booking(...).
            |&(?ok(...), ?error(binary)),
            |cancel()
        },
        ?error(binary)
    },
    |reject().Y
}
```

为清晰起见，S_client 被分为两部分：S_offers 和 S_details。此外，我们为每个负载类型添加标签，以便更清楚地显示需要传输什么数据 - ElixirST 也允许使用标签，前提是标签仅用于装饰目的。我们简要了解一下客户端如何预订航班。交互始于客户端发出请求以获取可用航班（S_client）。浏览 S_client，可以了解客户端需要在请求中包含哪些详细信息，例如出发地和目的地。请注意，我们使用 binary 类型，这是 Elixir 中字符串的类型。然后，客户端开始一次接收（并拒绝）一个报价，直到客户端决定接受某个报价（S_offers）。

要了解航班报价的更多信息，客户端发送请求以获取更多详细信息（例如运营航空公司和更新后的价格），并等待结果（S_details）。收到详细信息后，客户端可以决定取消订单或预订航班。在后一种情况下，预订将在客户端收到确认码后完成。在整个交互过程中，服务器可能会回复错误消息，客户端也需要处理该消息（即 ?error(binary)）。

由 S_client 形式化的此行为应用于模块 FlightSystem，该模块在清单 5 中部分显示。FlightSystem 包含公共函数 client、私有函数 consume_offer 以及一个省略的公共函数 gateway。client 函数使用 ElixirST.session/4 启动会话类型 S_client，然后等待客户端遵循协议（第 4 行）。client 函数随后执行操作：请求报价、接收报价，并调用函数 consume_offer。后者遵循会话类型中的其余操作，即 S_offers。交互的对偶部分，即 gateway 函数，应遵循兼容协议，例如对偶会话类型 S_client。这并未强制执行，因为 gateway 函数超出了第 3.3 节中定义的语法（例如，使用其他模块解析 JSON 响应，或使用动态类型），这些内容未由我们在第 3.4 节中的类型系统定义。该函数也可能无法进行静态分析（例如专有源代码），因此我们假设在运行时它遵守 S_client。尽管如此，我们可以使用我们的 session 函数启动一个会话，同时执行两个公共函数，如下所示：

```
ElixirST.session(@FlightSystem.Client,
    {"MAD", "CDG", "2023-11-24", :economy, 2},
    @FlightSystem.gateway/1,
    [1])
```

9 https://duelf.com/docs/api/overview/welcome.

```elixir
defmodule FlightSystem do
  use ElixirST

  @spec client(pid, binary, binary, binary, atom, number) :: ok
  def client(pid, origin, destination, dep_date, class, pass_no) do
    send(pid, {:request, origin, destination, dep_date, class, pass_no})
    IO.puts("Sending request for a flight from #{origin} to ...")
    IO.puts("Waiting for a response from the server...")
    consume_offer(pid)
  end

  @spec consume_offer(pid) :: atom
  defp consume_offer(pid) do
    receive do
      {:ok, offer_no, total_amount, currency, dur, stops, segments} ->
        IO.puts("Offer #{offer_no}: \n#{currency}#{total_amount}...")
        IO.puts("Accept? (y/n: ")
        case accept? do
          "y" -> send(pid, {:more_details})
            IO.puts("Requesting updated details for offer...")
            send(pid, {:reject})
          _ -> consume_offer(pid)
        end
      {:error, message} -> send(pid, {:cancel})
    end
  end
end
```

清单 5: 用 Elixir 编写的航班系统的会话类型代码片段。

ElixirST 确保函数 client 遵循 S_client 描述的模式，该模式反映了 Duelf 的 API 请求的隐式顺序。例如，如果客户端尝试在发送包含航班详细信息的请求之前进行预订（即跳过第 7 行），则订单将失败；这将由我们的类型系统更早地标记，而不是在运行时被 Duelf 拒绝。

此案例研究表明，ElixirST 足够灵活且实用，可以集成到实际应用程序中。除了静态验证单个函数外，通过明确添加有关交互的信息，我们在源代码本身中提供了文档来源。

在此案例研究中，我们分析了交互的客户端，未对网关进程进行验证，因此容易出现行为问题。要解决此问题，我们可以使用现有技术，例如为未验证部分合成运行时监视器 [21-23]，类似于 Bartolo Burlo 等人 [24] 的工作。

## 7. 相关工作

在本节中，我们将 ElixirST 与其他类型系统和实现进行比较。

### 7.1. Elixir 的类型系统

Cassola 等人 [13,25] 为 Elixir 提出了一种渐进式类型系统。它使用渐进方法静态类型检查 Elixir 模块的函数部分，其中某些术语可能保留未知的表达式类型。与 ElixirST 不同，Cassola 等人直接分析未展开的 Elixir 代码，从而产生更明确的类型检查规则。此外，他们专注于静态类型系统，而未制定操作语义。

另一个 Elixir 的静态类型检查器是 Gradient [26]。它是其 Erlang 对应工具的包装器，并采用与 [13] 类似的方法，其中使用了渐进式类型。另一个项目 Typecheck [27] 为 Elixir 程序添加了动态类型验证。Typecheck 通过在现有函数周围包装检查来执行运行时类型检查。Gradient 和 Typecheck 通过分析对 ElixirST 的调用来实现渐进式类型检查，而讨论的类型检查器 [13, 26,27] 分析了 Elixir 语言的很大一部分，但不检查与进程间消息传递相关的内容。

一些实现旨在检查与消息传递相关的问题。Harrison [28] 静态检查 Core Erlang 中的此类问题。例如，它检测孤儿消息（即永远不会被接收的消息）和不可达的接收分支。在另一项工作中，Christakis 和 Sagonas [29] 分析 Core Erlang 代码以构建通信图，该图描绘了不同进程之间的消息流。随后使用此图来检测类似类型的错误，例如永远不会接收任何消息的接收构造。此工作作为 Dialyzer 的一部分实现。Harrison [30] 扩展了 [28] 以分析 Erlang/OTP 行为（例如 gen_server，它以层次结构方式组织进程），通过注入

