

```java
case Node.ENTITY_NODE:
    return "ENTITY_NODE";
case Node.TEXT_NODE:
    return "TEXT_NODE";
default:
    return "Unknown";
}

private void parseXML( Document document ) {
Element element = document.getDocumentElement();
List<Element> elements =
XMLUtility.getAllElements( element, "empty" );
System.out.println( "Element: " + elements.get( 0 ).getNodeName() );
List<Element> shorthand =
XMLUtility.getAllElements( element, "shorthand" );
System.out.println( "Element: " + shorthand.get( 0 ).getNodeName() );
List<Element> text = XMLUtility.getAllElements( element, "text" );
System.out.println( "Text: " + text.get( 0 ).getTextContent() );
List<Element> nested = XMLUtility.getAllElements( element, "nested" );
System.out.println( "Element: " + nested.get( 0 ).getNodeName() );
List<Element> elementChildren =
XMLUtility.getElements( element, "child" );
System.out.println( "Get-Child-Count: " + elementChildren.size() );
List<Element> child =
XMLUtility.getElements( nested.get( 0 ), "child" );
System.out.println( "Get-Child-Count: " + child.size() );
List<Element> allChildren =
XMLUtility.getAllElements( element, "child" );
System.out.println( "Get-AllChild-Count: " + allChildren.size() );
List<Element> nestedText =
XMLUtility.getElements( element, "nested-text" );
System.out.println( "nested-text: " +
nestedText.get( 0 ).getTextContent() );
List<Element> nestedChild =
XMLUtility.getElements( nestedText.get( 0 ), "child" );
System.out.println( "nested-text: " +
nestedChild.get( 0 ).getNodeName() );
List<Element> attributes =
    XMLUtility.getElements( element, "attributes" );
Element attrElement = attributes.get( 0 );
System.out.println(
    "attr1: " + attrElement.getAttribute( "attr1" ) );
System.out.println(
    "attr2: " + attrElement.getAttribute( "attr2" ) );
List<Element> specialChars =
    XMLUtility.getElements( element, "special-chars" );
System.out.println( "special-chars: " +
    specialChars.get( 0 ).getTextContent() );
List<Element> cdata = XMLUtility.getElements( element, "cdata" );
System.out.println( "cdata: " + cdata.get( 0 ).getTextContent() );
}
public static void main( String[] args ) {
    new LoadXMLExample().loadFile();
}
}
```

关于使用 XML 文件的内容已经介绍了很多，如果你觉得还不够扎实，也不用担心。在第 16 章“工具”和第 17 章“太空岩石”中，完整的游戏将从类路径上的归档文件中提取的 XML 文件创建和加载多边形。所以坚持住。如果游戏编程很容易，每个人都会做它。:-)

## 资源与进一步阅读

- Roubtsov, Vladimir，“智能加载属性”，2003 年，http://www.javaworld.com/javaqa/2003-08/01-qa-0808-property.html.
- “文档对象模型”，1995 年，http://docs.oracle.com/javase/tutorial/jaxp/dom/index.html.
- “如何使用 JAR 文件”，1995 年，http://docs.oracle.com/javase/tutorial/deployment/jar/basicsindex.html.

## 第 10 章

![](img/588a4cda8f2acae94a7e1987bf99400d_275_0.png)

### 图像

Java 提供了多种创建图像的方法。较常见的有 ImageIcon、BufferedImage 和 VolatileImage。还有其他格式和类，但就本书而言，仅涵盖 BufferedImage 和 VolatileImage。此外，由于该语言已存在很长时间并在多种操作系统上运行，某些图像格式仅用于向后兼容，不应用于新开发。尽管并非全部都需要，但熟悉所有不同选项是件好事。

### 在 Java 中了解颜色

