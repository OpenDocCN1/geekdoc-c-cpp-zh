We don’t need to go into details about SVG; for our purposes, we just need to know how to express a set of colored rectangles. Here is a sample:

```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 20000802//EN"
  "http://www.w3.org/Graphics/SVG/20000802/DTD/svg-20000802.dtd">
<svg xmlns="http://www.w3.org/2000/svg" width="150" height="150">
  <rect x="231" y="61" width="9" height="12" fill="#6e4a13"/>
  <rect x="107" y="106" width="5" height="5" fill="#c406eb"/>
  ...
</svg>
```
```

As you can see, each rectangle is described as a rect node. The position, width, height, and fill color are attributes. The fill color is an RGB value in hexadecimal.

![](bbox=[0.194, 0.409, 0.234, 0.441])

> > **NOTE:** SVG uses attributes heavily. In fact, some attributes are quite complex. For example, here is a path element:

```
```xml
<path d="M 100 100 L 300 100 L 200 300 Z"/>
```
```

> > The M denotes a “moveto” command, L is “lineto,” and z is “closepath” (!). Apparently, the designers of this data format didn’t have much confidence in using XML for structured data. In your own XML formats, you might want to use elements instead of complex attributes.

# 3.9 XSL Transformations

The XSL Transformations (XSLT) mechanism allows you to specify rules for transforming XML documents into other formats, such as plain text, XHTML, or any other XML format. XSLT is commonly used to translate from one machine-readable XML format to another, or to translate XML into a presentation format for human consumption.

You need to provide an XSLT stylesheet that describes the conversion of XML documents into some other format. An XSLT processor reads an XML document and the stylesheet and produces the desired output (see Figure 3.4).

The XSLT specification is quite complex, and entire books have been written on the subject. We can’t possibly discuss all the features of XSLT, so we will just work through a representative example. You can find more information in the book *Essential XML* by Don Box et al. The XSLT specification is available at www.w3.org/TR/xslt.