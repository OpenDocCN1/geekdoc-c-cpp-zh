
（用于存储数据），它们的所有方式大体都相似，但每种都使用不同的术语：XML 自称为一种“语言”（language），JSON 称为“记法”（notation），而 RDF 称为一种“框架”（framework）。为了避免偏袒，我们将坚持统称它们为“范式”（paradigms）。我们将详细查看每一种，但它们都共享一个共同原则：提供了一种定义良好的、不包含任何应用层语义的语法。这使得可以为每种范式制作稳健的通用解析器，而无需担心像空格和国际字符之类的琐碎细节。除了可以免费获得稳固的词法和语法解析外，使用这些任何一种范式的重要优势在于，它们允许我们构建可扩展的模式和格式。与过去临时和自定义的文件格式不同——在过去，我们不知道第三方是如何实现它们的，因此不知道我们引入的更改是否会破坏他们的软件——有了这些范式，我们假设只要语法是正确的，解析器遇到它不理解的应用数据时将简单地忽略它并继续处理文件的下一个部分，而不会崩溃，也不一定会报告错误。这意味着，只要我们不通过更改结构来破坏之前的模式，就可以轻松地添加新信息，而任何感知不到这些新信息的客户端将像什么都没有发生一样继续工作。随着我们逐一检查，实现这些优势的方法将变得更加清晰。

## JSON

这些范式中最简单的是 JSON，即 JavaScript 简单对象记法（JavaScript Simple Object Notation），尽管它的名称中包含了 JavaScript（这也是该记法在该背景下流行的原因），但大多数现代编程语言都存在 JSON 解析器。JSON 提供了一种表示字符字符串、数字、布尔值、数组（可以被视为列表）和字典（关联两个值的结构）的语法，对于表示程序和数据库中常见的层次级数据结构非常有效。尽管 JSON 对命名空间和元数据没有明确支持，但 JSON 的简单性在于，构建生成或消费 JSON 的系统可以非常快速。

让我们以 PIR 格式表示的蛋白质序列为例。我之前在图 41 中见过它，但为了方便起见，这里再次重复：

```
>P1H_HUMAN
Homog subunit alpha Homo sapiens Gn=HBA1 PE=1 SV=2
MVLSPDKKTNVKAAAGKVHAGGAELERMSLSFFTPKYTFHLRSQVKGHKKKVALTANNAVHDDDMON
ALSDLHHKVRDPNPFKSCLLTYTLLAHVTKTYS
```

记住，PIR 格式以 '>' 开头，因此 'P1' 是一个标记，告诉我们文件的其余部分描述的是蛋白质（而不是核苷酸序列或序列片段），第一行分号后的文本是序列的标识符。诸如人类可读序列描述的行，随后的行包含氨基酸本身的单字母代码，并以星号结束。

## 生物学与计算机科学交叉领域的生物信息挑战

在 JSON 中，我们可以省略大部分语法修饰，因为 '>'、';' 和 '\*' 字符只是为了让解析器区分文件的不同部分。我们真正关心的是：

- 1 这是一个蛋白质
- 2 它的标识符是 HBA_HUMAN
- 3 它有一个人类可读的描述
- 4 它有一个氨基酸序列

在 JSON 语法中，我们可以将其编码为：

```
{
  "type": "protein",
  "identifier": "HBA_HUMAN",
  "description": "Hemoglobin subunit alpha gene=Homo sapiens HBA1 PE=1 SV=2",
  "sequence": "MLVSPDKTNVVKWKGGAHAGEYGAEALERFMSFTTKTYFPHDLSAQVKGHGRKVYDAATNAVVDMPNPALSALHHKRLVDPNFKLLSHCLLTAALAEPTPAVHASSDLDKFLAVSVSTLTKYR"
}
```

尽管在某些方面可能更冗长——但以这种方式编码数据的优势在于无需编写自定义解析器。相反，你只需将数据加载到标准的 JSON 解析器中，然后查询以检索 'type'、'identifier'、'description' 和 'sequence'并以对你的应用程序有意义的方式使用它们。我们在这里创建的是单个 JSON 字典（由顺序 { } 定义），它是 JSON 语法的一部分，包含四个由 ':' 分隔的键值对（type 是键，protein 是值），对应我们想要记录的四个属性中的每一个。我们在这里选择的键完全是任意的，仅对我们的特定应用程序有意义——JSON 解析器不在乎它们是什么，因为它们是用正确的语法表示的。

如果我们想在以后日期扩展我们记录的这种蛋白质的属性数量，只需使用 JSON 语法添加新的键值对即可，非常简单。在此之前构建的工具将继续无缝工作；JSON 解析器会“乐意地”读取新的键值对，但它并没有被设计为这样做。框 7.5 显示了一个更复杂的 JSON 示例，说明了嵌套结构和数组的使用。

## XML

可扩展标记语言（XML）与 JSON 共享一些共同目标，即允许对象及其属性以一种定义良好的语言进行编码，这种语言可以由标准解析器创建和消费。XML 自称为一种“语言”而非“记法”，并且比 JSON 丰富且复杂得多。基于更早且更复杂的标记语言 SGML (Goldfarb, 1990)，XML 提供了一套关于如何编码层次结构数据的高度规则规则。

## 第 7 章 表示含义

## 框 7.5 JSON: JavaScript 简单对象记法

JavaScript 简单对象记法 (JSON) 是一种基于 JavaScript 语言中值表示方式的序列化格式。字符字符串、数字、布尔值、字典（建立两个值之间的关联），因此对名称、来源或元数据没有内置支持。我们需要的一切必须由自己指定，并且必须显式编码在 JSON 本身中。

初看，JSON 似乎过于限制而无法使用，但它是有效的，并且在大多数编程语言中都有很好的支持。因此，构建消费 JSON 的系统可以非常快速；如果数据是简单的，不需要复杂的元数据，这变得几乎轻而易举。

下方的 JSON 片段显示了查询 Europe PubMed Central 返回的 UniProtKB 条目的简单结果，ID 为 2137202 (Dryja et al., 1990) 的文章作为证据支持数据库记录中的声明。方括号 [] 包围的项是键值对。例如，JSON 的顶层是一个包含五个条目的字典，键为 dbCount、dbReferenceList、hitCount、request 和 version。根据 JSON，dbReferenceInfo 包含一个列表，这是一个字典，尽管字典使用的键毫无意义，但我们通过程序获取的 UniProtKB 访问号 (P08100) 被简单地称为 "info"；这使得计算机非常容易地使用这些特定数据（这是 Europe PMC 暴露数据方式的一种遗憾，而不是局限）。

```json
{
  "dbCount": {
    "db": 1,
    "dbName": "UniProtKB"
  },
  "dbReferenceList": {
    "dbReferenceInfo": [
      "dbCount": 1,
      "dbReferenceInfo": [
        "info1": "UniProtKB",
        "info2": "Homo sapiens",
        "info3": "P08100",
        "info4": "UniProtKB"
      ],
      "dbName": "UniProtKB"
    }
  },
  "hitCount": 1,
  "request": {
    "dbCount": 1,
    "dbName": "UniProtKB"
  },
  "version": "1.0"
}
```