在了解不同的图像格式之前，首先要了解 Java 如何表示颜色。Java 中的颜色由红、绿、蓝分量组成，还有一个可选的 alpha 分量，用于透明度。颜色可以使用 0.0f 到 1.0f 的浮点值创建，其中 0.0f 表示没有该颜色分量，1.0f 表示该分量最亮。无论使用何种方法创建颜色，每种颜色都由一个单一值组成，红、绿、蓝和 alpha 值以一定数量的位表示。每种颜色的位组合在一起形成一个 32 位的单一值。但这个值只是在绘制到图像之前的颜色表示。最终，决定颜色的是目标图像的格式。这些不同的格式将在本章后面介绍。

```
Color( float r, float g, float b )
Color( float r, float g, float b, float a )
```

前面的方法使用给定的红、绿、蓝和可选 alpha 值构造颜色，该值控制对象的透明度。如果未提供 alpha 值，则将其设置为 1.0f，表示完全不透明的值（无透明度）。

还有使用 0-255 整数值的构造函数。0-255 的值表示用于表示颜色的四个字节之一。这些方法构造颜色的方式与浮点版本相同。

```
Color( int r, int g, int b )
Color( int r, int g, int b, int a )
```

另一个构造函数接受一个单一整数。这个单一值包含每个颜色分量的 (r, g, b, a) 分量，通过按位或操作组合成一个单一值。

```
Color( int rgb )
```

alpha 值默认为 255（十六进制表示为 0xFF）。颜色通过将每个整数值移位到正确位置来构造。

```
int rgba = 0xFF << 24 | r << 16 | g << 8 | b;
```

另一种思考这个值的方式如下：

```
0xAARRGGBB
```

其中每对字母表示该颜色的相应字节。

```
Color( int rgb, boolean hasAlpha )
```

此构造函数允许使用不同的 alpha 值来生成透明度。

### 探索不同的图像类型

了解 Java 如何表示颜色只是拼图的一部分。当构造颜色并使用 Graphics 对象将其绘制到图像上时，最终决定写入图像的颜色格式的是目标图像的颜色格式。

BufferedImage 类支持多种图像类型。下面的列表简要描述了 BufferedImage 类支持的不同图像格式。

- TYPE_BYTE_BINARY—1 位、2 位或 4 位图像，使用 IndexColorModel 来选择适当的颜色值。
- TYPE_BYTE_GRAY—每种颜色表示为从 0（黑色）到 255（白色）的单个字节。
- TYPE_BYTE_INDEXED—每个字节值都是一个索引，指向包含 Web 安全颜色和灰度值的 256 个值的颜色数组。
- TYPE_CUSTOM—未知类型使用此值作为图像类型。
- TYPE_3BYTE_BGR—每三个字节一组表示一种颜色，其中索引 0 是蓝色，索引 1 是绿色，索引 2 是红色。
- TYPE_4BYTE_ABGR—每四个字节一组表示一种颜色，其中索引 0 是 alpha，索引 1 是蓝色，索引 2 是绿色，索引 3 是红色。
- TYPE_4BYTE_ABGR_PRE—这与前一种类型相同，但所有颜色在存储前都已按 alpha 值预乘。
- TYPE_USHORT_555_RGB—表示每种颜色五位、打包为 16 位值且无 alpha 值的图像。参见图 10.1。
- TYPE_USHORT_565_RGB—红色和蓝色分量各五位、绿色六位且无 alpha 值。参见图 10.2。
- TYPE_USHORT_GRAY—与 8 位灰度图像相同，高八位未使用。
- TYPE_INT_BGR—格式为 0x00BBGRR 且无 alpha 值的整数。
- TYPE_INT_RGB—格式为 0x00RRGGBB 且无 alpha 值的整数。
- TYPE_INT_ARGB—格式为 0xAARRGGBB 且 alpha 值未与 RGB 颜色值预乘的整数。
- TYPE_INT_ARGB_PRE—格式为 0xAARRGGBB 且 alpha 值已与 RGB 颜色值预乘的整数。

![](img/588a4cda8f2acae94a7e1987bf99400d_277_0.png)

图 10.1 555 无符号短整型颜色。© 2014 Timothy Wright.

