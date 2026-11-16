
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

There was a lot of information covered about using XML files, and if you don't feel like everything is solid, do not worry. In Chapters 16, “Tools,” and 17, “Space Rocks,” the complete game will create and load polygons using XML files pulled from archive files located on the classpath. So hang in there. If game programming was easy, everyone would do it. :-)

## RESOURCES AND FURTHER READING

- Roubtsov, Vladimir, “Smartly Load Your Properties,” 2003, http://www.javaworld.com/javaqa/2003-08/01-qa-0808-property.html.
- “Document Object Model,” 1995, http://docs.oracle.com/javase/tutorial/jaxp/dom/index.html.
- “How to Use JAR Files,” 1995, http://docs.oracle.com/javase/tutorial/deployment/jar/basicsindex.html.

## CHAPTER 10

![](img/588a4cda8f2acae94a7e1987bf99400d_275_0.png)

### IMAGES

Java has a variety of methods for creating images. Some of the more common are ImageIcon, BufferedImage, and VolatileImage. There are other formats and other classes, but for the purposes of this book, BufferedImage and VolatileImage are all that are covered. Also, because the language has been around a long time and works on multiple operating systems, some of the image formats are only available for backward compatibility, and should not be used for new development. Even though they are not all needed, it is good to be familiar with all the different options.

### LEARNING ABOUT COLORS IN JAVA

Before understanding the different formats for images, it is important to understand how Java represents colors. Colors in Java consist of red, green, and blue components, with an optional alpha component that is used for transparency. Colors can be created using floating-point values from 0.0f to 1.0f, where 0.0f is no color component at all, and 1.0f is the brightest of that component. Each color, regardless of the method used to create it, consists of a single value, with red, green, blue, and alpha values represented as a certain number of bits. Together, the bits of each color are combined to form a single value of 32 bits. But this value is only the representation of the color before it is drawn to an image. Ultimately, it is the format of the destination image that determines the color. These different formats are covered later in the chapter.

```
Color( float r, float g, float b )
Color( float r, float g, float b, float a )
```

The previous methods construct a color with the given red, green, blue, and optional alpha value, which controls the transparency of the object. If the alpha value is not supplied, it is set to 1.0f, which represents a completely opaque value (no transparency).

There are also constructors using integer values from 0-255. The 0-255 values represent one of the four bytes available to represent the color. These methods construct a color the same as the floating-point versions.

```
Color( int r, int g, int b )
Color( int r, int g, int b, int a )
```

Another constructor takes a single integer. This single value contains the (r, g, b, a) components of each color component or-ed together into a single value.

```
Color( int rgb )
```

The alpha value is defaulted to 255 (0xFF in hexadecimal representation). The color is constructed by shifting each integer value into the correct position.

```
int rgba = 0xFF << 24 | r << 16 | g << 8 | b;
```

Another way to think of this value is the following:

```
0xAARRGGBB
```

where each pair of letters represents that color's corresponding byte.

```
Color( int rgb, boolean hasAlpha )
```

This constructor allows a different alpha value to be used to produce transparency.

### EXPLORING DIFFERENT IMAGE TYPES

Understanding how Java represents color is only part of the puzzle. When a color is constructed, and is drawn onto an image with a Graphics object, it is the color format of the destination image that ultimately determines the color format written to the image.

The BufferedImage class supports a wide variety of image types. The following list briefly describes the different image formats supported by the BufferedImage class.

- TYPE_BYTE_BINARY—1-, 2-, or 4-bit image with an IndexColorModel used to select the appropriate color values.
- TYPE_BYTE_GRAY—Each color is represented as a single byte from 0 (black) to 255 (white).
- TYPE_BYTE_INDEXED—Each byte value is an index into a 256 value array of colors containing web-safe colors and gray values.
- TYPE_CUSTOM—Unknown types use this value for the image type.
- TYPE_3BYTE_BGR—Each three byte group represents a color, where index 0 is blue, index 1 is green, and index 2 is red.
- TYPE_4BYTE_ABGR—Each four byte group represents a color, where index 0 is alpha, index 1 is blue, index 2 is green, and index 3 is red.
- TYPE_4BYTE_ABGR_PRE—This is the same as the previous type, but all the colors have been pre-multiplied by the alpha value before being stored.
- TYPE_USHORT_555_RGB—Represents an image with five bits for each color, packed into a 16-bit value, with no alpha value. See Figure 10.1.
- TYPE_USHORT_565_RGB—Five bits for each red and blue component, and 6 bits for green, with no alpha value. See Figure 10.2.
- TYPE_USHORT_GRAY—Same as an 8-bit gray-scale image, with the upper eight bits unused.
- TYPE_INT_BGR—Integer with the format 0x00BBGRR with no alpha value.
- TYPE_INT_RGB—Integer with the format 0x00RRGGBB with no alpha value.
- TYPE_INT_ARGB—Integer with the format 0xAARRGGBB where the alpha value has not been pre-multiplied with the RGB color values.
- TYPE_INT_ARGB_PRE—Integer with the format 0xAARRGGBB where the alpha value has been pre-multiplied with the RGB color values.

![](img/588a4cda8f2acae94a7e1987bf99400d_277_0.png)

Figure 10.1 555 Unsigned Short Color. © 2014 Timothy Wright.
