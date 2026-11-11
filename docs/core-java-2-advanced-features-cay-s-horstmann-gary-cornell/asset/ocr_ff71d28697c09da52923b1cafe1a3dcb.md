```
handler.endElement("", rootElement, rootElement);
handler.endDocument();
```

The SAXSource for the transformer is constructed from the XML reader:

```
t.transform(new SAXSource(new EmployeeReader()),
            new InputSource(new FileInputStream(filename)), result);
```

This is an ingenious trick to convert non-XML legacy data into XML. Of course,
most XSLT applications will already have XML input data, and you can simply
invoke the transform method on a StreamSource:

```
t.transform(new StreamSource(file), result);
```

The transformation result is an object of a class that implements the Result interface.
The Java library supplies three classes:

+   - DOMResult
+   - SAXResult
+   - StreamResult

To store the result in a DOM tree, use a DocumentBuilder to generate a new document
node and wrap it into a DOMResult:

```
Document doc = builder.newDocument();
t.transform(new DOMResult(doc));
```

To save the output in a file, use a StreamResult:

```
t.transform(source, new StreamResult(file));
```

Listing 3.15 contains the complete source code.

# Listing 3.13  transform/makethtml.xsl

```
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
```

(Continues)