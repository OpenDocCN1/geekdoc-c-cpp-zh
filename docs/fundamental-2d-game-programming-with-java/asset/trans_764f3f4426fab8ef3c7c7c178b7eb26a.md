

```java
public void createXMLFile() {
    File file = new File( "sample.xml" );
    PrintWriter out = null;
    try {
        out = new PrintWriter( file );
        writeXML( out );
    } catch( FileNotFoundException fex ) {
        fex.printStackTrace();
    } finally {
        try {
            out.close();
            System.out.println( "Wrote: " + file.getPath() );
        } catch( Exception e ) { }
    }
}

private void writeXML( PrintWriter out ) {
    out.println( "<?xml version=\"1.0\" encoding=\"UTF-8\" ?>" );
    // all XML must have a single root tag
    out.println( "<root>" );
    // a comment
    out.println( " <!-- This is a comment -->" );
    // and empty tag
    out.println( " <empty></empty>" );
    // shorthand for a tag with no children
    out.println( " <shorthand/>" );
    // text element
    out.println( " <text>I'm some text</text>" );
    // nested elements
    out.println( " <nested><child/></nested>" );
    // nested text with child
    out.println( " <nested-text>I'm some text <child/></nested-text>" );
    // attributes
    out.println( " <attributes attr1=\"value1\" attr2=\"value2\" />" );
    // special characters
    out.println(
        "<special-chars> &lt; &gt; &amp; &apos;" +
        "&quot; </special-chars>" );
    // unparsed character data CDATA
    out.println( " <cdata>" );
    // Starting CDATA tag
    out.println( " <![CDATA[" );
    out.println( "<xml><attr=\"xml inside xml\"/></xml>" );
    // Ending CDATA tag
    out.println( " ]]>" );
    out.println( " </cdata>" );
    // ending root tag
    out.println( " </root>" );
}

public static void main( String[] args ) {
    new SaveXMLExample().createXMLFile();
}
```

编写 XML 文件比解析它们容易得多。幸运的是，加载游戏数据不需要 XML 规范中那些真正复杂且令人困惑的部分。

XMLUtility 类已添加到 javagames.util 包中，包含一些用于解析 XML 文件的辅助方法。parseDocument() 方法接受 InputStream 或 Reader，并返回一个包含整个 XML 文件（在内存中）的 Document 对象。getElements() 和 getAllElements() 方法返回具有给定标签名的元素。区别在于，getElements() 方法仅搜索一层标签，而 getAllElements() 返回文档中任何位置具有给定名称的所有标签。

```java
package javagames.util;
import java.io.*;
import java.util.*;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import org.xml.sax.*;
```

```java
public class XMLUtility {
    public static Document parseDocument( InputStream inputStream )
            throws ParserConfigurationException, SAXException, IOException {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        Document document = builder.parse( new InputSource( inputStream ) );
        return document;
    }

    public static Document parseDocument( Reader reader )
            throws ParserConfigurationException, SAXException, IOException {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        Document document = builder.parse( new InputSource( reader ) );
        return document;
    }

    public static List<Element> getAllElements(
            Element element, String tagName ) {
        ArrayList<Element> elements = new ArrayList<Element>();
        NodeList nodes = element.getElementsByTagName( tagName );
        for( int i = 0; i < nodes.getLength(); i++ ) {
            elements.add( (Element)nodes.item( i ) );
        }
        return elements;
    }

    public static List<Element> getElements(
            Element element, String tagName ) {
        ArrayList<Element> elements = new ArrayList<Element>();
        NodeList children = element.getChildNodes();
        for( int i = 0; i < children.getLength(); i++ ) {
            Node node = children.item( i );
            if( node.getNodeType() == Node.ELEMENT_NODE ) {
                String nodeName = node.getNodeName();
                if( nodeName != null && nodeName.equals( tagName ) ) {
                    elements.add( (Element)node );
                }
            }
        }
        return elements;
    }
}
```

