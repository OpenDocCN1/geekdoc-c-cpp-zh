
## 清单 3.7（续）

```java
/**
 * This program demonstrates how to use a SAX parser. The program prints all
 * hyperlinks of an XHTML web page. <br>
 * Usage: java SAXTest URL
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */
public class SAXTest
{
   public static void main(String[] args) throws Exception
   {
      String url;
      if (args.length == 0)
      {
         url = "http://www.w3.org";
         System.out.println("Using " + url);
      }
      else url = args[0];

      var handler = new DefaultHandler()
      {
         public void startElement(String namespaceURI, String lname,
               String qname, Attributes attrs)
         {
            if (lname.equals("a") && attrs != null)
            {
               for (int i = 0; i < attrs.getLength(); i++)
               {
                  String aname = attrs.getLocalName(i);
                  if (aname.equals("href"))
                     System.out.println(attrs.getValue(i));
               }
            }
         }
      };

      SAXParserFactory factory = SAXParserFactory.newInstance();
      factory.setNamespaceAware(true);
      factory.setFeature(
            "http://apache.org/xml/features/nonvalidating/load-external-dtd",
            false);
      SAXParser saxParser = factory.newSAXParser();
      InputStream in = new URL(url).openStream();
      saxParser.parse(in, handler);
   }
}
```

## javax.xml.parsers.SAXParserFactory 1.4

- `static SAXParserFactory newInstance()`  
  返回 SAXParserFactory 类的实例。
- `SAXParser newSAXParser()`  
  返回 SAXParser 类的实例。
- `boolean isNamespaceAware()`
- `void setNamespaceAware(boolean value)`  
  获取或设置工厂的 namespaceAware 属性。如果设置为 `true`，则该工厂生成的解析器是命名空间感知的。
- `boolean isValidating()`
- `void setValidating(boolean value)`  
  获取或设置工厂的 validating 属性。如果设置为 `true`，则该工厂生成的解析器会验证其输入。

## javax.xml.parsers.SAXParser 1.4

- `void parse(File f, DefaultHandler handler)`
- `void parse(String uri, DefaultHandler handler)`
- `void parse(InputStream in, DefaultHandler handler)`  
  从给定文件、URL 或输入流解析 XML 文档，并将解析事件报告给给定的处理器。

## org.xml.sax.ContentHandler 1.4

- `void startDocument()`
- `void endDocument()`  
  在文档开始或结束时被调用。
- `void startElement(String uri, String lname, String qname, Attributes attr)`
- `void endElement(String uri, String lname, String qname)`  
  在元素开始或结束时被调用。如果解析器是命名空间感知的，它会报告命名空间的 URI、不带前缀的本地名称以及带前缀的限定名称。
- `void characters(char[] data, int start, int length)`  
  当解析器报告字符数据时被调用。

## org.xml.sax.Attributes 1.4

- `int getLength()`  
  返回此属性集合中存储的属性数量。
- `String getLocalName(int index)`  
  返回给定索引处属性的本地名称（不带前缀）；如果解析器不是命名空间感知的，则返回空字符串。
- `String getURI(int index)`  
  返回给定索引处属性的命名空间 URI；如果节点不属于命名空间，或解析器不是命名空间感知的，则返回空字符串。
- `String getQName(int index)`  
  返回给定索引处属性的限定名称（带前缀）；如果解析器不报告限定名称，则返回空字符串。
- `String getValue(int index)`
- `String getValue(String qname)`
- `String getValue(String uri, String lname)`  
  从给定索引、限定名称或命名空间 URI + 本地名称返回属性值。如果值不存在，则返回 `null`。

## 3.7.2 使用 StAX 解析器

StAX 解析器是一种“拉式解析器”。无需安装事件处理器，只需使用以下基本循环遍历事件：

```
InputStream in = url.openStream();
XMLInputFactory factory = XMLInputFactory.newInstance();
XMLStreamReader parser = factory.createXMLStreamReader(in);
while (parser.hasNext())
{
    int event = parser.next();
    Call parser methods to obtain event details
}
```

例如，解析以下片段时

```xml
<font>
    <name>Helvetica</name>
    <size units="pt">36</size>
</font>
```

解析器会产生以下事件：

