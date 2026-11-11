

## 6.7 与遗留代码互操作

作为一项全新的成果，Java 日期和时间 API 必须与现有类互操作——特别是无处不在的 `java.util.Date`、`java.util.GregorianCalendar` 以及 `java.sql.Date/Time/Timestamp`。

`Instant` 类与 `java.util.Date` 非常相似。在 Java SE 8 中，该类新增了两个方法：将 `Date` 转换为 `Instant` 的 `toInstant` 方法，以及进行反方向转换的静态 `from` 方法。

类似地，`ZonedDateTime` 与 `java.util.GregorianCalendar` 非常相似，并且该类在 Java SE 8 中获得了转换方法。`toZonedDateTime` 方法将 `GregorianCalendar` 转换为 `ZonedDateTime`，而静态 `from` 方法进行相反的转换。

`java.sql` 包中的日期和时间类还提供了另一组转换。你还可以将日期/时间格式化器传递给使用 `java.text.Format` 的遗留代码。表 6.9 总结了这些转换。

**表 6.9** `java.time` 类与遗留类之间的转换

| 类 | 转换为遗留类 | 从遗留类转换 |
|---|---|---|
| `Instant` ↔ `java.util.Date` | `Date.from(instant)` | `date.toInstant()` |
| `ZonedDateTime` ↔ `java.util.GregorianCalendar` | `GregorianCalendar.from(zonedDateTime)` | `cal.toZonedDateTime()` |
| `Instant` ↔ `java.sql.Timestamp` | `Timestamp.from(instant)` | `timestamp.toInstant()` |
| `LocalDateTime` ↔ `java.sql.Timestamp` | `Timestamp.valueOf(localDateTime)` | `timestamp.toLocalDateTime()` |
| `LocalDate` ↔ `java.sql.Date` | `Date.valueOf(localDate)` | `date.toLocalDate()` |
| `LocalTime` ↔ `java.sql.Time` | `Time.valueOf(localTime)` | `time.toLocalTime()` |
| `DateTimeFormatter` → `java.text.DateFormat` | `formatter.toFormat()` | 无 |
| `java.util.TimeZone` → `ZoneId` | `TimeZone.getTimeZone(id)` | `timeZone.toZoneId()` |
| `java.nio.file.attribute.FileTime` → `Instant` | `FileTime.from(instant)` | `fileTime.toInstant()` |

你现在已经知道如何使用 Java 8 日期和时间库处理世界各地的日期和时间值。下一章将进一步讨论面向国际受众的编程。你将看到如何以对客户有意义的方式格式化程序消息、数字和货币，无论他们身在何处。

## 第 7 章 国际化

### 本章内容

- 7.1 区域设置，第 372 页
- 7.2 数字格式，第 378 页
- 7.3 货币，第 384 页
- 7.4 日期和时间，第 385 页
- 7.5 排序与规范化，第 393 页
- 7.6 消息格式化，第 400 页
- 7.7 文本输入与输出，第 404 页
- 7.8 资源包，第 408 页
- 7.9 一个完整示例，第 413 页

外面是一个广阔的世界；我们希望其中许多居民会对你的软件感兴趣。毕竟，互联网毫不费力地跨越了国家之间的障碍。另一方面，当你完全不关注国际受众时，你就是在设置障碍。

Java 编程语言是第一种从底层开始设计以支持国际化的语言。从一开始，它就具备有效国际化所需的一项基本特性：所有字符串都使用 Unicode。Unicode 支持使编写 Java 程序变得容易，这些程序可以操纵多种语言中任意一种语言的字符串，以面向德国用户。当然，如果月份名称明确写出来，语言之间的差异就会变得明显。英文的 March 22, 1961 应表示为德语的 22. März 1961，或中文的 1961 年 3 月 22 日。

有多个格式化器类会考虑这些差异。要控制格式化，请使用 Locale 类。区域设置最多由五个组成部分构成：

