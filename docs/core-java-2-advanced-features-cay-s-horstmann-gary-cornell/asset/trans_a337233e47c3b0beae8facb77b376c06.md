
在 Java 平台上生成 XSL 转换很简单。为每个样式表设置一个转换器工厂。然后，获取一个转换器对象，并告诉它将源转换为结果：

```java
File styleSheet = new File(filename);
StreamSource styleSource = new StreamSource(styleSheet);
Transformer t = TransformerFactory.newInstance().newTransformer(styleSource);
t.transform(source, result);
```

transform 方法的参数是实现了 `Source` 和 `Result` 接口的类的对象。有几个类实现了 `Source` 接口：

- DOMSource
- SAXSource
- StreamSource

可以从文件、流、读取器或 URL 构造 `StreamSource`，并从 DOM 树的节点构造 `DOMSource`。例如，在上一节中，我们按如下方式调用了恒等转换：

```java
t.transform(new DOMSource(doc), result);
```

在我们的示例程序中，我们做了稍微更有趣的事情。我们不从现有的 XML 文件开始，而是生成一个 SAX XML 读取器，它通过发出适当的 SAX 事件来造成正在解析 XML 文件的假象。实际上，我们的 XML 读取器读取的是一个平面文件，如第 2 章所述。输入文件如下所示：

```
Carl Cracker|75000.0|1987|12|15
Harry Hacker|50000.0|1989|10|1
Tony Tester|40000.0|1990|3|15
```

我们的 XML 读取器在处理输入时生成 SAX 事件。下面是实现了 `XMLReader` 接口的 `EmployeeReader` 类的 `parse` 方法的一部分：

```java
AttributesImpl attributes = new AttributesImpl();
handler.startDocument();
handler.startElement("", "staff", "staff", attributes);
while ((line = in.readLine()) != null)
{
    handler.startElement("", "employee", "employee", attributes);
    StringTokenizer t = new StringTokenizer(line, "|");
    handler.startElement("", "name", "name", attributes);
    String s = t.nextToken();
    handler.characters(s.toCharArray(), 0, s.length());
    handler.endElement("", "name", "name");
    . . .
    handler.endElement("", "employee", "employee");
}
handler.endElement("", rootElement, rootElement);
handler.endDocument();
```

转换器的 `SAXSource` 从该 XML 读取器构造：

```java
t.transform(new SAXSource(new EmployeeReader()),
            new InputSource(new FileInputStream(filename)), result);
```

这是将非 XML 遗留数据转换为 XML 的一种巧妙技巧。当然，大多数 XSLT 应用程序已经拥有 XML 输入数据，你可以直接在 `StreamSource` 上调用 `transform` 方法：

```java
t.transform(new StreamSource(file), result);
```

转换结果是实现了 `Result` 接口的类的对象。Java 库提供了三个类：

- DOMResult
- SAXResult
- StreamResult

要将结果存储到 DOM 树中，请使用 `DocumentBuilder` 生成一个新的文档节点，并将其包装到 `DOMResult` 中：

```java
Document doc = builder.newDocument();
t.transform(new DOMResult(doc));
```

要将输出保存到文件中，请使用 `StreamResult`：

```java
t.transform(source, new StreamResult(file));
```

清单 3.15 包含完整的源代码。

### 清单 3.13 transform/makehtml.xsl

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

    <xsl:output method="html"/>

    <xsl:template match="/staff">
        <table border="1"><xsl:apply-templates/></table>
    </xsl:template>

    <xsl:template match="/staff/employee">
        <tr><xsl:apply-templates/></tr>
    </xsl:template>

    <xsl:template match="/staff/employee/name">
        <td><xsl:apply-templates/></td>
    </xsl:template>

    <xsl:template match="/staff/employee/salary">
        <td><xsl:apply-templates/></td>
    </xsl:template>

    <xsl:template match="/staff/employee/hiredate">
        <td><xsl:value-of select="@year"/>-<xsl:value-of
            select="@month"/>-<xsl:value-of select="@day"/></td>
    </xsl:template>

