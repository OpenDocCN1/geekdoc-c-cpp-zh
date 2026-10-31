

## 名称结构定义搜索策略

在 SOA 中，名称的结构不仅标识被命名的项，而且通常指示如何找到该项。当人们查找某个工件时，往往一开始只有一个模糊的概念。虽然索引和关键字关联可能有所帮助，但名称的结构隐含地定义了定位项目的搜索策略。例如，考虑 Nouveau Health Care 支付管理器的索赔支付接口，其 WSDL 可能具有如下 URL：

```
http://insurance.nouveau.com/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl
```

这个名称不仅唯一标识了 WSDL 文件，还告诉我们在哪里找到它：前往 `insurance.nouveau.com` 指定的机器（默认端口 80），在 `finance/paymentManager/claimPayment/wsdl` 目录中查找，并获取 `claimPayment.wsdl` 文件。

## 名称结构定义路由策略

虽然端口（端点）并非正式属于 Web 服务范式的一部分，但它们通常利用名称将服务请求导向实际的服务提供者。接受服务请求的组件（通常也是机器）往往不同于实际处理这些请求的组件。恰当的命名可以帮助接收组件将请求路由到提供者。

例如，端口（端点）地址（服务请求所指向的地址）由 URI 指定，URI 是名称的一种形式。考虑 Nouveau Health Care 的索赔支付接口地址，如下所示：

```
https://insurance.nouveau.com:443/finance/paymentManager/claimPayment
```

再考虑索赔提交接口的地址，如下所示：

```
https://insurance.nouveau.com:443/claims/claimRouter/claimSubmission
```

两种请求所指向的实际组件由地址 URI 的第一部分指定，即域名和端口（不要与 WSDL 中的端口概念混淆）：

```
https://insurance.nouveau.com:443
```

这表示请求被接收到 `insurance.nouveau.com` 所指定机器的 443 端口。如果这些请求需要由另一个组件处理，则必须将它们路由到实际的服务提供者。地址中位于 Internet 域名和端口号下方的 URI 路径结构，使得可以根据该路径对到达 443 端口的请求进行路由。或者，可以忽略此信息，将所有请求路由到一个公共目的地，该目的地为共享该域名和端口的所有 Web 服务提供支持。

相比之下，两个地址也可以都写成：

```
https://insurance.nouveau.com:443
```

在这种情况下，由于路径不存在，就没有可用于路由请求的信息。

当然，使用地址结构并不是唯一的路由方式。其他信息，如 `soapAction`、WSDL 命名空间 URI 的结构以及其下的端口/操作命名结构，也可以用于路由。无论使用哪些名称，这些名称的结构以及该结构使用的一致性都能极大地简化服务请求的路由。

## 哪些东西需要命名？

在 SOA 环境中，有许多东西需要命名。这些包括：

-   WSDL 相关名称：
    -   WSDL 本身（顶层 `<definitions>` 标签中的 `name` 属性）。
    -   WSDL 文件名。
    -   WSDL 定义的 `targetNamespace`（同样位于顶层 `<definitions>` 标签中）。该名称是一个 URI，是 WSDL 中定义的每个实体名称的逻辑前缀。
    -   WSDL 定义的实体：服务、端口类型（接口）、操作、消息、绑定和端口（端点）。
    -   `soapAction`。
    -   每个导入的 XSD 文件的 `schemaLocation`。
    -   每个服务端口（端点）的地址。
-   Schema 相关名称：
    -   XSD 文件名（如果 schema 未嵌入 WSDL 中）。
    -   schema 定义的 `targetNamespace`（无论是嵌入在 WSDL 中还是独立的 XSD）。该名称是一个 URI，是 schema 中定义的每个实体名称的逻辑前缀。
    -   schema 定义的实体：类型、元素和属性。
    -   每个导入的 XSD 文件的 `schemaLocation`。
-   JMS 相关名称：
    -   静态目标（主题或队列）名称
    -   EMS 服务器名称
-   SCA 相关名称：
    -   复合名称
    -   组件类型名称
    -   服务名称

其中一些项是实际的工件，例如文件。其他项则只是定义（端口类型、消息、元素等）或定义组（命名空间 URI）的逻辑名称。服务的生产者和消费者都必须处理所有这些名称。这些名称及其定义标准是本章的重点。

