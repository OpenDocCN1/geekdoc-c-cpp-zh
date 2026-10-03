
在 OS X 10.8 到 10.11 上，Apple 的 `NSXMLParser` 在相同文件上的速度为 44 MB/s，这比我们未优化的版本快，并且显著快于之前操作系统版本的 `NSXMLParser` 实现，即使考虑到硬件的改进。然而，实现这种性能提升似乎陷入了缓存的陷阱之一：缓存了（太多）内存。第一个指标是图 4.5 中的顶部输出，显示有 997 MB 的 RPRVT 内存（进程本身使用的非共享脏内存）。运行工具运行堆显示，这个初始评估基本上是正确的，但低了；有 320 MB 的 `NSString` 和 270 MB 的 `NSDictionary`。

![](img/29111a88ed1326b01d04057a653fdbec_110_0.png)

图 4.4 优化的 XML 解析器的性能

| 调用树 | 调用树 | 符号名称 | 库 |
| :--- | :--- | :--- | :--- |
| 1820.0 | 1820.0 | - -[NSObject release] | libobjc.A.dylib |
| 1710.0 | 1370.0 | -malicious_zone_call | |
| 1210.0 | 1210.0 | -[Scanner scan] | libsystem.dylib |
| 1100.0 | 1100.0 | -[NSObject alloc] | libobjc.A.dylib |
| 637.0 | 637.0 | -malloc |.system |
| 511.0 | 511.0 | -[NSData initialize] | Foundation |
| 293.0 | 293.0 | -[NSParser release] | libobjc.A.dylib |
| 268.0 | 268.0 | -[NSString stringWithLength:] | Foundation |
| 195.0 | 195.0 | -[NSString release] | libobjc.A.dylib |
| 168.0 | 168.0 | -[CFString release] | libobjc.A.dylib |
| 132.0 | 132.0 | -[CFRelease] | libobjc.A.dylib |
| 119.0 | 119.0 | -[NSData release] | libobjc.A.dylib |
| 103.0 | 103.0 | -[NSParser release] | Foundation |
| 100.0 | 100.0 | -[NSObject dealloc] | libobjc.A.dylib |
| 95.0 | 95.0 | -[NSString release] | libobjc.A.dylib |
| 87.0 | 87.0 | -anonymous | libobjc.A.dylib |
| 82.0 | 82.0 | -_objc_msgSend | libobjc.A.dylib |
| 85.0 | 85.0 | -class_instantiate | libobjc.A.dylib |
| 76.0 | 76.0 | -small_free_list | libsystem.dylib |
| 72.0 | 72.0 | -malloc | libsystem.dylib |

*图 4.3 未优化 XML 解析器的性能*

![](img/29111a88ed1326b01d04057a653fdbec_108_0)

| PID | COMMAND | %CPU | %TIME | # | RPRVT | SIZE |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 3500 | WebProcess | 0.85 | 00:06:27 | 17 | 140 | 339M |
| 2594 | Terminal | 0.64 | 00:11:59 | 24 | 141 | 131M |
| 275 | SystemUI-Serv | 0.00 | 00:10:31 | 3 | 264 | 550M |
| 3530 | mwshared_data | 0.00 | 00:00:12 | 3 | 63 | 252K |
| 5084 | screencapture | 0.00 | 00:08:03 | 4 | 51 | 592K |
| 6995 | mmfs | 0.00 | 00:08:33 | 3 | 63 | 508 | 3064K |
| 3700 | WebProcess | 0.00 | 00:01:01 | 0 | 181 | 240 | 91M |
| 4514 | VLC | 0.05 | 00:11:04 | 8 | 206 | 539 | 350K |
| 3530 | Post-View | 0.00 | 00:03:58 | 0 | 124 | 155 | 47M |
| 0 | kernel_task | 0.13 | 01:46:27 | 16 | 140 | 234 | 845K |
| 5083 | xml_parse | 100.2 | 00:05:26 | 0 | 254 | 47 | 24M |
| 3530 | TeShop | 0.00 | 00:11:22 | 0 | 241 | 335 | 127M |

*图 4.5 NSXMLParser 解析 291-MB 文件的顶部输出*

## marcel — top — 80x24

进程总数 112，5 个正在运行，3 个阻塞，104 个睡眠，571 个线程

平均负载: 0.63, 0.49, 0.49 CPU 使用率: 25.5%, 2.81%, 71.12% 空闲

共享库: 654M 驻留，278M 数据，0b 链接

内存: 2302M 总计，1727M 私有，567M 共享

物理内存: 1023M 大小，1311M 活跃，555M 不活跃，2889M 已用，1206M 空闲

