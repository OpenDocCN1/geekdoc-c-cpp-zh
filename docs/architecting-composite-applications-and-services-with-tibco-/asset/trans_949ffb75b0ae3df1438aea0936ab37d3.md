
应易于阅读。满足这一标准的两种常见约定是：

- 非开头大写：字段中除第一个单词外的每个单词以大写字母开头，例如 `ClaimService`（用于类型）或 `claimService`（用于实例）。开头是否大写应由字段引用的是类型还是实例来决定（参见上一节）。
- 所有字母均大写，单词之间使用下划线（_）或其他分隔符，例如 `CLAIM_SERVICE`。这种约定几乎要求使用附加术语来区分类型和实例（参见上一节）。

应避免的一种约定是使用全大写且不允许特殊字符（例如下划线）。这种约定会产生像 CLAIMSERVICE 这样的名称，不仅难以阅读，还可能导致歧义。

## 最佳实践：规划多词字段

采用一种大小写命名约定，确保生成的多词名称易于阅读。

## 为每个接口使用独立的 WSDL 命名空间 URI

为了避免不同接口的消息、端口和操作之间的命名冲突，每个接口都应拥有自己的命名空间 URI。同样重要的是，使用独立的命名空间 URI 使得接口可以独立进行版本控制。这将有助于接口在环境中平滑演进。

## 最佳实践：为每个接口使用唯一的 WSDL 命名空间 URI

在单独的 WSDL 中定义每个接口，并为每个 WSDL 使用唯一的命名空间 URI。

## 纳入接口主版本号

根据第 7 章概述的版本控制最佳实践，在接口名称被纳入某些命名结构的地方，应在这些结构中向接口名称附加接口的 `<major>` 版本号。这会影响以下项目：

- WSDL 命名空间 URL
- 当 schema 专用于特定 WSDL 时的 Schema 命名空间 URL（参见本章后面的“特定于接口和操作的 Schema 类型”一节）
- WSDL 文件名（同时包含接口的 `<minor>` 版本号，按照版本控制最佳实践）
- 当 schema 专用于特定 WSDL 时的 Schema 文件名（同时在文件名中包含接口的 `<minor>` 版本号，按照版本控制最佳实践）
- SOAP 地址（端点）
- SOAP 操作名称

为简单起见，以下章节的示例中省略了版本号。

## 应用命名原则

## 理想化的名称结构

鉴于上文阐述的结构化名称设计原则，命名服务操作的理想化结构形式可能如下：

```
<functionalContext><abstractService><interfaceName>
<operationName>²
```

2. 在 WSDL 中，操作名称的作用域是 portType（WSDL 1.1）或 interface（WSDL 2.0）。

实际上，enterpriseID 几乎总是使用互联网域名来定义。例如，

```
nouveau.com
```

大多数情况下，企业 ID 出现在 URL 或 URI 上下文中，其形式为

```
http://nouveau.com
```

许多企业拥有不止一条业务线，每条业务线基本上都作为独立公司运营（尤其从 IT 角度来看）。在这种情况下，最佳实践是将业务线作为 `<functionalContext>` 的一部分。这有助于避免同一公司不同业务线中相似功能领域（例如销售、人力资源、财务）之间的名称冲突。结果如下：

```
<functionalContext> ::= <enterpriseID><lineOfBusiness>
<functionalArea>
```

以 Nouveau Health Care 为例，它可能拥有两条截然不同的业务线。一条是保险提供商，另一条是在线药店。那么 Nouveau 的理想化企业标识符将是

```
com.nouveau.insurance
com.nouveau.pharmacy
```

在将理想化形式转换为 URL 或 URI 所需形式时，你有两种选择，取决于你是否希望业务线名称成为互联网域名或路径的一部分。如果你希望它成为互联网域名的一部分，最终会得到

```
http://insurance.nouveau.com
http://pharmacy.nouveau.com
```

如果你希望业务线成为路径的一部分，最终会得到

```
http://nouveau.com/insurance
http://nouveau.com/pharmacy
```

实际上，这可能并非随意选择：将业务线作为互联网域名的一部分，允许使用不同的机器作为不同业务线的目标；而将业务线作为路径的一部分，则迫使同一台机器用作两条业务线的入口点。这可能涉及组织和管理问题。这些将在本章后面的“复杂现实”一节中讨论。

为了应对这种情况，许多企业采用网络设备，可以在两种格式之间进行无缝转换。虽然这增加了灵活性，但需要网络配置——这又是一项管理任务。

## 最佳实践：全局唯一性

在功能上下文中加入企业特定的限定符。如果企业有独立的业务线，也应将业务线包含在功能上下文中。

## 互联网域名的符号约定

关于理想化名称中有多少将成为互联网域名的一部分，这个问题经常出现，因此我们将采用一种约定来表示答案：理想化结构中将成为互联网域名部分的部分将用边框标出。使用此约定，业务线名称作为互联网域名一部分的示例将理想化为

```
<enterpriseID><lineOfBusiness><functionalArea>
```

业务线名称作为路径一部分的示例将理想化为

```
<enterpriseID><lineOfBusiness><functionalArea>
```

## WSDL 和 XSD 命名空间 URI

WSDL 命名空间 URI 的理想化结构形式如下：

```
<functionalContext><abstractService><abstractInterface>wsdl
<wsdlName>
```

展开功能上下文，我们得到

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<abstractInterface>wsdl<wsdlName>
```

通常的做法是将实际名称结构设置为 URI。对于 Payment Manager 服务的 Claim Payment 接口 WSDL，并在名称中包含主版本号，这得到

```
http://insurance.nouveau.com/finance/paymentManager/
claimPayment/wsdl/claimPayment1
```

Schema 命名空间 URI 的理想化结构形式如下：

```
<functionalContext><abstractService><abstractInterface>schema
<schemaName>
```

展开功能上下文，我们得到

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<abstractInterface>schema<schemaName>
```

通常的做法是将实际名称结构设置为 URI。对于与 Claim Payment WSDL 关联的 Claim Payment schema，并在名称中包含 schema 主版本号，这得到

```
http://insurance.nouveau.com/finance/paymentManager/
claimPayment/schema/claimPayment1
```

## 最佳实践：WSDL 和 Schema 命名空间 URI

在 WSDL 和 schema 命名空间 URI 中包含完整的功能上下文、抽象服务名称、抽象接口名称以及 WSDL 或 schema 名称。在 WSDL 或 schema 名称之前插入 wsdl 或 schema，以区分 WSDL 和 schema 命名空间。

## WSDL 和 XSD 文件名

最佳实践是使用 WSDL 或 schema 命名空间结构作为定义文件名（即文件路径）结构的基础。其思想是使完全限定的文件名成为 URL（或至少是 URI）。使其成为 URL 可以告诉你文件的位置。采用这种方法，文件名的理想化结构如下：

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService
<abstractInterface>wsdl<filename>
<enterpriseID><lineOfBusiness><functionalArea><abstractService
<abstractInterface>schema<filename>
```