## 结构化名称设计原则

### 采用从一般到具体的结构

结构化名称（想想 `www.nouveau.com`）是树状的。树的根代表整棵树。下面的每个节点代表以该节点为根的子树。Internet 的根（`com` 的父级）没有显式命名，但 Internet 命名系统中的下一层（称为顶级域）由 `.com`、`.net`、`.org` 和 `.edu` 等节点组成。在每个这样的域内，还有子域，其名称仅在父域的上下文中才有意义。因此，为了唯一性，你会使用 `nouveau.com` 而不是仅仅使用 `nouveau`（后者在 `.com`、`.net`、`.org` 等中具有不同的含义）。

由于固有的树状结构，你所定义的结构逻辑必须围绕真实的层级关系来组织，这一点很重要。服务层级结构的轮廓源于前面概念讨论中对服务的描述。从抽象概念的讨论中，我们得到：

```
<functionalContext><abstractService><abstractInterface>
```

这是一种从一般到具体的结构。一个功能上下文可以包含多个服务，每个服务可以包含多个接口。反过来，服务特定于某个功能上下文，每个接口特定于某个服务。

理想情况下，实际层级结构以从左到右、从最一般到最具体的统一字段序列来表示。这就是你在 Java 类命名中看到的模式：

```
com.nouveau.insurance.finance.paymentManager.claimPayment.payClaim
```

这里，`com.nouveau.insurance.finance` 代表功能上下文。抽象服务由 `paymentManager` 表示。抽象接口由 `claimPayment.payClaim` 表示，即用于支付索赔的接口和操作。请注意，功能上下文内部和接口内部都存在层级结构。

遗憾的是，SOA 世界中的许多名称必须采用 URI 或 URL 形式。这些包括命名空间名称以及 WSDL/SOAP 地址和 `soapAction` 字段。URI 的结构化方案并不严格遵循统一原则。每个 URI 或 URL 实际上包含两个名称层级结构，每个结构都有不同的构造规则。考虑前面的示例：

```
http://insurance.nouveau.com/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl
```

这个字符串包含三个部分，涉及两种不同的名称结构：

1.  `http://`，第一部分，表示用于访问该工件的协议。从名称结构的角度来看，我们可以忽略它。
2.  `insurance.nouveau.com`，第二部分，是一个 Internet 域名，指定 Internet 上的一台机器。在 Internet 域名中，层级结构是从右向左读取的。
3.  `/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl`，第三部分，称为路径。它表示 Internet 域名所指定机器本地的名称层级结构。路径名称层级结构是从左向右读取的。

使两种不同名称层级结构及其从右向左和从左向右读取的差异变得无歧义的，是使用了两种不同的字段分隔符。Internet 域名命名空间的字段以句点（`.`）分隔，而本地命名空间的字段以正斜杠（`/`）分隔。Internet 域名右侧出现的第一个斜杠是提示你已切换命名层级结构的线索。

如果你想让这个命名空间统一，完全从左向右读取，就必须交换 Internet 命名空间元素的顺序：

```
com.nouveau.insurance.finance.paymentManager.claimPayment.wsdl.claimPayment.wsdl
```

这当然就是用于命名 Java 类的那类结构。

### 最佳实践：从一般到具体的结构

当名称的结构尚未受到约束时，请按照以下模式为名称建立统一的从左到右、从一般到具体的层级结构：

```
<functionalContext><abstractService><abstractInterface>
```

当名称的结构受到部分约束时（例如 URL 和 URI），请将此原则应用于名称的较低层级结构（即 URL 或 URI 中的路径）。

### 采用层级命名机构

名称要有用，必须是唯一的。唯一性要求某种机构跟踪已分配的名称，以确保新发布的名称不会重复。遗憾的是，由单一机构来跟踪所有名称是不切实际的，尤其是对于具有全局范围的名称。

为解决这个问题而演化出的（在许多地方出现的）系统涉及使用层级机构。该策略包含两个要素。第一个是标准化的句法结构，用于将名称定义为字段序列。Internet 域名结构（例如 `insurance.nouveau.com`）就是一个例子。