位于 javagames.filesandres 包中的 LoadXMLExample 代码解析了前一个示例中的 sample.xml 文件。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<root>
<!-- This is a comment -->
<empty/></empty>
<shorthand/>
<text>I'm some text</text>
<nested><child/></nested>
<nested-text>I'm some text <child/></nested-text>
<attributes attr1="value1" attr2="value2" />
<special-chars>&lt; &gt; &amp; &apos; &quot; </special-chars>
<cdata>
<![CDATA[
<xml><attr="xml inside xml"/></xml>
]]>
</cdata>
</root>
```

处理文档时需要采用递归方法，因为 XML 标签可以包含其他标签。在不知道文档结构的情况下检查文档时，您将使用以下模式：

```java
// LoadXMLExample.java
private void inspectXML( Node node ) {
  printNode( node );
  if( node.hasAttributes() ) {
    NamedNodeMap nodeMap = node.getAttributes();
    for( int i = 0; i < nodeMap.getLength(); ++i ) {
      inspectXML( nodeMap.item( i ) );
    }
  }
  if( node.hasChildNodes() ) {
    NodeList nodeList = node.getChildNodes();
    for( int i = 0; i < nodeList.getLength(); ++i ) {
      inspectXML( nodeList.item( i ) );
    }
  }
}
```

将打印每个节点的类型、名称和值。然后使用相同的函数递归处理任何属性。对任何子元素也执行相同操作。parseXML() 方法使用 XMLUtility 类通过标签名提取每个元素。

以下方法从每个元素中获取所需信息：

- Element.getNodeName()—返回 XML 标签的名称。
- Element.getTextContent()—返回开始标签和结束标签之间的文本值。
- Element.getAttribute(String name)—给定属性名称，此方法返回属性值；如果属性不可用，则返回 null。

请注意尝试获取 “child” 标签的部分。有两个不同的元素具有该标签名，但根据使用的检索方法不同，可能返回零个、一个或两个标签。有时您希望检索具有特定名称的所有标签，但有时所有元素都有同名标签（例如 <name>），而您只想获取当前元素的标签。同时使用工具类中的 getElements() 和 getAllElements() 方法即可实现此目的。

```java
package javagames.filesandres;

import java.io.*;
import java.util.List;
import org.w3c.dom.*;
import org.xml.sax.*;
import javagames.util.*;
import javax.xml.parsers.ParserConfigurationException;

public class LoadXMLExample {
    public LoadXMLExample() {
    }

    public void loadFile() {
        InputStream in = null;
        try {
            in = ResourceLoader.load( LoadXMLExample.class, "sample.xml",
                    "/sample/xml" );
            Document document = XMLUtility.parseDocument( in );
            System.out.println( "*************" );
            System.out.println( "* INSPECT*" );
            inspectXML( document );
            System.out.println( "*************" );
            System.out.println( "* PARSE*" );
            parseXML( document );
        } catch( ParserConfigurationException pex ) {
            System.out.println( "ParserConfigurationException" );
            pex.printStackTrace();
        } catch( SAXException ex ) {
            System.out.println( "SAXException" );
            ex.printStackTrace();
        } catch( IOException ex ) {
            System.out.println( "IOException" );
            ex.printStackTrace();
        } finally {
            try {
                in.close();
            } catch (IOException ex) {
            }
        }
    }

    private void inspectXML( Node node ) {
        printNode( node );
        if( node.hasAttributes() ) {
            NamedNodeMap nodeMap = node.getAttributes();
            for( int i = 0; i < nodeMap.getLength(); ++i ) {
                inspectXML( nodeMap.item( i ) );
            }
        }
        if( node.hasChildNodes() ) {
            NodeList nodeList = node.getChildNodes();
            for( int i = 0; i < nodeList.getLength(); ++i ) {
                inspectXML( nodeList.item( i ) );
            }
        }
    }

    private void printNode( Node node ) {
        System.out.print( "Type: " + getNodeType( node ) );
        System.out.print( ", Name: " + node.getNodeName() );
        String value = node.getNodeValue() == null ?
                "\"" : node.getNodeValue().trim();
        System.out.println( ", Value: \"" + value + "\"" );
    }

    private String getNodeType( Node node ) {
        switch( node.getNodeType() ) {
        case Node.ATTRIBUTE_NODE:
            return "ATTRIBUTE_NODE";
        case Node.CDATA_SECTION_NODE:
            return "CDATA_SECTION_NODE";
        case Node.COMMENT_NODE:
            return "COMMENT_NODE";
        case Node.DOCUMENT_NODE:
            return "DOCUMENT_NODE";
        case Node.ELEMENT_NODE:
            return "ELEMENT_NODE";
        }
    }
}
```