- 1. 语言，由两个或三个小写字母指定，例如 `en`（英语）、`de`（德语）或 `zh`（中文）。表 7.1 列出了常见代码。
- 2. 可选地，一个文字系统，由四个字母指定，首字母大写，例如 Latn（拉丁文）、Cyrl（西里尔文）或 Hant（繁体汉字）。这很有用，因为某些语言（如塞尔维亚语）用拉丁字母或西里尔字母书写，而一些中文读者更喜欢繁体字而非简体字。
- 3. 可选地，一个国家或地区，由两个大写字母或三位数字指定，例如 US（美国）或 CH（瑞士）。表 7.2 列出了常见代码。
- 4. 可选地，一个变体，指定方言或拼写规则等杂项特性。变体现在很少使用。挪威语曾有一个“新挪威语”变体，但现在用不同的语言代码 nn 表示。过去用于日本皇历和泰语数字的变体现在表示为扩展（见下一项）。
- 5. 可选地，一个扩展。扩展描述本地偏好，例如日历（如日本历）、数字（泰语数字而非西方数字）等。Unicode 标准规定了其中一些扩展。扩展以 u- 开头，并跟一个两字母代码，指定该扩展涉及日历（ca）、数字（nu）等。例如，扩展 u-nu-thai 表示使用泰语数字。其他扩展完全任意，以 x- 开头，例如 x-java。

区域设置的规则在互联网工程任务组（Internet Engineering Task Force）的“最佳当前实践”备忘录 BCP 47（http://tools.ietf.org/html/bcp47）中制定。你可以在 www.w3.org/International/articles/language-tags 找到更通俗的摘要。

### 表 7.1 常见 ISO 639-1 语言代码

| 语言 | 代码 | 语言 | 代码 |
|---|---|---|---|
| 中文 | zh | 意大利语 | it |
| 丹麦语 | da | 日语 | ja |
| 荷兰语 | nl | 韩语 | ko |
| 英语 | en | 挪威语 | no |
| 法语 | fr | 葡萄牙语 | pt |
| 芬兰语 | fi | 西班牙语 | es |
| 德语 | de | 瑞典语 | sv |
| 希腊语 | el | 土耳其语 | tr |

### 表 7.2 常见 ISO 3166-1 国家代码

| 国家 | 代码 | 国家 | 代码 |
|---|---|---|---|
| 奥地利 | AT | 日本 | JP |
| 比利时 | BE | 韩国 | KR |
| 加拿大 | CA | 荷兰 | NL |
| 中国 | CN | 挪威 | NO |
| 丹麦 | DK | 葡萄牙 | PT |
| 芬兰 | FI | 西班牙 | ES |
| 德国 | DE | 瑞典 | SE |
| 英国 | GB | 瑞士 | CH |
| 希腊 | GR | 台湾 | TW |
| 爱尔兰 | IE | 土耳其 | TR |
| 意大利 | IT | 美国 | US |

语言和国家代码看起来有点随机，因为其中一些源自当地语言。德语中的“德语”是 Deutsch，中文中的“中文”是 zhongwen：因此有 de 和 zh。而瑞士是 CH，源自拉丁语术语 *Confoederatio Helvetica*，意为瑞士联邦。

区域设置由标签描述——即由区域设置元素组成的连字符串，例如 en-US。

在德国，你会使用区域设置 de-DE。瑞士有四种官方语言（德语、法语、意大利语和罗曼什语）。在瑞士的德语使用者会希望使用区域设置 de-CH。该区域设置使用德语的规则，但货币值用瑞士法郎表示，而不是欧元。

如果只指定语言（例如 de），那么该区域设置不能用于货币等国家/地区特定问题。

你可以像这样从标签字符串构造 Locale 对象：

```
Locale usEnglish = Locale.forLanguageTag("en-US");
```

`toLanguageTag` 方法生成给定区域设置的语言标签。例如，`Locale.US.toLanguageTag()` 是字符串 "en-US"。

为方便起见，针对各个国家/地区预定义了区域设置对象：

- Locale.CANADA
- Locale.CANADA_FRENCH
- Locale.CHINA
- Locale.FRANCE
- Locale.GERMANY
- Locale.ITALY
- Locale.JAPAN
- Locale.KOREA
- Locale.PRC
- Locale.TAIWAN
- Locale.UK
- Locale.US

一些预定义区域设置只指定语言而不指定位置：

- Locale.CHINESE
- Locale.ENGLISH
- Locale.FRENCH
- Locale.GERMAN
- Locale.ITALIAN
- Locale.JAPANESE
- Locale.KOREAN
- Locale.SIMPLIFIED_CHINESE
- Locale.TRADITIONAL_CHINESE

最后，静态方法 getAvailableLocales 返回虚拟机已知的所有区域设置组成的数组。

