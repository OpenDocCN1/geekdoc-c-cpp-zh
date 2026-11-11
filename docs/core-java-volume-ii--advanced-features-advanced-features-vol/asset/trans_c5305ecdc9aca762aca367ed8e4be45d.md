
| java.util.Scanner 5.0 |
| --- |
| - `Stream<MatchResult> findAll(Pattern pattern)` 9<br>生成一个流，包含该扫描器产生的输入中给定模式的所有匹配项。 |

现在你已经了解了如何在 Java 中执行输入和输出操作，并概览了作为“新 I/O”规范一部分的正则表达式包。下一章，我们将转向 XML 数据的处理。

*本页有意留白*

本章介绍 XML，并涵盖 Java 库的 XML 特性。一如既往，我们会在此过程中指出何时使用 XML 是合理的——以及何时你必须有所保留，并尝试用老办法解决问题：通过良好的设计和代码。

### 3.1 XML 简介

在第一卷第 13 章中，你已经看到了使用*属性文件*来描述程序配置的方法。属性文件包含一组名称/值对，例如

```
fontname=Times Roman
fontsize=12
windowsize=400 200
color=# 50 100
```

你可以使用 `Properties` 类通过一次方法调用读取这样的文件。这是一个不错的功能，但它还远远不够。在许多情况下，你想要描述的信息比属性文件格式能够轻松处理的结构更复杂。考虑示例中的 *字体名称*/*字体大小* 条目。更面向对象的做法是使用单个条目：

```
font=Times Roman 12
```

但这样一来，解析字体描述就变得很麻烦，因为你必须弄清楚字体名称在哪里结束、字体大小从哪里开始。

属性文件只有单一的扁平层级结构。你经常能看到程序员通过如下键名来绕过这一限制：

```
title.fontname=Helvetica
title.fontsize=36
body.fontname=Times Roman
body.fontsize=12
```

属性文件格式的另一个缺点是键必须唯一。要存储一系列值，你需要另一种变通方法，例如

```
menu.item.1=Times Roman
menu.item.2=Helvetica
menu.item.3=Goudy Old Style
```

XML 格式解决了这些问题。它可以表达层次结构，因此比属性文件的扁平表结构更灵活。

用于描述程序配置的 XML 文件可能如下所示：

```xml
<config>
    <entry id="title">
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </entry>
    <entry id="body">
        <font>
            <name>Times Roman</name>
            <size>12</size>
        </font>
    </entry>
    <entry id="background">
        <color>
            <red>0</red>
            <green>50</green>
            <blue>100</blue>
        </color>
    </entry>
</config>
```

XML 格式允许你表达层次结构并记录重复元素，而无需扭曲形式。

XML 文件的格式很直观。它看起来类似于 HTML 文件。这是有充分理由的——XML 和 HTML 都是古老的标准通用标记语言（SGML）的后代。

SGML 自 20 世纪 70 年代以来一直用于描述复杂文档的结构。它在一些需要持续维护大量文档的行业中得到了成功应用——尤其是飞机制造业。然而，SGML 相当复杂，因此从未大规模流行起来。这种复杂性很大程度上源于 SGML 有两个相互冲突的目标。SGML 希望确保文档按照其文档类型的规则形成，但它也希望通过允许减少输入量的快捷方式来使数据录入变得容易。XML 被设计为 SGML 的简化版本，以便在互联网上使用。正如通常情况那样，越简单越好，XML 立即受到了热烈欢迎，而这是 SGML 长期以来未能获得的。

> **注意：** 你可以在 www.xml.com/axml/axml.html 找到一个非常好的 XML 标准版本，其中带有 Tim Bray 的注释。

尽管 XML 和 HTML 有共同的根源，但两者之间存在重要差异。

- 与 HTML 不同，XML 区分大小写。例如，`<H1>` 和 `<h1>` 是不同的 XML 标签。
- 在 HTML 中，如果从上下文中可以清楚看出段落或列表项在哪里结束，你可以省略结束标签，例如 `</p>` 或 `</li>`。在 XML 中，你绝不能省略结束标签。
- 在 XML 中，只有单个标签而没有匹配结束标签的元素必须以 `/` 结尾，例如 `<img src="coffeecup.png"/>`。这样，解析器就知道不必寻找 `</img>` 标签。
- 在 XML 中，属性值必须用引号括起来。在 HTML 中，引号是可选的。例如，`<applet code="MyApplet.class" width=300 height=300>` 是合法的 HTML，但不是合法的 XML。在 XML 中，必须使用引号：`width="300"`。
- 在 HTML 中，属性可以没有值，例如 `<input type="radio" name="language" value="Java" checked>`。在 XML 中，所有属性都必须有值，例如 `checked="true"` 或（唉）`checked="checked"`。
- 对于 HTML 版本 4 和 5，存在称为 XHTML 的 XML 表述。

### 3.2 XML 文档的结构

XML 文档应以如下头部开始

```xml
<?xml version="1.0"?>
```

或

```xml
<?xml version="1.0" encoding="UTF-8"?>
```

严格来说，头部是可选的，但强烈建议使用。

> **注意：** 由于 SGML 是为处理真实文档而创建的，因此 XML 文件被称为文档，尽管其中许多描述的是通常不会被称为文档的数据集。

头部之后可以跟一个*文档类型定义*（DTD），例如

```
<!DOCTYPE web-app PUBLIC
  "-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
  "http://java.sun.com/j2ee/dtds/web-app_2_2.dtd">
```

DTD 是确保文档正确性的重要机制，但并非必需。我们将在本章后面讨论它们。

最后，XML 文档的正文包含*根元素*，它可以包含其他元素。例如，

```xml
<?xml version="1.0"?>
<!DOCTYPE config ...>
<config>
    <entry id="title">
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </entry>
    ...
</config>
```

一个元素可以包含*子元素*、文本，或两者兼有。在前面的示例中，font 元素有两个子元素：name 和 size。name 元素包含文本 "Helvetica"。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_179_0.png)

> **提示：** 最好将 XML 文档结构化为一个元素要么包含子元素，要么包含文本。以下是你应避免的示例：

```xml
<font>
    Helvetica
    <size>36</size>
</font>
```

这在 XML 规范中称为*混合内容*。正如你将在本章后面看到的，如果避免混合内容，可以简化解析。

XML 元素可以包含属性，例如

```xml
<size unit="pt">36</size>
```

XML 设计者对于何时使用元素、何时使用属性存在一些分歧。例如，将字体描述为

```xml
<font name="Helvetica" size="36"/>
```

似乎比

```xml
<font>
    <name>Helvetica</name>
    <size>36</size>
</font>
```

更容易。然而，属性的灵活性要差得多。假设你想为大小值添加单位。如果使用属性，就必须将单位添加到属性值中：

```xml
<font name="Helvetica" size="36 pt"/>
```

唉！现在你必须解析字符串 "36 pt"，这正是 XML 旨在避免的那种麻烦。向 size 元素添加属性要干净得多：

```xml
<font>
  <name>Helvetica</name>
  <size units="pt">36</size>
</font>
```

一个常用的经验法则是，属性只应用于修改值的解释，而不是用于指定值。如果你发现自己陷入一场形而上学式的讨论：某个特定设置是否是对值解释的修改，那就直接对属性说“不”，全程使用元素。许多有用的 XML 文档根本不使用属性。

> **注意：** 在 HTML 中，属性使用规则很简单：如果它不显示在网页上，它就是属性。例如，考虑超链接
>
>     <a href="http://java.sun.com">Java Technology</a>
>
> 字符串 Java Technology 会显示在网页上，但链接的 URL 不是显示页面的一部分。然而，这条规则对大多数 XML 文件并没有那么有帮助，因为 XML 文件中的数据通常不是供人查看的。

元素和文本是 XML 文档的“面包和黄油”。以下是你可能遇到的其他一些标记指令：

- *字符引用*的形式为 `&#decimalValue;` 或 `&#xhexValue;`。例如，é 字符可以用以下任一形式表示：

  ```
  &#233; &#xE9;
  ```

- *实体引用*的形式为 `&name;`。实体引用

  ```
  &lt; &gt; &amp; &quot; &apos;
  ```

  具有预定义含义：小于号、大于号、与号、引号和撇号字符。你可以在 DTD 中定义其他实体引用。