虚拟内存: 3016 大小，10386M 虚拟，1758770(页)，1062832(进程)

网络: 数据包：938/286576 入，152572/135M 出

磁盘：71/3164 读取，0/12 写入

| PID | 命令 | %CPU | %TIME | 时间 | #Q | RPRT | RSHD | 大小 |
|---|---|---|---|---|---|---|---|---|
| 5968 | screencout | 0.0 | 00:00:02 | 1 | 47 | 95 | 48922 | 35020K |
| 5967 | top | 0.0 | 00:00:01 | 0 | 25 | 30 | 106K | 216K 80B8K |
| 5966 | xlpage-mprw | 0.0 | 00:15:27 | 1 | 55 | 94 | 19206K | 812K 293M |
| 5963 | location | 0.0 | 00:00:00 | 0 | 66 | 75 | 19208K | 3324K 76B2K |
| 5953 | calender | 0.0 | 00:00:47 | 0 | 103 | 149 | 17204K | 6780K 168M |
| 5784 | Preview | 0.0 | 00:00:16 | 2 | 171 | 302 | 146M | 880K 136M |
| 5758 | bash | 0.0 | 00:00:00 | 1 | 21 | 25 | 396K | 972K 1236M |
| 5749 | login | 0.0 | 00:00:00 | 1 | 33 | 67 | 972K | 2726K 4028K |
| 5743 | accountsd | 0.0 | 00:00:05 | 2 | 45 | 66 | 12604K | 3220K | 5348K |
| 5742 | com.apple.Sh | 0.0 | 00:00:18 | 2 | 88 | 11 | 113843K | 53444K | 1M |
| 5737 | pbs | 0.0 | 00:00:16 | 2 | 46 | 56 | 4004K | 15480K | 50A4K |
| 5733 | jpcd | 0.0 | 00:00:00 | 2 | 37 | 64 | 22808K | 34652K |
| 5732 | com.apple.ic | 0.0 | 00:00:24 | 3 | 53 | 65 | 15586K | 34008K | 6552K |
| 5728 | cfprefs | 0.0 | 00:00:29 | 2 | 57- | 10856K - 224K | 15800K |

图 4.6 用于 MWXMLParser 解析 291-MB XML 文件的 top 输出

| 计数 | 字节 | 平均 | 类名 | 类型 | 二进制文件 |
|---|---|---|---|---|---|
| 1035 | 147440 | 142.5 | 非对象 | Obj | MPWFoundation |
| 90 | 4320 | 48.0 | MPFSubData | Obj | libxcpc.dylib |
| 71 | 3408 | 48.0 | _os_kpc_uint64 | Obj | Objective |
| 19 | 3952 | 208.0 | MWXMLAttributes | Obj | XML |

## 调优

虽然捕捉 bug 是一种胜利，但许多小任务也有帮助。例如，在解析期间委托代理保持不变，因此这些高频间隔的消息被发送到 `object-cache`。

用于检查格式良好性的标签堆栈是解析器内部的，并使用 C 数组实现。代表打开标签的对象被缓存起来，以验证实际字符没有被修改或复制；解析器仅产生原始字节的引用，同时也让客户端实际访问数据。这产生了一种“按需付费”的性能结构，在真正需要时才避免了实际工作。

## 优化整个组件：MAX

XML 解析器通常用于从 XML 文件中提取有用数据，这意味着用户代码必须解释解析结果。正如我们看到的，DOM 和 SAX 解析器为开发者带来了一个棘手的权衡：DOM 解析器相当方便，但本质上效率低下，需要将整个 XML 文档解析为内存树表示，在开始应用级处理之前至少需要 6 倍的内存。

另一方面，SAX 解析器可以非常高效，但对于非平凡的任务需要复杂的代码，这些代码难以编写且难以快速。示例 4.9 让我们体验了使用 SAX 解析器的真实感受虽然我们只处理一种特定的 XML 元素类型，但模拟了实际上需要以此方式处理的情况。

示例 4.9 使用 SAX 模拟加载和解析摘要

```objc
@interface MedParser:Object
{
    NSMutableString *content;
    NSMutableArray *abstracts;
}
@property (strong, nonatomic) NSMutableString *content;
@property (strong, nonatomic) NSMutableArray *abstracts;
@end

@implementation MedParser

(void)parser:(NSXMLParser *)parser
    didStartElement:(NSString *)elementName
    namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
    attributes:(NSDictionary *)attributeDict
{
    if ([elementName isEqual:@"Abstract"]) {
        [self setContent:[NSMutableString string]];
    } else {
        [self setContent:nil];
    }
}
@end
```

