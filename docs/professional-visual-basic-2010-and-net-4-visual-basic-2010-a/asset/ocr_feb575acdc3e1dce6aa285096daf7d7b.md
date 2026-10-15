external references are encountered when a document is transformed (the method, Transform, is executed). The System.Xml namespace contains a class, XmlUrlResolver, which is derived from XmlResolver. The XmlUrlResolver class resolves the external resource based on a URI.

Load — This overloaded method loads an XSLT style sheet to be used in transforming XML documents. It is permissible to specify the XSLT style sheet as a parameter of type XPathNavigator, filename of an XSLT file (specified as parameter type String), XmlReader, or IXPathNavigable. For each type of XSLT supported, an overloaded member is provided that enables an XmlResolver to also be specified. For example, it is possible to call Load(String, XsltSettings, XmlResolver), where String corresponds to a filename, XsltSettings is an object that contains settings to affect the transformation, and XmlResolver is an object that handles references in the style sheet of type xsl:import and xsl:include. It would also be permissible to pass in a value of Nothing for the third parameter of the Load method (so that no XmlResolver would be specified).

Transform — This overloaded method transforms a specified XML document using the previously specified XSLT style sheet. The location where the transformed XML is to be output is specified as a parameter to this method. The first parameter of each overloaded method is the XML document to be transformed. The most straightforward variant of the Transform method is Transform(String, String). In this case, a file containing an XML document is specified as the first parameter, and a filename that receives the transformed XML document is specified as the second. This is exactly how the first XSLT example utilized the Transform method:

```
myXslTransform.Transform("..\FilmOrders.xml", destFileName)
```

The first parameter to the Transform method can also be specified as IXPathNavigable or XmlReader. The XML output can be sent to an object of type Stream, TextWriter, or XmlWriter. In addition, a parameter containing an object of type XsltArgumentList can be specified. An XsltArgumentList object contains a list of arguments that are used as input to the transform. These may be used within the XSLT file to affect the output.

# XSLT Transforming between XML Standards

The first example used four XSLT elements to transform an XML file into an HTML file. Such an example has merit, but it doesn’t demonstrate an important use of XSLT: transforming XML from one standard into another standard. This may involve renaming elements/attributes, excluding elements/attributes, changing data types, altering the node hierarchy, and representing elements as attributes, and vice versa.

Returning to the example, a case of differing XML standards could easily affect your software that automates movie orders coming into a supplier. Imagine that the software, including its XML representation of a movie order, is so successful that you sell 100,000 copies. However, just as you are celebrating, a consortium of the largest movie supplier chains announces that they are no longer accepting faxed orders and that they are introducing their own standard for the exchange of movie orders between movie sellers and buyers.

Rather than panic, you simply ship an upgrade that includes an XSLT file. This upgrade (a bit of extra code plus the XSLT file) transforms your XML representation of a movie order into the XML representation dictated by the consortium of movie suppliers. Using an XSLT file enables you to ship the upgrade immediately. If the consortium of movie suppliers revises their XML representation, then you are not obliged to change your source code. Instead, you can simply ship the upgraded XSLT file that ensures each movie order document is compliant.

The specific source code that executes the transform is as follows:

```
Dim xslt As New XslCompiledTransform
Dim outputFile As String = "..\..\output.html"

xslt.Load("..\..\displayorders.xslt")
xslt.Transform("..\..\filmorama.xml", outputFile)
```