</xsl:stylesheet>
```

### 清单 3.14 transform/makereport.xsl

```xml
<?xml version="1.0"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

    <xsl:output method="text" omit-xml-declaration="yes"/>

    <xsl:template match="/staff/employee">
        employee:<xsl:value-of select="position()"
        />/name:<xsl:value-of select="name/text()"/>
        employee:<xsl:value-of select="position()"
        />/salary:<xsl:value-of select="salary/text()"/>
        employee:<xsl:value-of select="position()"
        />/hiredate:<xsl:value-of select="hiredate/@year"
        />-<xsl:value-of select="hiredate/@month"
        />-<xsl:value-of select="hiredate/@day"/>
    </xsl:template>

</xsl:stylesheet>
```

### 清单 3.15 transform/TransformTest.java

```java
package transform;

import java.io.*;
import java.nio.file.*;
import java.util.*;
```

```java
99    public ContentHandler getContentHandler()
100   {
101       return handler;
102   }
103
104   // the following methods are just do-nothing implementations
105   public void parse(String systemId) throws IOException, SAXException {}
106   public void setErrorHandler(ErrorHandler handler) {}
107   public ErrorHandler getErrorHandler() { return null; }
108   public void setDTDHandler(DTDHandler handler) {}
109   public DTDHandler getDTDHandler() { return null; }
110   public void setEntityResolver(EntityResolver resolver) {}
111   public EntityResolver getEntityResolver() { return null; }
112   public void setProperty(String name, Object value) {}
113   public Object getProperty(String name) { return null; }
114   public void setFeature(String name, boolean value) {}
115   public boolean getFeature(String name) { return false; }
116 }
```

- **javax.xml.transform.TransformerFactory 1.4**
  - `Transformer newTransformer(Source styleSheet)`  
    返回 `Transformer` 类的一个实例，该实例从给定源读取样式表。

- **javax.xml.transform.stream.StreamSource 1.4**
  - `StreamSource(File f)`
  - `StreamSource(InputStream in)`
  - `StreamSource(Reader in)`
  - `StreamSource(String systemID)`  
    从文件、流、读取器或系统 ID（通常是相对或绝对 URL）构造一个流源。

- **javax.xml.transform.sax.SAXSource 1.4**
  - `SAXSource(XMLReader reader, InputSource source)`  
    构造一个 SAX 源，它从给定输入源获取数据，并使用给定读取器解析输入。

| org.xml.sax.XMLReader 1.4 |  |
|---|---|
| `void setContentHandler(ContentHandler handler)` | 设置一个处理程序，在解析输入时它会收到解析事件通知。 |
| `void parse(InputSource source)` | 解析来自给定输入源的输入，并将解析事件发送到内容处理程序。 |

| javax.xml.transform.dom.DOMResult 1.4 |  |
|---|---|
| `DOMResult(Node n)` | 从给定节点构造一个结果。通常，n 是一个新的文档节点。 |

| org.xml.sax.helpers.AttributesImpl 1.4 |  |
|---|---|
| `void addAttribute(String uri, String lname, String qname, String type, String value)` | 向此属性集合添加一个属性。<br><br>_参数：_<br>`uri` — 命名空间的 URI<br>`lname` — 不带前缀的本地名称<br>`qname` — 带前缀的限定名称<br>`type` — 类型，取值为 "CDATA"、"ID"、"IDREF"、"IDREFS"、"NMTOKEN"、"NMTOKENS"、"ENTITY"、"ENTITIES" 或 "NOTATION" 之一<br>`value` — 属性值 |
| `void clear()` | 从此属性集合中移除所有属性。 |

这个示例结束了我们对 Java 库中 XML 支持的讨论。现在，你应该对 XML 的主要优势有了良好的认识——特别是用于自动解析和验证，以及作为一种强大的转换机制。当然，只有当你很好地设计 XML 格式时，所有这些技术才会为你发挥作用。你需要确保这些格式足够丰富，能够表达你所有的业务需求，确保它们长期稳定，并确保你的业务合作伙伴愿意接受你的 XML 文档。这些问题可能比处理解析器、DTD 或转换更具挑战性。

在下一章中，我们将讨论 Java 平台上的网络编程，从网络套接字的基础知识开始，然后转向用于电子邮件和万维网的更高级协议。