## 优化整个组件：MAX

```objc
(void)parser:(NSXMLParser *)parser didEndElement:(NSString *)elementName
    namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
{
    if ([elementName isEqual:@"Abstract"]) {
        [abstracts addObject:content];
        [self setContent:nil];
    } else if ([elementName isEqual:@"Acronym"])
    } else if ([elementName isEqual:@"Affiliation"])
    } else if ([elementName isEqual:@"Agency"])
    } else if ([elementName isEqual:@"Article"])
    } else if ([elementName isEqual:@"ArticleTitle"])
    } else if ([elementName isEqual:@"Author"])
    } else if ([elementName isEqual:@"AuthorList"])

(void)parser:(NSXMLParser *)parser foundCharacters:(NSString *)string
{
    [content appendString:string];
}
```

所涉及的 XML 文件是一个 130-MB 的医学期刊数据库。在本文章的“对象，廉价”部分，使用基础 SAX 解析器运行耗时 5.3 秒，使用 `NSXMLParser` 运行也是 5.3 秒。添加示例 4.9 中的客户端代码为两个计时都增加了 1.7 秒，分别将时间变为 3.0 秒和 7.0 秒。当然，1.7 秒仅代表 `NSXMLParser` 运行时间增长了 32%，而对于我们的 SAX 解析器来说增长 130%，这使得即使在使用有限的处理的情况下，我们的高效解析器也被客户端的处理成本所淹没。

原因当然是，SAX API 迫使客户端执行字符串比较和查找，以便为特定的 XML 元素分发正确的操作；正如我们探索过的，使用 `NSString` 和 `CFString` 进行这种操作是昂贵的。通过 instruments 确认了这一假设，但这些字符串比较真的可以消除吗？

XML Messaging API (MAX) 通过利用 Objective-C 运行时和一些调优的对象将字符串比较转换为消息发送。遇到的每个 XML 元素都会转换为一个发送给委托的 `<ElementName:attributes:parser>` 消息。参数是该元素的子元素（已由解析器处理），以及在客户端需要更多信息时的解析器本身。消息预期返回一个代表该元素的对象，然后该对象被作为元素栈上传处理消息的参数。

# 第 4 章 CPU 示例：XML 解析

示例 4.10 显示了与示例 4.9 中 SAX 实现的解析器相同的 MAX 客户端代码`-AbstractTextElement:attributes:parser:` 处理属性并返回空，因为我们没有在构建树，只是获取属性。（与 Cocoa 惯例相反，消息名大写，以精确匹配对应 XML 元素的名称。）没有需要管理累加器，通过添加处理消息来模拟额外负载没有意义，这不会增加开销。注意，类型信息纯粹用于文档目的：由于消息是在运行时合成的，编译器永远不会将源码与方法实现连接，也无法检查返回类型。

## 示例 4.10 使用 MAX 获取摘要

```objc
@interface MedParser:NSObject
{
    NSMutableArray *abstracts;
}
@property (strong, nonatomic) NSMutableArray *abstracts;
@end
```

```objc
@implementation MedParser

-AbstractTextElement:(MPXXMLAttributes *)elements
    attributes:(MPXXMLAttributes *)attrs
    parser:(MPWMAXParser *)parser
{
    id text = [elements combinedText];
    [abstracts addObject:text ? text : @""];
    return nil;
}

@end
```

由于构建（虚拟）树的努力，MAX 在处理 130-MB 数据库文件时比我们的 SAX 解析器慢一点，运行需 1.6 秒，但比 `NSXMLParser` 快了 3 倍。然而，添加实际的客户端代码仅为总处理时间增加了 0.1 秒（或 6%），使总时间达到 1.7 秒。

## MAX 实现

从之前的讨论可以显易见地，在 SAX 之上实现 MAX 至少在效率上是不可能的，事实上 SAX 解析器是

## 总结

而是实现在 MAX 之上。MAX 接收来自示例 4.4 中 XML 扫描器回调的字符输出，并使用一种特殊的 `MPWSmallStringTable` 字典将这些字符串映射到代理消息发送。该字典可以通过 `char const int length` 查找对象，而不需要一个完整的对象或以 UL 终止的 C-String。它所查找的对象是 `MPWFastInvocation` 的实例，它是 `NSInvocation` 的替代方案，通过仅处理对象参数，其速度大约是 `NSInvocation` 的 50 倍。

属性和（子）元素存储在一种特殊的 XML 字典/数组混合结构中，该结构保持了顺序并允许存在多个同名元素（这是 XML 的要求）。属性或元素会被高效地追加到存储区的末尾，并可以通过索引或键进行检索。