1. START_ELEMENT，元素名称：font
2. CHARACTERS，内容：空白
3. START_ELEMENT，元素名称：name
4. CHARACTERS，内容：Helvetica
5. END_ELEMENT，元素名称：name
6. CHARACTERS，内容：空白
7. START_ELEMENT，元素名称：size
8. CHARACTERS，内容：36
9. END_ELEMENT，元素名称：size
10. CHARACTERS，内容：空白
11. END_ELEMENT，元素名称：font

要分析属性值，请调用 `XMLStreamReader` 类的相应方法。例如，

```java
String units = parser.getAttributeValue(null, "units");
```

获取当前元素的 `units` 属性。

默认情况下，命名空间处理是启用的。你可以通过修改工厂来停用它：

```java
XMLInputFactory factory = XMLInputFactory.newInstance();
factory.setProperty(XMLInputFactory.IS_NAMESPACE_AWARE, false);
```

清单 3.8 包含使用 StAX 解析器实现的 Web 爬虫程序代码。如你所见，该代码比等效的 SAX 代码更简单，因为你不必担心事件处理。

## 清单 3.8 stax/StAXTest.java

```java
package stax;

import java.io.*;
import java.net.*;
import javax.xml.stream.*;

/**
 * This program demonstrates how to use a StAX parser. The program prints all
 * hyperlinks of an HTML web page. <br>
 * Usage: java stax.StAXTest URL
 * @author Cay Horstmann
 * @version 1.1 2018-05-01
 */
public class StAXTest
{
  public static void main(String[] args) throws Exception
  {
    String urlString;
    if (args.length == 0)
    {
      urlString = "http://www.w3.org";
      System.out.println("Using " + urlString);
    }
    else urlString = args[0];
    var url = new URL(urlString);
    InputStream in = url.openStream();
    XMLInputFactory factory = XMLInputFactory.newInstance();
    XMLStreamReader parser = factory.createXMLStreamReader(in);
    while (parser.hasNext())
    {
      int event = parser.next();
      if (event == XMLStreamConstants.START_ELEMENT)
      {
        if (parser.getLocalName().equals("a"))
        {
          String href = parser.getAttributeValue(null, "href");
          if (href != null)
            System.out.println(href);
        }
      }
    }
  }
}
```

## javax.xml.stream.XMLInputFactory 6

- `static XMLInputFactory newInstance()`  
  返回 XMLInputFactory 类的实例。
- `void setProperty(String name, Object value)`  
  为此工厂设置属性；如果该属性不受支持或无法设置为给定值，则抛出 `IllegalArgumentException`。JDK 实现支持以下布尔值属性：

| 属性 | 描述 |
| --- | --- |
| `"javax.xml.stream.isValidating"` | 当为 `false`（默认值）时，不验证文档。规范未要求。 |
| `"javax.xml.stream.isNamespaceAware"` | 当为 `true`（默认值）时，处理命名空间。规范未要求。 |
| `"javax.xml.stream.isCoalescing"` | 当为 `false`（默认值）时，相邻字符数据不合并。 |
| `"javax.xml.stream.isReplacingEntityReferences"` | 当为 `true`（默认值）时，实体引用被替换并作为字符数据报告。 |
| `"javax.xml.stream.isSupportingExternalEntities"` | 当为 `true`（默认值）时，解析外部实体。规范未为此属性提供默认值。 |
| `"javax.xml.stream.supportDTD"` | 当为 `true`（默认值）时，DTD 作为事件报告。 |

- `XMLStreamReader createXMLStreamReader(InputStream in)`
- `XMLStreamReader createXMLStreamReader(InputStream in, String characterEncoding)`
- `XMLStreamReader createXMLStreamReader(Reader in)`
- `XMLStreamReader createXMLStreamReader(Source in)`  
  创建一个从给定流、读取器或 JAXP 源读取的解析器。

## javax.xml.stream.XMLStreamReader 6

- `boolean hasNext()`  
  如果还有另一个解析事件，则返回 `true`。
- `int next()`  
  将解析器状态设置为下一个解析事件，并返回以下常量之一：START_ELEMENT、END_ELEMENT、CHARACTERS、START_DOCUMENT、END_DOCUMENT、CDATA、COMMENT、SPACE（可忽略的空白）、PROCESSING_INSTRUCTION、ENTITY_REFERENCE、DTD。
- `boolean isStartElement()`
- `boolean isEndElement()`
- `boolean isCharacters()`
- `boolean isWhiteSpace()`  
  如果当前事件是开始元素、结束元素、字符数据或空白，则返回 `true`。

